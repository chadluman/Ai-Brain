---
name: interface-pattern-reconstruction
description: Analyze an authorized website, application, or service and turn its observable interaction patterns into an original behavior specification and clean implementation plan. Use for competitive teardowns, migration parity, or learning from working flows; do not use to clone branding, protected assets or source, bypass access controls, or imitate a product so closely that users could confuse the source.
---

# Interface Pattern Reconstruction

## Outcome

Recover the useful functional principles of an interface—journeys, state transitions, information architecture, feedback, layout behavior, and failure recovery—then express them as an original design suited to the current product.

Read [Pattern Study Evidence](references/pattern-study-evidence.md) before observing a third-party product or defining a clean-room implementation boundary.

## Establish Authority and Scope

- Identify the owner, target surface, access method, account or data involved, purpose, jurisdiction, and intended output.
- Limit observation to public material or access the user is authorized to use. Respect terms, robots or rate limits where applicable, privacy, confidentiality, and data minimization.
- Do not bypass authentication, paywalls, technical protection, rate limits, feature gates, or anti-automation controls. Do not probe private APIs, vulnerabilities, or other users' data.
- Treat screenshots, recordings, markup, styles, scripts, API responses, copy, icons, images, fonts, and motion assets as potentially protected material. Observation is not permission to reuse.

Stop for qualified legal review when the request involves a close competitor, near-pixel parity, commercial redistribution, source extraction, proprietary formats, circumventing controls, confidential access, patents, or unresolved license and terms questions.

## Workflow

1. Define the user outcome and the narrow pattern under study, such as search refinement, progressive onboarding, keyboard command discovery, optimistic save, or a responsive data table.
2. Record provenance, date, version or visible release state, access conditions, and which evidence is direct observation versus inference.
3. Walk the full task using representative inputs. Record entry, action, system feedback, intermediate states, completion, cancel, back, retry, timeout, offline, permission, empty, error, and destructive paths.
4. Decompose the interface into invariants: information required, decision sequence, state machine, input and output contract, layout rules, responsiveness, keyboard and touch behavior, announcements, timing, and recovery.
5. Separate the useful principle from its expression. Mark brand identifiers, copy, media, illustrations, exact composition, ornamental treatment, and implementation details as excluded unless independently licensed.
6. Compare at least one alternative source or platform convention where practical. A repeated pattern can be evidence of user expectation; a single product is only one design decision.
7. Write a neutral behavior specification without screenshots or source fragments. Hand that specification to the implementation step and create a distinct visual direction through [Product Design Direction](../product-design-direction/SKILL.md).
8. Implement with native platform behavior and already approved project dependencies where possible. Any copied component, package, template, font, icon set, or asset requires exact-version review and attribution.
9. Validate functional parity against the behavior specification and intentional difference against the source. Test the critical journey, edge states, accessibility, responsive behavior, performance, and product-specific content.

## Required Output

- scope, authorization basis, provenance, access constraints, and legal or license flags
- observation log that distinguishes fact from inference
- task flow and state-transition model
- behavior, data, layout, interaction, accessibility, and recovery specification
- principle-versus-expression separation and originality plan
- candidate implementation boundaries, dependencies, and review needs
- comparison evidence, test matrix, known gaps, and stop conditions

## Completion Gate

Do not call reconstruction complete when only the happy path or appearance was captured. The output must explain why the pattern works, include important failure and recovery states, be implementable without copying protected expression, and pass both functional validation and an originality review.
