---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [catalog, backend, database, security, managed-service]
sources:
  - https://supabase.com/docs/guides/database/overview
  - https://firebase.google.com/docs/firestore/data-model
  - https://neon.com/docs/introduction
  - https://www.mongodb.com/docs/atlas/setup-cluster-security/
  - https://developers.cloudflare.com/d1/
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.html
---

# Backend and Database Services

## Scope

This is a curated, project-selection shortlist, not a claim that six services cover every valid backend. It compares materially different service shapes that can satisfy common web and application workloads. Re-run [Data Store Selection](../30-Skills/data-store-selection/Data%20Store%20Selection.md) and [Third-Party Service Evaluation](../30-Skills/third-party-service-evaluation/Third-Party%20Service%20Evaluation.md) when a project's requirements point elsewhere.

No provider or executable dependency is approved by this note. Pricing, quotas, regions, support, product maturity, API behavior, and security features must be rechecked from the linked official pages for the exact plan and region before an ADR is accepted.

## Decide the Service Shape First

| Shape | What it supplies | What the application still owns |
|---|---|---|
| Backend as a service (BaaS) | Database plus some combination of client API, identity, storage, realtime, and functions | Domain invariants, authorization policy, policy tests, abuse controls, recovery, cost, and exit |
| Managed database | Operated database endpoint, scaling, monitoring, and provider backup features | API/backend, end-user identity and authorization, schema, queries, migrations, restore validation, and most abuse controls |
| Edge-bound database | Database exposed only through a platform runtime binding | Authentication, authorization, tenant predicates, API behavior, consistency choices, and platform exit |
| Self-managed database | Engine and full configuration control | Patching, hardening, availability, backup, restore, observability, capacity, and incident response |

Do not choose a managed database expecting it to provide application authorization. Do not expose a database credential, administrator SDK, secret key, or service role to an untrusted client.

## Qualified Shortlist

| Service | Shape and data model | Strong fit | Decisive limitations and risks | Security boundary | Portability and cost shape |
|---|---|---|---|---|---|
| [Supabase](../40-Playbooks/Supabase%20Integration.md) | Postgres BaaS with Data API, Auth, Storage, Realtime, and functions | Relational applications that benefit from integrated services and tested Postgres row-level security (RLS) | RLS and grants are easy to misconfigure; secret/service-role access bypasses RLS; database backups do not include Storage objects; connection mode must match the runtime | A publishable client key is only safe with least-privilege grants and tested RLS on every exposed object | Core data is Postgres-portable; Auth, Storage, Realtime, and function behavior need separate migration work. Cost spans compute, storage, auth, egress, logs, and add-ons |
| [Firebase with Cloud Firestore](../40-Playbooks/Firebase%20Firestore%20Integration.md) | Mobile/web BaaS with a document database, client SDKs, Auth, Storage, functions, and offline support | Mobile, realtime, and offline-oriented products whose access patterns fit denormalized documents | No relational joins; query/index and document limits shape the model; reads, writes, deletes, rule lookups, storage, and egress drive cost; transactions fail offline; server SDKs bypass Firestore Security Rules | Mobile/web clients require Firebase Auth plus deny-by-default Security Rules; server SDK paths require IAM and application authorization | Data can be exported, but query, rules, offline, trigger, and SDK semantics create meaningful lock-in |
| [Neon Postgres](../40-Playbooks/Neon%20Postgres%20Integration.md) | Serverless managed Postgres with branching, autoscaling, scale-to-zero, pooling, and instant restore | Standard Postgres behind an existing backend, especially variable or preview-environment workloads | Scale-to-zero can add wake latency; transaction pooling does not support session-dependent features; plan controls history, private networking, and operational features | Keep Postgres credentials server-side; use separate migration and runtime roles plus application authorization and tenant-scoped queries | Strong SQL and `pg_dump` portability; cost follows compute time, storage, history, transfer, and plan. This playbook does not approve newer optional backend add-ons |
| [MongoDB Atlas](../40-Playbooks/MongoDB%20Atlas%20Integration.md) | Managed document database on AWS, Azure, or Google Cloud | Evolving aggregate-shaped documents, flexible nested data, and MongoDB-specific query or distribution needs | Flexible schema still requires validation; cross-document relations and transaction-heavy relational invariants can become awkward; tier, connection, feature, and backup limits vary | Atlas network and database users protect the database endpoint; end-user authorization and tenant scoping remain application responsibilities | BSON/JSON export helps, but query, index, transaction, search, and operational semantics are MongoDB-specific. Cost depends on tier/usage, cloud, region, storage, transfer, backups, and add-ons |
| [Cloudflare D1](../40-Playbooks/Cloudflare%20D1%20Integration.md) | Managed SQLite-compatible database accessed through Cloudflare Workers bindings | Worker-native applications with bounded databases, SQL needs, and globally distributed reads | Current paid database size is 10 GB; row, parameter, statement, and per-invocation limits apply; read replicas are asynchronous and require Sessions for sequential consistency; no database-native end-user policy layer | The Worker is the authorization boundary. Every query must derive tenant/user scope from verified identity and bind it as a parameter | SQL export is available and SQLite concepts transfer, but the binding, operational model, limits, and replication API are platform-specific; cost is driven by Workers plus rows read/written and storage |
| [Amazon Aurora PostgreSQL](../40-Playbooks/Amazon%20Aurora%20PostgreSQL%20Integration.md) | AWS-managed PostgreSQL-compatible relational cluster, provisioned or Serverless v2 | AWS-centered production systems needing VPC controls, replicas, mature operations, and configurable capacity/availability | Highest setup and operating surface here; engine/version/region compatibility matters; connection storms need pooling; many separate cost dimensions and IAM/VPC/KMS/backup decisions | Private VPC placement, security groups, TLS, database roles, Secrets Manager or IAM database auth, and server-side application authorization | SQL and logical export are portable in principle; Aurora features, AWS networking, IAM, replicas, and operations increase switching cost. Cost spans capacity/instances, I/O mode, storage, backup, proxy, transfer, monitoring, and support |

## Fast Routing by Requirement

| Requirement that dominates | Start with | Prove before selecting |
|---|---|---|
| Integrated relational MVP with client data access | Supabase | RLS/grant negative tests, restore scope, connection mode, and exit for Auth/Storage |
| Mobile or web offline synchronization with document access | Firebase/Firestore | Access-pattern model, Security Rules tests, hot-document contention, query cost, and export |
| Portable Postgres behind existing server code with variable demand | Neon | wake latency, pooled-driver compatibility, connection recovery, restore window, and network controls |
| Document aggregates or MongoDB ecosystem are requirements | MongoDB Atlas | schema validation, tenant queries, indexes, transaction boundaries, tier limits, and backup restore |
| Cloudflare Worker runtime plus bounded SQLite data | D1 | database and row limits, write path, tenant enforcement, Sessions consistency, and export |
| AWS private networking, mature controls, or demanding relational operations | Aurora PostgreSQL | minimum cost, failover, connection pooling, IAM/secret lifecycle, restore timing, and operator capacity |

If two options remain credible, build the same thin vertical slice with synthetic data and compare observable latency, correctness, denied access, migration, restore, cost drivers, and operator effort. Do not compare dashboard screenshots or free tiers alone.

## Non-Negotiable Gates

Disqualify a candidate for the project when any required gate fails:

- the data model cannot preserve critical invariants or required transactions;
- residency, region, privacy, retention, deletion, encryption, audit, or qualified-review needs are unmet;
- tenant isolation cannot be enforced and tested on every access path;
- the plan lacks an achievable RPO/RTO, export, or restore path;
- required features exceed documented hard limits or depend on a preview/beta feature without accepted risk;
- the worst credible cost exceeds the approved ceiling;
- a required executable asset has not passed exact-version review;
- the team cannot operate, monitor, rotate, recover, and migrate the service within its capacity.

## Evidence and Review Boundary

Verified on 2026-10-21 against the official sources recorded in each provider playbook and the [Source Registry](Sources/Source%20Registry.md). The comparison summarizes current documented behavior; it is not load-test, restore-test, privacy, legal, compliance, or security-assurance evidence for a particular project.

