---
name: content-cms-architecture
description: Design or select content models, editorial workflow, authoring tools, delivery architecture, governance, localization, accessibility, search, migration, and CMS boundaries. Use when non-developers manage web or app content or when content must be reused across channels.
---

# Content and CMS Architecture

## Outcome

Choose the smallest content system that supports real author and audience needs, produces accessible structured output, preserves ownership and portability, and avoids turning every page or UI string into unnecessary CMS complexity.

## Required Inputs

- content types, audiences, journeys, channels, volume, relationships, and reuse needs
- author, editor, reviewer, translator, legal, and publisher roles and accessibility needs
- draft, preview, approval, scheduling, embargo, versioning, audit, and emergency workflows
- localization, search, SEO, personalization, retention, deletion, and compliance requirements
- availability, latency, rendering, caching, offline, migration, portability, cost, and team constraints

## Safety and Permission Constraints

- Treat rich text, embeds, media, URLs, templates, webhooks, preview data, and imported content as untrusted. Sanitize for the output context and restrict active content.
- Authoring tools must be usable by disabled authors and help produce accessible content; an accessible public theme cannot compensate for an inaccessible editorial system.
- Separate editorial roles and least privilege. Preview and unpublished content can be confidential; prevent predictable URLs, cache leaks, search indexing, and cross-tenant access.
- Do not transmit content or personal data to plugins, translation, search, optimization, or AI services without provider review and authorization.
- Enabling a production CMS, migrating content, publishing, deleting, changing workflow, or installing an extension is R3 and requires authorization, version-specific review, backup, and rollback.

## Workflow

1. Inventory content by purpose, owner, audience, lifecycle, sensitivity, language, channel, update frequency, relationships, and source of truth.
2. Observe author and reviewer workflows. Define roles, accessible editing needs, approval boundaries, version history, scheduled work, emergency publishing, and support.
3. Model semantic reusable fields before pages. Keep presentation out of content where reuse matters, but allow bounded composition when authors need it.
4. Decide whether files, a database, a coupled CMS, a headless CMS, or no CMS best fits edit frequency, author count, preview, reuse, operations, and cost.
5. Evaluate authoring accessibility and generated-output accessibility, structured fields, validation, media alternatives, headings, link purpose, language, and preview fidelity.
6. Design API, webhook, cache, rendering, search-index, localization, and asset flows with versioned contracts, authentication, idempotency, freshness, deletion, and outage behavior.
7. Define canonical URLs, metadata, redirects, sitemap, content expiry, review reminders, archive, legal holds, export, and deletion across channels.
8. Prove representative content: a simple page, complex structured item, media item, localized variant, scheduled release, correction, rollback, and emergency update.
9. Test migration export and re-import, broken references, concurrent edits, provider outage, webhook duplication, preview leakage, inaccessible output, stale caches, and complete retirement.

## Required Output

- content inventory, ownership, lifecycle, and channel map
- author roles, editorial workflow, accessibility, and governance requirements
- content model, validation, relationships, identifiers, and localization design
- CMS-versus-simpler-system decision and comparison evidence
- rendering, API, webhook, cache, search, preview, and asset architecture
- migration, export, backup, rollback, deletion, and provider-exit plan
- representative author and audience validation results

## Completion Gate

Do not call the content architecture ready until representative authors can create and recover accessible content, unpublished material cannot leak, structured export is proven, and the selected system shows a material advantage over simpler repository or database content.

## Conditional Reference

Read [Content and CMS Evidence](references/content-cms-evidence.md) when evaluating authoring accessibility, content structure, tool portability, or workflow fit.
