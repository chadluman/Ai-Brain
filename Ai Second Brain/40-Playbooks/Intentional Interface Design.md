---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R2
tags: [playbook, design, ux, frontend, quality]
sources: []
---

# Intentional Interface Design

## Purpose

Use this playbook to turn a product brief into an original, coherent, accessible, and verifiably functional interface. It prevents “vibe coding” by requiring traceable design intent, real states and content, lawful precedent study, a maintained visual architecture, and quality evidence before release.

This playbook does not authorize third-party asset import, account creation, payment, source extraction, private-data capture, production deployment, or public release.

## Design Record

Maintain one [Interface Design Brief](../60-Templates/Interface%20Design%20Brief.md) inside the project. Link to evidence rather than pasting galleries or duplicating standards.

| Phase | State | Evidence | Blocking decision |
|---|---|---|---|
| Frame | not-started |  |  |
| Study | not-started |  |  |
| Direct | not-started |  |  |
| Systematize | not-started |  |  |
| Prototype | not-started |  |  |
| Implement | not-started |  |  |
| Qualify | not-started |  |  |

Use `not-started`, `active`, `blocked`, or `complete`. A phase is complete only when its exit evidence exists.

## 1. Frame the Experience

1. Start from the [Project Intake](../60-Templates/Project%20Intake.md): users, product promise, critical journeys, measurable success, risks, platforms, content, and constraints.
2. Identify what users must understand, feel, and accomplish. Functional understanding and task success take precedence over emotional tone.
3. Inventory real content, data ranges, user roles, locales, permissions, and states. Mark assumptions that will use fixtures.
4. Define accessibility, browser/device, input, performance, privacy, and maintenance boundaries.

Exit: a design-ready brief, critical-journey map, representative content set, and named acceptance evidence.

## 2. Study Precedents Lawfully

1. Use the [Design Reference Catalog](../20-Catalog/Design/Design%20Reference%20Catalog.md) to find sources for a named problem, not to browse until a style feels exciting.
2. Use [Interface Pattern Reconstruction](../30-Skills/interface-pattern-reconstruction/Interface%20Pattern%20Reconstruction.md) for focused product studies.
3. Compare multiple precedents. Record the functional principle, why it works, where it fails, what is protected or excluded, and how this product will differ.
4. Do not import assets or code during research. Quarantine candidates for exact-version review.

Exit: provenance and authorization record, principle-versus-expression matrix, behavior specifications, and originality risks.

## 3. Establish Direction

Use [Product Design Direction](../30-Skills/product-design-direction/Product%20Design%20Direction.md) to create the experience contract, design thesis, principles, anti-principles, grayscale hierarchy, semantic color architecture, typography, layout rhythm, shape, icon and imagery language, motion rules, and one or two product-specific signature expressions.

Compare plausible directions when the decision affects brand, cost, or longevity. Choose from evidence, not trend.

Exit: accepted direction with representative critical, dense, sparse, error, and small-viewport specimens.

## 4. Systematize Without Flattening the Product

1. Use [Design System Selection](../30-Skills/design-system-selection/Design%20System%20Selection.md) to choose only the CSS, token, primitive, component, documentation, and governance layers the product needs.
2. Define ownership from primitives to semantic tokens, components, patterns, and page composition. Record intentional exceptions.
3. Use [Information Architecture and Routing](../30-Skills/information-architecture-routing/Information%20Architecture%20and%20Routing.md) for navigation, labels, URLs, deep links, and route transitions.
4. Review exact external assets with [Software Supply Chain Review](../30-Skills/software-supply-chain-review/Software%20Supply%20Chain%20Review.md) before import.

Exit: UI-layer map, component/state inventory, token and theme model, approved asset list, and removal paths.

## 5. Prototype the Whole Critical Journey

Prototype one end-to-end journey with realistic content and these states where applicable: initial, loading, empty, partial, success, validation error, system error, timeout, offline, unauthorized, disabled, destructive confirmation, undo, and recovery.

Test comprehension and task completion with representative users at the lowest fidelity that answers the question. Test keyboard and touch behavior, focus movement, zoom/reflow, reduced motion, small and large viewports, long translations, and content extremes before polishing secondary screens.

Exit: observed task evidence, updated decisions, state-complete prototype, and stopped or revised ideas.

## 6. Implement a Vertical Slice

1. Build semantic structure and working behavior before decorative effects.
2. Keep content, tokens, component contracts, and state transitions traceable to the brief.
3. Prefer platform capabilities and approved dependencies. Add effects only after meaning, budget, fallbacks, and maintenance are defined.
4. Verify changes with representative fixtures at each increment. Preserve the same source of truth in design and code.

Exit: working critical journey with tested states, responsive behavior, approved assets, and documented exceptions.

## 7. Qualify the Interface

Use [Interface Quality Review](../30-Skills/interface-quality-review/Interface%20Quality%20Review.md) for intent, state completeness, hierarchy, coherence, responsive behavior, interaction craft, originality, and release findings. Use [Web Accessibility Review](../30-Skills/web-accessibility-review/Web%20Accessibility%20Review.md), [Web Performance Plan](../30-Skills/web-performance-plan/Web%20Performance%20Plan.md), [Web Platform Compatibility](../30-Skills/web-platform-compatibility/Web%20Platform%20Compatibility.md), and [Software Quality Review](../30-Skills/software-quality-review/Software%20Quality%20Review.md) for specialist evidence.

Release evidence must name the build, environments, content fixtures, journeys, viewports, themes, input modes, checks run, results, accepted risks, untested areas, and owners. A screenshot approval is not release qualification.

## Completion

The interface is ready only when the critical journeys work across required states and environments; major design choices trace to user or product intent; protected expression and unreviewed assets are excluded; accessibility, performance, compatibility, and quality evidence meet the project's gates; and remaining gaps have explicit owners and dates.

This first edition remains `draft` until used on a representative project. Record routing confusion, missing states, subjective review disputes, asset-review friction, and observed user failures, then revise this playbook instead of layering a competing process.
