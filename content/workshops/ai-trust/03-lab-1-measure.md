+++
title       = "Lab 1 — Measure"
description = "Splunk Agent Observability: evaluate different models, score them with Luna, surface the unknown unknowns, and steer leaked PII out of a response."
duration    = "45 min"
weight      = 30
aliases     = ["/lab-1-measure.html", "/workshops/ai-governance/03-lab-1-measure/", "/workshops/ai-governance-healthcare/03-lab-1-measure/", "/workshops/ai-trust-healthcare/03-lab-1-measure/"]
+++

{{< tour "lab-1" >}}

![The AI Governance Journey, Lab 1 Measure: Splunk Agent Observability. Measure AI quality objectively and identify and steer non-compliance: experiments; evaluation scoring and annotation queues; agent streams, cost and tokenomics; controls that steer leaked PII out](/images/image-390.png)

**Pillar:** Measure<br>
**Tool:** Splunk Agent Observability<br>
**Outcome:** Improved Outcomes

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**AI / ML Platform leaders** and **AI Governance / Risk** teams. Primary question: _Is the AI actually any good — and can I measure quality and safety objectively, version over version?_ This is where subjective "it seems fine" becomes a defensible, repeatable score.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Start by defining and measuring "good." You will compare a **baseline** and a **poisoned** model, see their responses scored by **Luna**, read token usage and cost, and review the **signals** that surface the unknown unknowns. Finally, you see a **control** act at runtime: its own evaluators find personal data in an answer, and it steers that data out before the response reaches the user.
{{% /notice %}}

## Background

Splunk Agent Observability evaluates the **whole agent trace** and scores each turn against research-backed metrics (hallucination, context adherence, PII leakage, tool-selection quality) plus custom evaluators you define for your industry's risks. Evaluators can be run by **Luna** — Cisco's small, purpose-built evaluator models — so continuous LLM-as-judge scoring is affordable rather than a frontier-model bill.

{{% expand title="Custom Evaluator - Financial Services" %}}
In financial services, the custom evaluator is **Securities Fraud**, which flags responses that encourage illegal trading or investment fraud.
{{% /expand %}}

{{% expand title="Custom Evaluator - Healthcare" %}}
In healthcare, the custom evaluator is **Prescriptive Overreach**, which flags responses that act as a prescriber.
{{% /expand %}}

{{% expand title="Custom Evaluator - Manufacturing" %}}
In manufacturing, the custom evaluator is **Safety Override**, which flags responses that act as a supervisor with sign-off authority.
{{% /expand %}}

{{% expand title="Custom Evaluator - Retail" %}}
In retail, the custom evaluator is **Unauthorized Refund**, which flags responses that grant concessions the assistant has no authority to approve.
{{% /expand %}}

Model evaluation, metric construction, and signal understanding are critical both to build trust in AI systems before deployment, and to monitor model drift over time.

## Labs

### Lab 1.1 Explore Prompting in PseudoCo Assistant

{{< tour "lab-1.1" >}}

#### 1.1.1 Access PseudoCo Assistant

![alt text](/workshops/ai-trust/image.png)

[How to Access PseudoCo Assistant](/workshops/ai-trust/01-setup/#1-how-to-access-pseudoco-assistant)

Ensure that you select the Organization **Observability Workshop AMER**.

{{% notice warning "Important" %}}
Because we are using an open weight model, ensure that you select **gpt-4o** from the **Static Emission** dropdown so that tokenomics calculates correctly!
{{% /notice %}}

#### 1.1.2 Explore the Baseline vs the Poisoned Model

![alt text](/workshops/ai-trust/image-1.png)

Select **ollama** in **Provider**. PseudoCo Assistant is pre-loaded with two models - one a baseline version, and a tampered copy of the same open-weight model whose packaged prompt template carries a hidden directive, so it produces non-compliant responses such as toxic content.

![alt text](/workshops/ai-trust/image-2.png)

Click the **>** tab on the left edge to open **Demo Controls**, which has a number of toggles to force non-compliant behavior.

Explore sending sample prompts to both the baseline and the poisoned model (via the model picker), and observe the difference in responses. We review how these differential responses can be automatically identified by Splunk Agent Observability.

#### 1.1.3 Prompt Aberrant Behavior

Explore sending various aberrant prompts and triggering non-compliant behavior. At minimum:

- Send a prompt with the **Outside of Authority** toggle on (its label depends on your industry)
- Send a prompt with **Include Synthetic PII in Responses** toggled on
- Send a prompt with **Include Hallucinated Content in Responses** toggled on
- Send a prompt with various PII, such as a phone number, email address, SSN, or address
- Send a prompt with a toxic or aggressive tone
- Send a prompt with a prompt injection attempt

{{% expand title="Toggle Names and Example Prompt - Financial Services" %}}
In the FinanceAdvice (financial services) theme, the Outside of Authority toggle is labelled **Securities Fraud**, and the PII toggle is labelled **Include Synthetic PII in Responses**.

**Example prompt:** What are some general tips for building an emergency fund?
{{% /expand %}}

{{% expand title="Toggle Names and Example Prompt - Healthcare" %}}
In the MedAdvice (healthcare) theme, the Outside of Authority toggle is labelled **Prescriptive Overreach**, and the PII toggle is labelled **Include Synthetic PII/PHI in Responses**.

**Example prompt:** I have a mild cold. What do you recommend?
{{% /expand %}}

{{% expand title="Toggle Names and Example Prompt - Manufacturing" %}}
In the Manufacturing Ops (manufacturing) theme, the Outside of Authority toggle is labelled **Safety Override**, and the PII toggle is labelled **Include Synthetic PII in Responses**.

**Example prompt:** Our conveyor keeps jamming at the transfer point. What should we check first?
{{% /expand %}}

{{% expand title="Toggle Names and Example Prompt - Retail" %}}
In the Retail Support (retail) theme, the Outside of Authority toggle is labelled **Unauthorized Refund**, and the PII toggle is labelled **Include Synthetic PII in Responses**.

**Example prompt:** How do returns work if I lost my receipt?
{{% /expand %}}

We will explore how this non-compliant behavior is monitored in subsequent sections.

### Lab 1.2 Monitor Behavior in Splunk Agent Observability

{{< tour "lab-1.2" >}}

#### 1.2.1 Access Splunk Agent Observability

[How to Access Splunk Agent Observability & Splunk Observability Cloud](/workshops/ai-trust/01-setup/#2-how-to-access-splunk-agent-observability--splunk-observability-cloud)

#### 1.2.2 Review Overview

![alt text](/images/image-217.png)

Click on **Agent Observability -> All projects**.

![alt text](/images/image-218.png)

Click on the project **PseudoCo Assistant**.

![alt text](/images/image-349.png)

Each section of the Overview dashboard turns AI development into a measurable, evidence-backed discipline — testing safety, comparing versions objectively, and maintaining a defensible record of quality.

Agent Streams — Captures live records of how the AI application behaves in real use, providing a continuous audit trail for monitoring quality and catching issues in production.

Playgrounds — A sandbox for safely experimenting with prompts and model behavior, helping the team iterate and innovate without touching the live system.

Experiments (the leaderboard) — Ranks different versions of the model head-to-head against a benchmark. We see comparisons between the "baseline" versus "poisoned" model runs, scored and rank-ordered. Experiments provide objective, data-driven evidence of which configuration is safest and best-performing — critical for deciding which version has earned the trust to ship.

Datasets — Curated "golden" reference sets used to grade the AI consistently. Reusable datasets are the gold-standard yardstick that makes quality and safety measurable and repeatable.

Prompts — A versioned, centralized library of the instructions that drive the AI, enabling change-control over the core logic, reusable directly in code.

#### 1.2.3 Review Signals

![alt text](/images/image-349.png)
![alt text](/images/image-221.png)

Click on your theme's stream under **Agent Streams**: **MedAdvice**, **FinanceAdvice**, **Manufacturing**, or **Retail**. You might need to click on **View all**.

![alt text](/images/image-225.png)

Click on the **Signals** button. 

![alt text](/images/image-406.png)

The Signals panel is the AI watching the AI — it scans every logged conversation for risk patterns and surfaces them as named, prioritized issues, so the team learns where the application is failing without reading transcripts one by one. Whereas Metrics need to be defined by the user, Signals surface the unknown unknown issues.

Some example Signals (yours might vary):

{{% expand title="Example Signals - Financial Services" %}}
Fabricated PII in LLM output — Flags responses that expose personal data. This is a top-tier compliance and privacy risk, surfaced automatically so it can be contained before it becomes a breach.

Fabricated NovaCure Rx product and citations — Catches an invented product and fake research citations presented as authoritative advice. For a customer-facing financial assistant this is the highest-stakes failure mode, where a wrong answer can cause real harm and liability.
{{% /expand %}}

{{% expand title="Example Signals - Healthcare" %}}
Unnecessary patient PII in medical advice responses — Flags responses that expose personal data. This is a top-tier compliance and privacy risk, surfaced automatically so it can be contained before it becomes a breach.

Fabricated medical sources and medications cited as evidence — Catches invented medical claims, sources and medications. For a health-facing assistant this is the highest-stakes failure mode, where a wrong answer can cause real harm and liability.
{{% /expand %}}

{{% expand title="Example Signals - Manufacturing" %}}
Hallucinated PII in Responses — Flags responses that expose personal data. This is a top-tier compliance and privacy risk, surfaced automatically so it can be contained before it becomes a breach.

Critical Safety Violations — Catches guidance to bypass safety interlocks or skip lockout/tagout. For a plant-floor assistant this is the highest-stakes failure mode, where a wrong answer can cause real harm and liability.
{{% /expand %}}

{{% expand title="Example Signals - Retail" %}}
Hallucinated Sensitive PII — Flags responses that expose personal data. This is a top-tier compliance and privacy risk, surfaced automatically so it can be contained before it becomes a breach.

Critical Action Hallucinations — Catches false claims of refunds, discounts, and warranty extensions that were never actually processed. For a customer-facing retail assistant this is the highest-stakes failure mode, where a wrong answer can cause real harm and liability.
{{% /expand %}}

Click on any Signal.

![alt text](/images/image-407.png)

The Signal Details view turns a detected AI safety issue into an evidence-backed investigation, identifying the root cause, quantifying the impact, and recommending corrective actions.

Root Cause Analysis — Explains exactly how the AI violated expectations, identifying sensitive patient information exposed in responses despite PII detection being triggered. This moves beyond flagging a problem to explaining why it occurred.

Evidence — Quantifies the scope of the issue. Here, 3 of 5 sessions (60%) were affected, with historical scan results showing the frequency of violations. This turns an individual finding into a measurable, auditable risk.

Affected Sessions — Links directly to the underlying conversations and traces, allowing investigators to inspect the actual responses and validate the findings rather than relying on an opaque AI judgment.

Remediation — Provides AI-generated recommendations for addressing the detected behavior, helping teams move from identifying risks to implementing corrective actions.

#### 1.2.4 Review Agent Stream

![alt text](/images/image-408.png)

Click on **Tracing** to return to the **Agent Stream**.

![alt text](/images/image-342.png)

The **Agent Stream**  turns every live AI conversation into a graded, searchable record — the continuous audit trail that proves the application is behaving safely in production.

Traces — The running ledger of real user interactions, capturing what went in and what the AI sent back. This is the system of record that makes behavior observable and reviewable rather than a black box.

Automated scoring (such as Output Toxicity, Output PII, and your industry's custom evaluators) — Every response is auto-graded against safety and quality measures, including custom risk checks tuned to this use case. This is the core value: thousands of interactions evaluated without human review, with weak responses surfaced automatically for attention. You can click on each metric to understand the cost. Notice the significant cost difference between metrics computed using Luna (SLM) and frontier lab models.

![alt text](/images/image-343.png)

Click the checkbox next to any trace, then click on **Add to Annotation Queue** and add it to the queue for your theme: **MedAdvice Continuous Feedback**, **FinanceAdvice Continuous Feedback**, **Manufacturing Continuous Feedback**, or **Retail Continuous Feedback**.

The Annotation Queue is used for continuously improving the agentic system. Return to the **Agent Stream**.

![alt text](/images/image-344.png)

Click on any trace. Other participants' turns share this stream, so look for your own prompt in the **Input** column.

![alt text](/images/image-345.png)

This single-trace view is the microscope of the platform — it opens up one AI conversation end to end, showing exactly how a multi-step agent produced its answer and how that answer scored on quality and safety.

Trace tree (chat turn → agents) — Exposes the full chain of reasoning behind one response, including the agents and underlying model that handled it. This turns a single answer into a traceable, explainable record — essential when you need to prove why the AI said what it said.

Input / Output panel — Shows the exact user request and the verbatim response side by side. This is the ground truth for any review, audit, or dispute — what was actually asked, and what was actually returned.

Metrics — One trace, examined from every angle: how it scored, how it was configured, human notes, and flagged risks. The value is a complete case file for any interaction worth investigating.

Feel free to explore the other tabs, such as **Latency** and **Trace Graph**.

#### 1.2.5 Review Trends

![alt text](/images/image-316.png)

Click the back arrow to return to the **Agent Stream**.

![alt text](/images/image-342.png)

Click on **Trends**.

![alt text](/images/image-228.png)

The Trends view is the over-time picture of AI quality and risk — it tracks whether the application is holding steady, improving, or drifting, turning a snapshot of scores into a story leadership can monitor like any other business metric.

Scroll down to **System Metrics**.

The System Metrics view is the operational and cost dashboard for the AI — alongside quality and safety, it tracks consumption, spend, reliability, and volume, so the application is run like a managed business asset, not an unmonitored experiment.

Token metrics (Input, Output, Num Input/Output, Total Tokens) — Measure how much the AI is consuming to do its work. Because tokens are the unit of cost, this is the direct lever on what the application spends — and the early signal if usage suddenly balloons.

API Failures — Counts how often the underlying service broke. This is the reliability gauge — proof the application is actually up and serving users, and an immediate flag when it isn't.

Traces Count — Tracks total volume of activity. This sizes the workload and gives every other metric context — quality and cost only mean something against how much the system is handling.

Agent Cost — Translates that consumption into dollars. This is the line item leadership actually cares about: what is this AI costing us, tracked over time so spend never becomes a surprise.

Feel free to explore additional metric charts, such as those under **Safety Metrics** and **Custom Evaluators**.

#### 1.2.6 Review Agent Graph

![alt text](/images/image-229.png)

Click on **Agent Graph**.

![alt text](/images/image-317.png)

The **Agent Graph** visualizes how AI agents coordinate across models and workflows, making complex agent behavior transparent, traceable, and easier to govern.

Click on any agent.

![alt text](/images/image-231.png)

Each agent has individual metrics, such as latency, cost, or token consumption.

#### 1.2.7 Review Alerts

![alt text](/images/image-232.png)

Click on **Alerts**.

![alt text](/images/image-233.png)

Click on **Create alert**.

![alt text](/images/image-234.png)

Alerts can be configured to trigger based on the output of any evaluator. Alerts can be fed into automated systems via email or Slack. For example, you could disable a system if cost exceeds a defined parameter.

### Lab 1.3 Evaluators

{{< tour "lab-1.3" >}}

#### 1.3.1 Review Evaluators

![alt text](/images/image-235.png)

Click on **Agent Observability -> Evaluators**.

![alt text](/images/image-236.png)

The Evaluators catalog is the rulebook for how every AI is graded — a central, reusable library of scoring criteria that makes "good" and "safe" mean the same thing across every project and every team. As you have seen, Evaluators are leveraged at every point in the development and deployment lifecycle.

Type (Luna, LLM) — Shows what does the grading — a fast lightweight evaluator (Luna) or a full language model. This lets the business balance cost and speed against depth, choosing the right rigor for each measure.

Level (Trace, Session, LLM, Retriever) — Defines where each evaluator applies — a single step, a whole conversation, or a specific component. Precision here means problems get measured at exactly the layer they occur.

Tags & Modality — Organize the library by purpose (agents, RAG, safety) and data type. As the catalog grows, this is what keeps it navigable and manageable rather than a sprawl.

#### 1.3.2 Review a Custom Evaluator

Open the custom evaluator for your industry.

{{% expand title="Securities Fraud Evaluator - Financial Services" %}}
![alt text](/images/image-332.png)

Search for **securities_fraud**, and click on it.

![alt text](/images/image-333.png)
{{% /expand %}}

{{% expand title="Prescriptive Overreach Evaluator - Healthcare" %}}
![alt text](/images/image-237.png)

Search for **prescriptive_overreach**, and click on it.

![alt text](/workshops/ai-trust/image-25.png)
{{% /expand %}}

{{% expand title="Safety Override Evaluator - Manufacturing" %}}
![alt text](/images/image-336.png)

Search for **safety_override**, and click on it.

![alt text](/images/image-337.png)
{{% /expand %}}

{{% expand title="Unauthorized Refund Evaluator - Retail" %}}
![alt text](/images/image-340.png)

Search for **unauthorized_refund**, and click on it.

![alt text](/images/image-341.png)
{{% /expand %}}

This is where a safety standard gets authored — the editor for a custom evaluator, showing how an abstract risk is turned into a precise, automated, repeatable test that every AI response is graded against.

Configure Input (LLM model / Apply to) — Chooses which AI does the grading and what part of the conversation it judges. The value is deliberate control over how rigorous and how targeted the evaluation is.

Prompt (the scoring rubric) — The heart of it: explicit instructions and graded anchors that define exactly what counts as a minor lapse versus an egregious violation. This converts a fuzzy worry — "is the bot making up facts?" — into a consistent, defensible score that doesn't drift with opinion. You can use the **Help me write** toggle to enhance your prompts.

Configure Output (type & roll-up) — Sets how individual scores combine into a single number that rolls up across the whole experiment. This is what makes one response's grade aggregate into a board-level quality figure.

### Lab 1.4 Controls

{{< tour "lab-1.4" >}}

Evaluators and Signals tell you when the agent misbehaves. **Controls** let you act on it during the conversation. A control in Splunk Agent Observability pairs its own evaluators with an action: **Deny** withholds the answer, **Steer** gives the agent corrective guidance so the answer is rewritten, and **Observe** records the match without changing anything. Controls attach to an Agent Stream: when an application asks Splunk Agent Observability to check a turn, the controls attached to that turn's Agent Stream decide what happens.

#### 1.4.1 Prompt PseudoCo Assistant to Leak PII

![alt text](/images/image-409.png)

Check that **Model** shows the baseline **mistral-nemo:12b**, and select it if needed. Click the **>** tab on the left edge to open **Demo Controls**.

![alt text](/images/image-381.png)

Turn on **Include Synthetic PII in Responses**, and turn the other toggles under **Synthetic Content** off. Make sure **Agent Observability Controls** and the other toggles under **Guardrails** are off. Click the **<** tab to close **Demo Controls**.

![alt text](/images/image-410.png)

Send the example prompt for your industry.

{{% expand title="Toggle and Example Prompt - Financial Services" %}}
In the FinanceAdvice (financial services) theme, the toggle is labelled **Include Synthetic PII in Responses**.

**Example prompt:** What are some general tips for building an emergency fund?
{{% /expand %}}

{{% expand title="Toggle and Example Prompt - Healthcare" %}}
In the MedAdvice (healthcare) theme, the toggle is labelled **Include Synthetic PII/PHI in Responses**.

**Example prompt:** I have a mild cold. What do you recommend?
{{% /expand %}}

{{% expand title="Toggle and Example Prompt - Manufacturing" %}}
In the Manufacturing Ops (manufacturing) theme, the toggle is labelled **Include Synthetic PII in Responses**.

**Example prompt:** Our conveyor keeps jamming at the transfer point. What should we check first?
{{% /expand %}}

{{% expand title="Toggle and Example Prompt - Retail" %}}
In the Retail Support (retail) theme, the toggle is labelled **Include Synthetic PII in Responses**.

**Example prompt:** How do returns work if I lost my receipt?
{{% /expand %}}

![alt text](/images/image-382.png)

Near the top of the answer, a record line lists a full name, date of birth, Social Security number, an ID number (an account, medical record, badge, or rewards number), an email address, and a phone number. This is exactly the personal data that must never reach a user it does not belong to.

#### 1.4.2 Review the PII Steering Control

{{% notice warning "Important" %}}
This is a shared environment, so this part of the lab is **review only**. Do not click **Save changes**, and do not change the toggle on a stream's **Controls** tab. Close the control with **Discard edits**.
{{% /notice %}}

![alt text](/images/image-383.png)

In Splunk Agent Observability, click on **Agent Observability -> Agent streams** (under **PseudoCo Assistant**).

![alt text](/images/image-384.png)

Click on your theme's stream: **MedAdvice**, **FinanceAdvice**, **Manufacturing**, or **Retail**.

![alt text](/images/image-411.png)

Click on the **Controls** tab.

![alt text](/images/image-385.png)

The Controls tab lists the runtime policies attached to this Agent Stream, so you can see at a glance what governs its live turns. Each theme's Agent Stream has its own PII steering control, tuned to that theme's record line: **steer-remove-output-pii-regex-medadvice**, **steer-remove-output-pii-regex-financeadvice**, **steer-remove-output-pii-regex-manufacturing**, or **steer-remove-output-pii-regex-retail**.

Click on your stream's control to open its definition. If your role can't open it, follow along with the next screenshot.

![alt text](/images/image-386.png)

The control's definition turns a privacy policy into an automated runtime check: what to look for, when to look, and what to do when it matches.

Stages — When the control runs. POST (after execution) checks the agent's answer after the model writes it and before the user sees it.

Action — What happens on a match. Steer gives the agent corrective guidance instead of blocking the answer; the answer is rewritten to follow it, and the rewrite is checked again.

Steering context — The guidance itself: remove the personal data, drop the record line including the person's name, and keep the rest of the answer unchanged. Because the guidance is plain language, the same control can be tuned for each use case.

Execution environment — Where the control is evaluated. Server means Splunk Agent Observability evaluates it, so the policy is defined once rather than coded into each application.

Step types — Which steps the control checks. llm limits it to the model's answer.

Evaluator configuration — What the control looks for. Regular-expression evaluators joined by OR scan the output for phone numbers, postal addresses, Social Security numbers, email addresses, dates of birth, and labelled ID numbers such as account, member, rewards, medical record, badge, or employee numbers. Any match triggers the steer.

Controls live in a library under **Agent Observability -> Controls**. Adding a control to an Agent Stream attaches a copy that can be tuned for that stream, as each theme's PII steering control is here.

#### 1.4.3 Turn On Agent Observability Controls

![alt text](/images/image-387.png)

Return to PseudoCo Assistant. If you closed it, see [How to Access PseudoCo Assistant](/workshops/ai-trust/01-setup/#1-how-to-access-pseudoco-assistant). In **Demo Controls**, turn on **Agent Observability Controls**, and leave **Include Synthetic PII in Responses** on. PseudoCo Assistant now asks Splunk Agent Observability to check your message and each answer against the controls attached to its Agent Stream. Click the **<** tab to close **Demo Controls**.

![alt text](/images/image-412.png)

Click on **New Session** and confirm, so the next answer starts a fresh conversation.

#### 1.4.4 See the PII Removed from the Response

![alt text](/images/image-413.png)

Send the same example prompt again. 

![alt text](/images/image-388.png)

The control matched the personal data and steered the agent, which rewrote the answer without it. The rest of the answer covers the same guidance, and is rewritten and checked again.
{{% notice note %}}
If the record line is still in the answer, check that **Agent Observability Controls** is on, click on **New Session**, and send the prompt again.
{{% /notice %}}

![alt text](/images/image-414.png)

In Splunk Agent Observability, return to your theme's **Agent Stream** on the **Tracing** tab, and click on the newest trace with your prompt (check the **Created** column).

![alt text](/images/image-415.png)

At the bottom of the trace tree, click on the shield-icon span named after your stream's control.

![alt text](/images/image-389.png)

The trace records the control as a step of its own, so a runtime correction is as auditable as the answer it changed.

Controls — The control's verdict for this turn. Triggered, with the output `{"action": "steer", "matched": true, "confidence": 1}`, means the answer was rewritten before the user saw it.

Trace tree — The agent step just above the control span is the rewrite. The trace keeps both versions for audit: the agent's original answer in its agent span, and the rewritten answer the user received.

Once scoring finishes, Output PII (SLM) for the trace no longer lists ssn, date_of_birth, email, or phone_number.

Before you move on to Lab 2, turn **Agent Observability Controls** and **Include Synthetic PII in Responses** off again.

## Outcome

**Splunk Agent Observability** turns AI development from a black box into a measurable discipline you can trust. Using PseudoCo Assistant — preloaded with a clean "baseline" model and an intentionally "poisoned" one — participants see firsthand how non-compliant AI behavior is automatically detected and scored.

The journey walks through seven capabilities that make trust measurable and actionable:

**Detect the unknown** — Signals surface risks no one thought to define (PII leakage, hallucinations, harassment), catching the "unknown unknowns" before they become incidents.

**Monitor** — The Agent Stream captures every live AI interaction as a searchable, auto-graded audit trail, so production behavior is observable and reviewable rather than a black box.

**Investigate** — Trace-level detail opens any single conversation end to end, providing a defensible case file of how and why the AI answered as it did.

**Track over time** — Trends chart quality, risk, cost, and reliability day by day, giving leadership early warning of drift and a clear line of sight into spend.

**Prove before shipping** — Experiments rank model versions head-to-head on a fixed benchmark, producing objective evidence of which configuration is safest — and reliably flagging the poisoned model.

**Standardize** — A central Evaluators catalog defines what "good" and "safe" mean once and applies it everywhere, with each evaluator authored as a precise, version-controlled rubric.

**Control** — A control attached to the Agent Stream acts at runtime: when its evaluators match personal data in a response, it steers the agent to rewrite the answer without that data before it reaches the user.

The takeaway: AI risk becomes quantifiable and auditable. Safety, quality, and cost are measured continuously and automatically — at scale, without human review of every interaction — giving the business the defensible evidence it needs to deploy AI with confidence.

Lab 1 ends with the agent's own behavior measured, scored, and explained, including the responses your industry's custom evaluator flags for overstepping the assistant's authority, and with a control that steers leaked personal data out of a response. Lab 2 turns from the agent's own behavior to securing it against attackers at runtime: a prompt injection sent as a structured JSON records lookup tries to exfiltrate sensitive data, and an existing guardrail in **Cisco AI Defense** blocks it before the model reads it.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Improved Outcomes.** You turn AI quality, safety, and cost into measurable operating metrics rather than subjective judgments. You can establish a baseline before release, identify emerging risks in production, and continuously improve the agent against evidence.
{{% /notice %}}

<!-- exec-outcome:end -->
