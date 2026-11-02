# External API Evidence

Verified: 2026-10-21

## Standards and Security Guidance

- [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html) defines safe and idempotent methods, status semantics, redirects, and `Retry-After`. Protocol idempotence does not prove business-level duplicate safety.
- [RFC 9457: Problem Details for HTTP APIs](https://www.rfc-editor.org/rfc/rfc9457.html) defines interoperable machine-readable HTTP error details. Problem bodies remain untrusted input and must not leak secrets.
- [OWASP REST Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html) covers HTTPS, per-operation authorization, token validation, method and media-type controls, input validation, CORS, and security response behavior.
- [IETF RateLimit header fields draft](https://datatracker.ietf.org/doc/draft-ietf-httpapi-ratelimit-headers/) was an active Internet-Draft at verification, not an RFC. Treat its fields as evolving and follow the actual provider contract.

## Decision Boundaries

- `Retry-After` is server guidance, not proof that a retry is safe or will succeed. Combine it with operation semantics, a deadline, jitter, and an attempt cap.
- A 2xx response can represent acceptance rather than completion; a timeout or 5xx can occur after a provider committed work. Model unknown outcomes explicitly.
- Provider SDK convenience can add telemetry, dependencies, hidden retries, broad permissions, or version lag. Compare it with a direct standards-based adapter.
- Sandboxes frequently differ in data, fraud controls, quotas, timing, webhooks, regional behavior, and failure modes. Production activation still needs bounded canary evidence.
