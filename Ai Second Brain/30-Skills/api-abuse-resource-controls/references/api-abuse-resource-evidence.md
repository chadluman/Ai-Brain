# API Abuse and Resource Evidence

Verified: 2026-10-22

## Primary Sources

- [OWASP API Security Top 10 2023](https://api-security.owasp.org/editions/2023/en/0x11-t10/) includes unrestricted resource consumption, unrestricted access to sensitive business flows, authorization failures, inventory gaps, SSRF, and unsafe dependency consumption. It is an awareness list, not a complete control set.
- [OWASP API4:2023](https://api-security.owasp.org/editions/2023/en/0xa4-unrestricted-resource-consumption/) identifies time, memory, processes, file descriptors, upload size, batch operations, records per page, and paid provider calls as resource dimensions. A request-per-second limit covers only part of this surface.
- [OWASP Automated Threats to Web Applications](https://owasp.org/projects/automated-threats-to-web-applications) provides vocabulary for credential, account, scraping, scalping, carding, spam, and other automation-driven business harms. Use it as a threat catalog and verify current project status.
- [RFC 6585](https://www.rfc-editor.org/info/rfc6585/) defines `429 Too Many Requests` and optional `Retry-After` without specifying identity or counting semantics. It also notes that responding to every abusive request can itself consume resources.
- [IETF RateLimit header fields draft](https://datatracker.ietf.org/doc/draft-ietf-httpapi-ratelimit-headers/) was revision 11 in May 2026 and remained an Internet-Draft at verification. Its fields, security, privacy, and interoperability behavior can change before an RFC.

## Decision Implications

- Protect resources, not only request counts. Model amplification and paid side effects explicitly.
- Use multiple identity and behavioral dimensions with privacy and false-positive controls; IP-only enforcement is brittle.
- Enforce authorization and business invariants regardless of rate-limit state.
- Treat quota headers as hints, not grants. Clients must tolerate absence and changes; servers should avoid disclosing exploitable capacity detail.
- Test fail-open and fail-closed behavior of the counter store, gateways, application enforcement, and downstream provider limits under real concurrency.
