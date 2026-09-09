# Prompt Injection Attack - Investigation and Response SOP

> **SOP Agent Instructions:** This SOP contains exactly **4 phases** and **2 tasks per phase** (8 tasks total). Generate the response plan with the following structure and no additional tasks or phases:
>
> Phase 1: **Detection and Analysis** — Task 1.1, Task 1.2
> Phase 2: **Containment** — Task 2.1, Task 2.2
> Phase 3: **Eradication** — Task 3.1, Task 3.2
> Phase 4: **Post-Incident Activity** — Task 4.1, Task 4.2

> **Overview:** This SOP guides security analysts through investigating and responding to findings related to a prompt injection attack against the MedAdvice patient-advice assistant. It applies to findings from the GenAI - Prompt Injection Attack Correlation detection set including instruction override, guardrail bypass, persona jailbreak, jailbreak mode, system prompt disclosure, and obfuscated payload. All containment actions run on the identity plane through the MedAdvice Identity Provider SOAR app. This SOP follows the NIST SP 800-61 Incident Response lifecycle.

## Detection and Analysis

### Task 1.1 — Build the injection attack timeline

Correlate this finding across all MedAdvice GenAI telemetry to identify which stage of the attack triggered the alert and whether it is part of a sustained campaign. Use the actor and the client address from the finding to search gen_ai_log across every application, model, and session the actor touched. The finding deliberately carries no prompt text, so this search is the only place the raw prompts are read, under the index-level access controls that apply to gen_ai_log.

```
index=gen_ai_log `exclude_scoring_sourcetypes` earliest=-24h
| eval actor=coalesce('gen_ai.user.id', 'enduser.id', 'client.address')
| eval src_ip='client.address'
| search actor="<USERNAME>" OR src_ip="<ATTACKER_IP>"
| eval stage=case(
    'gen_ai.policy.blocked'="true" AND prompt_category="prompt_injection", "Stage 1 - Injection blocked by policy",
    'gen_ai.guardrail.triggered'="true", "Stage 1 - Guardrail triggered",
    'gen_ai.policy.blocked'="true", "Stage 1 - Policy block (other category)",
    'gen_ai.prompt.is_anomaly'="true", "Stage 2 - Anomalous prompt allowed through",
    'gen_ai.safety.violated'="true", "Stage 3 - Safety violation in the response",
    'gen_ai.pii.detected'="true", "Stage 4 - PII/PHI returned to the actor",
    true(), "Context - " . 'gen_ai.app.name')
| table _time stage gen_ai.app.name gen_ai.request.model gen_ai.session.id actor src_ip risk_score
| sort 0 _time
```

### Task 1.2 — Assess risk score and scope

Query the risk index to determine the cumulative risk score for the actor and identify all contributing detections. The correlation rule contributes 80 to the user risk object and 60 to the source address on every fire. A score above 160 across more than one session or application indicates a sustained campaign rather than an isolated attempt and requires immediate escalation to Containment.

```
index=risk risk_object="<USERNAME>" earliest=-24h
| stats sum(risk_score) as total_risk_score
        count as risk_event_count
        values(source) as contributing_detections
        values(risk_message) as risk_messages
        by risk_object risk_object_type
| sort - total_risk_score
```

## Containment

### Task 2.1 — Disable the offending account and revoke its sessions

**Containment standard:** three or more blocked prompt-injection attempts within 24 hours from one actor, with no authorized-testing record for that actor, means the account is inactivated pending review. The finding's `injection_attempts` and `policy_blocks` counts are the evidence, and the note on this task is the review record. Validate intent with the actor's manager before proceeding: an authorized red-team or model-evaluation record makes this a Benign Positive.

If the standard is met, run the **MedAdvice Identity Provider -> disable user** SOAR action from this task's Actions panel with the username taken from the finding's `user` field and a reason naming this incident. Then run **MedAdvice Identity Provider -> clear user sessions** for the same username to invalidate any token issued before the account was inactivated. The Guided Response agent runs both from the prompt "Disable user \<USERNAME\>". Results are recorded on this task and on the investigation's Automation tab, and `enable user` on the same app reverses the change during Eradication.

The MedAdvice Identity Provider is a workshop simulator: every result carries `simulated: true` and no directory is touched. On a stack with no paired SOAR, run the adaptive response actions Suspend User (AI Defense) and Revoke Session / API Key instead; both are equally simulated and write their audit entry to gen_ai_log under sourcetype ai_cim:response:action. This task requires a note.

### Task 2.2 — Identify injection attempts that were not blocked

Search for prompts from this actor that Cisco AI Defense allowed through during the attack window. These are the guardrail gaps: they reached the model and produced a real response, and they determine whether the incident is contained or still ongoing. If this search returns any results, the incident cannot be dispositioned as benign and the guardrail identified here must be tightened during Eradication.

```
index=gen_ai_log `exclude_scoring_sourcetypes` earliest=-24h
    (gen_ai.user.id="<USERNAME>" OR enduser.id="<USERNAME>" OR client.address="<ATTACKER_IP>")
    gen_ai.policy.blocked="false"
| table _time gen_ai.session.id gen_ai.app.name gen_ai.request.model prompt_category
        gen_ai.prompt.is_anomaly gen_ai.safety.violated gen_ai.pii.detected gen_ai.pii.types
| sort 0 _time
```

## Eradication

### Task 3.1 — Close the guardrail gap for the observed technique

Tighten the Cisco AI Defense guardrail profile for the technique family recorded in the finding's `techniques` field so the same prompt pattern is blocked for every user, not just this actor. Run the adaptive response action Tighten Guardrail Policy scoped to the application named in the finding, and work with the AI platform owner to make the policy change permanent rather than incident-scoped. Record the policy name and version before and after in the task notes. Verify that every response action has been logged with the search below.

```
index=gen_ai_log sourcetype=ai_cim:response:action
    (target="<USERNAME>" OR target="<APP_NAME>")
| table _time action action_label target_type target status simulated executed_by search_name execution_id
| sort 0 _time
```

### Task 3.2 — Restore the account after credential hygiene

Confirm that no new activity has arrived from the actor for at least 15 minutes and that the guardrail change from Task 3.1 is live. If the actor is a legitimate user whose account was misused, reset the credentials and re-enroll MFA through a verified out-of-band channel, then re-activate the account with the **MedAdvice Identity Provider -> enable user** SOAR action, recording the justification in the task notes. If the actor is confirmed malicious, leave the account inactivated and record that decision instead.

## Post-Incident Activity

### Task 4.1 — Document the full incident timeline

Build a complete chronological record of every event from the first injection attempt through to the last containment action, and record the total time between them as the response latency in the investigation case notes. This search deliberately omits the `exclude_scoring_sourcetypes` macro so the response actions appear alongside the attack events in one timeline.

```
index=gen_ai_log earliest=-24h
| eval actor=coalesce('gen_ai.user.id', 'enduser.id', 'client.address', target)
| search actor="<USERNAME>" OR client.address="<ATTACKER_IP>"
| eval summary=case(
    sourcetype="ai_cim:response:action", "Response - " . action_label . " - " . status . " (simulated=" . simulated . ")",
    'gen_ai.policy.blocked'="true", "Blocked - " . 'gen_ai.policy.name' . " - " . prompt_category,
    'gen_ai.pii.detected'="true", "PII exposure - " . 'gen_ai.pii.types',
    'gen_ai.safety.violated'="true", "Safety violation - " . 'gen_ai.app.name',
    true(), "Allowed - " . 'gen_ai.app.name' . " - " . 'gen_ai.request.model')
| table _time sourcetype summary gen_ai.session.id actor
| sort 0 _time
```

### Task 4.2 — Close the finding and tune detections

Close the Mission Control finding with a True Positive, Benign Positive, or False Positive disposition, and state explicitly in the record that the containment actions were simulated. Map the incident to OWASP LLM Top 10 LLM01 (Prompt Injection) and MITRE ATLAS AML.T0051 (LLM Prompt Injection), adjusting the mapping if the campaign also achieved data exposure. File tuning requests for any technique family that reached the model without matching the correlation rule, and add the exact prompt pattern to the prompt injection training corpus so the detection covers it next time.
