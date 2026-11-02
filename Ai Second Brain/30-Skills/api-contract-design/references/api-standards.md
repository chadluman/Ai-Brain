# API Standards

Verified 2026-10-21. Pin the exact specification dialect used by a project.

- [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) is the IETF Standards Track source for methods, status codes, representations, intermediaries, safety, idempotency, and related semantics.
- [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html) defines cache storage, freshness, validation, invalidation, authenticated responses, and security considerations.
- [Problem Details for HTTP APIs, RFC 9457](https://www.rfc-editor.org/rfc/rfc9457.html) defines machine-readable HTTP error details and obsoletes RFC 7807. Its security section still applies; a standard format does not make every detail safe to disclose.
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html) defines a language-neutral interface description for HTTP APIs. Version 3.2.1 was the latest published version when verified. Confirm generator, validator, and gateway support before selecting a dialect.
- [JSON Schema](https://json-schema.org/specification) lists 2020-12 as the current published core and validation dialect when verified. Format vocabularies and implementation support require explicit checking.
- The [GraphQL specification](https://spec.graphql.org/) listed September 2025 as the latest release when verified. Use the released specification rather than the working draft unless experimental behavior is explicitly accepted.
- [CloudEvents](https://cloudevents.io/) standardizes an event envelope. It does not define a broker's delivery, ordering, retention, replay, or authorization guarantees.

## Interpretation

Select a specification because consumers and tooling benefit from a precise contract, not because code generation is available. Validate the specification itself, examples, server behavior, and generated clients against the same compatibility policy. Treat undefined and implementation-defined areas as risks to test.
