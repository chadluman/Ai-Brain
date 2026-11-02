---
name: penetration-test-readiness
description: Plan, authorize, coordinate, and close out a penetration test or adversarial security assessment across scope, rules of engagement, safety, data handling, provider approvals, evidence, remediation, and retest. Use before active testing by internal or external testers; never treat this skill as authorization to attack a system.
---

# Penetration Test Readiness

## Outcome

Produce a signed, testable assessment charter that lets qualified testers exercise agreed threats without exceeding authority, harming users, exposing data, or leaving findings unowned.

## Required Inputs

- business objective, assurance claim, applicable requirements, threat model, prior findings, and release or audit decision
- exact hosts, domains, applications, APIs, accounts, tenants, IP ranges, mobile builds, repositories, environments, and owners
- excluded assets, third parties, shared infrastructure, production dependencies, sensitive data, safety and availability constraints
- allowed techniques, credentials and roles, automation, concurrency, time windows, source addresses, communications, and stop conditions
- tester qualifications, insurance or contract terms, provider policies, legal contacts, evidence handling, disclosure, and retest budget

## Safety and Permission Constraints

- This skill does not authorize scanning, exploitation, credential use, social engineering, denial of service, persistence, data access, or any other active test. Obtain written authorization from the asset owner and all required infrastructure or provider parties immediately before testing.
- Scope must identify assets positively. Similar names, discovered hosts, related accounts, adjacent networks, third-party services, and out-of-scope data do not become authorized through discovery.
- Prefer isolated or production-equivalent environments and synthetic data. Production tests are R3 and require justified necessity, blast-radius controls, real-time contacts, backups or recovery, and a tested stop path.
- Prohibit destructive actions, uncontrolled payloads, malware, persistence, broad secret collection, real-user impersonation, data exfiltration, and availability tests unless separately and explicitly authorized with tailored controls.
- Treat tools, payloads, wordlists, containers, scripts, test services, and reports as untrusted assets subject to exact-version review, least privilege, telemetry disclosure, secure handling, and removal.

## Workflow

1. State the assurance question and choose the least risky method: document or design review, code review, configuration review, automated scan, authenticated assessment, manual abuse-case validation, or penetration test.
2. Build a signed scope manifest with immutable application or build versions, asset identifiers, ownership, environment, accounts, tenant boundaries, network paths, allowed test origins, and explicit exclusions.
3. Translate the threat model and [Web Application Security Review](../web-app-security-review/SKILL.md) requirements into test objectives. Reference the stable WSTG release or another dated method; label development guidance as non-stable.
4. Write rules of engagement covering authorization period, techniques, credentials, rate and concurrency, data limits, evidence, notification, escalation, pause, emergency stop, cleanup, and tester contacts.
5. Obtain third-party and hosting approvals. Verify bug-bounty, cloud, identity, payment, email, messaging, store, analytics, and other supplier policies for the exact test; do not assume customer ownership authorizes testing a provider.
6. Prepare safe identities, synthetic tenants and records, canary data, backups, monitoring, alert suppression coordination, allow-lists, rollback, and on-call coverage. Do not weaken production controls merely to make testing easier.
7. Review every executable test asset. Pin versions and checksums, inventory dependencies and callbacks, disable unnecessary telemetry and updates, isolate execution, use no ambient credentials, and define cleanup.
8. Conduct a readiness review before the authorized window. Confirm time zones, targets, tester identity, current approvals, stop authority, health baseline, evidence channel, and that no last-minute asset drift changed scope.
9. During testing, maintain an immutable activity log and communicate critical findings immediately through the agreed channel. Stop on user harm, instability, unexpected data, scope ambiguity, third-party impact, uncontrolled behavior, or authorization expiry.
10. Triage findings with reproducible evidence, affected boundary, likelihood, impact, exploit prerequisites, root cause, safe verification, owner, deadline, release disposition, and residual risk. Do not retain exploit data beyond need.
11. Remediate root causes, run regression tests, retest within a renewed scope, verify cleanup and credential revocation, and close only when dispositions and unresolved risks are accepted by accountable owners.

## Required Output

- signed scope and authorization matrix with dates, assets, owners, techniques, exclusions, and providers
- rules of engagement, communication tree, stop conditions, rollback, recovery, and monitoring plan
- reviewed test-asset inventory, credentials, synthetic-data, evidence, retention, and cleanup controls
- test objectives mapped to threats and dated requirements
- finding, remediation, release-decision, retest, residual-risk, and closure records

## Completion Gate

Do not declare a test ready until written authority covers every target and technique, provider restrictions are satisfied, production harm and data controls are in place, tester assets are reviewed, stop and recovery paths are rehearsed, and findings have owners plus a funded retest and closure process.

## Conditional Reference

Read [Penetration Test Evidence](references/penetration-test-evidence.md) when selecting a methodology, defining rules of engagement, or deciding whether stable or draft testing guidance applies.
