---
name: teach-web-architecture-leadership
description: Teach web architecture and technical leadership through requirements, ADRs, system boundaries, tradeoffs, cost, capacity, risk, communication, and incremental delivery. Use for senior-level design practice, architecture interviews, mentoring, or project-planning curricula.
---

# Teach Web Architecture and Leadership

## Outcome

Help the learner turn ambiguous product needs into a small, evidence-backed architecture and communicate decisions, consequences, uncertainty, and change paths clearly.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

- [Product Discovery and Scope](../product-discovery-scope/SKILL.md) for users, journeys, outcomes, constraints, risks, and a thin validation plan.
- [Architecture Selection](../architecture-selection/SKILL.md) for system boundaries, candidate comparison, ADRs, vertical slices, and exit paths.
- [Information Architecture and Routing](../information-architecture-routing/SKILL.md) when user navigation, URLs, and content structure are material.
- [Third-Party Service Evaluation](../third-party-service-evaluation/SKILL.md) for service fit, permissions, cost, operations, and exit.
- [Product Economics Planning](../product-economics-planning/SKILL.md), [Capacity and Cost Planning](../capacity-cost-planning/SKILL.md), and [Hosting and Runtime Selection](../hosting-runtime-selection/SKILL.md) for delivery and operating economics.
- [Service Resilience Design](../service-resilience-design/SKILL.md), [Multi-Region Resilience Design](../multi-region-resilience-design/SKILL.md), and [Privacy and Data Governance](../privacy-data-governance/SKILL.md) when requirements justify them.

## Teaching Priorities

Begin with users, critical journeys, success measures, constraints, and risk. Separate hard requirements from preferences and guesses. Have the learner propose the smallest vertical slice, identify trust and failure boundaries, compare credible options, and write a short ADR with an exit path.

Use scenario changes—traffic growth, reduced budget, regional requirement, dependency outage, team turnover, or deadline compression—to test whether the architecture and reasoning adapt. Assess communication to product, design, security, operations, and future maintainers, not diagram polish alone.

For senior-level practice, require explicit assumptions, estimates with ranges, organizational ownership, irreversible-versus-reversible decision classification, re-evaluation triggers, and a migration or rollback path.

## Boundaries

- Do not reward complexity, diagram count, or fashionable infrastructure as evidence of seniority.
- Architecture instruction does not authorize service purchase, account creation, deployment, production-data movement, or external-system change.
- Recheck current service capabilities, versions, pricing, limits, licensing, support, and security guidance before using them as decision evidence.
- Identify where qualified legal, privacy, financial, accessibility, or security review is needed rather than presenting architectural judgment as that review.

## Completion

The learner delivers a decision-ready brief, a bounded architecture, a thin vertical slice, one or more material ADRs, evidence and uncertainty labels, risk and cost implications, ownership, verification steps, and re-evaluation or exit triggers.
