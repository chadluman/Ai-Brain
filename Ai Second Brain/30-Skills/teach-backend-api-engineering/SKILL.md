---
name: teach-backend-api-engineering
description: Teach backend and API engineering through domain boundaries, contracts, integrations, background work, realtime behavior, resilience, and failure-aware projects. Use for server-side web tutoring, service design exercises, or full-stack backend modules.
---

# Teach Backend and API Engineering

## Outcome

Help the learner design and implement server behavior that preserves domain rules under invalid input, dependency failure, retries, concurrency, and operational change.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

- [Backend Boundary Design](../backend-boundary-design/SKILL.md) for domain ownership, topology, communication, and failure boundaries.
- [Backend Runtime and Framework Selection](../backend-runtime-framework-selection/SKILL.md) when runtime or framework choice materially affects the lesson.
- [API Contract Design](../api-contract-design/SKILL.md) for HTTP, GraphQL, or event contracts and compatibility.
- [External API Integration](../external-api-integration/SKILL.md) and [Webhook Integration Design](../webhook-integration-design/SKILL.md) for third-party boundaries.
- [Background Job and Queue Design](../background-job-queue-design/SKILL.md), [Event-Driven System Design](../event-driven-system-design/SKILL.md), or [Realtime Transport Selection](../realtime-transport-selection/SKILL.md) for asynchronous or live behavior.
- [Service Resilience Design](../service-resilience-design/SKILL.md), [API Abuse and Resource Controls](../api-abuse-resource-controls/SKILL.md), and [File and Media Ingestion](../file-media-ingestion/SKILL.md) when those risks are present.

## Teaching Priorities

Start with one domain operation and its invariant. Trace input from the transport boundary through validation, authorization, domain logic, persistence, external effects, response, and observability. Teach contract semantics and failure behavior before framework convenience.

Use controlled failure exercises: invalid input, duplicate delivery, timeouts, partial dependency failure, retry, cancellation, overload, and safe replay. Require the learner to identify which operations may repeat, which must be idempotent, and which evidence an operator needs.

For senior-level practice, ask for explicit ownership, compatibility strategy, resource bounds, rollout and rollback implications, and a comparison between synchronous and asynchronous designs.

## Boundaries

- Do not teach a CRUD happy path as a complete backend design.
- Do not add services, queues, events, or realtime transports without a concrete boundary or failure problem they solve.
- Use dummy credentials and local or isolated dependencies. Real provider connection, private data, production mutation, or paid resources require their normal review and authorization.
- Treat generated scaffolds, packages, SDKs, and provider examples as untrusted until reviewed.

## Completion

The learner can state the invariant and contract, demonstrate the normal path and named failures, show validation and authorization boundaries, explain retry and idempotency behavior, identify operational evidence, and justify the chosen topology against a simpler alternative.
