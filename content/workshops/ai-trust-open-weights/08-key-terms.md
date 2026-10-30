+++
title       = "Key Terms & Definitions"
description = "A glossary of the common AI terms used across the workshop."
duration    = "Reference"
weight      = 80
+++

Common AI terms used throughout this workshop, listed alphabetically.

| **Term** | **Definition** |
| --- | --- |
| **Agentic AI** | AI systems built from agents that plan, make decisions, and take actions, such as calling tools or other agents, with little or no human involvement at each step. |
| **AI governance** | The policies, controls, and evidence an organization uses to make sure its AI is safe, compliant, and accountable, and to prove it to auditors, regulators, and its board. |
| **Data exfiltration** | Moving sensitive data out of a system without authorization. Against an AI assistant, an attacker tricks it into reading the data back in its reply or sending it somewhere the attacker controls. |
| **Drift** | A gradual change in a model's or agent's behavior away from the baseline it was tested and approved with, as models, prompts, tools, and real-world traffic change. |
| **Evaluation (evals)** | Systematically scoring AI output for quality and safety against defined metrics. Offline evaluation runs against a fixed dataset before release; online evaluation scores live production traffic continuously. |
| **Fine-tuning** | Further training a pre-trained model on a smaller, task-specific dataset to adapt it to a domain, a style, or a narrow task, such as scoring another model's output. |
| **Frontier model** | One of the largest, most capable general-purpose models from the leading AI labs. |
| **Guardrail** | A runtime control that inspects an AI system's inputs or outputs for a specific risk, such as prompt injection or PII, and blocks or flags what it finds. |
| **Hallucination** | Output that a model presents as fact but that has no basis in its data or in reality, such as an invented product, citation, or medication. |
| **Indirect prompt injection** | A prompt injection hidden inside content the AI is asked to process, such as a document, a web page, an email, or a record, rather than typed by the user. |
| **Inference** | Running a trained model on new input to produce output, such as generating a response to a prompt. Inference is where a deployed model spends its compute, and so most of its running cost. |
| **Large language model (LLM)** | A model trained on large amounts of text to understand and generate language. LLMs power most AI assistants and agents. |
| **LLM-as-a-judge** | Using a language model to score another model's output against a rubric, in place of a human reviewer. |
| **Model Context Protocol (MCP)** | An open standard for connecting AI applications and agents to external tools and data sources through MCP servers, so an agent can discover and call them in a consistent way. |
| **Multi-agent system** | An application in which several AI agents, each with its own role, coordinate to complete a task or produce one answer. |
| **Open-weight model** | A model whose trained weights are published, so it can be run, inspected, and fine-tuned on your own infrastructure. |
| **PII leakage** | An AI system revealing personally identifiable information, such as a name, date of birth, Social Security number, email address, or phone number, in its output. |
| **Prompt** | The input given to an AI model: a user's question or instruction, plus any context sent with it. |
| **Prompt injection** | Instructions embedded in a prompt that try to override the AI's own instructions, for example to reveal sensitive data or to ignore its safety rules. |
| **Small language model (SLM)** | A compact language model trained for a narrow task. It is faster and much cheaper to run than a frontier model. |
| **System prompt** | Instructions set by an application's developer that frame every conversation, such as the assistant's role, rules, and limits. Users don't normally see it, and attackers often try to extract or override it. |
| **Token** | The unit of text, roughly a word or part of a word, that a language model reads and writes. Model usage is measured and billed in tokens. |
| **Tool calling** | An AI model or agent invoking an external function, API, or data source to complete a task. |
| **Toxicity** | Abusive, harassing, hateful, or profane content in a prompt or a response. |
| **Trace** | The end-to-end record of one AI request, showing every step, such as each agent, tool call, and model call, with its timing and results. Each step is a **span**. |
| **Turn** | One exchange in a conversation with an AI: a user's prompt and the model's response. |
