+++
title       = "Lab 4 — Review Denied Calls in Agent Observability"
description = "Start the plan's review task and follow ravi.patel's denied run in Splunk Agent Observability to the Control that stopped it."
duration    = "10 min"
weight      = 45
aliases     = ["/workshops/agentic-patch-ops/07-lab-5-govern/"]
+++

{{< tour "lab-4" >}}

**Pillar:** Govern<br>
**Tool:** Splunk Agent Observability<br>
**Outcome:** Trusted Agents

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security architects**, **AI governance** teams and **auditors**. Primary question: _What was the agent stopped from doing, by which rule, and for whom?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Start the plan's review task, then follow ravi.patel's denied run in Splunk Agent Observability to the policy decision that stopped it and the Controls behind it.
{{% /notice %}}

## Background

Splunk Agent Observability records every PatchBot run as a trace in Splunk Observability Cloud: the request, each step, each tool call, and the policy decision made before each call.

Its Controls are the security team's policies on PatchBot's tool calls: role, viewer, production approval, change scope, change window and restricted tools. Each is judged before the tool runs, and a deny stops the call.

## Labs

### Lab 4.1 Start the Review Task

{{< tour "lab-4.1" >}}

#### 4.1.1 Start the Review Task

![Remediate task ended](/images/image-702.png)

Click on **Review denied and refused calls**.

![Review task](/images/image-703.png)

Click on **Start**.

![Review task in progress](/images/image-704.png)

The review task makes the security team look at what the agent was not allowed to do, before the change goes on.

Description — Two kinds of stopped work: calls a Splunk Agent Observability Control denied, and work PatchBot refused because a Cisco AI Defense MCP Scanner verdict wasn't clean. This lab reviews the denied calls; Lab 5 reviews the refusals.

Respond — A Splunk search of PatchBot's denied and refused calls for this investigation. The review starts from evidence.

### Lab 4.2 Find the Denied Run

{{< tour "lab-4.2" >}}

Open Splunk Observability Cloud in a new browser tab.

#### 4.2.1 Open the PatchBot Agent Stream

![Agent Observability menu](/images/image-705.png)

Click on **Agent Observability -> Agent streams**.

![Agent Streams](/images/image-706.png)

Click on **PatchBot**.

![PatchBot agent stream](/images/image-707.png)

The PatchBot agent stream records every PatchBot run as a trace: each request from Splunk SOAR, each approved change and each scheduled read of the estate.

Tracing — One row per run, with its input (the request), its output and its number of spans. Every request is on the record with what came of it.

Tabs — Trends, Agent graph, Signals, Controls and Alerts show the same runs as metrics, a graph, quality signals, the policies and the alerts.

Click on the newest trace whose **Output** starts with **Denied for ravi.p…**.

### Lab 4.3 Read the Policy Decision

{{< tour "lab-4.3" >}}

#### 4.3.1 Read the Trace

![ravi.patel's run](/images/image-708.png)

The trace shows ravi.patel's run step by step, with the policy decision before each tool call.

Steps — The workflow, the PatchBot agent and its tool calls, with a deny-patch-outside-role-os control span for each change it tried. The Control decided before the change tool could run, so it never did.

Input and Output — The request from Splunk SOAR and PatchBot's answer: denied, with the reason.

Click on the first **deny-patch-o…** span.

#### 4.3.2 Read the Control Span

![Control decision](/images/image-709.png)

The control span is the policy decision itself, recorded in the trace.

Output — The decision: deny, because the Control matched. The call never reached a server.

Controls — deny-patch-outside-role-os, Triggered, and what it applies to, with a link to the Control. The security team goes from a denied call straight to the rule that denied it.

Click on the back arrow at the top left.

### Lab 4.4 Review the Controls

{{< tour "lab-4.4" >}}

#### 4.4.1 Open the Controls

![PatchBot agent stream](/images/image-710.png)

Click on the **Controls** tab.

![Controls](/images/image-711.png)

The Controls tab lists the policies Splunk Agent Observability applies to PatchBot's tool calls, owned by the security team rather than written into the agent.

Control name — Role, viewer, production approval, change scope, change window, restricted tools and an observe-everything Control, each switchable. Each is a rule a security team can read, switch and audit.

Step types, Stages and Execution — Tool, PRE and Server: every Control is judged on the server before the tool call runs. If Agent Observability can't answer, PatchBot refuses the call.

## Outcome

Lab 4 follows a denied call from the plan's review task to the trace and the Control that denied it.

**Every run traced** — Each PatchBot run is a trace with its input, its output and every step.

**Decision before action** — A control span records the policy decision before the tool call it judged.

**Rules you can read** — The Controls are owned by the security team, switchable and auditable, not coded into the agent.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Trusted Agents.** Every call the agent makes passes a policy the security team owns, and every denial is recorded with the rule that made it.
{{% /notice %}}

<!-- exec-outcome:end -->
