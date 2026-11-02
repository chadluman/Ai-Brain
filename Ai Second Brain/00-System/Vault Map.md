---
status: approved
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-31
review_by: 2027-01-21
risk: R0
tags: [system, map]
sources: []
---

# AI Second Brain — Vault Map

## Start Here

This vault is a safety-first working knowledge base for choosing and applying technologies to websites and applications. The project's root `AGENTS.md` governs AI work; the [Operating Principles](Operating%20Principles.md) provide its vault-facing summary.

For a new product idea:

1. Copy the [Project Intake template](../60-Templates/Project%20Intake.md) into a new folder under `50-Projects/`.
2. Follow the [Web Application Delivery playbook](../40-Playbooks/Web%20Application%20Delivery.md) for the ordered evidence and approval path.
3. Use [Architecture Selection](../30-Skills/architecture-selection/Architecture%20Selection.md) to turn the brief into compared options and decisions.
4. Record each material choice with the [Technology ADR template](../60-Templates/Technology%20ADR.md).
5. Review every external skill, script, dependency, extension, or template with the [Security Review template](../60-Templates/Security%20Review.md) before use.
6. Document provider setup with the [Service Integration Playbook template](../60-Templates/Service%20Integration%20Playbook.md).

For a user-facing product, copy the [Interface Design Brief](../60-Templates/Interface%20Design%20Brief.md) and follow [Intentional Interface Design](../40-Playbooks/Intentional%20Interface%20Design.md). Use the [Design Reference Catalog](../20-Catalog/Design/Design%20Reference%20Catalog.md) to route focused precedent research without treating galleries, code libraries, or generators as pre-approved assets.

## Active Navigation

| Area | Purpose | Current entry point |
|---|---|---|
| System | Rules, navigation, vocabulary, and maintenance | [Operating Principles](Operating%20Principles.md), [Research Standard](Research%20Standard.md), [Research Queue](Research%20Queue.md), [Maintenance Log](Maintenance%20Log.md), this note, and the [Glossary](Glossary.md) |
| Catalog | Qualified sources and evaluated technologies | [Source Registry](../20-Catalog/Sources/Source%20Registry.md), [Backend and Database Services](../20-Catalog/Backend%20and%20Database%20Services.md), and [Design Reference Catalog](../20-Catalog/Design/Design%20Reference%20Catalog.md) |
| Skills | Focused AI operating instructions | [Skills Map](../30-Skills/Skills%20Map.md) |
| Playbooks | Ordered, end-to-end delivery procedures | [Playbooks Map](../40-Playbooks/Playbooks%20Map.md) |
| Templates | Repeatable project and review records | [Templates Map](../60-Templates/Templates%20Map.md) |

Folders for architecture patterns, catalog entries, playbooks, projects, and archives should be created only when they receive real content.

## Status Vocabulary

- `draft`: incomplete and not ready for operational reliance
- `reviewed`: inspected, with findings recorded, but not necessarily approved
- `approved`: suitable for its documented scope and exact reviewed version
- `deprecated`: still present for transition but should not be selected for new work
- `retired`: historical only

## Naming

- Use clear title-case filenames for notes.
- Use lowercase hyphenated folder names for skills.
- Prefix ADR filenames with a sequence and decision, such as `ADR-001-web-framework.md`.
- Put project-specific decisions inside that project's folder; keep reusable knowledge outside projects.

## Maintenance Queue

Review a note when its `review_by` date arrives or when a security, compatibility, pricing, licensing, or major-version change affects it. Update the source note and archive superseded material instead of creating contradictory copies.

## Current Build Status

| Item | State |
|---|---|
| Root operating contract | Approved |
| Vault map and glossary | Approved |
| Starter templates | Core templates approved for first use; interface design brief is draft pending representative project use |
| Architecture Selection | Draft pending realistic project validation |
| Research waves | Focused skills drafted or maintained; all 138 currently present skill formats and local links validated on 2026-10-31, including 11 reviewed Bootstrap 6 prerelease skills |
| Technology catalog | Source registry, design-reference catalog, and six-service backend/database shortlist reviewed; exact provider/plan/asset decisions remain project-driven |
| End-to-end web application playbook | Drafted and link-validated; pending representative project exercise |
| Intentional interface design playbook | Drafted and link-validated; pending representative design-to-implementation exercise |


