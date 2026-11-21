+++
title       = "Lab 1 — Detect"
description = "PatchBot reads the estate, ranks what an attacker can reach with CISA BOD 26-04 and your own exposure answer, and Cisco MCP Scanner rates its toolchain."
duration    = "15 min"
weight      = 30
+++

{{< tour "lab-1" >}}

**Pillar:** Detect<br>
**Tool:** PatchBot, Cisco MCP Scanner<br>
**Outcome:** Risk-Ranked Exposure

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Vulnerability management** and **IT operations** leaders. Primary question: _Of everything the scanners report, what can actually hurt us, and in what order do we fix it?_ This is where a raw CVE list becomes a short, ranked plan.
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Give PatchBot the one fact no scanner knows, let it read the estate, and check its toolchain before you trust it.
{{% /notice %}}

## Background

PatchBot is the PseudoCo Assistant's patch agent. It reads scanner reports for a six-server estate, rates every finding with CISA BOD 26-04 (public exposure, known exploitation in CISA KEV, whether exploitation is automatable, and technical impact) and writes each one as what an attacker could do.

Before an agent uses a tool, someone should know what that tool tells it. PatchBot's tools sit behind MCP servers, and **Cisco MCP Scanner** reads each server's tool catalogue for hidden instructions and unsafe behavior before PatchBot trusts it.

## Labs

### Lab 1.1 Choose Who Is Asking

{{< tour "lab-1.1" >}}

#### 1.1.1 Pick a Persona

![Persona picker](/images/image-417.png)

The persona picker is how PatchBot knows who is asking: every tool call it makes carries that person's role, so the Controls judge the request rather than the bot.

Persona cards — each card is an identity with its role, from read-only viewer to estate owner. On a box without Duo, picking a card stands in for signing in, and every event records it.

Click on **dana.lee** (Linux Patch Operator).

#### 1.1.2 Answer the Exposure Question

![Exposure question](/images/image-418.png)

The exposure question asks for the one fact no scanner can see: who can actually reach a server.

Your estate — the six servers PatchBot watches, with its state. Until the first full read, PatchBot has nothing to rank.

Before the first full read — PatchBot asks who can reach web-prod-01 on port 443. Your answer becomes a documented exposure model that changes how every finding on that server is rated. If nobody answers, the full read starts on its own with the asset data.

Findings — empty until the full read finishes.

Click on **1 Anyone on the internet**.

### Lab 1.2 Read the Findings

{{< tour "lab-1.2" >}}

#### 1.2.1 Review the Ranked Findings

![Findings after the full read](/images/image-419.png)

The Findings view turns raw CVE reports into a short, ranked list of what an attacker could actually do, so the team starts with the risk that matters most.

Chat — your answer is recorded as the exposure model, and the full read reports how many CVE reports it found across the estate. This is the paper trail behind every rating that follows.

Severity bar — open findings by severity, rated with CISA BOD 26-04: public exposure, known exploitation (CISA KEV), whether exploitation is automatable, and technical impact.

PatchBot recommends — the single next action, with its reasons: in CISA KEV, a fix is ready, staging first, and the BOD 26-04 deadline.

Open list — each finding is written as what an attacker could do, with the server, the package and the CVE underneath, so a non-specialist can read the list.

Click on the **Toolchain** tab.

### Lab 1.3 Scan the Toolchain

{{< tour "lab-1.3" >}}

#### 1.3.1 Scan the MCP Servers

![Toolchain before a scan](/images/image-420.png)

The Toolchain tab lists the MCP servers behind PatchBot's tools, so you can rate every tool before the agent is allowed to use it.

MCP servers — PatchBot's own scanner and patch servers, the Splunk MCP Server, and a third-party vendor's advisory server. Each lists the tools it offers.

Scan all servers — Cisco MCP Scanner reads each server's tool catalogue, the same list the agent would read, and rates it. A rating on one of PatchBot's own tools also names the control that already stops it at runtime.

Click on **Scan all servers**.

![Toolchain after the scan](/images/image-421.png)

Every server now carries the scanner's verdict, the time of the scan and the analyzers it used, so trust in a tool is a recorded decision rather than an assumption.

Server verdicts — SAFE means the scanner found no hidden instructions or unsafe behavior in that server's tool descriptions.

Vendor Advisories — the third-party server stays not connected. PatchBot connects it only on a clean scan of the catalogue it serves right now.

Demo Controls — the instructor's switches for Lab 4. Leave them alone for now.

Click on the **Findings** tab.

## Outcome

Lab 1 turns raw scanner output into a ranked plan you can defend, and checks the agent's own tools before it uses them.

**Context** — One answer about exposure re-rates every finding on that server, and the answer is recorded as a documented exposure model.

**Rank** — CISA BOD 26-04 orders the findings by what an attacker can reach and exploit, with a deadline for each.

**Trust the toolchain** — Cisco MCP Scanner rates every MCP server before PatchBot connects it.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Risk-Ranked Exposure.** Your team works the vulnerabilities an attacker can actually reach first, ranked against CISA BOD 26-04 with your own knowledge of exposure, and every tool the agent depends on is rated before it is trusted.
{{% /notice %}}

<!-- exec-outcome:end -->
