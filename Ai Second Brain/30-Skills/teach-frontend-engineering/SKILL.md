---
name: teach-frontend-engineering
description: Teach production-minded frontend engineering through UI architecture, rendering, state, forms, accessibility, performance, discoverability, and progressive projects. Use for frontend tutoring, curricula, code walkthroughs, or review practice beyond basic browser syntax.
---

# Teach Frontend Engineering

## Outcome

Help the learner turn user journeys into accessible, resilient interfaces and explain the architectural and product tradeoffs behind the implementation.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

- [Frontend Rendering Selection](../frontend-rendering-selection/SKILL.md) for route-level static, server, client, streamed, or hybrid rendering.
- [Frontend Framework Selection](../frontend-framework-selection/SKILL.md) when framework choice or migration is itself the lesson.
- [Frontend State Design](../frontend-state-design/SKILL.md) for ownership, lifetime, persistence, server synchronization, optimistic work, and conflicts.
- [Design System Selection](../design-system-selection/SKILL.md) for tokens, components, CSS strategy, and UI governance.
- [Web Form Design](../web-form-design/SKILL.md) and [Web Accessibility Review](../web-accessibility-review/SKILL.md) for inclusive interaction and validation.
- [Web Performance Plan](../web-performance-plan/SKILL.md), [Web Platform Compatibility](../web-platform-compatibility/SKILL.md), [Web Discoverability and SEO](../web-discoverability-seo/SKILL.md), [Web Internationalization](../web-internationalization/SKILL.md), or [PWA and Offline Design](../pwa-offline-design/SKILL.md) only when the request reaches those concerns.
- [Interface Quality Review](../interface-quality-review/SKILL.md) for critique and release-candidate review practice.

## Teaching Priorities

Start from a critical user journey and its states: initial, loading, empty, success, invalid, unauthorized, partial, offline, and failed. Teach semantic structure and native behavior before component abstraction. Make data ownership, rendering boundaries, URL behavior, focus management, responsive layout, and recovery paths explicit.

Use a vertical slice that can be exercised in a browser. Require observable checks for keyboard access, assistive semantics, responsive states, slow or failed requests, stale data, and the performance behaviors material to the journey.

For senior-level practice, ask the learner to compare an alternative design, identify coupling and change cost, define an escape path, and review the interface from both user and operator perspectives.

## Boundaries

- Preserve a settled project stack unless framework change is the learning objective.
- Do not equate component reuse with good product design or abstraction depth with seniority.
- Do not hide server trust boundaries, authorization, or data validation behind client state.
- Teaching examples with mocked data or ideal networks must say so and include a path to failure-state exercises.

## Completion

The learner demonstrates the journey in supported states, explains rendering and state ownership, verifies accessibility and failure behavior, identifies performance and compatibility evidence still needed, and can justify when a simpler or different frontend design would fit better.
