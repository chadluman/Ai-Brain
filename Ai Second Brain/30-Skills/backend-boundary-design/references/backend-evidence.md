# Backend Boundary Evidence

Verified 2026-10-21.

- [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) defines the stateless application protocol, method semantics, status codes, intermediaries, origins, and caching-related behavior for HTTP systems.
- [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html) defines shared and private cache behavior and calls out cache poisoning, timing attacks, and sensitive-information risks.
- [CloudEvents](https://cloudevents.io/) is a CNCF specification for a common event envelope. It standardizes event description, not broker durability, ordering, delivery guarantees, consumer idempotency, or business reconciliation.
- [NIST SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final) supplies lifecycle practices for secure software development. Use the web application security skill for technical control verification.

## Boundary Tests

A proposed separation should answer all of these questions:

- What independently changing or failing concern does this boundary isolate?
- Who owns its data and invariants?
- What happens on timeout, retry, duplication, reordering, overload, or partial completion?
- How are identity, authorization, secrets, logs, metrics, traces, deployment, rollback, backup, and restore handled?
- Can the project remove, merge, or migrate the component without rewriting unrelated domain logic?

If the answers add more uncertain infrastructure than product value, keep the boundary inside one deployable application and preserve it as a module.
