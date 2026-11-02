---
name: session-cookie-security
description: Design or review browser sessions, cookies, OAuth browser tokens, CSRF defenses, login state, rotation, logout, timeout, revocation, device and origin boundaries, and session monitoring. Use when a web application authenticates users or stores security-sensitive browser state.
---

# Session and Cookie Security

## Outcome

Create a browser-session design that minimizes credential exposure, binds state to the intended origin and transaction, rotates at privilege changes, survives realistic logout and recovery needs, and fails safely under script compromise or provider outage.

## Required Inputs

- authentication and federation flows, browser and client types, origins, domains, and redirects
- session sensitivity, privileges, duration, concurrent-device policy, recovery, and support needs
- server-side store, token format, cookie scope, CSRF model, API topology, and CORS needs
- third-party scripts, iframes, service workers, local storage, proxies, caches, logs, and analytics
- revocation, risk signals, audit, incident, accessibility, privacy, and regulatory constraints

## Safety and Permission Constraints

- Prefer opaque server-side session identifiers in cookies for same-origin web applications when they meet the architecture. Do not put bearer credentials in URLs or persistent browser storage by default.
- Assume malicious JavaScript in an origin has the privileges of legitimate application code. `HttpOnly` limits cookie reads but does not stop same-origin authenticated actions.
- Use narrow cookie domain and path scope, `Secure`, `HttpOnly` where script access is unnecessary, an intentional `SameSite` policy, and restrictive lifetime. Cookie `Path` is not an authorization boundary.
- Defend every state-changing browser request against CSRF according to the session and origin design; do not rely on one browser behavior without tests.
- Changing production identity flow, cookie domain, token storage, session invalidation, or OAuth redirect configuration is R3 and requires authorization, staged migration, active-session analysis, and rollback.

## Workflow

1. Threat-model theft, fixation, replay, CSRF, XSS, open redirect, login CSRF, session confusion, subdomain compromise, shared device, stale privilege, and support takeover.
2. Define the session authority, identifier entropy, server record, user and tenant binding, authentication strength, issued and last-active times, privilege version, device metadata, and revocation state.
3. Set exact cookie name, host or domain, path, `Secure`, `HttpOnly`, `SameSite`, expiry, prefix, and partition behavior from the deployment. Avoid broad parent-domain scope.
4. Rotate the session identifier after authentication, privilege elevation, recovery, password or MFA change, suspicious activity, and other trust changes. Prevent pre-authentication state from fixing the privileged session.
5. Define absolute, idle, and risk-based expiry. Make logout invalidate server state, expire the browser cookie, handle all devices according to policy, and revoke related refresh credentials where applicable.
6. Implement CSRF protection with same-site design, unpredictable tokens bound to the session or request, origin checks, and content-type or custom-header controls as appropriate. Test cross-site top-level, form, fetch, iframe, and redirect flows.
7. For OAuth or OpenID Connect, use current authorization-code guidance, PKCE, exact redirect matching, transaction-bound state or nonce, issuer validation, and minimal audience and scope. Avoid deprecated implicit and password flows.
8. Keep tokens, session IDs, authorization codes, and sensitive URLs out of logs, analytics, traces, referrers, browser history, error pages, and support exports.
9. Monitor anomalous creation, rotation, refresh, reuse, geographic or device shifts, privilege changes, CSRF failures, logout, and revocation without creating an unjustified tracking profile.
10. Test fixation, stolen and replayed cookie, expired state, clock skew, logout in multiple tabs and devices, subdomain collision, provider outage, account disablement, privilege downgrade, redirect attack, and active-session migration.

## Required Output

- session and browser threat model
- server-side record and lifecycle state machine
- exact cookie and browser-storage policy
- rotation, expiry, logout, revocation, recovery, and multi-device behavior
- CSRF, OAuth or OIDC, redirect, origin, CORS, and token controls
- logging, privacy, monitoring, incident, migration, and rollback plan
- adversarial browser and session test evidence

## Completion Gate

Do not call session handling ready until fixation and CSRF fail, logout and privilege changes invalidate authority as designed, credentials do not leak through browser or telemetry surfaces, and active-session migration plus provider failure have tested recovery paths.

## Conditional Reference

Read [Session and Cookie Evidence](references/session-cookie-evidence.md) when selecting cookie attributes, OAuth browser topology, token storage, or session lifecycle controls.
