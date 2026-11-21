+++
title       = "Lab 5 — Govern"
description = "Follow PatchBot's requests through Splunk Agent Observability traces and Controls, the PatchBot dashboards in Splunk, and the findings in Splunk Enterprise Security."
duration    = "25 min"
weight      = 50
+++

{{< tour "lab-5" >}}

**Pillar:** Govern<br>
**Tool:** Splunk Agent Observability, Splunk Enterprise, Splunk Enterprise Security<br>
**Outcome:** Provable Governance

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SOC leaders**, **auditors** and **CISOs**. Primary question: _Can I prove what the agent did, for whom, and under which policy?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Follow one PatchBot request from the person who asked, through every tool call and policy decision, to the dashboards and findings your security team works from.
{{% /notice %}}

## Background

Every PatchBot request is a trace in Splunk Agent Observability, with one span for each model call, each policy decision and each tool call.

Every step is also a Splunk event, mapped to the Common Information Model. The PatchBot app turns them into dashboards, and Splunk Enterprise Security raises findings on the patterns a SOC should see, with risk on the person the agent acted for.

## Labs

### Lab 5.1 Every Request Is a Trace

{{< tour "lab-5.1" >}}

This lab works in Splunk Observability Cloud.

#### 5.1.1 Open the PatchBot Agent Stream

![Agent Observability navigation](/images/image-468.png)

Click on **Agent Observability -> Agent streams** (under PseudoCo Assistant).

![Agent streams](/images/image-469.png)

Click on **PatchBot**.

#### 5.1.2 Open a Trace

![PatchBot traces](/images/image-470.png)

The PatchBot Agent stream records one trace per request, so every action the agent took can be traced back to the person and the words that started it.

Tracing — each row is one request: when it ran, what was asked, and what PatchBot answered. Sessions, Traces and Spans count the conversations, requests and individual steps.

Tabs — Trends, Agent graph, Signals, Controls and Alerts read the same stream from other angles.

Click on the newest trace, **The vendor's MCP server (Vendor Advisories) returned this advisory…**.

![Trace of the poisoned vendor advisory](/images/image-471.png)

The trace shows the whole request in order: the advisory PatchBot was handed, every model call, every policy check and every tool call, with the time each took.

Span tree — the workflow and the PatchBot agent, then each step: the MCP call that fetched the advisory, the model's turns, and each tool call with the control that judged it just before it (the shield icon).

Input — exactly what PatchBot read, including the attacker's step hidden in the advisory. This is the evidence an investigator needs.

Output — what PatchBot told the operator: what was refused and why, and not to run those steps by hand.

Click on the first **deny-restricted-tools** span (the shield icon).

#### 5.1.3 Read the Policy Decision

![Control span](/images/image-472.png)

A control span is the policy decision itself, recorded in the same trace as the action it judged.

Output — the control's verdict: deny, matched.

Controls — the control by name, Triggered, what it applies to (tool calls) and a link to its definition. Policy lives in Agent Observability, not in PatchBot's code.

Click on **execute_tool stop_service**.

![Denied tool span](/images/image-473.png)

The tool span shows what the agent asked for and what came back instead: the request never reached the server.

Input — the arguments PatchBot sent: stop the EDR agent on web-prod-01.

Output — the denial, with the control that decided it and the reason the operator saw.

Click on the back arrow at the top left.

### Lab 5.2 The Controls

{{< tour "lab-5.2" >}}

#### 5.2.1 Review the Controls

![PatchBot traces](/images/image-470.png)

Click on the **Controls** tab.

![Controls on the PatchBot stream](/images/image-474.png)

The Controls tab is the agent's policy as a list a security team can read, switch and audit: every control here runs before every PatchBot tool call.

Control list — seven controls on the PatchBot Agent stream: patches outside the operator's role, any change by a viewer, production without an approved change, a patch outside its change, a patch outside the change window (steered, not denied), restricted tools (commands and service stops), and an observe-only record of every patch.

Step types, Stages and Execution — each control applies to tool calls, before they run (PRE), on the server side, so the agent cannot skip it.

### Lab 5.3 The Splunk Dashboards

{{< tour "lab-5.3" >}}

In Splunk, open the **PatchBot** app (TA-patchbot).

#### 5.3.1 Open the PatchBot App

![PatchBot app home](/images/image-475.png)

The PatchBot home page is the security team's view of the agent: every dashboard in the app, each with a live count, and the headline numbers underneath.

Dashboard cards — Exposure and Patch Pipeline, Initiators and Roles, Tool-Call Policy, Agent Tool Calls and Change Chain, each with one live number on the right.

Scoreboard — open KEV findings, median hours to remediate, tool calls denied by policy, production patches made under an approved change, and PatchBot sessions. Five numbers a CISO can track week to week.

Click on **Open Exposure and Patch Pipeline**.

#### 5.3.2 Exposure and Patch Pipeline

![Exposure and Patch Pipeline](/images/image-476.png)

The Exposure and Patch Pipeline shows how much risk is open and how fast it is closing, rated the same way PatchBot rated it.

KPI row — open findings, open critical findings, findings on a CISA KEV CVE, hosts with an open CVE, and the median hours from finding to fix.

Open findings by BOD 26-04 timeline and severity — what is due in three days, fourteen days, sixty days, or at the next upgrade.

Remediation funnel — how far each finding got: reported, change opened, change approved, patched, fixed.

Resolutions and Time to remediate — how findings closed (fixed by a change, dismissed, reopened) and whether each fix landed inside its BOD 26-04 deadline.

Click on **C** (Change Chain) in the app's left navigation.

#### 5.3.3 Change Chain

![Change Chain](/images/image-477.png)

The Change Chain follows one remediation from end to end, by finding, change or investigation ID.

Click on the **Change ID (CHG-…)** box.

![Change ID entered](/images/image-478.png)

Type the change ID PatchBot opened in Lab 3 and press **Enter**.

![Change Chain for one change](/images/image-479.png)

One change ID pulls in every event that shares its keys, so an auditor can replay a production patch from scanner report to closed change.

Completeness checklist — each hop of the chain (scanner report, finding opened, tool calls and verdicts, change opened, change approved, patch, finding fixed, change closed) and whether it is present.

Linked keys — the finding, changes, estate owner, CVE and sessions the chain holds.

Timeline — every event in order, with who acted and which sourcetype recorded it.

Click on **T** (Tool-Call Policy) in the left navigation.

#### 5.3.4 Tool-Call Policy

![Tool-Call Policy](/images/image-480.png)

The Tool-Call Policy dashboard is the Controls' report card: what was judged, what was stopped, and by which control.

KPI row — tool calls judged, denied by policy, steered, fail-closed (the Controls could not answer and PatchBot refused the call), and the share denied.

Verdicts over time and Denies by control — allow, deny and observe decisions over time, and which controls did the stopping.

Role and tool grid — for each role and tool, how many calls ran and how many were denied. A viewer's triage attempts and an operator's restricted tools show up as denied cells.

Click on **I** (Initiators and Roles) in the left navigation.

#### 5.3.5 Initiators and Roles

![Initiators and Roles](/images/image-481.png)

Initiators and Roles answers the first question in any agent incident: who was the agent acting for, and how did they sign in?

KPI row — sessions, initiators, Duo-verified sessions, role-map sessions and revoked sessions.

Sessions by role and sign-in method, and Sessions by initiator — who uses PatchBot, in which role.

Duo groups — the Duo groups behind each Duo-verified session and the PatchBot role they map to.

Initiators with denied calls — each person whose requests the Controls refused, with the tools and controls involved.

Click on **A** (Agent Tool Calls) in the left navigation.

#### 5.3.6 Agent Tool Calls

![Agent Tool Calls](/images/image-482.png)

Agent Tool Calls is the operational view of every tool call, whichever MCP server it went to.

KPI row — tool calls, distinct tools, median latency, error rate and sessions with tool calls.

Tool calls over time by tool server — the load on each MCP server.

Top tools — each tool's calls with its allow, observe, deny and steer counts and its latency.

Cisco AI Defense verdicts — the AI Defense verdict on each rendered call, where AI Defense inspected it.

Scroll down to the MCP panels.

![MCP panels](/images/image-483.png)

The MCP panels put the scanner's verdicts and every connection decision in the same place as the calls themselves.

Every tool call — the newest calls with their decision, AI Defense verdict, initiator, server and Agent Observability trace ID. The poisoned steps from Lab 4 show as denied, and AI Defense flags them as prompt injection.

MCP servers: latest Cisco MCP Scanner verdict — each server's last verdict, with the threat and the unsafe tool.

Vendor server connections — every attempt to connect the vendor's server: refused without a clean scan, or forced.

### Lab 5.4 The Findings in Enterprise Security

{{< tour "lab-5.4" >}}

In Splunk, open **Apps -> Enterprise Security**.

#### 5.4.1 Open the Analyst Queue

![Enterprise Security home](/images/image-484.png)

Click on **Mission Control**.

![Analyst Queue search](/images/image-485.png)

Type **PatchBot** in the search box and click on **Apply**.

#### 5.4.2 Review PatchBot's Findings

![PatchBot findings](/images/image-486.png)

The Analyst Queue now holds only PatchBot's findings, ready for the same triage workflow as every other security finding.

Vulnerability remediation required — one finding per estate owner and critical or high CVE, with the BOD 26-04 row and deadline in its details.

Risk score — the person's accumulated risk next to each finding.

Scroll down.

![More PatchBot findings](/images/image-487.png)

Below the vulnerabilities sit the agent-behavior findings: an unscanned or unsafe MCP server was connected, a restricted tool was attempted, and the 24-hour risk threshold was exceeded for the person PatchBot acted for.

Click on **PatchBot restricted tool attempt for dana.lee (high)**.

#### 5.4.3 Open a Finding

![Restricted tool attempt finding](/images/image-488.png)

The finding tells the analyst what happened and what it probably means, without copying the attacker's text into the case.

Description — the Controls denied restricted tool calls made for this person, which tools against which servers, the control that matched, and the PatchBot sessions. A patch operator never needs these tools, so treat it as prompt injection until proven otherwise.

Owner, Status, Urgency and Disposition — the analyst's triage fields, and Start investigation to open a case.

Details — the detection name, severity and origin: a risk-based finding built from the same events the dashboards read.

## Outcome

Lab 5 shows one record of the agent: who asked, what the agent tried, what policy decided, and what the SOC sees.

**Trace** — Every request, model call, policy decision and tool call, in order.

**Policy** — The Controls are a list a security team can read, switch and audit.

**Evidence** — Dashboards for exposure, change, policy, people and tools, and Enterprise Security findings with risk on the person.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Provable Governance.** One record ties every request to its person, every tool call to its policy decision, and every exception to a finding the security team already works, so auditors and the SOC see the same evidence.
{{% /notice %}}

<!-- exec-outcome:end -->
