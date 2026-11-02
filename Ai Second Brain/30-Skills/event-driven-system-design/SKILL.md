---
name: event-driven-system-design
description: Design or review domain events, commands, event streams, schemas, producers, consumers, brokers, replay, ordering, delivery, compatibility, and recovery across an application. Use when asynchronous communication spans services or bounded modules; do not use a broker merely to avoid defining ownership or transactions.
---

# Event-Driven System Design

## Outcome

Produce an event architecture in which business meaning, authority, delivery semantics, ordering, compatibility, privacy, tenant context, recovery, and operational ownership are explicit and proven under duplication, delay, replay, and partial failure.

Use [Backend Boundary Design](../backend-boundary-design/SKILL.md) for deployment boundaries, [Background Job and Queue Design](../background-job-queue-design/SKILL.md) for worker execution, [Transaction and Concurrency Design](../transaction-concurrency-design/SKILL.md) for state invariants, and [API Contract Design](../api-contract-design/SKILL.md) for general compatibility. This skill owns event semantics and topology.

## Required Inputs

- business capabilities, authoritative state, invariants, producers, consumers, commands, facts, notifications, queries, and external integrations
- required latency, throughput, durability, delivery, ordering, replay, retention, fan-out, geographic, and recovery behavior
- event payloads, identity and tenant context, personal or regulated data, schema ownership, compatibility horizon, and consumer inventory
- transaction boundaries, outbox or change-capture options, broker or log capabilities, partitions, offsets, dead letters, and quotas
- monitoring, support, backfill, incident, disaster, migration, cost, provider, and team ownership constraints

## Safety and Permission Constraints

- An event is not automatically true, authorized, unique, ordered, delivered once, or safe to replay. Define how consumers establish authenticity, authority, context, freshness, and idempotency.
- Publish facts after the authoritative state transition. Do not use an event bus to conceal an undefined distributed transaction or let multiple components silently own the same invariant.
- Minimize payloads. Never broadcast secrets, bearer credentials, unrestricted URLs, unnecessary personal data, or client-supplied tenant identity. Treat retained event logs as data stores with access, retention, export, deletion, and incident obligations.
- Schema registries, brokers, connectors, change-data-capture agents, generators, SDKs, and hosted event systems are untrusted R2 or R3 assets requiring exact-version, permission, network, telemetry, and rollback review.
- Creating topics or accounts, connecting production systems, replaying or deleting real events, changing retention, or cutting live consumers is R3 and requires immediate authorization and bounded impact.

## Workflow

1. Identify the business fact or requested action, authoritative owner, transaction, consumers, and reason asynchronous communication is better than a direct call, scheduled query, or job. Remove events with no independent consumer value.
2. Distinguish commands, domain facts, integration events, notifications, change records, and audit records. Name events in completed domain language and state what they do and do not guarantee.
3. Draw producer, transactional store, publication mechanism, broker or log, partition, consumer group, consumer state, side effects, dead-letter or quarantine path, replay source, and observability. Assign one owner to each boundary.
4. Define an envelope with stable event ID, type, schema version, occurrence and publication time, source, subject, correlation and causation, tenant or domain context, trace context, and content type. Include only fields consumers are allowed and need to receive.
5. State delivery and ordering per producer-consumer path. Design every consumer for duplicates and retries; scope ordering only to the key and operation that require it; define late, missing, corrupt, poison, and out-of-order handling.
6. Make publication atomic with the state transition where required through a transactional outbox, log-derived publication, or an equivalent proven pattern. Define duplicate publication, relay recovery, and reconciliation rather than claiming exactly-once end-to-end behavior.
7. Version schemas and semantics for the full retention and replay window. Prefer additive evolution, tolerant readers, explicit defaults, and consumer contract tests; coordinate breaking changes with parallel events or translators and an exit date.
8. Define retention, compaction, redaction, deletion markers, legal holds, encryption, tenant isolation, access, export, replay authorization, and backup. Replayed historical events must not resurrect deleted data or repeat irreversible external effects.
9. Add bounded concurrency, quotas, backpressure, lag thresholds, retry budgets, circuit behavior, cost controls, and recovery tooling. Preserve the original event and decision evidence without leaking sensitive payloads into logs.
10. Test duplicates, reordering, gaps, stale and future schemas, producer transaction failure, relay failure, broker outage, partition loss, consumer crash before and after effects, poison data, replay, tenant crossing, deletion, new consumer backfill, region failover, and rollback.

## Required Output

- event catalog with type, owner, authoritative transition, consumers, purpose, payload class, and guarantees
- topology and data-flow map with transaction, publication, partition, delivery, ordering, retention, and replay decisions
- versioned envelope and schemas, compatibility rules, consumer contracts, and deprecation plan
- idempotency, side-effect, retry, backpressure, dead-letter, reconciliation, security, privacy, tenant, and cost controls
- failure, replay, deletion, migration, monitoring, ownership, rollback, and exit evidence

## Completion Gate

Do not call the design ready until every event has an authoritative owner and necessary consumer, publication cannot silently diverge from source state, consumers tolerate declared duplication and ordering behavior, schema evolution covers retained history, tenant and data boundaries survive replay, irreversible effects are protected, lag and loss are observable, and recovery tests reconcile to source truth.

## Conditional Reference

Read [Event-Driven System Evidence](references/event-driven-system-evidence.md) when selecting an event envelope, documenting asynchronous APIs, interpreting delivery claims, or designing compatibility and replay.
