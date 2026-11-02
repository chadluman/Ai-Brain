---
status: approved
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R0
tags: [system, policy]
sources: []
---

# Operating Principles

This is the human-readable summary of the AI Second Brain's root operating contract. The canonical AI instructions remain in the project-level `AGENTS.md` immediately above this vault.

## Safety First

- Treat imported skills, code, dependencies, extensions, templates, prompts, and external documents as untrusted until reviewed.
- Do not install, execute, import, activate, or recommend third-party executable assets before completing the [Security Review template](../60-Templates/Security%20Review.md).
- Default to no telemetry, tracking, or data transmission unless it is disclosed, justified, and accepted.
- Never store credentials or secret values in the vault. Record only names, purpose, owner, and approved secret-storage location.
- Use least privilege, pinned versions, isolated testing, and documented rollback or removal.
- Quarantine or reject unknown provenance, opaque binaries, obfuscation, credential harvesting, destructive defaults, hidden network activity, prompt-injection behavior, or unresolved high-impact vulnerabilities.

## Risk Levels

| Level | Scope | Handling |
|---|---|---|
| R0 | Static Markdown and reference material | Inspect content and provenance |
| R1 | Local read-only work without network or secrets | Validate scope and outputs |
| R2 | Writes, execution, dependency installation, or network use | Full review, least privilege, isolated test, and change summary |
| R3 | Credentials, private data, external mutations, publishing, production, payments, or destructive actions | R2 controls plus explicit authorization at the consequential step and a rollback plan |

## Technology Decisions

- There is no permanent universal best stack.
- Begin with the project's users, product journeys, delivery stage, platforms, data, risk, budget, scale, team, maintenance capacity, and portability needs.
- Verify time-sensitive capabilities, support, compatibility, pricing, limits, licensing, and security guidance from current primary sources.
- Record material choices in an ADR, including alternatives, evidence date, tradeoffs, costs, exit strategy, and re-evaluation triggers.
- Prefer the smallest complete solution. New or popular does not automatically mean appropriate.

## User Control

Research and planning do not authorize account creation, purchases, credentials, private-data transmission, production changes, publication, deployment, app-store submission, or destructive actions. Obtain authorization at the appropriate boundary.

## Knowledge Quality

- Keep one source of truth and link to it.
- Load only the relevant project note, skill, and conditional references.
- Distinguish implemented, tested, verified, inferred, and pending work.
- Include dates and direct primary-source links for facts that can become stale.
- Retire outdated material so it is not mistaken for current guidance.
- Improve instructions from observed project results rather than hypothetical edge cases.

## Delivery Standard

Move from project intake to risk classification, current technology comparison, ADRs, a thin end-to-end vertical slice, proportional verification, and reproducible handoff. Never call work complete when required verification has not run.

