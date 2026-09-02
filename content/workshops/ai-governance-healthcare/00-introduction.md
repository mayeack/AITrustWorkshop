+++
title       = "Introduction"
description = "Measured. Secured. Observable. Governed. Agentic Trust delivered - One Cisco, end to end."
duration    = "15 min"
weight      = 5
aliases     = ["/workshops/ai-governance/00-introduction/"]
+++

*A field workshop for the executives accountable for AI — and the engineers who run it. Observability is one of four governed pillars covered here, not the whole story.*

## The Problem: AI Is Moving Faster Than Trust is Being Built

Enterprises are shipping agentic AI into production faster than they can trust it. Autonomous and semi-autonomous agents now make decisions, call tools, and generate language that reaches customers, patients, and regulators — at machine speed, around the clock, at a volume no human review queue can keep pace with.

The risk is not theoretical. A single AI interaction can leak PII or PHI, absorb a prompt injection that overrides its instructions, fabricate a medical treatment that never existed, or quietly drift away from the behavior it was certified with. Each of these is, simultaneously, a **security** event, an **operations** event, a **quality** event, and a **compliance** event.

Yet most organizations are trying to govern this with disconnected point solutions. The security team sees a blocked prompt in one console. The SRE sees a latency spike in another. The data-science team sees a quality score in a third. The compliance officer, during an audit, is handed screenshots from all three and asked to reconstruct what actually happened on a given turn. **Four tools, four truths, no single thread connecting them.** By the time the story is stitched together by hand, the agent has served thousands more turns.

That gap — between the speed of agentic AI and the speed at which you can prove it deserves trust — is the problem this workshop closes.

---

## The Scenario

![alt text](/images/image-120.png)

MedAdvice has demonstrated the value of agentic AI in healthcare: reducing the cost of routine patient interactions, accelerating access to guidance, and allowing skilled clinical staff to focus on higher-acuity cases where their expertise delivers the greatest impact.

That creates a compelling opportunity to improve both operating efficiency and patient outcomes.

![alt text](/images/image-121.png)

But scaling that value introduces material governance risk. Hallucinations, PII exposure, and prescriptive overreach can quickly turn an efficiency gain into a clinical, regulatory, or reputational event.

**The value of MedAdvice can scale. So can the risk. Governance is what makes the economics sustainable.**

---

## The One Cisco Thesis

One Cisco closes the governance gap end to end with **one integrated architecture across four pillars** — and the differentiator versus point tools is structural, not cosmetic.

> **Every AI interaction is captured once and correlated on a shared, OTel-compliant identifier, so security, operations, quality, and audit become one investigation, not four disconnected tools.**

The four pillars:

| **Pillar** | **Capability** | **Platform** |
| --- | --- | --- |
| **Measure / Evaluate** | Define **good**, then prove it — baseline vs. poisoned behavior, token & cost, signals that surface unknown unknowns, continuous metrics on a deployed agent | Splunk Agent Observability |
| **Secure** | Runtime policy + guardrails on every prompt and response | Cisco AI Defense |
| **Observe** | End-to-end tracing, latency, and cost | Splunk Observability Cloud |
| **Govern** | Immutable audit trail + forensics + security incident response | Splunk Core / Enterprise Security |

![alt text](/images/image-118.png)

One Cisco AI Governance architecture: production AI traffic flows through Cisco Cloud Control, Cisco AI Defense, and Cisco Data Fabric into Splunk Observability Cloud and Splunk Core, with Splunk Agent Observability closing the continuous feedback loop back to the AI system — delivering a cohesive agentic AI governance solution.

---

## The Journey: One Turn, Four Pillars

The workshop is delivered against a real, running application: MedAdvice — a multi-agent medical-advice chatbot.

The architectural anchor is the **AI Governance Overview dashboard** in Splunk Core (AI Governance Overview Dashboard). It answers, in one view, the question every leader is actually asking — *"Is our AI safe, reliable, accurate, and accountable right now?"*.

Splunk Agent Observability (Lab 1) is where agentic behavior gets evaluated, defined, and measured. It evaluates the whole agent trace — workflow, agents, tool calls, and the LLM response — and scores each turn against research-backed metrics (hallucination, context adherence, PII/PHI leakage, tool-selection quality) plus custom metrics you define. Those metrics are run by Luna, one of Cisco’s purpose-built small language models, so you get LLM-as-judge quality without paying frontier-model prices to score every turn — and that cost profile is exactly what makes evaluation affordable to run continuously, not just once. You run it two ways: as an offline experiment over a dataset before you ship — and as continuous scoring on live traffic once deployed, where its signals surface the unknown unknowns no one anticipated.

{{% notice style="info" title="What is Luna?" icon="users" %}}
Luna is Splunk Agent Observability's purpose-built small language model family for AI evaluation and runtime protection. Instead of using an expensive frontier LLM to judge every AI interaction, Luna provides specialized, low-latency scoring that can run continuously in production.

The key advantages are:

**Much lower cost:** Luna makes it economically practical to evaluate 100% of production AI traffic rather than sampling. Luna costs pennies per million tokens, roughly 97% lower cost than GPT-style judges for guardrail workloads.

**Real-time performance:** Luna returns evaluations in milliseconds. That allows evaluations to sit directly in the user request/response path without materially degrading experience.

**Purpose-built accuracy:** Rather than being a general-purpose LLM prompted to act as a judge, Luna is specifically trained for evaluation tasks such as hallucination detection, context adherence, security, privacy, and agent behavior.

**Continuous monitoring and protection:** The same evaluation approach can be used offline during development and online as a runtime guardrail, including blocking unsafe responses, detecting prompt injection, identifying PII leakage, or escalating to a human.

**Customizable to enterprise requirements:** Luna can support custom metrics and can be tuned against an organization's own data and definition of acceptable AI behavior, making it more relevant than generic LLM-as-a-judge approaches.

Luna changes AI governance from periodic sampling to continuous control. Its cost and latency profile makes it feasible to evaluate and protect AI interactions at production scale instead of relying primarily on expensive LLM judges or manual review.
{{% /notice %}}

MedAdvice applies safety gates before and after every LLM call. **Cisco AI Defense (Lab 2)** is a live integration: it inspects the prompt pre-LLM and the response post-LLM against multiple guardrails — PII, PHI, PCI, Harassment, Hate, Profanity, Prompt Injection, etc. — and blocks non-compliant content. Every turn is logged with full governance and audit metadata in Cisco Data Fabric.

That same per-turn telemetry feeds **Splunk Observability Cloud (Lab 3)**, the operational lens on the running agent. Where Cisco AI Defense governs what MedAdvice is allowed to say, Observability Cloud watches how it runs, emitting OpenTelemetry traces, spans, latency, and token/cost telemetry for every LLM call and tool hop across the multi-agent graph. The AI Troubleshooting Agent then uses this telemetry to identify incidents, evaluate their root cause and impact, and resolve issues across the agentic workflow.

**Splunk Core (Lab 4)** is where all of it comes to rest, providing the immutable audit trail and unified security record for every governed turn. If MedAdvice detects a prompt injection attempt, Splunk can correlate the malicious prompt, AI Defense verdict, affected agent actions, and downstream response into a single investigation. Enterprise Security Agents can then help triage the event, assess its scope and severity, recommend next actions, and accelerate response, turning that governed telemetry into the foundation for an agentic SOC.

### AI Governance Overview Dashboard: The Single Pane of Glass

**Scenario.** You open the AI Governance Overview dashboard. Governed turns, policy blocks, injections, hallucinations, PII hits, and token cost are all on one screen.

**What One Cisco does.** You see the security, quality, operational, and governance signals for each AI interaction in a common view. Every KPI rolls back to the same correlated interaction record, allowing you to move from program-level posture to the evidence behind an individual turn without reconstructing the story across multiple systems.

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome - Unified Visibility & Control.** You see the posture of the AI program at a glance — and know that any number on the screen is one click from the evidence behind it.
{{% /notice %}}

### Lab 1 — Measure (Splunk Agent Observability): Define Good, Then Prove It

**Scenario.** Before you can trust MedAdvice at scale, you need an objective definition of acceptable behavior. You compare a baseline agent with intentionally degraded behavior against the same patient interactions to see where quality, safety, and economics begin to diverge.

**What One Cisco does.** You use Splunk Agent Observability to evaluate the entire agent trace, including agent decisions, tool calls, context, and LLM responses, against research-backed and custom metrics such as hallucination, context adherence, PII/PHI leakage, and tool-selection quality. Luna, Cisco's purpose-built small language model, makes those evaluations economical enough to run across both pre-production experiments and live production traffic.

You quantify differences between baseline and degraded behavior, understand token usage and cost, and use continuous signals to identify drift, anomalous behavior, and failure modes that predefined test cases may never have anticipated.

The result is not simply a pass/fail test before deployment. You establish a measurable behavioral baseline and continue evaluating the agent against it as the application, models, prompts, tools, and real-world traffic change.

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Improved Outcomes.** You turn AI quality, safety, and cost into measurable operating metrics rather than subjective judgments. You can establish a baseline before release, identify emerging risks in production, and continuously improve the agent against evidence.
{{% /notice %}}

### Lab 2 — Secure (Cisco AI Defense): Operationalize Policies Into Runtime Enforcement

**Scenario.** MedAdvice may evaluate well overall, but every individual interaction still introduces risk. A patient prompt can contain a prompt injection or sensitive information, and an otherwise valid model can generate an inappropriate or overly prescriptive response.

**What One Cisco does.** You use Cisco AI Defense to place runtime controls around every MedAdvice interaction. Prompts are inspected before the LLM is invoked, and generated responses are independently inspected before they reach the patient. Policies detect and enforce against risks such as prompt injection, PII/PHI exposure, prohibited content, and prescriptive overreach.

You then tune a response-direction guardrail against MedAdvice's clinical requirements and immediately re-run the interaction. You see how an observed behavioral risk becomes an enforceable runtime policy, with the resulting verdict and enforcement action captured as part of the governed interaction record.

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Trusted AI.** You move governance from written policy to machine-speed enforcement. Unsafe interactions can be detected and blocked before they create patient, regulatory, or reputational exposure, while controls can be continuously tuned as requirements and risks evolve.
{{% /notice %}}

### Lab 3 — Observe (Splunk Observability Cloud): Find the Failure, Restore the Service

**Scenario.** MedAdvice is now producing compliant responses, but a subset of interactions has become slow and expensive. The answer may be correct, yet degraded latency or runaway token consumption can still undermine adoption, economics, and patient experience.

**What One Cisco does.** You use Splunk Observability Cloud to follow the same MedAdvice interaction across OpenTelemetry traces, spans, latency, service dependencies, token consumption, and cost to see exactly how the agent executed. Splunk Agent Observability tells you whether the agent answered well; Observability Cloud shows you whether it ran well.

You then use the AI Troubleshooting Agent to identify the incident, evaluate its root cause and impact, and drive resolution across the multi-agent workflow. Instead of manually inspecting services and spans until you find the failure, you move from symptom to cause to remediation using the telemetry already emitted by the running application, then validate that performance has returned to the expected SLO.

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Operational Excellence.** You move AI incidents faster from detection to root cause and resolution, reducing operational effort while protecting performance, user experience, and the economics of running AI at scale.
{{% /notice %}}

### Lab 4 — Govern (Splunk Core / Enterprise Security): From Evidence to an Agentic SOC

**Scenario.** MedAdvice receives a prompt-injection attempt. You need to determine what was attempted, how the control responded, whether the interaction affected downstream agent activity, and whether further investigation or response is required.

**What One Cisco does.** You use Splunk Core to preserve the interaction as a correlated, immutable governance record. Using the shared identifier for that turn, you connect the malicious prompt, Cisco AI Defense verdict and enforcement action, relevant agent activity, and supporting telemetry into a single investigation rather than reconstructing the event across separate consoles.

You can then move evidence-backed findings into Splunk Enterprise Security, where Enterprise Security Agents help you triage the event, assess scope and severity, investigate surrounding activity, recommend next actions, and accelerate response. The same telemetry that gives you defensible evidence for governance and audit now becomes actionable security context for an increasingly agentic SOC.

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Accountability & Evidence.** You can make every consequential AI interaction attributable, explainable, and actionable. Audit evidence is available on demand, while security findings can move directly into AI-assisted investigation and response rather than ending in a governance report.
{{% /notice %}}

---

## Executive Outcomes

| **Outcome** | **What it means** | **Grounded in** |
| --- | --- | --- |
| **Unified Visibility & Control** | See the posture of your AI program at a glance, with every material signal traceable to the evidence behind it. | AI Governance Overview Dashboard |
| **Improved Outcomes** | Turn AI quality, safety, and cost into measurable operating metrics, establish a baseline before release, identify emerging risks in production, and continuously improve against evidence. | Splunk Agent Observability |
| **Trusted AI** | Move governance from written policy to machine-speed enforcement, detecting and blocking unsafe interactions before they create patient, regulatory, or reputational exposure. | Cisco AI Defense |
| **Operational Excellence** | Move AI incidents faster from detection to root cause and resolution, reducing operational effort while protecting performance, user experience, and the economics of AI at scale. | Splunk Observability Cloud |
| **Accountability & Evidence** | Make consequential AI interactions attributable, explainable, and actionable, with audit evidence available on demand and security findings flowing directly into AI-assisted investigation and response. | Splunk Enterprise Security |

---

## The Call to Action

Agentic AI is already in production. The question for every CISO, CIO, CTO, and Chief Risk and Compliance officer is no longer *whether* to govern it, but *whether you can prove you are.*

One Cisco makes that proof a single screen and a single thread. **Capture every AI interaction once. Correlate it across security, operations, quality, and audit. Investigate once, not four times.**

This workshop puts that correlated architecture in your hands against a live, running multi-agent application, showing how you measure agent behavior, enforce runtime policy, identify and resolve operational failures, and turn evidence-backed threats into AI-assisted security response, all on the same turn, all on the same thread.

**Measured. Secured. Observable. Governed. One Cisco, end to end.**

Let's govern AI at machine speed.

---
