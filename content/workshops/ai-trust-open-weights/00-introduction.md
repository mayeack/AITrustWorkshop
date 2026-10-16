+++
title       = "Introduction"
description = "Open weights give you control. Continuous evaluation and runtime enforcement turn it into trust."
duration    = "10 min"
weight      = 5
+++

*A hands-on workshop for the leaders accountable for enterprise AI — and the teams who build and run it.*

## The Problem: Control Is Not Trust

Open-weight models give enterprises greater control over how agentic systems are designed, evaluated, and governed against business-specific outcomes. You decide which weights run and where they run, and when models are served as NVIDIA NIM microservices on infrastructure you choose, prompts and data can stay inside your own environment. For agents that make decisions, call tools, and generate language that reaches customers, that control is the right place to start.

But control alone does not create trust. Owning the weights tells you *what* is running. It does not tell you *how it is behaving*. A model you selected and host yourself can still fabricate an answer with no basis in fact, leak PII or other regulated data, absorb a prompt injection that overrides its instructions, or step beyond its mandate. When you choose the model, the accountability for what it says is yours as well.

Most organizations still treat trust as a gate: evaluate before launch, sign off, and hope the behavior holds. Agentic AI does not stand still long enough for that to work. It runs at machine speed, around the clock, at a volume no human review queue can keep pace with — while models, prompts, tools, and real-world traffic keep changing underneath it. A benchmark passed at launch is not proof of how the agent behaves today.

**Trust has to be proven continuously, on every interaction — not assumed or measured after the fact.**

That gap — between the control open weights give you and the continuous proof that trust requires — is the problem this workshop closes.

---

{{% expand title="The Scenario - Healthcare" %}}
![alt text](/images/image-120.png)

PseudoCo Assistant's MedAdvice has demonstrated the value of agentic AI in healthcare: reducing the cost of routine patient interactions, accelerating access to guidance, and allowing skilled clinical staff to focus on higher-acuity cases where their expertise delivers the greatest impact.

MedAdvice is a multi-agent healthcare assistant running on Cisco Secure AI Factory with NVIDIA, using NVIDIA NIM microservices and Nemotron open models. That foundation gives the organization control over the models behind every patient conversation.

![alt text](/images/image-121.png)

But control over the model is not control over the answer. Asked about a routine ankle injury, MedAdvice appended a prescription for a Schedule II controlled substance. Nothing validated that behavior before launch, and no policy screened the response in flight. Hallucinations, PII/PHI exposure, prompt injection, and prescriptive overreach can quickly turn an efficiency gain into a clinical, regulatory, or reputational event.

**The value of MedAdvice can scale. So can the risk. Trust — proven, not assumed — is what makes the economics sustainable.**
{{% /expand %}}

---

## The Thesis: Intelligence, Evidence, Enforcement

This workshop takes a practical approach to AI trust, with a clear job for each layer of the stack.

![The Trusted AI Stack: a pyramid with Cisco Secure AI Factory with NVIDIA at the base, NVIDIA NIM inference with Nemotron open models in the middle, and Splunk Agent Observability beside Cisco Agent Security at the top, with a chevron pointing to Trusted AI as the outcome](/images/image-319.png)

> **NVIDIA Nemotron open models provide the intelligence. Continuous evaluation provides the evidence. Runtime enforcement keeps AI aligned with intended business outcomes.**

| **Layer** | **What it answers** | **Platform** |
| --- | --- | --- |
| **Intelligence** | *What runs, and where?* Open models whose weights, serving, and placement the enterprise decides | NVIDIA Nemotron open models as NVIDIA NIM microservices, on Cisco Secure AI Factory with NVIDIA |
| **Evidence** (Lab 1 — Measure) | *Is it good?* Every agent interaction measured against trust criteria such as accuracy, safety, and policy alignment, surfacing hallucination, PII leakage, prompt injection, and responses outside the assistant's authority | Splunk Agent Observability |
| **Enforcement** (Lab 2 — Secure) | *Is it safe?* Runtime guardrails on every prompt and response that stop attacks such as prompt injection and data exfiltration before they reach the model | Agent Security |

{{% notice note "The foundation: open models on infrastructure you control" %}}
**NVIDIA Nemotron** is a family of open models that NVIDIA builds for agentic AI. NVIDIA publishes the model weights, training recipes, and large portions of the training data, so enterprises can inspect and adapt the models they deploy.

**NVIDIA NIM microservices** are prebuilt, optimized inference microservices that run AI models on NVIDIA-accelerated infrastructure, whether in the cloud, the data center, on workstations, or at the edge. Because NIM runs as containers on infrastructure you choose, prompts and data can stay inside your own environment. NIM exposes industry-standard, OpenAI-compatible APIs, so agent frameworks and applications can call a self-hosted model the same way they would call a hosted one.

**Cisco Secure AI Factory with NVIDIA** is a modular reference architecture, built from Cisco AI PODs, that combines high-performance AI infrastructure with full-stack security and observability. In this workshop, it is the platform PseudoCo Assistant runs on.
{{% /notice %}}

Trust is not a single product or a one-time test. It is a loop — intelligence, evidence, enforcement — and the two labs walk through each layer of it:

1. **Intelligence answers.** PseudoCo Assistant, a multi-agent assistant themed for your industry, responds to user questions using open models.
2. **Evidence finds the risk.** Splunk Agent Observability scores every interaction and surfaces what is going wrong. Lab 1 ends with a response outside the assistant's authority, flagged by a custom evaluator for your industry.
3. **Enforcement stops the attack.** In Lab 2, a prompt injection hidden in a document tries to pull sensitive data out through the assistant. Without a guardrail, the response carries that data. With Agent Security policy review on, the request is blocked before it reaches the model.
4. **Proof closes the loop.** You re-run the attack against the live application, and the block shows up as an event in Agent Security.

{{% expand title="The Risks - Healthcare" %}}
In healthcare, Lab 1's risk is **Prescriptive Overreach**: the assistant acting like a prescriber, which the custom evaluator flags. Lab 2's attack hides instructions in a patient history to exfiltrate the patient's identifiers and medical history.
{{% /expand %}}

Because evaluation runs continuously, the loop does not stop there. As models, prompts, and real-world traffic change, the evidence keeps showing you where the next guardrail belongs.

---

## Executive Outcomes

Each lab ends in one outcome. Together they take you from evidence to enforcement.

| **Outcome** | **What it means** | **Grounded in** |
| --- | --- | --- |
| **Improved Outcomes** | Turn AI quality, safety, and cost into measurable operating metrics, establish a baseline before release, identify emerging risks in production, and continuously improve against evidence. | Splunk Agent Observability |
| **Trusted AI** | Turn written policy into machine-speed enforcement, detecting and blocking unsafe interactions before they create customer, regulatory, or reputational exposure. | Agent Security |

---
