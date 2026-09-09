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
After applying the guardrail in Cisco AI Defense, the response is now compliant. However, latency has spiked beyond SLO. Use the Troubleshooting & Remediation Agent to trace the request end-to-end, isolate the bottleneck, and restore performance.
{{% /notice %}}

## Background

Splunk Observability Cloud instruments the AI application the way you'd instrument any production service — using **OpenTelemetry traces** that follow a request end-to-end, across every agent, model, and operation. Every turn carries the same identity used to score quality in Lab 1 and to record the AI Defense verdict in Lab 2. Operations, quality, and forensics are not three datasets — they are three views of one trace.

The guardrail you applied in [Lab 2](/workshops/ai-trust-healthcare/04-lab-2-secure/) made the response compliant — but latency has now breached SLO. Here you trace that exact request, isolate the slow span, and let the **Troubleshooting & Remediation Agent** pinpoint the bottleneck — instead of grepping logs. AI reliability, cost, and quality are managed on the same screen, as one operational discipline.

## Labs

### Lab 3.1 Triage and Resolve a Latency Incident

#### 3.1.1 Access Splunk Observability Cloud

[How to Access Splunk Observability Cloud](/workshops/ai-trust-healthcare/01-setup/#2-how-to-access-splunk-agent-observability--splunk-observability-cloud)

#### 3.1.2 Review Alerts

![alt text](/images/image-108.png)

Navigate to **Alerts -> Active Alerts**.

![alt text](/images/image-109.png)

The Active alerts view is the incident command center for the AI application — it consolidates every firing alert into one prioritized queue, ranked by severity, so teams know instantly what's broken, how badly, and where to act first.

#### 3.1.3 Generate Latency Incident

![alt text](/images/image-30.png)

Go to DemoBot, and open the left side-panel.

Toggle **Trigger Demo Incident** on to trigger a series of alerts.

#### 3.1.4 Triage and Resolve an Alert

![alt text](/images/image-110.png)

Return to Observability Cloud, and click on any alert corresponding to the environment you previously selected, e.g. "medadviceX". You might need to toggle **AI Troubleshooting Agent to On**.

![alt text](/images/image-113.png)

This is the alert investigation experience — drilling into a single firing incident to see what broke, what it affected, and why, with an AI Troubleshooting Agent automatically working the root cause. This is where monitoring stops being a dashboard and becomes an answer.

Overview / Root Cause Analysis / Evidence tabs — Structures the investigation from headline, to diagnosis, to the raw proof behind it. The value is a complete, defensible incident case file — conclusions always traceable to evidence.

Alert summary & detail chart — Lays out exactly what triggered: the rule, the condition breached, current versus historical error rate, and the precise moment it spiked. The value is unambiguous detection — not "something feels off," but a measured deviation with a timestamp and a threshold.

Root cause (AI-generated, with confidence) — Delivers a plain-language verdict on the likely cause — and, crucially, states its confidence and admits when evidence is insufficient. The value is honest automation: it accelerates diagnosis without pretending to certainty it doesn't have, which is exactly what you want from AI in a high-stakes operational role.

![alt text](/images/image-112.png)

Impact summary — Quantifies the blast radius: which service and how many business transactions are affected, and confirms what's not impacted. This is the business-language translation of a technical alert — "what does this actually break for users?"

Troubleshooting tools (Runbooks, Related content, Data links) — Connects the alert to the next actions: established procedures, related dashboards, and deeper traces. This is how an incident moves from understood to resolved, fast.

![alt text](/images/image-114.png)

Because we triggered the alert synthetically, there is nothing to fix. Go ahead and click **Resolve alert**.

## Outcome

A latency spike was traced to its exact cause — and resolved — without reading a single log line. The slow request was isolated, diagnosed by an AI agent, and performance returned to baseline.

- **One platform, one turn.** The slow turn in APM is the *same* turn as the audit log and the quality score — operations, quality, and
  forensics share one identity.
- **The agent traces; you don't grep.** A Troubleshooting & Remediation Agent follows the request end-to-end and points at the bottleneck automatically.
- **Cost and latency, on the very same turn.** Observe shows token spend and latency on the very turns Splunk Agent Observability already scored for quality — not in a separate dashboard.

APM detectors breach during the ~90s incident; the trace view isolates the slow span; latency returns to ~8s baseline after the fault expires.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Operational Excellence.** You move AI incidents faster from detection to root cause and resolution, reducing operational effort while protecting performance, user experience, and the economics of running AI at scale.
{{% /notice %}}

<!-- exec-outcome:end -->
