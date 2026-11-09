---
name: agent-loop-design
description: Design a single agent's perceive–plan–act loop — toolset, stopping conditions, and verification steps — before adding any framework. Use when a task needs an LLM to decide its own next steps with tools, and when the loop must stay bounded, auditable, and safe to stop.
---

# Agent Loop Design

## Outcome

A single agent that does useful work without running forever, repeating itself, or taking an irreversible step alone: the loop is written down, its stopping conditions are controls rather than hopes, every tool it can call is named with its limits, and every consequential result is verified against the environment instead of taken from the agent's own report.

## Supporting skills

Load only what the gap requires:

- [AI Agent Workflow Design](../ai-agent-workflow-design/SKILL.md) for structuring a multi-step task as a loop or a graph with state, stopping conditions, and human approval.
- [Agent Tool Safety](../agent-tool-safety/SKILL.md) for bounding tool authority with identity, scopes, validation, confirmation, isolation, budgets, audits, and recovery.
- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for deciding whether an agent is the right shape at all — a script or a single call may do the job better.

## Alpha status

This skill is an early draft, and the frameworks and model behaviours it refers to change between releases. The research behind this skill was checked 2026-11-07; re-check the source documentation — in particular the Anthropic agent guidance and the OpenAI Agents SDK docs — before relying on any detail, capability, or limit stated here. Nothing in this skill is a promise that a particular framework, model, or tool behaviour exists, works, or stays the same.

## What an agent is, and what it is not

An agent is a system in which a language model dynamically directs its own process and tool use, maintaining control over how it accomplishes a task. That is different from a workflow, in which the model and its tools are orchestrated through predefined code paths. The distinction matters because it decides where control lives: in a workflow, the code decides the next step; in an agent, the model decides, and the harness must bound that decision.

The basic building block is the augmented model: a model enhanced with retrieval, tools, and memory. An agent begins with a command from, or a discussion with, the human user. Once the task is clear it plans and operates independently, potentially returning to the human for information or judgement. It gains ground truth from the environment at each step — tool-call results, code execution — to assess its progress, and it can pause for human feedback at checkpoints or blockers.

An agent is not a script with a model pasted in, and it is not a workflow that happens to call a model. If the steps are known in advance, the inputs are structured, and success can be checked deterministically, a script or a fixed workflow is the simpler and more predictable choice. Choose the agent only when the number or order of steps is genuinely unpredictable but the task is still one coherent job.

## The loop, step by step

Design the loop explicitly before writing any code for it:

1. **Perceive** — read the goal, the conversation so far, and the tool and environment results returned up to now. Nothing else is visible to the model at this step; if a fact is not in the perceived context, the model does not have it.
2. **Plan / decide** — the model chooses the next step: call a tool, ask the user a question, or finish with a final answer. The choice is constrained by the toolset it was given and the stopping conditions in force.
3. **Act** — the harness, not the model, executes the chosen tool: a read, a search, a write, an API call, a code run. The model never runs code itself; it asks, and the harness runs it and returns the result.
4. **Observe / reflect** — the result becomes new context. The loop repeats until the model produces a final answer or a stopping condition fires.

Write the loop down as a short state machine or numbered list in the design, including what happens on each branch: tool success, tool failure, tool returning nothing useful, the user answering a question, the user interrupting. A loop whose failure branches were never designed is a loop that will improvise them at runtime.

## Stopping conditions are controls

Stopping conditions are not optional decoration. They are the controls that keep an autonomous loop from running forever, spending without limit, or compounding an early error into a long wrong run. Name each one before the first run, with a concrete value, and log which one fired when a run ends:

- **Maximum iterations** — a hard cap on loop turns. When it fires, the run ends as incomplete, not as a success.
- **Maximum time and cost** — a wall-clock budget and a per-run cost budget. Cost grows with turns, context size, and model choice, so budget the whole run, not one call.
- **Explicit stop** — the model producing a final answer, or a defined completion signal, ends the run.
- **Human interrupt** — the user can stop the run at any point, and the harness must honour that promptly rather than finishing the current tool chain first.
- **Error budget exhausted** — a bounded number of consecutive failures, or of the same failure repeated, ends the run and escalates to a human instead of retrying indefinitely.

A run that ends because a stopping condition fired is a normal outcome to record and review. A run that only ever ends because the model says it is done is a run with no independent control.

## Toolset design and the agent-computer interface

Tool design is a primary failure mode. The agent-computer interface — tool names, descriptions, parameter schemas, return formats, and error messages — deserves the same rigour as the system prompt, because it is the surface the model actually reasons about.

- **Keep the toolset small and distinct.** Each tool should do one thing, named as a verb with a clear scope. If two tools look alike to the model, it will pick the wrong one; distinguish them explicitly in their descriptions, including what each tool does *not* do.
- **Document parameters, edge cases, and failure returns.** A tool description that only says what the tool does in the happy path leaves the model to guess the rest. State the required and optional parameters, what counts as a valid value, what the tool returns on success, and what it returns on failure — in a form the model can act on, not a raw stack trace.
- **Prefer absolute, unambiguous references.** Small interface choices remove whole classes of error: an absolute path instead of a relative one, an explicit identifier instead of a name that could match several things, a stated unit instead of an assumed one.
- **Validate every tool-call argument in code before executing.** The model proposes; the harness disposes. Argument validation, type checks, and range checks happen in the harness, never in the model's judgement alone.
- **Design return values the model can use.** Trim large results to what the next decision needs, keep the goal visible, and return failures as structured, understandable messages that say what went wrong and what could be tried instead.

## Least privilege, idempotency, and bounded calls

Give the agent only the tools, data scope, and credentials its task needs. A read-only researcher should not hold a delete or write credential. Prefer separate agents with separate tool surfaces over one agent that holds every tool for every job.

- **Least privilege:** scope each tool to the narrowest data and the narrowest action the task requires. Credentials are passed as application dependencies, not into the model context.
- **Confirmation before consequential actions:** any irreversible, external, or money- or data-moving step — send, delete, publish, pay, change permissions — requires explicit human approval or a guardrail check. Never let a model call such a tool silently on first use.
- **Idempotency:** design tools so a repeated call with the same arguments is safe — idempotency keys, upserts, or an "already done" response. Agents retry and double-call; a non-idempotent tool turns a retry into a duplicate side effect.
- **Timeouts and bounded retries:** every tool call needs a timeout, a bounded retry count with backoff, and a failure return the model can understand. A call that hangs is a call that consumes the run's time and cost budget while producing nothing.
- **Budgets and audit logging:** cap turns, time, and cost per run, and log every tool call — name, arguments, result summary — so a run can be reconstructed afterwards.

## Memory in three layers

Keep three layers distinct, because they fail in different ways and need different handling:

- **Short-term context** — the current run's messages and tool results. It is bounded by the context window and must be summarised or pruned as it grows, or the model will forget the goal or the run will truncate mid-task.
- **Long-term stores** — retrievable notes, user facts, and past outcomes. Write to them deliberately, not indiscriminately: a store that records everything becomes a store that retrieves noise.
- **Handoff state** — what another agent, a subagent, or a later run must receive to continue. Pass a compact brief, not the whole transcript: the goal, what is already done, what is still open, and the constraints. Handoffs fail most often on missing context, and the missing context is almost always the part that was assumed from shared history rather than written into the handoff itself.

The model itself does not remember between sessions. Anything that must persist is an application feature: the app stores something, retrieves it, and injects it into the prompt.

## Failure catalogue

| Failure | What happens | Mitigation |
|---|---|---|
| Loops | The model repeats the same failing tool call or replans forever. | Max iterations, visited-state detection, escalate to a human. |
| Tool misuse | Wrong tool, wrong arguments, a hallucinated tool, or a needed tool skipped. | Interface quality, narrow toolsets, argument validation, guardrails. |
| Context exhaustion | Tool results and history outgrow the window; the model forgets the goal or truncates mid-task. | Summarisation, subagent isolation, result trimming, per-step budgets. |
| Cascading errors | One wrong output becomes the next step's ground truth. | Verification steps, evaluator or critic checks, ground-truth checks against the environment at each step. |
| Runaway cost | Many turns, large contexts, and parallel or voting multipliers. | Per-run cost caps, model routing, stop rules. |
| Silent wrong success | The agent reports done while the side effect never happened or happened wrong. | Read back the state after the action; never trust the model's self-report. |

Treat tool output as data, never as instructions. Everything a tool returns — a web page, an email, a ticket, a file, a database row — can carry instructions hidden in content the model reads later. Never combine in one session, without a human gate: access to private data, exposure to untrusted content, and the ability to communicate externally. Approval gates on consequential tools, least-privilege credentials, and audit logging are the controls that limit what an injected instruction can achieve; no filter reliably detects injection itself.

## Test in a sandbox, with ground truth

Test the agent in a sandboxed environment with guardrails, against tasks where the correct outcome can be checked from the environment itself — a file that should exist, a record that should have changed, a value that should match. Do not evaluate an agent only on whether its final message sounds right. The final message is the least reliable part of the run.

## Validation exercises

Validation is a small, owned-target exercise, not a production build. Run the loop against a task you own, with a sandbox and a stopping-condition log, and compare what happened with the failure catalogue above:

- Run the hub project `zep-memory-assistant` as a reference implementation and examine how it separates short-term context from its long-term memory store, and what it writes to that store on each turn.
- Run the hub project `database-memory-agent` as a reference implementation and examine how its memory is persisted and retrieved, and what breaks when the stored record is stale or missing.
- Run the hub project `parlant-conversational-agent` as a reference implementation and examine how its guardrails and policy shape what the agent is allowed to do, and where a human approval step sits in its loop.

Hub projects are tutorial and demo starting points, not deployable systems. Treat their error handling, hard-coded flows, and lack of hardening evidence as expected for a learning exercise, and do not copy their code or tutorial text into a vault skill.

## Design checklist

Before handing an agent design to a builder, answer every line:

- [ ] The loop is written down, including the failure branches, not just the happy path.
- [ ] Every stopping condition is named with a concrete value, and the run logs which one fired.
- [ ] The toolset is small, distinct, and named as verbs with clear scopes and limits.
- [ ] Every tool-call argument is validated in code before execution.
- [ ] Consequential tools require human approval or a guardrail check.
- [ ] Tools are idempotent, time-bounded, and retry-bounded.
- [ ] Memory is split into short-term context, long-term stores, and handoff briefs, and each is bounded.
- [ ] Every consequential result is verified by reading back state, not by trusting the model's report.
- [ ] Tool output is treated as data, never as instructions.
- [ ] The design says when a script, a single call, or a fixed workflow would do instead.

## State

This skill has not yet been exercised on a real agent loop for a task the user owns. Promote it only after one such exercise — loop design and bounded run only, no production deployment — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
