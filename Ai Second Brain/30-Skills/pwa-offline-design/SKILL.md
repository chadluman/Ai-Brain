---
name: pwa-offline-design
description: Design or review installable, offline-capable, resilient web application behavior using service workers, manifests, browser storage, synchronization, and permissions. Use when offline or app-like web behavior serves a real user need; do not add a service worker solely for a PWA label.
---

# PWA and Offline Design

## Outcome

Produce an explicit offline and update model that improves critical journeys without serving stale private data, losing work, trapping clients on bad code, or depending on unsupported install behavior.

Read [offline platform evidence](references/offline-platform-evidence.md) before selecting manifest, service-worker, storage, or synchronization behavior.

## Inputs

Identify offline and unreliable-network journeys, install value, supported browsers and webviews, data sensitivity, shared-device risk, read and write behavior, conflict rules, storage volume, update urgency, authentication and session behavior, notifications, background work, content freshness, accessibility, and backend idempotency.

## Workflow

1. Define which actions must work offline, degrade read-only, queue safely, or stop with a clear explanation. Design online failure well before adding installation.
2. Classify resources and data. Choose an explicit network, cache, revalidation, or offline strategy per class; never use one catch-all caching rule.
3. Define service-worker install, activation, versioning, client control, cache migration, update prompt, rollback, and removal. Test old clients during a mixed-version rollout.
4. Define local data schema, quota expectations, persistence request, eviction and corruption behavior, encryption limits, logout cleanup, account switching, and shared-device exposure.
5. For offline writes, define durable queue state, ordering, retries, idempotency keys, authentication expiry, conflicts, user review, cancellation, reconciliation, and permanent failure.
6. Treat cached API responses and documents according to user and tenant. Prevent private data from entering shared or cross-account caches and clear it on lifecycle transitions.
7. Add manifest metadata, install prompts, push, notifications, file or protocol handlers, and background behavior only when supported targets and user value justify each permission and maintenance surface.
8. Test first visit, repeat visit, slow and absent network, partial cache, quota pressure, eviction, update during use, revoked auth, duplicate sync, conflict, multi-tab behavior, browser restart, uninstall, and service-worker removal.

## Safety and Scope

- Service workers can intercept origin requests and persist beyond a page. Their scripts and dependencies require the same security scrutiny as privileged application code.
- Browser storage is not a secret vault and can be lost, evicted, inspected, or exposed through application compromise.
- Push and notification providers, analytics, sync services, and production permission changes can transmit user data and require explicit authorization and privacy review.
- Installability and feature behavior differ across browsers, operating systems, and webviews; define fallbacks rather than claiming universal PWA support.

## Completion

Deliver the offline capability matrix, cache and freshness policy, service-worker lifecycle, local schema and quota behavior, sync and conflict protocol, security and privacy controls, manifest and permission scope, update and removal plan, representative test evidence, observability, and unresolved platform gaps.
