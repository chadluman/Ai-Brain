# Data Retention and Deletion Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [NIST SP 800-88 Rev. 2](https://csrc.nist.gov/pubs/sp/800/88/r2/final) is the final September 2025 media-sanitization guide, superseding Rev. 1. It addresses a sanitization program and rendering access to target data on media infeasible for a chosen effort level; it is not an application-record retention schedule.
- [NIST Privacy Framework 1.1 project](https://www.nist.gov/privacy-framework/new-projects/privacy-framework-version-11) still labels Version 1.1 an initial public draft and “coming soon” as of verification. Use final Privacy Framework 1.0 or the draft only with its status stated; do not present 1.1 as final.
- [European Commission GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en) includes purpose limitation, data minimization, and storage limitation. Applicability, lawful basis, exceptions, rights, and exact retention need qualified legal review.
- [UK ICO storage limitation guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-protection-principles/a-guide-to-the-data-protection-principles/storage-limitation/) distinguishes deletion, offline storage, anonymization, pseudonymization, backups, review, and justified retention. It is UK regulatory guidance, not a universal technical standard.
- [OWASP Logging Vocabulary](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Vocabulary_Cheat_Sheet.html) recommends recording sensitive deletion without copying the deleted contents into the log and disposing of retained copies according to policy. Use the broader audit-log design for integrity and access.
- [OWASP User Privacy Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/User_Privacy_Protection_Cheat_Sheet.html) supplies developer privacy protections and transparency principles. Some older references on that page require independent current verification.

## Decision Implications

- Product and legal policy decides what should be retained; engineering proves where copies exist and whether the rule executes. Neither discipline can substitute for the other.
- “Deleted” must name the layer: hidden from user, soft-deleted, inaccessible, anonymized, cryptographically erased, removed from active stores, expired from backup, or sanitized from media.
- Immutable backups can use bounded expiry plus restore-time re-deletion when immediate selective deletion is infeasible, but the residual window, access restrictions, and user statement must be explicit and qualified.
- Pseudonymized data is often still linkable; anonymization requires evidence that the applicable reidentification risk is acceptably low, not removal of one obvious identifier.
- Keep proof of process, not a shadow copy of the data: policy and job version, safe subject or object reference, target set, counts, time, hold decision, failures, retries, and final reconciliation.
