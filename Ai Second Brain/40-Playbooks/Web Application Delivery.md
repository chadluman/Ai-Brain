---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-25
review_by: 2027-01-21
risk: R2
tags: [playbook, web, delivery]
sources: []
---

# Web Application Delivery

## Purpose

Use this playbook to move a web application from an idea to an operated release without selecting a universal stack. It defines the order, evidence, handoffs, and stopping conditions; linked skills contain the detailed decision guidance.

This playbook does not itself authorize third-party installation, account creation, spending, production deployment, data migration, public release, or destructive cleanup.

## Inputs

- completed or partially completed [Project Intake](../60-Templates/Project%20Intake.md)
- product owner, delivery stage, users, critical journeys, constraints, budget, deadline, and maintenance owner
- data classifications, trust boundaries, compliance needs, and risk tolerance
- known external systems, providers, dependencies, and organizational approval boundaries

## Delivery State

Maintain one project note under `50-Projects/<project-name>/` with this compact state table. Link to evidence instead of copying it.

| Phase | State | Owner | Evidence | Blocking decision |
|---|---|---|---|---|
| Discover | not-started |  |  |  |
| Decide | not-started |  |  |  |
| Prove | not-started |  |  |  |
| Build | not-started |  |  |  |
| Qualify | not-started |  |  |  |
| Release | not-started |  |  |  |
| Operate | not-started |  |  |  |
| Handoff | not-started |  |  |  |

Use only `not-started`, `active`, `blocked`, or `complete`. A phase is complete only when its exit evidence exists.

## Phase 1: Discover the Right Outcome

1. Use [Product Discovery and Scope](../30-Skills/product-discovery-scope/Product%20Discovery%20and%20Scope.md) to separate the problem from a presumed solution, map the whole journey, rank assumptions, set measurable outcomes, and define stop criteria.
2. Complete the [Project Intake](../60-Templates/Project%20Intake.md). Ask only unanswered questions that could materially change scope, architecture, risk, time, or cost.
3. Classify data, users, abuse cases, external systems, accessibility needs, regions, expected demand, recovery needs, and maintenance capacity.
4. Decide whether the smallest useful next step is no build, process change, prototype, technical spike, integration proof, or thin production slice.
5. Use [Software Quality Assurance](../30-Skills/software-quality-assurance/Software%20Quality%20Assurance.md) to turn the critical journey, stakeholder needs, and unacceptable outcomes into proportionate quality objectives, requirements, responsibilities, evidence, and improvement controls.

Exit evidence:

- named user outcome and complete critical journey
- baseline, success measures, harm guardrails, scope, non-goals, budget, and deadline
- ranked assumptions with evidence plan
- quality objectives, measurable acceptance rules, owners, and evidence routes for material risks
- initial R0-R3 risk classification and authorization boundaries
- explicit proceed, revise, or stop decision

## Phase 2: Compare Architecture, Not Brands

1. Use [Architecture Selection](../30-Skills/architecture-selection/Architecture%20Selection.md) to derive candidate architectures from the intake.
2. Resolve route rendering with [Frontend Rendering Selection](../30-Skills/frontend-rendering-selection/Frontend%20Rendering%20Selection.md), platform support with [Web Platform Compatibility](../30-Skills/web-platform-compatibility/Web%20Platform%20Compatibility.md), and framework need with [Frontend Framework Selection](../30-Skills/frontend-framework-selection/Frontend%20Framework%20Selection.md).
3. Define [Backend Boundary Design](../30-Skills/backend-boundary-design/Backend%20Boundary%20Design.md), [API Contract Design](../30-Skills/api-contract-design/API%20Contract%20Design.md), and [Data Store Selection](../30-Skills/data-store-selection/Data%20Store%20Selection.md) from domain invariants and failure behavior. When a managed provider is credible, compare the [Backend and Database Services catalog](../20-Catalog/Backend%20and%20Database%20Services.md) rather than selecting from familiarity.
4. Resolve identity with [Identity and Authentication Selection](../30-Skills/identity-auth-selection/Identity%20and%20Authentication%20Selection.md) and resource policy with [Authorization and Tenancy Design](../30-Skills/authorization-tenancy-design/Authorization%20and%20Tenancy%20Design.md).
5. Compare hosting with [Hosting and Runtime Selection](../30-Skills/hosting-runtime-selection/Hosting%20and%20Runtime%20Selection.md), capacity and cost with [Capacity and Cost Planning](../30-Skills/capacity-cost-planning/Capacity%20and%20Cost%20Planning.md), and delivery with [CI/CD and Release Design](../30-Skills/ci-cd-release-design/CI-CD%20and%20Release%20Design.md).
6. For each material choice, copy the [Technology ADR](../60-Templates/Technology%20ADR.md), cite current primary evidence, and record exit or migration triggers.

Apply only the capabilities the brief requires:

| Need | Route |
|---|---|
| Product interface design | [Intentional Interface Design](Intentional%20Interface%20Design.md) |
| TypeScript | [TypeScript Project Foundation](../30-Skills/typescript-project-foundation/TypeScript%20Project%20Foundation.md) |
| UI system | [Design System Selection](../30-Skills/design-system-selection/Design%20System%20Selection.md) |
| Forms | [Web Form Design](../30-Skills/web-form-design/Web%20Form%20Design.md) |
| Client and server state | [Frontend State Design](../30-Skills/frontend-state-design/Frontend%20State%20Design.md) |
| Search | [Search Architecture Selection](../30-Skills/search-architecture-selection/Search%20Architecture%20Selection.md) |
| Caching | [Cache and Consistency Design](../30-Skills/cache-consistency-design/Cache%20and%20Consistency%20Design.md) |
| Realtime behavior | [Realtime Transport Selection](../30-Skills/realtime-transport-selection/Realtime%20Transport%20Selection.md) |
| Jobs and queues | [Background Job and Queue Design](../30-Skills/background-job-queue-design/Background%20Job%20and%20Queue%20Design.md) |
| Webhooks | [Webhook Integration Design](../30-Skills/webhook-integration-design/Webhook%20Integration%20Design.md) |
| Files or media | [File and Media Ingestion](../30-Skills/file-media-ingestion/File%20and%20Media%20Ingestion.md) |
| Notifications | [Notification Delivery Design](../30-Skills/notification-delivery-design/Notification%20Delivery%20Design.md) |
| Content management | [Content and CMS Architecture](../30-Skills/content-cms-architecture/Content%20and%20CMS%20Architecture.md) |
| Offline or installable web | [PWA and Offline Design](../30-Skills/pwa-offline-design/PWA%20and%20Offline%20Design.md) |
| International audiences | [Web Internationalization](../30-Skills/web-internationalization/Web%20Internationalization.md) |
| Discoverability | [Web Discoverability and SEO](../30-Skills/web-discoverability-seo/Web%20Discoverability%20and%20SEO.md) |
| Analytics or experiments | [Analytics and Experimentation Design](../30-Skills/analytics-experimentation-design/Analytics%20and%20Experimentation%20Design.md) |
| Payments or credits | [Payments and Ledger Design](../30-Skills/payments-ledger-design/Payments%20and%20Ledger%20Design.md) |
| AI features | [AI Feature Architecture](../30-Skills/ai-feature-architecture/AI%20Feature%20Architecture.md) |

Exit evidence:

- system context and data-flow diagrams where they improve understanding
- accepted ADRs with verified facts, estimates, risks, costs, and exit paths
- thin vertical-slice architecture and acceptance criteria
- exact R3 actions held for later authorization

## Phase 3: Admit Dependencies and Providers

1. Prefer platform features and existing approved components. Every new package, template, CLI, extension, image, binary, hosted API, or imported skill enters quarantine.
2. Complete a [Security Review](../60-Templates/Security%20Review.md) using [Software Supply Chain Review](../30-Skills/software-supply-chain-review/Software%20Supply%20Chain%20Review.md). Approval applies only to the inspected version or commit.
3. Record license, provenance, complete inventory, install hooks, code execution, network destinations, telemetry, permissions, secrets, advisories, isolated tests, removal, and rollback.
4. For an approved provider, copy the [Service Integration Playbook](../60-Templates/Service%20Integration%20Playbook.md) and fill it from current official documentation. For a cataloged backend/database provider, use [Managed Backend Integration](../30-Skills/managed-backend-integration/Managed%20Backend%20Integration.md), the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md), and only the selected provider playbook. Do not store secret values.
5. Use [Secrets and Configuration Management](../30-Skills/secrets-config-management/Secrets%20and%20Configuration%20Management.md) and keep local, test, staging, and production identities separated.

Exit evidence:

- version-specific decision for every external asset
- no unresolved high-impact finding, opaque behavior, hidden telemetry, or unexplained permission
- isolated test with dummy data for every R2 or R3 integration
- provider limits, data handling, cost, disablement, export, and deletion documented

## Phase 4: Prove a Thin Vertical Slice

Build one critical journey across the real boundaries needed for the architecture: interface, validation, authorization, domain logic, persistence, and one representative integration. Use synthetic data and local or isolated test resources.

The slice must prove:

- build and startup from a clean environment using [Build and Package Toolchain](../30-Skills/build-package-toolchain/Build%20and%20Package%20Toolchain.md)
- traceable design intent, real content, complete critical states, and product-specific expression using [Intentional Interface Design](Intentional%20Interface%20Design.md)
- semantic, keyboard-accessible interaction using [Web Accessibility Review](../30-Skills/web-accessibility-review/Web%20Accessibility%20Review.md)
- explicit trust boundaries using [Web Application Security Review](../30-Skills/web-app-security-review/Web%20Application%20Security%20Review.md)
- representative latency and payload evidence using [Web Performance Plan](../30-Skills/web-performance-plan/Web%20Performance%20Plan.md)
- one stored record, authorization decision, error path, retry boundary, and observable trace where applicable
- export or migration feasibility for an irreversible data or provider choice
- updated ADRs when evidence contradicts assumptions

Stop and revise the architecture if the slice misses a non-negotiable gate. Do not hide the failure by widening scope.

## Phase 5: Build in Verified Increments

For each increment:

1. Link work to a user outcome and acceptance evidence.
2. Inspect before editing and preserve unrelated work.
3. Make the smallest coherent change.
4. Add tests using [Test Strategy Design](../30-Skills/test-strategy-design/Test%20Strategy%20Design.md), review maintainability with [Software Quality Review](../30-Skills/software-quality-review/Software%20Quality%20Review.md), and keep the [Software Quality Assurance](../30-Skills/software-quality-assurance/Software%20Quality%20Assurance.md) traceability current when risks or requirements change.
5. Update contracts, threat cases, migration behavior, observability, costs, and documentation in the same increment.
6. Verify the critical journey, failure behavior, authorization, and rollback before broadening.

When persistent data changes, use [Data Migration Design](../30-Skills/data-migration-design/Data%20Migration%20Design.md). When infrastructure changes, use [Infrastructure as Code Design](../30-Skills/infrastructure-as-code-design/Infrastructure%20as%20Code%20Design.md).

## Phase 6: Qualify the Release

Use [Release Quality Evaluation](../30-Skills/release-quality-evaluation/Release%20Quality%20Evaluation.md) to create a candidate-specific release evidence record and a `ready`, `conditional`, `not ready`, or `insufficient evidence` recommendation, not a claim of general quality.

| Area | Minimum evidence route |
|---|---|
| Functional behavior | Acceptance, integration, contract, and critical-journey tests from [Test Strategy Design](../30-Skills/test-strategy-design/Test%20Strategy%20Design.md) |
| Interface design | Brief-to-screen traceability, state coverage, responsive specimens, originality evidence, and findings from [Interface Quality Review](../30-Skills/interface-quality-review/Interface%20Quality%20Review.md) |
| Accessibility | Automated checks plus keyboard, zoom, screen-reader, error, and disabled-user evidence appropriate to risk |
| Security | Threat-model review, dependency review, negative authorization tests, input limits, secret scan, and current advisories |
| Performance | Representative device, network, route, data, and load measurements with budgets |
| Privacy | [Privacy and Data Governance](../30-Skills/privacy-data-governance/Privacy%20and%20Data%20Governance.md), data-flow, minimization, consent, export, retention, and deletion evidence |
| Reliability | [Observability and SLO Design](../30-Skills/observability-slo-design/Observability%20and%20SLO%20Design.md), dependency failures, timeouts, retries, overload, and alert routing |
| Recovery | [Backup and Disaster Recovery](../30-Skills/backup-disaster-recovery/Backup%20and%20Disaster%20Recovery.md) restore exercise against the stated RPO and RTO |
| Operations | Runbooks, ownership, support, escalation, incident roles, capacity, quotas, and cost alerts |

Do not mark an unrun check as passed. Record it as pending, blocked, or not applicable with rationale.

Qualification recommends a disposition but does not authorize deployment or acceptance of high-impact residual risk. Keep those decisions in Phase 7 with the named authority.

## Phase 7: Authorize and Release

Before any production or externally consequential step, present one approval packet:

- exact change, environment, target, version, and operator
- verified release evidence and unresolved risks
- data affected and migration state
- expected one-time and ongoing cost with ceilings
- deployment sequence, health signals, pause and abort thresholds
- rollback or roll-forward procedure and last known restore evidence
- user, support, security, privacy, and incident communications

Obtain immediate explicit authorization for R3 actions. Release through the reviewed [CI/CD and Release Design](../30-Skills/ci-cd-release-design/CI-CD%20and%20Release%20Design.md), then verify externally observable behavior before increasing exposure.

For a public hostname, use [Domain, DNS, and TLS Operations](../30-Skills/domain-dns-tls-operations/Domain%2C%20DNS%2C%20and%20TLS%20Operations.md). Never combine unrelated DNS, certificate, database, and application changes into one opaque cutover.

## Phase 8: Operate, Learn, and Handoff

1. Watch user-centered SLOs, errors, security signals, cost, saturation, queues, provider health, and support outcomes through the defined observation window.
2. Use [Incident Response](../30-Skills/incident-response/Incident%20Response.md) for live coordination and learning. Mitigation authority does not imply authority for unrelated expansion.
3. Reconcile migrations, messages, webhooks, indexes, analytics, payments, and background work where used.
4. Deliver reproducible setup, environment ownership, architecture diagrams, accepted ADRs, provider playbooks, runbooks, restore evidence, known limitations, and maintenance triggers.
5. Retire old systems only after required retention, export, rollback, and observation gates. Revoke access and verify deletion when authorized.
6. Feed observed failures back into the linked skill or source note. Mark superseded guidance and preserve history rather than layering contradictions.

Completion requires:

- the critical journey is implemented and verified in its target environment
- required accessibility, security, performance, privacy, recovery, and failure evidence exists
- R3 actions have explicit authorization records
- ongoing ownership, costs, alerts, support, rollback, and maintenance are accepted
- known gaps are named with owners and dates rather than described as complete

## Playbook Validation Record

This first edition is structurally reviewed as portable Markdown and all links are checked, but it remains `draft` until exercised on a representative end-to-end project. During that exercise record confusing routing, missing gates, duplicate instructions, and evidence that could not be produced; then revise this note rather than adding an overlapping playbook.
