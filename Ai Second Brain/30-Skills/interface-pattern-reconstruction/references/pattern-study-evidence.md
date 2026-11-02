# Pattern Study Evidence

Verified 2026-10-21. This note provides a conservative research boundary, not legal advice. Laws, contracts, platform rules, and organizational policy vary by jurisdiction and use.

## Functional Principle Versus Expression

United States copyright law distinguishes ideas, procedures, processes, systems, and methods of operation from the original expression used to describe or embody them. That distinction supports studying how a task works, but it does not create a general right to copy source code, text, graphics, audiovisual captures, creative selection or arrangement, or other protected expression.

Brand names, logos, symbols, and designs can identify the source of goods or services. Avoid names, marks, trade dress, copy, imagery, and overall presentation likely to create source confusion. Patent, contract, database, privacy, publicity, and unfair-competition questions may apply independently of copyright.

The DMCA's anti-circumvention rules are separate from copyright infringement. Section 1201 includes a narrow reverse-engineering exception related to interoperability for a lawfully obtained program, with conditions; it is not permission for general bypass. Never assume an exception applies without qualified review.

Primary sources:

- [U.S. Copyright Office Circular 33](https://www.copyright.gov/circs/circ33.pdf) — ideas, methods, systems, and unprotected subject matter.
- [17 U.S.C. § 102](https://www.copyright.gov/title17/92chap1.html#102) — subject matter and the idea/expression boundary.
- [17 U.S.C. § 1201](https://www.copyright.gov/title17/92chap12.html#1201) — anti-circumvention rules and limited exceptions.
- [USPTO trademark basics](https://www.uspto.gov/trademarks/basics/what-trademark) — source-identifying words, symbols, and designs.

## Observation Record

For each study, record:

| Field | Evidence |
|---|---|
| Product, owner, URL or app, and visible version |  |
| Observation date and environment |  |
| Public or authorized access basis |  |
| Account, payment, private-data, and terms boundaries |  |
| User goal and scenario |  |
| Direct observations |  |
| Inferences to validate |  |
| Captured material and approved retention |  |
| License, attribution, brand, patent, or legal flags |  |
| Allowed output and excluded material |  |

Do not retain another user's information, session tokens, private responses, or unnecessary screenshots. A capture used internally for study remains subject to its source and retention rules.

## Behavioral Decomposition

Describe the pattern without brand language:

1. Trigger and user intent
2. Preconditions and required information
3. Available actions and decision order
4. State before action
5. Immediate feedback
6. Asynchronous progress and cancellation
7. Success result and next action
8. Empty, partial, invalid, unavailable, unauthorized, timeout, offline, and conflict states
9. Undo, retry, back, escape, and destructive confirmation
10. Keyboard, pointer, touch, screen-reader, zoom, and reduced-motion behavior
11. Responsive rules and content extremes
12. Data or API behavior inferred from observation, clearly labeled as inference

Represent non-trivial interactions as a state table or state diagram. A screenshot cannot express time, focus, causality, recovery, or hidden state.

## Originality Matrix

| Preserve as a functional requirement | Reinterpret for this product | Exclude unless licensed |
|---|---|---|
| user goal and necessary data | information grouping and progressive disclosure | source code and private APIs |
| familiar platform convention | component composition and responsive layout | brand names, logos, icons, and proprietary fonts |
| feedback and recovery principle | copy, tone, visual hierarchy, and motion | exact copy, images, illustration, audio, and video |
| accessibility behavior | token values, shape, material, and signature motif | near-pixel arrangement or confusingly similar overall presentation |

Use multiple precedents where possible. For each adopted principle, write why it fits the current users and what changed. If the rationale is only “the source did it,” the analysis is incomplete.

## Validation

- Re-run the same task against the neutral specification, not side-by-side pixels.
- Verify all defined state transitions and recovery paths.
- Review at representative widths, input modes, themes, locales, content extremes, and network conditions.
- Compare the final brand, composition, copy, assets, and signature behavior with the source. A reasonable user should not mistake the new product for the observed one.
- Record deviations that intentionally improve accessibility, clarity, privacy, performance, or product fit.
