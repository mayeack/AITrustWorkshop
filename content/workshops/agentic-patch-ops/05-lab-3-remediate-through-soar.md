+++
title       = "Lab 3 — Remediate Through SOAR, with Identity"
description = "Start the Remediate task, ask the Security Assistant to patch through Splunk SOAR for an operator with the wrong role and then the right one, and record the runs."
duration    = "20 min"
weight      = 40
aliases     = ["/workshops/agentic-patch-ops/05-lab-3-patch/", "/workshops/agentic-patch-ops/05-lab-3-act-through-soar/"]
+++

{{< tour "lab-3" >}}

**Pillar:** Remediate<br>
**Tool:** Splunk SOAR, Cisco Duo, Splunk Agent Observability Controls<br>
**Outcome:** Trusted Agents

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security architects**, **IT operations leaders** and **AI governance** teams. Primary question: _When an AI agent acts for us, how do we know it only does what that person may do?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Start the plan's Remediate task, ask the Security Assistant to run PatchBot's patch servers action through Splunk SOAR, first for ravi.patel, whose role doesn't cover the servers, and then for dana.lee, whose role does, and record the runs on the task.
{{% /notice %}}

## Background

The plan's remediation runs as a Splunk SOAR action: the PatchBot connector hands the job to PatchBot, an AI patching agent. You name the operator the patch runs as, and you approve the action before it runs.

Before PatchBot acts, three checks run. Its tools must have a clean Cisco AI Defense MCP Scanner verdict, or it refuses the job. Cisco Duo's directory gives the operator's role. Splunk Agent Observability Controls judge every tool call against that role before it runs.

Changes follow the change model. Non-production servers fall under a pre-approved standard change and are patched at once; production servers get a normal change that waits for a person.

## Labs

### Lab 3.1 Start the Remediate Task

{{< tour "lab-3.1" >}}

#### 3.1.1 Start the Patch Task

![Remediate phase](/images/image-682.png)

Click on **Patch every affected server through PatchBot**.

![Remediate task](/images/image-683.png)

Click on **Start**.

![Remediate task in progress](/images/image-684.png)

The Remediate task is where the plan hands the patching to automation: its action runs PatchBot through Splunk SOAR.

Description — How to run the action and what happens: the operator's role comes from Cisco Duo, Splunk Agent Observability Controls judge every call, non-production servers fall under a pre-approved standard change, and production gets a normal change. The policy is written into the plan, where the analyst reads it.

Respond — The **patch servers - PatchBot** action and a Splunk search of PatchBot's runs for this CVE. The plan carries the fix itself, not only the instruction.

### Lab 3.2 Patch as the Wrong Role

{{< tour "lab-3.2" >}}

#### 3.2.1 Ask to Patch as ravi.patel

![Prompt for ravi.patel](/images/image-685.png)

In the Security Assistant, type the example prompt, replacing INVESTIGATION-ID with your investigation's ID (for example, ES-00005), and press Enter. ravi.patel is a Windows Patch Operator, and the four web servers run Linux.

**Example prompt:** Containment is done: 203.0.113.66 is blocked at the perimeter firewall. Using PatchBot, patch servers for CVE-2021-41773 as ravi.patel. Reason: INVESTIGATION-ID active exploitation

#### 3.2.2 Review and Run the Action

![Action for approval](/images/image-686.png)

The Security Assistant prepares the Splunk SOAR action and stops for your approval: nothing runs until a person reviews it.

Get SOAR Actions, Choose SOAR Action and Prepare SOAR Action — The assistant found the PatchBot connector and chose its patch servers action. The AI picks the tool; a person still decides to use it.

PatchBot - patch servers — The action card: the target (this investigation), the asset and the parameters, with Run action and Cancel. This is the approval step the security team required for every PatchBot action.

Click on **Show more**.

![Action parameters](/images/image-687.png)

Type your investigation's ID in **investigation_id** (for example, ES-00005) and **admin** in **requested_by**. The assistant leaves both empty, and Splunk needs the investigation ID to close the investigation in Lab 7.

![Action parameters filled](/images/image-688.png)

Check that **operator** is ravi.patel, then click on **Run action**.

#### 3.2.3 Read the Result

![Denied for ravi.patel](/images/image-689.png)

PatchBot refused every change: ravi.patel's role doesn't cover these servers, so nothing was patched.

Connector report — Denied for ravi.patel, a Windows Patch Operator, on every server, with the reason in the security team's own words. The person asking learns why, and which role would be allowed.

Approved parameters — Exactly what ran: the CVE, the investigation, the operator, the reason and the requester, with the SOAR action run ID. Every automated action is attributable.

### Lab 3.3 Patch as the Right Role

{{< tour "lab-3.3" >}}

#### 3.3.1 Ask to Patch as dana.lee

![Prompt for dana.lee](/images/image-690.png)

Type the example prompt for dana.lee, a Linux Patch Operator, replacing INVESTIGATION-ID with your investigation's ID, and press Enter.

**Example prompt:** Containment is done: 203.0.113.66 is blocked at the perimeter firewall. Using PatchBot, patch servers for CVE-2021-41773 as dana.lee. Reason: INVESTIGATION-ID active exploitation

#### 3.3.2 Review and Run the Action

![Action for approval](/images/image-691.png)

Click on **Show more**.

![Action parameters](/images/image-692.png)

Type your investigation's ID in **investigation_id** and **admin** in **requested_by**.

![Action parameters filled](/images/image-693.png)

Click on **Run action**.

#### 3.3.3 Read the Result

![Standard and normal changes](/images/image-694.png)

This time PatchBot worked within the change model: what was pre-approved ran at once, and production waits for a person.

Connector report — The development and staging servers patched and verified under a standard change, and one normal change for both production servers, waiting for the Change Board. The agent moved fast where policy allows and stopped where policy requires a person.

Approved parameters — The same request with dana.lee as the operator, and its SOAR action run ID.

{{% notice note %}}
If the assistant answers that containment isn't verified instead of preparing the action, check that both Contain tasks are ended and the block task has its note, then send the prompt again.
{{% /notice %}}

Click on the **Automation** tab.

### Lab 3.4 Record the Runs and End the Task

{{< tour "lab-3.4" >}}

#### 3.4.1 Read Who PatchBot Acted For

![Automation](/images/image-695.png)

The Automation tab is the investigation's record of every Splunk SOAR action: what ran, for whom, and what came back.

Runs — One entry per action, the newest first, each with who ran it and when. This lab adds two: ravi.patel's, then dana.lee's.

Click on the arrow at the top right to hide the investigation details.

![Runs with the details hidden](/images/image-696.png)

Click on the older **AI-SOC-Analyst_PatchBot_patch-servers** run, ravi.patel's.

![ravi.patel's run](/images/image-697.png)

Scroll its result down to **operator**.

![Who PatchBot acted for](/images/image-698.png)

The result shows who PatchBot acted for and where that identity came from.

operator — ravi.patel, the Windows Patch Operator role, and the source duo_directory: Cisco Duo's directory gave the role on this call. Nobody typed the role in, so nobody can type in a better one.

toolchain — The Cisco AI Defense MCP Scanner's check of PatchBot's own MCP servers before the run: none unsafe. Lab 5 shows what happens when a server fails it.

Click on the arrow at the top right to show the investigation details again.

![ravi.patel's run with the details](/images/image-699.png)

Click on the **Response** tab.

#### 3.4.2 Record the Changes and End the Task

![Remediate task in progress](/images/image-684.png)

Scroll the task down to its **Notes** box, click in it and type the run's change IDs from dana.lee's connector report.

**Example note:** Patched as dana.lee through PatchBot: standard change CHG-1010 for web-dev-01 and web-stg-01, normal change CHG-1011 for web-prod-01 and web-prod-02, waiting for the Change Board.

![Remediate note](/images/image-700.png)

Click on **Save**.

![Remediate note saved](/images/image-701.png)

Click on **End**.

![Remediate task ended](/images/image-702.png)

The patching is recorded on its task: who it ran as, and the changes it made and opened.

Remediate — The patch task ended, with its owner and its note. The review task is next, in Labs 4 and 5.

## Outcome

Lab 3 makes one request twice: it is denied for the wrong role, and carried out within the change model for the right one.

**Verified operator** — Cisco Duo names the operator's role on every call; nobody types it in.

**Policy on every call** — Splunk Agent Observability Controls deny a patch outside the operator's role before any tool runs.

**On the record** — The SOAR run record and the task's note show who the agent acted for and what it changed.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Trusted Agents.** Every action the agent takes runs for a verified person and passes a policy check first, so automation can never do more than the person who asked.
{{% /notice %}}

<!-- exec-outcome:end -->
