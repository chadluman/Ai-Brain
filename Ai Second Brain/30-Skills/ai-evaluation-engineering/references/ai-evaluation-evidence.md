# AI Evaluation Evidence

Verified: 2026-10-22

## Primary Sources

- [NIST AI 600-1: Generative AI Profile](https://csrc.nist.gov/pubs/ai/600/1/final) frames generative-AI risk through Govern, Map, Measure, and Manage. It calls for empirically validated evaluation, representative populations and conditions, human oversight, incident learning, and documentation of limitations. It is voluntary cross-sector guidance, not a product certification.
- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/) supplies optional actions aligned to AI RMF outcomes. The site notes that AI RMF 1.0 and the Playbook are being updated; recheck before using its suggestions as current organizational policy.
- [Stanford CRFM HELM](https://crfm.stanford.edu/helm/index.html) demonstrates multi-scenario, multi-metric evaluation and transparent raw results. Its benchmark scenarios and leaderboards illustrate coverage and reproducibility; they do not replace task-specific product evaluation.
- [UK AI Security Institute Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) is an MIT-licensed evaluation framework with support for models, tools, multi-turn tasks, scorers, logs, and sandboxed execution. The repository and its dependencies are unreviewed executable assets in this vault and remain R2 until a complete version-specific safety review.
- [UK AISI Inspect Evals](https://github.com/UKGovernmentBEIS/inspect_evals) is a maintained evaluation collection with task versioning and contribution controls. Community inclusion does not establish dataset rights, safety, fitness, or reproducibility for a different product.

## Decision Implications

- Evaluation begins with a claim and use context, not a model name. Record which population, workflow, version tuple, and failure types a result covers.
- Aggregate scores can hide rare severe failures and weak subgroups. Report critical failures and decision-changing slices separately.
- Reusable frameworks can improve repeatability but introduce code, model, dataset, sandbox, network, and dependency risk. Documentation review does not approve installation or execution.
- Model graders can improve scale, but need human calibration, blinded samples, disagreement analysis, and versioning. A grader update can change the result without a product change.
- Holdouts lose value when cases are copied into prompts, examples, or tuning loops. Maintain a deliberate promotion and refresh policy.
