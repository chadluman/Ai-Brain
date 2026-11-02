---
name: developer-extension-evaluation
description: Evaluate, install, configure, and remove IDE, editor, and browser developer extensions safely, including AI coding assistant extensions. Use when a developer tool, extension, or plugin will read code, run commands, or send data; do not use for hosted services, which are covered by Third-Party Service Evaluation, or for browser scripts on a production site, which are covered by Third-Party Script Governance.
---

# Developer Extension Evaluation

## Outcome

Produce a defensible decision for each developer extension: what it can access, what it sends, how it is updated and removed, and whether its benefit justifies its access — with untrusted or over-privileged extensions rejected, not merely warned about.

An extension is an executable asset, not a documentation reference. It is subject to the root security-review gate at its exact version, even when it is popular, free, or recommended by a colleague or an AI tool.

## Required Inputs

- The extension's purpose: what developer task it actually improves, and what happens if it is not installed.
- Its access: workspace files, terminal, network, credentials, clipboard, browser data, and any AI or cloud service it connects to.
- Its provenance: publisher, marketplace, source repository, version, update mechanism, license, and maintenance state.
- Its data handling: what code, prompts, or telemetry it sends, where it sends it, how long it is retained, and whether it is used for training.

## Workflow

1. Start from the task, not from the marketplace. Name the developer problem, the minimum capability that solves it, and whether a built-in editor feature, a local script, or a smaller extension already solves it.
2. Review the exact version before installation: publisher identity and history, source code or a trusted build if available, requested permissions, declared network destinations, telemetry and data-use statements, and any install-time or update-time scripts. Reject obfuscation, unexplained network calls, credential access, or broad workspace access that the stated purpose does not require.
3. Pay special attention to AI coding assistant extensions: they may send code, prompts, file paths, and repository context to a provider. Check provider retention, training use, region, and subprocessors, and do not use such an extension on private, client, or regulated code until that review is complete and the user has accepted the data handling.
4. Install with least privilege: workspace trust, restricted mode, or a separate profile where the editor supports it; disable the extension for sensitive workspaces; and do not grant it access to credentials, production environments, or unrelated repositories.
5. Define update and removal rules before installation: who may update it, whether auto-update is allowed, how a malicious or compromised update would be detected, and how to remove it completely, including any settings, caches, or cloud data it created.
6. Re-review on version change, publisher change, permission change, or a security advisory. Approval applies only to the reviewed version. A new major version, a new owner, or a new data destination is a new review.

## Safety and Permission Boundaries

- Never install an extension that requests credential, token, or secret access unless that access is the stated purpose, is least-privilege, and has been explicitly reviewed and authorized.
- Never allow an extension to send private code, credentials, or customer data to an unreviewed destination. Telemetry is data transmission, not a harmless default.
- Installing, updating, or removing an extension that touches production, credentials, or private repositories is R2/R3 and requires the authorization that applies to that action.
- Never store secret values in extension settings, prompts, or shared workspace configuration. Record secret names and approved storage locations only.

## Outputs and Evidence

- A review note per extension: purpose, publisher, version, permissions, network destinations, telemetry and data handling, findings, decision, and next review trigger.
- A workspace policy: which extensions are approved, which are prohibited, and which workspaces they may run in.
- A removal test: proof that uninstalling the extension removes its access and, where applicable, its local data, without breaking the project.
