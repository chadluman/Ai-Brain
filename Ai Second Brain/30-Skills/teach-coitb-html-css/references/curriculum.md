# COITB HTML and CSS Curriculum

Use this as an adaptable exam-preparation sequence, not a fixed calendar. Preserve the official domain weights while ordering instruction by dependency. Build one original site throughout so knowledge checks remain connected to working behavior.

## Learner Assumptions

- No JavaScript, framework, package manager, or preprocessor experience is required.
- The learner can create and edit files and open a page in a browser; teach these first if the diagnostic shows a gap.
- Practice content and assets are original, licensed, or explicitly permitted.
- Exam preparation and certification are separate outcomes. Completing this curriculum does not guarantee a passing score.

## Final Observable Outcome

The learner can answer original questions across all six published domains and build a responsive multi-section website containing meaningful HTML structure, links and images, maintainable CSS, box-model reasoning, Flexbox and Grid layouts, media-query adaptations, a native HTML form, custom properties, and a restrained transition or animation that respects user preferences.

## Project Spine

Use a three-page site such as a community event, small nonprofit, personal portfolio, or local service:

- `index.html`: multi-section landing page;
- `details.html`: detailed content, media, and a layout variation;
- `contact.html`: native form and validation attributes;
- `styles.css`: shared base, layout, component, state, and responsive rules;
- `assets/`: permitted images and other static files.

No deployment, live form endpoint, dependency installation, or account is required.

## Module 0 — Diagnostic and Exam Orientation

- **Outcome:** Produce domain-level evidence and a prioritized study plan.
- **Demo:** Work through one original item by identifying the exact objective, eliminating distractors, and confirming the behavior in a minimal page.
- **Guided lab:** Inspect a deliberately uneven sample page for an HTML, selector, box-model, layout, responsive, form, and animation issue.
- **Independent task:** Complete a short original mixed diagnostic without notes.
- **Verification:** Record correct and incorrect results by domain and error type; do not reduce the result to a single score.

## Module 1 — HTML Structure, 20%

- **Concepts:** document skeleton, metadata, language, headings, sections, landmarks, paragraphs, lists, links, paths, images, alternatives, tables, media, and source order.
- **Demo:** Convert unstructured event copy into a meaningful document and inspect its outline and accessibility tree.
- **Guided lab:** Build the landing-page structure, navigation, content sections, image, and footer before adding CSS.
- **Independent task:** Build the detail page from a content brief with different hierarchy and media needs.
- **Original exam practice:** identify missing or misplaced structure; select the suitable element, link, path, or image markup; predict the effect of incorrect nesting.
- **Verification:** the page remains understandable without CSS; links resolve; images have appropriate alternatives; headings and regions reflect content relationships.

## Module 2 — CSS Basics, 25%

- **Concepts:** stylesheet connection, rule syntax, element, class and ID selectors, combinators and states needed by the project, cascade, inheritance, specificity, source order, color, typography, alignment, spacing, and computed styles.
- **Demo:** Predict and inspect the winner among conflicting declarations.
- **Guided lab:** Create a low-specificity base layer and style the landing page's type, colors, links, and reusable sections.
- **Independent task:** change the visual theme with a small set of shared decisions instead of one-off overrides.
- **Original exam practice:** match selectors, compute specificity, identify invalid declarations, and select the smallest maintainable fix.
- **Verification:** the learner predicts computed styles before using development tools and can remove an unnecessary ID or `!important` escalation.

## Module 3 — Layout Techniques, 20%

- **Concepts:** normal flow, display roles, box model, `box-sizing`, intrinsic sizing, min/max constraints, overflow, positioning basics, Flexbox axes and alignment, Grid tracks and placement, gaps, and source-order implications.
- **Demo:** Diagnose an unexpected box size and compare a Flexbox relationship with a Grid relationship.
- **Guided lab:** use Flexbox for navigation or action alignment and Grid for cards or the main page composition.
- **Independent task:** adapt the layout to additional cards and long headings without fixed-height assumptions.
- **Original exam practice:** calculate box dimensions, identify axes, predict wrapping and alignment, and choose between flow, Flexbox, Grid, and positioning.
- **Verification:** the site tolerates content variation; required content is not clipped; visual order does not contradict reading or focus order.

## Module 4 — Responsive Design, 20%

- **Concepts:** viewport behavior, fluid media, relative units, flexible sizing, content-driven breakpoints, media-query syntax, mobile-first and other valid strategies, adaptable navigation, logical properties, and progressive enhancement.
- **Demo:** shrink a page until content—not a named device—reveals the first necessary breakpoint.
- **Guided lab:** adapt navigation, content columns, cards, media, and type across the agreed width range.
- **Independent task:** test longer text, zoom, and one alternate reading direction or preference and repair physical assumptions.
- **Original exam practice:** evaluate media-query conditions, predict the active rules, and choose changes that preserve content across screens.
- **Verification:** agreed narrow, medium, and wide checks have no unintended loss or horizontal scrolling; enhancements have acceptable fallbacks.

## Module 5 — HTML Forms, 10%

- **Concepts:** `form`, labels, inputs, buttons, names, types, grouping, instructions, required and optional fields, built-in constraint-validation attributes, and the boundary between browser and server validation.
- **Demo:** compare a field that uses transient hint text as its only identification with a persistently labeled control and inspect submitted name/value pairs conceptually.
- **Guided lab:** build the contact page without claiming that data is actually sent.
- **Independent task:** add grouped choices and validation requirements while preserving logical reading and focus order.
- **Original exam practice:** select appropriate input types and attributes, find missing labels or names, and distinguish client hints from authoritative validation.
- **Verification:** controls have usable labels, related inputs are grouped, keyboard interaction works, and the page does not imply a successful live submission.

## Module 6 — Advanced CSS, 5%

- **Concepts:** custom properties, transitions, keyframe animations, transform and opacity choices, reduced motion, and preprocessor purpose, compilation, variables, nesting, costs, and native-CSS alternatives.
- **Demo:** add a restrained state transition, then provide a reduced-motion treatment and inspect the computed custom-property value.
- **Guided lab:** create shared color and spacing properties and one purposeful transition or animation.
- **Independent task:** refactor a repeated value and explain whether Sass would solve a real problem in this project.
- **Original exam practice:** identify variable scope and fallback, select valid transition or animation syntax, and distinguish preprocessor source from browser-executable CSS.
- **Verification:** motion is optional and does not hide state; custom properties have clear roles; the learner can explain that Sass requires compilation and is not natively executed by the browser.

## Module 7 — Integration, Review, and Timed Practice

- **Outcome:** Combine practical and exam evidence into a defensible readiness decision.
- **Demo:** review one missed item and one project defect from symptom to governing rule and durable correction.
- **Guided lab:** inspect the capstone for structure, cascade, layout, responsive behavior, forms, motion, accessibility, and compatibility.
- **Independent task:** complete an original mixed practice set under the current published time budget, then correct every missed item in writing or code.
- **Verification:** report weighted score, per-domain score, error types, project acceptance results, untested areas, and readiness uncertainty.

## Capstone Acceptance Criteria

- Each page has a unique title, declared language, coherent landmarks, and logical headings.
- Navigation, links, images, lists, and controls use elements that match their meaning.
- CSS uses understandable selectors and shared custom properties without avoidable specificity escalation.
- The learner can explain computed styles, box dimensions, Flexbox axes, Grid tracks, and the effect of each media query.
- The agreed narrow, medium, and wide viewport checks pass with representative long content.
- Keyboard order and focus visibility are coherent; text alternatives, labels, grouping, contrast, zoom or reflow, and reduced motion where applicable have been reviewed.
- The form demonstrates native attributes without pretending to provide a backend or complete security validation.
- Motion has a purpose, and the site remains understandable without it.
- Content and assets are original, licensed, or permitted.
- A short implementation note records browser checks, limitations, exam-domain coverage, and the next improvement.

Automated validators and audits may supplement this evidence but cannot prove accessibility, compatibility, or exam readiness alone.

## Original Practice Assessment Rules

- Map every item to exactly one primary published objective and optionally one secondary skill.
- Use fresh examples; do not imitate recalled live questions or present unofficial wording as COITB content.
- Include code-reading, selector matching, computed-style, box-model, layout, media-query, form, custom-property, and motion scenarios.
- Keep distractors plausible and diagnose why each is wrong in the answer rationale.
- Hide answers only until the learner attempts the set; never hide the scoring rubric.
- For a full mock, mirror the currently published 90-item and 90-minute shape only after re-verifying it. Label the mock as original and unofficial.

## Assessment Rubric

| Dimension | Functional | Reliable | Senior-practitioner teaching target |
|---|---|---|---|
| Exam knowledge | Reaches the official passing threshold on one original set | Sustains the local readiness heuristic across sets and domains | Explains rules, catches ambiguity, and transfers knowledge to unseen scenarios |
| HTML | Uses common structures and elements correctly | Preserves meaning, relationships, paths, media alternatives, and source order | Can critique tradeoffs and anticipate user and maintenance consequences |
| CSS | Produces the intended appearance | Predicts cascade and computed styles and controls specificity | Builds adaptable boundaries and explains when another mechanism is preferable |
| Layout and responsive design | Works in demonstrated conditions | Handles content and agreed viewport variation | Selects mechanisms from relationships and support evidence rather than habit |
| Forms and accessibility | Creates labeled native controls | Verifies keyboard, state, instruction, validation, and preference behavior | Connects decisions to user impact, standards, server boundaries, and residual risk |
| Diagnosis | Fixes a known example with guidance | Uses tools and governing rules to isolate new defects | Communicates evidence, uncertainty, alternatives, and proportionate next work |

## Minimal Setup

No installation is required. Open the HTML files in the agreed browsers and use built-in development tools for DOM, computed-style, layout, responsive, and accessibility inspection. Use a reviewed local server only when the environment already has one or browser file restrictions materially block a lesson.
