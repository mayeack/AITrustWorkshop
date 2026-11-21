+++
title       = "Lab 5 — Close the Loop and Govern"
description = "See Splunk resolve the investigation from the verified fixes, try the attack again, and follow the denied calls in Splunk Agent Observability."
duration    = "20 min"
weight      = 50
aliases     = ["/workshops/agentic-patch-ops/07-lab-5-govern/"]
+++

**Pillar:** Govern<br>
**Tool:** Splunk Enterprise Security, Splunk SOAR, Splunk Agent Observability<br>
**Outcome:** Closed-Loop Proof

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SOC leaders**, **auditors** and **CISOs**. Primary question: _Can I prove the vulnerability is fixed, and prove what the agent was and wasn't allowed to do?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
See Splunk resolve the investigation from the verified fixes, read the record of each SOAR run, try the attack again, and follow the denied calls in Splunk Agent Observability.
{{% /notice %}}

## Background

PatchBot never writes to Enterprise Security. A Splunk search watches for verified fixes, and when every affected server has one, Splunk resolves the investigation itself and writes a note naming the changes and the servers.

Every SOAR run, every tool call and every policy decision is on the record: in the investigation's automation history, in Splunk Agent Observability traces, and in the PatchBot app's dashboards in Splunk.

## Labs

### Lab 5.1 See Splunk Resolve the Investigation

Go back to the Enterprise Security tab with your investigation and reload the page.

#### 5.1.1 Reload the Investigation

![Investigation resolved](/images/image-637.png)

Nobody clicked Resolve: Splunk resolved the investigation from the evidence, shortly after the last fix was verified.

Status and Disposition — Resolved, and judged a true positive. The case closes with a verdict, not just a closed ticket.

PatchBot: verified fix — Splunk's note: the fix verified on every server in scope, the changes that made it, when the last verification ran, and the search that resolved the investigation. The resolution cites its evidence, so an auditor can check it.

Notes — The containment note from Lab 2 sits beside it. A person's work and the automation's work are in one record.

{{% notice note %}}
If the investigation isn't resolved yet, wait a minute and reload: the resolve search runs every minute.
{{% /notice %}}

Click on the **Automation** tab.

### Lab 5.2 Read the Record of Each SOAR Run

#### 5.2.1 Open the First Run

![Automation](/images/image-638.png)

The Automation tab is the investigation's record of every Splunk SOAR action: what ran, for whom, and what came back.

Runs — One entry per action, the newest first: dana.lee's run and ravi.patel's run from Lab 3, each with who ran it and when.

Run details — The connector, the parameters and PatchBot's summary, then the full result. The record holds the action's evidence, not only its status.

Click on the arrow at the top right to hide the investigation details, then click on the older **AI-SOC-Analyst_PatchBot_patch-servers** run, ravi.patel's. Scroll its result down to **operator**.

#### 5.2.2 Read Who and What Was Checked

![Who PatchBot acted for](/images/image-639.png)

The result shows who PatchBot acted for and where that identity came from.

operator — ravi.patel, the Windows Patch Operator role, and the source duo_directory: Cisco Duo's directory gave the role on this call. Nobody typed the role in, so nobody can type in a better one.

Scroll down to **toolchain**.

![What PatchBot checked](/images/image-640.png)

Before it acted, PatchBot checked its own tools.

toolchain — The Cisco AI Defense MCP Scanner verdict for each of PatchBot's MCP servers, with when each was scanned. Every server must be safe, or PatchBot refuses the job before any tool runs.

### Lab 5.3 Try the Attack Again

Go back to the attack console tab and reload it.

#### 5.3.1 Launch the Exploit Again

![Attack console](/images/image-601.png)

Click on **Launch the exploit**.

#### 5.3.2 Read What the Server Answered

![Exploit refused](/images/image-641.png)

The same exploit now fails: the patched server refuses every request.

Requests — Answered Forbidden and Bad Request: no file read and no command run. The fix holds from the attacker's side too.

Now switch sides — Splunk still sees the attempts, and raises no new active-exploitation finding: the detection fires only when an exploit succeeds against a server that is still reported vulnerable.

### Lab 5.4 See What the Controls Blocked

Open Splunk Observability Cloud in a new browser tab.

#### 5.4.1 Open the PatchBot Agent Stream

![Agent Observability menu](/images/image-642.png)

Click on **Agent Observability -> Agent streams**.

![Agent Streams](/images/image-643.png)

Click on **PatchBot**.

#### 5.4.2 Open the Denied Run

![PatchBot agent stream](/images/image-644.png)

The PatchBot agent stream records every PatchBot run as a trace: each request from Splunk SOAR, each approved change and each scheduled read of the estate.

Tracing — One row per run, with its input (the request), its output and its number of spans. Every request is on the record with what came of it.

Tabs — Trends, Agent graph, Signals, Controls and Alerts show the same runs as metrics, a graph, quality signals, the policies and the alerts.

Click on the newest trace whose **Output** starts with **Denied for ravi.p…**.

![ravi.patel's run](/images/image-645.png)

The trace shows ravi.patel's run step by step, with the policy decision before each tool call.

Steps — The workflow, the PatchBot agent, and for each change it tried, a deny-patch-outside-role-os control span right before the create_change tool span. The Control decided before the tool ran.

Input and Output — The request from Splunk SOAR and PatchBot's answer: denied, with the reason.

Click on the first **deny-patch-o…** span.

#### 5.4.3 Read the Policy Decision

![Control decision](/images/image-646.png)

The control span is the policy decision itself, recorded in the trace.

Output — The decision: deny, because the Control matched. The call never reached a server.

Controls — deny-patch-outside-role-os, Triggered, and what it applies to, with a link to the Control. The security team goes from a denied call straight to the rule that denied it.

Click on the back arrow at the top left.

#### 5.4.4 Review the Controls

![PatchBot agent stream](/images/image-647.png)

Click on the **Controls** tab.

![Controls](/images/image-648.png)

The Controls tab lists the policies Splunk Agent Observability applies to PatchBot's tool calls, owned by the security team rather than written into the agent.

Control name — Role, viewer, production approval, change scope, change window, restricted tools and an observe-everything Control, each switchable. Each is a rule a security team can read, switch and audit.

Step types, Stages and Execution — Tool, PRE and Server: every Control is judged on the server before the tool call runs. If Agent Observability can't answer, PatchBot refuses the call.

### Lab 5.5 Optional: Replay the Change Chain

In Splunk, click on the Splunk logo to go back to the home page.

#### 5.5.1 Open the PatchBot App

![Splunk home](/images/image-649.png)

Type **PatchBot** in the **Apps** search box and click on **PatchBot**.

![PatchBot app](/images/image-650.png)

The PatchBot app turns PatchBot's events in Splunk into dashboards, each with a live count on its card.

Cards — Exposure and Patch Pipeline, Initiators and Roles, Tool-Call Policy, Agent Tool Calls and Change Chain, each with a one-line purpose and its count for the last 24 hours. One page tells you where to look.

Click on **Change Chain** in the left navigation.

#### 5.5.2 Read the Change Chain

![Change Chain](/images/image-651.png)

Type your investigation's ID in **Investigation ID (ES-...)**.

The Change Chain replays one remediation end to end, from the scanner report to the closed change, from events Splunk already holds.

Completeness checklist — Which hops of the chain have events: scanner report, finding opened, tool calls and verdicts, change opened, change approved, patch, finding fixed and change closed. A missing hop shows at a glance.

Linked keys — Every finding, change and investigation ID the chain holds, with its first and last event. One key finds all the others.

Timeline — Every event of the chain in order, with who acted and where it was recorded. The whole story, in Splunk's own record.

## Outcome

Lab 5 closes the loop with evidence: the fix is verified, the attack fails, and every decision can be shown.

**Resolved from evidence** — Splunk resolves the investigation only when every affected server has a verified fix.

**The attack fails** — The patched server refuses the same exploit.

**The record** — SOAR runs, traces and Controls show who asked, what was checked and what was denied.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Closed-Loop Proof.** The investigation resolves from verified fixes, not from someone's say-so, and every approval and denial is on the record for the SOC and the auditors.
{{% /notice %}}

<!-- exec-outcome:end -->
