# Privacy Evidence

Verified: 2026-10-21

## Standards and Authoritative Guidance

- [W3C Privacy Principles](https://www.w3.org/TR/privacy-principles/), a W3C Statement dated 2025-05-15, covers purpose limitation, minimization, transparency, meaningful consent and withdrawal, recognition, and accountability for web information flows.
- [NIST Privacy Framework 1.0](https://www.nist.gov/privacy-framework/privacy-framework) provides a voluntary enterprise privacy-risk structure. NIST Privacy Framework 1.1 was still an Initial Public Draft at verification, so do not cite it as final.
- [FTC Privacy and Security guidance](https://www.ftc.gov/business-guidance/privacy-security) emphasizes collecting only what is needed, protecting it, and disposing of it securely. It is United States regulatory guidance, not a global compliance checklist.
- [EU General Data Protection Regulation](https://eur-lex.europa.eu/eli/reg/2016/679/oj) is the official legal text for Regulation (EU) 2016/679. Applicability and interpretation require qualified legal review.
- [OWASP User Privacy Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/User_Privacy_Protection_Cheat_Sheet.html) supplies engineering mitigations for privacy and anonymity risks but does not establish legal compliance.

## Interpretation Boundaries

- Privacy is contextual and includes collection, inferences, recognition, manipulation, interruption, and flows toward people, not only confidentiality.
- De-identification claims require a threat model for linkage and auxiliary data. Hashing a stable identifier generally preserves linkability.
- A policy document cannot compensate for unnecessary collection or inaccessible controls. Verify actual data flows.
- Laws, regulatory interpretations, app-store rules, and vendor terms change; re-verify them for the product, users, and jurisdictions.
