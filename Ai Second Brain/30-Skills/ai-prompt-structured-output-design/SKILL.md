---
name: ai-prompt-structured-output-design
description: Design prompts, structured outputs, and tool calls for an AI feature in a web application, so model output is validated, versioned, and safely usable by code. Use when a web feature calls a language model and code must act on its output; do not use for AI feature architecture or evaluation strategy, which are covered by AI Feature Architecture and AI Evaluation Engineering.
---

# AI Prompt Structured Output Design

## Outcome

Produce a prompt and output contract that code can trust: a versioned prompt, a machine-readable output schema, validation and retry rules, and a safe fallback when the model does not comply — without treating model fluency as correctness.

Use [AI Feature Architecture](../ai-feature-architecture/SKILL.md) to decide whether AI is the right approach at all. Use this skill for the implementation of the prompt and output layer once that decision is made.

## Required Inputs

- The task in user terms: what the user wants, what a good answer looks like, and what an unacceptable answer would do.
- The output contract: fields, types, allowed values, required versus optional fields, and what code will do with each field.
- The data the prompt may see: user input, retrieved passages, and system context, with their sensitivity and authorization boundaries.
- Failure tolerance: what happens when output is malformed, incomplete, unsafe, or too slow, and whether a human, a retry, or a non-AI fallback should handle it.

## Workflow

1. Write the prompt as a versioned artefact, not as an inline string scattered through code. Record its version, its intended model, and the date it was last evaluated, so a model change does not silently change behavior.
2. Separate instructions, data, and authority. Put system instructions in the system prompt, user data in a clearly delimited user message, and retrieved passages as data, never as instructions. Treat retrieved text as untrusted: it may contain prompt injection.
3. Require structured output where code acts on the result: a JSON schema, a function/tool schema, or an equivalent typed contract. Do not parse free-form prose with regular expressions as the primary contract.
4. Validate every model output before use: schema, types, allowed values, ranges, and cross-field consistency. Reject or repair only in defined ways: one bounded retry with a repair prompt, then a fallback. Do not retry indefinitely, and do not silently coerce invalid output into a plausible-looking value.
5. Define tool calling narrowly: each tool, its allowed arguments, its authorization check, and its reversibility. The model proposes; code authorizes and executes. Use [Agent Tool Safety](../agent-tool-safety/SKILL.md) for tool authority, and require human confirmation at consequential boundaries.
6. Keep the prompt minimal and privacy-minimal: send only the data the task needs, for the retention and region the provider actually offers. Do not send secrets, credentials, or unrelated user data in a prompt.
7. Test with adversarial and edge cases, not only with happy-path examples: injection in user input and in retrieved passages, missing fields, contradictory instructions, and out-of-scope requests. Use [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for the evaluation set and release gate.

## Safety and Permission Boundaries

- Treat model output as untrusted probabilistic data. Validate structure and facts before display, storage, or action, and do not present an AI answer as verified when it has not been checked.
- Publishing AI output, acting on real accounts, handling sensitive data, spending money, or making high-impact decisions is R3 and requires explicit authorization at that step.
- Prompt, model, and provider changes are versioned changes. Re-evaluate after a model, provider, or prompt change, and keep a rollback to the previous prompt and model version.
- Never place secret values in prompts, examples, logs, traces, or evaluation sets.

## Outputs and Evidence

- The versioned prompt, its output schema, and its validation and retry rules.
- An evaluation sample showing happy-path, malformed, injection, and out-of-scope cases, with the fallback taken in each failure case.
- A note recording model, provider, prompt version, cost and latency observed, and the conditions that trigger re-evaluation.
