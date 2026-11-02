---
name: web-internationalization
description: Design or review a web application for multiple languages, scripts, regions, formats, and translation workflows. Use before localization, adding locales, supporting right-to-left content, or internationalizing routes and data; do not reduce locale to a country flag or machine translation step.
---

# Web Internationalization

## Outcome

Create a locale-aware architecture and content workflow that preserves meaning, accessibility, layout, data integrity, and user choice across supported languages and regions.

Read [internationalization evidence](references/internationalization-evidence.md) before defining language tags, locale data, or formatting behavior.

## Inputs

Identify target users, languages, scripts, regions, regulatory and market needs, content owners, translation method, release cadence, URLs and discoverability, user-generated content, names and addresses, dates and calendars, time zones, numbers, currencies and units, sorting and search, typography, bidirectionality, accessibility, and offline behavior.

## Workflow

1. Separate language, script, region, locale, currency, time zone, and market. Store only the distinctions the product actually needs.
2. Use Unicode and UTF-8 end to end. Declare the document language and changes within content with valid language tags; set direction from content and test mixed-direction text.
3. Externalize user-facing messages with stable meanings and context. Avoid sentence concatenation, fixed word order, embedded markup fragments, and assumptions about plural or grammatical categories.
4. Use standard locale data and platform formatting for dates, times, numbers, lists, plurals, currencies, units, and collation. Store canonical values separately from localized display.
5. Design locale selection and fallback deliberately. Preserve user choice, make language navigation understandable in the target language, and do not infer a permanent preference from location alone.
6. Allow expansion, contraction, alternate line breaks, input methods, long names, varying address formats, RTL layouts, vertical or mixed scripts when required, and fonts with correct glyph coverage.
7. Define translation source, glossary, context, review, status, versioning, missing-message behavior, content fallback, and urgent correction. Human review is required where meaning, safety, law, commerce, or brand impact is material.
8. Test pseudolocalization, target scripts, keyboard and assistive technology, zoom, truncation, bidi isolation, forms, search and sort, dates around time-zone boundaries, currency precision, and multilingual URLs.

## Safety and Scope

- Language and locale can reveal sensitive identity or location. Minimize collection and do not send content to translation services without authorization and data review.
- Machine translation can assist drafts but does not certify legal, medical, financial, safety, policy, or high-impact content.
- Do not use flags as the only representation of language; countries and languages are not one-to-one.
- Localization dependencies, font files, translation platforms, and automated content services require exact-version, license, privacy, and telemetry review.

## Completion

Deliver the supported-locale matrix, tag and fallback policy, route and discovery behavior, message and formatting architecture, content workflow, RTL and layout requirements, privacy boundaries, representative test evidence, ownership, rollout and rollback, and expansion triggers.
