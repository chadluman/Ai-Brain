# Event-Driven System Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [CloudEvents](https://cloudevents.io/) is a CNCF graduated project whose current core specification release remains 1.0.2; CloudEvents SQL reached 1.0 in 2024. The core gives events a common envelope and bindings but does not define broker delivery, authorization, ordering, retention, idempotency, or business semantics.
- [AsyncAPI 3.1.0](https://www.asyncapi.com/docs/reference/specification/v3.1.0) is the current machine-readable, protocol-agnostic specification for message-driven APIs. An AsyncAPI document describes servers, channels, operations, messages, and schemas; its generators and tools are separate unreviewed executable assets.
- [CloudEvents specification repository](https://github.com/cloudevents/spec) is the canonical source for released and developing specifications. Pin a release; default-branch work can change and repository presence does not approve SDKs.
- [AsyncAPI documentation](https://www.asyncapi.com/docs) separates the specification from concepts, tutorials, migration guides, and tools. Document conformance does not prove that a producer or consumer implements its declared behavior.
- [CloudEvents specification](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md) defines the versioned 1.0.2 context attributes and extension model. Application identity, tenant, causation, privacy, and domain semantics still require explicit contracts.

## Decision Implications

- Use a standard envelope to reduce transport-specific glue, not to avoid defining the domain fact and delivery contract.
- A queue, broker, log, and webhook have different replay, fan-out, ordering, retention, push or pull, and ownership characteristics. Choose per path rather than declaring the entire system event-driven.
- End-to-end exactly-once effects usually require application state and idempotency even when a broker offers transactional or exactly-once features within a narrower boundary.
- Retained streams are databases. Compatibility and privacy obligations span the oldest replayable event and every active or recoverable consumer.
- Machine-readable contracts improve discovery and testing only when deployed producers and consumers are checked against the same pinned version.
