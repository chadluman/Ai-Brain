---
name: information-architecture-routing
description: Design or review site structure, navigation, route hierarchy, URL policy, redirects, page identity, wayfinding, and deep-link behavior. Use when organizing a website or application, changing routes, merging content, or diagnosing findability and orientation problems.
---

# Information Architecture and Routing

## Outcome

Create a task-centered, accessible information architecture with durable resource identifiers, predictable navigation, explicit route ownership, and a tested redirect and retirement strategy.

## Required Inputs

- users, critical tasks, content and records, mental models, terminology, and search behavior
- public, authenticated, administrative, locale, tenant, and deep-link surfaces
- current routes, inbound links, bookmarks, indexed URLs, analytics, support evidence, and redirects
- rendering, authorization, cache, SEO, localization, offline, and application-state constraints
- ownership, content lifecycle, migration, retention, and backwards-compatibility requirements

## Safety and Permission Constraints

- Never place secrets, credentials, session identifiers, personal data, or sensitive internal state in a path, query, fragment, page title, referrer, or analytics label.
- Navigation visibility is not authorization. Enforce permission on every resource and prevent leaks through titles, counts, breadcrumbs, search, prefetch, cache, and error differences.
- Redirect destinations derived from input require allow-lists or safe relative resolution. Prevent open redirects, credential forwarding, method changes, and cross-origin leakage.
- Production route deletion, mass redirect, canonical change, domain cutover, or indexed URL migration is R3 and requires authorization, crawl and dependency evidence, rollback, and monitoring.

## Workflow

1. Map user tasks and content relationships independently of the current menu, team structure, database, or favored framework.
2. Inventory every route and state: purpose, audience, owner, identifier, canonical URL, method, render mode, auth, cache, indexability, locale, and lifecycle.
3. Define a shallow task-centered hierarchy with stable labels. Test grouping, naming, findability, and orientation with representative users, including assistive-technology users.
4. Provide multiple appropriate find paths: global and local navigation, contextual links, breadcrumbs, search, sitemap, recent or saved items, and direct deep links.
5. Give durable resources stable opaque or meaningful identifiers as the domain requires. Keep presentation, temporary state, and sensitive values out of canonical URLs.
6. Define query parameters for shareable filters and views, fragments for document-local navigation, and client state only when it does not need durable linking, recovery, or server interpretation.
7. Specify trailing slash, case, encoding, locale, pagination, sort, filter, tenant, version, and canonical policies. Normalize one way and test browser history, refresh, back, forward, and new-tab behavior.
8. Plan route change as a data migration: map old to new, choose status and method semantics, preserve query data safely, update internal links and sitemaps, retain redirects, and monitor unresolved traffic.
9. Test keyboard and screen-reader navigation, focus after route change, zoom, small viewport, no JavaScript, expired session, unauthorized deep link, missing record, stale bookmark, locale switch, and offline recovery.

## Required Output

- task and content model
- route inventory with ownership, identity, auth, cache, index, locale, and lifecycle
- navigation, label, breadcrumb, search, and page-structure design
- URL, query, fragment, canonical, and browser-history policy
- old-to-new redirect map with method and status rationale
- accessibility, authorization, analytics, crawl, and migration tests
- monitoring, rollback, retirement, and broken-link ownership

## Completion Gate

Do not call routing ready until representative users can find and identify critical destinations, every protected deep link enforces authorization, URLs contain no sensitive state, browser navigation is correct, and changed routes have verified redirects plus rollback.

## Conditional Reference

Read [Information Architecture Evidence](references/information-architecture-evidence.md) when defining navigation, page structure, URL identity, or redirects.
