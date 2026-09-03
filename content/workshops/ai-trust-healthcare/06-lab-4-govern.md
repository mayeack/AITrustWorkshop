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

Expand the left side-panel, and toggle "Prompt-Injection Spray" on. Set the duration to 60.

#### 4.1.3 Investigate the Prompt Injection Spray

![alt text](/images/image-44.png)

Return to Splunk, and navigate to **AI Governance -> Dashboards -> Prompt Injection Detection**.

![alt text](/images/image-116.png)

Each section of the Prompt Injection Detection dashboard turns AI security into a measurable, governed discipline — proving the organization can detect, classify, and defend against adversarial attacks on its AI models.

Total Scanned — Establishes the denominator of coverage: how much AI traffic is actually being inspected for attacks. It answers the first governance question — "are we even looking?" — and proves monitoring is comprehensive, not selective.

Injections Detected, Injections by Severity, and Detection Rate — The headline count of adversarial prompt-injection attempts caught. This is the tangible evidence that the AI is under active threat and that defenses are working, translating an abstract risk into a tracked number leadership can act on.

Detection Trend — Shows whether attack volume and detection are rising or falling over time, turning point-in-time alerts into a directional signal for emerging campaigns and capacity planning.

Injections by Technique — Breaks attacks down by method, revealing how adversaries are trying to manipulate the AI. This intelligence drives where defenses and training need to be hardened next.

Severity & Confidence Distribution — Shows how threats spread across severity levels and how sure the detection model is of its calls. Confidence is the audit lens — it separates high-certainty threats from noise and keeps the system's own judgment accountable.

Top Injection Sources — Identifies where attacks originate, enabling blocking, rate-limiting, and attribution. Knowing the source converts passive detection into active defense.

![alt text](/images/image-117.png)

Recent Detections — A live, row-level audit trail of individual attacks for investigation and forensics — the defensible record that proves what happened, when, and how it was handled.

### Lab 4.2 Follow the Detection into Enterprise Security

#### 4.2.1 Review the Detection Search

![alt text](/images/image-52.png)

Click the Splunk logo in the top left to navigate home.

In the left side-panel, click on **Enterprise Security**.

![alt text](/images/image-53.png)

Navigate to **Security content -> Content management**.

![alt text](/images/image-54.png)

Search for "Prompt Injection Attack Correlation", and click on **GenAI - Prompt Injection Attack Correlation**.

![alt text](/images/image-128.png)

Each section of this Enterprise Security detection editor turns AI threat-hunting into a governed, auditable control — codifying how prompt-injection attacks are detected, correlated, and turned into accountable action.

This is where security logic is authored and version-controlled as a managed asset, not tribal knowledge. Putting detections under formal edit-and-save governance is what makes AI defense repeatable, reviewable, and defensible to auditors.

Click on the **sparkle** icon to expand the Security Assistant right sidepanel.

#### 4.2.1 Review Detection Builder Agent

![alt text](/images/image-129.png)

Click "Explain this Detection", or otherwise chat with the Detection Builder agent.

![alt text](/images/image-130.png)

Review the explanation provided by the agent.

![alt text](/images/image-131.png)

You can also ask the agent "How else can you help me with this detection?".

### 4.3 Review Generated Notable Event

#### 4.3.1 Find the Generated Notable Event

![alt text](/images/image-56.png)

Click on **Mission Control**.

![alt text](/images/image-57.png)

The Analyst Queue is where AI-security detections become accountable casework — every prompt-injection attack is triaged, owned, and dispositioned through a governed investigation workflow.

Analyst Queue — A prioritized, filterable list of every active security finding awaiting human judgment. This is the operational proof that detections don't just fire into the void — they land in a managed queue where someone is accountable for resolving each one.

Click on any record with title **GenAI Prompt Injection Attack...**

![Mission Control finding "GenAI Prompt Injection Attack: t.nguyen (critical)" open in the Analyst Queue, showing its triage fields and AI-assisted analysis](/images/image-132.png)

Finding header (e.g. "GenAI Prompt Injection Attack: t.nguyen (critical)") — Names the threat by actor and severity. Naming the adversary, not just the event, is what turns detection into accountability.

Finding narrative — A plain-language summary of the actor, the attempts, the apps and sessions targeted, the source IPs, and the correlated policy blocks and safety violations. The auditable story of what happened, written so a human can act without decoding raw logs.

Triage fields (Owner, Status, Urgency, Sensitivity, Disposition) — Who owns the case, where it stands, and how it was judged. Still *unassigned*, *New*, and *Undetermined*, this finding is an open obligation; filling these fields is what closes it with a name attached.

Analysis panel — Splunk's Triage agent: a determination ("True Positive - Suspicious Activity"), a severity, and a confidence score (72%), backed by expandable **Justification**, **Tools**, **Evidence**, and **Analysis Details**. The machine's judgment arrives with its evidence attached, so a human can accept or overturn it — and that review is itself recorded.

Details (Finding metadata, Entity, Source, Additional fields, Event) — The raw event behind the summary, so an auditor can verify the story rather than take it on trust.

Click on **Start investigation**.

## 4.3.2 Investigate the Notable Event

![alt text](/images/image-133.png)

Click on the **sparkle** icon to expand the Security Assistant right sidepanel.

![alt text](/images/image-134.png)

Ask the Security Assistant, powered by Splunk's Guided Response agent, how to respond to the event.

For example, you could ask "How should I respond to the prompt injection attempt from t.nguyen?"

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
