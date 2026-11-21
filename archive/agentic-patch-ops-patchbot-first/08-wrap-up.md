+++
title       = "Wrap-Up & Outcomes"
description = "An agent that patches, under controls a person can see and prove: five labs, five executive outcomes."
duration    = "5 min"
weight      = 70
+++

## What You Did

- **Lab 1 — Detect.** You gave PatchBot the one fact no scanner knows, who can reach a server, and watched it turn the scanner's reports into a short list ranked with CISA BOD 26-04. Cisco MCP Scanner rated every server behind PatchBot's tools before it used them.
- **Lab 2 — Investigate.** You opened a finding's attack path, fix and evidence, and asked PatchBot in plain language what to patch first.
- **Lab 3 — Patch.** PatchBot patched staging on its own. Production was refused until a Change Approver, not the requester, approved the change on the Change Board; then the same request went through.
- **Lab 4 — Defend.** The Controls refused a patch outside the operator's role and a viewer's attempt to dismiss a finding. Steps hidden in a vendor advisory and in an MCP tool description were denied at runtime, and PatchBot warned the operator not to run them by hand.
- **Lab 5 — Govern.** You followed PatchBot's requests through Agent Observability traces and Controls, the PatchBot dashboards in Splunk, and the findings and risk in Splunk Enterprise Security.

## Outcome

**The gap.** An agent that can patch production acts with whatever access it is given, and it reads text written by others. Without controls, speed comes at the price of change control, least privilege and evidence.

**The value.** PatchBot shows that an agent can move fast where it is safe and wait for a person where it matters, with every action checked against the role of the person who asked and every step on the record.

| **Outcome** | **What it means** | **Grounded in** |
| --- | --- | --- |
| **Risk-Ranked Exposure** | Work the vulnerabilities an attacker can reach first, and rate every tool the agent depends on before trusting it. | PatchBot, Cisco MCP Scanner |
| **Explainable Decisions** | Check the agent's reasoning: every recommendation comes with its attack path, fix and deadline. | PatchBot |
| **Controlled Change** | Production waits for a person, and nobody approves their own change. | Change Board, Splunk Agent Observability Controls |
| **Least-Privilege Agents** | The agent does only what the person asking may do, and injected instructions stop at runtime. | Splunk Agent Observability Controls, Cisco MCP Scanner |
| **Provable Governance** | One record of who asked, what the agent tried and what policy decided, for auditors and the SOC alike. | Splunk Agent Observability, Splunk Enterprise, Splunk Enterprise Security |

**What's next.** The question is no longer *whether* agents will patch production. It's whether you can prove, for every change they make, who asked, what was allowed, and who approved it.
