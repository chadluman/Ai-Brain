---
status: approved
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-31
review_by: 2027-01-21
risk: R0
tags: [system, research, roadmap]
sources: []
---

# Research Queue

Research is organized in waves so the vault gains usable skills instead of a large undifferentiated link collection.

## Product and Measurement Foundations

- User needs, problem framing, journeys, success, evidence, scope, and validation - [Product Discovery and Scope](../30-Skills/product-discovery-scope/Product%20Discovery%20and%20Scope.md) drafted 2026-10-21
- Privacy-conscious event analytics, data quality, outcome measurement, and experiments - [Analytics and Experimentation Design](../30-Skills/analytics-experimentation-design/Analytics%20and%20Experimentation%20Design.md) drafted 2026-10-21
- User support, assisted journeys, capacity, privileged actions, escalation, and feedback - [Customer Support Readiness](../30-Skills/customer-support-readiness/Customer%20Support%20Readiness.md) drafted 2026-10-21
- Segment, problem, alternatives, reachable demand, market bounds, and proceed-or-stop evidence - [Market Validation Research](../30-Skills/market-validation-research/Market%20Validation%20Research.md) drafted 2026-10-21
- Delivery and operating estimates, scenarios, schedule effects, unit economics, and actuals reconciliation - [Product Economics Planning](../30-Skills/product-economics-planning/Product%20Economics%20Planning.md) drafted 2026-10-21
- Tax and invoicing readiness, payment fraud and abuse controls, marketplace platform design, and billing reconciliation operations drafted 2026-10-22; provider-specific pricing, filing, identity-verification, payout, sales-compensation, and regulated-economics execution playbooks remain

## Wave 1 — Web Engineering Foundations

| Topic | Evidence base | Skill | State |
|---|---|---|---|
| Source and repository qualification | Standards bodies, official maintainers, academic material, OpenSSF | Research Standard | Approved policy |
| Accessibility | W3C WCAG 2.2, WAI-ARIA 1.2, APG, official W3C repository | [Web Accessibility Review](../30-Skills/web-accessibility-review/Web%20Accessibility%20Review.md) | Draft; format validation required |
| Application security | OWASP ASVS 5.0.0, OWASP Cheat Sheet Series, NIST SSDF 1.1, CISA Secure by Design | [Web Application Security Review](../30-Skills/web-app-security-review/Web%20Application%20Security%20Review.md) | Draft; format validation required |
| Browser security policy | W3C WebAppSec drafts, IETF HSTS, OWASP deployment guidance | [Browser Security Policy](../30-Skills/browser-security-policy/Browser%20Security%20Policy.md) | Draft; supported-browser and negative-test validation required |
| Web performance | Current Core Web Vitals guidance, Lighthouse source, `web-vitals` source | [Web Performance Plan](../30-Skills/web-performance-plan/Web%20Performance%20Plan.md) | Draft; format validation required |
| Software quality | MIT 6.102 Software Construction, web-platform-tests | [Software Quality Review](../30-Skills/software-quality-review/Software%20Quality%20Review.md) | Draft; format validation required |
| Test strategy | MIT 6.102, Google Testing, W3C evaluation, WPT, OWASP WSTG | [Test Strategy Design](../30-Skills/test-strategy-design/Test%20Strategy%20Design.md) | Draft; realistic release validation required |
| Authorized penetration-test preparation | NIST SP 800-115, stable OWASP WSTG, current provider rules | [Penetration Test Readiness](../30-Skills/penetration-test-readiness/Penetration%20Test%20Readiness.md) | Draft; representative signed charter and safety tabletop required |
| Quality assurance | ISO 9000:2026, ISO 9001:2026, ISO 19011:2026, SQuaRE 25010/25019/25020/25030 | [Software Quality Assurance](../30-Skills/software-quality-assurance/Software%20Quality%20Assurance.md) | Draft; representative project-plan and assurance-review validation required |
| Release quality control | SQuaRE 25040, ISO/IEC/IEEE 29119 series, ISO/IEC 20246, ISTQB CTFL 4.0.1 | [Release Quality Evaluation](../30-Skills/release-quality-evaluation/Release%20Quality%20Evaluation.md) | Draft; representative release qualification and decision validation required |
| Codebase module boundaries | CMU SEI maintainability and ATAM, MIT 6.102 abstraction and specification | [Codebase Module Boundaries](../30-Skills/codebase-module-boundaries/Codebase%20Module%20Boundaries.md) | Draft; representative change, enforcement, and incremental-refactor validation required |

Specialized exploratory-test execution and defect-causal-analysis skills remain candidates only when a real project shows that the existing test-strategy, quality-review, assurance, and release-evaluation boundaries are insufficient.

## Wave 2 — Frontend Platform Decisions

- Web platform baseline: semantic HTML, CSS, JavaScript, browser compatibility, and progressive enhancement — [Web Platform Compatibility](../30-Skills/web-platform-compatibility/Web%20Platform%20Compatibility.md) drafted 2026-10-21
- Rendering choices: static, client-rendered, server-rendered, streamed, and hybrid — [Frontend Rendering Selection](../30-Skills/frontend-rendering-selection/Frontend%20Rendering%20Selection.md) drafted 2026-10-21
- TypeScript adoption, compiler boundaries, strictness, runtime validation, and migration — [TypeScript Project Foundation](../30-Skills/typescript-project-foundation/TypeScript%20Project%20Foundation.md) drafted 2026-10-21
- Framework and meta-framework comparison — [Frontend Framework Selection](../30-Skills/frontend-framework-selection/Frontend%20Framework%20Selection.md) drafted 2026-10-21
- Build tooling, package-management, lockfile, lifecycle-script, and reproducibility policy - [Build and Package Toolchain](../30-Skills/build-package-toolchain/Build%20and%20Package%20Toolchain.md) drafted 2026-10-21
- Monorepo, polyrepo, workspace, access, ownership, affected-build, release, host-scale, and source-preserving migration decisions - [Repository Topology Selection](../30-Skills/repository-topology-selection/Repository%20Topology%20Selection.md) drafted 2026-10-22
- Reproducible local and remote developer setup, runtime pinning, reviewed bootstrap, synthetic data, local-service lifecycle, verification, update, rollback, and teardown - [Developer Environment Reproducibility](../30-Skills/developer-environment-reproducibility/Developer%20Environment%20Reproducibility.md) drafted 2026-10-22
- CSS architecture, utility systems, component libraries, theming, and design tokens — [Design System Selection](../30-Skills/design-system-selection/Design%20System%20Selection.md) drafted 2026-10-21
- Bootstrap 6 prerelease installation, npm/Vite/Webpack/Parcel integration, color tokens, utility generation, component CSS and TypeScript, and staged v4/v5 migration — 11 [Bootstrap skills](../30-Skills/Skills%20Map.md) adapted from the official immutable source and approved-with-conditions as R0 guidance on 2026-10-31; exact dependencies, execution, project validation, and production suitability remain gated
- Product-specific art direction, semantic color architecture, typography, layout rhythm, motion, and signature expression — [Product Design Direction](../30-Skills/product-design-direction/Product%20Design%20Direction.md) drafted 2026-10-21
- Lawful observation, behavior decomposition, clean-room specification, and originality controls — [Interface Pattern Reconstruction](../30-Skills/interface-pattern-reconstruction/Interface%20Pattern%20Reconstruction.md) drafted 2026-10-21
- Intent, state, hierarchy, coherence, responsive, interaction, originality, and craft qualification — [Interface Quality Review](../30-Skills/interface-quality-review/Interface%20Quality%20Review.md) drafted 2026-10-21
- Decision-centered KPIs, metric contracts, lineage, freshness, comparisons, accessible data views, drill-downs, reports, and alerts - [Management Dashboard Design](../30-Skills/management-dashboard-design/Management%20Dashboard%20Design.md) drafted 2026-10-25
- Ordered design-to-implementation path — `Intentional Interface Design` playbook drafted 2026-10-21
- Forms and validation — [Web Form Design](../30-Skills/web-form-design/Web%20Form%20Design.md) drafted 2026-10-21
- Frontend state and browser persistence - [Frontend State Design](../30-Skills/frontend-state-design/Frontend%20State%20Design.md) drafted 2026-10-21
- Browser storage API selection, authority, quota, eviction, corruption, schema migration, concurrency, account separation, cleanup, and recovery - [Browser Storage Data Safety](../30-Skills/browser-storage-data-safety/Browser%20Storage%20Data%20Safety.md) drafted 2026-10-22
- Browser runtime failure taxonomy, cancellation, stale-response control, bounded retry, error isolation, draft preservation, accessible recovery, and privacy-safe telemetry - [Frontend Runtime Resilience](../30-Skills/frontend-runtime-resilience/Frontend%20Runtime%20Resilience.md) drafted 2026-10-22
- Third-party browser scripts, tags, pixels, widgets, frames, loaders, destinations, consent, isolation, controlled change, failure, and removal - [Third-Party Script Governance](../30-Skills/third-party-script-governance/Third-Party%20Script%20Governance.md) drafted 2026-10-22
- Internationalization and localization - [Web Internationalization](../30-Skills/web-internationalization/Web%20Internationalization.md) drafted 2026-10-21
- Structured content, editorial workflows, accessible authoring, CMS boundaries, and portability - [Content and CMS Architecture](../30-Skills/content-cms-architecture/Content%20and%20CMS%20Architecture.md) drafted 2026-10-21
- Task-centered information architecture, durable URLs, deep links, navigation, and redirects - [Information Architecture and Routing](../30-Skills/information-architecture-routing/Information%20Architecture%20and%20Routing.md) drafted 2026-10-21
- Permissioned ranking research, content opportunity, discoverability, and technical SEO - [Web Discoverability and SEO](../30-Skills/web-discoverability-seo/Web%20Discoverability%20and%20SEO.md) revised 2026-10-22; realistic owned-data and production-equivalent crawl validation remain
- Installable and offline web behavior - [PWA and Offline Design](../30-Skills/pwa-offline-design/PWA%20and%20Offline%20Design.md) drafted 2026-10-21
- Long-lived tab, cached asset, service-worker, API, flag, browser-schema, rollout, rollback, and mixed-version compatibility - [Web Client Release Compatibility](../30-Skills/web-client-release-compatibility/Web%20Client%20Release%20Compatibility.md) drafted 2026-10-22

## Wave 3 — Backend, API, and Data

- Backend topology, execution, communication, and service boundaries - [Backend Boundary Design](../30-Skills/backend-boundary-design/Backend%20Boundary%20Design.md) drafted 2026-10-21
- Backend runtime and framework lifecycle, workload, ecosystem, operations, and measured comparison - [Backend Runtime and Framework Selection](../30-Skills/backend-runtime-framework-selection/Backend%20Runtime%20and%20Framework%20Selection.md) drafted 2026-10-21
- Relational identities, types, relationships, constraints, indexes, history, tenancy, and evolution - [Relational Data Modeling](../30-Skills/relational-data-modeling/Relational%20Data%20Modeling.md) drafted 2026-10-21
- Deadlines, cancellation, retry ownership, idempotency, overload control, degradation, and recovery - [Service Resilience Design](../30-Skills/service-resilience-design/Service%20Resilience%20Design.md) drafted 2026-10-21
- API resource amplification, multi-dimensional quotas, concurrency, paid effects, harmful automation, sensitive-flow state, fair-use recovery, and draft-aware client feedback - [API Abuse and Resource Controls](../30-Skills/api-abuse-resource-controls/API%20Abuse%20and%20Resource%20Controls.md) drafted 2026-10-22
- HTTP/API contracts, schema evolution, idempotency, retries, and rate limits - [API Contract Design](../30-Skills/api-contract-design/API%20Contract%20Design.md) drafted 2026-10-21
- Outbound third-party API credentials, timeouts, retries, quotas, reconciliation, and exit - [External API Integration](../30-Skills/external-api-integration/External%20API%20Integration.md) drafted 2026-10-21
- Webhook authenticity, ingestion, deduplication, replay, and reconciliation - [Webhook Integration Design](../30-Skills/webhook-integration-design/Webhook%20Integration%20Design.md) drafted 2026-10-21
- Background jobs, queues, retries, backpressure, and operator recovery - [Background Job and Queue Design](../30-Skills/background-job-queue-design/Background%20Job%20and%20Queue%20Design.md) drafted 2026-10-21
- Domain events, authoritative publication, envelopes, delivery and ordering semantics, schema evolution, retained replay, tenant and privacy boundaries, and reconciliation - [Event-Driven System Design](../30-Skills/event-driven-system-design/Event-Driven%20System%20Design.md) drafted 2026-10-22
- Realtime transport, authorization, delivery, backpressure, and recovery - [Realtime Transport Selection](../30-Skills/realtime-transport-selection/Realtime%20Transport%20Selection.md) drafted 2026-10-21
- Relational, document, key-value, graph, search, cache, and object-storage choices - [Data Store Selection](../30-Skills/data-store-selection/Data%20Store%20Selection.md) revised 2026-10-21 with a service-shape, client-access, and managed-provider decision boundary
- Managed backend and database implementation - [Managed Backend Integration](../30-Skills/managed-backend-integration/Managed%20Backend%20Integration.md) plus shared security baseline drafted 2026-10-21
- Provider playbooks for Supabase, Firebase/Firestore, Neon Postgres, MongoDB Atlas, Cloudflare D1, and Amazon Aurora PostgreSQL drafted 2026-10-21; each remains pending isolated integration and restore validation
- Cache keys, freshness, invalidation, consistency, and overload - [Cache and Consistency Design](../30-Skills/cache-consistency-design/Cache%20and%20Consistency%20Design.md) drafted 2026-10-21
- Full-text, semantic, and hybrid search architecture and relevance - [Search Architecture Selection](../30-Skills/search-architecture-selection/Search%20Architecture%20Selection.md) drafted 2026-10-21
- File and media upload, remote import, quarantine, processing, storage, delivery, moderation, and deletion - [File and Media Ingestion](../30-Skills/file-media-ingestion/File%20and%20Media%20Ingestion.md) drafted 2026-10-21
- Schema, store, and provider migrations, reconciliation, cutover, rollback, and cleanup - [Data Migration Design](../30-Skills/data-migration-design/Data%20Migration%20Design.md) drafted 2026-10-21
- Transactions, isolation, constraints, locks, races, retries, and cross-system effects - [Transaction and Concurrency Design](../30-Skills/transaction-concurrency-design/Transaction%20and%20Concurrency%20Design.md) drafted 2026-10-21
- Cross-provider and high-volume migration playbooks remain; provider integration notes now define export, migration, and restore gates for the initial shortlist
- Identity, authentication, assurance, provider selection, federation architecture, recovery strategy, and sessions - [Identity and Authentication Selection](../30-Skills/identity-auth-selection/Identity%20and%20Authentication%20Selection.md) drafted 2026-10-21
- OAuth 2.0 and OpenID Connect client profiles, redirect and issuer trust, token validation, browser exposure, sender constraints, logout, key rotation, outage, and provider migration - [OAuth and OpenID Connect Integration Security](../30-Skills/oauth-oidc-integration-security/OAuth%20and%20OpenID%20Connect%20Integration%20Security.md) drafted 2026-10-22
- Authenticator loss, password reset, recovery codes and contacts, support-assisted recovery, channel changes, post-compromise restoration, notification, and appeal - [Account Recovery Security](../30-Skills/account-recovery-security/Account%20Recovery%20Security.md) drafted 2026-10-22
- Individual account creation, stable identity, external identity binding, sensitive identifier changes, restriction, suspension, reactivation, closure, deprovisioning, and re-registration - [User Account Lifecycle](../30-Skills/user-account-lifecycle/User%20Account%20Lifecycle.md) drafted 2026-10-25
- User-facing profile, contact, identity, authenticator, session, device, membership, privacy, export, closure, and deletion settings - [Account Management Experience](../30-Skills/account-management-experience/Account%20Management%20Experience.md) drafted 2026-10-25
- Browser sessions, cookies, CSRF, OAuth browser tokens, rotation, logout, and revocation - [Session and Cookie Security](../30-Skills/session-cookie-security/Session%20and%20Cookie%20Security.md) drafted 2026-10-21
- Configuration, secrets, credential inventory, injection, rotation, revocation, and recovery - [Secrets and Configuration Management](../30-Skills/secrets-config-management/Secrets%20and%20Configuration%20Management.md) drafted 2026-10-21
- Workload attestation, trust domains, short-lived service credentials, federation, token exchange, sender constraints, and static-secret retirement - [Workload Identity Federation](../30-Skills/workload-identity-federation/Workload%20Identity%20Federation.md) drafted 2026-10-22
- Authorization, object access, tenant isolation, policy freshness, and negative tests - [Authorization and Tenancy Design](../30-Skills/authorization-tenancy-design/Authorization%20and%20Tenancy%20Design.md) drafted 2026-10-21
- Tenant identity, provisioning, invitations, domain claims, membership, ownership, entitlements, restriction, suspension, transfer, merge, split, export, offboarding, retention, and deletion - [Tenant Lifecycle Operations](../30-Skills/tenant-lifecycle-operations/Tenant%20Lifecycle%20Operations.md) drafted 2026-10-22
- Administrative and support identity, just-in-time elevation, approval, impersonation, audit, entitlement review, break-glass, and revocation - [Privileged Access Operations](../30-Skills/privileged-access-operations/Privileged%20Access%20Operations.md) drafted 2026-10-22
- Staff and tenant-admin user discovery, inspection, role and access changes, exact selection scope, high-impact confirmation, and recoverable bulk operations - [User Administration Console](../30-Skills/user-administration-console/User%20Administration%20Console.md) drafted 2026-10-25
- Personal-data purpose, minimization, retention, user controls, vendors, export, and deletion - [Privacy and Data Governance](../30-Skills/privacy-data-governance/Privacy%20and%20Data%20Governance.md) drafted 2026-10-21
- Operational retention schedules, holds, expiry, primary and derived deletion, vendor propagation, backup residual windows, restore anti-resurrection, media sanitization, reconciliation, and safe evidence - [Data Retention and Deletion Operations](../30-Skills/data-retention-deletion-operations/Data%20Retention%20and%20Deletion%20Operations.md) drafted 2026-10-22

## Wave 4 — Delivery and Operations

- Dependency and software-supply-chain review - [Software Supply Chain Review](../30-Skills/software-supply-chain-review/Software%20Supply%20Chain%20Review.md) drafted 2026-10-21
- Routine, breaking, security, runtime, base-image, CI-action, transitive, deprecation, replacement, and removal upgrade operations - [Dependency Upgrade Operations](../30-Skills/dependency-upgrade-operations/Dependency%20Upgrade%20Operations.md) drafted 2026-10-22
- Continuous vulnerability intake, asset exposure, CVSS/EPSS/KEV/SSVC context, remediation, disclosure, deployment coverage, closure, and recurrence - [Vulnerability Management Operations](../30-Skills/vulnerability-management-operations/Vulnerability%20Management%20Operations.md) drafted 2026-10-22
- Exact-version open-source and source-available license evidence, obligations, compatibility questions, and release ownership - [Open Source License Review](../30-Skills/open-source-license-review/Open%20Source%20License%20Review.md) drafted 2026-10-21
- CI/CD, environments, deployment, and rollback - [CI/CD and Release Design](../30-Skills/ci-cd-release-design/CI-CD%20and%20Release%20Design.md) drafted 2026-10-21
- Infrastructure as code, state, plans, approvals, drift, and recovery - [Infrastructure as Code Design](../30-Skills/infrastructure-as-code-design/Infrastructure%20as%20Code%20Design.md) drafted 2026-10-21
- Application cryptographic purpose, inventory, approved implementation, key hierarchy and lifecycle, compromise recovery, agility, and post-quantum transition - [Cryptography and Key Management](../30-Skills/cryptography-key-management/Cryptography%20and%20Key%20Management.md) drafted 2026-10-22
- Hosting, static delivery, managed platforms, functions, containers, and virtual machines - [Hosting and Runtime Selection](../30-Skills/hosting-runtime-selection/Hosting%20and%20Runtime%20Selection.md) drafted 2026-10-21
- Single-region, multi-zone, warm-standby, active-passive, partitioned, and active-active regional resilience with consistency, fencing, residency, capacity, failover, and failback - [Multi-Region Resilience Design](../30-Skills/multi-region-resilience-design/Multi-Region%20Resilience%20Design.md) drafted 2026-10-22
- Domains, DNS, certificates, HTTPS enforcement, migration, and recovery - [Domain, DNS, and TLS Operations](../30-Skills/domain-dns-tls-operations/Domain%2C%20DNS%2C%20and%20TLS%20Operations.md) drafted 2026-10-21
- Logs, metrics, traces, alerts, and SLOs - [Observability and SLO Design](../30-Skills/observability-slo-design/Observability%20and%20SLO%20Design.md) drafted 2026-10-21
- Authoritative application audit events, actor and tenant context, integrity, access, retention, export, and failure handling - [Audit Log Design](../30-Skills/audit-log-design/Audit%20Log%20Design.md) drafted 2026-10-22
- Demand forecasting, measured capacity, overload behavior, cost allocation, and spend controls - [Capacity and Cost Planning](../30-Skills/capacity-cost-planning/Capacity%20and%20Cost%20Planning.md) drafted 2026-10-21
- Reliability and cybersecurity incident coordination, recovery, communications, and learning - [Incident Response](../30-Skills/incident-response/Incident%20Response.md) drafted 2026-10-21
- Backup, restore, continuity, and disaster recovery - [Backup and Disaster Recovery](../30-Skills/backup-disaster-recovery/Backup%20and%20Disaster%20Recovery.md) drafted 2026-10-21
- Exact plan, region, price, and quota facts remain project-time checks; the initial backend/database provider playbooks route to current official sources and cost drivers

## Wave 5 — Mobile and Cross-Platform

- Native iOS and Android versus shared-logic, cross-platform UI, and web selection - [Mobile Stack Selection](../30-Skills/mobile-stack-selection/Mobile%20Stack%20Selection.md) drafted 2026-10-21
- Signing, store accounts, test tracks, review, staged rollout, and update continuity - [Mobile Release Operations](../30-Skills/mobile-release-operations/Mobile%20Release%20Operations.md) drafted 2026-10-21
- Offline reads, queued writes, synchronization, conflicts, background retry, and recovery - [Mobile Offline Sync](../30-Skills/mobile-offline-sync/Mobile%20Offline%20Sync.md) drafted 2026-10-21
- Verified app links, safe route handling, OAuth redirects, navigation recovery, and web fallback - [Mobile Deep Link Navigation](../30-Skills/mobile-deep-link-navigation/Mobile%20Deep%20Link%20Navigation.md) drafted 2026-10-21
- Native accessibility semantics, adaptive settings, assistive-technology testing, and quality evidence - [Mobile Accessibility Quality](../30-Skills/mobile-accessibility-quality/Mobile%20Accessibility%20Quality.md) drafted 2026-10-21
- Mobile storage, network, platform interaction, permissions, SDKs, resilience, and privacy - [Mobile Security and Privacy](../30-Skills/mobile-security-privacy/Mobile%20Security%20and%20Privacy.md) drafted 2026-10-21
- Risk-based native and cross-platform test layers, lifecycle cases, device coverage, cadence, data, and flake controls - [Mobile Test Strategy](../30-Skills/mobile-test-strategy/Mobile%20Test%20Strategy.md) drafted 2026-10-22
- Local physical, virtual, remote, store, and beta device-lab selection with privacy, provider-lifecycle, fallback, and exit controls - [Mobile Device Lab Selection](../30-Skills/mobile-device-lab-selection/Mobile%20Device%20Lab%20Selection.md) drafted 2026-10-22
- Launch, responsiveness, frame, memory, storage, network, background, energy, crash, hang, and field quality - [Mobile Performance and Energy Quality](../30-Skills/mobile-performance-energy-quality/Mobile%20Performance%20and%20Energy%20Quality.md) drafted 2026-10-22
- Apple App Store and Google Play rules, target deadlines, declarations, listing, reviewer access, and continuing policy readiness - [App Store Policy Readiness](../30-Skills/app-store-policy-readiness/App%20Store%20Policy%20Readiness.md) drafted 2026-10-22
- Provider-specific mobile synchronization and framework-specific automation implementation playbooks remain
- Cross-channel in-app, email, mobile push, and web push delivery - [Notification Delivery Design](../30-Skills/notification-delivery-design/Notification%20Delivery%20Design.md) drafted 2026-10-21; provider-specific push and voice playbooks remain
- Sending identity, SPF, DKIM, DMARC, consent, suppression, bounces, complaints, unsubscribe, reputation, and provider migration - [Email Deliverability Operations](../30-Skills/email-deliverability-operations/Email%20Deliverability%20Operations.md) drafted 2026-10-22
- SMS consent, country and route constraints, sender registration, segmentation cost, STOP and HELP handling, delivery evidence, number reassignment, and fallback - [SMS Messaging Readiness](../30-Skills/sms-messaging-readiness/SMS%20Messaging%20Readiness.md) drafted 2026-10-22

## Wave 6 — AI and Economic Systems

- COITB Certified GPT Professional exam preparation across the five published domains, original weighted assessment, safe synthetic-data labs, and explicit exam-versus-current-provider distinctions - [Teach COITB Certified GPT Professional](../30-Skills/teach-coitb-gpt-professional/Teach%20COITB%20Certified%20GPT%20Professional.md) drafted 2026-10-25
- Model/provider evaluation, retrieval, tool use, evals, guardrails, privacy, latency, and cost - [AI Feature Architecture](../30-Skills/ai-feature-architecture/AI%20Feature%20Architecture.md) drafted 2026-10-21
- Task-specific datasets, risk slices, metrics, deterministic and model graders, human calibration, variance, regression, and release gates - [AI Evaluation Engineering](../30-Skills/ai-evaluation-engineering/AI%20Evaluation%20Engineering.md) drafted 2026-10-22
- Corpus authority, ingestion, segmentation, access-filtered retrieval, reranking, grounding, citation support, freshness, deletion, poisoning defense, and rebuild - [Retrieval and Grounding Design](../30-Skills/retrieval-grounding-design/Retrieval%20and%20Grounding%20Design.md) drafted 2026-10-22
- Agent and MCP authority, identity, scopes, tool review, schemas, prompt injection, confirmation, isolation, budgets, termination, auditing, and recovery - [Agent and Tool Safety](../30-Skills/agent-tool-safety/Agent%20and%20Tool%20Safety.md) drafted 2026-10-22
- Production AI versioning, privacy-minimized telemetry, quality and service objectives, quotas, cost, routing, fallback, canaries, incidents, provider exit, and retirement - [AI Runtime Governance](../30-Skills/ai-runtime-governance/AI%20Runtime%20Governance.md) drafted 2026-10-22
- Payments, subscriptions, entitlements, refunds, disputes, credits, and auditable ledgers - [Payments and Ledger Design](../30-Skills/payments-ledger-design/Payments%20and%20Ledger%20Design.md) drafted 2026-10-21
- Jurisdiction-aware transaction-tax evidence, registration and collection states, price display, invoices, corrections, filing boundaries, and retention - [Tax and Invoicing Readiness](../30-Skills/tax-invoicing-readiness/Tax%20and%20Invoicing%20Readiness.md) drafted 2026-10-22
- Layered account-takeover, card-testing, payment, promotion, refund, and marketplace-abuse controls with privacy and false-positive safeguards - [Payment Fraud and Abuse Controls](../30-Skills/payment-fraud-abuse-controls/Payment%20Fraud%20and%20Abuse%20Controls.md) drafted 2026-10-22
- Multi-party roles, seller onboarding, listings, funds and obligations, payouts, disputes, trust, compliance boundaries, and exit - [Marketplace Platform Design](../30-Skills/marketplace-platform-design/Marketplace%20Platform%20Design.md) drafted 2026-10-22
- Order, invoice, payment, provider balance, ledger, payout, bank, tax, and entitlement reconciliation and close controls - [Billing Reconciliation Operations](../30-Skills/billing-reconciliation-operations/Billing%20Reconciliation%20Operations.md) drafted 2026-10-22
- Fair revenue models, packaging, price metrics, channel rules, customer comprehension, entitlement lifecycle, and economic validation - [Monetization Model Design](../30-Skills/monetization-model-design/Monetization%20Model%20Design.md) drafted 2026-10-21

## Cross-Cutting Delivery Controls

- Safe, minimal-context orientation, status retrieval, and bounded vault changes for filesystem-capable agents - [Second Brain Context Access](../30-Skills/second-brain-context-access/Second%20Brain%20Context%20Access.md) reviewed 2026-10-26; live Cursor or Grok integration remains tool- and permission-specific
- External SaaS, managed service, hosted API, and supplier comparison - [Third-Party Service Evaluation](../30-Skills/third-party-service-evaluation/Third-Party%20Service%20Evaluation.md) drafted 2026-10-21
- Feature flags, canaries, kill switches, exposure gates, and cleanup - [Feature Flag and Rollout Design](../30-Skills/feature-flag-rollout-design/Feature%20Flag%20and%20Rollout%20Design.md) drafted 2026-10-21
- User-generated and AI-assisted content policy, reporting, blocking, review, enforcement, reasons, appeals, restoration, and moderator safety - [Content Moderation Operations](../30-Skills/content-moderation-operations/Content%20Moderation%20Operations.md) drafted 2026-10-22
- System, trust-boundary, business-logic, privacy, and operational threat analysis - [Application Threat Modeling](../30-Skills/application-threat-modeling/Application%20Threat%20Modeling.md) drafted 2026-10-21
- Tested technical documentation, operational ownership, onboarding, maintenance, and retirement handoff - [Documentation and Handoff](../30-Skills/documentation-handoff/Documentation%20and%20Handoff.md) drafted 2026-10-21

## Prioritization Rule

Move an item forward when a real project needs it or when it closes a safety-critical gap shared by many projects. Before starting a research item, define the decision it will improve and the output skill or playbook it should produce.
