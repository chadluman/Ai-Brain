---
name: ai-evaluation-engineering
description: Design and operate task-specific evaluations for generative-AI, retrieval, classification, or tool-using systems across datasets, metrics, graders, human review, adversarial cases, regression gates, and production feedback. Use after an AI task contract exists; do not use a public leaderboard as proof that a product is safe or fit.
---

# AI Evaluation Engineering

## Outcome

Produce a reproducible evaluation system that measures the actual product task, exposes critical failure rates and uncertainty, and gates model, prompt, retrieval, tool, and policy changes with accountable evidence.

## Required Inputs

- task contract, users, decisions affected, acceptable and unacceptable outcomes, deterministic or human baselines, and deployment stage
- input and output classes, languages, modalities, user groups, jurisdictions, data sensitivity, and known abuse patterns
- exact model, prompt, tool, retrieval, policy, and runtime versions plus sampling and nondeterminism controls
- quality, safety, security, fairness, privacy, latency, availability, and cost requirements with failure severity
- data rights, provenance, labeling expertise, contamination risk, retention, and access constraints

Stop if the task cannot be expressed as observable cases and decision thresholds. Route initial workflow design to [AI Feature Architecture](../ai-feature-architecture/SKILL.md).

## Safety and Permission Constraints

- Treat benchmark and grader output as evidence with scope and error, not a safety certificate. Public benchmark rank does not establish product fitness.
- Never put secrets, unapproved personal data, production conversations, copyrighted corpora without rights, or harmful content beyond the approved test need into an evaluation set or external evaluator.
- Separate test cases from prompts, training, examples, and tuning data where leakage would invalidate results. Record provenance and contamination risks.
- Model-based graders are fallible and can share the evaluated model's biases. Calibrate them against blinded human judgments and retain disagreement and uncertainty.
- Sending protected data to a provider, running high-risk red-team content, or using results to make consequential decisions is R3 and requires authorization, access controls, qualified review, and a response plan.

## Workflow

1. Write the evaluation claim: the exact workflow, population, conditions, version tuple, success criteria, prohibited failures, and decision the evidence will support.
2. Build a risk taxonomy before metrics. Partition ordinary, boundary, rare, multilingual, accessibility, adversarial, stale-data, injection, permission, tool-failure, refusal, and recovery cases by severity and exposure.
3. Assemble datasets with lawful provenance, representative distributions, scenario identifiers, expected behavior or rubric, reviewer guidance, split policy, and protected holdouts. Prefer a small high-signal set before a large weak one.
4. Select metrics by decision. Include task success and critical-failure rate; add calibrated precision/recall, ranking, groundedness, citation support, tool correctness, policy compliance, fairness slices, latency, availability, and unit cost only where meaningful.
5. Choose scorers in layers: deterministic assertions, reference comparisons, structured rule checks, domain-human review, and calibrated model graders. Define abstention, ambiguity, tie, and scorer-failure behavior.
6. Establish baselines and variance. Compare the non-AI or human workflow, repeat stochastic cases, retain raw outputs and seeds where available, and report confidence or stability rather than false precision.
7. Test the complete system, not only a model endpoint. Include retrieval, authorization, tools, retries, truncation, rate limits, provider errors, content controls, user interface, and downstream validation.
8. Set release gates before seeing candidate results. Weight critical harms separately from averages, define no-regression slices, require review for threshold exceptions, and document who may approve them.
9. Version the dataset, labels, rubric, grader, model, prompt, corpus, tools, policy, and code. Produce a comparison that attributes changes and makes unreviewed drift visible.
10. After launch, sample privacy-minimized production failures and user corrections into a controlled review queue. Investigate distribution shift and incidents, then add regression cases without leaking the holdout into tuning.

## Required Output

- scoped evaluation claim, risk taxonomy, case matrix, provenance, and data controls
- versioned dataset and holdout design with labeling and adjudication instructions
- metric, scorer, calibration, variance, and slice definitions
- baseline, candidate results, raw-evidence location, confidence, and known blind spots
- release thresholds, exception authority, regression policy, and failure triage
- production feedback, drift, incident, retention, and re-evaluation plan

## Completion Gate

Do not claim an AI change evaluated until representative and critical-risk cases ran against the complete versioned workflow, graders were calibrated for their intended use, threshold decisions were set and recorded, sensitive data controls were verified, failures remain inspectable, and results state their scope, uncertainty, and unresolved risks.

## Conditional Reference

Read [AI Evaluation Evidence](references/ai-evaluation-evidence.md) when selecting evaluation dimensions, frameworks, datasets, graders, or release evidence.
