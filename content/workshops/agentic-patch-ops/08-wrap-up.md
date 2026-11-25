+++
title       = "Wrap-Up & Outcomes"
description = "From exploit to resolution in Splunk, with an AI agent doing the patching: seven labs, five executive outcomes."
duration    = "5 min"
weight      = 70
+++

## What You Did

- **Lab 1 — Attack and Detect.** You exploited CVE-2021-41773 on an internet-facing web server and toured the PatchBot dashboards while Splunk Enterprise Security raised one finding and the AI SOC analyst triaged it, with its justification, tools and evidence.
- **Lab 2 — Plan and Contain.** You started the investigation and its Exploited Vulnerability Response Plan, asked the Security Assistant how to respond, and started, recorded and ended the two Contain tasks.
- **Lab 3 — Remediate Through SOAR, with Identity.** The Security Assistant ran PatchBot's patch action through Splunk SOAR, with your approval. For ravi.patel, Splunk Agent Observability Controls denied every change outside the Windows Patch Operator role. For dana.lee, PatchBot patched development and staging under a pre-approved standard change and opened a normal change for production, and you recorded it on the task.
- **Lab 4 — Review Denied Calls in Agent Observability.** You followed ravi.patel's denied run to the control span that stopped it and the Controls the security team owns.
- **Lab 5 — Review Refused Calls with Cisco AI Defense.** A third-party MCP server shipped a poisoned tool description; the Cisco AI Defense MCP Scanner flagged it, PatchBot refused to connect it, and Splunk recorded both.
- **Lab 6 — Approve the Normal Change.** You signed in with Cisco Duo as the Change Approver and approved production. PatchBot patched and verified both production servers on its own, and Splunk SOAR read the approved change back.
- **Lab 7 — Close the Loop.** Splunk resolved the investigation from the verified fixes, the attack failed against the patched server, and you closed the plan with its time to remediate on the record.

## Outcome

**The gap.** Exploitation moves faster than patching, and an AI agent that can patch production acts with whatever access it is given, on tools someone else wrote. Without controls, speed comes at the price of change control, least privilege and proof.

**The value.** Splunk runs the response from detection to resolution, and the agent does the patching inside controls a person can see: vetted tools, a verified operator, a policy check on every call, a person for production, and a fix proven by evidence.

| **Outcome** | **What it means** | **Grounded in** |
| --- | --- | --- |
| **Exploitation Seen Early** | The SOC sees a known-exploited CVE in use, with the AI analyst's triage attached. | Splunk Enterprise Security, AI SOC analyst |
| **AI-Planned Response** | The assistant turns a finding into a patch plan the analyst approves in minutes. | Splunk Enterprise Security, Security Assistant |
| **Trusted Agents** | A verified operator, a policy check on every call, and only vetted tools. | Cisco Duo, Splunk Agent Observability Controls, Cisco AI Defense MCP Scanner |
| **Governed Automation** | One action hands the work to an agent; production still waits for a person. | Splunk SOAR, Change Board |
| **Closed-Loop Proof** | The investigation resolves from verified fixes, and the plan records every step and the time to remediate. | Splunk Enterprise Security, the PatchBot app |

**What's next.** The question is no longer *whether* agents will patch production. It's whether you can prove, for every change they make, what was exploited, who it acted for, what was allowed, and who approved it.
