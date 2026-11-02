# Web Client Release Compatibility Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html) is the current Internet Standard for cache storage, freshness, reuse, validation, invalidation, and directives. Browser history and application-managed caches can have additional behavior outside its direct requirements.
- [Immutable HTTP Responses, RFC 8246](https://www.rfc-editor.org/rfc/rfc8246.html) defines the `immutable` cache-control extension. It reduces unnecessary validation only when a resource URL truly never changes representation.
- [Service Workers](https://www.w3.org/TR/service-workers/) is a current Candidate Recommendation Draft snapshot in 2026. Registrations can outlive pages, workers move through installing, waiting, and active states, and user agents can terminate running workers.
- [The service worker lifecycle](https://web.dev/articles/service-worker-lifecycle) is Google-authored operational guidance explaining that a new worker normally waits until old clients close, old clients can remain for long periods, and immediate activation can mix versions. It is informative, not a substitute for the normative specification or product testing.
- [HTML Standard: scripting](https://html.spec.whatwg.org/multipage/scripting.html) defines script, module, and import-map processing that underlies generated bundles and dynamic loading. A build tool's chunk behavior remains implementation-specific.

## Decision Implications

- Cache content-addressed assets for long reuse only when the URL changes with the bytes. Retain every asset referenced by any supported HTML, worker, or rollback release.
- A service worker is a separately deployed client runtime. Page, worker, cache, API, and schema versions need an explicit compatibility contract.
- Immediate worker activation can be appropriate for an urgent isolated fix only when old pages remain compatible; it is not a universal freshness improvement.
- HTTP cache correctness does not guarantee application-version coherence. Release manifests, asset retention, API compatibility, local migrations, flags, and user-safe recovery must be coordinated and tested together.
