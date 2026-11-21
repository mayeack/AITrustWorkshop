+++
title       = "Wrap-Up & Outcomes"
description = "From exploit to resolution in Splunk, with an AI agent doing the patching: five labs, five executive outcomes."
duration    = "5 min"
weight      = 70
+++

## What You Did

- **Lab 1 — Attack and Detect.** You exploited CVE-2021-41773 on an internet-facing web server. Splunk Enterprise Security joined the attack with the vulnerability inventory and raised one finding, and the AI SOC analyst triaged it before you opened it.
- **Lab 2 — Plan the Response with AI.** You started the investigation and its Exploited Vulnerability Response Plan, asked the Security Assistant how to respond, and recorded the containment a person has to do.
- **Lab 3 — Act Through SOAR, with Identity.** The Security Assistant ran PatchBot's patch action through Splunk SOAR, with your approval. For ravi.patel, Splunk Agent Observability Controls denied every change his role didn't cover. For dana.lee, PatchBot patched development and staging under a pre-approved standard change and opened a normal change for production.
- **Lab 4 — Approve the Normal Change.** You signed in with Cisco Duo as the Change Approver and approved production, and PatchBot patched and verified both production servers on its own.
- **Lab 5 — Close the Loop and Govern.** Splunk resolved the investigation from the verified fixes. The SOAR record showed the Duo role and the Cisco AI Defense MCP Scanner verdicts behind each run, the attack failed against the patched server, and Agent Observability showed every denied call and the Control that denied it.

## Outcome

**The gap.** Exploitation moves faster than patching, and an AI agent that can patch production acts with whatever access it is given, on tools someone else wrote. Without controls, speed comes at the price of change control, least privilege and proof.

**The value.** Splunk runs the response from detection to resolution, and the agent does the patching inside controls a person can see: vetted tools, a verified operator, a policy check on every call, a person for production, and a fix proven by evidence.

| **Outcome** | **What it means** | **Grounded in** |
| --- | --- | --- |
| **Exploitation Seen Early** | The SOC sees a known-exploited CVE in use, with the AI analyst's triage attached. | Splunk Enterprise Security, AI SOC analyst |
| **AI-Planned Response** | The assistant turns a finding into a patch plan the analyst approves in minutes. | Splunk Enterprise Security, Security Assistant |
| **Trusted Agents** | Vetted tools, a verified operator and a policy check on every call. | Cisco AI Defense MCP Scanner, Cisco Duo, Splunk Agent Observability Controls |
| **Governed Automation** | One action hands the work to an agent; production still waits for a person. | Splunk SOAR, Change Board |
| **Closed-Loop Proof** | The investigation resolves from verified fixes; every denial is on the record. | Splunk Enterprise Security, Splunk Agent Observability |

**What's next.** The question is no longer *whether* agents will patch production. It's whether you can prove, for every change they make, what was exploited, who it acted for, what was allowed, and who approved it.
