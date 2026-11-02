# Search Evidence

Verified: 2026-10-21

## Standards and Product Evidence

- [Unicode Standard Annex #29](https://www.unicode.org/reports/tr29/) version 49 for Unicode 18.0.0 defines stable default grapheme, word, and sentence segmentation guidance. Language-specific tailoring may still be needed.
- [PostgreSQL current full-text search](https://www.postgresql.org/docs/current/textsearch.html) documents parsing, dictionaries, ranking, highlighting, indexes, debugging, and explicit limitations for database-native search.
- [OpenSearch text analysis](https://docs.opensearch.org/latest/analyzers/) documents character filters, tokenizers, token filters, index-time and query-time analysis, and analyzer consistency.
- [OpenSearch Search Relevance Workbench](https://docs.opensearch.org/latest/search-plugins/search-relevance/using-search-relevance-workbench/) documents query sets and judgment lists as inputs to iterative relevance evaluation. It is product-specific tooling, not a universal methodology.

## Interpretation Boundaries

- Search-engine documentation establishes available behavior, not relevance for a domain. Representative judgments are required.
- Database-native search can be the best operational choice at moderate scale; a separate cluster adds synchronization, security, backup, and cost burdens.
- Vector similarity is not a truth or authorization signal. Embedding models can change, leak information, add bias, and require reindexing.
- The index must remain disposable derived state unless a deliberately designed system makes it authoritative.
