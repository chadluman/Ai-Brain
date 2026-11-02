---
name: ai-streaming-web-design
description: Design streaming AI responses in a web UI, from token delivery to partial rendering, cancellation, and error recovery. Use when an AI feature streams text, tool progress, or partial results to the browser; do not use for transport selection alone, which is covered by Realtime Transport Selection, or for AI architecture, which is covered by AI Feature Architecture.
---

# AI Streaming Web Design

## Outcome

Produce a streaming experience where partial AI output is useful, cancellable, and recoverable: the user sees progress early, can stop a run, and never mistakes a partial or failed stream for a complete answer.

## Required Inputs

- The streamed content type: text, structured partial output, tool progress, or a mix, and what part of it is safe to show before completion.
- Latency and cost expectations: time to first token, total duration, token budget, and what happens when a budget or timeout is reached.
- Cancellation and recovery needs: can the user stop, retry, or resume, and what state survives a disconnect, reload, or navigation away?
- Accessibility and correctness needs: how partial, loading, and failed states are announced, and how a completed answer is distinguished from a partial one.

## Workflow

1. Choose the transport with [Realtime Transport Selection](../realtime-transport-selection/SKILL.md), not by fashion. Server-sent events usually fit server-to-browser text streams; a persistent socket fits bidirectional tool interaction. Record why the chosen transport fits the direction, latency, and reconnection needs.
2. Render partial output progressively, but mark it as partial until the stream completes and the output passes validation from [AI Prompt Structured Output Design](../ai-prompt-structured-output-design/SKILL.md). Do not store, act on, or present a partial result as final.
3. Make cancellation first-class: a visible stop control, server-side cancellation of the model call and any tool work, and a clear state after cancellation (partial output kept, discarded, or saved as a draft — chosen explicitly, not by accident).
4. Handle every stream failure as a state, not as a blank screen: network drop, model error, timeout, budget exhaustion, and validation failure each get a user-actionable message, a retry path where safe, and a non-AI fallback where one exists. Do not retry a non-idempotent tool action blindly after a disconnect.
5. Bound cost and duration on the server: token budget, timeout, rate limit, and per-user quota, enforced server-side, not in client code. Show cost-relevant progress (for example, that a run is still generating) without leaking provider internals or other users' usage.
6. Design for reload and navigation: decide whether a stream survives, resumes, or restarts, and what happens to partial output and any side effects. Persist only completed, validated results unless a draft model is explicitly defined.
7. Make partial and loading states accessible: announce status changes, preserve focus and reading order, and do not auto-scroll or replace content in a way that loses the user's place.

## Safety and Permission Boundaries

- Authenticate the stream and authorize each subscription and tool action. A connected client does not gain blanket access, and streaming does not bypass the authorization checks in the non-streaming path.
- Treat streamed output as untrusted until validated. Do not execute, store as fact, or act on streamed tool calls without the authorization checks in [Agent Tool Safety](../agent-tool-safety/SKILL.md).
- Streaming, token spend, and tool execution are R2/R3 actions where they apply. Enforce server-side budgets and require explicit authorization at consequential boundaries.
- Never stream secrets, other users' data, or internal reasoning that was not intended for display.

## Outputs and Evidence

- A stream state diagram: idle, streaming, partial, completed, cancelled, failed, and recovered, with the user-visible state and the server action for each transition.
- Tests proving cancellation stops server work, a dropped connection does not double-apply a tool action, and a partial stream is never presented as complete.
- A note recording transport choice, token budget, timeout, and the conditions that trigger re-evaluation, linked to [AI Runtime Governance](../ai-runtime-governance/SKILL.md) for ongoing operation.
