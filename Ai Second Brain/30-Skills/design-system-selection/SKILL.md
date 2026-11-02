---
name: design-system-selection
description: Select and govern CSS architecture, design tokens, component libraries, and reusable UI patterns for a web product. Use when choosing between native CSS, scoped styles, utility CSS, a component kit, or a multi-product design system; do not add a design-system platform when a small style layer is sufficient.
---

# Design System Selection

## Outcome

Create an accessible, portable, and maintainable UI foundation whose complexity matches the number of products, themes, contributors, and repeated components.

Read [UI system evidence](references/ui-system-evidence.md) before recommending a token format, CSS framework, or component source.

## Inputs

Establish brand and theme needs, product and platform count, component repetition, accessibility requirements, browser policy, visual change rate, designer-developer workflow, team ownership, localization, right-to-left support, performance budgets, delivery schedule, and willingness to maintain shared infrastructure.

## Workflow

1. Inventory recurring decisions and components. Distinguish a style guide, token set, component library, pattern library, and governed design system.
2. Start with native semantic elements and CSS custom properties when they satisfy the need. Add scoping, utilities, components, or generation only for observed repetition or consistency problems.
3. Compare plausible layers independently: CSS architecture, token exchange, primitives, composed components, documentation, and visual testing. Avoid adopting a complete suite for one needed layer.
4. Evaluate candidates against accessibility behavior, browser floor, theming, responsive and forced-color behavior, reduced motion, localization, markup ownership, override cost, client JavaScript, bundle output, license, dependencies, release policy, maintenance, and removal path.
5. Define tokens by semantic intent before component-specific aliases. Keep source-of-truth ownership and generated artifacts explicit.
6. Prototype high-risk components and states: keyboard operation, focus, errors, loading, empty, overflow, high zoom, long translations, RTL, high contrast, reduced motion, and touch.
7. Review the exact package, generator, copied component source, plugin, and build integration before use. Copied code remains owned code and must be maintained.
8. Record the layers selected, version boundaries, governance, test expectations, and exit path in an ADR.

## Guardrails

- A component library cannot guarantee accessibility after composition, styling, content, and application state are added.
- Do not encode raw brand values throughout components; preserve a replaceable semantic boundary.
- Do not add runtime theming, token transformation, documentation platforms, or visual-test services unless the product and team need them.
- Generated CSS and copied components must remain inspectable, reproducible, and attributable under their licenses.
- Never send private design files or product data to a design service without authorization and data review.

## Completion

Deliver the UI-layer map, selected and rejected options, token model if needed, representative component evidence, accessibility and browser tests, dependency and build impact, ownership and contribution rules, upgrade and rollback plan, ADR, and re-evaluation triggers.
