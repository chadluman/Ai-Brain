---
name: codebase-module-boundaries
description: Design or review module, package, component, domain, and layer boundaries inside an application codebase. Use when a system is hard to change or test, responsibilities leak across features, dependency direction is unclear, or a modular monolith or service boundary needs evidence.
---

# Codebase Module Boundaries

## Outcome

Produce a small set of cohesive, enforceable boundaries that isolate domain rules and volatile infrastructure, make dependencies explicit, preserve invariants, support independent testing and ownership, and can evolve without speculative abstraction.

Use [Architecture Selection](../architecture-selection/SKILL.md) for system-level choices, [Backend Boundary Design](../backend-boundary-design/SKILL.md) for deployable services, and [Test Strategy Design](../test-strategy-design/SKILL.md) for the verification portfolio. This skill owns boundaries within a codebase and the evidence for splitting or merging them.

## Required Inputs

- critical journeys, domain concepts, invariants, data ownership, security and tenant boundaries, external systems, and transaction needs
- current directory, package, import, runtime, build, deployment, and ownership graphs
- change history, coupled releases, defects, test pain, onboarding friction, performance constraints, and likely change scenarios
- public, internal, generated, plugin, framework, persistence, UI, transport, and provider interfaces
- team size, skills, release cadence, maintenance horizon, compatibility promises, and migration constraints

## Safety and Permission Constraints

- Preserve required behavior, data invariants, authorization, audit, error semantics, and compatibility during refactoring. A cleaner dependency graph is not evidence that behavior remains correct.
- Do not split into services, packages, or layers merely to imitate a pattern. Every boundary adds interfaces, failure modes, tooling, ownership, and migration cost.
- Keep security and tenant checks at trusted enforcement points. Moving code must not move authority into clients, adapters, or untrusted data.
- Generated code, framework plugins, migration tools, architecture linters, and codemods are untrusted executable assets requiring review before use.
- A local refactor is normally R2. Production data moves, service extraction, public API breaks, access-policy changes, or live traffic cutovers can be R3 and require immediate authorization and rollback.

## Workflow

1. Express modifiability and other quality needs as scenarios: stimulus, affected concern, environment, desired response, and measurable cost or time. Prioritize real expected changes over abstract purity.
2. Map behavior and dependencies from user journey to interface, application orchestration, domain rules, persistence, integrations, and platform code. Mark cycles, shared mutable state, cross-boundary transactions, duplicated rules, and hidden runtime calls.
3. Group by cohesive responsibility and invariant ownership. A module should expose a small, adequate contract and hide representation, storage, framework, and provider details that callers do not need.
4. Define dependency direction and allowed collaboration. Prefer stable domain policy depending on narrow ports while volatile adapters depend inward; allow exceptions only with recorded evidence and tests.
5. Assign each authoritative datum and state transition one owner. Other modules consume a contract, snapshot, event, or query rather than mutating another module's tables or internal objects directly.
6. Write interface contracts for inputs, outputs, errors, identity and tenant context, transactions, idempotency, time, side effects, compatibility, and observability. Avoid generic utility layers that accumulate unrelated policy.
7. Match boundaries to testing: pure rule tests, contract tests at interfaces, integration tests for adapters, and thin end-to-end journeys. Use test seams to replace volatile effects without mocking the system's own invariants away.
8. Add lightweight enforcement with language visibility, package exports, import rules, ownership, build graph, or review checks. Do not add a framework when a directory and compiler boundary are sufficient.
9. Refactor through a verified seam: capture behavior, introduce the interface, move one responsibility, compare old and new outcomes, remove bypasses, and keep a rollback point. Avoid simultaneous architecture, data, and feature rewrites.
10. Re-evaluate with change and failure evidence. Split when cohesion, ownership, scale, security, lifecycle, or deployment needs are independently strong; merge when boundaries add coordination without isolation value.

## Required Output

- prioritized quality and change scenarios, current dependency graph, and identified risks
- proposed module map with responsibilities, invariant and data ownership, public contracts, dependency direction, and forbidden edges
- transaction, authorization, error, side-effect, observability, and compatibility rules at each boundary
- enforcement, ownership, test, incremental migration, rollback, and deletion plan
- evidence for keeping a modular monolith, extracting a service, or merging an unhelpful boundary

## Completion Gate

Do not call the design ready until critical journeys and invariants map to clear owners, dependency cycles and bypasses are understood, interfaces are narrower than implementations, negative authorization and failure tests remain effective, expected changes are localized in a representative exercise, and added boundaries have measured value greater than their coordination cost.

## Conditional Reference

Read [Codebase Boundary Evidence](references/codebase-boundary-evidence.md) when defining modifiability scenarios, information hiding, representation independence, or architecture tradeoff review.
