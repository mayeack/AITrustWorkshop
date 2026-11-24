+++
title       = "Lab 3 — Act Through SOAR, with Identity"
description = "Ask the Security Assistant to patch through Splunk SOAR, first for an operator with the wrong role and then for the right one."
duration    = "20 min"
weight      = 40
aliases     = ["/workshops/agentic-patch-ops/05-lab-3-patch/"]
+++

{{< tour "lab-3" >}}

**Pillar:** Act<br>
**Tool:** Splunk SOAR, Cisco AI Defense MCP Scanner, Cisco Duo, Splunk Agent Observability Controls<br>
**Outcome:** Trusted Agents

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security architects**, **IT operations leaders** and **AI governance** teams. Primary question: _When an AI agent acts for us, how do we know its tools are safe and it only does what that person may do?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Ask the Security Assistant to run PatchBot's patch servers action through Splunk SOAR, first for ravi.patel, whose role doesn't cover the servers, and then for dana.lee, whose role does.
{{% /notice %}}

## Background

The plan's remediation runs as a Splunk SOAR action: the PatchBot connector hands the job to PatchBot, PseudoCo's patch agent. You name the operator the patch runs as, and you approve the action before it runs.

Before PatchBot acts, three checks run. Its tools must have a clean Cisco AI Defense MCP Scanner verdict, or it refuses the job. Cisco Duo's directory gives the operator's role. Splunk Agent Observability Controls judge every tool call against that role before it runs.

Changes follow the change model. Non-production servers fall under a pre-approved standard change and are patched at once; production servers get a normal change that waits for a person.

## Labs

### Lab 3.1 Patch as the Wrong Role

{{< tour "lab-3.1" >}}

#### 3.1.1 Ask to Patch as ravi.patel

![Prompt for ravi.patel](/images/image-620.png)

In the Security Assistant, type the example prompt, replacing INVESTIGATION-ID with your investigation's ID (for example, ES-00005), and press Enter. ravi.patel is a Windows Patch Operator, and the four web servers run Linux.

**Example prompt:** Containment is done: 203.0.113.66 is blocked at the perimeter firewall. Using PatchBot, patch servers for CVE-2021-41773 as ravi.patel. Reason: INVESTIGATION-ID active exploitation

#### 3.1.2 Review and Run the Action

![Action for approval](/images/image-621.png)

The Security Assistant prepares the Splunk SOAR action and stops for your approval: nothing runs until a person reviews it.

Get SOAR Actions, Choose SOAR Action and Prepare SOAR Action — The assistant found the PatchBot connector and chose its patch servers action. The AI picks the tool; a person still decides to use it.

PatchBot - patch servers — The action card: the target (this investigation), the asset and the parameters, with Run action and Cancel. This is the approval step the security team required for every PatchBot action.

Click on **Show more**.

![Action parameters](/images/image-622.png)

Type your investigation's ID in **investigation_id** (for example, ES-00005) and **admin** in **requested_by**. The assistant leaves both empty, and Splunk needs the investigation ID to close the investigation in Lab 5.

![Action parameters filled](/images/image-623.png)

Check that **operator** is ravi.patel, then click on **Run action**.

#### 3.1.3 Read the Result

![Denied for ravi.patel](/images/image-624.png)

PatchBot refused every change: ravi.patel's role doesn't cover these servers, so nothing was patched.

Connector report — Denied for ravi.patel, a Windows Patch Operator, on every server, with the reason in the security team's own words. The person asking learns why, and which role would be allowed.

Approved parameters — Exactly what ran: the CVE, the investigation, the operator, the reason and the requester, with the SOAR action run ID. Every automated action is attributable.

### Lab 3.2 Patch as the Right Role

{{< tour "lab-3.2" >}}

#### 3.2.1 Ask to Patch as dana.lee

![Prompt for dana.lee](/images/image-625.png)

Type the example prompt for dana.lee, a Linux Patch Operator, replacing INVESTIGATION-ID with your investigation's ID, and press Enter.

**Example prompt:** Containment is done: 203.0.113.66 is blocked at the perimeter firewall. Using PatchBot, patch servers for CVE-2021-41773 as dana.lee. Reason: INVESTIGATION-ID active exploitation

#### 3.2.2 Review and Run the Action

![Action for approval](/images/image-626.png)

Click on **Show more**.

![Action parameters](/images/image-627.png)

Type your investigation's ID in **investigation_id** and **admin** in **requested_by**.

![Action parameters filled](/images/image-628.png)

Click on **Run action**.

#### 3.2.3 Read the Result

![Standard and normal changes](/images/image-629.png)

This time PatchBot worked within the change model: what was pre-approved ran at once, and production waits for a person.

Connector report — The development and staging servers patched and verified under a standard change, and one normal change for both production servers, waiting for the Change Board. The agent moved fast where policy allows and stopped where policy requires a person.

Approved parameters — The same request with dana.lee as the operator, and its SOAR action run ID. Lab 5 shows what checked each request.

{{% notice note %}}
If the assistant answers that containment isn't verified instead of preparing the action, check that both Contain tasks are ended and the block task has its note, then send the prompt again.
{{% /notice %}}

## Outcome

Lab 3 makes one request twice: it is denied for the wrong role, and carried out within the change model for the right one.

**Vetted tools** — PatchBot uses its tools only while their Cisco AI Defense MCP Scanner verdicts are clean.

**Verified operator** — Cisco Duo names the operator's role on every call; nobody types it in.

**Policy on every call** — Splunk Agent Observability Controls deny a patch outside the operator's role before any tool runs.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Trusted Agents.** Every action the agent takes uses vetted tools, runs for a verified person and passes a policy check first, so automation can never do more than the person who asked.
{{% /notice %}}

<!-- exec-outcome:end -->
