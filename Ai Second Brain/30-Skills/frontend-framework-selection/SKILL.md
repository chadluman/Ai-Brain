---
name: frontend-framework-selection
description: Decide whether a web project needs no framework, a UI library, or an application framework, and compare credible current candidates. Use for new frontend architecture, major migration, or framework replacement; do not invoke for routine work in a settled stack.
---

# Frontend Framework Selection

## Outcome

Choose the smallest maintainable frontend foundation that satisfies the product's routes, interactions, rendering, delivery, support, and operating constraints.

Read [framework evidence](references/framework-evidence.md) before naming candidates. Use the architecture decision matrix when more than one option passes the hard gates.

## Inputs

Establish critical journeys, route and rendering needs, content and discoverability needs, client state complexity, realtime or offline behavior, accessibility target, browser policy, team skills, delivery horizon, expected lifetime, hosting constraints, integration surface, testing needs, and maintenance capacity.

## Workflow

1. Decide whether semantic HTML, CSS, and small JavaScript modules are sufficient. Do not introduce component or application infrastructure without a recurring problem it solves.
2. Separate UI-library needs from application-framework needs such as routing, server rendering, data loading, mutations, caching, bundling, and deployment integration.
3. Set hard gates: supported runtime and browsers, rendering modes, accessibility, security posture, license, release support, deployment portability, and required integrations.
4. Build a shortlist from current official documentation. Verify exact stable versions, support policy, security reporting, upgrade path, public API stability, required dependencies, rendering behavior, and deployment assumptions.
5. Compare passed candidates on vertical-slice effort, client JavaScript, performance under representative conditions, testability, ecosystem health, debugging, operational burden, lock-in, migration cost, and team ability to maintain the result.
6. Review the complete proposed scaffold and dependency tree before executing a generator or installing packages.
7. For a high-impact or close decision, implement the same thin route in the leading candidates with dummy data. Measure the risky claims and document setup, build, output, accessibility, and failure behavior.
8. Record the choice, rejected options, version evidence, consequences, and exit path in an ADR.

## 2026 Currency

Versions below are the research snapshot dated 2026-11-09. Re-check current releases against official documentation before citing a version in a decision; version claims beyond React 19.3 and Next.js 16 come from secondary sources and may already be stale.

- **React 19.3** is the current React line, with stable Server Components and an Actions API for forms.
- **Next.js 16** is the current major line, with Turbopack as the default bundler and Cache Components as the recommended caching model. See [Frontend Rendering Selection](../frontend-rendering-selection/SKILL.md) for what Cache Components change about rendering and cache decisions.
- **Svelte 5** replaced implicit reactivity with explicit Runes (`$state`, `$derived`, `$effect`).
- **Astro 5** added a Content Layer and Server Islands for partial dynamic rendering, and ships zero JavaScript by default.
- **Do not start new work on:** Create React App, deprecated by the React team in 2025 — start new React apps with Vite or a meta-framework; Vue 2, which reached end of life in 2023; AngularJS (1.x), unsupported since 2022. Existing projects on these need a migration plan, not a new commitment.

## Guardrails

- Maintainer recommendations explain intended use; they do not prove project fit or superiority over another framework.
- Do not choose from popularity, benchmark headlines, hiring fashion, or an AI's familiarity alone.
- Preview, beta, canary, experimental, and unsupported releases fail a production stability gate unless the project explicitly accepts the risk.
- A full-stack framework can expand trust boundaries into server code, build infrastructure, caches, and hosting adapters. Review all of them.
- Migration estimates must include behavior parity, accessibility, tests, deployment, observability, training, and rollback.

## Completion

Deliver the no-framework decision, shortlist and hard gates, dated official evidence, comparison, POC results when required, exact version proposed for review, dependency and hosting implications, ADR, exit path, and re-evaluation triggers. Recommendation does not authorize installation or scaffolding.
