+++
title       = "Lab 3 — Patch"
description = "Patch staging, see production refused until a person approves the change on the Change Board, then patch production under that approval."
duration    = "20 min"
weight      = 40
+++

{{< tour "lab-3" >}}

**Pillar:** Patch<br>
**Tool:** PatchBot, Change Board, Splunk Agent Observability Controls<br>
**Outcome:** Controlled Change

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Change managers** and **IT operations leaders**. Primary question: _Can an agent patch production without going around change control?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
Patch staging, then see production refused until a person approves the change, and patch production under that approval.
{{% /notice %}}

## Background

PatchBot patches staging on its own and verifies the fix. Production needs an approved change: PatchBot opens the change and asks for approval, but only a person with the Change Approver role can approve it, and never the person who asked for it.

The rule is not in PatchBot's prompt. **Splunk Agent Observability Controls** judge every tool call before it runs, so a production patch without an approved change is refused however the request is worded.

## Labs

### Lab 3.1 Patch Staging

{{< tour "lab-3.1" >}}

#### 3.1.1 Patch the Staging Server

![Patch menu](/images/image-426.png)

Click on **Patch -> Patch staging**.

![Staging patched](/images/image-427.png)

PatchBot patched the staging server and checked its work, and each step shows the policy decision it ran under.

Chat — the summary of what PatchBot did, with one tag per tool call: `apply_patch · allowed`, then `verify_patch · allowed`. Each tag is a decision the Controls made before the tool ran.

Evidence — the staging server now shows the fixed version, marked patched. Production is still open.

### Lab 3.2 Try Production

{{< tour "lab-3.2" >}}

#### 3.2.1 Request the Production Patch

![Patch menu for production](/images/image-428.png)

Click on **Patch -> Patch production (needs an approved change)**.

![Production refused](/images/image-429.png)

PatchBot opened a change for the production server, and the Controls refused the patch itself until that change is approved.

Chat — `create_change · allowed` opened the change and asked for approval. `apply_patch · denied` carries the security team's own reason: production needs an approved change, so request approval on the Change Board first.

Click on **Change Board** at the top of the page.

### Lab 3.3 Approve the Change as Someone Else

{{< tour "lab-3.3" >}}

#### 3.3.1 Open the Change Board

![Change Board as the requester](/images/image-430.png)

The Change Board is where a person, never PatchBot, decides a production change.

Awaiting approval — each change lists its CVE, priority, servers, environment and window, who requested it and for whose estate, and the plan with its rollback.

Role line — your role can read changes; a Change Approver decides them. Nobody can approve a change they requested.

Click on the persona chip at the top right (**Linux Patch Operator · dana.lee · role map · Switch**).

#### 3.3.2 Switch to the Change Approver

![Change Board persona picker](/images/image-431.png)

Click on **sam.ortiz** (Change Approver).

#### 3.3.3 Approve with a Note

![Change Board as the approver](/images/image-432.png)

As a Change Approver, the same change now offers a decision note with Approve and Reject.

Click on the **Decision note** box.

![Approval note](/images/image-433.png)

Type the note and click on **Approve**.

**Example note:** Staging verified on web-stg-01. Approved for tonight's window.

#### 3.3.4 Review the Change Record

![Queue after approval](/images/image-434.png)

The change leaves the approval queue as soon as it is decided.

Click on **All**.

![Approved change](/images/image-435.png)

The All view is the change record: who asked, who approved, the note they left, and the window. It is the same record Splunk receives.

Click on **PatchBot** at the top of the page.

### Lab 3.4 Patch Production Under the Approved Change

{{< tour "lab-3.4" >}}

#### 3.4.1 Switch Back to the Operator

![PatchBot as the approver](/images/image-436.png)

PatchBot opens on sam.ortiz's own estate, because the persona follows you between pages.

Click on the persona chip at the top right (**Change Approver · sam.ortiz · role map · Switch**).

![Persona picker](/images/image-437.png)

Click on **dana.lee**.

#### 3.4.2 Patch Production

![Findings with the approved change](/images/image-438.png)

The finding now shows that its change is approved, with the change ID, so the operator knows production can go ahead.

Click on the first finding, **Anyone on the internet can read files and run code on web-prod-01**.

![Patch menu with an approved change](/images/image-439.png)

Click on **Patch -> Patch production (needs an approved change)**.

![Production patched](/images/image-440.png)

With the change approved, the same Controls allow the production patch, and PatchBot verifies it.

Chat — `apply_patch · allowed` and `verify_patch · allowed`. Nothing about PatchBot changed; the approval did.

Evidence — both servers show the fixed version. The finding closes as fixed by an approved change, and the change closes with it.

## Outcome

Lab 3 lets the agent move fast where it is safe and makes production wait for a person.

**Staging first** — PatchBot patches and verifies staging on its own.

**Approval** — Production is refused until a Change Approver approves the change, and the requester can never approve their own change.

**Record** — Every change carries who asked, who approved, the note they left and the window.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Controlled Change.** The agent moves fast in staging, and production waits for a person. Separation of duties is enforced by policy rather than habit, and every production change carries its approval record.
{{% /notice %}}

<!-- exec-outcome:end -->
