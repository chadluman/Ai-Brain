---
name: llm-application-integration-design
description: Wire messages, context budgets, streaming, and validated tool and function calls into one LLM application, so the model, the app, and the tools each do only their own job. Use when building or reviewing a chat or assistant feature that sends text to a model and acts on what comes back.
---

# LLM Application Integration Design

## Outcome

An LLM application in which the message list, the context budget, the streaming states, the tool-call loop, and the memory type are each explicit — so a wrong answer, a truncated prompt, or a bad tool call can be traced to the step that caused it instead of blamed on "the model".

## Supporting skills

Load only what the gap requires:

- [AI Prompt Structured Output Design](../ai-prompt-structured-output-design/SKILL.md) for prompt design, structured outputs, and tool-call schemas.
- [AI Streaming Web Design](../ai-streaming-web-design/SKILL.md) for streaming UI — partial rendering, cancellation, and error recovery in the browser.
- [AI Agent Workflow Design](../ai-agent-workflow-design/SKILL.md) for multi-step structure, stopping conditions, and human approval when one call becomes a loop or a graph.

## Alpha status

This skill is early draft material, and the APIs it names change between releases. The research behind this skill was checked 2026-11-07; re-check the provider API reference and the runtime documentation before relying on any detail, role name, limit, or behaviour stated here. Model names, version numbers, and defaults are a 2026-11-07 snapshot and will date fast. Nothing in this skill is a promise that a particular API shape, role, or limit exists, works, or stays the same.

## The application, not the model, runs the app

An LLM application is ordinary software that sends text to a large language model and does something useful with the text that comes back — chat, summarising, drafting, code help, question-answering over documents. The model itself does not run the app, store files, or call tools on its own; the app around it does that. Keep that split in mind whenever a design says "the model will handle it": if the job is storing, calling, checking, or deciding with consequences, it belongs in code, not in a prompt.

## Message roles, including the developer and system change

A chat request is a list of messages with roles. The roles in common use are:

- **`developer` / `system`:** developer-provided instructions the model should follow regardless of what the user types. With newer OpenAI models (o1 and newer), `developer` messages replace the previous `system` messages, according to the OpenAI API reference as checked 2026-11-07. Older models and other providers still use `system`. Check the API reference for the exact model in use before choosing, and do not mix the two roles in one request without knowing which one the model honours.
- **`user`:** what the user typed, including anything they pasted in.
- **`assistant`:** what the model said before, kept so the conversation continues.
- **`tool`:** the result of a function the model asked the application to run, sent back as a new message so the model can produce a final answer.

Treat the system or developer prompt as configuration, not as a security control and not as a secret. Anything the model must never do should also be enforced in code. Instructions in a prompt are not an access control, and a prompt that is assumed secret will leak eventually — through the model repeating it, through logs, or through a tool result that echoes it.

Mark untrusted content clearly when it is injected into a prompt — with delimiters, source labels, or both — and never concatenate system instructions and untrusted pasted content into one undifferentiated block. Pasted text, retrieved documents, web pages, emails, and files can all carry instructions the model will read as if they were part of the task. The model cannot tell, on its own, which text is instruction and which is data; the application has to mark the boundary for it.

## Context budgeting and silent-truncation defence

The context window is the total amount of text, measured in tokens, the model can see in one request. It is a budget, and every part of the request spends from it:

- System or developer prompt.
- Conversation history.
- Retrieved documents, where retrieval is used.
- Tool definitions — every tool schema consumes context, which is one reason to keep toolsets small.
- The new user message.

Anything beyond the window is truncated or rejected, depending on the provider or runtime — and truncation can be silent. Open WebUI's Ollama guide makes the practical point concrete: a context that is too small silently truncates the prompt, and at a small context size a model can run out of room and return a blank response or raw tool-call JSON. A blank answer or a JSON fragment in the chat window is often a context problem, not a model failure.

Defend the budget deliberately:

- Keep a written budget for a request: how much goes to the system prompt, how much to history, how much to retrieved chunks, how much to tools, and how much is left for the new message and the answer.
- Summarise or drop old turns instead of letting the window silently truncate the newest, most relevant material. Dropping the oldest history first is the usual shape; summarising it first preserves more, at the cost of a summarisation call.
- Watch the budget as history grows. A conversation that worked at turn three can overflow at turn thirty, and the failure will look like the model suddenly getting worse.
- Where the runtime allows it, set the context size explicitly rather than relying on a default that may be picked from available memory. Ollama's default context length, for example, is set server-side and a per-request override exists — check the runtime's documentation for the install in use before relying on a particular default.

## Streaming states

Streaming returns the answer token by token as it is generated instead of waiting for the whole answer. It is a user-experience and latency pattern, not a capability change: the same tokens arrive, just earlier. The application must therefore handle states a non-streaming call never shows:

- **Partial output:** tokens arrive incrementally and are rendered as they come. Render them as a draft in progress, not as a finished answer — a partial sentence is not a claim yet.
- **Cancellation:** the user stops the stream. Stop the request, keep the partial text visible and marked as stopped, and do not present it as complete.
- **Error mid-stream:** the stream ends mid-sentence on error. Keep the partial text, mark it as incomplete, and offer a retry. Do not silently discard it and do not silently present it as finished.
- **Thinking traces, where the runtime returns them:** since Ollama v0.9.0, models with thinking support return the trace in a separate `thinking` field, shown collapsibly. A visible thinking trace is not evidence the answer is correct — evaluate the final answer. Do not log or display raw thinking content to end users without checking what the provider returns and whether it can leak prompt or tool data.

The exact transport for a provider's streaming endpoint was not confirmed on a primary page in the research behind this skill; do not assume a particular transport for a provider until its API reference is checked.

## The tool-call loop, with argument validation

Tool calling, also called function calling, lets the model ask the application to run a function. The loop is:

1. The developer describes each function with a name, a description, and a JSON Schema for its parameters.
2. The model returns a structured tool-call object with arguments — it does not run the function itself.
3. The application runs the function and sends the result back as a new `tool` message.
4. The model then produces a final answer from that result.

The model never runs code itself. Everything that happens in step 3 is the application's responsibility, and the application is where the safety lives:

- **Validate every tool-call argument in code before executing** — types, ranges, and allow-lists. Never pass model output straight into a shell command, a SQL string, or a privileged API. A tool-call argument is untrusted input until the application's own checks pass it.
- **Keep tool schemas small and few.** Every tool definition consumes context and increases the chance of a wrong or hallucinated call. The OpenAI API reference states a maximum of 128 functions; that ceiling is a limit, not a target. Fewer, well-described tools beat a long list of vaguely described ones.
- **Design the tool surface as a user interface.** Tool names, descriptions, parameter schemas, return formats, and error messages are what the model sees of your system. A tool that is unclear about what it does, what it needs, and what it does not do will be called wrongly — and the failure will look like a model error.
- **Give every tool call a timeout, a bounded retry count, and a failure return the model can understand.** A tool that hangs, or that fails with a raw stack trace, gives the model nothing useful to act on.
- **Treat every model output as untrusted input to the next step.** Enforce authorisation in code downstream of the model: the model proposes, code disposes. Least privilege for tools, and human approval for high-impact actions — anything irreversible, external, or money- or data-moving.
- **Test with adversarial prompts,** including pasted text containing instructions to ignore previous instructions, and treat the model as an untrusted user in that test. Prompt injection is the top-ranked LLM-application risk in the OWASP GenAI Top 10 for LLM Applications (2025), and its damage is usually agentic — injected text driving a tool call — not merely textual.

## Memory, named by type

The model itself does not remember between sessions. Memory is an application feature, and it comes in different kinds that fail in different ways. Name the kind in any design instead of saying "the model remembers":

- **History (in-context memory):** conversation history re-sent on every request, bounded by the context window, lost when the history is dropped. Its failure mode is context exhaustion — see the budgeting section above.
- **Summary:** a condensed record of earlier turns, written by the application and injected into the prompt. Its failure mode is a stale or wrong summary becoming the model's ground truth; version it and say when it was written.
- **Retrieved fact:** a stored note, user fact, or past conversation retrieved from a store and injected into the prompt. Its failure mode is retrieving the wrong fact, or a fact the current user should not see; filter at retrieval time, never by prompt instruction.
- **Handoff state:** what another agent, worker, or session must receive to continue — goal, what is already done, what is still open, and constraints, passed as a compact brief, not as a whole transcript. Its failure mode is missing context: include the brief in the handoff itself, not assumed from shared history.

LibreChat's manual context compaction and context-usage inspection are a concrete example of an application managing history explicitly rather than letting it overflow silently. Whatever the mechanism, the rule is the same: the application stores something, retrieves it, and injects it — the model remembers nothing on its own.

## Design checklist

Before calling an LLM application integration finished, answer every line:

- [ ] Message roles are explicit, and the `developer` vs `system` choice matches the model in use.
- [ ] The system or developer prompt is treated as configuration, not as a secret or a security control.
- [ ] A written context budget exists (system + history + retrieval + tools + new message), with a summarise-or-drop rule for old turns.
- [ ] Silent truncation is defended against: the app detects or prevents it rather than showing a blank answer or raw tool-call JSON.
- [ ] Streaming handles partial output, cancellation, and mid-stream error as distinct, visible states.
- [ ] Every tool-call argument is validated in code before execution; no model output goes straight into a shell, SQL, or privileged API.
- [ ] Tool schemas are small and few, with clear names, descriptions, and stated non-goals.
- [ ] Every tool call has a timeout, a bounded retry count, and a failure return the model can understand.
- [ ] Memory is named by type (history, summary, retrieved fact, handoff state) in the design, not described as "the model remembers".
- [ ] The integration was tested with adversarial prompts, including pasted instructions to ignore previous instructions.

## Validation exercises

Use the hub projects below only as exercises — they are tutorial and demo starting points, not deployable systems. Run each exercise against a target you own and compare what happens with this skill's checklist. Do not copy hub code, notebooks, or tutorial text into the vault.

- Run the hub's `streaming-ai-chatbot` as a reference implementation of token-by-token streaming chat: drive it through each streaming state — partial output, cancellation, and an error mid-stream — and record what the UI shows in each case against the streaming section above.
- Run the hub's `deepseek-thinking-ui` as a reference implementation of a chat UI that shows the model's reasoning trace visibly: check where the thinking trace is shown, whether it is separated from the final answer, and whether anything in the UI treats the trace as evidence the answer is correct.

## State

This skill has not yet been exercised on a real LLM application integration. Promote it only after at least one such exercise — messages, context budget, streaming states, tool-call loop, and memory type all checked against a real integration — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
