# Queue and Job Evidence

Verified: 2026-10-21

## Primary Guidance

- [Google SRE: Addressing Cascading Failures](https://sre.google/sre-book/addressing-cascading-failures/) explains why overload, large queues, slow failure, and uncontrolled retries can amplify failure. It supports bounded queues, early rejection, load shedding, and cautious recovery.
- [Google SRE: Production Services Best Practices](https://sre.google/sre-book/service-best-practices/) recommends exponential backoff with jitter and warns that retries can amplify low error rates into cascading load.
- [CloudEvents specification repository](https://github.com/cloudevents/spec/tree/ce%40v1.0.2) provides a stable, portable event-envelope vocabulary. It does not specify a broker's delivery, ordering, transaction, retention, or retry guarantees.
- [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) defines safety and idempotency for HTTP interactions used by workers. Application-side effects can require stronger idempotency controls than the HTTP method alone.

## Interpretation Boundaries

- Exactly-once business effects are an end-to-end invariant, not a queue marketing label. Broker deduplication cannot cover every database or external side effect.
- FIFO delivery usually has a limited scope such as a partition or message group and can trade throughput for ordering. Require order only where the domain needs it.
- A dead-letter queue is not recovery by itself. Define ownership, triage, privacy, retention, repair, safe replay, and retirement.
- Vendor-specific limits, billing, delivery contracts, encryption, regions, and failure behavior must be re-verified for the exact service and plan.
