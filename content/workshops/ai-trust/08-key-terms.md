+++
title       = "Key Terms & Definitions"
description = "A glossary of the AI trust, security, observability, and governance terms used across the workshop."
duration    = "Reference"
weight      = 80
+++

The terms used throughout this workshop, grouped by the platform and lab where you meet them and listed alphabetically within each group. Industry-specific names, such as each theme's custom evaluator, are in the panels under [Industry Terms](#industry-terms).

## Core Concepts

| **Term** | **Definition** |
| --- | --- |
| **Agentic AI** | AI built from autonomous or semi-autonomous agents that make decisions, call tools, and generate language that reaches customers and regulators, at machine speed and at a volume no human review queue can keep pace with. |
| **Executive outcomes** | The five business results the workshop delivers, one per lab: Unified Visibility & Control, Improved Outcomes, Trusted AI, Operational Excellence, and Accountability & Evidence. See [Wrap-Up & Outcomes](/workshops/ai-trust/07-wrap-up/). |
| **Four pillars of trust** | Measure (*Is it good?*), Secure (*Is it safe?*), Observe (*Is it reliable?*), and Govern (*Is it accountable?*). Each pillar has its own lab and platform. |
| **Governance record** | The record of one turn, logged with full governance and audit metadata: the prompt and response, model, tokens, cost, latency, safety verdicts, and user and session context. Every pillar reads the same record. |
| **Multi-agent application** | An application in which several AI agents, each with its own role, coordinate to produce one answer. PseudoCo Assistant is one. |
| **Non-compliant response** | A response that breaks a quality, safety, or policy requirement, for example one that leaks PII, contains toxic content, or oversteps the assistant's authority. |
| **One Cisco** | The integrated Cisco and Splunk architecture that captures every AI interaction once and correlates it across security, operations, quality, and audit, so they become one investigation rather than four. |
| **Session** | A series of related turns from one user, such as one chat conversation. |
| **Trust gap** | The gap between the speed at which agentic AI is deployed and the speed at which an organization can prove it deserves trust. |
| **Turn** | One AI interaction: a user's prompt, the assistant's response, and every agent step, tool call, and LLM call in between. |
| **Unknown unknowns** | Failure modes no one anticipated, so no predefined test or metric looks for them. Signals in Splunk Agent Observability surface them. |

## AI Models and Cost

| **Term** | **Definition** |
| --- | --- |
| **Frontier model** | One of the largest, most capable general-purpose LLMs from the leading AI labs. A capable judge of AI output, but expensive to run on every turn. |
| **LLM (large language model)** | A model that reads and generates language. Every PseudoCo Assistant turn includes at least one LLM call. |
| **LLM-as-judge** | Using a language model to score another model's output against a rubric, in place of a human reviewer. |
| **Open-weight model** | A model whose weights are published, so it can run on your own infrastructure. The workshop's baseline and poisoned models are open-weight models. |
| **SLM (small language model)** | A compact language model trained for a narrow task. It is faster and much cheaper to run than a frontier model. Luna is a family of SLMs. |
| **Token** | The unit of text a language model reads and writes, and the unit of LLM cost. Token metrics count input, output, and total tokens. |
| **Tokenomics** | Token usage and the cost it implies, tracked per turn, agent, model, and session. |

## Risks and Attacks

| **Term** | **Definition** |
| --- | --- |
| **Attack vector** | A technique an attacker uses against an AI system, such as role or persona hijacking, system prompt extraction, encoded or obfuscated payloads, indirect injection through pasted content, or a jailbreak framed as a hypothetical. |
| **Data exfiltration** | Getting sensitive data out of a system, either by reading it straight back into the reply or by sending it somewhere the attacker controls. In Lab 2, a prompt injection tries to exfiltrate personal details on file. |
| **Drift** | A gradual change in an agent's behavior away from the baseline it was certified with, as the application, models, prompts, tools, and real-world traffic change. |
| **Hallucination** | A response that states something with no basis in fact, such as an invented product, citation, or medication. |
| **Indirect prompt injection** | A prompt injection that a third party plants inside content the assistant is asked to process, such as a document, a web page, an email, or a record, so the person sharing the content never notices it. |
| **Jailbreak** | An attempt to talk a model out of its safety rules, often framed as a hypothetical or a role-play. |
| **Outside of Authority** | A response that oversteps the assistant's authority, acting as a licensed professional or an approver. Each industry has its own name for it and a custom evaluator that flags it; see [Industry Terms](#industry-terms). |
| **PCI** | Payment card data, governed by the Payment Card Industry standards. |
| **PHI** | Protected health information: health data tied to an individual, such as a medical record number. |
| **PII** | Personally identifiable information: data that identifies a person, such as a full name, date of birth, Social Security number, email address, phone number, or home address. |
| **Prompt injection** | Instructions embedded in a prompt, or in content the assistant processes, that try to override the assistant's own instructions, for example to reveal sensitive data. |
| **Shadow AI** | AI applications, models, and services in use that the security team does not know about. |
| **System prompt extraction** | An attack that tries to make a model reveal the hidden instructions it was given. |
| **Toxicity** | Abusive, harassing, hateful, or profane content in a prompt or a response. |

## PseudoCo Assistant

The live, multi-agent application the workshop runs against. See [Setup & Prerequisites](/workshops/ai-trust/01-setup/).

| **Term** | **Definition** |
| --- | --- |
| **Baseline model** | The unmodified model, **mistral-nemo:12b**: the reference for acceptable behavior. Lab 2 uses it, so anything that goes wrong comes from the attack. |
| **Cisco AI Defense Policy Review** | The toggle that sends each prompt and each response to Cisco AI Defense, which blocks unsafe inputs before they reach the assistant and unsafe outputs before they reach the user. |
| **Demo Controls** | The left side-panel, opened with the **>** tab, whose toggles force non-compliant behavior, switch defenses on and off, and start incidents and attacks. |
| **Include Hallucinated Content in Responses** | The toggle that forces hallucinated content into responses, so you can see it detected and scored in Lab 1. |
| **Include Synthetic PII in Responses** | The toggle that forces synthetic personal data into responses, so you can see it detected and scored in Lab 1. |
| **Ollama** | The **Provider** that serves the workshop's open-weight models, including the baseline and poisoned models. |
| **Poisoned model** | **mistral-nemo:12b-poisoned**: the same model, intentionally poisoned to produce non-compliant responses such as toxic content. Comparing it with the baseline model is the heart of Lab 1. |
| **Prompt Injection Spray** | The toggle that stages prompt injection at scale: one named actor tries many techniques across several sessions for a set duration. Used in Lab 4. |
| **PseudoCo Assistant** | The workshop's multi-agent chatbot, themed for your industry. |
| **Static Emission** | The dropdown that sets the model used to calculate token cost. With the workshop's open-weight model, select **gpt-4o** so tokenomics calculate correctly. |
| **Theme** | The industry persona PseudoCo Assistant runs: FinanceAdvice, MedAdvice, Manufacturing Ops, or Retail Support. |
| **Trigger Demo Incident** | The toggle that adds latency and errors for everyone on the instance; by default, 20 s of latency and 50% errors for 600 s. Used in Lab 3. |

## Splunk Agent Observability (Lab 1 — Measure)

Used in [Lab 1 — Measure](/workshops/ai-trust/03-lab-1-measure/).

| **Term** | **Definition** |
| --- | --- |
| **Agent Graph** | A visualization of how the application's agents coordinate across models and workflows. Click an agent to see its own latency, cost, and token metrics. |
| **Agent Stream** | The live, graded, searchable record of every conversation for one application: the continuous audit trail of its behavior in production. The workshop has one stream per theme. |
| **Alert** | A notification that fires on the output of any evaluator and can be sent by email or Slack, for example when cost exceeds a set limit. |
| **Annotation Queue** | A queue of traces set aside for human review and feedback, used to continuously improve the agentic system. Each theme has a *Continuous Feedback* queue. |
| **Context adherence** | A research-backed metric that checks whether a response stays grounded in the context it was given, rather than adding claims that context does not support. |
| **Continuous evaluation** | Scoring live production traffic as it arrives, so quality and safety are measured after deployment, not only before it. |
| **Custom evaluator** | An evaluator you write for a risk specific to your business, defined by its own scoring rubric. |
| **Dataset** | A curated "golden" reference set used to grade the AI consistently, so quality and safety are measurable and repeatable. |
| **Evaluator** | A reusable scoring criterion that grades AI output and produces a metric. Evaluators run in experiments, on Agent Streams, and behind alerts. |
| **Evaluator level** | Where an evaluator applies: **Trace**, **Session**, **LLM**, or **Retriever**. |
| **Evaluator type** | What does the grading: **Luna**, a fast, lightweight evaluator, or a full **LLM**. |
| **Evaluators catalog** | The central library of evaluators, so "good" and "safe" mean the same thing across every project and team. |
| **Experiment** | An offline run that scores model versions against the same dataset and ranks them on a leaderboard, such as the baseline model against the poisoned one. It provides the evidence of which version has earned the trust to ship. |
| **Luna** | Splunk Agent Observability's family of purpose-built small language models for AI evaluation and runtime protection. Its low cost and millisecond latency make it practical to score 100% of production traffic rather than a sample. |
| **Playground** | A sandbox for experimenting with prompts and model behavior without touching the live system. |
| **Project** | The container for one AI application, holding its Agent Streams, experiments, datasets, and prompts. The workshop project is **PseudoCo Assistant**. |
| **Prompts** | A versioned, central library of the instructions that drive the AI, under change control and reusable directly in code. |
| **Scoring rubric** | The prompt inside an evaluator: explicit instructions and graded anchors that define what counts as a minor lapse and what counts as an egregious violation. |
| **Signal** | A named, prioritized issue that Splunk Agent Observability finds by scanning every logged conversation for risk patterns. You define metrics in advance; signals surface the unknown unknowns. **Signal Details** adds the root cause, evidence, recommendations, and a **Create Evaluator** option. |
| **Splunk Agent Observability** | The platform for the Measure pillar. It evaluates the whole agent trace, including the workflow, agents, tool calls, and LLM response, against research-backed and custom metrics, both before release and on live traffic. |
| **System Metrics** | The Trends charts for token usage, API failures, trace count, and agent cost. |
| **Tool-selection quality** | A research-backed metric that checks whether an agent chose the right tool for the task. |
| **Trace** | The full record of one turn: the input, the output, and every agent, tool call, and LLM call in between, with its scores. The **trace tree** shows the chain of agents behind one response. |
| **Trends** | The over-time view of quality, risk, cost, and reliability, showing whether the application is holding steady, improving, or drifting. |

## Cisco AI Defense (Lab 2 — Secure)

Used in [Lab 2 — Secure](/workshops/ai-trust/04-lab-2-secure/).

| **Term** | **Definition** |
| --- | --- |
| **Action** | What a guardrail does when it matches: **Block** stops the prompt or response, while monitoring only records it. |
| **Adaptive guardrail profile** | A guardrail defined by intent rather than keyword lists or code, written in plain language in Policy Studio. It is explainable, versioned, and governed, and it is enforced only where a runtime policy applies it. |
| **AI Assets** | The map of the AI attack surface: the agents, models, data, and third-party apps in use, including shadow AI. |
| **Built-in guardrail** | A guardrail that Cisco AI Defense provides out of the box for a common threat, such as Prompt Injection, PII, PHI, PCI, Harassment, Hate, or Profanity. |
| **Cisco AI Defense** | The platform for the Secure pillar. It inspects every prompt before the LLM reads it and every response before it reaches the user, and blocks non-compliant content. |
| **Direction** | Which side of the conversation a guardrail inspects: **Prompt**, **Response**, or both. |
| **Event Logs** | The log of Cisco AI Defense verdicts. **Event details** shows the **Rule matches**, the matching adaptive profile, and **Why was this blocked**. |
| **Filter strength** | A tunable setting, such as **Medium**, for how aggressively a guardrail fires. |
| **Guardrail** | A rule that inspects prompts or responses for one kind of risk and acts on what it finds. |
| **Guardrail profiles** | The groups of guardrails in a runtime policy, covering three dimensions: keeping attackers out, keeping data private, and keeping responses appropriate. |
| **Policy Studio** | Where adaptive guardrail profiles are created, evaluated, and fine-tuned from plain-language intent. Its **Policy Studio Assistant** asks clarifying questions about the application context, attack vectors, and risk posture before it writes a policy. |
| **Pre-LLM and post-LLM inspection** | Inspecting the prompt before the model reads it, and the response before it reaches the user. |
| **Prompt Injection - Master** | The adaptive guardrail profile reviewed in Lab 2. Its published version appears in PseudoCo Protect as **Prompt Injection**, applied to prompts with the action **Block**. |
| **PseudoCo Protect** | The runtime policy that protects PseudoCo Assistant. |
| **Publish** | The step that makes a new version of a guardrail take effect. An approved guardrail changes only through a deliberate publish. |
| **Runtime policy** | The policy that applies built-in guardrails and adaptive profiles to applications, with a direction, action, and filter strength for each. Because it sits outside the application and the model, one policy can protect every application it covers, whichever model it runs. |
| **Source text** | The exact step-by-step instructions an adaptive guardrail profile applies. |
| **Verdict** | Cisco AI Defense's decision on a prompt or a response, together with the enforcement action. It travels with the turn's governance record into Splunk. |

## Splunk Observability Cloud (Lab 3 — Observe)

Used in [Lab 3 — Observe](/workshops/ai-trust/05-lab-3-observe/).

| **Term** | **Definition** |
| --- | --- |
| **Active alerts** | The queue of every firing alert, ranked by severity. |
| **AI Troubleshooting Agent** | An AI agent that works an alert end to end: it identifies the incident, evaluates the root cause and impact with a stated confidence, and drives resolution. |
| **APM (application performance monitoring)** | Monitoring a service's requests, latency, errors, and dependencies through traces. |
| **Latency** | How long a request takes to complete, end to end. |
| **OpenTelemetry (OTel)** | The open standard for emitting traces, metrics, and logs. PseudoCo Assistant emits OpenTelemetry traces, spans, latency, and token and cost telemetry for every LLM call and tool hop. |
| **Root cause analysis** | Determining why an incident happened. The AI Troubleshooting Agent writes it in plain language, states its confidence, and says when the evidence is insufficient. |
| **SLO (service level objective)** | A target for a service's performance, such as a latency or error-rate threshold. |
| **Span** | One timed operation within a trace, such as a single LLM call, tool call, or agent step. |
| **Splunk Observability Cloud** | The platform for the Observe pillar. It instruments the AI application like any production service and follows each request across every agent, model, and operation. |

## Splunk Core and Enterprise Security (Lab 0 and Lab 4 — Govern)

Used in [Lab 0 — AI Governance Overview](/workshops/ai-trust/02-overview/) and [Lab 4 — Govern](/workshops/ai-trust/06-lab-4-govern/).

| **Term** | **Definition** |
| --- | --- |
| **Actor** | The user or identity behind an AI interaction. The Lab 4 detection correlates all of one actor's activity into a single finding. |
| **Agentic SOC** | A security operations center in which AI agents help analysts triage, investigate, and respond, while humans stay accountable for the outcome. |
| **AI Disposition** | The Triage agent's judgment on a finding, such as **True Positive**, shown in the Analyst Queue. |
| **AI Governance app** | The Splunk app that holds the AI Governance Overview and Prompt Injection Detection dashboards. |
| **AI Governance Overview dashboard** | The single pane of glass for the AI program: usage, cost, performance, safety, and compliance across every model, app, and session, with every number one click from the raw event behind it. |
| **Analyst Queue** | A prioritized, filterable list of active security findings awaiting human judgment, in Mission Control. |
| **Cisco Data Fabric** | The foundation, powered by Splunk, that ingests AI telemetry from every model, app, and session and normalizes it into one queryable record. |
| **Correlation search** | A scheduled search that defines how a threat is detected and raises a finding when it matches. Lab 4 uses **GenAI - Prompt Injection Attack Correlation**. |
| **Detection Builder Agent** | The Enterprise Security agent that builds a detection from a plain-language description and explains existing ones. |
| **Disposition** | The documented judgment on a finding, such as True Positive, recorded with an owner. |
| **Enterprise Security Agents** | The AI agents in Splunk Enterprise Security that help build detections, triage findings, and guide the response. |
| **Finding** | A security detection raised in Enterprise Security for an analyst to triage, also called a notable. |
| **Guided Response agent** | The Enterprise Security agent that works a response plan with the analyst and can run automated actions, such as disabling a user's account. |
| **Immutable audit trail** | A permanent record of every AI interaction and its governance metadata that cannot be altered and can be reconstructed on demand for an auditor, a regulator, or the board. |
| **Investigation type** | The Enterprise Security category for a kind of threat, such as **prompt_injection**, that decides which response plan a finding receives. A finding takes the type its detection carries at the moment it fires. |
| **Mission Control** | The Enterprise Security workspace where analysts triage and investigate findings. |
| **NIST 800-61** | The NIST guide to computer security incident handling. The response plan in Lab 4 follows its four phases. |
| **Prompt Injection Detection dashboard** | The AI Governance dashboard for prompt-injection attacks: traffic scanned, injections detected by severity and technique, detection confidence, top sources, and recent detections. |
| **Response plan** | The phases and tasks attached to an investigation type that guide how an analyst responds to a finding. |
| **Risk-based alerting (RBA)** | Assigning risk scores to risk objects, such as a user or a source address, so risk accumulates against an entity rather than raising an alert for every event. |
| **Security Assistant** | The Enterprise Security side panel, opened with the sparkle icon, for working with Enterprise Security Agents. |
| **SOP (standard operating procedure)** | The written procedure for handling a type of incident. In Lab 4, the SOP agent generates the response plan from an imported SOP. |
| **Splunk Core** | The Splunk platform (Splunk Cloud Platform or Splunk Enterprise) for the Govern pillar. It keeps each turn's governance record as the immutable audit trail and hosts the AI Governance app and Enterprise Security. |
| **Splunk Enterprise Security** | Splunk's security operations platform, where findings are triaged, investigated, and responded to. |
| **Triage agent** | The Enterprise Security agent that analyzes a finding and returns a determination, a severity, and a confidence score, with the justification and evidence a human needs to accept or overturn it. |
| **True Positive** | A finding judged to be real suspicious or malicious activity rather than a false alarm. |

## Industry Terms

{{% expand title="Key Terms - Financial Services" %}}
| **Term** | **Definition** |
| --- | --- |
| **FinanceAdvice** | The financial services theme of PseudoCo Assistant: a multi-agent personal-finance guidance chatbot. Its Agent Stream is **FinanceAdvice**, and its annotation queue is **FinanceAdvice Continuous Feedback**. |
| **Insider trading** | Trading on material, non-public information. One of the behaviors the Securities Fraud evaluator flags. |
| **Securities Fraud** | The financial services name for Outside of Authority, used for both the PseudoCo Assistant toggle and the custom evaluator (**securities_fraud**). It flags responses that encourage illegal trading or investment fraud, recommending insider trading or market manipulation or promising a guaranteed return, instead of general financial literacy, scam warnings, or referral to a licensed financial advisor. |
{{% /expand %}}

{{% expand title="Key Terms - Healthcare" %}}
| **Term** | **Definition** |
| --- | --- |
| **Controlled medication** | A medication whose prescribing is restricted by law because of its potential for misuse, such as hydrocodone. |
| **MedAdvice** | The healthcare theme of PseudoCo Assistant: a multi-agent medical-advice chatbot. Its Agent Stream is **MedAdvice**, its annotation queue is **MedAdvice Continuous Feedback**, and its PII toggle is labelled **Include Synthetic PII/PHI in Responses**. |
| **MRN (medical record number)** | The identifier a provider assigns to a patient's record, and a form of PHI. |
| **OTC (over-the-counter)** | A medication sold without a prescription. |
| **Prescriptive Overreach** | The healthcare name for Outside of Authority, used for both the PseudoCo Assistant toggle and the custom evaluator (**prescriptive_overreach**). It flags responses that act as a prescriber, recommending prescription-only or controlled medications or prescription-style dosing, instead of OTC products, self-care, or referral to a licensed professional. |
{{% /expand %}}

{{% expand title="Key Terms - Manufacturing" %}}
| **Term** | **Definition** |
| --- | --- |
| **Failed lot** | A production batch that failed quality inspection and must not be released without proper sign-off. |
| **Lockout/tagout** | The safety procedure that isolates and locks a machine's energy sources before maintenance, so it cannot start unexpectedly. |
| **Manufacturing Ops** | The manufacturing theme of PseudoCo Assistant: a multi-agent plant-floor operations and maintenance chatbot. Its Agent Stream is **Manufacturing**, and its annotation queue is **Manufacturing Continuous Feedback**. |
| **Safety interlock** | A device that stops a machine, or keeps it from starting, while a guard is open or a condition is unsafe. |
| **Safety Override** | The manufacturing name for Outside of Authority, used for both the PseudoCo Assistant toggle and the custom evaluator (**safety_override**). It flags responses that act as a supervisor with sign-off authority, clearing an operator to bypass a safety interlock, skip lockout/tagout, or release a failed lot, instead of troubleshooting, a line stop, or escalation to a supervisor. |
{{% /expand %}}

{{% expand title="Key Terms - Retail" %}}
| **Term** | **Definition** |
| --- | --- |
| **Concession** | Something of value granted to a customer outside normal policy, such as a refund with no return, a discount, or a warranty extension. |
| **Retail Support** | The retail theme of PseudoCo Assistant: a multi-agent retail customer-care chatbot. Its Agent Stream is **Retail**, and its annotation queue is **Retail Continuous Feedback**. |
| **Unauthorized Refund** | The retail name for Outside of Authority, used for both the PseudoCo Assistant toggle and the custom evaluator (**unauthorized_refund**). It flags responses that grant concessions the assistant has no authority to approve, announcing a refund with no return, a discount, or a warranty extension, instead of return-policy guidance, order troubleshooting, or referral to customer care. |
{{% /expand %}}
