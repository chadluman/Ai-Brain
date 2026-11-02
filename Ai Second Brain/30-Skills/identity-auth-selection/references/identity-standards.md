# Identity Standards

Verified 2026-10-21. Apply requirements to the exact profile, client type, and assurance context in use.

- [NIST SP 800-63B-4](https://csrc.nist.gov/pubs/sp/800/63/B/4/final), published July 2025, defines authentication and authenticator-management requirements across three assurance levels. Its government scope and normative language must be interpreted for the project's regulatory context rather than copied as universal product policy.
- [Web Authentication Level 3](https://www.w3.org/TR/webauthn-3/) is a W3C Recommendation dated 2026-08-25. It defines public-key credentials scoped to a relying party and browser-mediated authenticator access. Product recovery, account linking, device coverage, and user support remain application responsibilities.
- [OpenID Connect Core 1.0 with errata set 2](https://openid.net/specs/openid-connect-core-1_0.html) defines an identity layer over OAuth 2.0, including ID Tokens, claims, flows, validation, and security and privacy considerations.
- [OAuth 2.0 Security Best Current Practice, RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html), published January 2025, updates OAuth threat guidance and deprecates insecure modes. It requires controls appropriate to the selected client and flow; do not rely on older examples that conflict with this BCP.
- The [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) supplies implementation guidance that should be mapped to versioned ASVS requirements and the project's threat model.

## Protocol Boundary

OAuth is delegated authorization. OpenID Connect adds an authentication and identity layer. WebAuthn supplies a public-key authentication API. None of them independently designs application roles, resource authorization, tenant isolation, recovery policy, or identity proofing.
