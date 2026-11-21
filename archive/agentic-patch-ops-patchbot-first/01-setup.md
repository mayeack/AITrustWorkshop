+++
title       = "Setup & Prerequisites"
description = "Open PatchBot, the Change Board, Splunk Agent Observability and Splunk."
duration    = "5 min"
weight      = 10
+++

All lab work happens in your web browser; there is nothing to install. Before you start Lab 1, confirm you can reach the environments below.

## What You Need

- A laptop with a current web browser

## What You Will Use

| **Environment** | **What it is** | **Used in** |
| --- | --- | --- |
| **PatchBot** | The PseudoCo Assistant's patch agent, at `/patchbot-ui` on your PseudoCo Assistant | Labs 1–4 |
| **Change Board** | Where a person approves or rejects PatchBot's production changes, at `/change-board-ui` | Lab 3 |
| **Splunk Agent Observability** | Records every PatchBot request as a trace, and runs the Controls that judge each tool call | Lab 5 |
| **Splunk Enterprise** with **Splunk Enterprise Security** | The PatchBot app's dashboards, and the findings and risk on the person PatchBot acted for | Lab 5 |

## Personas

PatchBot acts with the role of the person who asks. On an environment without Duo sign-in, PatchBot offers five personas, and the labs switch between them:

| **Persona** | **Role** | **Can** |
| --- | --- | --- |
| dana.lee | Linux Patch Operator | Triage, correct the exposure model, open changes, patch Linux servers |
| ravi.patel | Windows Patch Operator | The same for Windows servers |
| sam.ortiz | Change Approver | Approve or reject changes on the Change Board, never their own |
| jo.kim | Patch Viewer | Read findings, activity and resources |
| instructor | Estate owner | Everything above |

{{% notice note %}}
On an environment with Duo sign-in, PatchBot shows **Sign in with Duo** instead of the personas, and your role comes from your Duo groups. Anyone in none of the PatchBot groups is a Patch Viewer.
{{% /notice %}}

## Access

- Open **PatchBot** at `/patchbot-ui` on your PseudoCo Assistant address.
- Sign in to **Splunk Observability Cloud**; Lab 5 opens **Agent Observability** there.
- Sign in to **Splunk**; Lab 5 opens the **PatchBot** app and **Enterprise Security** there.
