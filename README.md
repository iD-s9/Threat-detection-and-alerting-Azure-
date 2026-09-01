# Azure Defender for Cloud: Threat Detection & Alerting

## Problem

Without active monitoring, security misconfigurations and risky administrative activity in a cloud environment can go unnoticed until it's too late. This project sets up Azure's built-in detection and posture management tools, then wires up an automated alert so administrative activity is surfaced directly to my inbox rather than requiring manual checks.

## What I built

- Enabled **Microsoft Defender for Cloud** on the subscription, specifically the **Foundational CSPM (Cloud Security Posture Management)** plan, the free tier that continuously assesses resource configuration against security best practices. All paid plans (Servers, Storage, Containers, etc.) were left disabled since they weren't needed for this project.
- Reviewed the account's **security posture**: 0 Critical, 0 High, 0 Medium, and 0 Low severity recommendations were flagged at time of review, reflecting the least-privilege setup already in place from the RBAC project.
- Created an **Azure Monitor alert rule** scoped to the subscription, triggered on the **"All Administrative operations"** Activity Log signal, meaning any admin-level change across the account raises an alert.
- Built an **action group** connected to the alert rule that sends an email notification whenever the alert condition is met, so security-relevant activity reaches me without needing to check the portal manually.

## Evidence

| State | Screenshot |
|---|---|
| Defender plans — only Foundational CSPM enabled | [`Defender-plans.png`](./Screenshots/Defender-plans.png) |
| Security posture report — 0 critical/high/medium/low recommendations | [`Defender-report.png`](./Screenshots/Defender-report.png) |
| Alert rule created and enabled | [`Alert-rule.png`](./Screenshots/Alert-rule.png) |

## What I learned / next steps

Defender for Cloud's full recommendation catalog (under Security Policies) contains close to 1,800 possible checks, covering everything from Kubernetes cluster hardening to database configuration — most of which don't apply to a small account like this one. The more useful view for a real environment is Security Posture, which filters that catalog down to findings that actually apply to deployed resources.

A natural next step would be testing the alert end-to-end by triggering a real administrative change (e.g. creating or deleting a resource) and confirming the email notification arrives, then expanding the alert conditions to cover more specific signals (like failed sign-in attempts or role assignment changes) rather than the broad "all administrative operations" signal used here.

## Tools used

Microsoft Azure (Free Tier), Microsoft Defender for Cloud, Azure Monitor, Action Groups
