---
name: full-stack-server-data-design
description: Design server-side data loading, mutations, and revalidation for a full-stack web framework, using loaders and server actions rather than ad-hoc client fetches. Use when a framework offers server loaders, server actions, or route actions; do not use for a public API, which is covered by API Contract Design, or for client-only state, which is covered by Frontend State Design.
---

# Full Stack Server Data Design

## Outcome

Produce a server-data model where each route loads exactly what it renders, each mutation is validated and authorized on the server, and the UI revalidates predictably after a change — without duplicating data logic in the client.

Use [Frontend Rendering Selection](../frontend-rendering-selection/SKILL.md) to choose rendering per route. Use this skill for what happens inside the server part of that route: loading, mutating, and revalidating.

## Required Inputs

- Routes and their data needs: what each route renders, what it must not expose, and what changes it can make.
- Authorization and tenancy: who may read or change each record, and how that is enforced on the server.
- Mutation outcomes: success, validation failure, authorization failure, conflict, and partial failure, and what the user sees in each case.
- Revalidation needs: which routes, caches, and client views become stale after each mutation, and how quickly they must refresh.

## Workflow

1. Put data loading on the server for server-rendered routes. Load only what the route renders, in as few round trips as the data model allows, and do not fetch the same record twice through different paths.
2. Put every mutation behind a server action or route action, never behind a client-only write. Validate input with the shared schema from [Full Stack Type Safety](../full-stack-type-safety/SKILL.md), authorize on the server, and enforce invariants and tenant isolation there, even if the client already checked them.
3. Make mutations idempotent where a retry, double-submit, or duplicate request is possible. Use idempotency keys, unique constraints, or conditional updates, and define what a duplicate submission returns.
4. Define revalidation explicitly per mutation: which routes and caches refresh, which stay stale and why, and what happens if revalidation fails. Do not rely on a full page reload as the revalidation strategy unless that is a deliberate, documented choice.
5. Separate optimistic UI from server truth. Use [Frontend State Design](../frontend-state-design/SKILL.md) for optimistic updates, and always reconcile against the server result: confirm, roll back, or surface a conflict, with an accessible status while the mutation is in flight.
6. Handle errors as user-actionable states, not as stack traces: validation errors field by field, authorization errors without leaking existence, and server errors with a retry or recovery path. Log the server detail; show the user only what helps them act.

## Safety and Permission Boundaries

- Never trust client-sent ids, roles, tenant ids, or prices. Re-derive authorization and pricing on the server from the authenticated session and the stored record.
- Never return another user's or tenant's data through a loader, even if the client route is not supposed to request it. Authorization is a server property, not a UI property.
- Server actions that change data, send messages, charge money, or delete records are R2/R3 actions. They require the authorization and rollback planning that applies to that action, not just a UI button.
- Do not expose database errors, internal ids, or secret values in loader or action responses.

## Outputs and Evidence

- A per-route loading and mutation table: route, server loader/action, authorization check, validation schema, and revalidation targets.
- Tests proving unauthorized access is rejected on the server, validation failures are field-accurate, and duplicate submissions do not double-apply.
- A note in the relevant ADR for any framework-specific server-data choice that locks in a rendering, caching, or deployment assumption.
