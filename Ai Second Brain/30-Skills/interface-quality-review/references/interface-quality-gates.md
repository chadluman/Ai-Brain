# Interface Quality Gates

Use this matrix for full-flow or release-candidate review. Scale depth to product risk; do not mark an unrun check as passed.

| Gate | Questions | Minimum evidence |
|---|---|---|
| Intent | Can major choices be traced to the brief, design thesis, content, or user need? | decision trace and named exceptions |
| Critical journey | Can representative users start, complete, cancel, retry, and recover? | task run with expected outcomes |
| State coverage | Are initial, loading, empty, partial, success, error, timeout, offline, permissions, disabled, and destructive states defined where relevant? | state inventory plus observed specimens |
| Information hierarchy | Is the page purpose, current state, primary action, and next step evident without color or motion? | grayscale or reduced-styling inspection |
| Content | Are labels specific, data realistic, errors actionable, and localization/content extremes supported? | representative and adversarial content set |
| System coherence | Do color, type, spacing, grid, radius, border, elevation, icon, and motion decisions come from maintained rules? | token/component trace and exception list |
| Responsive composition | Does priority and composition adapt at content-driven breakpoints without hidden or clipped work? | screenshots or live checks at target widths and zoom |
| Interaction | Are affordance, focus, hover where applicable, pressed, selected, disabled, progress, completion, undo, and error responses clear? | keyboard, pointer, and touch runs as supported |
| Accessibility | Do semantics, names, roles, values, sequence, focus, contrast, non-color cues, targets, zoom/reflow, and reduced motion meet the target? | specialist review and manual evidence |
| Motion | Does motion explain cause, hierarchy, continuity, progress, or direct manipulation; can it be interrupted or reduced? | normal and reduced-motion recordings or observations |
| Performance | Do media, fonts, effects, shaders, and transitions stay within budgets and avoid layout instability? | target-device/network measurements |
| Originality | Are precedents documented, protected expression excluded, and signature choices grounded in this product? | provenance and originality matrix |
| Trust | Are permissions, destructive choices, costs, subscriptions, privacy choices, and consequences presented without manipulation? | flow inspection against product policy and FTC dark-pattern risks |
| Craft | Are alignment, optical balance, wrapping, truncation, raster quality, icon consistency, hit areas, and transitions clean under real content? | high-resolution visual inspection across themes |

## Anti-Generic Review

An interface is likely under-specified when several of these are true:

- the product name could be swapped without changing the design logic
- every section uses the same card treatment regardless of information type
- hierarchy depends on a gradient, glow, or oversized heading rather than content priority
- default library components remain visually and behaviorally unrelated to the brand or task
- spacing, radius, shadow, icon style, and motion vary without named rules
- the only distinctive feature is a decorative hero effect
- key screens lack error, empty, loading, or edge-content design
- desktop is composed but mobile is merely stacked
- copy is generic, synthetic, or still placeholder text

Do not “fix” these by adding more effects. Return to the experience contract, content model, and product-specific signature.

## Visual Comparison Method

1. Capture the same state, content, theme, and viewport before and after a change.
2. Check macro hierarchy and composition before pixels.
3. Check component states, alignment, rhythm, wrapping, and optical balance.
4. Inspect focus, hover, press, animation, loading, and route changes over time.
5. Repeat with longest content, empty data, errors, 200% zoom, reduced motion, and the smallest supported viewport.
6. Record observations and measurements; do not use a screenshot-diff threshold as the sole quality judgment.

## Release Record

Record build identifier, date, reviewer, environments, critical journeys, themes, viewport and input matrix, data fixtures, automated tools, manual methods, findings by severity, fixes verified, accepted risks, untested areas, and follow-up owner/date.
