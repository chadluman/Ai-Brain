---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R0
tags: [catalog, design, frontend, inspiration]
sources:
  - https://developer.mozilla.org/en-US/docs/Learn_web_development
  - https://www.w3.org/TR/WCAG22/
  - https://designspells.com/
  - https://reactbits.dev/
  - https://toolfolio.com/
  - https://flexboxlabs.netlify.app/
  - https://iconsax.io/
  - https://www.shadergradient.co/
  - https://www.vengenceui.com/
---

# Design Reference Catalog

This is a routing catalog, not a blanket recommendation or installation allow-list. Use it to find evidence and precedents for a specific design problem. Every package, CLI, copied component, font, icon, image, shader, template, registry item, account, or paid service still needs its exact version, license, dependencies, telemetry, permissions, cost, and removal path reviewed before use.

## Start With the Platform

| Need | Preferred reference | Boundary |
|---|---|---|
| Learn or verify HTML, CSS, JavaScript, SVG, Canvas, and browser APIs | [MDN Learn Web Development](https://developer.mozilla.org/en-US/docs/Learn_web_development), [MDN Web technology](https://developer.mozilla.org/en-US/docs/Web) | Practical reference; use WHATWG, W3C, TC39, or another defining specification for normative behavior |
| HTML semantics and browser behavior | [WHATWG HTML Living Standard](https://html.spec.whatwg.org/) | Normative but not a tutorial; load only the relevant section |
| CSS features and layout | [MDN CSS](https://developer.mozilla.org/en-US/docs/Web/CSS), [CSS specifications](https://www.w3.org/Style/CSS/specs.en.html) | Confirm target-browser support and test actual content |
| JavaScript language behavior | [ECMAScript specification](https://tc39.es/ecma262/), [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) | Browser APIs are specified separately from the language |
| Accessibility | [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [WAI tutorials](https://www.w3.org/WAI/tutorials/), [ARIA APG](https://www.w3.org/WAI/ARIA/apg/) | APG is informative; prefer native HTML and test composed behavior |
| Compatibility | [Web Platform Baseline](https://web.dev/baseline), [MDN browser compatibility](https://developer.mozilla.org/en-US/docs/Glossary/Baseline/Compatibility) | Baseline is not the project's browser policy or test evidence |

## Study Real Products Without Cloning Them

| Resource | Best use | Evidence boundary |
|---|---|---|
| [Design Spells](https://designspells.com/) | Small interaction, motion, delight, transition, and easter-egg precedents | Inspiration only. It showcases third-party products; no code or asset reuse is implied. Study purpose, trigger, feedback, and fallback. |
| [Page Flows](https://pageflows.com/) | End-to-end onboarding, search, checkout, upgrade, cancellation, settings, permission, and recovery flows | Recorded third-party flows may be paid and copyrighted. Do not create an account or spend without authorization; extract neutral behavior, not screens. |
| [Mobbin](https://mobbin.com/) | Screen and flow comparisons across web and mobile products | Commercial reference library; terms and access control. Compare multiple products and validate with users. |
| [Godly](https://godly.design/) | Broad visual direction, typography, composition, brand expression, and interactive-web references | Curation is inspiration, not usability or implementation evidence. Avoid whole-site imitation. |
| [Lapa Ninja](https://www.lapa.ninja/) | Landing-page structure, content rhythm, section sequencing, and visual comparison | Marketing-page curation. Conversion claims and licenses require independent evidence. |

Use [Interface Pattern Reconstruction](../../30-Skills/interface-pattern-reconstruction/Interface%20Pattern%20Reconstruction.md) for any focused teardown.

## Code and Effect References

| Resource | What it demonstrates | Current admission decision |
|---|---|---|
| [React Bits](https://reactbits.dev/) | Animated React text, backgrounds, components, and micro-interactions in JavaScript or TypeScript with CSS or Tailwind variants | R0 browsing approved with conditions. The free repository currently uses an MIT license plus Commons Clause restriction; exact code or CLI use remains R2 and requires commit-level review. Pro has separate commercial terms. |
| [Vengeance UI](https://www.vengenceui.com/) | Animated React/Next.js, Tailwind, and shadcn-compatible landing-page interactions | R0 browsing approved with conditions. Repository states MIT, but exact component, registry payload, dependencies, accessibility, reduced motion, browser behavior, and commit require review before import. |
| [ShaderGradient](https://www.shadergradient.co/) | Configurable WebGL gradient scenes and integration patterns for design tools and React | R0 browsing approved with conditions. The repository states MIT but the React path brings Three.js and related peer dependencies plus GPU, battery, fallback, SSR, and accessibility concerns. |
| [shadcn/ui](https://ui.shadcn.com/) | Open-code component composition and registry model | Official project is MIT, but community registries are independent and can distribute code, config, workflows, or agent instructions. Review every registry item as a package. |
| [Motion](https://motion.dev/) | CSS, JavaScript, React, Vue, gesture, layout, spring, scroll, and reduced-motion patterns | Documentation is useful R0 evidence. Installing the library or AI skill and copying paid examples are separate assets with separate review and license boundaries. Prefer CSS for simple transitions. |

These are ingredients, not art direction. Importing several “interesting” effects usually makes a product less coherent. Choose an effect only after its meaning, frequency, performance budget, and reduced-motion behavior are defined.

## Layout and Icon References

| Resource | Best use | Current admission decision |
|---|---|---|
| [Flexbox Labs](https://flexboxlabs.netlify.app/) | Interactive exploration of flex container and item behavior plus generated HTML/CSS | R0 interactive reference approved with conditions. Canonical repository `prazzon/Flexbox-Labs` states MIT; clone, install, or generated-code reuse still needs exact-commit and dependency review. |
| [Lucide](https://lucide.dev/) | A consistent, customizable SVG icon language with public design rules | Official site states ISC. Candidate for project review; maintain one stroke/filled language and verify brand-logo restrictions separately. |
| [Iconsax](https://iconsax.io/) | Broad static and animated icon exploration | Discovery only; asset reuse is quarantined until the exact file/source license is resolved. Current official pages describe proprietary V2 terms while some FAQ text references older or alternative licenses. Do not assume a package mirror carries the site's rights. |

## Discovery Directories

[Toolfolio](https://toolfolio.com/) can surface design tools, component libraries, generators, and galleries, including sponsored listings. Treat every entry as an unverified lead. Popularity, a “free” label, or directory inclusion does not establish provenance, license, security, accessibility, privacy, maintenance, or product fit.

## Reference-to-Implementation Method

1. Name the design problem before browsing.
2. Collect three to five references from different products or categories.
3. For each, record the user goal, useful principle, evidence, failure risk, and excluded expression.
4. Sketch at least two product-specific interpretations without importing code or assets.
5. Select using the design thesis, user needs, accessibility, performance, content, maintainability, and originality.
6. Review any external asset at an immutable version before import.
7. Verify the implementation with real content and complete states, then record what was learned and what intentionally differs.

See [Design Reference Resources Review](../Reviews/Design%20Reference%20Resources%20Review.md) for the research-only safety decision covering the named resources.
