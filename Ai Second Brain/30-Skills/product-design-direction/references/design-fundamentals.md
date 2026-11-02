# Design Fundamentals

Verified 2026-10-21. These are decision defaults, not a universal style. Product evidence, user research, platform conventions, and accessibility requirements can justify a different choice.

## The Design Stack

| Layer | Question | Evidence |
|---|---|---|
| Purpose | What user outcome and product promise does this serve? | brief, research, success measure |
| Structure | What is present, in what order, and through which journey? | content model, task flow, information architecture |
| Composition | How do hierarchy, grid, spacing, scale, and density guide attention? | wireframes, responsive specimens |
| Visual language | Which color, type, shape, image, icon, material, and motion rules express the product? | semantic tokens, art direction, asset provenance |
| Components | How do controls and content behave across states? | component contracts and state matrix |
| Patterns | How do components cooperate in recurring tasks? | flow prototypes and usability evidence |
| Product surfaces | How do pages and screens adapt to content, viewport, input, theme, and locale? | representative data and environment tests |

Changes should usually flow downward. A page-specific exception must have a reason; it must not silently become another system.

## Durable Principles

1. **Purpose before style.** A clear product promise and critical journey outrank visual novelty.
2. **Hierarchy before decoration.** Reading order, grouping, emphasis, and primary action should remain understandable in grayscale and without animation.
3. **Consistency with meaningful variation.** Repeat rules so users can predict behavior; vary composition where content or task genuinely differs.
4. **Recognition and feedback.** Make available actions, current state, system progress, results, and recovery visible. Do not make users remember hidden modes.
5. **Content is interface.** Real labels, data ranges, empty states, errors, and translations shape the design; placeholder copy is not validation.
6. **Accessibility is a design input.** Keyboard, focus, zoom, reflow, contrast, non-color cues, reduced motion, touch, and assistive-technology semantics affect the direction from the start.
7. **Performance is part of feel.** A heavy shader, font, video, or animation that delays or destabilizes the journey is a design defect.
8. **Originality comes from synthesis.** Study multiple sources, name the principle learned, and re-express it through this product's content, brand, constraints, and implementation.

## Color Architecture

Define roles before values:

- neutral canvas and nested surfaces
- primary and secondary text, icons, borders, and disabled content
- one primary action family plus restrained secondary and tertiary emphasis
- success, warning, error, and informational states
- focus, selection, hover, pressed, visited, and drag/drop states
- data-series colors, thresholds, and non-color encodings when data visualization exists
- scrim, shadow, highlight, and media-overlay roles when needed

Map roles through semantic tokens such as `surface`, `on-surface`, `action-primary`, `on-action-primary`, `border-subtle`, `status-error`, and `focus-ring`. Components consume roles rather than raw palette values. A theme remaps roles while preserving meaning and state distinguishability.

Build the scheme in this order:

1. Prove hierarchy in monochrome.
2. Establish accessible foreground/background and control-boundary pairs.
3. Add functional state colors with text, icon, shape, pattern, or placement cues.
4. Add brand accents and emotional tone.
5. Test every actual pair in every supported theme and state; palette membership does not prove contrast.
6. Test common color-vision differences, forced colors where relevant, representative displays, and content over images or gradients.

WCAG 2.2 Level AA requires at least 4.5:1 for normal text and 3:1 for large text; relevant non-text controls and state indicators require 3:1. Color cannot be the only visual means of conveying information. Treat these as minimum conformance checks, not a complete color-quality model.

CSS Color 4 adds spaces such as Lab, LCH, Oklab, and Oklch. They can make palette authoring and interpolation more perceptually useful, but CSS Color 4 remains a Candidate Recommendation Draft and target-browser support must be verified. Provide an sRGB fallback when the browser policy requires it.

## Typography

- Choose type for the product's content, scripts, numeric needs, tone, and loading budget—not from a pairing trend.
- Use named roles such as display, heading, body, label, code, caption, and numeric data. Limit distinct roles and weights to those that create real hierarchy.
- Start body text near an effective 16 CSS pixels, then test the chosen face's optical size. Use unitless line height and allow user scaling.
- For sustained reading, begin around 45–90 characters per line; USWDS identifies about 66 as a useful target, then adjust for language, typeface, size, and context.
- Keep headings closer to the content they introduce than to the preceding section. Use spacing and scale before relying on weight or color.
- Test real longest labels, large numbers, localization, bold/italic availability, fallback fonts, font swap, and zoom. Use tabular figures where changing numbers would otherwise jitter.

## Layout, Density, and Responsive Behavior

- Derive breakpoints from content failure, not a list of popular devices.
- Use a small spacing scale, often based on 4 or 8, while allowing optical corrections that are documented rather than accidental.
- Define container, gutter, column, alignment, and vertical-rhythm rules. Avoid independent page-level magic numbers.
- Group related items with proximity and shared alignment; separate unrelated regions with stronger space, surface, or headings.
- Let priority, density, and interaction change deliberately across widths. Responsive design is not proportional shrinking.
- Test small phone, large phone, tablet or narrow desktop, wide desktop, landscape, 200% and 400% zoom/reflow as applicable, long content, no data, and maximum realistic data.

## Interaction and Motion

- Every interactive element needs perceivable affordance and visible focus, hover where supported, pressed, disabled, loading, success, and error behavior as applicable.
- Keep the same action in the same conceptual place across states. Avoid layout shifts that move a target while it is being used.
- Motion should explain causality, hierarchy, continuity, progress, or direct manipulation. Decorative motion earns its budget only after functional motion is clear.
- Define duration, easing or spring, distance, choreography, interruption, and reduced-motion alternatives as tokens or pattern rules.
- Prefer CSS for simple state transitions. Add a runtime animation or shader dependency only when the interaction cannot be expressed reliably and accessibly with the platform.
- Never depend on hover, motion, gesture, or color alone. Preserve visible controls and equivalent outcomes.

## A Coherent Signature

A product usually needs fewer distinctive devices than a mood board suggests. Select one or two devices that reinforce meaning—for example, a cartographic grid for a logistics product, a layered-paper material for a research notebook, or a measured pulse for live monitoring. Define where each device appears, what it communicates, its performance and reduced-motion fallback, and where it must not appear.

## Primary Evidence

- [WCAG 2.2](https://www.w3.org/TR/WCAG22/) — normative accessibility requirements; W3C Recommendation.
- [WCAG 2.2 Understanding documents](https://www.w3.org/WAI/WCAG22/understanding/) — informative explanations for contrast, color, reflow, target size, focus, motion, and related criteria.
- [CSS Color Module Level 4](https://www.w3.org/TR/css-color-4/) — current CSS color-space specification status and behavior.
- [USWDS design principles](https://designsystem.digital.gov/design-principles/) — public-service design principles centered on real user needs.
- [USWDS using color](https://designsystem.digital.gov/design-tokens/color/overview/) and [typography](https://designsystem.digital.gov/components/typography/) — practical token, color, hierarchy, measure, and rhythm guidance; adapt outside government contexts.
- [Material 3 color roles](https://m3.material.io/styles/color/roles) and [typography](https://m3.material.io/styles/typography/overview) — a vendor design system showing role-based color and type architecture, not a universal style requirement.
- [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) — platform-owner guidance for Apple surfaces; apply only where the target platform warrants it.
- [Nielsen Norman Group usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/) — durable evaluation heuristics, not a substitute for task-based user research.
- [FTC, Bringing Dark Patterns to Light](https://www.ftc.gov/reports/bringing-dark-patterns-light) — consumer-protection evidence for avoiding manipulative interface choices.
