+++
title       = "Introduction"
description = "From an exploited vulnerability to a resolved investigation in Splunk, with an AI agent doing the patching under controls a person can prove."
duration    = "10 min"
weight      = 5
+++

*A hands-on workshop for the leaders accountable for vulnerability risk — and the SOC and operations teams who respond.*

## The Problem: Exploitation Moves Faster Than Patching

Every week the scanners report more vulnerabilities than a team can patch, and attackers go straight for the ones in CISA's Known Exploited Vulnerabilities catalog. The question that matters is not which CVEs exist, but *which one is being exploited right now, and how fast can we close it everywhere it lives?*

AI agents promise to close that gap: they can patch around the clock. But an agent that can patch production can also break it. It acts with whatever access it is given, it depends on tools someone else wrote, and nobody can tell afterwards who it acted for unless that was recorded at the time.

**Patching at machine speed needs the same governance as patching by hand: a confirmed incident, a plan, a verified operator, an approved production change, and proof that the fix worked.**

---

## The Solution: Splunk Runs the Response, an Agent Does the Patching

The workshop starts and ends in **Splunk Enterprise Security**. An AI agent, PatchBot, does the patching, but every step around it is a Splunk or Cisco control you can watch working:

**Splunk Enterprise Security** detects the exploitation by joining the attack traffic with the vulnerability inventory, and its **AI SOC analyst** triages the finding.

**The Security Assistant** reads the investigation and plans the response with its response plan.

**Splunk SOAR** hands the patching to the agent, as an action a person approves.

**Cisco AI Defense MCP Scanner** vets the agent's tools before it uses them, and **Cisco Duo** says who the agent is acting for.

**Splunk Agent Observability Controls** judge every tool call against that person's role before it runs.

**The Change Board** keeps production behind a person, while pre-approved standard changes run at once.

**Splunk** resolves the investigation itself once it sees the verified fixes.

## The Journey

| Lab | What you do | What it proves | Time |
| --- | --- | --- | --- |
| **Lab 1 — Attack and Detect** | Launch the exploit from the attack console, then open the finding and the AI SOC analyst's triage | The SOC sees a known-exploited CVE in use, already triaged | 15 min |
| **Lab 2 — Plan the Response with AI** | Start the investigation, ask the Security Assistant how to respond, complete the containment tasks | A finding becomes a plan that people and AI work through together | 15 min |
| **Lab 3 — Act Through SOAR, with Identity** | Run PatchBot's patch action through Splunk SOAR for the wrong role, then the right one | The agent uses vetted tools, acts for a verified person and can't exceed that person's role | 20 min |
| **Lab 4 — Approve the Normal Change** | Sign in with Cisco Duo as the Change Approver and release production | Standard changes run at once; production waits for a person | 15 min |
| **Lab 5 — Close the Loop and Govern** | See Splunk resolve the investigation, try the attack again, and follow the denied calls in Agent Observability | The fix is proven, and every decision is on the record | 20 min |

## Executive Outcomes

**Exploitation Seen Early** — The SOC sees a known-exploited vulnerability in use as it happens, with the AI SOC analyst's triage attached.

**AI-Planned Response** — The assistant turns a finding into a patch plan the analyst approves in minutes, while the steps only a person can take stay with a person.

**Trusted Agents** — Every action the agent takes uses vetted tools, runs for a verified person and passes a policy check first.

**Governed Automation** — One action hands the work to an agent, pre-approved changes run at once, and production still waits for a person.

**Closed-Loop Proof** — The investigation resolves from verified fixes, and every approval and denial is on the record.
