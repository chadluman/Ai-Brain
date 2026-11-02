# Observability Evidence

Verified 2026-10-21.

- [Google SRE: Implementing SLOs](https://sre.google/workbook/implementing-slos/) routes from SLI specification to implementation and recommends moving measurement closer to users or improving coverage when evidence is weak. Treat it as experienced industry guidance, not a normative standard.
- [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/) describes traces, metrics, logs, and baggage in the vendor-neutral telemetry project. Signal and component maturity vary by language and release; verify exact SDK and collector versions before use.
- [W3C Trace Context](https://www.w3.org/TR/trace-context/) standardizes `traceparent` and `tracestate` propagation. Its privacy section prohibits personal or otherwise sensitive information in those fields and discusses correlation risk.
- [Prometheus instrumentation practices](https://prometheus.io/docs/practices/instrumentation/) provides opinionated metric guidance for online, offline, and batch systems. It is Prometheus-specific operational guidance, not a universal requirement to instrument every internal detail.

## Signal Roles

| Signal | Strong use | Common risk |
|---|---|---|
| Metrics | Trends, ratios, distributions, SLO evaluation, capacity | Unbounded labels, aggregation hiding affected users |
| Logs | Discrete events, structured context, audits where appropriate | Sensitive data, volume, inconsistent fields |
| Traces | Request paths, latency attribution, dependency and fan-out analysis | Sampling gaps, correlation privacy, instrumentation overhead |
| Profiles | Code-level resource diagnosis when mature and justified | Overhead, sensitive symbol or data exposure, tool maturity |

Choose signals by the question they answer. A dashboard or telemetry backend is not a substitute for a defined user outcome and response action.
