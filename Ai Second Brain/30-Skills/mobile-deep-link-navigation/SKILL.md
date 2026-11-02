---
name: mobile-deep-link-navigation
description: Design or review secure mobile deep links, verified web-to-app links, navigation state restoration, OAuth redirects, and fallback behavior for iOS and Android. Use when URLs, notifications, QR codes, email, widgets, or external apps must open a specific native destination.
---

# Mobile Deep Link Navigation

## Outcome

Create one governed route contract that opens the correct app destination safely across installed, uninstalled, signed-out, stale, unauthorized, and version-skewed states.

## Required Inputs

- supported iOS and Android versions, application identifiers, signing identities, domains, and web fallback ownership
- route inventory, parameters, authentication requirements, authorization rules, and sensitive actions
- link sources such as web, email, push, QR, widgets, OAuth, password reset, invitations, and other apps
- install, first-run, account-switch, deleted-content, offline, and minimum-app-version behavior
- analytics and attribution needs, privacy constraints, redirectors, and third-party link services

## Safety and Permission Constraints

- Treat every incoming URL, intent, activity, notification payload, and route parameter as untrusted input. Parse with platform URL APIs, allow-list hosts and routes, validate types and lengths, and authorize the resolved resource server-side.
- Prefer platform-verified HTTPS associations for ordinary content links. Private custom schemes are not proof of app ownership and may be intercepted or ambiguously claimed.
- A link may select a destination, but it must not silently delete, transfer, purchase, disclose, or approve. Require normal confirmation and step-up controls for consequential actions.
- Do not put credentials, session tokens, personal data, or long-lived secrets in URLs. Query strings can leak through logs, analytics, screenshots, pasteboards, and intermediaries.
- OAuth for native apps must use a current reviewed profile, an external user-agent, exact redirect matching, state binding, and PKCE. Do not use embedded webviews for sign-in.
- Domain association, production OAuth registration, signing changes, provider configuration, and public-link deployment are R3 actions requiring immediate authorization and rollback steps.

## Workflow

1. Define a canonical route table with stable route names, URL forms, typed parameters, ownership, authentication and authorization requirements, supported app versions, and web fallbacks.
2. Separate URL parsing from navigation. Normalize once, reject ambiguous encodings and unexpected origins, then resolve a validated route object.
3. Configure and verify HTTPS app associations for every owned host and app identity. Keep association files narrowly scoped and served with the platform-required path, content, TLS, and redirect behavior.
4. Define startup and warm-app handling through one router. Restore or preserve navigation state deliberately and prevent duplicate handling when lifecycle callbacks repeat.
5. Resolve authentication without losing intent: store a short-lived, bounded pending route, complete sign-in or account selection, re-authorize, then continue only if still valid.
6. Define missing, deleted, moved, unauthorized, incompatible, or offline destinations and a useful fallback. Do not reveal resource existence through differing unauthorized errors.
7. Isolate OAuth callbacks, password resets, invitations, payments, and other security-sensitive routes from general content navigation. Apply protocol-specific replay, expiry, and one-time-use controls.
8. Avoid third-party redirectors unless their data collection, domain control, availability, pricing, deprecation, and exit path have passed service review.
9. Test verified association and routing on physical devices for fresh install, no install, cold start, warm state, signed out, wrong account, revoked access, old app version, offline, malformed input, duplicate delivery, and web fallback.
10. Monitor association-file reachability, route failures, unsupported versions, and fallback rates without recording sensitive URL data.

## Required Output

- canonical route and parameter contract
- verified-domain, app-identity, signing, and association-file matrix
- parsing, validation, authentication, authorization, and navigation flow
- fallback, account-switch, version-skew, and state-restoration behavior
- OAuth and other sensitive-callback controls where applicable
- device and web-fallback test evidence
- monitoring, rollback, domain migration, and provider-exit plan

## Completion Gate

Do not call deep links ready until both platform associations are verified on representative physical devices and adversarial route tests show that malformed, duplicated, expired, unauthorized, and wrong-account links cannot bypass normal controls.

## Conditional Reference

Read [Mobile Deep Link Evidence](references/mobile-deep-link-evidence.md) before choosing link types or OAuth redirect behavior. Use [Information Architecture and Routing](../information-architecture-routing/SKILL.md) for the shared URL and navigation taxonomy.
