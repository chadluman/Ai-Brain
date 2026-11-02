---
status: approved
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R0
tags: [architecture, map]
sources: []
---

# Architecture Map

This folder holds cross-cutting architecture patterns — guidance that has proven useful across more than one project. It does not hold project-specific decisions, and it does not duplicate skill guidance.

## How to use it

1. Start from a project brief, not from a pattern. Copy the [Project Intake template](../60-Templates/Project%20Intake.md) into a new folder under [50-Projects](../50-Projects/Projects%20Map.md) if you do not have one yet.
2. Use [Architecture Selection](../30-Skills/architecture-selection/Architecture%20Selection.md) to turn the brief into compared options and decisions.
3. Record each material choice with the [Technology ADR template](../60-Templates/Technology%20ADR.md), and keep that ADR inside the project folder, not here.
4. Follow the [Web Application Delivery playbook](../40-Playbooks/Web%20Application%20Delivery.md) for the ordered evidence and approval path.

## What belongs here

- A pattern only when it has been used, or is clearly needed, across projects — for example a recurring boundary, data, identity, or delivery pattern.
- A pattern note should state its context, when it applies, when it does not, its consequences, and its exit or migration path, in the same spirit as an ADR.

## What does not belong here

- A single project's ADR. That lives in that project folder under [50-Projects](../50-Projects/Projects%20Map.md).
- A copy of a skill. Link to the skill instead, and keep one source of truth.
- An empty pattern created to look comprehensive. This folder intentionally starts with this map only; add pattern notes when real projects produce them.

## Navigation

- [Vault Map](../00-System/Vault%20Map.md)
- [Skills Map](../30-Skills/Skills%20Map.md)
- [Playbooks Map](../40-Playbooks/Playbooks%20Map.md)
- [Templates Map](../60-Templates/Templates%20Map.md)
- [Archive Map](../90-Archive/Archive%20Map.md)
