# AI Runtime Governance Evidence

Verified: 2026-10-22

## Primary Sources

- [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) supplies voluntary Govern, Map, Measure, and Manage outcomes across the AI lifecycle. It supports named ownership, documented risk tolerance, monitoring, incident learning, and decommissioning, but does not prescribe a runtime stack.
- [NIST AI RMF Playbook: Measure](https://airc.nist.gov/airmf-resources/playbook/measure/) emphasizes context-specific metrics, comparison to simpler and human baselines, regular monitoring, error and complaint response, oversight, and emergent risk. The Playbook is being updated with AI RMF and must be rechecked.
- [OpenTelemetry GenAI semantic conventions](https://github.com/open-telemetry/semantic-conventions-genai/blob/main/docs/gen-ai/README.md) define emerging spans, metrics, and events for inference, agents, tools, retrieval, and evaluations. Their status is Development; pin the schema version and expect changes.
- [OpenTelemetry GenAI attribute registry](https://github.com/open-telemetry/semantic-conventions-genai/blob/main/docs/registry/attributes/gen-ai.md) warns that prompts, outputs, system instructions, retrieval queries, tool arguments, and results can contain sensitive information. Content collection must be deliberate, minimized, and protected.
- [OWASP LLM10:2025 Unbounded Consumption](https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/) describes denial of service, denial of wallet, excessive input and output, model extraction, and uncontrolled inference. Rate limits alone are insufficient without size, time, concurrency, iteration, and spend controls.
- [FOCUS Specification 1.4](https://focus.finops.org/docs/specification/v1-4/) provides a vendor-neutral schema for technology cost and usage data, attribution, unit economics, anomaly analysis, and reconciliation. Whether an AI provider emits conformant data must be verified; application-level request and tenant attribution remain necessary.

## Decision Implications

- Keep runtime service health and product quality distinct but correlated. Fast successful HTTP responses can still contain harmful or unusable answers.
- A version record must include more than a model name. Prompts, policies, retrieval, tools, routing, parameters, graders, and provider behavior can change outcomes.
- Observability content is a high-risk data collection feature, not a default. Prefer metadata and derived measures; use time-bound, access-controlled capture for investigations.
- Token counts are provider-specific operational units, not comparable business value. Reconcile them with task success, external tool cost, retries, invoices, and unit economics.
- Emerging semantic conventions improve portability but are not stable. Pin and translate at an internal boundary so telemetry changes do not dictate application architecture.
