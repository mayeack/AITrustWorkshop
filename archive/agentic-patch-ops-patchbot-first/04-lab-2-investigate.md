+++
title       = "Lab 2 — Investigate"
description = "Open a finding's attack path, fix and evidence, and ask PatchBot what to patch first."
duration    = "15 min"
weight      = 35
+++

{{< tour "lab-2" >}}

**Pillar:** Investigate<br>
**Tool:** PatchBot<br>
**Outcome:** Explainable Decisions

<!-- persona:start -->

{{% notice style="info" title="Who this is for" icon="users" %}}
**Security analysts** and **IT operations** teams. Primary question: _Why did the agent rank this first, and can I check its reasoning?_
{{% /notice %}}

<!-- persona:end -->

{{% notice style="info" title="Objective" icon="target" %}}
See why PatchBot ranked a finding the way it did, and ask it a question in plain language.
{{% /notice %}}

## Background

A ranking is only useful if people can check it. Each PatchBot finding opens as a case file: the attack path from the attacker to the asset, the missing control that would break it, the fix, and the evidence behind the rating.

PatchBot also answers questions in plain language. It reads the same findings you see, and anything it does still goes through the Controls.

## Labs

### Lab 2.1 Open a Finding

{{< tour "lab-2.1" >}}

#### 2.1.1 Open the Top Finding

![Findings list](/images/image-422.png)

Click on the first finding, **Anyone on the internet can read files and run code on web-prod-01**.

#### 2.1.2 Review the Finding

![Finding detail](/images/image-423.png)

The finding detail is the case file for one vulnerability: how an attacker gets in, what to do about it, and the evidence behind the rating.

Attack path — who can reach the service, the vulnerable package, and what it exposes, with the missing control that would break the chain marked in red.

What we found — the CVE in plain language, with the servers it affects.

How to fix it — the fixed version and any caveat, such as an earlier fix that was incomplete.

Evidence — each affected server's installed and fixed version, with its BOD 26-04 row and deadline. Below it, the CISA KEV date, whether exploitation is automatable, and its technical impact.

Triage, Patch and Review — the actions on this finding. Each one becomes a tool call that the Controls judge first.

### Lab 2.2 Ask PatchBot

{{< tour "lab-2.2" >}}

#### 2.2.1 Ask What to Patch First

![Chat question](/images/image-424.png)

Type the example prompt in the chat box and click on **Send**.

**Example prompt:** What should I patch first, and why?

#### 2.2.2 Review the Answer

![Chat answer](/images/image-425.png)

PatchBot answers in a sentence or two, grounded in the estate's own facts: the CVE, the server, its severity and whether it is reachable from the internet.

Chat — the model reads the same findings you see and names servers and CVEs exactly as they appear. It can recommend; any action it takes still goes through the Controls.

## Outcome

Lab 2 shows that every recommendation comes with its evidence, in language a non-specialist can read.

**Explain** — Each finding shows how an attacker gets in and what breaks the chain.

**Evidence** — Installed and fixed versions, the BOD 26-04 row and deadline, and the CISA KEV date back every rating.

**Ask** — Plain-language questions get answers grounded in the estate's own facts.

<!-- exec-outcome:start -->

{{% notice style="info" title="Executive outcome" icon="star" %}}
**Executive outcome — Explainable Decisions.** Every recommendation the agent makes comes with its evidence: the attack path, the fix and the deadline. People check the agent's reasoning instead of taking it on trust.
{{% /notice %}}

<!-- exec-outcome:end -->
