---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, firebase, firestore, security]
sources:
  - https://firebase.google.com/docs/firestore/data-model
  - https://firebase.google.com/docs/firestore/manage-data/transactions
  - https://firebase.google.com/docs/firestore/security/overview
  - https://firebase.google.com/docs/firestore/security/rules-structure
  - https://firebase.google.com/docs/firestore/security/test-rules-emulator
  - https://firebase.google.com/docs/firestore/quotas
  - https://firebase.google.com/docs/firestore/backups
  - https://firebase.google.com/pricing
---

# Firebase Firestore Integration

## Scope and Fit

This playbook covers Firebase Authentication plus Cloud Firestore Native mode for mobile and web clients. It does not cover Realtime Database, SQL Connect, Firestore Enterprise with MongoDB compatibility, App Hosting, Cloud Functions, Storage, Analytics, or Extensions except where they cross the Firestore trust boundary.

Use Firestore when the product benefits from client SDKs, realtime listeners, offline behavior, and access patterns that fit small documents and denormalized collections. Avoid it when relational constraints, joins, cross-record invariants, ad hoc reporting, predictable query cost, or provider portability dominate.

Recheck [data modeling](https://firebase.google.com/docs/firestore/data-model), [transactions](https://firebase.google.com/docs/firestore/manage-data/transactions), [quotas](https://firebase.google.com/docs/firestore/quotas), [backups](https://firebase.google.com/docs/firestore/backups), and [pricing](https://firebase.google.com/pricing) for the selected edition, plan, and location.

## Trust Boundary

```text
mobile/web client -> Firebase Auth token -> Firestore Security Rules -> documents
trusted server -> Admin/server SDK + IAM -> Firestore (Security Rules bypassed)
```

Security Rules are the authorization and data-validation boundary for mobile/web SDK calls. Server client libraries and Admin SDKs bypass those rules and require least-privilege IAM plus application authorization before every protected operation. App Check can reduce abuse from unofficial clients; it does not replace identity or authorization.

## Prerequisites and Approval Boundaries

- Apply the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md).
- Accept an ADR covering document model, location, edition/plan, offline behavior, query/index design, cost, recovery, and exit.
- Security-review the exact Firebase CLI, client/Admin SDKs, Rules test library, emulator binaries, and build plugins before installation or execution.
- Project/account creation, billing enablement, location selection, credentials, production rule/index deployment, real-data import/export, restore, and deletion are R3.

## Configuration Inventory

| Item | Exposure | Purpose |
|---|---|---|
| Firebase web app configuration | Client-visible identifiers | Selects the Firebase project/app; it is not authorization |
| Project ID per environment | Client/server configuration | Prevents accidental cross-environment access |
| Service-account key | Server secret; avoid when workload identity/ADC is available | Admin/server SDK credential that bypasses Rules |
| Emulator hosts | Local/test only | Routes SDKs to isolated emulators |

Use separate Firebase/Google Cloud projects for local/test, staging, and production. Never ship service-account JSON or Admin SDK credentials to a client.

## Data and Query Design

1. Derive collections and document boundaries from required reads and writes. Firestore stores documents in collections and has no relational joins.
2. Denormalize deliberately. Record the owner of duplicated data, update protocol, repair/reconciliation path, and deletion propagation.
3. Keep tenant-owned documents under a tenant path or include an immutable tenant field. Ensure every query is structurally compatible with the rules; Firestore Rules are not filters.
4. Define indexes, page bounds, listener lifecycle, fan-out, hot-document contention, transaction retries, and offline conflict behavior.
5. Use transactions only for atomic read-modify-write invariants. Transaction callbacks can run more than once and transactions fail when the client is offline; keep side effects outside the callback.

## Deny-by-Default Rules Example

This example allows tenant members to read projects but only the document owner to mutate a project. Membership writes are server-only. Adapt the role model and test every match path.

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    function signedIn() {
      return request.auth != null;
    }

    function isMember(tenantId) {
      return signedIn() &&
        exists(/databases/$(database)/documents/tenants/$(tenantId)/members/$(request.auth.uid));
    }

    function validProjectData(tenantId) {
      return request.resource.data.keys().hasAll(["tenantId", "ownerUid", "name"]) &&
        request.resource.data.keys().hasOnly(["tenantId", "ownerUid", "name"]) &&
        request.resource.data.tenantId == tenantId &&
        request.resource.data.ownerUid is string &&
        request.resource.data.name is string &&
        request.resource.data.name.size() > 0 &&
        request.resource.data.name.size() <= 120;
    }

    match /tenants/{tenantId}/members/{userId} {
      allow read: if signedIn() && request.auth.uid == userId;
      allow write: if false;
    }

    match /tenants/{tenantId}/projects/{projectId} {
      allow read: if isMember(tenantId);

      allow create: if isMember(tenantId) &&
        validProjectData(tenantId) &&
        request.resource.data.ownerUid == request.auth.uid;

      allow update: if isMember(tenantId) &&
        resource.data.ownerUid == request.auth.uid &&
        validProjectData(tenantId) &&
        request.resource.data.diff(resource.data).affectedKeys().hasOnly(["name"]);

      allow delete: if isMember(tenantId) &&
        resource.data.ownerUid == request.auth.uid;
    }

    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

Overlapping `match` statements are ORed: any matching `allow` that evaluates true permits the request. Review broad recursive wildcards carefully. Rules that call `exists()`, `get()`, or `getAfter()` have access-call limits and can add billed reads; verify the current rules and pricing documentation.

## Reference Client Query

After reviewing the exact modular web SDK, query inside the authorized tenant path. The path does not prove authorization; Rules still decide.

```ts
import {
  collection,
  getDocs,
  limit,
  query,
  type Firestore,
} from "firebase/firestore";

export async function listTenantProjects(db: Firestore, tenantId: string) {
  if (!tenantId) throw new Error("Missing tenant context");
  const ref = collection(db, "tenants", tenantId, "projects");
  const snapshot = await getDocs(query(ref, limit(100)));
  return snapshot.docs.map((doc) => ({ id: doc.id, ...doc.data() }));
}
```

Use the SDK's actual exported database type in project code. Bound list size and validate the tenant selection against the signed-in user's server/provider membership.

## Server/Admin Boundary

Admin SDK code bypasses Security Rules. Put it in server-only modules and require a completed application authorization decision before constructing a document path or query. Use Google Cloud workload identity/Application Default Credentials where available instead of a downloadable key. Grant the workload only the IAM permissions it needs.

## Local and Release Workflow

1. Store rules and indexes in version control and point `firebase.json` at them.
2. Run Auth and Firestore emulators with a clearly non-production project ID and synthetic fixtures. An emulator without configured rules can be open.
3. Use the Rules unit-testing library to assert allowed and denied operations with authenticated and unauthenticated contexts. Clear state between tests.
4. Treat emulator results as necessary but not sufficient; verify documented emulator/production differences and run an isolated hosted test before release.
5. Review the rule diff, target project, CLI identity, and rollback before an authorized deployment. Do not deploy rules interactively from an unreviewed workstation session.

## Required Verification

- unauthenticated access and unmatched paths denied
- member can read tenant data; non-member and wrong-tenant user cannot list or fetch by guessed ID
- owner can create/update/delete; another member cannot mutate; tenant and owner fields cannot be changed; missing, extra, wrong-type, empty, and oversized fields are denied
- broad collection-group queries, batch writes, transactions, listeners, server jobs, exports, and functions preserve the same authorization model
- malicious field types, unexpected fields, oversized content, operator-like objects, replay, contention, and offline retry do not break invariants
- rule access-call limits, index requirements, document/read/write limits, and representative billed reads/writes are measured
- scheduled backup and restore tested when required. Current scheduled backups require billing, restore into a new database, and do not include TTL policies; reapply IAM and TTL deliberately

## Operations, Cost, and Exit

Monitor denied Rules evaluations, Auth/App Check anomalies, reads/writes/deletes, listener fan-out, rule-dependent reads, storage, indexes, egress, contention, function triggers, backup state, quotas, and billing alerts.

For exit, export representative documents and index/rule definitions, then prove transformation into the target model. Inventory coupling to Auth identities/custom claims, Rules, offline caches and conflict assumptions, listeners, Cloud Functions, Storage, Analytics, App Check, and mobile release cadence.

## Re-Review Triggers

- edition, plan, pricing, location, SDK/CLI major version, emulator, Rules language, quota, backup, or Auth behavior changes
- new collection, collection-group query, custom claim, membership model, Admin SDK path, trigger, Storage dependency, or offline write pattern
- unexpected billing, hot-document contention, rule-limit failures, cross-tenant finding, export gap, or restore failure

