---
name: audit-log-design
description: Design or review application audit records for sensitive business, security, administrative, data, and financial actions with attribution, integrity, access, retention, and verification controls. Use when a system must reconstruct who did what to which resource and why; do not use it as a general debug-logging or observability guide.
---

# Audit Log Design

## Outcome

Produce a minimal, queryable, tamper-evident audit trail that reconstructs consequential actions across users, staff, services, tenants, and providers without becoming a secret or personal-data dump.

## Required Inputs

- decisions the audit trail must support: security review, user support, financial control, access review, incident response, dispute, change management, or qualified compliance
- sensitive actions, resources, state transitions, identities, tenants, services, providers, and administrative pathways
- trust boundaries, identity and authorization evidence, clocks, offline clients, queues, retries, correlation, and failure behavior
- readers, approvers, investigators, exporters, retention, legal hold, deletion, residency, privacy, volume, latency, and cost
- existing operational logs, traces, analytics, ledgers, database history, provider logs, and evidence gaps

## Safety and Permission Constraints

- Keep audit records distinct from debug logs, observability telemetry, analytics, and financial ledgers. Link them with stable identifiers; do not copy entire payloads between systems.
- Never record passwords, private keys, session or access tokens, full authentication codes, payment credentials, unnecessary request or response bodies, or sensitive personal content. Record references, classifications, bounded before-and-after fields, and approved redactions.
- An audit record is evidence from a source with known trust and limitations, not automatic proof of identity, intent, non-repudiation, legality, or correctness.
- Audit access is itself sensitive. Enforce least privilege, purpose, approval where warranted, export limits, watermarking or traceability as appropriate, and auditing of reads, searches, exports, retention changes, and deletion.
- Enabling production capture, exporting real audit data, changing retention, placing legal holds, connecting a hosted log service, or correcting historical evidence is R3 and requires authorization, privacy and qualified review, cost bounds, and recovery.

## Workflow

1. Define audit questions and threat model before events. Identify which decisions need reconstruction, expected users, evidence sensitivity, adversaries, retention, latency, and acceptable loss.
2. Select consequential events: authentication and recovery, authorization and policy changes, privileged access, impersonation, user and tenant administration, configuration and feature changes, secret or key lifecycle references, data view or export where material, financial actions, moderation, support, consent, and audit-system changes.
3. Define a versioned event contract with event ID, schema version, action, resource type and stable ID, tenant, actor type and stable ID, effective subject, authentication and authorization context, source service and version, request or job correlation, occurred and recorded times, outcome, reason, approved bounded changes, and confidence or provenance.
4. Emit at the trusted decision or effect boundary. Distinguish requested, authorized, attempted, succeeded, failed, reversed, and reconciled states; do not infer success from a client event or an accepted asynchronous request.
5. Make retries idempotent and ordering explicit. Preserve original event IDs and causal links across queues, providers, offline clients, compensations, imports, and migrations while documenting clock confidence and time-zone normalization.
6. Protect integrity and availability with append-oriented storage, restrictive writer identities, independent administration, encryption, secure transport, access monitoring, backups, tamper detection, retention controls, and tested capacity limits. Choose stronger immutability only when the risk and operations justify it.
7. Design failure behavior per event. Logging failure must not leak data or create an uncontrolled denial of service; for narrowly defined high-impact actions, decide whether to fail closed, queue locally, or stop the workflow and how operators recover.
8. Provide scoped searches and exports by tenant, actor, resource, action, outcome, and time. Redact by role, preserve stable pagination and time semantics, bound queries, and prevent cross-tenant inference.
9. Define retention, legal hold, correction, deletion, and archive by purpose and jurisdiction. Never silently edit a record; link an explanatory correction or mark a proven ingestion defect through an authorized process.
10. Test missing identity, forged actor fields, log injection, newline and delimiter payloads, duplicate and out-of-order events, clock skew, queue loss, storage full, writer compromise, reader overreach, tampering, backup restore, schema evolution, tenant isolation, retention expiry, and export completeness.

## Required Output

- audit purposes, threat model, event inventory, owners, and excluded data
- versioned event contract with trust, attribution, correlation, time, result, and reason semantics
- emission, idempotency, ordering, storage, integrity, access, retention, and failure design
- query, export, correction, legal-hold, deletion, migration, and recovery procedures
- privacy, tenant-isolation, cost, capacity, monitoring, and incident controls
- negative and recovery test evidence plus unresolved qualified-review questions

## Completion Gate

Do not call the audit trail ready until every required action is emitted at an authoritative boundary, sensitive data is excluded by tests, actor and tenant context cannot be forged by the client, access and export are themselves audited, tampering and loss are observable, retention is purpose-bound, and restore and schema-evolution exercises preserve reconstruction.

## Conditional Reference

Read [Audit Log Evidence](references/audit-log-evidence.md) when defining event fields, log-management lifecycle, integrity controls, or interoperable representation.
