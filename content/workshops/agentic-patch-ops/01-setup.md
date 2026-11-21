+++
title       = "Setup & Prerequisites"
description = "Open the attack console, Splunk Enterprise Security, the Change Board and Splunk Observability Cloud."
duration    = "5 min"
weight      = 10
+++

All lab work happens in your web browser; there is nothing to install. Before you start Lab 1, confirm you can reach the environments below. Your instructor gives you the addresses and sign-ins for your environment.

## What You Need

- A laptop with a current web browser

## What You Will Use

| **Environment** | **What it is** | **Used in** |
| --- | --- | --- |
| **Attack console** | Replays a known exploit against a PseudoCo web server, at `/attack-ui` on your PseudoCo Assistant address | Labs 1 and 5 |
| **Splunk Enterprise Security** | The finding, the AI SOC analyst's triage, the investigation and its response plan, the Security Assistant, and the Splunk SOAR actions it runs | Labs 1, 2, 3 and 5 |
| **Change Board** | Where a person approves or rejects production changes, at `/change-board-ui` on your PseudoCo Assistant address | Lab 4 |
| **Splunk Observability Cloud** | Splunk Agent Observability: every PatchBot run as a trace, and the Controls that judge each tool call | Lab 5 |
| **Splunk** | The PatchBot app's dashboards, including the Change Chain | Lab 5 (optional) |

## People in the Labs

PatchBot acts for the person named in each request, and takes that person's role from their Cisco Duo groups:

| **Person** | **Role** | **In the labs** |
| --- | --- | --- |
| ravi.patel | Windows Patch Operator | Lab 3.1: asks to patch the Linux web servers and is denied |
| dana.lee | Linux Patch Operator | Lab 3.2: patches the web servers within the change model |
| sam.ortiz | Change Approver | Lab 4: approves the production change on the Change Board |

{{% notice note %}}
The labs act on one set of four web servers per environment, so everyone in the same environment works the same finding and investigation.
{{% /notice %}}

## Access

- Open the **attack console** at `/attack-ui` on your PseudoCo Assistant address.
- Sign in to **Splunk**; Labs 1, 2, 3 and 5 open **Enterprise Security** there.
- Sign in to **Splunk Observability Cloud**; Lab 5 opens **Agent Observability** there.
- For Lab 4, your instructor gives you a one-time passcode for sam.ortiz.
