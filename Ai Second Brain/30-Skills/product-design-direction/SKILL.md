---
name: product-design-direction
description: Define an original, usable visual and interaction direction for a website or application before detailed UI implementation. Use when establishing art direction, color and type systems, layout rhythm, motion character, signature motifs, or a design brief; do not use to select a CSS or component library.
---

# Product Design Direction

## Outcome

Turn product intent, user journeys, content, and constraints into a coherent design thesis and implementation-ready visual language. The result should feel specific to the product without sacrificing clarity, accessibility, performance, or platform conventions.

Read [Design Fundamentals](references/design-fundamentals.md) before defining color, typography, layout, theme, or motion. Consult the [Design Reference Catalog](../../20-Catalog/Design/Design%20Reference%20Catalog.md) only for the part of the design under study.

## Inputs

- product promise, target users, critical journeys, success criteria, stage, and supported platforms
- brand character, existing assets, content types, emotional tone, and explicit anti-references
- accessibility target, locales and writing systems, device and browser policy, performance budget, and maintenance capacity
- design constraints that are required, preferred, prohibited, or still assumptions

Ask only questions that could materially change the direction. If work can safely continue, label assumptions and make them easy to replace.

## Workflow

1. Establish the experience contract: what users must understand, feel, and accomplish, in that order. Separate functional requirements from taste words.
2. Write a one-sentence design thesis plus three to five principles that can decide between alternatives. Add anti-principles that prevent predictable drift.
3. Map content priority, reading order, navigation, primary actions, and critical states in grayscale before using color or effects to manufacture hierarchy.
4. Study precedents by function or design problem. When a particular product is being analyzed, use [Interface Pattern Reconstruction](../interface-pattern-reconstruction/SKILL.md) and extract principles rather than pixels.
5. Define the visual architecture from primitives to semantic tokens, component decisions, patterns, and page or screen compositions. Use [Design System Selection](../design-system-selection/SKILL.md) only when choosing the implementation and governance layers.
6. Specify color roles, typography, spacing and grid rhythm, shape, imagery, iconography, elevation, and motion. Design light, dark, high-contrast, or brand themes as deliberate semantic mappings, not automatic inversions.
7. Create one or two signature expressions tied to product meaning: a spatial motif, material treatment, illustration language, transition, data treatment, or content behavior. Repeat them with restraint; novelty must not obscure tasks.
8. Apply the direction to representative specimens: the critical journey, a dense screen, a sparse screen, an error or recovery state, and a small viewport. Include loading, empty, success, disabled, focus, hover where supported, and reduced-motion behavior.
9. Compare at least two plausible directions when the choice is consequential. Select against the thesis, user evidence, accessibility, performance, implementation cost, content fit, and longevity rather than trend or personal preference.

## Anti-Vibe-Coding Guardrails

- Do not start from a fashionable component collection and invent the product around it.
- Do not mix unrelated visual styles, arbitrary radii, shadows, gradients, type scales, or motion curves.
- Do not use effects to compensate for weak information hierarchy, content, or task flow.
- Do not treat a screenshot, generated mockup, or default theme as a specification.
- Do not call a direction original because its colors changed. Distinction must come from product meaning, content, composition, behavior, or an owned visual motif.
- Do not import code, fonts, icons, images, templates, or generators until the exact asset passes the repository review gate.

## Required Output

- experience contract, assumptions, design thesis, principles, and anti-principles
- reference and anti-reference matrix with extracted principles and provenance
- content hierarchy and critical-flow sketch
- visual architecture and semantic token model
- color, type, layout, shape, icon, imagery, and motion specifications
- signature expressions with rationale and restraint rules
- representative specimens and complete state matrix
- accessibility, responsive, performance, localization, and asset-license constraints
- unresolved decisions, validation plan, and owners

## Completion Gate

Do not call the direction ready until a reviewer can trace each major design choice to the product thesis or a user need, the critical journey works without decorative effects, all essential states are specified, foreground/background pairs and interactions have test plans, and the result is distinguishable without copying another product's protected expression or identity.
