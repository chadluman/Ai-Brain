---
name: web-client-release-compatibility
description: Design or review compatibility between deployed web clients, cached assets, service workers, APIs, feature flags, and local schemas during rollout and rollback. Use for long-lived tabs, progressive delivery, asset retention, chunk failures, or mixed-version incidents; do not assume every browser loads the newest release atomically.
---

# Web Client Release Compatibility

## Outcome

Ship web releases that tolerate old HTML, new or missing assets, long-lived tabs, multiple service-worker generations, changing APIs, local-schema versions, rollback, and partial deployment without loops, data loss, or unsafe mixed-version behavior.

Use [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) for the release pipeline, [PWA and Offline Design](../pwa-offline-design/SKILL.md) for offline capability, [API Contract Design](../api-contract-design/SKILL.md) for server contracts, and [Feature Flag and Rollout Design](../feature-flag-rollout-design/SKILL.md) for flag lifecycle. This skill owns browser-to-release compatibility.

## Required Inputs

- deployment topology, CDN and cache behavior, asset naming and retention, HTML and API cache rules, service workers, dynamic imports, manifests, and rollback mechanics
- maximum tab, session, offline, cache, local-schema, API, and flag lifetimes; supported browsers, webviews, regions, and staged rollout duration
- critical journeys, unsaved work, authentication, tenant context, data migrations, failure budgets, monitoring, incident response, and user communication

## Safety and Permission Constraints

- A deployment is not atomic from the browser's perspective. Design for old HTML with new servers, new HTML with old or unavailable assets, old clients with new APIs, and simultaneous worker generations.
- Never solve version skew by unconditional refresh, destructive cache clearing, forced service-worker activation, or local-data deletion. Protect unsaved work and consequential operations first.
- Keep authentication and authorization server-enforced across the entire compatibility horizon. A feature flag, asset name, client version, or service worker is not an access-control boundary.
- Production cache purge, asset deletion, service-worker activation, API retirement, schema migration, flag change, rollback, or client blocking is R3 and requires immediate authorization, impact evidence, sequencing, monitoring, and a recovery path.

## Workflow

1. Draw every independently changing artifact and authority: HTML, immutable assets, runtime configuration, API, data schema, flags, service worker, browser storage, edge cache, and deployment region. Record owners and propagation delay.
2. Define a compatibility horizon from realistic tab, offline, cache, rollout, rollback, and client-update lifetimes. State which client and server versions must coexist and when support may end.
3. Give content-addressed assets immutable names and retain them through the compatibility and rollback horizon. Keep navigational HTML and mutable manifests revalidated so they can point to a coherent release.
4. Version APIs and semantics for supported clients. Prefer additive server evolution, tolerant readers, capability negotiation where justified, and server-side defaults; do not retire fields or behavior until usage and horizon evidence permit it.
5. Design service-worker install, waiting, activation, client control, cache namespaces, migration, and removal. Use immediate activation only when mixed old-page/new-worker behavior is proven safe.
6. Version browser schemas and make upgrades restartable and rollback-compatible. Coordinate flags, API behavior, and local migrations so a partial rollout cannot make stored data unreadable by the recovery release.
7. Detect release and asset mismatch without retry loops. For missing chunks or invalid manifests, preserve input, stop duplicate actions, attempt bounded recovery, and offer an accessible refresh or resume path only when safe.
8. Define rollout and rollback sequence, including artifact retention, cache invalidation, API compatibility, data migration, flag state, service-worker behavior, and regional propagation. Prefer roll-forward when rollback cannot read new state safely.
9. Observe release identifiers, asset and API failures, worker states, schema versions, refresh loops, recovery outcomes, and user impact without logging private payloads. Maintain kill switches and a tested support message.
10. Test every required old-client/new-server and new-client/old-server pair, long-lived tabs, offline return, multi-tab worker update, staged region, partial asset upload, chunk removal, cache purge, schema upgrade and downgrade, flag reversal, failed rollout, rollback, and interrupted critical action.

## Required Output

- artifact and version topology with cache, propagation, owner, and compatibility horizon
- client-server, worker-page, schema-code, flag-code, and asset-HTML compatibility matrix
- exact caching, retention, update, mismatch recovery, rollout, rollback, and user-communication design
- mixed-version test evidence, telemetry, stop conditions, residual risks, retirement criteria, and incident runbook

## Completion Gate

Do not call a client release safe until required version pairs pass critical journeys, referenced assets remain available for the full horizon, service-worker transitions avoid unsafe code mixing, local data survives upgrade and recovery, version mismatch cannot create refresh or retry loops, rollback is sequenced with server and data compatibility, and users with unsaved work retain control.

## Conditional Reference

Read [Web Client Release Compatibility Evidence](references/web-client-release-compatibility-evidence.md) before defining cache headers, asset retention, service-worker activation, or mixed-version support.
