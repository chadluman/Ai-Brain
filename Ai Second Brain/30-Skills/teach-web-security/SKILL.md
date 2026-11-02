---
name: teach-web-security
description: Teach defensive web security through threat modeling, identity, authorization, sessions, browser controls, secrets, dependency risk, and secure failure analysis. Use for security modules, code review practice, defensive labs, or integrating security into a web curriculum.
---

# Teach Web Security

## Outcome

Help the learner reason about assets, trust boundaries, attacker goals, control placement, verification, and recovery without turning instruction into unauthorized testing.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

- [Application Threat Modeling](../application-threat-modeling/SKILL.md) to frame assets, actors, trust boundaries, misuse, controls, and residual risk.
- [Web Application Security Review](../web-app-security-review/SKILL.md) for requirements-led architecture and implementation review.
- [Identity and Authentication Selection](../identity-auth-selection/SKILL.md), [OAuth and OpenID Connect Integration Security](../oauth-oidc-integration-security/SKILL.md), and [Session and Cookie Security](../session-cookie-security/SKILL.md) for sign-in and session flows.
- [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md) for permission and isolation enforcement.
- [Browser Security Policy](../browser-security-policy/SKILL.md) and [Secrets and Configuration Management](../secrets-config-management/SKILL.md) for browser and credential boundaries.
- [Software Supply Chain Review](../software-supply-chain-review/SKILL.md), [Vulnerability Management Operations](../vulnerability-management-operations/SKILL.md), or [Penetration Test Readiness](../penetration-test-readiness/SKILL.md) only when the exercise reaches those scopes.

## Teaching Priorities

Begin with a small data-flow and threat model. Trace each control to a named threat and verification method. Teach prevention, detection, response, and recovery together, including user harm and false positives.

Use isolated, intentionally vulnerable local examples with dummy data when an exploit demonstration is necessary. Prefer defensive tests that prove rejection, isolation, revocation, auditability, and safe failure. Discuss secure defaults and the consequence of bypasses or operational mistakes.

For senior-level practice, require control ownership, abuse cases, least privilege, tenant-negative tests, incident implications, and residual-risk communication.

## Boundaries

- Security teaching does not authorize scanning, exploitation, credential use, access-control bypass, persistence, traffic interception, or testing of systems outside an exact written scope.
- Do not include live secrets, personal data, production endpoints, public targets, or destructive payloads in labs.
- Current threats, standards, advisories, browser behavior, libraries, and provider guidance must be rechecked from authoritative sources for the lesson date.
- Do not claim compliance, absence of vulnerabilities, or penetration-test coverage from instructional exercises.

## Completion

The learner can identify assets and trust boundaries, connect threats to controls, demonstrate expected rejection or containment in an authorized environment, explain monitoring and recovery, and communicate residual risk and further verification needs.
