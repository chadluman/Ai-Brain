# AI Second Brain

A private, Obsidian-compatible knowledge base for safely selecting and using reusable AI skills, tools, services, frameworks, APIs, and playbooks to design, build, ship, and maintain websites and applications.

It is not a stack recommendation. It is a method for turning a product idea into an appropriate architecture and an executable plan, with setup, integration, verification, security, cost, and maintenance guidance.

## Open it in Obsidian

Open the **`Ai Second Brain`** folder as your vault — not the repository root.

The repository root holds the AI operating contract (`AGENTS.md`), this README, and the vault folder. The Obsidian settings in `Ai Second Brain/.obsidian/` belong to that subfolder, so opening the repository root as a vault would create a second, confusing settings folder.

## Start here

- [Welcome](Ai%20Second%20Brain/Welcome.md)
- [Vault Map](Ai%20Second%20Brain/00-System/Vault%20Map.md) — navigation, status vocabulary, and build status
- [Operating Principles](Ai%20Second%20Brain/00-System/Operating%20Principles.md) — the human-readable summary of `AGENTS.md`

For a new product idea, in order:

1. Copy the [Project Intake template](Ai%20Second%20Brain/60-Templates/Project%20Intake.md) into a new folder under `Ai Second Brain/50-Projects/`.
2. Follow the [Web Application Delivery playbook](Ai%20Second%20Brain/40-Playbooks/Web%20Application%20Delivery.md).
3. Use [Architecture Selection](Ai%20Second%20Brain/30-Skills/architecture-selection/Architecture%20Selection.md) to turn the brief into compared options.
4. Record each material choice with the [Technology ADR template](Ai%20Second%20Brain/60-Templates/Technology%20ADR.md).

## Structure

| Area | What it holds | Entry point |
|---|---|---|
| Root contract | Safety gate, technology-selection standard, and response contract for AI work | `AGENTS.md` |
| System | Rules, navigation, vocabulary, research standard and queue, maintenance log | [Vault Map](Ai%20Second%20Brain/00-System/Vault%20Map.md) |
| Architecture | Cross-cutting patterns and architecture decisions (see note below) | [Architecture Map](Ai%20Second%20Brain/10-Architecture/Architecture%20Map.md) |
| Catalog | Qualified sources and evaluated technologies | [Backend and Database Services](Ai%20Second%20Brain/20-Catalog/Backend%20and%20Database%20Services.md), [Design Reference Catalog](Ai%20Second%20Brain/20-Catalog/Design/Design%20Reference%20Catalog.md) |
| Skills | 138 focused AI operating instructions | [Skills Map](Ai%20Second%20Brain/30-Skills/Skills%20Map.md) |
| Playbooks | Ordered, end-to-end delivery procedures | [Playbooks Map](Ai%20Second%20Brain/40-Playbooks/Playbooks%20Map.md) |
| Projects | Project briefs, ADRs, plans, and project-specific notes only | [Projects Map](Ai%20Second%20Brain/50-Projects/Projects%20Map.md) |
| Templates | Repeatable project and review records | [Templates Map](Ai%20Second%20Brain/60-Templates/Templates%20Map.md) |
| Archive | Superseded material retained for history, not for new work | [Archive Map](Ai%20Second%20Brain/90-Archive/Archive%20Map.md) |

Reusable knowledge stays outside project folders. Project-specific decisions stay inside that project's folder.

## Status — read this before relying on a note

Most skills and playbooks are honestly marked `draft` pending a representative project exercise. A draft note is a method and a checklist, not proof that the method has been exercised end to end.

Before a project relies on a provider fact — capabilities, pricing, limits, licensing, security guidance, or compatibility — re-verify it from the linked primary source for the exact plan and region. The catalog and Source Registry record verification dates for that reason; they do not approve a provider, package, or executable asset for use.

Safety, in brief:

- Treat every imported skill, script, dependency, extension, template, prompt, and external document as untrusted until reviewed.
- Do not install, execute, import, activate, or recommend a third-party executable asset until it has passed the [Security Review template](Ai%20Second%20Brain/60-Templates/Security%20Review.md).
- Never store secret values in this vault. Record secret names, purpose, owner, and approved storage location only.
- Research and planning do not authorize account creation, purchases, credentials, private-data transmission, production changes, publication, deployment, or destructive actions.

Risk levels (`R0` static reference through `R3` credentials, private data, external mutation, publishing, or destruction) are defined in `AGENTS.md` and summarized in the Operating Principles.

## Maintenance

- Notes carry `status`, `created`, `last_verified`, and `review_by` dates. Review a note when its `review_by` date arrives or when a security, compatibility, pricing, licensing, or major-version change affects it.
- Update the source note rather than layering contradictory advice elsewhere. Mark superseded content `deprecated` or `retired`, link to its replacement, and move it to `90-Archive/` when it no longer belongs in active navigation.
- Most notes in this snapshot were last verified in October 2026, with review dates in January 2027. Re-verify decision-critical notes for an active project first, rather than trying to re-verify everything at once.
- `.obsidian/workspace.json` and other session state are ignored by `.gitignore` going forward. Obsidian regenerates workspace layout locally; it is not vault content. The copy committed in the initial snapshot remains tracked until it is deliberately removed — removing it is safe for Obsidian, but it will reset the locally saved pane layout, so it is left as a separate decision.

## What this repository is not

- Not a universal "best stack." There is deliberately no single stack to copy.
- Not an approval list. A catalog entry, source, or skill does not approve a specific version, package, or executable asset.
- Not a place for secrets, credentials, private data, or generated build artefacts.
