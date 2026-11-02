# Audit Log Evidence

Verified: 2026-10-22

## Standards and Maintainer Sources

- [NIST SP 800-92](https://csrc.nist.gov/pubs/sp/800/92/final) is the final 2006 Guide to Computer Security Log Management. Its lifecycle and governance principles remain useful, but technology examples and some operational assumptions are old.
- [NIST SP 800-92 Revision 1 initial public draft](https://csrc.nist.gov/pubs/sp/800/92/r1/ipd) frames log management as generation, transmission, storage, access, disposal, and use for incidents and operations. It is a 2023 draft with a closed comment period, not a final replacement at verification.
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) includes the Audit and Accountability control family. NIST's page records Release 5.2.0 in August 2025; controls such as AU-3, AU-9, AU-11, and AU-12 inform content, protection, retention, and generation but require organization-specific tailoring.
- [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html) covers application security logging, event attributes, excluded data, injection defenses, verification, protection, monitoring, failure, and disposal. It distinguishes audit and transaction trails from general security logging.
- [OpenTelemetry Logs Data Model](https://opentelemetry.io/docs/specs/otel/logs/data-model/) defines a vendor-neutral representation for log records from multiple sources. It improves interoperability but does not decide which audit events, sensitive fields, integrity, retention, or access controls a product needs.

## Decision Implications

- Separate the semantic audit record from its transport and storage. A standard logging envelope cannot supply missing business action, resource, tenant, actor, authorization, outcome, or reason context.
- Protect confidentiality, integrity, availability, and accountability independently. Append-only behavior helps but does not prove the actor was legitimate or the event was correct.
- Audit logs often contain personal, security, commercial, and employee data. Purpose, reader access, export, retention, legal hold, and disposal need explicit governance.
- Logging infrastructure can fail or be attacked. Test full disks, unavailable collectors, malformed events, injection, clock drift, reader abuse, tampering, and restore rather than validating only the happy path.
- Use final standards as the baseline and label drafts as future-direction evidence. Recheck NIST SP 800-92 Revision 1 status before relying on it as final guidance.
