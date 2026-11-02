---
name: frontend-runtime-resilience
description: Design or review browser runtime failure handling, cancellation, retries, stale responses, recoverable UI states, error isolation, and accessible feedback. Use when a web interface depends on asynchronous data, dynamic code, browser APIs, or long-running user input; do not hide failures behind generic toasts or automatic reloads.
---

# Frontend Runtime Resilience

## Outcome

Make browser failures bounded, understandable, accessible, observable, and recoverable while preserving user intent and preventing duplicate effects, stale commits, retry storms, and data loss.

Use [Service Resilience Design](../service-resilience-design/SKILL.md) for distributed-service controls, [Frontend State Design](../frontend-state-design/SKILL.md) for state ownership, [Interface Quality Review](../interface-quality-review/SKILL.md) for interaction quality, and [Observability and SLO Design](../observability-slo-design/SKILL.md) for system telemetry. This skill owns browser-runtime failure behavior.

## Required Inputs

- critical journeys, mutations, drafts, unsaved work, dependencies, dynamic imports, workers, browser APIs, supported environments, and offline behavior
- request semantics, time budgets, cancellation, idempotency, conflict, auth expiry, rate limits, retry signals, stale-response risk, and recovery source
- accessibility, privacy, telemetry, source-map, support, incident, kill-switch, release, and user-communication requirements

## Safety and Permission Constraints

- A rejected `fetch` promise does not represent every HTTP failure, and a timeout or navigation does not prove a side effect did not occur. Interpret transport, protocol, application, cancellation, and ambiguous outcomes separately.
- Do not automatically retry non-idempotent work, submit after a user cancellation, overwrite newer state with a late response, reload away unsaved work, or present cached or partial data as current authority.
- Preserve original user input when safe. Never include secrets, personal content, full URLs, credentials, or raw form bodies in client errors, analytics, traces, replay tools, or source-map services.
- Adding telemetry, session replay, remote error collection, or a production kill switch is R2 or R3 depending on data and external effects and requires exact provider, permission, retention, sampling, and rollback review.

## Workflow

1. Map each critical browser operation from user intent through validation, request or worker, response, state commit, rendering, and confirmation. Mark the authoritative commit and every ambiguous point.
2. Classify expected failures: validation, authorization or session expiry, conflict, rate limit, timeout, abort, offline or network, HTTP or application error, malformed data, stale response, rendering or hydration, dynamic asset load, worker, browser capability denial, storage or quota, and unknown defect.
3. Define pending, empty, degraded, stale, offline, conflict, recoverable error, terminal error, and success states. Keep actions operable where safe and prevent duplicate activation.
4. Set end-to-end deadlines and cancellation. Abort obsolete requests when useful, tag or sequence results, and refuse late responses that no longer match route, query, account, tenant, or user intent.
5. Retry only classified transient operations with bounded attempts, time, concurrency, backoff, jitter, and idempotency. Honor server pushback and stop on cancellation, auth failure, validation failure, or a newer user action.
6. Localize failure with route, component, worker, and feature boundaries appropriate to the framework. Handle event-handler, promise, worker, and global failures explicitly; no single error boundary catches every runtime fault.
7. Preserve drafts and task context when safe. Offer a truthful retry, resume, copy, refresh, alternate path, or support reference without loops, coercion, or destructive defaults.
8. Communicate status programmatically and visually. Associate field errors with controls, focus summaries deliberately, avoid surprise focus changes, distinguish progress from completion, and ensure feedback works with keyboard, zoom, reduced motion, and assistive technology.
9. Record sanitized error class, release, operation, correlation, environment, and recovery outcome with sampling and budgets. Keep client telemetry useful without stable cross-context tracking or payload capture.
10. Test slow, offline, aborted, duplicated, out-of-order, unauthorized, rate-limited, malformed, partially successful, stale, storage-full, chunk-missing, worker-failed, render-failed, and recovered cases during navigation, multi-tab use, account change, and deployment overlap.

## Required Output

- critical-operation and failure taxonomy with authority and ambiguity points
- state, deadline, cancellation, retry, idempotency, stale-response, and recovery rules
- accessible message, focus, draft-preservation, and user-control behavior
- error-isolation, telemetry, privacy, support, kill-switch, test, rollback, and residual-risk plan

## Completion Gate

Do not call the frontend resilient until representative failures preserve server authority and user intent, never duplicate irreversible effects, do not lose unsaved work without warning, expose an accessible recovery path, avoid loops and unbounded retries, and produce privacy-controlled evidence that support and operators can use.

## Conditional Reference

Read [Frontend Runtime Resilience Evidence](references/frontend-runtime-resilience-evidence.md) before defining cancellation, network-error interpretation, accessible notifications, or client error isolation.
