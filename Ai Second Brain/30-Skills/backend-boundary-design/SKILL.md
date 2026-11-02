---
name: backend-boundary-design
description: Define the smallest reliable backend shape, service boundaries, execution modes, and failure behavior for a web or application project. Use for new backend architecture or a material topology change; do not split a system into services merely for scale or fashion.
---

# Backend Boundary Design

## Outcome

Produce a backend topology that keeps domain invariants and trust boundaries clear while meeting latency, availability, scaling, delivery, and operating constraints with the fewest necessary deployment units.

Read [backend evidence](references/backend-evidence.md) when choosing communication and event boundaries.

## Inputs

Establish domain capabilities, critical operations, data ownership, consistency needs, latency and throughput targets, background and scheduled work, realtime behavior, external integrations, failure tolerance, security and privacy classification, regions, expected growth, team ownership, deployment environment, budget, and recovery objectives.

## Workflow

1. Map user-visible capabilities, domain invariants, data flows, trust boundaries, and external dependencies before drawing service boxes.
2. Start with one deployable backend when it can safely satisfy the requirements. Keep internal modules and ownership boundaries explicit so later extraction remains possible.
3. Separate a component only when an independent security boundary, scaling profile, failure domain, runtime, release cadence, data owner, or team boundary justifies the operational cost.
4. Choose synchronous calls only where the caller needs an immediate result. For asynchronous work define durability, ordering, duplication, retries, idempotency, backpressure, deadlines, poison-message handling, and reconciliation.
5. Define transaction boundaries and ownership for every invariant. Do not hide a cross-service distributed transaction behind optimistic diagrams.
6. Model dependency failure, overload, partial completion, timeouts, cancellation, restarts, region loss, and deploy rollback. Set resource limits and degradation behavior.
7. Attach authentication, authorization, validation, audit, secrets, privacy, retention, observability, backup, and restore responsibilities to named boundaries.
8. Prove the riskiest path with a thin vertical slice and representative load or failure tests, then record material choices in ADRs.

## Guardrails

- More services increase network, identity, consistency, deployment, monitoring, incident, and cost surfaces.
- A queue or event bus changes delivery semantics; it does not make work reliable without idempotent consumers, durable state, and recovery.
- Serverless, containers, long-running services, edge runtimes, and managed workflows are execution choices, not architecture goals.
- Never place secrets, private data, or authorization decisions in messages, logs, caches, or client-visible state without explicit need and protection.
- Provisioning accounts, infrastructure, paid resources, production data, or deployments is R3 and requires authorization at the consequential step.

## Completion

Deliver the domain and trust-boundary map, deployment units, communication modes, data ownership, failure and overload behavior, security and observability responsibilities, cost and operations implications, vertical-slice evidence, ADRs, exit paths, and re-evaluation triggers.
