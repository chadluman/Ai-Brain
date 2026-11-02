# Tenant Lifecycle Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [OWASP Multi-Tenant Application Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Multi_Tenant_Security_Cheat_Sheet.html) covers server-verified tenant context, isolation strategies, tenant-aware data, cache, storage and jobs, onboarding and offboarding, backup restore, resource isolation, logging, and negative tests. It is practical guidance, not a certification.
- [RFC 7643](https://www.rfc-editor.org/rfc/rfc7643.html) defines SCIM users, groups, enterprise extensions, attribute characteristics, mutability, and schemas. It models identity resources, not a product tenant's billing, data, region, or ownership lifecycle.
- [RFC 7644](https://www.rfc-editor.org/rfc/rfc7644.html) defines SCIM provisioning operations, discovery, bulk, filtering, patching, versioning, and security considerations. It explicitly does not define registering tenants, associating clients to tenants, or indicating tenancy in requests.
- [RFC 9865](https://www.rfc-editor.org/rfc/rfc9865.html) updated SCIM in October 2025 with cursor pagination and requires authorization to be continuously enforced as permissions change; a cursor is not an authorization grant.
- [RFC 9967](https://www.rfc-editor.org/rfc/rfc9967.html) is the May 2026 Standards Track SCIM profile for Security Event Tokens, including create, patch, put, delete, activate, deactivate, feed, and asynchronous events. Its coordinated-provisioning model minimizes event data and retrieves current details through normal SCIM authorization.
- [NIST SP 800-207A](https://csrc.nist.gov/pubs/sp/800/207/A/final) supports identity-tier policy for cloud-native applications. It does not prescribe a tenant lifecycle or make shared infrastructure isolated by default.

## Decision Implications

- Tenant and user are different entities. A user may belong to many tenants, and tenant ownership, contract, region, billing, resources, and deletion outlive individual login sessions.
- SCIM can synchronize workforce identity, but its base RFC deliberately leaves tenancy mapping outside the protocol. Keep product tenant authority in the application model.
- Provisioning and deletion should converge from durable desired state. Idempotent retries and reconciliation are safer than long chains of assumed successful API calls.
- A suspended tenant may still generate queue, storage, vendor, domain, observability, and cost activity. Define the lifecycle state at every entry point and resource.
- Tenant restore from shared backup is a cross-tenant security operation: restore into isolation, select only authorized data, reapply current policy, and prove other tenants are absent.
