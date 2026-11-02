---
name: web-app-security-review
description: Design or review web-application and API security using threat-informed, versioned requirements. Use for architecture reviews, security acceptance criteria, implementation findings, or release readiness; do not use as authorization for exploit testing, credential access, or production changes.
---

# Web Application Security Review

## Outcome

Produce a scoped security review that traces assets, threats, controls, findings, verification evidence, and residual risk to current authoritative requirements.

Read [security baselines](references/security-baselines.md) before choosing requirements or citing controls.

## Establish Context

- Identify assets, users, roles, trust boundaries, entry points, data flows, sensitive data, third parties, environments, and operational owners.
- Model plausible misuse and abuse, including business-logic failures, privilege changes, automation, fraud, denial of service, and dependency compromise.
- Define the reviewed version, environment, interfaces, and exclusions.
- Select project-appropriate ASVS 5.0.0 requirements and cite them with versioned identifiers such as `v5.0.0-1.2.5`.

## Review Areas

Cover only applicable controls, including:

- Encoding, sanitization, validation, parsing, and injection prevention
- Business rules, anti-automation, workflows, and race conditions
- Browser/frontend controls, cookies, origins, headers, and third-party scripts
- API contracts, rate limits, resource ownership, mass assignment, retries, and idempotency
- File upload, download, storage, transformation, and content handling
- Authentication, recovery, MFA, sessions, authorization, tenancy, and administrative access
- Tokens, OAuth/OIDC, cryptography, secrets, transport, configuration, and data protection
- Dependencies, build/release integrity, logging, error handling, monitoring, backup, and recovery

Integrate security into planning, development, review, release, and vulnerability response rather than treating it as a final scan.

## Evidence and Findings

For each control, record `pass`, `fail`, `not applicable`, or `not tested`, with evidence. For each finding include:

- Asset, threat, affected boundary, and reproducible evidence
- Versioned requirement or authoritative guidance
- Likelihood, impact, exploit prerequisites, and affected users/data
- Root cause, durable remediation, compensating controls, and owner
- Safe verification and regression steps
- Release disposition and accepted residual risk

Do not perform exploit testing, access credentials, exfiltrate data, change production, or exceed approved targets. Use synthetic data and isolated environments unless explicit authorization defines otherwise. Do not claim an application is "secure"; state the verified scope and remaining uncertainty.

## Completion

Deliver the threat summary, reviewed requirement set, prioritized findings, evidence, remediation plan, verification gaps, supply-chain concerns, and re-review triggers.

