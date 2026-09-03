+++
title       = "Lab 1 — Measure"
description = "Splunk Agent Observability: run a baseline-vs-poisoned evaluation, score it with Luna, and surface the unknown unknowns."
duration    = "1 hour"
weight      = 30
aliases     = ["/lab-1-measure.html", "/workshops/ai-governance/03-lab-1-measure/", "/workshops/ai-governance-healthcare/03-lab-1-measure/"]
+++

![alt text](/images/image-123.png)

**Pillar:** Measure<br>
**Tool:** Splunk Agent Observability<br>
**Outcome:** Improved Outcomes

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**AI / ML Platform leaders** and **AI Governance / Risk** teams. Primary question: _Is the AI actually any good — and can I measure quality and safety objectively, version over version?_ This is where subjective "it seems fine" becomes a defensible, repeatable score.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Before you guard or operate anything, define and measure "good." You will run a **baseline-vs-poisoned** evaluation, see it scored by **Luna**, read token/cost, and the **signals** that surface the unknown unknowns.
{{% /notice %}}

## Background

Splunk Agent Observability evaluates the **whole agent trace** and scores each turn against research-backed metrics (hallucination, context adherence, PII/PHI leakage, tool-selection quality) plus custom metrics you define, such as Prescriptive Overreach. Metrics are run by **Luna** — Cisco's small, purpose-built evaluator models — so continuous LLM-as-judge scoring is affordable rather than a frontier-model bill.

Model evaluation, metric construction, and signal understanding is critical both to build trust in AI systems before deployment, and to monitor model drift over time.

## Labs

### Lab 1.1 Explore Prompting in DemoBot

#### 1.1.1 Access DemoBot

![alt text](/images/image-21.png)

[How to Access DemoBot](/workshops/ai-trust-healthcare/01-setup/#1-how-to-access-demobot)

{{% notice warning "Important" %}}
Because we are using an open weight model, ensure that you select **gpt-4o-mini** from the **Static Emission** dropdown so that tokenomics calculates correctly!
{{% /notice %}}

#### 1.1.2 Explore the Baseline vs the Poisoned Model

![alt text](/images/image-92.png)

Select **ollama** in **Provider**. DemoBot is pre-loaded with two models - one a baseline version, and one that has been intentionally poisoned to produce non-compliant responses, such as toxic content.

![alt text](/images/image-119.png)

The left sidepanel also has a number of controls to force non-compliant behavior.

Explore sending sample prompts to both the baseline and the poisoned model (via the model picker), and observe the difference in responses. We will then review how these differential responses can be automatically identified by Splunk Agent Observability.

#### 1.1.3 Prompt Aberrant Behavior

Explore sending various aberrant prompts and triggering non-compliant behavior. At minimum:

- Send a prompt with **Prescriptive Overreach** toggled on
- Send a prompt with **Include Synthetic PII/PHI in Responses** toggled on
- Send a prompt with various PII, such as a phone number, email address, SSN, or address
- Send a prompt with a toxic or aggressive tone
- Send a prompt with a prompt injection attempt

We will explore how this non-compliant behavior is monitored in subsequent sections.

### Lab 1.2 Monitor Production Behavior in Splunk Agent Observability

#### 1.2.1 Access Splunk Agent Observability

Go to **https://console.multitenant.galileocloud.io/splunkse** and enter the username / password provided by the facilitator.

#### 1.2.2 Review Overview

![alt text](/images/image-94.png)

Search for the project **DemoBot**, and then click on it.

![alt text](/images/image-95.png)

Click on **Overview**.

Each section of the Overview dashboard turns AI development into a measurable, evidence-backed discipline — testing safety, comparing versions objectively, and maintaining a defensible record of quality.

Log Streams — Captures live records of how the AI application behaves in real use, providing a continuous audit trail for monitoring quality and catching issues in production.

Playgrounds — A sandbox for safely experimenting with prompts and model behavior, helping the team iterate and innovate without touching the live system.

Experiments (the leaderboard) — Ranks different versions of the model head-to-head against a benchmark. We see comparisons between the "baseline" versus "poisoned" model runs, scored and rank-ordered. Experiments provide objective, data-driven evidence of which configuration is safest and best-performing — critical for deciding which version has earned the trust to ship.

Datasets — Curated "golden" reference sets used to grade the AI consistently. Reusable datasets are the gold-standard yardstick that makes quality and safety measurable and repeatable.

Prompts — A versioned, centralized library of the instructions that drive the AI, enabling change-control over the core logic, reusable directly in code.

#### 1.2.3 Review Logs

![alt text](/images/image-96.png)

Click on **Logs**.

The Log Stream view turns every live AI conversation into a graded, searchable record — the continuous audit trail that proves the application is behaving safely in production.

Logs — The running ledger of real user interactions, capturing what went in and what the AI sent back. This is the system of record that makes behavior observable and reviewable rather than a black box.

Automated scoring (such as Output Toxicity, Prescriptive Overreach, Completeness) — Every response is auto-graded against safety and quality measures, including custom risk checks tuned to this use case. This is the core value: thousands of interactions evaluated without human review, with weak responses surfaced automatically for attention. You can click on each metric to understand the cost. Notice the significant cost difference between metrics computed using Luna (SLM) and frontier lab models.

#### 1.2.4 Review Signals

![alt text](/images/image-3.png)

Click on the **Signals** button. Click on **Refresh** if no signals appear. 

The Signals panel is the AI watching the AI — it scans every logged conversation for risk patterns and surfaces them as named, prioritized issues, so the team learns where the application is failing without reading transcripts one by one. Whereas Metrics need to be defined by the user, Signals surface the unknown unknown issues, such as:

Some example Signals (yours might vary):

Sensitive PII Leakage — Flags responses that expose personal data. This is a top-tier compliance and privacy risk, surfaced automatically so it can be contained before it becomes a breach.

Medical Hallucinations & Violations — Catches invented medical claims and unauthorized prescriptions. For a health-facing assistant this is the highest-stakes failure mode, where a wrong answer can cause real harm and liability.

Unexpected Harassment — Detects abusive or harassing language from the AI. A direct guard on brand safety and user trust.

#### 1.2.5 Review Log Details

Click on any log.

![alt text](/images/image-4.png)

This single-trace view is the microscope of the platform — it opens up one AI conversation end to end, showing exactly how a multi-step agent produced its answer and how that answer scored on quality and safety.

Trace tree (Session → chat turn → agents) — Exposes the full chain of reasoning behind one response, including the specialist agents and underlying model that handled it. This turns a single answer into a traceable, explainable record — essential when you need to prove why the AI said what it said.

Input / Output panel — Shows the exact user request and the verbatim response side by side. This is the ground truth for any review, audit, or dispute — what was actually asked, and what was actually returned.

Metrics — One trace, examined from every angle: how it scored, how it was configured, human notes, and flagged risks. The value is a complete case file for any interaction worth investigating.

Feel free to explore the other tabs, such as **Latency** and **Trace Graph**.

#### 1.2.6 Review Trends

![alt text](/images/image-10.png)

Click on the back arrow, then click on **Trends**.

The Trends view is the over-time picture of AI quality and risk — it tracks whether the application is holding steady, improving, or drifting, turning a snapshot of scores into a story leadership can monitor like any other business metric.

Metrics charts — Plots the application's domain-specific risks day by day, so emerging problems show up as a rising line before they become incidents. This is early warning for the failure modes that matter most to this business.

![alt text](/images/image-97.png)

Scroll down to **System Metrics**.

The System Metrics view is the operational and cost dashboard for the AI — alongside quality and safety, it tracks consumption, spend, reliability, and volume, so the application is run like a managed business asset, not an unmonitored experiment.

Token metrics (Input, Output, Num Input/Output, Total Tokens) — Measure how much the AI is consuming to do its work. Because tokens are the unit of cost, this is the direct lever on what the application spends — and the early signal if usage suddenly balloons.

API Failures — Counts how often the underlying service broke. This is the reliability gauge — proof the application is actually up and serving users, and an immediate flag when it isn't.

Traces Count — Tracks total volume of activity. This sizes the workload and gives every other metric context — quality and cost only mean something against how much the system is handling.

Agent Cost — Translates that consumption into dollars. This is the line item leadership actually cares about: what is this AI costing us, tracked over time so spend never becomes a surprise.

Feel free to explore additional metric charts.

### Lab 1.3 Prove Before Shipping with Experiments

#### 1.3.1 Review Experiments

{{% notice style="WARNING" title="KNOWN BUG" %}}
**NOTE: There is a known bug with ranking of Experiments; SKIP Lab 1.3 (1.3.1 & 1.3.2), and proceed to Lab 1.4**
{{% /notice %}}

![alt text](/images/image-5.png)

Click on **Experiments**.

Because Experiments can take 10+ minutes to execute, we have already executed an experiment for you to review the results.

The Experiments leaderboard is where AI changes are proven before they ship — it pits different versions of the application head-to-head on the same tests and ranks them by safety and quality, turning "we think this is better" into evidence.

Rank (with the crowned #1) — Orders every version best-to-worst based on the selected metrics, crowning a clear winner. This is the objective verdict leadership needs to decide which configuration is safe to trust.

Name (baseline vs. poisoned runs) — Identifies what each run is — including deliberately compromised "poisoned" versions tested against clean "baseline" ones. This shows the team can detect a degraded or tampered model rather than discovering it in production.

Dataset (with versions) — Records exactly which reference test set each run was graded against, and which version of it. This is what makes a comparison fair and repeatable — everyone is measured against the same yardstick.

Scoring columns (Prompt Injection, Output Toxicity, Prescriptive Overreach, Completeness, etc.) — Grades each version across the safety and quality dimensions that matter most for this use case, including resistance to attacks and overstepping into unauthorized advice. The value is a multi-dimensional safety scorecard, not a single pass/fail.

#### 1.3.2 Compare Two Experiments

![alt text](/images/image-6.png)

Click on the checkbox next to the two experiments, then click **Compare Experiments**.

![alt text](/images/image-7.png)

You can review two or more experiments side by side.

### Lab 1.4 Standardize Metrics

#### 1.4.1 Review Metrics

![alt text](/images/image-8.png)

Click on **Metrics**.

The Metrics catalog is the rulebook for how every AI is graded — a central, reusable library of scoring criteria that makes "good" and "safe" mean the same thing across every project and every team. As you have seen, Metrics are leveraged at every point in the development and deployment lifecycle.

Metric type (Luna, LLM) — Shows what does the grading — a fast lightweight evaluator (Luna) or a full language model. This lets the business balance cost and speed against depth, choosing the right rigor for each measure.

Metric level (Trace, Session, LLM, Retriever) — Defines where each metric applies — a single step, a whole conversation, or a specific component. Precision here means problems get measured at exactly the layer they occur.

Tags & Modality — Organize the library by purpose (agents, RAG, safety) and data type. As the catalog grows, this is what keeps it navigable and manageable rather than a sprawl.

#### 1.4.2 Review Prescriptive Overreach Metric

![alt text](/images/image-98.png)

Scroll down to (or search for) the **Prescriptive Overreach Metric**, and click on it.

![alt text](/images/image-99.png)

This is where a safety standard gets authored — the editor for a custom Prescriptive Overreach Metric, showing how an abstract risk is turned into a precise, automated, repeatable test that every AI response is graded against.

Metric description (the intent) — States in plain terms what this metric watches for and how to read it — higher means worse, lower is better. This is the business definition of the risk, written so anyone reviewing results knows exactly what's being measured and which direction is good.

Configure Input (LLM model / Apply to) — Chooses which AI does the grading and what part of the conversation it judges. The value is deliberate control over how rigorous and how targeted the evaluation is.

Prompt (the scoring rubric) — The heart of it: explicit instructions and graded anchors that define exactly what counts as a minor lapse versus an egregious violation. This converts a fuzzy worry — "is the bot making up medical facts?" — into a consistent, defensible score that doesn't drift with opinion. You can use the **Help me write** toggle to enhance your prompts.

Configure Output (type & roll-up) — Sets how individual scores combine into a single number that rolls up across the whole experiment. This is what makes one response's grade aggregate into a board-level quality figure.

## Outcome

**Splunk Agent Observability** turns AI development from a black box into a measurable discipline you can trust. Using DemoBot — preloaded with a clean "baseline" model and an intentionally "poisoned" one — participants see firsthand how non-compliant AI behavior is automatically detected, scored, and contained.

The journey walks through six capabilities that make trust measurable:

**Monitor** — Logs capture every live AI interaction as a searchable, auto-graded audit trail, so production behavior is observable and reviewable rather than a black box.

**Detect the unknown** — Signals surface risks no one thought to define (PII leakage, medical hallucinations, harassment), catching the "unknown unknowns" before they become incidents.

**Investigate** — Trace-level detail opens any single conversation end to end, providing a defensible case file of how and why the AI answered as it did.

**Track over time** — Trends chart quality, risk, cost, and reliability day by day, giving leadership early warning of drift and a clear line of sight into spend.

**Prove before shipping** — Experiments rank model versions head-to-head on a fixed benchmark, producing objective evidence of which configuration is safest — and reliably flagging the poisoned model.

**Standardize** — A central Metrics catalog defines what "good" and "safe" mean once and applies it everywhere, with each metric authored as a precise, version-controlled rubric.

The takeaway: AI risk becomes quantifiable and auditable. Safety, quality, and cost are measured continuously and automatically — at scale, without human review of every interaction — giving the business the defensible evidence it needs to deploy AI with confidence.

Now that we have identified the critical metric Prescriptive Overreach, let's operationalize that in **Cisco AI Defense**.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Improved Outcomes.** You turn AI quality, safety, and cost into measurable operating metrics rather than subjective judgments. You can establish a baseline before release, identify emerging risks in production, and continuously improve the agent against evidence.
{{% /notice %}}

<!-- exec-outcome:end -->
