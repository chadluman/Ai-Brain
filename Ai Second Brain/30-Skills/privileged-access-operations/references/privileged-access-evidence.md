# Privileged Access Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [CISA Identity and Access Management Recommended Best Practices for Administrators](https://www.cisa.gov/sites/default/files/2023-12/ESF%20IDENTITY%20AND%20ACCESS%20MANAGEMENT%20RECOMMENDED%20BEST%20PRACTICES%20FOR%20ADMINISTRATORS%20PP-23-0248_508C.pdf) recommends phishing-resistant authentication for privileged roles, separate user and administrative accounts, and privileged-access management with auditing.
- [NIST SP 800-53 Rev. 5 Update 1](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) provides a control catalog for account management, least privilege, separation of duties, privileged functions, remote access, authentication, audit, incident response, and contingency. Select and tailor controls to the system; citation is not certification.
- [NIST SP 800-207](https://csrc.nist.gov/pubs/sp/800/207/final) rejects implicit trust based on network location or asset ownership and makes access a resource-focused authentication and authorization decision.
- [NIST SP 1800-35](https://csrc.nist.gov/pubs/sp/1800/35/final) is a June 2025 final practice guide for implementing zero trust. Its example products and architectures are reference implementations, not automatically approved dependencies or a universal stack.
- [NIST SP 800-63B-4](https://pages.nist.gov/800-63-4/sp800-63b.html) supplies current authenticator, lifecycle, reauthentication, phishing resistance, session, and recovery guidance. Target assurance and applicability remain project decisions.
- [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) emphasizes deny by default, least privilege, per-request validation, relationship and attribute-aware policy, and authorization tests. Administrative identity does not permit every resource or tenant operation.
- [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html) covers security event attributes, protection, monitoring, and exclusion of secrets and sensitive data. Privileged session recording needs the same minimization and access controls.

## Decision Implications

- Privilege is an action and resource property, not only a role name. Inventory alternate consoles, local accounts, API keys, scripts, CI identities, and vendor channels.
- Just-in-time access reduces standing exposure only when eligibility, approval, duration, propagation, expiry, and provider-side revocation are enforced and reconciled.
- Strong authentication cannot compensate for excessive scope, unsafe impersonation, shared accounts, missing authorization, or unaudited emergency paths.
- Full command or screen recording can collect secrets and personal data. Prefer structured action evidence where it provides sufficient accountability; restrict and retain richer recordings by defined need.
- Break-glass is a designed degraded mode. It needs independent custody, minimal capability, detection, tested availability, rapid expiry or rotation, and mandatory after-action review.
