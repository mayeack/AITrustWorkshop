+++
title       = "Lab 4 — Approve the Normal Change"
description = "Sign in with Cisco Duo as the Change Approver, compare the pre-approved standard change with the normal change, and release production."
duration    = "15 min"
weight      = 45
aliases     = ["/workshops/agentic-patch-ops/06-lab-4-defend/"]
+++

**Pillar:** Approve<br>
**Tool:** PatchBot Change Board, Cisco Duo<br>
**Outcome:** Governed Automation

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Change managers** and **IT operations leaders**. Primary question: _Can automation move fast without going around change control?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Sign in to the Change Board with Cisco Duo as sam.ortiz, the Change Approver, compare the standard change with the normal change, and approve production.
{{% /notice %}}

## Background

Not every change needs a meeting. A standard change is pre-approved: the same package, a tested fix, a documented rollback, and no production server. Development and staging were patched under one in Lab 3.

Production needs a normal change, decided by a person with the Change Approver role and never by the person who requested it. The Change Board is where that person decides. The approval releases the queued work: PatchBot patches and verifies production on its own.

## Labs

### Lab 4.1 Sign In as the Change Approver

{{% notice warning "Important" %}}
Get sam.ortiz's passcode from your instructor before you start: Duo must bring you back within 5 minutes of **Continue with Duo**, or PatchBot shows an error and you sign in again. Sign in at `/login/duo`, not with the Change Board's own **Sign in with Duo** button.
{{% /notice %}}

Open `/login/duo` on your PseudoCo Assistant address.

#### 4.1.1 Sign In with Duo

![Sign in with Duo](/images/image-630.png)

Type **sam.ortiz** in **Username** and click on **Continue with Duo**.

![Duo passcode](/images/image-631.png)

Cisco Duo verifies the person, not just a password, and sam.ortiz's Change Approver role comes from a Duo group.

Type the passcode your instructor gave you and click on **Verify**.

#### 4.1.2 Open the Change Board

![PseudoCo Assistant](/images/image-632.png)

Duo brings you back to the PseudoCo Assistant, signed in as sam.ortiz.

Open `/change-board-ui` on your PseudoCo Assistant address.

![Change Board](/images/image-633.png)

The Change Board is where a person, never the agent, decides a production change.

Change Approver · sam.ortiz · Duo — Who is deciding, their role and how they signed in. The line under the tabs says you can approve or reject only changes you did not request: separation of duties is enforced, not assumed.

Awaiting approval — The normal change from Lab 3: opened from Splunk SOAR for your investigation, the production servers, the change window, who requested it, and the plan with its rollback. Everything an approver needs is on the card.

Decision note — The note, Approve and Reject. The decision and its reason go on the record together.

Click on **All**.

### Lab 4.2 Compare Standard and Normal Changes

#### 4.2.1 Review Every Change

![Every change](/images/image-634.png)

The All view puts the two kinds of change side by side: the one that needs a person, and the one that didn't.

Normal change — Awaiting approval, decided on this board by a Change Approver. Production never changes without a person's decision.

Standard change — Closed, approved by the template SC-APACHE-SEC: an Apache security update on non-production servers, with the vendor's fixed version, a tested fix and a rollback from the package cache. Pre-approval is a policy with criteria, not an exception.

{{% notice note %}}
Changes from earlier runs in your environment may be listed under these two.
{{% /notice %}}

Click on the **Decision note** box of the change awaiting approval.

### Lab 4.3 Approve the Normal Change

#### 4.3.1 Approve with a Note

![Approval note](/images/image-635.png)

Type the note and click on **Approve**.

**Example note:** Approved: emergency fix for actively exploited CVE-2021-41773. Dev and staging verified under the standard change.

#### 4.3.2 Review the Closed Change

![Change closed](/images/image-636.png)

The approval released the queued work: within seconds PatchBot patched both production servers, verified the fix and closed the change.

Closed — Patched and verified, with no second request and no manual step. The approval was the last thing a person had to do.

Approved by — The approver and their note. The change record shows who asked, who approved and why.

## Outcome

Lab 4 keeps people where they matter: production waits for an approver, and everything else flows.

**Standard** — Pre-approved changes run at once, under a named template and its criteria.

**Normal** — Production waits for a Change Approver, signed in with Cisco Duo, who can't approve their own request.

**Release** — The approval releases the queued work: no second request and no manual patching.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Governed Automation.** One action hands the work to an agent, pre-approved changes run at once, and production still waits for a person, with every decision on the record.
{{% /notice %}}

<!-- exec-outcome:end -->
