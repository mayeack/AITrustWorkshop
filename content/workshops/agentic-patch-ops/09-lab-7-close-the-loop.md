+++
title       = "Lab 7 — Close the Loop"
description = "See Splunk resolve the investigation from the verified fixes, try the attack again, and close the response plan with the time to remediate on the record."
duration    = "15 min"
weight      = 60
aliases     = ["/workshops/agentic-patch-ops/07-lab-5-close-the-loop/"]
+++

{{< tour "lab-7" >}}

**Pillar:** Close<br>
**Tool:** Splunk Enterprise Security, the PatchBot app in Splunk<br>
**Outcome:** Closed-Loop Proof

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**SOC leaders**, **auditors** and **CISOs**. Primary question: _Can I prove the vulnerability is fixed, and how long it took?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
See Splunk resolve the investigation from the verified fixes, confirm every server's fix, try the attack again, and close the response plan with the time to remediate on the record.
{{% /notice %}}

## Background

PatchBot never writes to Enterprise Security. A Splunk search watches for verified fixes, and when every affected server has one, Splunk resolves the investigation itself and writes a note naming the changes and the servers.

The plan's last tasks check that work: every server's fix, the automatic resolution, and the time from the first exploitation request to the last verified fix.

## Labs

### Lab 7.1 Confirm Every Server Has a Verified Fix

{{< tour "lab-7.1" >}}

Reload the Enterprise Security tab with your investigation.

#### 7.1.1 Reload the Investigation

![Investigation resolved](/images/image-740.png)

Nobody clicked Resolve: Splunk resolved the investigation from the evidence, shortly after the last fix was verified.

Status and Disposition — Resolved, and judged a true positive. The case closes with a verdict, not just a closed ticket.

PatchBot: verified fix — Splunk's note: the fix verified on every server in scope, the changes that made it, when the last verification ran, and the search that resolved the investigation. The resolution cites its evidence, so an auditor can check it.

{{% notice note %}}
If the investigation isn't resolved yet, wait a minute and reload: the resolve search runs every minute.
{{% /notice %}}

Click on **Confirm every server has a verified fix**.

#### 7.1.2 Verify Every Server

![Verify task](/images/image-741.png)

Click on **Start**.

![Verify task in progress](/images/image-742.png)

The second Verify task checks each server, not the investigation's status.

Description — Every server in scope needs a verified fix newer than its last open scanner report. A server reported open again after its verification isn't verified.

Respond — The **Verification per server** search: the last open report and the last verified fix for each server. It is the same test the resolve search applies.

Click on **End**.

### Lab 7.2 Try the Attack Again

{{< tour "lab-7.2" >}}

Go back to the attack console tab and reload it.

#### 7.2.1 Launch the Exploit Again

![Attack console](/images/image-743.png)

Click on **Launch the exploit**.

#### 7.2.2 Read What the Server Answered

![Exploit refused](/images/image-744.png)

The same exploit now fails: the patched server refuses every request.

Requests — Answered Forbidden and Bad Request: no file read and no command run. The fix holds from the attacker's side too.

Now switch sides — Splunk still sees the attempts, and raises no new active-exploitation finding: the detection fires only when an exploit succeeds against a server that is still reported vulnerable.

### Lab 7.3 Close the Plan

{{< tour "lab-7.3" >}}

Go back to the Enterprise Security tab with your investigation.

#### 7.3.1 Confirm the Resolution

![Close phase](/images/image-745.png)

Click on **Confirm the automatic resolution**.

![Resolution task](/images/image-746.png)

Click on **Start**.

![Resolution task in progress](/images/image-747.png)

The first Close task confirms what Splunk did on its own.

Description — The TA-patchbot search sets the investigation to Resolved within a minute of the last verified fix and adds the PatchBot: verified fix note. The automation's work is checked by a person before the plan closes.

Click on **End**.

#### 7.3.2 Record the Time to Remediate

![Time to remediate task](/images/image-748.png)

Click on **Record the time to remediate**.

![Time to remediate task opened](/images/image-749.png)

Click on **Start**.

![Time to remediate task in progress](/images/image-750.png)

The last task records how long the response took, for the post-incident review.

Description — Measure from the first exploitation request to the last verified fix, and record it with the disposition and the change IDs. A production change that waited long for approval is the usual driver.

Respond — The **Exploitation to verified fix** search: the minutes from the first exploitation request to the last verified fix on this estate.

Click in the **Notes** box and type the time to remediate, the disposition and the change IDs.

**Example note:** Time to remediate: 42 minutes from the first exploitation request to the last verified fix. True Positive - Suspicious Activity. Changes CHG-1010 (standard) and CHG-1011 (normal).

![Time to remediate note](/images/image-751.png)

Click on **Save**.

![Time to remediate note saved](/images/image-752.png)

Click on **End**.

![Plan complete](/images/image-753.png)

Every task in the plan is ended, in order, each with its owner.

Exploited Vulnerability Response Plan — 100% completed: Contain, Remediate, Verify and Close. The response is on the record from the first containment to the time it took.

### Lab 7.4 Optional: Replay the Change Chain

{{< tour "lab-7.4" >}}

Go back to the PatchBot app's tab in Splunk.

#### 7.4.1 Open the Change Chain

![Agent Tool Calls](/images/image-754.png)

Click on **Change Chain** in the left navigation.

![Change Chain](/images/image-755.png)

Type your investigation's ID in **Investigation ID (ES-...)**.

#### 7.4.2 Read the Change Chain

![Change Chain replay](/images/image-756.png)

The Change Chain replays this remediation end to end, from the scanner report to the closed change, from events Splunk already holds.

Completeness checklist — Which hops of the chain have events: scanner report, finding opened, tool calls and verdicts, change opened, change approved, patch and finding fixed. A missing hop shows at a glance.

Linked keys — Every finding, change and investigation ID the chain holds, with its first and last event. One key finds all the others.

Timeline — Every event of the chain in order, with who acted and where it was recorded. The whole story, in Splunk's own record.

## Outcome

Lab 7 closes the loop with evidence: the fix is verified, the attack fails, and the plan ends with its time to remediate.

**Resolved from evidence** — Splunk resolves the investigation only when every affected server has a verified fix.

**The attack fails** — The patched server refuses the same exploit.

**Plan complete** — Every task is ended in order, and the time to remediate is on the record.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Closed-Loop Proof.** The investigation resolves from verified fixes, not from someone's say-so, and the plan records every step and how long it took, for the SOC and the auditors.
{{% /notice %}}

<!-- exec-outcome:end -->
