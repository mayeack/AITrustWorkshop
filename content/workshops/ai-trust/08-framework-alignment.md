+++
title       = "Framework Alignment"
description = "Where the labs demonstrate controls for the OWASP LLM Top 10, MITRE ATLAS, NIST AI RMF, ISO/IEC 42001, and the EU AI Act."
duration    = "Reference"
weight      = 75
+++

Risk, compliance, and security teams measure AI trust against a small set of public frameworks. This page maps the workshop's labs to five of them: the **OWASP Top 10 for LLM Applications (2025)**, **MITRE ATLAS**, the **NIST AI Risk Management Framework (AI RMF 1.0)**, **ISO/IEC 42001**, and the **EU AI Act**. Use it to connect what you did in each lab to the controls those teams already track.

{{% notice note %}}
**Alignment, not certification.** The labs demonstrate controls that these frameworks call for. Completing them does not make an AI system compliant or certified. That depends on how the controls are deployed, operated, and evidenced in your own environment, and on how your AI systems are classified.
{{% /notice %}}

## How to Read the Coverage

Each framework below starts with a chart of its items across the five labs, followed by a table that links each item to the lab steps where you see it.

**Demonstrated:** You do it hands-on in the lab, and the control visibly acts: a score, a block, a detection, or a finding.

**Shown:** You review the capability in the product, or it is part of a control the lab exercises, but the lab doesn't exercise that item end to end.

**Not covered:** Outside the scope of this workshop. See [Not Covered in This Workshop](#not-covered-in-this-workshop).

## OWASP Top 10 for LLM Applications (2025)

![OWASP Top 10 for LLM Applications coverage by lab. Demonstrated: LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM04 Data and Model Poisoning, and LLM09 Misinformation. Shown: LLM03 Supply Chain, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, and LLM10 Unbounded Consumption. Not covered: LLM08 Vector and Embedding Weaknesses. The table below lists the labs for each risk.](/images/image-358.png)

| **Risk** | **Coverage** | **Where you see it** |
| --- | --- | --- |
| **LLM01:2025** Prompt Injection | Demonstrated | A prompt injection sent as a structured JSON request is blocked by Cisco AI Defense before the model reads it ([Lab 2.1.3](/workshops/ai-trust/04-lab-2-secure/#213-prompt-a-data-exfiltration-attack), [Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)). A spray of injection attempts is detected and becomes a finding in Enterprise Security ([Lab 4.3.2](/workshops/ai-trust/06-lab-4-govern/#432-review-the-prompt-injection-spray), [Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). You also send a first injection attempt in [Lab 1.1.3](/workshops/ai-trust/03-lab-1-measure/#113-prompt-aberrant-behavior). |
| **LLM02:2025** Sensitive Information Disclosure | Demonstrated | The attack's request to read back personal data is blocked ([Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)). PII Signals and output PII scoring flag responses that expose personal data ([Lab 1.2.3](/workshops/ai-trust/03-lab-1-measure/#123-review-signals), [Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)), and PII detections roll up on the Overview dashboard ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard)). The Lab 4 finding counts PII exposure events without copying the prompt text into the finding ([Lab 4.2.2](/workshops/ai-trust/06-lab-4-govern/#422-review-the-detection-builder-agent)). |
| **LLM03:2025** Supply Chain | Shown | The AI asset inventory in Cisco AI Defense ([Lab 2.2.2](/workshops/ai-trust/04-lab-2-secure/#222-review-dashboard)) and model usage on the Overview dashboard ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard)) show which models and AI applications are in use. Model provenance and scanning aren't covered. |
| **LLM04:2025** Data and Model Poisoning | Demonstrated | A baseline model and an intentionally poisoned one are compared, and evaluation flags the poisoned model's behavior ([Lab 1.1.2](/workshops/ai-trust/03-lab-1-measure/#112-explore-the-baseline-vs-the-poisoned-model), [Lab 1.2.2](/workshops/ai-trust/03-lab-1-measure/#122-review-overview)). |
| **LLM05:2025** Improper Output Handling | Shown | The runtime policy inspects responses as well as prompts ([Lab 2.2.6](/workshops/ai-trust/04-lab-2-secure/#226-review-the-runtime-policy)). Validating output before a downstream system acts on it isn't covered. |
| **LLM06:2025** Excessive Agency | Shown | Your industry's Outside of Authority evaluator flags responses in which the assistant oversteps its authority ([Lab 1.1.3](/workshops/ai-trust/03-lab-1-measure/#113-prompt-aberrant-behavior), [Lab 1.3.2](/workshops/ai-trust/03-lab-1-measure/#132-review-a-custom-evaluator)), and the Agent Graph shows how the agents coordinate ([Lab 1.2.6](/workshops/ai-trust/03-lab-1-measure/#126-review-agent-graph)). Tool permission scoping and approval steps aren't covered. |
| **LLM07:2025** System Prompt Leakage | Shown | System prompt extraction is one of the attack vectors the Prompt Injection - Master guardrail profile covers ([Lab 2.2.4](/workshops/ai-trust/04-lab-2-secure/#224-review-how-the-guardrail-was-written)). |
| **LLM08:2025** Vector and Embedding Weaknesses | Not covered | — |
| **LLM09:2025** Misinformation | Demonstrated | Hallucinated content is triggered, scored by evaluators, and surfaced as Signals ([Lab 1.1.3](/workshops/ai-trust/03-lab-1-measure/#113-prompt-aberrant-behavior), [Lab 1.2.3](/workshops/ai-trust/03-lab-1-measure/#123-review-signals), [Lab 1.3.1](/workshops/ai-trust/03-lab-1-measure/#131-review-evaluators)). |
| **LLM10:2025** Unbounded Consumption | Shown | Token usage and cost are tracked ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard), [Lab 1.2.5](/workshops/ai-trust/03-lab-1-measure/#125-review-trends)), alerts can act on evaluator results such as cost ([Lab 1.2.7](/workshops/ai-trust/03-lab-1-measure/#127-review-alerts)), and a latency and error spike is triaged ([Lab 3.1.4](/workshops/ai-trust/05-lab-3-observe/#314-triage-and-resolve-an-alert)). Token quotas and rate limits aren't covered. |

## MITRE ATLAS

Technique IDs and names are from the ATLAS 2026.09 release.

![MITRE ATLAS coverage by lab. Demonstrated: AML.T0051 LLM Prompt Injection, AML.T0057 LLM Data Leakage, and AML.T0018 Manipulate AI Model. Shown: AML.T0054 LLM Jailbreak, AML.T0056 Extract LLM System Prompt, AML.T0029 Denial of AI Service, and AML.T0034 Cost Harvesting. The table below lists the labs for each technique.](/images/image-359.png)

| **Technique** | **Coverage** | **Where you see it** |
| --- | --- | --- |
| **AML.T0051** LLM Prompt Injection | Demonstrated | A direct prompt injection (AML.T0051.000) is blocked at the prompt ([Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)) and detected as a finding for the actor behind it ([Lab 4.2.1](/workshops/ai-trust/06-lab-4-govern/#421-review-the-detection-search), [Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). You also send a first injection attempt in [Lab 1.1.3](/workshops/ai-trust/03-lab-1-measure/#113-prompt-aberrant-behavior). |
| **AML.T0054** LLM Jailbreak | Shown | Jailbreaks framed as hypotheticals are among the attack vectors in Prompt Injection - Master ([Lab 2.2.4](/workshops/ai-trust/04-lab-2-secure/#224-review-how-the-guardrail-was-written)), and the Prompt Injection Detection dashboard breaks attempts down by technique ([Lab 4.3.2](/workshops/ai-trust/06-lab-4-govern/#432-review-the-prompt-injection-spray)). |
| **AML.T0056** Extract LLM System Prompt | Shown | System prompt extraction is one of the attack vectors in Prompt Injection - Master ([Lab 2.2.4](/workshops/ai-trust/04-lab-2-secure/#224-review-how-the-guardrail-was-written)). |
| **AML.T0057** LLM Data Leakage | Demonstrated | The data-exfiltration prompt is blocked before any data is read back ([Lab 2.1.3](/workshops/ai-trust/04-lab-2-secure/#213-prompt-a-data-exfiltration-attack), [Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)). Personal data in responses is scored in the Agent Stream ([Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)). |
| **AML.T0018** Manipulate AI Model | Demonstrated | A poisoned model (AML.T0018.000 Poison AI Model) is identified by comparing it with the baseline ([Lab 1.1.2](/workshops/ai-trust/03-lab-1-measure/#112-explore-the-baseline-vs-the-poisoned-model), [Lab 1.2.2](/workshops/ai-trust/03-lab-1-measure/#122-review-overview)). |
| **AML.T0029** Denial of AI Service | Shown | A synthetic latency and error incident is detected and its root cause investigated ([Lab 3.1.3](/workshops/ai-trust/05-lab-3-observe/#313-review-alerts), [Lab 3.1.4](/workshops/ai-trust/05-lab-3-observe/#314-triage-and-resolve-an-alert)). |
| **AML.T0034** Cost Harvesting | Shown | Token consumption and agent cost are tracked over time ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard), [Lab 1.2.5](/workshops/ai-trust/03-lab-1-measure/#125-review-trends)). |

## NIST AI RMF 1.0

![NIST AI RMF 1.0 coverage by lab. Demonstrated: GOVERN, MEASURE, and MANAGE. Shown: MAP. The table below lists the labs for each function.](/images/image-360.png)

| **Function** | **Coverage** | **Where you see it** | **Related subcategories** |
| --- | --- | --- | --- |
| **GOVERN** | Demonstrated | A guardrail written from plain-language intent, versioned, and changed only through a deliberate publish ([Lab 2.2.3](/workshops/ai-trust/04-lab-2-secure/#223-open-the-prompt-injection---master)–[2.2.5](/workshops/ai-trust/04-lab-2-secure/#225-review-the-policy-details)). A response plan generated from an SOP and assigned to an investigation type, with a named owner and disposition on each finding ([Lab 4.1.2](/workshops/ai-trust/06-lab-4-govern/#412-create-the-investigation-type-and-response-plan), [Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). An inventory of the models and AI applications in use ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard), [Lab 2.2.2](/workshops/ai-trust/04-lab-2-secure/#222-review-dashboard)). | GOVERN 1.4, 1.6, 2.1, 4.3 |
| **MAP** | Shown | Custom evaluators encode the risks specific to your industry's use case ([Lab 1.3.2](/workshops/ai-trust/03-lab-1-measure/#132-review-a-custom-evaluator)). | MAP 1.1 |
| **MEASURE** | Demonstrated | Evaluators score every turn for quality, safety, and privacy; Experiments compare model versions; Signals surface emergent risks; and the Annotation Queue routes traces for human review ([Lab 1.2.2](/workshops/ai-trust/03-lab-1-measure/#122-review-overview)–[Lab 1.3.2](/workshops/ai-trust/03-lab-1-measure/#132-review-a-custom-evaluator)). The Overview dashboard reports safety and compliance metrics ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard)), and the Prompt Injection Detection dashboard tracks detection rates ([Lab 4.3.2](/workshops/ai-trust/06-lab-4-govern/#432-review-the-prompt-injection-spray)). | MEASURE 2.4, 2.5, 2.6, 2.7, 2.10, 3.1 |
| **MANAGE** | Demonstrated | A high-priority risk is treated at runtime by blocking the attack ([Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)), a production incident goes from alert to root cause to resolution ([Lab 3.1.4](/workshops/ai-trust/05-lab-3-observe/#314-triage-and-resolve-an-alert)), and a finding is investigated and contained with the Guided Response agent ([Lab 4.4.2](/workshops/ai-trust/06-lab-4-govern/#442-respond-with-the-guided-response-agent)). | MANAGE 1.3, 4.1, 4.3 |

The Lab 4 response plan follows the incident response phases of NIST SP 800-61.

## ISO/IEC 42001

Control titles refer to Annex A of ISO/IEC 42001:2023. See the standard for the normative text.

![ISO/IEC 42001 Annex A coverage by lab. Demonstrated: A.6.2.4 verification and validation, A.6.2.6 operation and monitoring, A.6.2.8 recording of event logs, and A.9 use of AI systems. Shown: A.7 data for AI systems. Not covered: A.5 assessing impacts of AI systems. The table below lists the labs for each control.](/images/image-361.png)

| **Control** | **Coverage** | **Where you see it** |
| --- | --- | --- |
| **A.5** Assessing impacts of AI systems | Not covered | — |
| **A.6.2.4** AI system verification and validation | Demonstrated | Experiments rank model versions against golden datasets, and the poisoned model is flagged before it would ship ([Lab 1.2.2](/workshops/ai-trust/03-lab-1-measure/#122-review-overview)). |
| **A.6.2.6** AI system operation and monitoring | Demonstrated | The Agent Stream, Trends, and Alerts monitor production behavior ([Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)–[Lab 1.2.7](/workshops/ai-trust/03-lab-1-measure/#127-review-alerts)), a live incident is triaged in Splunk Observability Cloud ([Lab 3.1.4](/workshops/ai-trust/05-lab-3-observe/#314-triage-and-resolve-an-alert)), and the Overview dashboard rolls it all up ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard)). |
| **A.6.2.8** AI system recording of event logs | Demonstrated | Every turn is logged with governance metadata, and the detection's drilldown reconstructs one actor's activity ([Lab 4.2.1](/workshops/ai-trust/06-lab-4-govern/#421-review-the-detection-search), [Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). Traces ([Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)) and the raw request log ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard)) show the same record. |
| **A.7** Data for AI systems | Shown | Curated golden datasets grade the AI consistently ([Lab 1.2.2](/workshops/ai-trust/03-lab-1-measure/#122-review-overview)). Training data provenance and quality aren't covered. |
| **A.9** Use of AI systems | Demonstrated | A runtime policy enforces how the assistant may be used and blocks the out-of-bounds request ([Lab 2.2.6](/workshops/ai-trust/04-lab-2-secure/#226-review-the-runtime-policy), [Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)). |

## EU AI Act

The Act's obligations depend on how an AI system is classified. The articles below apply to high-risk AI systems.

![EU AI Act coverage by lab. Demonstrated: Art. 12 record-keeping, Art. 14 human oversight, Art. 15 accuracy, robustness and cybersecurity, and Art. 72 post-market monitoring. Shown: Art. 9 risk management system and Art. 73 reporting of serious incidents. Not covered: Art. 6 high-risk classification, Art. 10 data and data governance, and Art. 27 fundamental rights impact assessment. The table below lists the labs for each article.](/images/image-362.png)

| **Article** | **Coverage** | **Where you see it** |
| --- | --- | --- |
| **Art. 6** Classification rules for high-risk AI systems | Not covered | — |
| **Art. 9** Risk management system | Shown | The labs show parts of the cycle: identifying and measuring risks ([Lab 1.2.3](/workshops/ai-trust/03-lab-1-measure/#123-review-signals)), then mitigating one at runtime ([Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)). The documented risk management system itself isn't covered. |
| **Art. 10** Data and data governance | Not covered | — |
| **Art. 12** Record-keeping | Demonstrated | Every interaction is recorded as a traceable, auto-graded record ([Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)) and kept in Splunk, where it can be reconstructed per actor ([Lab 4.2.1](/workshops/ai-trust/06-lab-4-govern/#421-review-the-detection-search), [Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). Every number on the Overview dashboard opens to the raw, timestamped events behind it ([Lab 0.1.3](/workshops/ai-trust/02-overview/#013-review-ai-governance-overview-dashboard)). |
| **Art. 14** Human oversight | Demonstrated | The Triage agent's determination arrives with its evidence, so an analyst can accept or overturn it, and the finding carries an owner and a disposition ([Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). The Annotation Queue routes traces for human review ([Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)). |
| **Art. 15** Accuracy, robustness and cybersecurity | Demonstrated | Accuracy and the effects of a poisoned model are measured ([Lab 1.1.2](/workshops/ai-trust/03-lab-1-measure/#112-explore-the-baseline-vs-the-poisoned-model), [Lab 1.2.4](/workshops/ai-trust/03-lab-1-measure/#124-review-agent-stream)), an attack that manipulates the model's input is blocked ([Lab 2.3.1](/workshops/ai-trust/04-lab-2-secure/#231-send-the-attack-with-policy-review-on)), and a latency and error incident is triaged ([Lab 3.1.4](/workshops/ai-trust/05-lab-3-observe/#314-triage-and-resolve-an-alert)). |
| **Art. 27** Fundamental rights impact assessment | Not covered | — |
| **Art. 72** Post-market monitoring | Demonstrated | Trends track quality, risk, and cost over time ([Lab 1.2.5](/workshops/ai-trust/03-lab-1-measure/#125-review-trends)), and production alerts are triaged ([Lab 3.1.3](/workshops/ai-trust/05-lab-3-observe/#313-review-alerts)). |
| **Art. 73** Reporting of serious incidents | Shown | Findings are investigated and dispositioned internally ([Lab 4.4.1](/workshops/ai-trust/06-lab-4-govern/#441-investigate-with-the-triage-agent)). Reporting to authorities isn't covered. |

## Not Covered in This Workshop

These areas sit outside the labs' scope. Address them through your broader AI governance program.

**Model and component supply chain:** Provenance, integrity checks, and scanning for models and libraries (OWASP LLM03).

**Retrieval and vector stores:** Access control and isolation for embeddings and retrieval data (OWASP LLM08).

**Downstream output validation:** Checking generated code, queries, or tool payloads before another system runs them (OWASP LLM05).

**Agent permissions:** Least-privilege tool scopes and human approval for high-impact agent actions (OWASP LLM06).

**Consumption limits:** Token quotas and rate limits (OWASP LLM10).

**Impact assessment and classification:** AI system impact assessments (ISO/IEC 42001 A.5), fundamental rights impact assessments (EU AI Act Art. 27), and high-risk classification (EU AI Act Art. 6).

**Training data governance:** Provenance, quality, and rights for training data (ISO/IEC 42001 A.7, EU AI Act Art. 10).
