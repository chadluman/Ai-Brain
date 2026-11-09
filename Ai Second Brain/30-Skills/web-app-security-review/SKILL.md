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

## 2026 Currency: OWASP Top 10 2025 and Scanning Layers

Cite the OWASP Top 10:2025 edition when framing findings, and record the edition used. Two placements reported from that edition shape review priorities: supply-chain failures at #3 and exceptional conditions at #10. The exact ordering of the middle items was not checked against the primary source for this refresh, so cite only the placements recorded here and re-check the list before citing others.
- Layer scanning so each layer catches what the others miss, in order: secrets scanning, software composition analysis (SCA) for known dependency vulnerabilities, static analysis (SAST) for code-level flaws, and dynamic analysis (DAST) for running-application behaviour. A pass at one layer is not evidence for the others.
- Pin build and pipeline dependencies by content hash (SHA-pinning), not by mutable tag, after the March 2026 tag-rewriting attack reported against Trivy images showed a tag can point at different content over time. Apply the same rule to workflow actions and container images; see [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) and [Software Supply Chain Review](../software-supply-chain-review/SKILL.md).

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

