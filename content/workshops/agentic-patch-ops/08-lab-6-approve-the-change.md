+++
title       = "Lab 6 — Approve the Normal Change"
description = "Start the approval task, sign in with Cisco Duo as the Change Approver, release production and confirm the change from Splunk SOAR."
duration    = "15 min"
weight      = 55
aliases     = ["/workshops/agentic-patch-ops/06-lab-4-defend/", "/workshops/agentic-patch-ops/06-lab-4-approve-the-change/"]
+++

{{< tour "lab-6" >}}

**Pillar:** Approve<br>
**Tool:** Change Board, Cisco Duo, Splunk SOAR<br>
**Outcome:** Governed Automation

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Change managers** and **IT operations leaders**. Primary question: _Can automation move fast without going around change control?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Start the plan's approval task, sign in to the Change Board with Cisco Duo as sam.ortiz, the Change Approver, approve production, and confirm the change from Splunk SOAR before ending the task.
{{% /notice %}}

## Background

Not every change needs a meeting. A standard change is pre-approved: the same package, a tested fix, a documented rollback, and no production server. Development and staging were patched under one in Lab 3.

Production needs a normal change, decided by a person with the Change Approver role and never by the person who requested it. The approval releases the queued work: PatchBot patches and verifies production on its own, and Splunk SOAR reads the outcome back.

## Labs

### Lab 6.1 Start the Approval Task

{{< tour "lab-6.1" >}}

#### 6.1.1 Start the Approval Task

![Remediate complete](/images/image-724.png)

Click on **Get the production change approved**.

![Approval task](/images/image-725.png)

Click on **Start**.

![Approval task in progress](/images/image-726.png)

The first Verify task holds production until a person decides it.

Description — The normal change for the production servers waits on the Change Board, where a Change Approver decides it; nobody approves their own request. The approval runs the production patches on its own, each call judged by the Controls again.

Respond — The **get change status - PatchBot** action and a search of the Change Board's history for this CVE. You confirm the outcome from Splunk SOAR at the end of this lab.

### Lab 6.2 Sign In as the Change Approver

{{< tour "lab-6.2" >}}

{{% notice warning "Important" %}}
Duo must bring you back within 5 minutes of **Continue with Duo**, or PatchBot shows an error and you sign in again. Sign in at `/login/duo`, not with the Change Board's own **Sign in with Duo** button.
{{% /notice %}}

Go back to the PseudoCo Assistant tab and open `/login/duo`.

#### 6.2.1 Sign In with Duo

![Sign in with Duo](/images/image-727.png)

Type **sam.ortiz** in **Username** and click on **Continue with Duo**.

![Duo passcode](/images/image-728.png)

Type the workshop code your instructor gave you and click on **Verify**.

![PseudoCo Assistant](/images/image-729.png)

Cisco Duo verified the person, not just a password, and sam.ortiz's Change Approver role comes from a Duo group.

Open `/change-board-ui` on your PseudoCo Assistant address.

### Lab 6.3 Approve the Normal Change

{{< tour "lab-6.3" >}}

{{% notice info "A synthetic application" %}}
The Change Board is a synthetic change-management application built for this workshop. It stands in for the IT service management tool where your teams approve changes; the labs use only its approval.
{{% /notice %}}

#### 6.3.1 Approve with a Note

![Change Board](/images/image-730.png)

The Change Board is where a person, never the agent, decides a production change.

Awaiting approval — The normal change from Lab 3, for both production servers, requested by dana.lee and opened from Splunk SOAR for your investigation. The pre-approved standard change for development and staging has already closed.

Click on the **Decision note** box of the change awaiting approval.

![Approval note](/images/image-731.png)

Type the note and click on **Approve**.

**Example note:** Approved: emergency fix for actively exploited CVE-2021-41773. Dev and staging verified under the standard change.

#### 6.3.2 Find the Closed Change

![Nothing awaiting approval](/images/image-732.png)

The approved change leaves the list of changes awaiting approval.

Click on **All**.

![Change closed](/images/image-733.png)

The approval released the queued work: within seconds PatchBot patched both production servers, verified the fix and closed the change.

Approved by — sam.ortiz and the decision note. The change record shows who asked, who approved and why.

Standard change — The change below it, from the same run in Lab 3: web-dev-01 and web-stg-01 under the pre-approved template, closed at once. Pre-approval let the agent finish without waiting.

### Lab 6.4 Confirm the Change in Splunk SOAR

{{< tour "lab-6.4" >}}

Go back to the Enterprise Security tab with your investigation.

#### 6.4.1 Run the Change Status Action

![Approval task in progress](/images/image-734.png)

Under **Respond**, click on the run button to the left of **get change status - PatchBot**.

![Change status action](/images/image-735.png)

Type the normal change's ID in **change_id** (for example, CHG-1011) and click on **Run action**.

![Change status action completed](/images/image-736.png)

Click on **View results**.

#### 6.4.2 Read the Result and End the Task

![Change status](/images/image-737.png)

Splunk SOAR reads the change back from PatchBot, in the investigation's automation history.

Status and approver — Closed, approved by sam.ortiz, with both production servers patched and nothing awaiting approval. The SOC confirms the change from its own console, not from the agent's word.

Click on the **Response** tab.

![Approval task in progress](/images/image-738.png)

Click on **End**.

![Approval task ended](/images/image-739.png)

The approval is recorded on its task, beside the change status that confirmed it.

Verify — The approval task ended, with its owner. The second Verify task, in Lab 7, checks every server.

Respond — The get change status action, completed, with its results a click away. The confirmation stays on the task for anyone who reviews the response.

## Outcome

Lab 6 keeps people where they matter: production waits for an approver, and everything else flows.

**Standard** — Pre-approved changes run at once, under a named template and its criteria.

**Normal** — Production waits for a Change Approver, signed in with Cisco Duo, who can't approve their own request.

**Confirmed** — The Change Board and Splunk SOAR both show the approved change and its outcome on every server.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Governed Automation.** One action hands the work to an agent, pre-approved changes run at once, and production still waits for a person, with every decision on the record.
{{% /notice %}}

<!-- exec-outcome:end -->
