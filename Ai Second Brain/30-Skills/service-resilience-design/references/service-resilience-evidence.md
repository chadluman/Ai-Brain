# Service Resilience Evidence

Verified: 2026-10-21

## Protocol and Industry Evidence

- [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) defines safe and idempotent methods, the limits on automatic retry, and `Retry-After`. Application side effects and idempotency still require explicit design.
- [AWS Builders' Library: Timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) explains how Amazon uses measured timeouts, bounded retries, backoff, jitter, token buckets, and idempotency while warning that retries can increase overload. It is industry practice, not a universal configuration.
- [Google SRE: Addressing Cascading Failures](https://sre.google/sre-book/addressing-cascading-failures/) covers overload, resource exhaustion, deadlines, load shedding, degradation, retry amplification, backoff, jitter, retry budgets, and recovery behavior.
- [Google SRE: Handling Overload](https://sre.google/sre-book/handling-overload/) describes client-side throttling, rejecting work, per-request attempt limits, and avoiding retries at multiple layers.
- [gRPC deadlines](https://grpc.io/docs/guides/deadlines/) recommends explicit realistic deadlines and explains deadline propagation, cancellation, and the risk of wasted server work.
- [gRPC retry](https://grpc.io/docs/guides/retry/) documents retry policy, attempt limits, exponential backoff, jitter, throttling, pushback, commitment, and retry observability for that protocol.

## Interpretation Boundaries

- Timeout values must come from product latency budgets, measured dependency distributions, network setup, and false-timeout tolerance. Copying another system's number is unsafe.
- Retries trade availability against extra latency and load. They help only for transient failures with remaining deadline and capacity.
- A network failure after dispatch creates an ambiguous outcome. Idempotency keys, status lookup, or reconciliation are required before repeating consequential work.
- Circuit breakers add state, recovery probes, and tuning risk. Use them only when simpler deadline, admission, and retry controls are insufficient.
- Queues move pressure in time but do not remove it. Bound age and depth, shed expired work, and protect downstream recovery.
- Degraded or cached responses must be labeled and must preserve authorization, privacy, and data-integrity requirements.

## Test Scenarios

- slow connect, TLS, first-byte, body, database lock, and queue acquisition
- partial response, connection reset, timeout after commit, duplicate delivery, and reordered completion
- dependency overload, rate limiting, flapping, regional loss, stale fallback, and cold recovery
- retry bursts from many clients, nested retries, exhausted budgets, and invalid `Retry-After`
- cancelled caller, expired work, deploy shutdown, pool exhaustion, full queue, and lost telemetry

## Re-Review Triggers

- new dependency, call layer, queue, failover route, region, or side effect
- material latency, capacity, traffic-shape, or availability change
- retry storm, duplicate effect, queue runaway, cascading failure, or difficult recovery
- protocol, client library, provider retry default, or deadline behavior change
