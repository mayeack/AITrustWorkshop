+++
title       = "Introduction"
description = "An agent that can patch production needs controls a person can see and prove."
duration    = "10 min"
weight      = 5
+++

*A hands-on workshop for the leaders accountable for vulnerability risk — and the teams who patch.*

{{< tour >}}

## The Problem: Agents Are Reaching Production

Every week the scanners report more vulnerabilities than a team can patch. AI agents promise to close that gap: they read the reports, rank the risk and apply the fixes, around the clock.

But an agent that can patch production can also break it. It acts with whatever access it was given, so the question is no longer only *which vulnerability first*, but *who is the agent acting for, and what is that person allowed to do?* The agent also reads text written by others: a vendor's advisory, or the description of a tool it calls. An attacker who controls that text can steer the agent without ever signing in.

**An agent that patches has to be governed like a privileged operator: every action authorized, every production change approved, every step on the record.**

---

## The Solution: PatchBot, Under Controls You Can Prove

PatchBot is the PseudoCo Assistant's patch agent. It reads a six-server estate, ranks what an attacker can reach with CISA BOD 26-04, explains each finding and patches. Around it, the workshop puts four controls you can watch working:

**Splunk Agent Observability Controls** judge every tool call before it runs, on the role of the person who asked.

**Cisco MCP Scanner** rates every MCP server's tool catalogue before PatchBot connects it.

**The Change Board** makes production wait for a person, and never the person who asked.

**Splunk and Splunk Enterprise Security** record every step and raise findings on the patterns a SOC should see.

## The Journey

| Lab | What you do | What it proves | Time |
| --- | --- | --- | --- |
| **Lab 1 — Detect** | Pick a persona, answer one exposure question, read the ranked findings, scan the toolchain | The agent ranks risk with your context, and its tools are checked before they are trusted | 15 min |
| **Lab 2 — Investigate** | Open a finding, ask PatchBot what to patch first | Every recommendation shows its evidence | 15 min |
| **Lab 3 — Patch** | Patch staging, try production, approve the change as someone else, patch production | Production needs a person, and the requester can never approve their own change | 20 min |
| **Lab 4 — Defend** | Try a patch outside your role, a change as a viewer, a poisoned advisory and a poisoned MCP tool | The Controls stop what the person's role, or an attacker's text, should never reach | 25 min |
| **Lab 5 — Govern** | Read the traces and Controls in Agent Observability, the dashboards in Splunk and the findings in Enterprise Security | One record of who asked, what the agent tried and what policy decided | 25 min |

## Executive Outcomes

**Risk-Ranked Exposure** — Your team works the vulnerabilities an attacker can actually reach first, and every tool the agent depends on is rated before it is trusted.

**Explainable Decisions** — Every recommendation the agent makes comes with its evidence, so people check its reasoning instead of taking it on trust.

**Controlled Change** — The agent moves fast in staging, and production waits for a person. Separation of duties is enforced by policy rather than habit.

**Least-Privilege Agents** — The agent can only do what the person asking is allowed to do, and an attacker's instructions stop at runtime.

**Provable Governance** — One record ties every request to its person, every tool call to its policy decision, and every exception to a finding the security team already works.
