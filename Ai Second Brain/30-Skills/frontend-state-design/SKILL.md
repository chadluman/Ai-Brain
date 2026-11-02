---
name: frontend-state-design
description: Define ownership, lifetime, persistence, synchronization, and failure behavior for frontend application state. Use when state is duplicated, stale, difficult to test, shared across routes, persisted locally, or synchronized optimistically; do not add a state library before identifying the state categories and owners.
---

# Frontend State Design

## Outcome

Create a minimal state model with one authoritative owner per fact, predictable navigation and recovery, explicit server synchronization, and no unnecessary global or persistent data.

Read [browser state evidence](references/browser-state-evidence.md) before placing data in URLs, history, or persistent browser storage.

## Inputs

Inventory user journeys, routes, canonical server data, drafts, filters and navigation, authentication and tenant context, optimistic actions, realtime updates, offline needs, multiple tabs or devices, persistence, sensitivity, accessibility behavior, and failure or reload expectations.

## Workflow

1. Classify each value as authoritative server state, URL-addressable state, session or navigation state, local persistent state, ephemeral component state, or derived state.
2. Give each fact one owner. Derive views rather than copying values into multiple stores, and document intentional snapshots or caches with freshness rules.
3. Put shareable and navigable state in stable URLs when safe. Preserve back, forward, reload, deep link, and new-tab behavior without exposing secrets or sensitive filters.
4. Keep server data behind an explicit fetch, cache, invalidation, mutation, and error model. Do not treat a client cache as the authority for access or business invariants.
5. For optimistic work, define the predicted state, idempotency, conflict detection, rollback or reconciliation, duplicate events, out-of-order responses, cancellation, and accessible status.
6. Persist only data with clear reload or offline value. Define version migration, quota and eviction, corruption, account switching, logout deletion, retention, and recovery.
7. Handle multi-tab, realtime, and device updates according to the product's consistency need; choose refresh, invalidation, merge, or conflict presentation deliberately.
8. Add a state library only when framework primitives and small modules cannot meet measured coordination, debugging, or testing needs. Review its exact dependency and lifecycle.
9. Test navigation, refresh, deep link, slow and failed requests, duplicate submissions, stale responses, auth expiry, account change, storage loss, offline and reconnect, concurrency, and assistive announcements.

## Safety and Scope

- Do not store credentials, authorization decisions, private keys, or unnecessary personal data in URLs or browser persistence.
- Client state cannot authorize server actions, protect prices or roles, or make unvalidated external data trustworthy.
- Persistence and synchronization can extend retention and data exposure; include them in privacy and deletion design.
- Global state is a coupling cost, not a default architecture layer.

## Completion

Deliver the state inventory and owners, lifetime and persistence matrix, URL policy, server-cache and mutation rules, optimistic and conflict behavior, privacy and cleanup, failure and accessibility states, test evidence, library decision, and re-evaluation triggers.
