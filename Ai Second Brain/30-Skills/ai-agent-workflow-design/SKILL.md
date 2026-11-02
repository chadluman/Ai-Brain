---
name: ai-agent-workflow-design
description: Structure a multi-step AI task as a loop or a graph with state, stopping conditions, and human approval, so an agent can do useful work without running forever or taking an irreversible step alone. Use when an AI feature needs more than one model call or tool call; do not use for a single prompt or structured output, which is covered by AI Prompt Structured Output Design, or for tool safety alone, which is covered by Agent Tool Safety.
---

# AI Agent Workflow Design

## Outcome

Produce a multi-step AI workflow whose state is serializable, whose stopping conditions are explicit, and whose irreversible steps require approval before they run, so a long task can be paused, resumed, inspected, and stopped without losing progress or acting without consent.

Use [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for the overall AI feature shape. Use this skill for the workflow inside it: who decides the next step, what state survives between steps, and where a human must approve.

## Required Inputs

- The task and its success criteria: what "done" means in a way that can be checked from tool results, not from the model's confidence.
- The tool set: each tool's schema, side effects, reversibility, and failure modes, with irreversible tools identified before design.
- The state the workflow needs across steps: inputs, intermediate results, decisions, and checkpoints, and how long each must survive.
- The budget: maximum steps, tokens, time, and cost per run, and what happens when each is hit.
- The approval surface: which steps need human approval, who approves, and how approval is recorded.

If there is no checkable success criterion, do not build an agent loop. A loop without a stopping test is a loop that runs until it runs out of budget.

## Workflow

1. Choose who decides the next step, and say so. In a graph or workflow, code decides: steps, branches, and retries are declared in advance, and the model fills in content within them. In a loop or agent, the model decides: it observes tool results and chooses the next tool until a stopping condition fires. The graph is more predictable and easier to test; the loop is more flexible for open-ended tasks. Do not present a loop as a workflow, or a workflow as an agent, because their failure modes and tests differ.
2. Make state explicit and serializable. Every step reads from and writes to a state record that can be inspected, checkpointed, paused, and resumed. Tool results are the source of truth for progress: the model must see the actual result before choosing the next step, not a summary that assumes success.
3. Set stopping conditions before the first run: task complete by the checkable criterion, maximum steps, maximum tokens or cost, maximum time, and a refusal or error state. Hitting a budget is a defined outcome with partial progress saved, not a crash and not a silent truncation.
4. Handle tool failure as a first-class path: retry with backoff for transient failures, fail loudly for deterministic failures, and save partial progress before either. A workflow that retries an irreversible tool on failure can double-charge, double-send, or double-create; mark irreversible tools non-retryable or idempotent by design.
5. Put human approval before irreversible steps, not after them. External actions, payments, messages, deletions, and publishing require approval at the step, with the exact action and its inputs shown to the approver, and the approval recorded. A prompt that says "be careful" is not approval, and a log entry after the fact is not consent. See [Agent Tool Safety](../agent-tool-safety/SKILL.md) and [AI Runtime Governance](../ai-runtime-governance/SKILL.md).
6. Keep the context bounded. Summarize or checkpoint intermediate state instead of appending every tool result forever, and record which facts were summarized, so a later step can re-fetch the source instead of trusting a summary. Unbounded context is a cost, latency, and accuracy failure that arrives gradually.
7. Observe every run as a trace: steps, tool calls, inputs, outputs, approvals, cost, and duration, per run. Without a trace, a failed multi-step task cannot be debugged, and a successful one cannot be reproduced.
8. Test with deterministic fixtures and failure injection: a run that succeeds, a run that hits each stopping condition, a tool that fails transiently and then succeeds, a tool that fails permanently, an approval that is denied, and a run that is paused and resumed. A workflow tested only on the happy path will fail in production in the ways its tests never covered.

## Safety and Permission Boundaries

- Treat model output as untrusted input to every tool. Validate tool arguments against their schemas, enforce allowlists, and never let the model choose a tool, a recipient, or a destination outside the approved set for that workflow.
- Never let an agent use credentials, tokens, or private data beyond the scope of its task, and never let it exfiltrate state through a tool whose output leaves the system. Tool outputs are reviewed at the boundary that applies.
- A new agent framework, tool library, or model still requires the root security-review gate at its exact version. This skill approves no provider, model, or package, and a framework's default approval behavior is not your approval policy.

## Outputs and Evidence

- A loop-or-graph decision, with the stopping conditions, budget, and state schema stated.
- A tool inventory with side effects, reversibility, retry policy, and approval requirements per tool.
- A trace and checkpoint design, with pause, resume, and partial-progress behavior.
- Tests or a test report covering success, each stopping condition, transient and permanent tool failure, denied approval, and pause and resume.
