---
name: interface-quality-review
description: Review a website or application interface for design intent, functional completeness, coherence, responsive behavior, interaction craft, originality, and release readiness. Use when a UI feels generic, inconsistent, unfinished, or “vibe coded,” or before shipping a material interface change; route deep accessibility, performance, or security findings to their specialist reviews.
---

# Interface Quality Review

## Outcome

Produce prioritized, reproducible findings that separate broken behavior, missing states, system drift, weak hierarchy, inaccessible or costly polish, and subjective preference. The review tests the interface against its own brief and product needs rather than a universal aesthetic.

Read [Interface Quality Gates](references/interface-quality-gates.md) before reviewing a full flow or release candidate.

## Required Inputs

- product and interface brief, design thesis, supported platforms, critical journeys, and success criteria
- target build or prototype, representative content and data, themes, breakpoints, and known constraints
- token or style source of truth, component/state inventory, accepted exceptions, and reference provenance
- tests already run and areas explicitly outside the review

If no design thesis or acceptance criteria exist, report that as the first process finding and reconstruct a minimal contract with [Product Design Direction](../product-design-direction/SKILL.md) before judging polish.

## Review Order

1. **Task truth:** Can each critical user complete the journey, understand state, recover from failure, and trust the result?
2. **State completeness:** Are loading, empty, partial, success, error, timeout, offline, permission, disabled, destructive, and edge-content states handled where relevant?
3. **Structure and content:** Do hierarchy, labels, reading order, navigation, density, and primary action match the user goal?
4. **System coherence:** Do tokens, components, icons, radii, borders, elevation, spacing, type, and motion follow named rules with justified exceptions?
5. **Responsive and input behavior:** Does the design adapt rather than shrink across target widths, zoom, touch, pointer, and keyboard?
6. **Accessibility and inclusion:** Route a full conformance review to [Web Accessibility Review](../web-accessibility-review/SKILL.md); still block obvious keyboard, focus, contrast, reflow, target, semantics, flashing, or reduced-motion failures.
7. **Performance and resilience:** Route measurement to [Web Performance Plan](../web-performance-plan/SKILL.md); still flag design choices that create obvious loading, layout-shift, battery, GPU, bandwidth, or low-end-device risk.
8. **Distinctiveness and restraint:** Verify that signature choices support the product, borrowed ideas have provenance, and decoration does not overwhelm task or content.

## Findings

For every finding, include location and state, expected behavior or design rule, observed result, user or product impact, reproducible evidence, severity, smallest durable correction, and verification method.

Use these severities:

- **Blocker:** prevents or dangerously misleads a critical journey; severe accessibility, privacy, destructive-action, or source-confusion risk
- **Major:** substantial task friction, missing recovery or responsive state, systemic inconsistency, or material performance/accessibility harm
- **Moderate:** localized clarity, hierarchy, consistency, or craft problem with a credible user impact
- **Minor:** polish defect with limited impact and an objective rule or visible inconsistency
- **Preference:** optional alternative not supported by the brief or user evidence; keep separate from defects

## Completion Gate

Report reviewed environments, direct evidence, checks actually run, untested areas, accepted exceptions, and residual risk. The interface is ready only when blockers and majors are resolved or explicitly accepted by the accountable owner, critical journeys and states are verified, specialist gates have the required evidence, and remaining polish work is honestly classified rather than hidden behind a general “looks good” judgment.
