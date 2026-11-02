---
name: background-job-queue-design
description: Design or review asynchronous background jobs, queues, workers, retries, scheduling, backpressure, idempotency, dead-letter handling, and operational recovery. Use when work must outlive a request, absorb bursts, or retry independently; do not use when a synchronous operation is simpler and meets the requirement.
---

# Background Job and Queue Design

## Outcome

Produce the smallest asynchronous design that preserves business invariants under retries, concurrency, overload, worker failure, delayed delivery, and operator replay.

## Required Inputs

- job purpose, producer, consumer, payload, side effects, and source of truth
- completion deadline, throughput, burst shape, task duration, and resource cost
- delivery, ordering, uniqueness, consistency, cancellation, and concurrency requirements
- retryable and terminal failure classes
- retention, privacy, residency, recovery, and audit requirements
- deployment environments and operational ownership

If work can safely complete within the request and does not need independent retry or burst absorption, prefer the synchronous path.

## Safety and Permission Constraints

- Assume at-least-once execution unless an exact provider contract and end-to-end proof establish stronger behavior.
- Never place secrets or unnecessary personal data in job payloads. Prefer opaque identifiers and fetch authorized current state at execution time.
- Treat queue payloads as untrusted and version them. Re-authorize sensitive work at execution rather than relying only on producer context.
- Bound queue depth, payload size, concurrency, retries, execution time, and external calls. Unbounded queues hide overload and increase stale work.
- Production queue creation, destructive purge, bulk replay, priority changes, or real-data migration is R3 and requires immediate authorization and a verified rollback or reconciliation plan.
- Review each broker, worker library, hosted service, and dashboard as a versioned third-party asset before use.

## Workflow

1. Define the invariant and completion semantics before choosing a broker. Separate event notification, command, scheduled job, durable workflow, and batch processing needs.
2. Choose the least complex mechanism that satisfies durability, timing, scale, and recovery. Record why an in-process task, database-backed queue, broker, scheduler, or workflow engine fits.
3. Define the message envelope: stable identifier, type and schema version, creation and expiry time, tenant or security context, trace correlation, and an opaque reference to large or sensitive data.
4. Make the handler idempotent. Use state-machine preconditions, unique constraints, compare-and-set operations, idempotency records, or a transactional outbox/inbox as the invariant requires.
5. Define acknowledgement or lease timing, visibility renewal, crash recovery, concurrency limits, partitioning, and ordering scope. Do not promise global order unless the system truly provides and needs it.
6. Classify failures. Retry transient failures with exponential backoff and jitter within a retry budget; quarantine terminal, malformed, expired, or repeatedly failing work with a reason.
7. Design overload behavior: bounded admission, backpressure, per-tenant fairness, rate limits, load shedding, and degradation. Prevent retries from multiplying an outage.
8. Define cancellation, supersession, replay, draining, deployment compatibility, and schema migration. Make replay distinguishable and safe.
9. Observe age of oldest job, backlog, arrival/completion rates, latency, attempts, failures, quarantine, worker saturation, and cost. Alert on user impact and exhaustion risk.
10. Test duplicate execution, worker crash before and after the side effect, timeout, dependency outage, overload, poison input, delayed job, schema change, cancellation, replay, and recovery.

## Required Output

- synchronous-versus-asynchronous decision and selected mechanism
- message contract, delivery assumptions, ordering scope, and retention
- idempotency and transaction-boundary design
- retry, backoff, quarantine, replay, and cancellation policy
- capacity, fairness, backpressure, observability, and cost controls
- failure-injection test plan and evidence
- operations, drain, migration, rollback, and recovery procedure

## Completion Gate

Do not call the design complete until duplicate and crash-window tests preserve the invariant, overload has a bounded response, poison work cannot block healthy work, and operators can identify and safely replay or retire failures. Keep the skill draft until validated with a realistic worker failure exercise.

## Conditional Reference

Read [Queue and Job Evidence](references/queue-job-evidence.md) when deciding delivery assumptions, overload controls, event envelopes, or operational tests.
