# Cache Evidence

Verified: 2026-10-21

## Standards and Operations Guidance

- [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html) defines storage eligibility, freshness, age, validation, `Vary`, authorization interactions, and cache-control directives.
- [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) defines methods, representations, validators, conditional requests, and semantics that caching relies on.
- [RFC 5861](https://www.rfc-editor.org/rfc/rfc5861.html) defines the `stale-while-revalidate` and `stale-if-error` cache-control extensions. Stale serving must remain within application correctness and privacy limits.
- [Google SRE: Addressing Cascading Failures](https://sre.google/sre-book/addressing-cascading-failures/) supports bounded admission, overload protection, and cautious recovery relevant to cold-cache and stampede behavior.

## Interpretation Boundaries

- `no-cache` permits storage but requires validation before reuse; `no-store` addresses storage. Use the RFC meanings rather than their everyday wording.
- `private` and shared-cache rules do not replace application authorization or a complete cache key.
- An application cache, CDN, runtime cache, browser cache, and database cache have different contracts. Document each layer separately.
- A high hit rate can coexist with stale data, leaks, or poor product latency. Measure user outcomes and correctness.
