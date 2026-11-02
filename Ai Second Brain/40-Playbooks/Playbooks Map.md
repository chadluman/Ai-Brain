---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R0
tags: [playbooks, map]
sources: []
---

# Playbooks Map

Playbooks connect focused skills into an ordered delivery path. They route to one source of truth rather than repeating detailed guidance.

| Playbook | Use it for | State |
|---|---|---|
| [Web Application Delivery](Web%20Application%20Delivery.md) | Moving a web product from evidence and architecture through a thin vertical slice, release, operation, and handoff | Draft pending a complete representative project exercise |
| [Intentional Interface Design](Intentional%20Interface%20Design.md) | Turning a product brief into an original, state-complete, accessible, and verifiably functional interface | Draft pending a representative design-to-implementation exercise |
| [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md) | Applying shared trust-boundary, least-privilege, tenant-isolation, query, migration, recovery, and verification controls | Reviewed guidance; production application remains project-specific and R3 |
| [Supabase Integration](Supabase%20Integration.md) | Integrating hosted Postgres, Data API, Auth, grants, and RLS with tested client/server boundaries | Draft pending isolated RLS, migration, and restore exercise |
| [Firebase Firestore Integration](Firebase%20Firestore%20Integration.md) | Integrating Firebase Auth and Cloud Firestore with document modeling, Security Rules, emulator tests, and recovery | Draft pending isolated rules, quota, and restore exercise |
| [Neon Postgres Integration](Neon%20Postgres%20Integration.md) | Integrating managed Postgres with pooled/direct roles, branching, scaling, and recovery | Draft pending isolated connection, migration, and restore exercise |
| [MongoDB Atlas Integration](MongoDB%20Atlas%20Integration.md) | Integrating a managed document database with schema validation, indexes, network controls, roles, and backup | Draft pending isolated validation, failover, and restore exercise |
| [Cloudflare D1 Integration](Cloudflare%20D1%20Integration.md) | Integrating Worker-bound SQLite-compatible storage with tenant-scoped queries, limits, consistency, and Time Travel | Draft pending isolated Worker, limit, and restore exercise |
| [Amazon Aurora PostgreSQL Integration](Amazon%20Aurora%20PostgreSQL%20Integration.md) | Integrating Aurora PostgreSQL with VPC/IAM controls, roles, pooling, capacity, failover, and recovery | Draft pending isolated infrastructure, failover, and restore exercise |

These provider playbooks are reviewed documentation, not provider or dependency approval. Before project use, re-verify current official sources and complete exact-version review for every executable asset. Provisioning, credentials, billing, production changes, real-data operations, restore, and deletion remain R3.
