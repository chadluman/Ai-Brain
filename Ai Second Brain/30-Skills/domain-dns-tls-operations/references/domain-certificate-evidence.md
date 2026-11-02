# Domain and Certificate Evidence

Verified: 2026-10-21

## Standards and Security Guidance

- [ACME, RFC 8555](https://www.rfc-editor.org/rfc/rfc8555.html) standardizes automated certificate-management interactions, including account, order, authorization, challenge, finalization, issuance, and revocation behavior.
- [CAA, RFC 8659](https://www.rfc-editor.org/rfc/rfc8659.html) defines DNS records that identify certificate authorities authorized to issue for a domain. It narrows issuance policy but does not prevent every account, DNS, CA, or application compromise.
- [Certificate Transparency v2, RFC 9162](https://www.rfc-editor.org/rfc/rfc9162.html) defines public logging and audit of certificate issuance. It supports detection and accountability rather than blocking issuance by itself.
- [OWASP Transport Layer Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html) provides application-facing HTTPS, protocol, certificate, and deployment guidance. Exact platform configuration must follow the current server and provider documentation.
- [OWASP HTTP Strict Transport Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html) explains HSTS behavior and deployment risk, including the effect of `includeSubDomains` and preload.

## Decision Boundaries

- ACME automation removes manual renewal work only when challenge credentials, renewal jobs, failure alerts, account recovery, and replacement are all operated correctly.
- CAA changes can break expected issuance when the actual CA chain or delegated service is not understood. Test before enforcing during a migration.
- Transparency logs may expose hostnames. Avoid unnecessary sensitive names in public certificates and monitor for unexpected issuance.
- A DNS provider, registrar, CDN, hosting provider, and certificate authority may be the same vendor but remain distinct failure and permission domains.
- HTTPS at the edge does not prove encrypted, authenticated, or correctly routed traffic from the edge to the application origin.
