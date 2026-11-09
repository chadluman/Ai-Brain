---
name: third-party-service-evaluation
description: Compare and review hosted APIs, SaaS products, managed infrastructure, SDK-backed platforms, and other external services before selection or renewal. Use when a provider will receive data, become an operational dependency, add cost, or create security and exit risk.
---

# Third-Party Service Evaluation

## Outcome

Select the smallest defensible external service, or choose not to outsource, using current evidence about product fit, security, privacy, reliability, cost, integration burden, portability, and supplier behavior.

## Required Inputs

- required capability, critical journeys, service level, volume, regions, and project stage
- data classes, secrets, permissions, network flows, tenants, retention, and compliance needs
- budget, cost drivers, team capacity, deadline, lifespan, and lock-in tolerance
- required APIs, SDKs, identity, webhooks, export, deletion, support, and incident behavior
- credible candidates, self-hosted or in-house baseline, and disqualifying gates

## Safety and Permission Constraints

- Marketing, marketplace listing, certifications, customer logos, AI summaries, and popularity are evidence inputs, not approval.
- Review the provider and every required SDK, CLI, action, template, extension, and transitive executable asset separately at the exact version.
- Do not send private data, create accounts, accept terms, connect production, enable telemetry, spend money, or grant OAuth or cloud access during evaluation without authorization.
- Unknown subprocessors, opaque data use, no workable export or deletion, unexplained broad permissions, hidden tracking, or unresolved high-impact vulnerabilities fail the applicable gate.
- Procurement, paid activation, private-data transfer, credential grant, or production integration is R3 and requires immediate authorization, contract and data review, cost ceiling, and exit plan.

## Workflow

1. Define the required outcome and a no-service or existing-service baseline. Separate non-negotiable gates from scored preferences.
2. Verify current official documentation, status history, pricing and limits, security, privacy, data regions, subprocessors, terms, support, API lifecycle, export, deletion, and end-of-life policy.
3. Map data and control flow, identities, scopes, network destinations, tenant boundaries, provider administrators, telemetry, retention, backups, and failure dependencies.
4. Assess supplier product-security practices, vulnerability disclosure, secure defaults, MFA and enterprise controls, audit evidence, incident communication, patch history, and supply-chain transparency.
5. Calculate total cost across environments, requests, seats, storage, transfer, support, overage, logs, backups, taxes, integration, operations, migration, and exit.
6. Inspect and security-review every local executable asset. Prefer standards, direct APIs, portable schemas, and replaceable adapters over required proprietary clients.
7. Run a time-boxed isolated proof with dummy data covering the critical path, failure behavior, rate limits, observability, export, deletion, revocation, and provider outage.
8. Compare qualified candidates consistently, record uncertainty, select only for the stated scope, and document a fallback or exit when impact warrants it.
9. Before activation, complete a provider-specific playbook with exact setup, least privilege, verification, monitoring, cost controls, rollback, disconnection, and removal.

## Structured Adoption Checklist

Run every candidate through the same checklist before selection, and record the evidence (or its absence) per item. This checklist is a synthesis assembled from several sources: no single retrieved source gave a complete checklist, so treat it as a working checklist to validate per candidate, not as a quoted standard.

- **Licence.** Is the licence compatible with the intended use and distribution, including any SDK or client the provider requires? See [Open Source License Review](../open-source-license-review/SKILL.md) for exact-version licence evidence.
- **CVE history.** What vulnerabilities have been disclosed, how fast were they patched, and are any high-impact issues unresolved? See [Vulnerability Management Operations](../vulnerability-management-operations/SKILL.md) for contextual priority.
- **Issue and PR responsiveness.** Do maintainers triage and fix in reasonable time, or do issues and pull requests sit unanswered? Unmaintained dependencies are a future incident, not a saving.
- **Bus factor.** How many people can keep the service or library alive? A single maintainer or a single vendor team is a concentration risk to price into the decision.
- **Exit cost.** What does leaving cost — export formats, migration effort, contract terms, data gravity, and replacement work? A cheap entry with an expensive exit is not cheap.
- **Spike validation.** Run a time-boxed isolated proof with dummy data on the critical path before committing: does the claimed fit hold, including failure behavior, rate limits, export, deletion, and revocation?

A candidate that fails a checklist item does not automatically fail the evaluation, but the failure, its consequence, and the accepted risk must be written down with the decision.

## Required Output

- capability and non-negotiable gate statement
- current candidate matrix with sources and verification dates
- provider, asset, permission, data, telemetry, and network inventory
- security, privacy, reliability, legal-review, and operational findings
- total-cost range and sensitivity drivers
- isolated proof results and unresolved uncertainty
- scoped decision, conditions, owner, review triggers, fallback, and exit plan

## Completion Gate

Do not approve a service until required executable assets have version-specific reviews, data and permission flows are explicit, cost and failure behavior are tested, export and revocation are demonstrated, and every consequential activation step remains separately authorized.

## Conditional Reference

Read [Service Evaluation Evidence](references/service-evaluation-evidence.md) when defining supplier-security questions, acquisition gates, or lifecycle review.
