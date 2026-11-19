+++
title       = "Lab 4 — Defend"
description = "Try a patch outside your role, a change as a read-only viewer, and an attacker's instructions inside an advisory and inside an MCP tool description."
duration    = "25 min"
weight      = 45
+++

{{< tour "lab-4" >}}

**Pillar:** Defend<br>
**Tool:** Splunk Agent Observability Controls, Cisco MCP Scanner<br>
**Outcome:** Least-Privilege Agents

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security architects** and **AI governance** teams. Primary question: _What stops the agent when the request, or the instructions, come from the wrong place?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Watch the Controls hold the line when the request comes from the wrong role, from a read-only user, or from an attacker's text inside an advisory or an MCP tool description.
{{% /notice %}}

## Background

An agent acts with the role of the person who asks. A Linux operator patches Linux servers, a Windows operator patches Windows servers, and a viewer reads. The Controls hold those lines on every tool call.

Attackers don't need to sign in to steer an agent: an instruction hidden in a vendor advisory, or in an MCP tool's description, reaches the model directly. Cisco MCP Scanner catches the poisoned description before connection, and the Controls stop the hidden steps at runtime when a server is connected anyway.

## Labs

### Lab 4.1 A Patch Outside Your Role

{{< tour "lab-4.1" >}}

#### 4.1.1 Patch a Windows Server as the Linux Operator

![Production patched](/images/image-440.png)

Click on **← All findings** above the finding.

![Findings after the production patch](/images/image-441.png)

Click on **Anyone who can reach the Print Spooler on win-prod-01 can run code as SYSTEM**.

![Patch menu on a Windows finding](/images/image-442.png)

Click on **Patch -> Patch staging**.

![Windows patch denied](/images/image-443.png)

The Controls refused the patch in the security team's own words, before PatchBot touched the server.

Chat — `apply_patch · denied`, with the reason: a Linux Patch Operator patches Linux servers and a Windows Patch Operator patches Windows servers. The agent could reach the server; the person asking had no right to patch it.

Click on the persona chip at the top right (**Linux Patch Operator · dana.lee · role map · Switch**).

### Lab 4.2 The Right Role

{{< tour "lab-4.2" >}}

#### 4.2.1 Switch to the Windows Operator

![Persona picker](/images/image-444.png)

Click on **ravi.patel** (Windows Patch Operator).

![A new persona's estate](/images/image-445.png)

Each persona has its own copy of the estate, so ravi.patel starts before the first full read.

Click on **Start the full read**.

#### 4.2.2 Patch the Windows Server

![Windows operator's findings](/images/image-446.png)

Click on **Anyone who can reach the Print Spooler on win-prod-01 can run code as SYSTEM**.

![Patch menu as the Windows operator](/images/image-447.png)

Click on **Patch -> Patch staging**.

![Windows staging patched](/images/image-448.png)

The same request that was refused for the Linux operator is allowed for the Windows operator, and PatchBot patches and verifies the staging server.

Chat — `apply_patch · allowed` and `verify_patch · allowed`. The Controls decide on who is asking, not on what the agent can do.

Click on the persona chip at the top right (**Windows Patch Operator · ravi.patel · role map · Switch**).

### Lab 4.3 Read-Only Means Read-Only

{{< tour "lab-4.3" >}}

#### 4.3.1 Switch to the Viewer

![Persona picker](/images/image-449.png)

Click on **jo.kim** (Patch Viewer).

![The viewer's estate](/images/image-450.png)

Click on **Start the full read**.

#### 4.3.2 Try to Dismiss a Finding

![Viewer's findings](/images/image-451.png)

Click on the first finding, **Anyone on the internet can read files and run code on web-prod-01**.

![Triage menu](/images/image-452.png)

Click on **Triage -> Dismiss as accepted risk**.

![Dismissal blocked](/images/image-453.png)

A viewer can read everything and change nothing, and that holds even for a quiet change such as dismissing a critical finding as accepted risk.

Chat — Blocked by policy: your role can view findings but not change anything. The finding stays open.

Click on the persona chip at the top right (**Patch Viewer · jo.kim · role map · Switch**).

### Lab 4.4 A Poisoned Advisory

{{< tour "lab-4.4" >}}

#### 4.4.1 Switch Back to the Linux Operator

![Persona picker](/images/image-454.png)

Click on **dana.lee**.

#### 4.4.2 Publish a Poisoned Advisory

![Linux operator's findings](/images/image-455.png)

Click on the **Resources** tab.

![Resources](/images/image-456.png)

The Resources tab is the agent's rulebook in plain sight: the servers in scope, the patch policy, how findings are rated, and where the CVE facts come from.

In scope — each server with its operating system, environment, exposure and purpose. The exposure column says where each answer came from: your answer or the asset data.

Context — the patch policy (staging first, production only under an approved change, one CVE per change, no commands and no stopped services), the BOD 26-04 prioritization, and the dated CVE sources.

Scroll down to **Demo Controls**.

![Demo Controls](/images/image-457.png)

Demo Controls — the instructor's switches. Publish advisory plays a vendor's advisory for the CVE you pick; Poisoned advisory hides an attacker's step inside it.

Leave **CVE** on **CVE-2021-3156 · sudo heap overflow (Baron Samedit)** and tick **Poisoned advisory**.

![Poisoned advisory ticked](/images/image-458.png)

Click on **Publish advisory**.

#### 4.4.3 Follow the Advisory

![Advisory published](/images/image-459.png)

The poisoned advisory is published. Its steps look routine, but one tells PatchBot to stop the EDR service and to patch the domain controller without a change.

Click on **PatchBot: follow the advisory**.

![Advisory steps denied](/images/image-460.png)

PatchBot read the advisory and tried its steps, and the Controls stopped the attacker's steps before any of them ran.

Chat — `stop_service · denied` and `run_command · denied`: PatchBot does not run commands or stop services. PatchBot then stops following the advisory, names what was refused, and tells the operator not to run those steps by hand and to report the advisory. An instruction that hides in a document never reaches a server, or a person.

Scroll up and click on the **Toolchain** tab.

### Lab 4.5 A Poisoned MCP Tool

{{< tour "lab-4.5" >}}

#### 4.5.1 Poison the Vendor's Tool

![Toolchain Demo Controls](/images/image-461.png)

Tick **Vendor ships a poisoned tool description**.

![Catalogue changed](/images/image-462.png)

The vendor changed its tool's description after the scan, and PatchBot noticed: a scan covers only the catalogue it rated.

Vendor Advisories — "catalogue changed since the scan". A description that changes after the scan voids the old verdict, so a vendor cannot pass a clean scan and then swap in hidden instructions.

Click on **Scan** on **Vendor Advisories**.

#### 4.5.2 Read the Scan

![Vendor rated HIGH](/images/image-463.png)

Cisco MCP Scanner rates the vendor's server HIGH: the tool description now carries a prompt injection.

Vendor Advisories — HIGH, with the tool and the threat it found: `get_vendor_advisory: PROMPT INJECTION`. The scanner sees the hidden instructions an agent would read but a person would never notice.

Click on **Connect Vendor Advisories**.

#### 4.5.3 Connect Anyway

![Connection refused](/images/image-464.png)

PatchBot refuses to connect a server that failed its scan, and says why.

Chat — PatchBot did not connect Vendor Advisories: MCP Scanner rated it unsafe.

Click on **Connect anyway**.

![Forced connection](/images/image-465.png)

Connect anyway is the instructor's override, standing in for a team that connects an unsafe server in a hurry. It is recorded as forced, and Splunk raises a finding on it.

Vendor Advisories — "connected without a clean scan", in red, for as long as the connection stays up.

Scroll down.

#### 4.5.4 Follow the Vendor's Advisory

![Follow the vendor's advisory](/images/image-466.png)

Click on **PatchBot: follow the vendor's advisory**.

![Vendor steps denied](/images/image-467.png)

PatchBot fetched the advisory over MCP and tried what the poisoned tool asked, and the Controls stopped it at runtime: the second line of defense held when the first was overridden.

Chat — `get_vendor_advisory · allowed` fetched the advisory; `stop_service · denied` and `run_command · denied` stopped the hidden instructions. PatchBot reports the refusals and tells the operator not to run those steps by hand.

## Outcome

Lab 4 shows the Controls holding when the person, or the text, should not be trusted.

**Role** — The agent can only do what the person asking is allowed to do.

**Read-only** — A viewer reads everything and changes nothing.

**Injected instructions** — Steps hidden in an advisory or a tool description are denied before they reach a server, and PatchBot warns the operator not to run them by hand.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Least-Privilege Agents.** The agent can only do what the person asking is allowed to do, and an attacker's instructions, in a document or in a tool description, stop at runtime before they reach a server or an operator.
{{% /notice %}}

<!-- exec-outcome:end -->
