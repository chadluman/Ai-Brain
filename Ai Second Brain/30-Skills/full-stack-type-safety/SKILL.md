---
name: full-stack-type-safety
description: Keep client and server types in agreement for a full-stack web project, using shared schemas and runtime validation so a type change cannot silently break the other side. Use when a frontend and backend share data shapes, forms, or API payloads; do not use for public API contract design alone, which is covered by API Contract Design.
---

# Full Stack Type Safety

## Outcome

Produce one authoritative data shape per shared concept, enforced at compile time and at runtime, so frontend, backend, and database code fail loudly — in tests, not in production — when they drift apart.

Use [API Contract Design](../api-contract-design/SKILL.md) for a public or third-party API contract. Use this skill for the internal full-stack boundary: the shapes a project's own client and server exchange.

## Required Inputs

- The shared concepts: entities, forms, API payloads, query results, and events that cross the client/server boundary.
- The current source of truth, if any: TypeScript types, a schema, an ORM model, a GraphQL schema, or handwritten interfaces on each side.
- Validation needs: which fields are user-controlled, which are server-generated, and which failures must be user-correctable versus rejected.
- The framework's type-sharing mechanism, if any: a monorepo package, generated client, tRPC-style router, or a shared schema package.

If there is no shared source of truth, create one before adding new shared fields. Do not fix drift by patching one side to match the other's mistake.

## Workflow

1. Name each shared concept once, and give it one schema file that both sides import or generate from. Prefer a runtime schema (for example Zod, Valibot, or an equivalent) over a TypeScript-only type, because a type disappears at runtime and cannot reject bad data.
2. Validate at every trust boundary: client input before it is sent, server input before it is used, and server output before it is trusted by the client. Never trust a shape because it type-checked in one codebase.
3. Separate three kinds of shape, even when they look similar: the database model, the API payload, and the UI form state. Map between them explicitly, and do not expose database fields, internal ids, or server secrets through an API payload by accident.
4. Make breaking changes explicit: add a field as optional first, migrate producers and consumers, then remove the old field. Record the change in an ADR when it changes a stored shape, a public payload, or a migration.
5. Generate, do not hand-copy, where generation is available: generate the client from the server schema, or generate both from one schema. If generation is not available, add a contract test that imports the shared schema on both sides and fails on mismatch.
6. Handle version skew: old clients, cached responses, and long-lived tabs may send or expect the previous shape. Use [Frontend State Design](../frontend-state-design/SKILL.md) and [Web Client Release Compatibility](../web-client-release-compatibility/SKILL.md) for mixed-version behavior, and reject or migrate stale payloads explicitly rather than coercing them silently.

## Safety and Permission Boundaries

- Treat client-sent data as untrusted, even when it was produced by your own frontend. Enforce authorization, tenant isolation, and invariants on the server for every request, regardless of what the client type says.
- Never put secrets, service keys, internal identifiers, or other users' data into a shared type that reaches the client.
- A shared schema is documentation, not approval. A new dependency, generated client, or schema library still requires the root security-review gate at its exact version.
- Do not change a stored shape, a migration, or a production payload without authorization at the R2/R3 boundary that applies to that change.

## Outputs and Evidence

- A list of shared schemas, their owners, and where each is imported or generated from.
- Contract tests or generation output proving client and server agree on the current shapes.
- A note, in the relevant ADR, for any breaking shape change: what changed, why, how old clients behave, and the migration or rollback path.
