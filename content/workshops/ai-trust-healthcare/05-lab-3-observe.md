+++
title       = "Lab 3 — Observe"
description = "Splunk Observability Cloud: trace a latency incident end to end and let the Troubleshooting Agent isolate the bottleneck."
duration    = "30 min"
weight      = 50
aliases     = ["/lab-3-observe.html", "/workshops/ai-governance/05-lab-3-observe/", "/workshops/ai-governance-healthcare/05-lab-3-observe/"]
+++

![alt text](/images/image-125.png)

**Pillar:** Observe<br>
**Tool:** Splunk Observability Cloud<br>
**Outcome:** Operational Excellence

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SRE / Observability** and **FinOps** teams, with **AI / ML Platform leaders**. Primary question: _Is the AI healthy, fast, and affordable in production — and when something breaks, can I trace it to the exact agent or request?_ This treats AI as a mission-critical service, monitored like any other.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
After applying the guardrail in Cisco AI Defense, the response is now compliant. However, the service is now slowing down and returning errors. Use the AI Troubleshooting Agent to investigate the alert, identify the root cause, and restore performance.
{{% /notice %}}

## Background

Splunk Observability Cloud instruments the AI application the way you'd instrument any production service — using **OpenTelemetry traces** that follow a request end-to-end, across every agent, model, and operation. The same turns you scored for quality in Lab 1 and screened with AI Defense in Lab 2 also appear here as traces and metrics, so operations, quality, and forensics live on one platform.

The guardrail you applied in [Lab 2](/workshops/ai-trust-healthcare/04-lab-2-secure/) made the response compliant — but the service is now slowing down and returning errors. Here you open the resulting alert and let the **AI Troubleshooting Agent** pinpoint the root cause — instead of grepping logs. AI reliability, cost, and quality are managed on the same screen, as one operational discipline.

## Labs

### Lab 3.1 Triage and Resolve a Latency Incident

#### 3.1.1 Access Splunk Observability Cloud

[How to Access Splunk Observability Cloud](/workshops/ai-trust-healthcare/01-setup/#2-how-to-access-splunk-agent-observability--splunk-observability-cloud)

#### 3.1.2 Review Alerts

![alt text](/workshops/ai-trust-healthcare/image-27.png)

Navigate to **Alerts -> Active alerts**.

![alt text](/workshops/ai-trust-healthcare/image-28.png)

The Active alerts view is the incident command center for the AI application — it consolidates every firing alert into one prioritized queue, ranked by severity, so teams know instantly what's broken, how badly, and where to act first. This workshop org is shared, so you will also see alerts from other services.

#### 3.1.3 Generate Latency Incident

![alt text](/workshops/ai-trust-healthcare/image-29.png)

Go to PseudoCo Assistant, and open the left side-panel.

Toggle **Trigger Demo Incident** on to trigger a series of alerts. With the default values it adds 20 s latency and 50% errors for 600 s for everyone on the instance. Alerts can take a few minutes to appear; if none appear after 5 minutes, let your instructor know.

#### 3.1.4 Triage and Resolve an Alert

![alt text](/workshops/ai-trust-healthcare/image-30.png)

Return to Observability Cloud. In **Active alerts**, set **Service** to **demobot-v3**, then click any alert. Its signal details should show "sf_environment=demobot-ec2-1, sf_service=demobot-v3".

![alt text](/workshops/ai-trust-healthcare/image-31.png)

You might need to toggle **AI Troubleshooting Agent** to **On**. The root cause analysis can take a few minutes to appear.

![alt text](/workshops/ai-trust-healthcare/image-32.png)

This is the alert investigation experience — drilling into a single firing incident to see what broke, what it affected, and why, with an AI Troubleshooting Agent automatically working the root cause. This is where monitoring stops being a dashboard and becomes an answer.

Overview / Root Cause Analysis / Evidence tabs — Structures the investigation from headline, to diagnosis, to the raw proof behind it. The value is a complete, defensible incident case file — conclusions always traceable to evidence.

Alert summary & detail chart — Lays out exactly what triggered: the rule, the condition breached, current versus historical error rate, and the precise moment it spiked. The value is unambiguous detection — not "something feels off," but a measured deviation with a timestamp and a threshold.

Root cause (AI-generated, with confidence) — Delivers a plain-language verdict on the likely cause — and, crucially, states its confidence and admits when evidence is insufficient. The value is honest automation: it accelerates diagnosis without pretending to certainty it doesn't have, which is exactly what you want from AI in a high-stakes operational role.

![alt text](/workshops/ai-trust-healthcare/image-33.png)

Impact summary — Quantifies the blast radius: which service and how many business transactions are affected, and confirms what's not impacted. This is the business-language translation of a technical alert — "what does this actually break for users?"

Troubleshooting tools (Runbooks, Related content, Data links) — Connects the alert to the next actions: established procedures, related dashboards, and deeper traces. This is how an incident moves from understood to resolved, fast.

![alt text](/workshops/ai-trust-healthcare/image-34.png)

Because we triggered the alert synthetically, there is nothing to fix. Go ahead and click **Resolve alert**. Once everyone on your instance is done, return to PseudoCo Assistant and toggle **Trigger Demo Incident** off. Resolving the alert does not stop the incident; it slows every chat on the instance until it is off or its 600 s run ends.

## Outcome

A latency and error spike was diagnosed by an AI agent — without reading a single log line — and resolved. Once the demo incident was switched off, performance returned to baseline.

- **One platform, three views.** APM, the audit log, and the quality scores all describe the same AI service — operations, quality, and forensics in one place.
  forensics share one identity.
- **The agent investigates; you don't grep.** The AI Troubleshooting Agent works the alert end to end and points at the root cause automatically.
- **Cost and latency, on the very same turn.** Observe shows token spend and latency on the very turns Splunk Agent Observability already scored for quality — not in a separate dashboard.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Operational Excellence.** You move AI incidents faster from detection to root cause and resolution, reducing operational effort while protecting performance, user experience, and the economics of running AI at scale.
{{% /notice %}}

<!-- exec-outcome:end -->
