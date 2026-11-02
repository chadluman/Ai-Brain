# Retrieval and Grounding Evidence

Verified: 2026-10-22

## Primary Sources

- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401) introduced a specific architecture combining parametric and non-parametric memory and highlighted provenance and knowledge updating as motivations. It does not establish a universal production pipeline or prove that retrieval makes generated claims correct.
- [BEIR](https://arxiv.org/abs/2104.08663) evaluates retrieval systems across heterogeneous domains and shows that effectiveness, generalization, computation, and reranking tradeoffs vary. Its result supports representative, domain-specific comparison and a lexical baseline rather than a universal embedding choice.
- [NIST AI 100-2e2025](https://www.nist.gov/publications/adversarial-machine-learning-taxonomy-and-terminology-attacks-and-mitigations-0) provides current terminology for generative-AI evasion, poisoning, privacy, and misuse risks across the AI lifecycle. NIST notes that mitigation effectiveness is contextual and does not set risk tolerance.
- [OWASP prompt-injection glossary](https://genai.owasp.org/glossaries/prompt-injection/) describes direct and indirect injection and emphasizes that instruction/data ambiguity cannot be fully patched. Use privilege minimization, output validation, and confirmation to limit impact.
- [W3C PROV-O](https://www.w3.org/TR/prov-o/) is a W3C Recommendation for representing entities, activities, agents, derivation, attribution, use, generation, and collections. It can inform lineage vocabulary; adopting RDF or the full ontology is not required for a practical corpus manifest.

## Decision Implications

- Evaluate lexical, structured, dense, hybrid, and reranked retrieval on the actual corpus and query distribution. Architecture labels do not predict relevance.
- Keep canonical content outside the index. Indexes and embeddings are derived artifacts that must be rebuildable and deletable.
- Source provenance needs stable document and revision identities plus transformation lineage. A link shown by a model is not proof that a passage supports a claim.
- Retrieval documents can contain adversarial instructions. The control boundary is deterministic authority and authorization, not a stronger instruction telling the model to ignore attacks.
- Measure retrieval misses separately from unsupported generation. Otherwise a single score cannot identify whether corpus, query, ranking, context construction, or generation failed.
