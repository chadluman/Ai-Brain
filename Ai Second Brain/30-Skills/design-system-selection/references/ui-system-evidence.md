# UI System Evidence

Verified 2026-10-21. Recheck exact stable versions, licenses, browser floors, and security notices before recommending or installing a tool.

## Portable Foundations

- The [Design Tokens Format Module 2025.10](https://www.w3.org/community/reports/design-tokens/CG-FINAL-format-20251028/) defines a vendor-neutral exchange format for design tokens. It is a stable W3C Community Group final report, not a W3C Recommendation or Standards Track document.
- The [Design Tokens Community Group repository](https://github.com/design-tokens/community-group) is the canonical specification repository and labels `2025.10` stable. Tool support for that format must still be tested; downloading or executing repository tooling requires R2 review.
- CSS custom properties and semantic HTML are web-platform primitives. Use the project's compatibility and accessibility skills to establish their actual support and behavior.

## Example CSS Systems, Not Defaults

- [Tailwind CSS compatibility](https://tailwindcss.com/docs/compatibility) documents its current browser floor and warns that some utilities use limited-availability platform features. Its utility workflow and build integration should be evaluated as a package, not reduced to class syntax.
- [Bootstrap accessibility guidance](https://getbootstrap.com/docs/6.0/getting-started/accessibility/) explains intended semantics and reduced-motion behavior while noting application authors remain responsible for accessible results. Verify the current stable release before use; documentation for a future or prerelease line is not production approval.

For any CSS or component candidate, inspect the official documentation and repository, exact release and license, dependencies and install scripts, supported browser matrix, security process, rendered markup, keyboard and assistive-technology behavior, CSS and JavaScript output, theming path, upgrade tools, and removal cost.

## Decision Boundary

Choose a token exchange standard only when design decisions cross tool, product, or platform boundaries. Choose a utility system only when its authoring and build model improves this team's work. Choose a component library only after representative composed components pass the product's accessibility, content, styling, performance, and maintenance tests.
