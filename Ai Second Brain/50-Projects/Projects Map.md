---
status: approved
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R0
tags: [projects, map]
sources: []
---

# Projects Map

This folder holds project-specific work only: briefs, architecture decisions, plans, and notes that would not make sense for another project.

Reusable knowledge stays outside this folder, in Skills, Playbooks, Catalog, and Architecture. If a note starts to help a second project, promote the reusable part out of the project folder and link to it, rather than copying it.

## Starting a project

1. Copy the [Project Intake template](../60-Templates/Project%20Intake.md) into a new folder here, named for the project.
2. Follow the [Web Application Delivery playbook](../40-Playbooks/Web%20Application%20Delivery.md) for the ordered evidence and approval path.
3. Use [Architecture Selection](../30-Skills/architecture-selection/Architecture%20Selection.md) to turn the brief into compared options and decisions.
4. Record each material choice with the [Technology ADR template](../60-Templates/Technology%20ADR.md), inside that project's folder. Prefix ADR filenames with a sequence and decision, such as `ADR-001-web-framework.md`.
5. Review every external skill, script, dependency, extension, or template with the [Security Review template](../60-Templates/Security%20Review.md) before use.
6. Document provider setup with the [Service Integration Playbook template](../60-Templates/Service%20Integration%20Playbook.md).

For a user-facing product, copy the [Interface Design Brief](../60-Templates/Interface%20Design%20Brief.md) and follow [Intentional Interface Design](../40-Playbooks/Intentional%20Interface%20Design.md).

## What belongs in a project folder

- The intake brief, with clearly marked assumptions where facts are not yet known.
- ADRs, with context, options considered, evidence and dates, decision, consequences, risks, costs, and exit path.
- The delivery plan, verification evidence, known limitations, and follow-up decisions.
- Project-specific notes, such as a deployment or operations note for that product only.

## What does not belong here

- A reusable skill, playbook, catalog entry, or architecture pattern. Those live in their own folders and are linked from the project.
- Secret values, credentials, or private data. Record secret names, purpose, owner, and approved storage location only.
- A claim that work is complete when required verification has not run. Distinguish implemented, tested, inferred, and pending items.

## Projects

No project folders exist yet in this snapshot. Add one when a real project starts; do not create placeholder project folders in advance.

## Navigation

- [Vault Map](../00-System/Vault%20Map.md)
- [Architecture Map](../10-Architecture/Architecture%20Map.md)
- [Skills Map](../30-Skills/Skills%20Map.md)
- [Playbooks Map](../40-Playbooks/Playbooks%20Map.md)
- [Templates Map](../60-Templates/Templates%20Map.md)
- [Archive Map](../90-Archive/Archive%20Map.md)
