---
name: secrets-config-management
description: Design or review application configuration, secret inventory, workload credentials, storage, injection, rotation, revocation, detection, auditing, and emergency recovery across local, CI, staging, and production environments. Use when systems need credentials or environment-specific settings; never store secret values in the vault.
---

# Secrets and Configuration Management

## Outcome

Produce a configuration and credential lifecycle in which settings are validated, secrets are minimized and short-lived, access is attributable and least-privileged, rotation is rehearsed, and no secret values enter source control or this vault.

## Required Inputs

- configuration keys, secret names, consumers, purpose, owner, environment, and sensitivity
- identity capabilities of workloads, CI, developers, vendors, and target platforms
- rotation, revocation, expiry, availability, recovery, audit, residency, and compliance needs
- application startup and refresh behavior, deployment model, and incident procedures

Record metadata and approved storage locations only. Never request or retain actual secret values in project notes.

## Safety and Permission Constraints

- Prefer workload identity and short-lived scoped credentials over static shared secrets where the platform supports them.
- Keep local, test, staging, and production trust domains separate. Test data and credentials must not grant production access.
- Never commit secrets, build them into client bundles or container layers, print them, pass them in URLs, or expose them through source maps, crash reports, telemetry, shell history, plans, or caches.
- Encryption and Base64 encoding do not make a value safe to commit unless the full key, access, rotation, and recovery design is approved.
- Grant each consumer only the secret and operations it needs. Attribute access, alert on unusual retrieval, and make revocation observable.
- Creating, viewing, rotating, revoking, exporting, or recovering real credentials is R3 and requires immediate authorization and a tested dependent-system plan.

## Workflow

1. Classify every setting as public build-time, public runtime, confidential configuration, credential, or cryptographic key. Remove obsolete and duplicate values.
2. Define a typed configuration schema with required values, safe defaults, environment rules, startup validation, and redacted diagnostics.
3. For each secret, document name, purpose, owner, issuer, consumers, scope, lifetime, approved store, rotation method, revocation, and incident contact.
4. Replace static credentials with platform workload identity, federation, or dynamic credentials when the trust model and availability fit.
5. Choose secret storage based on access control, audit, availability, rotation, versioning, recovery, regions, integration, export, cost, and operational ownership.
6. Deliver secrets at runtime through the narrowest supported channel. Account for process inspection, environment inheritance, filesystem permissions, memory, debug endpoints, and child processes.
7. Design overlapping rotation where needed: introduce the new credential, update consumers, verify use, revoke the old credential, and test rollback. Distinguish encryption-key rotation from ordinary credential replacement.
8. Add preventive scanning and response for source, history, artifacts, images, logs, tickets, chat, and telemetry. Treat detection as an incident; deleting one visible copy is insufficient.
9. Protect break-glass access independently, restrict and monitor use, and test it without exposing the credential. Back up irreplaceable key material under separate controls.
10. Test startup with missing and invalid config, secret-store outage, expired and revoked credentials, rotation, recovery, redaction, and least-privilege denial.

## Required Output

- configuration schema and environment matrix
- secret metadata inventory without values
- workload-identity and storage decision with failure modes
- injection, refresh, rotation, revocation, audit, and detection design
- break-glass and key-recovery procedure
- negative and outage test evidence
- migration, rollback, ownership, and review triggers

## Completion Gate

Do not call the design complete until repositories and artifacts contain no known secret values, least privilege and redaction are tested, rotation succeeds in a safe environment, and store outage and recovery behavior are documented. Production changes remain separately authorized.

## Conditional Reference

Read [Secrets and Configuration Evidence](references/secrets-config-evidence.md) when selecting workload identity, storage, injection, lifecycle, or detection controls.
