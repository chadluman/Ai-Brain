---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, mongodb, atlas, security]
sources:
  - https://www.mongodb.com/docs/atlas/setup-cluster-security/
  - https://www.mongodb.com/docs/atlas/security-add-mongodb-users/
  - https://www.mongodb.com/docs/manual/core/schema-validation/
  - https://www.mongodb.com/docs/manual/core/transactions/
  - https://www.mongodb.com/docs/atlas/backup/cloud-backup/overview/
  - https://www.mongodb.com/docs/atlas/reference/atlas-limits/
  - https://www.mongodb.com/pricing
---

# MongoDB Atlas Integration

## Scope and Fit

This playbook covers a MongoDB Atlas database accessed from trusted backend code. It does not approve Atlas Search, Vector Search, Stream Processing, Data Federation, Online Archive, Charts, triggers, or other add-ons.

Use Atlas when aggregates naturally fit documents, flexible nested structures are valuable, MongoDB query/index behavior is understood, and the team can operate a managed cluster across its chosen cloud/region. Avoid using document flexibility to skip a domain model. Relational joins, cross-document constraints, and transaction-heavy workflows may fit a relational database better.

Recheck [security configuration](https://www.mongodb.com/docs/atlas/setup-cluster-security/), [schema validation](https://www.mongodb.com/docs/manual/core/schema-validation/), [backup availability](https://www.mongodb.com/docs/atlas/backup/cloud-backup/overview/), [service limits](https://www.mongodb.com/docs/atlas/reference/atlas-limits/), and [pricing](https://www.mongodb.com/pricing) for the exact cluster type, tier, cloud, and region.

## Trust Boundary

```text
untrusted client -> application authentication + authorization -> server repository
server -> Atlas network boundary + least-privilege database user -> MongoDB collection
operator/automation -> separate Atlas control-plane role -> cluster configuration
```

Atlas database users and network controls secure the database endpoint; they do not decide which end user may access a project document. Never expose a MongoDB connection string to a browser or mobile client.

## Prerequisites and Approval Boundaries

- Apply the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md).
- Accept an ADR covering document boundaries, transactions, cloud/region, cluster type/tier, availability, network path, backups, cost, and exit.
- Security-review the exact MongoDB driver/ODM, migration tooling, Atlas CLI/API client, Kubernetes operator, and IaC modules before use.
- Organization/project/cluster creation, billing, database users, IP access/private endpoints, encryption keys, production schema/index changes, imports, restores, scaling, and deletion are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `MONGODB_URI_RUNTIME` | Server secret | Least-privilege application database user |
| `MONGODB_DATABASE` | Server configuration | Explicit database name per environment |
| `MONGODB_URI_MIGRATION` | CI/operator secret | Schema validation, indexes, and controlled migrations |
| Atlas API credentials | Automation secret only when approved | Control-plane operations, separate from data-plane access |

Prefer private endpoints/peering where required. Otherwise use narrow IP/CIDR access lists; never use `0.0.0.0/0` as a production convenience. Atlas requires TLS. Separate projects and credentials by environment and rotate temporary/bootstrap access promptly.

## Document and Index Workflow

1. Model aggregate boundaries and required queries first. Decide where references, denormalized copies, and transactions are justified.
2. Define JSON Schema validation for stable required fields and types. Reject invalid writes rather than merely warning unless a measured migration requires staged validation.
3. Create compound indexes beginning with tenant scope for tenant-owned query patterns. Validate selectivity and explain plans with representative data.
4. Create a custom runtime role limited to the required collections/actions. Keep schema/index/admin and backup privileges in separate identities.
5. Keep transactions short and free of external side effects. Verify cluster support and driver retry semantics; callbacks may be retried.
6. Bound pool size, server selection timeout, request timeout, page size, batch size, and retry count. A larger application fleet can exhaust tier connection limits.

## Reference Collection Validation and Indexes

Run this as a reviewed migration against an isolated database first:

```javascript
db.createCollection("projects", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["tenantId", "ownerId", "name", "createdAt"],
      additionalProperties: false,
      properties: {
        _id: { bsonType: "objectId" },
        tenantId: { bsonType: "string", minLength: 1 },
        ownerId: { bsonType: "string", minLength: 1 },
        name: { bsonType: "string", minLength: 1, maxLength: 120 },
        createdAt: { bsonType: "date" }
      }
    }
  },
  validationLevel: "strict",
  validationAction: "error"
});

db.projects.createIndex({ tenantId: 1, ownerId: 1 });
db.projects.createIndex({ tenantId: 1, createdAt: -1, _id: -1 });
```

Adding `additionalProperties: false` requires every stored field, including `_id`, to be declared. For existing data, audit nonconforming documents and stage validation deliberately.

A minimal custom database role for this collection can grant `find`, `insert`, `update`, and `remove` on the named resource. Add `changeStream`, index, database-wide, or administrative actions only when the workload explicitly requires them; use the Atlas custom-role workflow and verify the effective privileges.

## Reference Server Repository

After the exact Node driver version is reviewed, construct filters and updates field by field. Never merge request objects into MongoDB operators.

```ts
import { MongoClient, ObjectId } from "mongodb";

const connectionString = process.env.MONGODB_URI_RUNTIME;
const databaseName = process.env.MONGODB_DATABASE;
if (!connectionString || !databaseName) {
  throw new Error("Missing MongoDB server configuration");
}

const client = new MongoClient(connectionString, {
  maxPoolSize: 20,
  serverSelectionTimeoutMS: 5_000,
});

type ProjectPatch = { name?: string };

export async function renameProject(
  tenantId: string,
  projectId: string,
  patch: ProjectPatch,
) {
  if (!tenantId || !ObjectId.isValid(projectId)) throw new Error("Invalid scope");
  const name = patch.name?.trim();
  if (!name || name.length > 120) throw new Error("Invalid project name");

  const collection = client.db(databaseName).collection("projects");
  const result = await collection.updateOne(
    { _id: new ObjectId(projectId), tenantId },
    { $set: { name } },
  );
  return result.matchedCount === 1;
}
```

`tenantId` must come from verified membership/authorization. Do not let a request choose `$where`, `$expr`, operators, collection names, projections, or sort keys outside a fixed allow-list.

## Verification

- Network access accepts only approved sources/private paths; TLS and hostname verification succeed and plaintext access fails.
- Runtime user can access only intended database/collections/actions and cannot create users, roles, indexes, validators, backups, or cluster settings.
- Wrong-user and wrong-tenant direct IDs, lists, updates, deletes, bulk operations, aggregations, change streams, exports, and jobs are denied by application logic and scoped filters.
- Validator rejects missing, wrong-type, oversized, unexpected, and tenant/owner-changing documents.
- Query plans use intended indexes at representative cardinality; unbounded scans and fan-out are prevented.
- Pool saturation, primary election/failover, timeout, retry, duplicate request, transaction conflict, quota, and provider outage preserve invariants.
- The chosen tier's backup is restored to an isolated cluster and checked for data, indexes, validators, roles, tenant isolation, and critical journeys. Backup capabilities differ for Free, Flex, and M10+ clusters.

## Operations, Cost, and Exit

Monitor connections, pool waits, replication lag/elections, query latency and scanned/returned ratio, index size, storage, backup state, network transfer, tier/autoscaling, security events, and spend. Optional auditing, private endpoints, KMS, search, backup distribution, and support can add cost.

For exit, prove BSON/JSON export plus schema/index/validator capture and transform a representative dataset into the target model. Inventory MongoDB-specific queries, aggregations, transactions, change streams, search indexes, drivers/ODMs, Atlas APIs, encryption, and multi-region topology.

## Re-Review Triggers

- cluster type/tier, MongoDB major version, cloud/region, pricing, limits, backup, network, encryption, or support changes
- new collection, validator, index, transaction, change stream, search/analytics add-on, private endpoint, or control-plane automation
- connection exhaustion, unindexed scan, cross-tenant finding, unexpected cost, election/retry defect, export gap, or restore failure

