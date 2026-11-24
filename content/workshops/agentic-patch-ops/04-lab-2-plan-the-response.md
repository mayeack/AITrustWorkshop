+++
title       = "Lab 2 — Plan the Response with AI"
description = "Start the investigation, read the response plan it brings, ask the Security Assistant how to respond, and complete the containment tasks."
duration    = "15 min"
weight      = 35
aliases     = ["/workshops/agentic-patch-ops/04-lab-2-investigate/"]
+++

{{< tour "lab-2" >}}

**Pillar:** Plan<br>
**Tool:** Splunk Enterprise Security, Security Assistant<br>
**Outcome:** AI-Planned Response

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SOC analysts** and **incident responders**. Primary question: _What do we do about it, in what order, and who does each step?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Start an investigation from the finding, read the response plan it brings, ask the Security Assistant how to respond, and complete the plan's containment tasks.
{{% /notice %}}

## Background

An investigation in Splunk Enterprise Security brings its response plan with it. The Exploited Vulnerability Response Plan has four phases: contain the attacker, remediate every affected server, verify the fix, and close. Some tasks run a search, some run a Splunk SOAR action, and some are for a person.

The Security Assistant reads the investigation, its findings and its notes, and answers in plain language. It also follows the plan: it won't start patching until the manual containment task is done and recorded.

## Labs

### Lab 2.1 Start the Investigation

{{< tour "lab-2.1" >}}

#### 2.1.1 Start the Investigation

![Finding with the AI SOC analyst's triage](/images/image-606.png)

Click on **Start investigation** at the top of the finding.

![Investigation overview](/images/image-607.png)

The investigation opens on its Overview: one case for the finding, the AI's summary and the attack's techniques, under an ID the whole team can refer to.

Summary — The AI SOC analyst's summary of the investigation, with its disposition and confidence. It already scopes the response to every server that shares the flaw, not only the one under attack.

MITRE ATT&CK map — The techniques the detection observed, placed on the ATT&CK matrix. It puts the incident in the language threat teams and auditors share.

Click on **Response**.

#### 2.1.2 Review the Response Plan

![Response plan](/images/image-608.png)

The Response tab holds the Exploited Vulnerability Response Plan, attached by the investigation type, so every exploited vulnerability is worked the same way.

Exploited Vulnerability Response Plan — Four phases, Contain, Remediate, Verify and Close, each with its tasks and its progress. The team's runbook becomes tracked work.

Task — The selected task's description, what it offers under Respond, and its notes and files. Each task says what done looks like and records who did it.

Owner, Status, Urgency, Sensitivity and Disposition — The investigation's triage fields and notes, beside the plan. The case and the work stay on one screen.

Click on **Remediate**.

![Remediate task](/images/image-609.png)

Click on **Patch every affected server through PatchBot**.

The Remediate task is where the plan hands the patching to automation: its action runs PatchBot through Splunk SOAR.

Description — How to run the action and what happens: the operator's role comes from Cisco Duo, Splunk Agent Observability Controls judge every call, non-production servers fall under a pre-approved standard change, and production gets a normal change. The policy is written into the plan, where the analyst reads it.

Respond — The **patch servers - PatchBot** action and a Splunk search of PatchBot's runs for this CVE. The plan carries the fix itself, not only the instruction.

### Lab 2.2 Ask the Security Assistant

{{< tour "lab-2.2" >}}

#### 2.2.1 Ask How to Respond

![Security Assistant](/images/image-610.png)

Click on the **Security Assistant** orb at the right edge of the page.

![Planning prompt](/images/image-611.png)

Type the example prompt in the Security Assistant and press Enter.

**Example prompt:** How should I respond to the active exploitation of CVE-2021-41773 on web-prod-01?

#### 2.2.2 Review the Answer

![Security Assistant answer](/images/image-612.png)

The Security Assistant reads the investigation before it answers, so its recommendation is about this incident rather than general advice.

Get Findings, Get Notes and Get Object By ID — The tools the assistant used to read the investigation, its findings and its notes. Every answer starts from the case's own data.

Recommended response — Contain the attacking address first, patch every server where the CVE is open through PatchBot's patch servers action, get the production change approved, then verify and close. It follows the response plan and scopes the fix to the whole estate.

{{% notice note %}}
The assistant's wording changes from run to run. Look for the order of the steps: contain, patch every affected server, approve production, verify.
{{% /notice %}}

Click on **Confirm the exploitation and its scope** in the plan.

### Lab 2.3 Contain the Attack

{{< tour "lab-2.3" >}}

#### 2.3.1 Confirm the Scope

![Confirm task](/images/image-613.png)

The first containment task asks a person to confirm the attack and its scope before anything is patched.

Description — What to confirm: which servers the attacking address reached, and every server where the CVE is still open. Those are the servers Remediate patches.

Respond — Two Splunk searches: the requests from the attacking address, and the servers where the CVE is open. The evidence for the decision is one click away.

Click on **Start**.

![Confirm task in progress](/images/image-614.png)

Click on **End**.

#### 2.3.2 Record the Block

![Block task](/images/image-615.png)

Click on **Block the source address by hand**.

The block task is a person's job by design: this lab has no firewall connector, so a person blocks the address and records it, and the AI may not report it as done.

Click on **Start**.

![Block task in progress](/images/image-616.png)

Click in the **Notes** box and type where the address was blocked, by whom and when.

**Example note:** Blocked 203.0.113.66 at the perimeter firewall. Blocked by the on-call SOC analyst at the time of this note.

![Block note](/images/image-617.png)

Click on **Save**.

![Block note saved](/images/image-618.png)

Click on **End**.

![Contain complete](/images/image-619.png)

Contain is complete, and the plan shows who did each task and how the block was recorded.

Contain — Both tasks carry a check mark and their owner, and the phase shows it is done. The plan's progress moves on with them.

Notes — The block note, saved on its task. The Security Assistant reads it before it acts.

{{% notice note %}}
The Security Assistant checks the Contain tasks before it starts patching: if the block task isn't ended with its note, it refuses to run the patch action.
{{% /notice %}}

## Outcome

Lab 2 turns a finding into a response plan that people and the AI work through together.

**Plan** — The investigation type attaches the plan, so every exploited vulnerability is handled the same way.

**Ask** — The Security Assistant reads the investigation and recommends the response, scoped to every affected server.

**Contain** — Containment stays a person's job, recorded as a task with a note.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — AI-Planned Response.** The assistant turns a finding into a patch plan the analyst approves in minutes, while the steps only a person can take stay with a person and are recorded.
{{% /notice %}}

<!-- exec-outcome:end -->
