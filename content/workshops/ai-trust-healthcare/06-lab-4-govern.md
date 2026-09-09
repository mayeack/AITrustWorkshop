+++
title       = "Lab 4 — Govern"
description = "Splunk and Enterprise Security: immutable audit trail, prompt-injection detection, and accountable casework."
duration    = "1 hour"
weight      = 60
aliases     = ["/lab-4-govern.html", "/workshops/ai-governance/06-lab-4-govern/", "/workshops/ai-governance-healthcare/06-lab-4-govern/"]
+++

![alt text](/images/image-126.png)

**Pillar:** Govern<br>
**Tool:** Splunk and Enterprise Security<br>
**Outcome:** Accountability & Evidence

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security / SecOps** and **Risk & Compliance** teams, with **AI Governance leaders** and **CISOs**. Primary question: _When our AI is attacked or misused, can we prove what happened, who was accountable, and that we responded — with evidence that holds up in an audit?_ This treats AI as a regulated, adversary-facing system that must be governed like any other material business risk.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
During an audit, review immutable AI interaction logs, surface a prompt-injection attempt in the dashboard, and position the evidence-backed correlated record for handoff to Enterprise Security as part of security incident response.
{{% /notice %}}

## Background

Detection and observability tell you *what happened*. Governance is about being able to **prove it** — to an auditor, a regulator, or your own board — and to show that a human was accountable for the response. It is the pillar where trust becomes evidence.

In the earlier labs, every AI interaction was logged with full governance metadata and a shared correlation ID. That foundation is what makes this lab possible: an adversarial prompt-injection attempt isn't just blocked in the moment, it leaves a **permanent, immutable record** that can be reconstructed on demand.

You will stage a real prompt-injection attack against DemoBot, watch it surface in Splunk's Prompt Injection Detection dashboard, trace it back through the correlation search that defines *how* the threat is detected, and follow it into Enterprise Security as a notable event landing in an analyst's queue. The point is the **end-to-end chain**: a live attack becomes a measurable detection, turning a security incident into a defensible story with a clear owner and outcome.

## Labs

### Lab 4.1 Stage and Detect the Prompt Injection

#### 4.1.1 Access Splunk Cloud

[How to Access Splunk](/workshops/ai-trust-healthcare/01-setup/#5-how-to-access-splunk)

#### 4.1.2 Stage the Prompt Injection Spray

[How to Access DemoBot](/workshops/ai-trust-healthcare/01-setup/#1-how-to-access-demobot)

![alt text](/images/image-127.png)

Ensure that **Cisco AI Defense Policy Review** is toggled on.

Expand the left side-panel. Under "Prompt-Injection Spray", set the duration to 60s, then toggle "Prompt-Injection Spray" on.

#### 4.1.3 Investigate the Prompt Injection Spray

![alt text](/images/image-185.png)

Return to Splunk, and navigate to **AI Governance -> Dashboards -> Prompt Injection Detection**.

![alt text](/images/image-145.png)

Each section of the Prompt Injection Detection dashboard turns AI security into a measurable, governed discipline — proving the organization can detect, classify, and defend against adversarial attacks on its AI models.

Total Scanned — Establishes the denominator of coverage: how much AI traffic is actually being inspected for attacks. It answers the first governance question — "are we even looking?" — and proves monitoring is comprehensive, not selective.

Injections Detected, Injections by Severity, and Detection Rate — The headline count of adversarial prompt-injection attempts caught. This is the tangible evidence that the AI is under active threat and that defenses are working, translating an abstract risk into a tracked number leadership can act on.

Detection Trend — Shows whether attack volume and detection are rising or falling over time, turning point-in-time alerts into a directional signal for emerging campaigns and capacity planning.

Injections by Technique — Breaks attacks down by method, revealing how adversaries are trying to manipulate the AI. This intelligence drives where defenses and training need to be hardened next.

Severity & Confidence Distribution — Shows how threats spread across severity levels and how sure the detection model is of its calls. Confidence is the audit lens — it separates high-certainty threats from noise and keeps the system's own judgment accountable.

Top Injection Sources — Identifies where attacks originate, enabling blocking, rate-limiting, and attribution. Knowing the source converts passive detection into active defense.

![alt text](/images/image-117.png)

Recent Detections — A live, row-level audit trail of individual attacks for investigation and forensics — the defensible record that proves what happened, when, and how it was handled.

### Lab 4.2 Create a Response Plan using the SOP Agent

![alt text](/images/image-146.png)

Click the Splunk logo in the top left to navigate home.

In the left side-panel, click on **Enterprise Security**. Enter "Enterprise Security" in the search box if it does not appear.

![alt text](/images/image-157.png)

Click on **Configure -> All configurations**.

![alt text](/images/image-158.png)

Click on **Investigation types**.

![alt text](/images/image-159.png)

Click on **+ Investigation type** to create a new investigation type.

![alt text](/images/image-162.png)

Enter the following information, and then click **Next**.

**Investigation type name:** prompt_injection
**Investigation type description:** An attempted or actual prompt injection attack against an AI system.

![alt text](/images/image-163.png)

Click **Save**.

![alt text](/images/image-164.png)

Click on the created investigation type.

![alt text](/images/image-165.png)

Click **Create new response plan.**

![alt text](/images/image-166.png)

Click **Import**.

![alt text](/images/image-167.png)

The Guided Response agent works from a standard operating procedure. Download the SOP used for this scenario and load it into the agent to see the four-phase NIST 800-61 plan it generates.

{{< button href="/files/prompt-injection-investigation-and-response-sop.md" icon="download" style="primary" download="true" >}}Download the SOP (.md){{< /button >}} {{< button href="/files/prompt-injection-investigation-and-response-sop.html" icon="file" style="secondary" target="_blank" >}}View in browser{{< /button >}}

Upload the file in the box under **Import and generate with AI**.

![alt text](/images/image-168.png)

Click **Import**.

![alt text](/images/image-169.png)

Wait for generation to complete, then click on the created response plan.

![alt text](/images/image-170.png)

Feel free to explore the sections created by the SOP agent, then toggle to **Published**.

![alt text](/images/image-171.png)

Click **Save changes** if prompted.

![alt text](/images/image-177.png)

Click on **Configure -> All configurations**.

![alt text](/images/image-178.png)

Click on **Investigation types**.

![alt text](/images/image-179.png)

Click on **prompt_injection**.

![alt text](/images/image-180.png)

CLick on **Assign response plan**.

![alt text](/images/image-181.png)

Click on the response plan you just created **Prompt Injection Attack - Investigation and Response**, then click **Submit**.

![alt text](/images/image-182.png)

Click **Save changes**.

## Lab 4.3 Configure the Detection Search

#### 4.3.1 Review the Detection Search

![alt text](/images/image-147.png)

Navigate to **Security content -> Content management**.

![alt text](/images/image-148.png)

Search for "Prompt Injection Attack Correlation", and click on **GenAI - Prompt Injection Attack Correlation**.

![alt text](/images/image-149.png)

Each section of this Enterprise Security detection editor turns AI threat-hunting into a governed, auditable control — codifying how prompt-injection attacks are detected, correlated, and turned into accountable action.

This is where security logic is authored and version-controlled as a managed asset, not tribal knowledge. Putting detections under formal edit-and-save governance is what makes AI defense repeatable, reviewable, and defensible to auditors.

![alt text](/images/image-172.png)

Scroll down to **Analyst queue information** and click on the arrow next to **Create a finding**.

![alt text](/images/image-173.png)

Click on the dropdown for **Investigation type**.

![alt text](/images/image-174.png)

Select the investigation type, **prompt_injection**, you just created.

![alt text](/images/image-175.png)

Click **Save**.

Click on the **sparkle** icon to expand the Security Assistant right sidepanel.

#### 4.3.2 Review the Detection Builder Agent

![alt text](/images/image-150.png)

This detetection was built using the Detection Builder Agent. If you would like to experiment with building your own detections, you use the below prompt.

{{% expand title="Detection Prompt" %}}
Core metadata:
Name: GenAI - Prompt Injection Attack Correlation
App: TA-gen_ai_cim
Detection type: Event-Based Detection

Goal:
Detect actor-centric prompt injection attacks in GenAI telemetry by identifying any actor with at least one prompt injection attempt in the last 24 hours, then correlating that actor’s full related GenAI activity into a single finding. Aggregate repeat injections, policy blocks, guardrail triggers, safety violations, PII exposure, anomalous prompts, targeted apps, targeted models, and distinct sessions. Create both a finding and risk-based output. This rule is the actor-centric companion to GenAI - Prompt Injection Attempt Detected.

Description:
Detects prompt injection attacks (guardrail-, policy-, or pattern-based) and correlates each attacker's full GenAI activity into a single notable: repeat injections, policy blocks, guardrail trips, safety violations, PII exposure, anomalous prompts, and the apps/models/sessions targeted. Actor-centric companion to "GenAI - Prompt Injection Attempt Detected" (which is app-centric, ML-pipeline based). Seeded from event 858b92e6-9f26-49d9-aa53-ec48ad2884ef (Cisco AI Defense block of user x.collins). Raises a notable plus risk (RBA) against the offending identity and source address.

Schedule
Cron: */1 * * * *
Earliest: -24h
Latest: now
Allow skew: 5m
Trigger
Trigger type: number of events
Comparator: greater than
Threshold: 0
Throttling
Throttle window: 86400s
Throttle by field: actor
Finding output
Enable finding output with:

Title: GenAI Prompt Injection Attack: $user$ ($severity$)
Description: Actor "$user$" generated $injection_attempts$ prompt injection attempt(s) (max risk $max_risk_score$) across $apps_targeted$ app(s) and $distinct_sessions$ session(s) from $src$. Correlated activity: $policy_blocks$ policy block(s), $safety_violations$ safety violation(s), $pii_events$ PII exposure event(s), $anomalous_prompts$ anomalous prompt(s). Techniques: $techniques$. Investigate for jailbreak, guardrail bypass, or data exfiltration. Raw prompt text is deliberately NOT copied into this notable - use the drilldown to read it in gen_ai_log, where index-level access controls and retention apply.
Security domain: threat
Severity: high
Investigation type: ai security incident
Drilldown
Configure a drilldown search:

Name: View all GenAI activity for $user$
Search: index=gen_ai_log \exclude_scoring_sourcetypes` (gen_ai.user.id="$user$" OR enduser.id="$user$" OR client.address="$src$") | sort - _time`
Earliest offset: 1d
Latest offset: 1h
Recommended actions
ai_defense_suspend_user
ai_defense_revoke_session
ai_defense_tighten_guardrail
Next steps
Use this next-steps content:

Containment standard: 3 or more blocked prompt-injection attempts within 24 hours from one actor with no authorized-testing record means the account is inactivated pending review.

Review the actor's raw prompts and sessions through the Contributing events drill-down (the finding deliberately carries no prompt text).
Validate intent with the user's manager: is there an authorized red-team or testing record for this user?
If the standard is met, inactivate the account: run the response plan's Containment task action on the paired SOAR - identity provider connector -> disable user for this finding's user (the Guided Response agent runs it from the prompt "Disable user "; the TA ships a simulated MedAdvice Identity Provider whose results carry simulated=true). Without a paired SOAR run [[action|ai_defense_suspend_user]].
Revoke the actor's active sessions: identity provider connector -> clear user sessions, or [[action|ai_defense_revoke_session]].
Tighten the guardrail for the technique observed so every user is covered: [[action|ai_defense_tighten_guardrail]].
Record the disposition and rationale on the investigation; the Containment task requires a note.
Risk output
Enable risk output and create two risk objects:

Risk object field: user
Risk object type: user
Risk score: 80
and

Risk object field: src
Risk object type: `system
{{% /expand %}}

Click **Explain this Detection**, or otherwise chat with the Detection Builder agent.

![alt text](/images/image-151.png)

Review the explanation provided by the agent.

### Lab 4.4 Respond to the Notable Event

#### 4.4.1 Investigate with the Triage Agent

![alt text](/images/image-152.png)

Click on **Mission Control**.

![alt text](/images/image-153.png)

The Analyst Queue is where AI-security detections become accountable casework — every prompt-injection attack is triaged, owned, and dispositioned through a governed investigation workflow.

Analyst Queue — A prioritized, filterable list of every active security finding awaiting human judgment. This is the operational proof that detections don't just fire into the void — they land in a managed queue where someone is accountable for resolving each one.

Click on any record with title **GenAI Prompt Injection Attack...** where AI Dispoistion is **True Positive**.

![alt text](/images/image-154.png)

Finding header (e.g. "GenAI Prompt Injection Attack: t.nguyen (critical)") — Names the threat by actor and severity. Naming the adversary, not just the event, is what turns detection into accountability.

Finding narrative — A plain-language summary of the actor, the attempts, the apps and sessions targeted, the source IPs, and the correlated policy blocks and safety violations. The auditable story of what happened, written so a human can act without decoding raw logs.

Triage fields (Owner, Status, Urgency, Sensitivity, Disposition) — Who owns the case, where it stands, and how it was judged. Still *unassigned*, *New*, and *Undetermined*, this finding is an open obligation; filling these fields is what closes it with a name attached.

Analysis panel — Splunk's Triage agent: a determination ("True Positive - Suspicious Activity"), a severity, and a confidence score (72%), backed by expandable **Justification**, **Tools**, **Evidence**, and **Analysis Details**. The machine's judgment arrives with its evidence attached, so a human can accept or overturn it — and that review is itself recorded.

Details (Finding metadata, Entity, Source, Additional fields, Event) — The raw event behind the summary, so an auditor can verify the story rather than take it on trust.

Click on **Start investigation**.

#### 4.4.2 Respond with the Guided Response Agent

![alt text](/images/image-155.png)

Click on the **sparkle** icon to expand the Security Assistant right sidepanel.

![alt text](/images/image-156.png)

You can leverage the Security Assistant to provide you more details about the investigation.

Click on **Response**.

![alt text](/images/image-184.png)

The response plan that you previously created has been automatically attached to this investigation.

Automated actions, such as disabling the user's account, can be triggered from the response plan.

**Note:** Because this is a synthetic user, trigger the disable will result in an error.

## Outcome

- The logs are **immutable** and complete. Every turn carries full governance metadata — auditability you can defend.
- One search, one identifier, the whole story: what was asked, what the model said, what Splunk Agent Observability scored, what AI Defense ruled, what the detection pipelines flagged.
- The injection attempt didn't just get blocked — it left **evidence**, and that evidence became **accountable casework**: a named actor, an owner, and a documented disposition. That correlated record is exactly what Enterprise Security would promote to a notable in production.

The prompt injection turn is visible and flagged in the search results; the Prompt Injection dashboard shows the detection. The correlation search identifies the event, and then escalates a notable event as the evidence in Enterprise Security.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Accountability & Evidence.** You can make every consequential AI interaction attributable, explainable, and actionable. Audit evidence is available on demand, while security findings can move directly into AI-assisted investigation and response rather than ending in a compliance report.
{{% /notice %}}

<!-- exec-outcome:end -->
