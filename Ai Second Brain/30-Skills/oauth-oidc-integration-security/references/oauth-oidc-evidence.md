# OAuth and OpenID Connect Evidence

Verified: 2026-10-22

## Current Standards

- [RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html) is OAuth 2.0 Security Best Current Practice, published January 2025. It requires exact redirect matching except the defined native-loopback port case, requires public clients and recommends confidential clients use PKCE, discourages implicit issuance, requires mix-up defenses for multi-issuer clients, and recommends sender-constrained tokens where warranted.
- [RFC 10017](https://www.rfc-editor.org/rfc/rfc10017.html) is the August 2026 Best Current Practice for OAuth 2.0 browser-based applications. It replaces draft-era assumptions with a final threat and architecture baseline; use its browser token exposure and malicious-JavaScript analysis for SPAs and backend-for-frontend decisions.
- [OpenID Connect Core 1.0 incorporating errata set 2](https://openid.net/specs/openid-connect-core-1_0.html) is the approved identity layer used here. Its ID-token, issuer, audience, nonce, claims, UserInfo, and relying-party rules do not authorize application resources.
- [RFC 9126](https://www.rfc-editor.org/rfc/rfc9126.html) defines Pushed Authorization Requests. [RFC 9101](https://www.rfc-editor.org/rfc/rfc9101.html) defines JWT-Secured Authorization Requests. They can protect authorization-request integrity or confidentiality only when the authorization server and client implement the complete profile correctly.
- [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449.html) defines DPoP sender-constrained OAuth tokens. DPoP proves possession of a key; it is not client authentication or application authorization and still relies on TLS and correct proof, request, nonce, replay, and token-binding validation.
- [RFC 8705](https://www.rfc-editor.org/rfc/rfc8705.html) defines OAuth mutual-TLS client authentication and certificate-bound access tokens. It requires certificate lifecycle and end-to-end resource-server binding, not merely TLS at an unrelated proxy.
- [RFC 8693](https://www.rfc-editor.org/rfc/rfc8693.html) defines token exchange, including impersonation and delegation forms. The standard does not supply the deployment trust model; actor, subject, target, audience, scope, client authentication, revocation, and policy must be defined locally.
- [RFC 8252](https://www.rfc-editor.org/rfc/rfc8252.html) remains the native-application Best Current Practice: use an external user agent, claimed HTTPS or other permitted redirects, and PKCE rather than embedded credentials.

## Decision Implications

- Treat OAuth 2.1 as non-normative until it reaches the required publication status; current production guidance can rely on the finalized BCPs above without waiting for it.
- A backend-for-frontend can reduce browser token exposure but adds a session, CSRF, availability, scaling, and proxy trust boundary. It is not automatically safer for every client.
- PAR, JAR, DPoP, and mTLS address different threats. Add them only when issuer, client, resource server, key storage, reverse proxies, libraries, and operations support the full profile.
- Discovery and JWKS improve interoperability and rotation but expand remote trust. Anchor them to an exact issuer and safe network policy, cache deliberately, and test rollover and outage.
- Keep protocol conformance, user identity, local account linking, application session management, and application authorization as separate verification layers.
