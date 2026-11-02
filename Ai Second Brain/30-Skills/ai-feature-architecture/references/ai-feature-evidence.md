# AI Feature Evidence

Verified: 2026-10-21

## Risk and Security Guidance

- [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) provides the Govern, Map, Measure, and Manage structure for voluntary AI risk management.
- [NIST AI 600-1: Generative AI Profile](https://csrc.nist.gov/pubs/ai/600/1/final) applies AI RMF concepts to generative-AI risks and lifecycle controls.
- [OWASP Top 10 for LLM Applications 2025](https://owasp.org/www-project-top-10-for-large-language-model-applications/) is a practitioner threat reference covering prompt injection, sensitive-information disclosure, supply chain, poisoning, improper output handling, excessive agency, and related risks.

## Provider-Specific Evidence

- [OpenAI agent evaluation guide](https://developers.openai.com/api/docs/guides/agent-evals) documents traces, datasets, graders, and eval runs for OpenAI agent workflows.
- [OpenAI prompt-injection guidance](https://openai.com/index/designing-agents-to-resist-prompt-injection/) explains the risk from untrusted external content and defense-in-depth design for tool-using agents.
- [OpenAI building-agents track](https://developers.openai.com/tracks/building-agents) describes current OpenAI model, tool, guardrail, and evaluation concepts. These are provider claims, not an independent cross-provider benchmark.

## Interpretation Boundaries

- Benchmarks do not establish product fitness. Evaluate the exact model version, prompt, tools, data, and workflow on representative cases.
- A model upgrade can change behavior without application-code changes. Pin available versions and re-run evals on every material change.
- Guardrails are fallible classifiers and policies. Deterministic access control, transaction limits, validation, and human authorization must protect hard boundaries.
- Do not send provider credentials or sensitive production data during a proof of concept. SDKs and examples require exact-version supply-chain review before execution.
