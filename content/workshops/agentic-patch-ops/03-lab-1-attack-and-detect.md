+++
title       = "Lab 1 — Attack and Detect"
description = "Launch a known exploit against a PseudoCo web server, tour the PatchBot dashboards while Splunk Enterprise Security raises the finding, and read the AI SOC analyst's triage."
duration    = "25 min"
weight      = 30
aliases     = ["/workshops/agentic-patch-ops/03-lab-1-detect/"]
+++

{{< tour "lab-1" >}}

**Pillar:** Detect<br>
**Tool:** PseudoCo attack console, Splunk Enterprise Security, AI SOC analyst, the PatchBot app<br>
**Outcome:** Exploitation Seen Early

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SOC analysts** and **SOC leaders**. Primary question: _Of all the vulnerabilities we carry, which one is being exploited right now?_ This is where a scanner finding becomes an incident the SOC can see.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Launch a known exploit against a PseudoCo web server from the attack console, tour the PatchBot app's dashboards in Splunk while the finding arrives, then find the finding Splunk Enterprise Security raises and read the AI SOC analyst's triage.
{{% /notice %}}

## Background

CVE-2021-41773 is a path-traversal flaw in Apache HTTP Server 2.4.49, listed in the CISA Known Exploited Vulnerabilities catalog. An attacker who reaches a vulnerable server can read files outside the web root and, where CGI is enabled, run commands.

PseudoCo's vulnerability scanner already reports the CVE on four web servers. In this lab you play the attacker against one of them. Splunk Enterprise Security joins the attack traffic with the vulnerability inventory and raises one finding for the active exploitation, and the AI SOC analyst triages it before an analyst opens it. While that happens, you tour the dashboards the PatchBot app builds from PatchBot's events in Splunk.

## Labs

### Lab 1.1 Launch the Exploit

{{< tour "lab-1.1" >}}

Open the attack console at `/attack-ui` on your PseudoCo Assistant address.

#### 1.1.1 Launch the Exploit

![Attack console](/images/image-601.png)

The attack console puts you in the attacker's seat: one button sends a known exploit for CVE-2021-41773 to a PseudoCo web server from an address outside the company.

Target — The server the exploit is sent to: web-prod-01, PseudoCo's internet-facing web server. It is the server an outside attacker can reach.

Console — Shows each request the attacker sends and what the server answers. You see the attack exactly as the attacker does.

Leave the target at **web-prod-01 (internet-facing)** and click on **Launch the exploit**.

#### 1.1.2 Read What the Server Answered

![Exploit answered](/images/image-602.png)

The server answered the exploit: it is vulnerable, and the attacker read a system file and ran commands on it.

Requests — Path-traversal requests for CVE-2021-41773, answered 200 OK with the contents of a system file and the output of commands. This is what active exploitation looks like from the outside.

Now switch sides — Every request reaches Splunk as a web event, beside the vulnerability inventory the scanner sent before the attack. Everything on this page is simulated: no real system is attacked.

### Lab 1.2 Tour the PatchBot Dashboards

{{< tour "lab-1.2" >}}

{{% notice note %}}
Splunk raises the finding within a few minutes, and the AI SOC analyst can take up to ten more to triage it. Tour the PatchBot app while you wait.
{{% /notice %}}

Open Splunk in a new browser tab.

#### 1.2.1 Open the PatchBot App

![Splunk home](/images/image-654.png)

In the **Apps** panel, type **PatchBot** in the search box and click on **PatchBot**.

![PatchBot app](/images/image-655.png)

The PatchBot app turns what PatchBot, the patching agent in these labs, sends to Splunk into dashboards: one card per dashboard, each with a live count.

Cards — Exposure and Patch Pipeline, Initiators and Roles, Tool-Call Policy, Agent Tool Calls and Change Chain, each with its purpose and its count for the last 24 hours. The counts include earlier activity in your environment, and the labs add to them.

Scoreboard — Open KEV findings, median hours to remediate, tool calls denied by policy, production patches with approval and PatchBot sessions. These are the numbers the labs move.

Click on **Open Exposure and Patch Pipeline**.

#### 1.2.2 Exposure and Patch Pipeline

![Exposure and Patch Pipeline](/images/image-656.png)

Exposure and Patch Pipeline follows every finding from the scanner's report to the fix.

Open findings by timeline and severity — Every open CVE on PseudoCo's servers, grouped by its remediation deadline and severity. CVE-2021-41773 is in CISA's Known Exploited Vulnerabilities catalog, so its deadline is the shortest.

Remediation funnel and Time to remediate — How many findings move from reported to fixed, and how long that takes. Lab 7 records this incident's time to remediate on its response plan.

Click on **Initiators and Roles** in the left navigation.

#### 1.2.3 Initiators and Roles

![Initiators and Roles](/images/image-657.png)

Initiators and Roles shows who PatchBot acted for, with which role, and how that person signed in.

Sessions by role and sign-in method — Each PatchBot session, with the operator's role and whether Cisco Duo gave it. Lab 3 adds a session for each operator it runs as.

Initiators with denied calls — The people PatchBot was denied tool calls for. An agent's denials stay tied to the person it acted for.

Click on **Tool-Call Policy** in the left navigation.

#### 1.2.4 Tool-Call Policy

![Tool-Call Policy](/images/image-658.png)

Tool-Call Policy shows the verdict Splunk Agent Observability Controls gave on every PatchBot tool call.

Verdicts over time and Denies by control — Allowed and denied calls, and which Control denied what. Lab 4 follows one of these denials into its trace.

Role and tool grid — Which roles called which tools, and with what verdict. Least privilege, visible at a glance.

Click on **Agent Tool Calls** in the left navigation.

#### 1.2.5 Agent Tool Calls

![Agent Tool Calls](/images/image-659.png)

Agent Tool Calls lists every tool call PatchBot made, whichever server it went to.

Tool calls over time and Top tools — Calls by tool server, with their verdicts and latency. The agent's work is measured like any other service.

MCP servers: latest Cisco MCP Scanner verdict — The Cisco AI Defense MCP Scanner's latest verdict on each MCP server PatchBot can use. Lab 5 puts a poisoned third-party server in front of it.

Click on **Change Chain** in the left navigation.

#### 1.2.6 Change Chain

![Change Chain](/images/image-660.png)

Change Chain replays one remediation end to end: type a finding, change or investigation ID, and it lists every event in order. There is nothing to replay yet; the optional Lab 7.4 replays this incident.

### Lab 1.3 Find the Finding in Enterprise Security

{{< tour "lab-1.3" >}}

Open Splunk in another new browser tab, and keep the PatchBot app's tab open for later labs.

#### 1.3.1 Open Enterprise Security

![Splunk home](/images/image-661.png)

In the **Apps** panel, type **Enterprise Security** in the search box and click on **Enterprise Security**.

![Enterprise Security home](/images/image-662.png)

Click on **Mission Control**.

#### 1.3.2 Filter the Analyst Queue

![Analyst Queue](/images/image-663.png)

Type **Active exploitation of CVE-2021-41773** in the search box at the top right of the Analyst Queue and press Enter, then click on **Findings**.

The Analyst Queue is where detections become casework: every finding and investigation waits here for a person to own and resolve it.

Filters — The search, the type and the time range narrow the queue to one kind of finding. In a busy SOC, this is how an analyst works one incident without the noise of the rest.

Finding — The title names the exploited CVE and the server, the entity is the server under attack, and the score is the finding's risk. Scroll the table right: Status New and Owner unassigned mean nobody has picked it up yet.

AI Disposition — The AI SOC analyst's verdict, filled in on its own once its triage finishes. The analyst knows where to start before reading a single event.

{{% notice note %}}
If the AI Disposition is still empty, wait a minute and click **Refresh** above the queue: the AI SOC analyst can take up to ten minutes.
{{% /notice %}}

Click on **Active exploitation of CVE-2021-41773 on web-prod-01**.

### Lab 1.4 Read the AI SOC Analyst's Triage

{{< tour "lab-1.4" >}}

#### 1.4.1 Review the Triage

![Finding with the AI SOC analyst's triage](/images/image-664.png)

The finding opens with the AI SOC analyst's triage already attached, so the analyst starts from a judgment and its evidence rather than from raw events.

Description — Names the attacking address, what the server answered, the CVE's CISA KEV status and every other server that shares the flaw. The finding carries the whole scope, not only the server under attack.

Owner, Status, Urgency, Sensitivity and Disposition — Who owns the finding and how it is judged. Filling them is what turns an alert into accountable casework.

Summary — The AI SOC analyst's determination, severity and confidence, with a plain-language explanation. The machine's judgment arrives with its reasoning, so a person can accept or overturn it.

Under the summary, three closed sections show how the AI SOC analyst reached its verdict. Click on **Evidence**.

#### 1.4.2 Read the Evidence, Tools and Justification

![Evidence](/images/image-665.png)

The evidence comes first: the AI SOC analyst's own test of what else the activity could be.

Evidence — Its hypothesis analysis: each explanation it weighed, from a real compromise to an attempt that failed or a harmless scanner, and how strongly the data supports or contradicts each one. The alternatives are ruled out on the record, not ignored.

Click on **Tools**.

![Tools](/images/image-666.png)

Tools — Each Splunk search it ran, with its purpose and its result: the attacking address's requests per server and status, and the latest scanner reports for the CVE. The analysis is repeatable, not a black box.

Click on **Justification**.

![Justification](/images/image-667.png)

Justification — The reasoning behind the verdict, step by step: what the finding says, what the searches found and what the scanner data confirms. A person can check each step rather than trust the conclusion.

## Outcome

Lab 1 turns a known vulnerability into a confirmed, triaged incident within minutes of the attack.

**Evidence** — Every exploit request lands in Splunk as a web event, with the attacking address and the server's answer.

**Correlation** — One detection joins the attack with the vulnerability inventory, so the finding names the exploited server and every other server that shares the flaw.

**Triage** — The AI SOC analyst judges the finding and shows its justification, tools and evidence before a person opens it.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Exploitation Seen Early.** The SOC sees a known-exploited vulnerability in use as it happens, with the AI SOC analyst's triage attached, instead of finding out from the next scan or the next breach.
{{% /notice %}}

<!-- exec-outcome:end -->
