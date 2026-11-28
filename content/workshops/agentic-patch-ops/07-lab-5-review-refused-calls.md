+++
title       = "Lab 5 — Review Refused Calls with Cisco AI Defense"
description = "Watch the Cisco AI Defense MCP Scanner flag a poisoned third-party MCP server, see PatchBot refuse to connect it, and find the refusal in Splunk."
duration    = "10 min"
weight      = 50
aliases     = []
+++

{{< tour "lab-5" >}}

**Pillar:** Vet<br>
**Tool:** Cisco AI Defense MCP Scanner, PatchBot, the PatchBot app in Splunk<br>
**Outcome:** Trusted Agents

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security architects**, **AI governance** teams and **third-party risk** owners. Primary question: _How do we know the tools an AI agent uses haven't been tampered with?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
See the Cisco AI Defense MCP Scanner's verdicts on the MCP servers PatchBot uses, watch it flag a poisoned third-party MCP server, see PatchBot refuse to connect that server, find the refusal in Splunk, and end the review task.
{{% /notice %}}

## Background

An AI agent works through tools, and with MCP those tools come from servers: the agent's own, and increasingly a vendor's. A tool's description is read by the model, so a poisoned description can carry instructions the agent was never meant to follow.

PatchBot trusts an MCP server only on a clean Cisco AI Defense MCP Scanner verdict of its current tool catalogue. It refuses a job while one of its own servers is unsafe, and it won't connect a third-party server the scanner flags.

## Labs

### Lab 5.1 Open PatchBot's Toolchain

{{< tour "lab-5.1" >}}

{{% notice info "A synthetic application" %}}
PatchBot is a synthetic AI patching agent built for this workshop. It stands in for the AI agents and patch-management tools your teams use, so the labs show only what you need of PatchBot itself: the focus is the Splunk and Cisco controls around it.
{{% /notice %}}

{{% notice warning "Important" %}}
Get the workshop code from your instructor before you start. Duo must bring you back within 5 minutes of **Continue with Duo**, or PatchBot shows an error and you sign in again.
{{% /notice %}}

Open `/login/duo` on your PseudoCo Assistant address.

#### 5.1.1 Sign In as dana.lee

![Sign in with Duo](/images/image-712.png)

Type **dana.lee** in **Username** and click on **Continue with Duo**.

![Duo passcode](/images/image-713.png)

Type the workshop code your instructor gave you and click on **Verify**.

![PseudoCo Assistant](/images/image-714.png)

The PseudoCo Assistant opens signed in as dana.lee: Cisco Duo verified the person, not just a password, and the Linux Patch Operator role comes from a Duo group.

Open `/patchbot-ui` on your PseudoCo Assistant address.

#### 5.1.2 Open the Toolchain

![PatchBot](/images/image-715.png)

Click on the **Toolchain** tab.

![Toolchain](/images/image-716.png)

The Toolchain tab lists the MCP servers PatchBot can use in your workspace, with each one's latest scan.

MCP servers — PatchBot's own three servers and a third party's Vendor Advisories server. The scanner reads each server's tool catalogue before PatchBot trusts it: PatchBot refuses any job while one of its own servers lacks a clean verdict.

Vendor Advisories — A patch vendor's remediation advisories, from outside the company. PatchBot connects it only on a clean scan of its current catalogue.

### Lab 5.2 Poison the Vendor's Server

{{< tour "lab-5.2" >}}

Under **Demo Controls**, turn on **Vendor ships a poisoned tool description**.

#### 5.2.1 Poison the Vendor's Description

![Poisoned description on](/images/image-717.png)

The vendor's server now describes its tool with hidden instructions aimed at the AI model: a tool-poisoning attack through the software supply chain.

Click on **Scan all servers**.

#### 5.2.2 Scan Every Server

![Scan verdicts](/images/image-718.png)

The Cisco AI Defense MCP Scanner rated every catalogue again, and caught the poisoned description.

Vendor Advisories — Unsafe: its tool is flagged HIGH for prompt injection, the instructions hidden in its description. The attack is caught in the tool's metadata, before any model reads it.

PatchBot's own servers — Still safe, or compensated where a Control already denies a flagged tool for every role. A finding PatchBot can't use at runtime doesn't stop the work.

Click on **Connect Vendor Advisories**.

### Lab 5.3 Watch PatchBot Refuse the Server

{{< tour "lab-5.3" >}}

#### 5.3.1 Read the Refusal

![Connection refused](/images/image-719.png)

PatchBot refused the connection: the Cisco AI Defense MCP Scanner rated the server unsafe, so its tool never reaches the model.

Refusal — PatchBot names the server, the flagged tool and the threat. Nobody has to notice the poisoning for it to be stopped.

{{% notice note %}}
**Connect anyway** is an instructor's override for showing what happens without the scan. Leave it alone.
{{% /notice %}}

### Lab 5.4 Find the Refusal in Splunk

{{< tour "lab-5.4" >}}

Go back to the PatchBot app's tab in Splunk.

#### 5.4.1 Open Agent Tool Calls

![PatchBot app](/images/image-720.png)

Click on **Agent Tool Calls** in the left navigation.

![Agent Tool Calls](/images/image-721.png)

Scroll down to **MCP servers: latest Cisco MCP Scanner verdict**.

#### 5.4.2 Read the Verdicts in Splunk

![MCP Scanner verdicts in Splunk](/images/image-722.png)

Splunk holds the same verdicts and the refusal, from the events PatchBot sends.

MCP servers: latest Cisco MCP Scanner verdict — Each server's latest verdict, with the flagged tool and its threat. The security team sees the toolchain's state without opening PatchBot.

Vendor server connections — Every connection PatchBot made or refused, and why. A refused connection is on the record like any other decision.

Go back to the Enterprise Security tab with your investigation.

#### 5.4.3 End the Review Task

![Review task in progress](/images/image-723.png)

Click on **End**.

![Review task ended](/images/image-724.png)

The review is recorded: the denied calls from Lab 4 and the refused server from this lab.

Remediate — Both tasks ended. The plan moves on to Verify, where production waits for a person.

## Outcome

Lab 5 shows a supply-chain attack on an AI agent's tools caught before any model reads it.

**Vetted tools** — The Cisco AI Defense MCP Scanner rates every server's tool catalogue before PatchBot trusts it.

**Refusal by design** — A flagged server is refused, so a poisoned tool never reaches the model.

**On the record** — Scans, findings and refused connections land in Splunk beside every other PatchBot event.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Trusted Agents.** The agent uses only tools that pass the Cisco AI Defense MCP Scanner, so a poisoned third-party tool is refused before it can steer the agent.
{{% /notice %}}

<!-- exec-outcome:end -->
