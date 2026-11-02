---
name: domain-dns-tls-operations
description: Design or review domain registration, DNS, certificate issuance, HTTPS enforcement, email DNS, monitoring, renewal, transfer, and recovery. Use when a project will expose a public hostname, migrate traffic, configure certificates, or establish domain ownership controls.
---

# Domain, DNS, and TLS Operations

## Outcome

Create a recoverable domain and HTTPS control plan with explicit ownership, least privilege, automated certificate lifecycle, staged DNS changes, monitoring, and tested emergency access.

## Required Inputs

- registrable domains, hostnames, environments, regions, and public services
- registrar, registry, DNS, CDN, hosting, certificate authority, and email providers
- ownership, billing, administrative roles, recovery contacts, and organizational identity
- availability, migration, geographic, compliance, email, and security requirements
- current records, TTLs, DNSSEC, CAA, certificate, redirects, HSTS, and monitoring state

## Safety and Permission Constraints

- Domain registration, transfer, nameserver change, DNSSEC change, certificate issuance, production DNS edit, or HSTS preload is R3. Require immediate authorization, exact targets, a reviewed change set, and recovery steps.
- Use organization-owned accounts, phishing-resistant MFA where available, separate registrar and routine DNS roles, least privilege, audit logs, renewal controls, and tested recovery contacts.
- Never place secret values in the vault or DNS unless the protocol explicitly requires a public proof. Record the owner and approved secret store.
- Treat low TTLs as a migration tool, not permanent safety. Resolver caches, negative caching, propagation, DNSSEC state, and provider rollback behavior must be measured.
- Do not enable long-lived HSTS or preload until every required subdomain supports HTTPS and ownership, rollback consequences, and domain lifecycle are understood.

## Workflow

1. Inventory the registrable domain, subdomains, delegations, authoritative nameservers, record owners, certificates, email records, dependent services, and renewal dates.
2. Establish account ownership, role separation, hardware-backed recovery, registrar lock, billing continuity, change logging, and an out-of-band recovery runbook.
3. Keep DNS configuration reviewable and reproducible. Validate syntax, duplicate or conflicting records, environment boundaries, TTL intent, and provider-specific behavior before change.
4. Automate certificate issuance and renewal with narrowly scoped ACME credentials or delegated validation. Monitor expiration, renewal failures, unexpected issuance, and hostname coverage.
5. Use CAA when it improves issuance control and maintain it with the actual certificate-authority path. Monitor Certificate Transparency for unexpected certificates.
6. Enforce HTTPS with complete redirect, secure-cookie, mixed-content, protocol, cipher, and application-origin testing. Stage HSTS carefully and expand scope only after evidence.
7. Design DNS and origin cutovers with pre-change TTL planning, health verification, old-origin retention, reversible traffic shifts, and checks from multiple resolver and network viewpoints.
8. Document email-related records separately and coordinate with notification policy; avoid changing authentication or routing records as an incidental web deployment step.
9. Test issuance, automated renewal, failed challenge, certificate replacement, DNS provider outage, accidental record deletion, expired payment method, account recovery, transfer lock, and rollback.

## Required Output

- domain, delegation, record, certificate, and dependency inventory
- ownership, access, renewal, billing, and recovery controls
- DNS-as-reviewable-data and change procedure
- certificate automation, CAA, transparency, monitoring, and alert plan
- HTTPS, redirect, secure-cookie, HSTS, and mixed-content policy
- migration plan with TTL timeline, observable checks, rollback, and old-system retirement gate

## Completion Gate

Do not call domain operations ready until ownership and recovery are verified, certificate renewal has been exercised, production changes have explicit authorization and rollback, and monitoring covers domain expiry, DNS health, certificate expiry, renewal failure, and unexpected issuance.

## Conditional Reference

Read [Domain and Certificate Evidence](references/domain-certificate-evidence.md) when designing automated issuance, issuance restriction, transparency monitoring, HTTPS policy, or cutover procedures.
