# Authorization Evidence

Verified: 2026-10-21

## Primary Guidance

- [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) separates authentication from authorization and recommends least privilege, deny by default, permission checks on every request, trusted server-side enforcement, and authorization tests.
- [OWASP Authorization Patterns Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Patterns_Cheat_Sheet.html) describes policy enforcement and decision points, resource-local enforcement, freshness, failure handling, and the risks of centralized or distributed decision components.
- [NIST SP 800-162](https://csrc.nist.gov/pubs/sp/800/162/upd2/final) defines attribute-based access control in terms of subject, object, requested operation, environment, attributes, and policy. It is a model reference, not a mandate to adopt ABAC.
- [NIST SP 800-207](https://csrc.nist.gov/pubs/sp/800/207/final) provides zero-trust architecture concepts, including explicit resource-access decisions and policy components. Its federal enterprise scope must be adapted rather than copied wholesale.
- [OWASP ASVS 5.0.0](https://github.com/OWASP/ASVS/releases/tag/v5.0.0) is a versioned application-security verification baseline. Select applicable access-control requirements rather than treating all requirements as equally relevant.

## Interpretation Boundaries

- RBAC, ABAC, and ReBAC labels do not prove a correct policy. Domain invariants, enforcement coverage, policy freshness, and negative tests are decisive.
- Tenant isolation is a system property spanning queries, storage, caches, search, files, jobs, analytics, exports, and operations tooling.
- A gateway can reject early, but the protected service remains responsible for authorization when alternate or internal paths exist.
- Product-specific authorization engines and policy languages require exact-version safety, availability, consistency, migration, license, and lock-in review before use.
