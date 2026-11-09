---
name: web-accessibility-review
description: Plan or review the accessibility of web journeys, pages, and interactive components using current W3C requirements and platform semantics. Use for accessibility acceptance criteria, implementation review, remediation, or release evidence; do not use to claim legal compliance from automated scans alone.
---

# Web Accessibility Review

## Outcome

Produce an evidence-backed accessibility plan or review that connects user impact and observable behavior to versioned W3C requirements, then defines fixes and verification.

Read [standards and evidence](references/standards-and-evidence.md) when establishing the conformance target, reviewing custom widgets, or citing requirements.

## Establish Scope

- Identify target users, jurisdictions, product surfaces, critical journeys, supported browsers/devices, input methods, and assistive-technology expectations.
- Record the requested conformance target. If none is supplied, use WCAG 2.2 Level A and AA as a planning baseline and label that choice as an assumption, not legal advice.
- Record whether the European Accessibility Act applies to the product's markets. It has applied since June 2025. Treat that as a scoping input for which journeys and obligations to check, not as legal advice.
- Inventory pages, components, content types, states, errors, dialogs, asynchronous updates, authentication, checkout, and other high-impact flows.

## Review Priorities

1. Use semantic HTML and built-in control behavior before adding ARIA or custom interaction.
2. Verify keyboard access, logical order, visible and unobscured focus, escape/close behavior, and absence of keyboard traps.
3. Verify names, roles, values, states, relationships, headings, landmarks, page titles, language, and status/error announcements.
4. Verify text alternatives, captions/transcripts where required, form instructions, labels, validation, recovery, and authentication usability.
5. Verify contrast, non-color cues, zoom, reflow, text spacing, orientation, target size, motion, flashing, time limits, and reduced-motion behavior as applicable.
6. Exercise every critical journey and important component state, not only the initial page render.

Automated checks are useful for repeatable detectable rules but are not sufficient. Combine them with keyboard review, visual inspection at relevant zoom/reflow settings, assistive-technology testing appropriate to the support matrix, and task-based human evaluation when risk warrants it.

## Automated Tools and Their Limits

Treat automated-check coverage as partial, not as a conformance verdict. Research reported in 2026 puts automated detection at roughly 30–57% of accessibility issues, so a clean automated run is not evidence that a journey is accessible — manual keyboard, zoom and reflow, assistive-technology, and task-based testing remain required. [Unverified: the 30–57% figure is quoted from a secondary source, not read from the primary reports.]

The February 2026 WebAIM Million findings were reported in the same research as showing a regression in detected accessibility errors. [Unverified: secondary source only.] Re-check the current WebAIM findings before citing them, and do not carry a dated error count into a review as if it were current.

## Findings

For each issue, record:

- Affected journey, component, state, browser/device, and evidence
- User impact and affected interaction mode
- Exact WCAG 2.2 success criterion when applicable
- Severity based on impact, reach, frequency, and whether the journey is blocked
- Root cause and smallest durable fix
- Regression test and manual verification steps
- Owner and release disposition

Do not recommend ARIA solely to satisfy a checker. For custom widgets, compare behavior with the APG while remembering that APG is informative and its examples require project-specific testing.

## Completion

Report tested scope, tools and versions, manual methods, passed and failed criteria, untested areas, limitations, and residual risk. Never state that a product is accessible or legally compliant when only a partial review was performed.

