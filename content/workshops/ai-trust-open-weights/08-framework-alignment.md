+++
title       = "Framework Alignment"
description = "Where the labs demonstrate controls for the OWASP LLM Top 10, MITRE ATLAS, NIST AI RMF, ISO/IEC 42001, and the EU AI Act."
duration    = "Reference"
weight      = 75
+++

Risk, compliance, and security teams measure AI trust against a small set of public frameworks. This page maps the workshop's two labs to five of them: the **OWASP Top 10 for LLM Applications (2025)**, **MITRE ATLAS**, the **NIST AI Risk Management Framework (AI RMF 1.0)**, **ISO/IEC 42001**, and the **EU AI Act**. Use it to connect what you did in each lab to the controls those teams already track.

{{% notice note %}}
**Alignment, not certification.** The labs demonstrate controls that these frameworks call for. Completing them does not make an AI system compliant or certified. That depends on how the controls are deployed, operated, and evidenced in your own environment, and on how your AI systems are classified.
{{% /notice %}}

## How to Read the Coverage

Each framework below starts with a chart of its items across the two labs, followed by a table that describes each item in one line and links it to the lab steps where you see it.

**Demonstrated:** You do it hands-on in the lab, and the control visibly acts: a score, a block, or a logged event.

**Shown:** You review the capability in the product, or it is part of a control the lab exercises, but the lab doesn't exercise that item end to end.

**Not covered:** Outside the scope of this workshop. See [Not Covered in This Workshop](#not-covered-in-this-workshop).

## OWASP Top 10 for LLM Applications (2025)

![OWASP Top 10 for LLM Applications coverage by lab. Demonstrated: LLM01 Prompt Injection and LLM02 Sensitive Information Disclosure. Shown: LLM03 Supply Chain, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, LLM09 Misinformation, and LLM10 Unbounded Consumption. Not covered: LLM04 Data and Model Poisoning and LLM08 Vector and Embedding Weaknesses. The table below lists the labs for each risk.](/images/image-374.png)

| **Risk** | **Description** | **Coverage** | **Where you see it** |
| --- | --- | --- | --- |
| **LLM01:2025** Prompt Injection | Crafted input, typed directly or hidden in content the model reads, changes the model's behavior or overrides its instructions. | Demonstrated | Sent as a structured JSON request with policy review off, a prompt injection gets the model to read sensitive data back ([Lab 2.1.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#212-prompt-a-data-exfiltration-attack)). With policy review on, Agent Security blocks the same prompt before the model reads it ([Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)), and the block event names the Prompt Injection rule ([Lab 2.3.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#233-review-the-event-in-agent-security)). You also send a first injection attempt in [Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior). |
| **LLM02:2025** Sensitive Information Disclosure | The model reveals personal data, credentials, or confidential business information in its responses. | Demonstrated | You send PII in a prompt and turn on synthetic PII in responses ([Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior)); Signals surface the sensitive PII, and Output PII scores the responses that expose it ([Lab 1.2.4](/workshops/ai-trust-open-weights/03-lab-1-measure/#124-review-signals), [Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). In Lab 2, the attack's request to read back personal data succeeds with policy review off and is blocked with it on ([Lab 2.1.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#212-prompt-a-data-exfiltration-attack), [Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)). |
| **LLM03:2025** Supply Chain | Third-party models, datasets, and components are tampered with, outdated, or of unknown origin. | Shown | The Agent Security dashboard inventories the AI agents, MCP servers, models, and agent skills in the environment, with security findings for the MCP servers ([Lab 2.2.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#222-review-dashboard)). Provenance, signing and hash checks, and model scanning aren't covered. |
| **LLM04:2025** Data and Model Poisoning | Pre-training, fine-tuning, or embedding data is manipulated to plant backdoors, biases, or harmful behavior. | Not covered | — |
| **LLM05:2025** Improper Output Handling | Model output reaches downstream systems without validation, enabling attacks such as cross-site scripting, SQL injection, or code execution. | Shown | The runtime policy's guardrails inspect responses as well as prompts ([Lab 2.2.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#223-review-the-prompt-injection-guardrail)). Validating output before a downstream system acts on it isn't covered. |
| **LLM06:2025** Excessive Agency | An LLM-based system with too much functionality, permission, or autonomy takes damaging actions through its tools. | Shown | Your industry's Outside of Authority evaluator flags responses in which the assistant oversteps its authority ([Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior), [Lab 1.3.2](/workshops/ai-trust-open-weights/03-lab-1-measure/#132-review-a-custom-evaluator)), and the trace tree shows which agents handled each turn ([Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). Tool permission scoping and approval steps aren't covered. |
| **LLM07:2025** System Prompt Leakage | The system prompt holds secrets, rules, or logic that an attacker can extract and misuse. | Shown | The prompt injection you send asks the assistant to reveal its full system prompt ([Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior)), and its trace shows exactly what was asked and answered ([Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). The lab doesn't show a control acting on the extraction attempt, and keeping secrets and authorization logic out of system prompts isn't covered. |
| **LLM08:2025** Vector and Embedding Weaknesses | Weaknesses in how embeddings are generated, stored, or retrieved let attackers inject content or reach data they shouldn't. | Not covered | — |
| **LLM09:2025** Misinformation | The model produces false or misleading content that sounds credible, such as hallucinated facts or sources. | Shown | Evaluators such as context adherence score every turn, and their trends appear on the Overview ([Lab 1.2.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#123-review-agent-observability-overview)); the evaluator catalog holds the reusable checks ([Lab 1.3.1](/workshops/ai-trust-open-weights/03-lab-1-measure/#131-review-evaluators)). The labs don't trigger a hallucination. |
| **LLM10:2025** Unbounded Consumption | Uncontrolled use of the model drives up cost, degrades the service, or enables model extraction. | Shown | Token usage and estimated agent cost are tracked ([Lab 1.2.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#123-review-agent-observability-overview), [Lab 1.2.6](/workshops/ai-trust-open-weights/03-lab-1-measure/#126-review-trends)), and the Beyond Tokens panel shows how to measure what the same tokens cost in GPU power and hardware on your own AI Factory ([Lab 1.2.6](/workshops/ai-trust-open-weights/03-lab-1-measure/#126-review-trends)). Token quotas and rate limits aren't covered. |

## MITRE ATLAS

Technique IDs and names are from the ATLAS 2026.10 release. In 2026.09 and earlier, AML.T0085.003 was AML.T0056 Extract LLM System Prompt, and AML.T0085.002 was AML.T0057 LLM Data Leakage.

![MITRE ATLAS coverage by lab. Demonstrated: AML.T0051 LLM Prompt Injection and AML.T0085.002 Data from AI Services: Conversation Context and Memory. Shown: AML.T0085.003 Data from AI Services: System Instructions, AML.T0029 Denial of AI Service, and AML.T0034 Cost Harvesting. Not covered: AML.T0054 LLM Jailbreak and AML.T0018 Manipulate AI Model. The table below lists the labs for each technique.](/images/image-375.png)

| **Technique** | **Description** | **Coverage** | **Where you see it** |
| --- | --- | --- | --- |
| **AML.T0051** LLM Prompt Injection | An adversary crafts prompts that make an LLM act in unintended ways, such as ignoring its original instructions. | Demonstrated | A direct prompt injection (AML.T0051.000) gets through with policy review off ([Lab 2.1.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#212-prompt-a-data-exfiltration-attack)), is blocked at the prompt with it on ([Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)), and is logged as a Prompt Injection block event ([Lab 2.3.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#233-review-the-event-in-agent-security)). You also send a first injection attempt in [Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior). |
| **AML.T0054** LLM Jailbreak | An adversary gets an LLM to ignore or override its safety behavior and guardrails. | Not covered | — |
| **AML.T0085.003** Data from AI Services: System Instructions | An adversary collects the non-public instructions that configure a model or agent, such as its system prompt. | Shown | The prompt injection you send asks the assistant to reveal its system prompt verbatim, and its trace records the attempt ([Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior), [Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). The lab doesn't show a control acting on it. |
| **AML.T0085.002** Data from AI Services: Conversation Context and Memory | An adversary collects sensitive information from an AI service's current or stored conversation context and memory. | Demonstrated | With policy review off, the data-exfiltration prompt makes the model read personal data back in its response, the exfiltration path ATLAS tracks as AML.T0136 Exfiltration via AI User Interface ([Lab 2.1.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#212-prompt-a-data-exfiltration-attack)). With policy review on, it is blocked before any data is read back ([Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)). Personal data in responses is scored in the Agent Stream ([Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). |
| **AML.T0018** Manipulate AI Model | An adversary changes a model artifact or its bundled components, such as weights or prompt templates, to alter its behavior. | Not covered | — |
| **AML.T0029** Denial of AI Service | An adversary floods an AI service with requests or compute-heavy inputs to degrade or shut it down. | Shown | Visibility only: System Metrics count API failures and trace volume over time, where the degradation a denial-of-service attack causes would show up ([Lab 1.2.6](/workshops/ai-trust-open-weights/03-lab-1-measure/#126-review-trends)). No lab generates load or a fault. Rate and resource limits (AML.M0004, AML.M0036) aren't covered. |
| **AML.T0034** Cost Harvesting | An adversary drives a victim's AI services beyond normal capacity to run up their cost. | Shown | Cost visibility only: token use and estimated agent cost are tracked over time ([Lab 1.2.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#123-review-agent-observability-overview), [Lab 1.2.6](/workshops/ai-trust-open-weights/03-lab-1-measure/#126-review-trends)), and the Beyond Tokens panel adds GPU utilization and power. A spike from a cost-harvesting campaign would show up there, but no lab generates one. Budgets, quotas, and rate limits (AML.M0004, AML.M0036) aren't covered. |

## NIST AI RMF 1.0

![NIST AI RMF 1.0 coverage by lab. Demonstrated: MEASURE and MANAGE. Shown: GOVERN and MAP. The table below lists the labs for each function.](/images/image-376.png)

| **Function** | **Description** | **Coverage** | **Where you see it** | **Related subcategories** |
| --- | --- | --- | --- | --- |
| **GOVERN** | A culture of risk management is cultivated and present. | Shown | You review an inventory of the AI agents, MCP servers, and models in use ([Lab 2.2.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#222-review-dashboard)) and the application's runtime policy, which groups its guardrails into Security, Privacy, and Safety ([Lab 2.2.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#223-review-the-prompt-injection-guardrail)). Roles, accountability, and policy approval aren't covered. | GOVERN 1.4, 1.6 |
| **MAP** | Context is recognized and risks related to context are identified. | Shown | Your industry's custom evaluator turns the limit the assistant must not cross into a scored rubric ([Lab 1.3.2](/workshops/ai-trust-open-weights/03-lab-1-measure/#132-review-a-custom-evaluator)). | MAP 1.1, 3.3 |
| **MEASURE** | Identified risks are assessed, analyzed, or tracked. | Demonstrated | The behavior you prompt ([Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior)) is scored turn by turn for safety and privacy in the Agent Stream, Signals surface emergent risks, and Trends track quality, risk, and cost over time ([Lab 1.2.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#123-review-agent-observability-overview)–[Lab 1.3.2](/workshops/ai-trust-open-weights/03-lab-1-measure/#132-review-a-custom-evaluator)). | MEASURE 2.4, 2.6, 2.10, 3.1 |
| **MANAGE** | Risks are prioritized and acted upon based on a projected impact. | Demonstrated | A high-priority risk is treated at runtime: the data-exfiltration attack that got through in [Lab 2.1.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#212-prompt-a-data-exfiltration-attack) is blocked once policy review is on ([Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)). Incident response and recovery aren't covered. | MANAGE 1.3 |

## ISO/IEC 42001

Control titles refer to Annex A of ISO/IEC 42001:2023. See the standard for the normative text. ISO/IEC 42001 is a management-system standard: certification audits an organization's AI management system (clauses 4–10, including AI policy, AI risk assessment and treatment, the Statement of Applicability, impact assessment, internal audit, and management review) together with the Annex A controls it selects. The rows below are a small selection of Annex A's controls, and the labs don't produce management-system evidence.

![ISO/IEC 42001 Annex A coverage by lab. Demonstrated: A.6.2.6 operation and monitoring and A.6.2.8 recording of event logs. Shown: A.6.2.4 verification and validation and A.9.4 intended use of the AI system. Not covered: A.5 assessing impacts of AI systems and A.7 data for AI systems. The table below lists the labs for each control.](/images/image-377.png)

| **Control** | **Description** | **Coverage** | **Where you see it** |
| --- | --- | --- | --- |
| **A.5** Assessing impacts of AI systems | Assess how an AI system could affect individuals, groups, and society over its life cycle. | Not covered | — |
| **A.6.2.4** AI system verification and validation | Define and document how the AI system is verified and validated, and the criteria for its use. | Shown | The evaluator catalog holds reusable checks that can grade the assistant at every point in its life cycle ([Lab 1.3.1](/workshops/ai-trust-open-weights/03-lab-1-measure/#131-review-evaluators)), and a custom evaluator turns your industry's risk into a graded rubric ([Lab 1.3.2](/workshops/ai-trust-open-weights/03-lab-1-measure/#132-review-a-custom-evaluator)). The labs score production traffic only; defining verification and validation criteria and a release gate isn't covered. |
| **A.6.2.6** AI system operation and monitoring | Define what is needed to operate and monitor the AI system, including performance, repairs, and updates. | Demonstrated | The behavior you prompt ([Lab 1.1.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#113-prompt-aberrant-behavior)) appears in the Overview, Signals, Agent Stream, and Trends, which monitor production behavior, reliability, and cost ([Lab 1.2.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#123-review-agent-observability-overview)–[Lab 1.2.6](/workshops/ai-trust-open-weights/03-lab-1-measure/#126-review-trends)). |
| **A.6.2.8** AI system recording of event logs | Decide at which life cycle phases event logs are recorded, at least while the system is in use. | Demonstrated | Your blocked attack is recorded in Agent Security's Event Logs with its rule, action, and message type ([Lab 2.3.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#233-review-the-event-in-agent-security)). Every turn is also recorded as a trace ([Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). |
| **A.7** Data for AI systems | Manage the data used to develop and run AI systems, including its quality, provenance, and preparation. | Not covered | — |
| **A.9.4** Intended use of the AI system | Use the AI system as its documentation intends. | Shown | Your industry's custom evaluator flags responses outside the assistant's authority ([Lab 1.3.2](/workshops/ai-trust-open-weights/03-lab-1-measure/#132-review-a-custom-evaluator)), and a runtime policy blocks a request outside its intended use: a prompt injection asking it to read back personal data ([Lab 2.2.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#223-review-the-prompt-injection-guardrail), [Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)). Documented processes and objectives for responsible use (A.9.2, A.9.3) and a documented intended-use statement aren't covered. |

## EU AI Act

The Act's obligations depend on how an AI system is classified. The articles below apply to high-risk AI systems, except Art. 50, which applies more broadly.

![EU AI Act coverage by lab. Demonstrated: Art. 12 record-keeping and Art. 15 accuracy, robustness and cybersecurity. Shown: Art. 9 risk management system, Art. 14 human oversight, and Art. 72 post-market monitoring. Not covered: Art. 6 high-risk classification, Art. 10 data and data governance, Art. 27 fundamental rights impact assessment, Art. 50 transparency obligations, and Art. 73 reporting of serious incidents. The table below lists the labs for each article.](/images/image-378.png)

| **Article** | **Description** | **Coverage** | **Where you see it** |
| --- | --- | --- | --- |
| **Art. 6** Classification rules for high-risk AI systems | Sets the rules that decide whether an AI system is high-risk. | Not covered | — |
| **Art. 9** Risk management system | A risk management system runs across the high-risk system's whole life cycle. | Shown | The labs show parts of the cycle: identifying and measuring risks ([Lab 1.2.4](/workshops/ai-trust-open-weights/03-lab-1-measure/#124-review-signals)), then mitigating one at runtime ([Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)). The documented risk management system itself isn't covered. |
| **Art. 10** Data and data governance | Training, validation, and test data meet quality criteria and are governed. | Not covered | — |
| **Art. 12** Record-keeping | The system automatically records events (logs) over its lifetime. | Demonstrated | Your blocked attack is recorded as a timestamped event in Agent Security, with the rule that fired ([Lab 2.3.3](/workshops/ai-trust-open-weights/04-lab-2-secure/#233-review-the-event-in-agent-security)). Every interaction is also recorded as a traceable, auto-graded record ([Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). Log retention periods (Art. 19 for providers; at least six months for deployers under Art. 26(6)) aren't covered. |
| **Art. 14** Human oversight | The system is designed so people can oversee it while it is in use, including overriding or stopping it. | Shown | People can monitor the assistant while it runs and spot unexpected behavior: every turn is traced and scored, and Signals surface anomalies ([Lab 1.2.4](/workshops/ai-trust-open-weights/03-lab-1-measure/#124-review-signals), [Lab 1.2.5](/workshops/ai-trust-open-weights/03-lab-1-measure/#125-review-agent-stream)). The trace view shows exactly what was asked and answered, so a reviewer can interpret the output. Overriding, reversing, or stopping the assistant's output while it is in use (Art. 14(4)(d)–(e)) isn't covered. |
| **Art. 15** Accuracy, robustness and cybersecurity | The system achieves appropriate accuracy, robustness, and cybersecurity throughout its life cycle. | Demonstrated | Cybersecurity: an attack that manipulates the model's input gets through without a guardrail and is blocked with one ([Lab 2.1.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#212-prompt-a-data-exfiltration-attack), [Lab 2.3.2](/workshops/ai-trust-open-weights/04-lab-2-secure/#232-send-the-attack-again)). Accuracy: responses are scored by evaluators such as context adherence ([Lab 1.2.3](/workshops/ai-trust-open-weights/03-lab-1-measure/#123-review-agent-observability-overview)). Resilience to errors and faults, such as redundancy or fail-safe plans (Art. 15(4)), and declaring accuracy levels in the instructions for use (Art. 15(3)) aren't covered. |
| **Art. 27** Fundamental rights impact assessment | Certain deployers assess the impact on fundamental rights before first use. | Not covered | — |
| **Art. 50** Transparency obligations for providers and deployers of certain AI systems | People are told when they are interacting with an AI system, and AI-generated content is marked. | Not covered | — |
| **Art. 72** Post-market monitoring | The provider monitors the system after it is placed on the market, under a documented plan. | Shown | Trends and System Metrics track quality, risk, reliability, and cost over time ([Lab 1.2.6](/workshops/ai-trust-open-weights/03-lab-1-measure/#126-review-trends)). These supply the performance data a post-market monitoring system analyses. The documented system and its post-market monitoring plan (part of the Annex IV technical documentation) aren't covered. |
| **Art. 73** Reporting of serious incidents | The provider reports serious incidents to market surveillance authorities. | Not covered | — |

## Not Covered in This Workshop

These areas sit outside the labs' scope. Address them through your broader AI governance program.

**Model provenance and integrity:** Provenance, signing and hash checks, and scanning for models and libraries (OWASP LLM03).

**Model poisoning and tampering:** Poisoned training or fine-tuning data, and tampered weights or prompt templates (OWASP LLM04, MITRE ATLAS AML.T0018).

**Jailbreaks:** Prompts that talk a model out of its safety rules (MITRE ATLAS AML.T0054).

**Retrieval and vector stores:** Access control and isolation for embeddings and retrieval data (OWASP LLM08).

**Downstream output validation:** Checking generated code, queries, or tool payloads before another system runs them (OWASP LLM05).

**Agent permissions:** Least-privilege tool scopes and human approval for high-impact agent actions (OWASP LLM06).

**Consumption limits:** Token quotas and rate limits (OWASP LLM10).

**Impact assessment and classification:** AI system impact assessments (ISO/IEC 42001 A.5), fundamental rights impact assessments (EU AI Act Art. 27), and high-risk classification (EU AI Act Art. 6).

**Training data governance:** Provenance, quality, and rights for training data (ISO/IEC 42001 A.7, EU AI Act Art. 10).

**Responsible-use documentation:** Processes and objectives for the responsible use of AI systems (ISO/IEC 42001 A.9.2, A.9.3).

**Incident investigation and reporting:** Investigating a security finding, responding to it, and reporting serious incidents to authorities (EU AI Act Art. 73).

**Transparency to users:** Telling people they are interacting with an AI system, and marking AI-generated content (EU AI Act Art. 50).
