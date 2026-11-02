# Relational Data Modeling Evidence

Verified: 2026-10-21

## Engine and Academic Evidence

- [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html) documents check, not-null, unique, primary-key, foreign-key, and exclusion constraints, including important limits on cross-row check expressions and delete behavior.
- [PostgreSQL data types](https://www.postgresql.org/docs/current/datatype.html) documents current engine types and their semantics. Portable designs must separately evaluate other engines.
- [PostgreSQL indexes](https://www.postgresql.org/docs/current/indexes.html) describes index types, multicolumn, unique, expression, partial, covering, and planner behavior for the current PostgreSQL release.
- [PostgreSQL dependency tracking](https://www.postgresql.org/docs/current/ddl-depend.html) explains object dependencies and `RESTRICT` versus `CASCADE` effects.
- [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) documents isolation behavior and anomalies for the current engine version.
- [CMU 15-445/645 Introduction to Database Systems, Spring 2026](https://15445.courses.cs.cmu.edu/spring2026/schedule.html) provides university instruction on the relational model, SQL, storage, indexes, query execution, concurrency, recovery, and distributed databases. Course material is educational rather than a production-engine contract.

## Interpretation Boundaries

- PostgreSQL is a concrete evidence source, not a universal SQL specification. Verify syntax, types, constraints, indexes, isolation, and migration behavior on the exact selected engine and version.
- Normalization reduces update anomalies but is not a goal independent of domain clarity, query needs, and operating constraints. Denormalized copies need explicit freshness and repair.
- An ORM model is not necessarily the database model. Inspect generated DDL, constraints, indexes, transaction behavior, and migrations.
- Foreign keys establish referential integrity, not authorization or tenant isolation. Include tenant scope in access paths and constraints where the model requires it.
- Soft deletion can preserve references while breaking uniqueness, retention, user expectations, and queries. Define it as lifecycle state, not a universal default.
- Index recommendations require real predicates, data distributions, and query plans. Extra indexes increase write, storage, vacuum, and migration cost.

## Verification Prompts

- Can duplicate, orphaned, impossible, cross-tenant, negative, out-of-range, or invalid-transition rows be created?
- What does `NULL` mean for every nullable column, and does a default assert a true fact?
- What happens on parent update and deletion, account deletion, tenant export, retention expiry, and restore?
- Which invariants cross rows or systems, and what transaction or reconciliation mechanism protects them?
- Do current and previous application versions coexist during expand-contract migration?
- Can every important query be reproduced with representative cardinality and an inspected plan?

## Re-Review Triggers

- domain invariant, identity, tenancy, retention, query pattern, or scale change
- database engine or major version change
- ORM, migration tool, replication, partitioning, or deployment topology change
- integrity incident, query regression, restore failure, or repeated manual data repair
