---
name: api-contract-design
description: Design or review a stable HTTP, GraphQL, or event API contract, including schemas, errors, compatibility, retries, authorization, and consumer verification. Use for new APIs, public integrations, or breaking contract changes; do not select a protocol from fashion alone.
---

# API Contract Design

## Outcome

Create a precise, evolvable interface that consumers can use safely under validation errors, retries, concurrency, partial failure, and version change.

Read [API standards](references/api-standards.md) before selecting a specification version or asserting protocol behavior.

## Inputs

Identify consumers and owners, trust boundaries, operations and invariants, data sensitivity, latency and volume, client environments, caching, realtime or streaming needs, offline behavior, compatibility period, support model, and the cost of a breaking change.

## Workflow

1. Model consumer journeys and domain operations before paths, fields, or resolver shapes.
2. Choose the simplest protocol that fits. Use HTTP semantics directly where useful; choose GraphQL, events, streaming, or another style only for requirements that justify their additional runtime and governance.
3. Define identifiers, resources or operations, request and response schemas, null and absence behavior, field meanings, units, timestamps, pagination, filtering, ordering, concurrency, and size limits.
4. Define authentication and authorization independently. Enforce object, field, operation, and tenant access on the server for every request.
5. Define machine-readable errors without leaking secrets, internals, cross-tenant identifiers, or sensitive existence. Make retryability and user-correctable failures unambiguous.
6. For every mutation define atomicity, idempotency, duplicate and replay behavior, concurrency conflicts, timeouts, cancellation, and reconciliation. Do not retry a non-idempotent operation blindly.
7. Define cacheability, validators, privacy boundaries, rate and quota behavior, and client backoff. Shared caches must not mix users or tenants.
8. Specify evolution rules: additive changes, deprecation notice, version negotiation, compatibility window, schema migration, consumer inventory, and removal evidence.
9. Verify examples and schemas, run provider and consumer contract tests, and test malformed, unauthorized, oversized, duplicated, reordered, slow, and failed requests.

## Protocol, Specification, and Versioning

Use this section to make step 2 and step 8 concrete. It is a starting heuristic, not a ranking — choose from the requirements, never from fashion.

| Need | Lean toward |
|---|---|
| Simple CRUD over HTTP, with caching and broad client support | REST |
| Client-driven field selection, many related types, aggregated reads | GraphQL |
| Type-safe client-server calls inside one TypeScript codebase | tRPC |
| High-throughput service-to-service calls or streaming with strict schemas | gRPC |

Describe HTTP APIs with OpenAPI 3.1 as the current specification version, and record the exact specification version in the deliverable.

Prefer cursor pagination for large or changing lists: offset pagination can skip or repeat rows as data changes underneath the reader. [Standard practice; no dedicated source was retrieved for this guidance.]

Record a versioning plan up front, before the first consumer ships: how versions are signalled, how long old versions are supported, how consumers are notified before removal, and what evidence justifies removal. See [Deprecation and Sunset Design](../deprecation-and-sunset-design/SKILL.md) for the deprecation and sunset side of that plan.

## Safety and Scope

- A schema describes shape; it does not replace runtime validation, authorization, output encoding, abuse prevention, or business invariants.
- Generated servers and clients, validators, documentation UIs, SDKs, and linters are executable dependencies requiring exact-version R2 review.
- Never put credentials or sensitive values in URLs, example payloads, logs, specifications, or generated documentation.
- Public or partner API publication, credential issuance, external callbacks, and production traffic changes are R3.

## Completion

Deliver the contract and exact specification version, trust and authorization model, validation and error behavior, idempotency and concurrency rules, caching and quota behavior, compatibility policy, contract-test evidence, operational limits, migration and rollback path, and unresolved risks.
