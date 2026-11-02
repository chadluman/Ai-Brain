---
name: search-architecture-selection
description: Select or review exact, full-text, faceted, autocomplete, geospatial, vector, semantic, or hybrid search architecture, including indexing, relevance evaluation, authorization, freshness, deletion, scaling, and migration. Use when users must find domain records or content; do not add a dedicated search service before database search is proven insufficient.
---

# Search Architecture Selection

## Outcome

Choose the smallest search architecture that meets measured findability, relevance, language, security, freshness, and scale needs, with reproducible evaluation and a rebuildable index.

## Required Inputs

- searchable entities, fields, ownership, sensitivity, and source of truth
- representative queries, intents, languages, scripts, misspellings, filters, facets, and sort needs
- freshness, latency, availability, scale, update, and deletion objectives
- tenant and object authorization, privacy, abuse, and result-explanation requirements
- relevance owners, judgment process, operating capacity, cost, and vendor constraints

## Safety and Permission Constraints

- Search indexes are derived sensitive stores. Apply encryption, access control, retention, backup, deletion, region, and incident controls appropriate to their content.
- Authorization must filter results, counts, facets, suggestions, highlights, and direct document access. Post-filtering a leaked result set is insufficient.
- Treat queries and indexed documents as untrusted. Bound complexity, pagination, regex or script features, highlighting, snippets, and returned fields.
- Do not send private documents or queries to embedding, reranking, analytics, or hosted search providers without approved data handling.
- Production reindex, alias switch, deletion, provider migration, or semantic model change is R3 and requires authorization, reconciliation, and rollback.

## Workflow

1. Define search journeys and success with a versioned query set and human judgments. Include exact identifiers, common language, zero-result, adversarial, and multilingual cases.
2. Start with direct database lookup and native full-text capability where scale and features permit. Add a dedicated engine only for measured gaps such as relevance, facets, typo tolerance, language, scale, or latency.
3. Define document shape, field ownership, source identifiers, tenant and authorization attributes, language, timestamps, schema version, and deletion markers.
4. Choose lexical, vector, semantic, or hybrid retrieval from the query intents. Use semantic components only when they improve the judged set enough to justify privacy, latency, cost, and explainability.
5. Design language-specific normalization, segmentation, analyzers, stemming, synonyms, transliteration, and locale behavior. Test with native-language judgments.
6. Build an idempotent indexing path with an outbox or change stream, version checks, retries, gap detection, backfill, reconciliation, and complete rebuild from the source of truth.
7. Enforce authorization in the query or trusted index partition. Recheck authorization before consequential access when policy can change faster than the index.
8. Tune against offline relevance metrics and human review, then monitor click and task outcomes without turning popularity into an unchecked feedback loop.
9. Define zero-result handling, safe suggestions, pagination, stable sort, duplicate collapse, freshness indicators, and outage fallback.
10. Test stale and duplicate updates, deletion, schema and analyzer migration, reindex, alias switch, rollback, cross-tenant queries, hot queries, overload, and restore.

## Required Output

- query-intent set, judgments, and relevance metrics
- database-versus-dedicated-engine decision
- document, analyzer, retrieval, ranking, and authorization design
- indexing, freshness, deletion, reconciliation, and rebuild plan
- privacy, abuse, cost, observability, and fallback controls
- migration, rollback, and provider-exit strategy
- validation results by language and critical journey

## Completion Gate

Do not call search ready until relevance is measured on representative queries, protected records and metadata cannot leak, deletion and rebuild are verified, and dedicated infrastructure shows a material benefit over the simpler baseline.

## Conditional Reference

Read [Search Evidence](references/search-evidence.md) when selecting text analysis, database search, a dedicated engine, or relevance evaluation.
