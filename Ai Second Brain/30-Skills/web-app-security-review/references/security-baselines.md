# Web Security Baselines

Verified 2026-10-21. Recheck the stable versions and advisories before each material review.

## Source Roles

- [OWASP ASVS](https://asvs.owasp.org/) provides a testable set of technical security requirements for web applications and services. Version 5.0.0 was the stable release verified on 2026-10-21 and was published 2025-05-30.
- [ASVS downloads](https://asvs.owasp.org/downloads/) links the stable version, fixed release files, and canonical GitHub branches. Use the stable release rather than the changing default branch.
- [OWASP ASVS GitHub](https://github.com/OWASP/ASVS) is the canonical source repository. Its default branch can contain in-progress work.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) provides practical topic guidance. Its [ASVS index](https://cheatsheetseries.owasp.org/IndexASVS) maps cheat sheets to ASVS 5.0.x sections.
- [NIST SSDF 1.1, SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final) supplies high-level practices for preparing the organization, protecting software, producing well-secured software, and responding to vulnerabilities across the SDLC.
- [CISA Secure by Design](https://www.cisa.gov/securebydesign) supplies product-level secure-by-design and secure-by-default principles.

## Application Rules

- ASVS is the technical verification spine; choose and document applicable requirements rather than citing the whole standard vaguely.
- Cheat sheets explain implementation topics but do not replace a threat model or verification.
- NIST SSDF addresses lifecycle and organizational practice; it does not replace detailed application controls.
- CISA principles inform ownership and safe defaults; they are not a line-by-line test plan.
- Include the ASVS version in requirement identifiers because identifiers can change between releases.

