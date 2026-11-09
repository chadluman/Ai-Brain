---
name: oauth-oidc-integration-security
description: Design or review secure OAuth 2.0 and OpenID Connect integrations for browser, native, server, device, and service clients. Use when implementing authorization code flows, federated login, delegated API access, token validation, logout, or provider migration after identity architecture is selected.
---

# OAuth and OpenID Connect Integration Security

## Outcome

Produce an exact client, authorization-server, resource-server, and session design that uses current protocol profiles, validates every trust decision, limits token exposure, survives key and provider changes, and has negative-test evidence.

Use [Identity and Authentication Selection](../identity-auth-selection/SKILL.md) to choose the identity architecture, [Session and Cookie Security](../session-cookie-security/SKILL.md) for application sessions, and [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md) for resource decisions. This skill owns protocol integration rather than provider selection or application authorization.

## Required Inputs

- client type and execution boundary: browser, backend-for-frontend, native app, confidential server, device, CLI, or workload
- exact issuer, discovery and metadata source, authorization and token endpoints, supported profiles, redirect origins, resource servers, and audiences
- login, account-linking, delegated-access, consent, logout, reauthentication, and cross-device journeys
- token formats, lifetimes, storage and transport locations, sender constraints, scopes, claims, key rotation, revocation, and outage expectations
- browser, mobile, tenant, privacy, accessibility, provider, migration, and operational constraints

## Safety and Permission Constraints

- OAuth delegated authorization is not authentication unless an applicable OpenID Connect profile is used correctly. An ID token is not an API access token, and neither replaces application authorization.
- Use maintained, reviewed protocol libraries. Do not create custom token formats, signature validation, discovery, PKCE, DPoP, mTLS, or logout protocols.
- Never place client secrets in public clients, access or refresh tokens in URLs, or real tokens, keys, claims, or user identity data in the vault, logs, analytics, error pages, or examples.
- Treat provider metadata, discovery, dynamic registration, JWKS, claims, and logout URLs as trust inputs. Pin allowed issuers and redirect destinations; do not follow arbitrary endpoints or accept algorithm or key choices from an untrusted token.
- Adding a library or provider is R2. Registering a real client, configuring production redirects or credentials, changing sign-in, linking or migrating users, or transmitting real identity data is R3 and requires immediate authorization and rollback.

## Workflow

1. Draw the actors, browser or app, client components, authorization server, resource servers, session store, token paths, trust anchors, and front- versus back-channel communication. State which component can safely hold which credential.
2. Select the current standards profile for the exact client. For browser-based clients, start from RFC 10017; for native apps, use RFC 8252; apply RFC 9700 across deployments. Prefer authorization code with PKCE and avoid implicit and resource-owner-password flows.
3. Register exact redirect URIs and allowed origins. Prevent open redirects, bind the transaction with PKCE and the applicable `state`, `nonce`, and issuer checks, and define safe app-link or loopback behavior for native clients.
4. Obtain endpoints and capabilities from an authenticated, allow-listed issuer configuration. Validate issuer continuity and protect discovery from SSRF, mix-up, tenant confusion, and endpoint substitution.
5. Define token validation separately for each token type and receiver: signature and allowed algorithm, issuer, audience or resource, client, expiry and not-before with bounded skew, nonce, authorization context, sender constraint, and required claims. Reject ambiguous or missing critical values.
6. Minimize scopes, claims, audiences, lifetime, and downstream propagation. Decide whether a backend-for-frontend, PAR, JAR, mTLS, DPoP, token exchange, refresh-token rotation, or sender-constrained access is justified by the threat model and supported end to end.
7. Keep provider tokens at the narrowest trusted boundary. Convert successful authentication into a separately protected application session where appropriate; define refresh, rotation, revocation, logout, compromise response, and behavior when the authorization server or JWKS endpoint is unavailable.
8. Design account linking and multi-issuer identity keys explicitly. Do not merge accounts solely on an unverified or mutable email address; require proof appropriate to the takeover risk and record reversible decisions.
9. Test malicious redirect inputs, transaction replay, code injection, mix-up, issuer and audience confusion, algorithm and key substitution, expired or future tokens, wrong token type, scope escalation, stolen refresh tokens, DPoP or mTLS mismatch, key rotation, provider outage, logout gaps, and tenant crossing.
10. Rehearse migration and rollback without losing local account identity, authorization, audit continuity, recovery routes, or the ability to revoke old credentials.

## Current Direction (2026)

This section names the current direction; the workflow steps above remain the operative detail.

- Treat OAuth 2.1 as the current direction for new integrations: PKCE mandatory, with the implicit and resource-owner-password flows removed. [Unverified: its final IETF status was unverified at the time of the 2026 research — confirm the current status before citing it as final.] Keep this skill's RFC 9700, RFC 8252, and RFC 10017 profile guidance as the operative detail until that status is confirmed.
- Where a browser client holds tokens, prefer short-lived access tokens (5–15 minutes) with rotating refresh tokens held in HttpOnly cookies through a backend-for-frontend, rather than tokens in readable browser storage. See [Session and Cookie Security](../session-cookie-security/SKILL.md) for the session side.
- Passkeys as the primary login is an identity-architecture decision owned by [Identity and Authentication Selection](../identity-auth-selection/SKILL.md). This skill covers the federated and OIDC side once that decision is made — including how the federated login result is converted into the application session in step 7.

## Required Output

- actor, token, key, redirect, session, and trust-boundary map
- selected standards profile and explicit rejected flows
- client registration, issuer and endpoint trust, validation, storage, scope, claim, audience, sender-constraint, refresh, logout, and outage rules
- account-linking, provider migration, compromise, rollback, monitoring, and ownership plan
- conformance and adversarial test matrix with expected rejection behavior and captured evidence
- exact standards, library and provider versions, assumptions, residual risks, and re-review triggers

## Completion Gate

Do not call the integration ready until every client and token type has an explicit receiver and validation contract, redirects and issuers are allow-listed, browser or device exposure is bounded, key rotation and provider outage are tested, all negative cases fail safely, application authorization remains independent, and production changes have separate authorization.

## Conditional Reference

Read [OAuth and OpenID Connect Evidence](references/oauth-oidc-evidence.md) when selecting a client profile, deciding browser token architecture, or interpreting current OAuth, OpenID Connect, PAR, JAR, DPoP, mTLS, or token-exchange guidance.
