+++
title       = "Lab 1 — Attack and Detect"
description = "Launch a known exploit against a PseudoCo web server, then watch Splunk Enterprise Security raise the finding and the AI SOC analyst triage it."
duration    = "15 min"
weight      = 30
aliases     = ["/workshops/agentic-patch-ops/03-lab-1-detect/"]
+++

**Pillar:** Detect<br>
**Tool:** PseudoCo attack console, Splunk Enterprise Security, AI SOC analyst<br>
**Outcome:** Exploitation Seen Early

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SOC analysts** and **SOC leaders**. Primary question: _Of all the vulnerabilities we carry, which one is being exploited right now?_ This is where a scanner finding becomes an incident the SOC can see.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Launch a known exploit against a PseudoCo web server from the attack console, then find the finding Splunk Enterprise Security raises and read the AI SOC analyst's triage.
{{% /notice %}}

## Background

CVE-2021-41773 is a path-traversal flaw in Apache HTTP Server 2.4.49, listed in the CISA Known Exploited Vulnerabilities catalog. An attacker who reaches a vulnerable server can read files outside the web root and, where CGI is enabled, run commands.

PseudoCo's vulnerability scanner already reports the CVE on four web servers. In this lab you play the attacker against one of them. Splunk Enterprise Security joins the attack traffic with the vulnerability inventory and raises one finding for the active exploitation, and the AI SOC analyst triages it before an analyst opens it.

## Labs

### Lab 1.1 Launch the Exploit

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

### Lab 1.2 Find the Finding in Enterprise Security

Open Splunk in a new browser tab.

#### 1.2.1 Open Enterprise Security

![Splunk home](/images/image-603.png)

In the **Apps** panel, type **Enterprise Security** in the search box and click on **Enterprise Security**.

![Enterprise Security home](/images/image-604.png)

Click on **Mission Control**.

#### 1.2.2 Filter the Analyst Queue

![Analyst Queue](/images/image-605.png)

Type **Active exploitation** in the search box at the top right of the Analyst Queue and press Enter, then click on **Findings**.

The Analyst Queue is where detections become casework: every finding and investigation waits here for a person to own and resolve it.

Filters — The search, the type and the time range narrow the queue to one kind of finding. In a busy SOC, this is how an analyst works one incident without the noise of the rest.

Finding — The title names the exploited CVE and the server, the entity is the server under attack, and the score is the finding's risk. Status New and Owner unassigned mean nobody has picked it up yet.

AI Disposition — The AI SOC analyst's verdict, filled in on its own once its triage finishes. The analyst knows where to start before reading a single event.

{{% notice note %}}
The finding appears within a few minutes of the attack. The AI Disposition can take up to ten minutes; click **Refresh** above the queue to update it.
{{% /notice %}}

Click on **Active exploitation of CVE-2021-41773 on web-prod-01**.

### Lab 1.3 Read the AI SOC Analyst's Triage

#### 1.3.1 Review the Triage

![Finding with the AI SOC analyst's triage](/images/image-606.png)

The finding opens with the AI SOC analyst's triage already attached, so the analyst starts from a judgment and its evidence rather than from raw events.

Description — Names the attacking address, what the server answered, the CVE's CISA KEV status and every other server that shares the flaw. The finding carries the whole scope, not only the server under attack.

Owner, Status, Urgency, Sensitivity and Disposition — Who owns the finding and how it is judged. Filling them is what turns an alert into accountable casework.

Summary — The AI SOC analyst's determination, severity and confidence, with a plain-language explanation. The machine's judgment arrives with its reasoning, so a person can accept or overturn it.

Justification, Tools and Evidence — What the AI SOC analyst looked at, and which tools it used, to reach its verdict. This is the audit trail behind the AI's call.

## Outcome

Lab 1 turns a known vulnerability into a confirmed, triaged incident within minutes of the attack.

**Evidence** — Every exploit request lands in Splunk as a web event, with the attacking address and the server's answer.

**Correlation** — One detection joins the attack with the vulnerability inventory, so the finding names the exploited server and every other server that shares the flaw.

**Triage** — The AI SOC analyst judges the finding and shows its evidence before a person opens it.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Exploitation Seen Early.** The SOC sees a known-exploited vulnerability in use as it happens, with the AI SOC analyst's triage attached, instead of finding out from the next scan or the next breach.
{{% /notice %}}

<!-- exec-outcome:end -->
