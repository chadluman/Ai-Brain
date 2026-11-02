# Session and Cookie Evidence

Verified: 2026-10-21

## Standards and Security Guidance

- [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html) covers identifier properties, cookie attributes, lifecycle, renewal, expiration, logout, detection, and attack response.
- [RFC 6265: HTTP State Management Mechanism](https://www.rfc-editor.org/rfc/rfc6265.html) defines baseline cookie syntax and user-agent behavior. Modern browser attributes and defaults also require current browser and platform verification.
- [RFC 9700: OAuth 2.0 Security Best Current Practice](https://www.rfc-editor.org/rfc/rfc9700.html) updates the OAuth threat model, requires or recommends modern redirect, PKCE, CSRF, token, and sender constraints, and deprecates insecure patterns.
- [RFC 10017: OAuth 2.0 for Browser-Based Applications](https://www.rfc-editor.org/rfc/rfc10017.html) is current IETF guidance for browser application architectures and explicitly analyzes malicious JavaScript and token exposure.

## Decision Boundaries

- `Secure`, `HttpOnly`, and `SameSite` each address different threats; none makes a session safe alone.
- Browser storage gives origin scripts access. A compromised same-origin script can often act as the user even when an `HttpOnly` cookie prevents direct token extraction.
- A backend-for-frontend can reduce token exposure to browser JavaScript but creates a stateful security boundary that requires CSRF, session, scaling, and availability controls.
- OAuth authorizes access; identity claims and local application authorization still require issuer, audience, nonce, session, tenant, and policy validation.
