---
name: identity-auth-selection
description: Select and design user identity, authentication, sessions, federation, and recovery for a web or application project. Use when adding sign-in, passkeys, MFA, social or enterprise identity, or replacing an identity provider; pair with authorization design rather than treating login as access control.
---

# Identity and Authentication Selection

## Outcome

Produce a risk-based identity architecture that minimizes credential exposure, gives users safe enrollment and recovery, and preserves server-side authorization boundaries.

Read [identity standards](references/identity-standards.md) before choosing protocols, authenticators, assurance targets, or providers.

## Inputs

Identify user populations, account lifecycle, data and action sensitivity, abuse and takeover threats, regulatory or contractual requirements, workforce or customer identity, federation needs, platform and browser support, device sharing, accessibility, recovery and support capacity, tenant model, offline needs, regions, privacy, expected scale, budget, and migration constraints.

## Workflow

1. Separate identifiers, identity proofing, authentication, federation, delegated authorization, application sessions, and application authorization. Define which are actually needed.
2. Assign assurance and reauthentication requirements to risky journeys rather than forcing one control onto every action.
3. Compare managed and self-operated options on protocol conformance, authenticator support, recovery, account linking, tenant isolation, administrative access, security history, data processing, residency, accessibility, availability, export, cost, and incident response.
4. Prefer established protocols and reviewed libraries. For federated login, verify issuer, audience, redirect, state, nonce, PKCE, signature, key rotation, token lifetime, and logout behavior required by the selected standards and flow.
5. Design enrollment, verification, authenticator addition and removal, lost-device recovery, account linking, email or phone change, lockout, support escalation, and account deletion as security-critical flows.
6. Define server-managed session creation, rotation, expiration, revocation, cookie attributes, CSRF boundary, device display, and suspicious-session handling.
7. Enforce authorization from trusted server-side identity and resource context on every operation. Roles or claims from a client do not authorize access by themselves.
8. Test enumeration, credential stuffing, replay, fixation, cross-tenant access, recovery abuse, confused-deputy and redirect attacks, clock skew, key rotation, provider outage, accessibility, and rollback.

## Current Direction (2026)

- Treat passkeys as the primary login where platform and browser support allow, with a fallback authenticator and a recovery path designed alongside them — not added as an afterthought. Record which populations or devices cannot use passkeys and what they use instead.
- Treat OAuth 2.1 as the current direction for delegated authorization: PKCE mandatory, with the implicit and resource-owner-password flows removed. [Unverified: the final IETF status of OAuth 2.1 was unverified at the time of the 2026 research — confirm the current status before citing it as final.] See [OAuth and OpenID Connect Integration Security](../oauth-oidc-integration-security/SKILL.md) for the integration side.
- Keep access tokens short-lived: JWT access tokens with a 5–15 minute lifetime, paired with rotating refresh tokens stored in HttpOnly cookies rather than readable client storage. See [Session and Cookie Security](../session-cookie-security/SKILL.md) for the session side.

## Safety and Permission Boundaries

- Do not design custom password hashing, cryptographic protocols, token formats, or passkey verification when maintained standards-based implementations fit.
- Never store credentials, recovery codes, private keys, client secrets, session tokens, or real identity data in the vault, examples, logs, or analytics.
- Adding an identity SDK or provider is R2; creating accounts, configuring real credentials, migrating users, changing production login, or sending identity data is R3.
- Authentication proves control of an authenticator to a defined assurance; it does not prove every profile claim or authorize every resource.
- Recovery can be weaker than sign-in and therefore controls the real account-takeover boundary.

## Completion

Deliver the identity and trust-boundary map, assurance decisions, selected protocols and provider comparison, enrollment and recovery flows, session and authorization boundaries, privacy and retention, threat tests, monitoring and support plan, migration and rollback, ADR, and unresolved risks.
