---
name: documentation-handoff
description: Design, review, and deliver technical documentation, onboarding, runbooks, architecture references, maintenance ownership, deprecation, and operational handoff. Use before another person or team must build, operate, support, audit, migrate, or retire a system without relying on oral memory.
---

# Documentation and Handoff

## Outcome

Deliver a small, navigable, tested documentation set that lets each intended reader perform real work, understand key decisions, verify system state, respond to failure, and maintain or retire the system safely.

## Required Inputs

- reader roles, tasks, prior knowledge, access, environments, and accessibility needs
- system boundaries, repositories, services, data, owners, providers, dependencies, and ADRs
- setup, build, test, release, operation, support, incident, recovery, migration, and retirement workflows
- secret names, approved storage, account roles, cost owners, review dates, and escalation contacts
- known limitations, open risks, pending decisions, and evidence locations

## Safety and Permission Constraints

- Never place secret values, private keys, production tokens, recovery codes, unnecessary personal data, exploit details, or broad privileged commands in general documentation.
- Examples must use obviously synthetic data and safe targets. Mark destructive, paid, production, external, or irreversible steps and require immediate authorization.
- Do not claim a command, setup, restore, rollback, or runbook works unless it was exercised in the stated environment or clearly marked unverified.
- Keep one source of truth and link to it. Generated copies must identify their source and refresh process or they will drift.
- Publishing documentation, granting access, transferring ownership, or removing the prior owner's access is R3 when it exposes private material or changes external systems.

## Workflow

1. Identify readers and the decisions or tasks they must perform. Separate learning, goal-directed procedures, lookup reference, and explanatory context when that improves retrieval.
2. Start from the nearest map. Inventory existing notes, ADRs, provider playbooks, code reference, diagrams, runbooks, dashboards, and tickets; remove or link duplicates.
3. Write a short system orientation: purpose, users, boundaries, data classes, environments, dependencies, owners, critical journeys, and known limits.
4. Make procedures executable: prerequisites, exact scoped action, expected observation, failure branches, verification, rollback, permissions, cost, and evidence date.
5. Keep reference factual and versioned: schemas, interfaces, configuration names, roles, limits, compatibility, ownership, and source links. Put rationale and tradeoffs in ADRs or explanation.
6. Cover clean setup, development, testing, release, monitoring, alerts, support, incident response, backup restore, migrations, provider failure, cost controls, access recovery, and retirement in proportion to risk.
7. Have a representative new operator follow the docs in an isolated environment without oral correction. Record every ambiguity, missing permission, stale step, and undocumented dependency.
8. Verify links, commands where safe, expected outputs, screenshots only when necessary, accessibility, search terms, ownership, and review triggers.
9. Hand off through an explicit acceptance review. Record unresolved risks, accounts, on-call or support readiness, pending R3 actions, and the exact date responsibility changes.
10. Mark superseded material, link its replacement, preserve required history, revoke obsolete access when authorized, and keep maintenance tied to releases and incidents.

## Required Output

- reader and task inventory
- system orientation and map to source-of-truth notes
- tested setup, verification, operation, failure, recovery, and retirement procedures
- versioned interfaces, configuration names, limits, roles, and provider references
- ownership, access, cost, support, incident, and review schedule
- handoff exercise findings, acceptance record, unresolved risks, and follow-up owners

## Completion Gate

Do not call handoff complete until a representative receiver can use the documentation to set up or inspect the system, handle a defined failure, locate decisions and owners, and explain unresolved risks without undocumented assistance.

## Conditional Reference

Read [Documentation Evidence](references/documentation-evidence.md) when organizing document types, writing portable Markdown, or qualifying production readiness.
