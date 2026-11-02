# Documentation Evidence

Verified: 2026-10-21

## Documentation and Operations Sources

- [Diataxis](https://diataxis.fr/) distinguishes tutorials, how-to guides, reference, and explanation by reader need. Use it as a lightweight organizing lens, not a requirement to create four documents for every topic.
- [Google developer documentation style guide](https://developers.google.com/style) is current public editorial guidance for clear, consistent technical documentation. Project-specific terminology and reader needs take precedence.
- [Google Markdown style guide](https://google.github.io/styleguide/docguide/style.html) emphasizes readable, portable, maintainable source and simple Markdown. This vault's Obsidian practices control where its conventions differ.
- [Google SRE: Production Readiness Reviews](https://sre.google/sre-book/evolving-sre-engagement-model/) frames handoff as verification that service owners, reliability controls, and operational standards are ready before responsibility changes.

## Decision Boundaries

- Documentation structure is a means to help a reader complete work, not a reason to create empty sections or duplicate source material.
- A polished runbook is not evidence until a representative operator exercises it under realistic access and failure conditions.
- Screenshots age quickly and can expose data. Prefer durable text and expected observations; use an image only when it conveys otherwise difficult spatial context.
- Repository contribution guidance, product instructions, operational runbooks, and incident procedures serve different audiences and permission levels. Do not merge them into one catch-all file.
