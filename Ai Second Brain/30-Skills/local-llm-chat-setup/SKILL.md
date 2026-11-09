---
name: local-llm-chat-setup
description: Choose and run a local LLM runtime and chat interface, wire an OpenAI-compatible client, and keep inference local — knowing exactly when it is not. Use when setting up chat with a model on your own machine, picking a runtime or interface, or checking whether a "local" setup actually sends data anywhere.
---

# Local LLM Chat Setup

## Outcome

A working local chat setup whose data boundary is stated in plain terms: which model is running, where its inference runs, which runtime serves it, which interface talks to it, and what would have to change for any prompt or file to leave the machine.

## Supporting skills

Load only what the gap requires:

- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for provider and model selection and for the data-boundary decision across a whole feature.
- [AI Prompt Structured Output Design](../ai-prompt-structured-output-design/SKILL.md) for prompts, structured outputs, and tool calls once the client is wired.

## Alpha status

This skill is early draft material, and the tools it names change between releases. The research behind this skill was checked 2026-11-07; re-check the runtime, interface, and model documentation before relying on any detail, capability, port, or limit stated here. Model names, version numbers, and defaults are a 2026-11-07 snapshot and will date fast. Nothing in this skill is a promise that a particular runtime, interface, or model exists, works, or stays the same.

## Runtime vs interface: two different jobs

A model is not the runtime, and the runtime is not the interface. Keep the three apart in every setup, because each one can be swapped without changing the others:

- **Model:** the weights that do the generating — model families include Llama, Gemma, Qwen, Mistral, DeepSeek, and gpt-oss. A model name says what was loaded; it says nothing about how it is served.
- **Runtime:** the software that downloads, manages, and serves models over a local API. Examples checked 2026-11-07: Ollama (runtime plus CLI, desktop app, and server), llama.cpp (inference engine with `llama cli` for chat and `llama serve` for an HTTP server with a built-in web UI), LM Studio (GUI-first desktop app with a Developer tab server and an `lms` command-line tool), and TextGen, formerly text-generation-webui (desktop app for local models with chat, vision, file attachments, tool-calling, and MCP support).
- **Interface:** the chat window the user sees. Examples checked 2026-11-07: Open WebUI (self-hosted, ChatGPT-style web interface that connects to Ollama or to any OpenAI-compatible backend, and adds knowledge bases and multi-user features), LibreChat (self-hosted, multi-user chat platform unifying many providers and any OpenAI-compatible endpoint in one UI), and Jan (desktop ChatGPT alternative that runs local models and also connects to cloud providers with your own keys).

Ollama's own documentation lists Open WebUI and LibreChat under community chat integrations — the runtime-vs-interface split, confirmed by the runtime itself. A setup that names only "Ollama" or only "Open WebUI" is underspecified: record runtime, interface, model, and base URL together.

## Model and hardware fit

Local models are generally smaller and less capable than the largest hosted models for the same task. That is the trade for keeping inference on your own machine: no per-token bill, but you pay in hardware, electricity, download size and time, and in model quality. Pick the model for the task, then check the machine can actually run it:

- Start from the task, not the leaderboard: drafting and summarising tolerate a smaller model; long reasoning, code, and multi-step work need a larger or more capable one.
- Check the runtime's own hardware guidance for the model size you want before downloading. As one repo-stated example, Jan's guidance as fetched gives 8 GB of RAM for 3B models, 16 GB for 7B, and 32 GB for 13B — guidance for a decent experience, not a guarantee, and specific to that tool.
- Quantisation matters: llama.cpp supports reduced-precision (quantised) weights, which trade some quality for much lower memory. A quantised larger model and a full-precision smaller model are different choices; record which one was picked and why.
- Download size and time are part of the cost. A model that takes a long download and most of the machine's memory is not a casual swap; treat changing the model as a configuration change, with the new name and size recorded.

If the local model cannot do the task well enough, that is a reason to name a hosted model explicitly and accept the data leaving the machine — not a reason to quietly point the local interface at a hosted endpoint and keep calling the setup "local".

## Pulling and serving a model

The shape is the same across runtimes, even when the commands differ:

1. Install the runtime.
2. Pull or download the model through the runtime (or, for LM Studio and Jan, discover and download it from Hugging Face through the app).
3. Start the runtime's server, if it is not already running.
4. Point the interface or client at the server's base URL.
5. Send one test chat message and confirm the answer came from the model you intended, not from a different model or a fallback provider.

Keep model management in the runtime, not in application code. The runtime is what knows which models are pulled, which are running, and how much context they were started with. A client that tries to manage models itself duplicates that job badly.

## Base URLs and ports

Record the base URL in configuration, not in code, so the same client can point at a local or a hosted backend by changing configuration only. Defaults as checked 2026-11-07 — re-check them, because defaults change:

| Runtime | Default local API |
|---|---|
| Ollama | `http://localhost:11434` native API; OpenAI-compatible at `/v1` |
| LM Studio | `http://localhost:1234/v1`, OpenAI-compatible; also Anthropic-compatible |
| Jan | Local OpenAI-compatible server at `localhost:1337` |
| TextGen (full installs) | OpenAI/Anthropic-compatible API; web UI at `http://127.0.0.1:7860` |
| llama.cpp (`llama serve`) | OpenAI-compatible server; the port was not stated in the README excerpt fetched — check the command output or the runtime's docs for the install in use, do not guess one |

The de-facto integration shape across these runtimes is the OpenAI-compatible Chat Completions shape: `POST /v1/chat/completions` with a model name, a list of messages, and optional tools and streaming flags. Ollama also has a native API (`POST http://localhost:11434/api/chat`) and official Python and JavaScript packages; LM Studio offers its own REST API plus TypeScript and Python SDKs. Build against the OpenAI-compatible shape first, and keep a thin adapter for a native API only where it adds something the compatible shape does not — for example model management or pulling.

## The cloud-model trap

"Local app" does not automatically mean "no data leaves the machine". It depends on which model and provider is selected in that chat, not on which app window is open:

- Ollama's presentation now leads with a desktop-app and agent-launcher flow and offers cloud models alongside local ones. Jan likewise connects to cloud providers with your own keys alongside its local models. A local chat UI can also be pointed at a hosted endpoint.
- Before calling any setup local, check three things: which model is actually selected, where that model's inference runs, and whether the interface phones home for updates or telemetry. TextGen describes itself as having no telemetry; that claim was not independently verified in the research behind this skill.
- Default to local for anything sensitive, and to hosted only for a named reason — capability, speed, or a feature the local model lacks. Record the reason with the choice.

## Localhost binding: keep the API on the machine

A local runtime's API has no login by default. That is safe only while it stays on the machine:

- Ollama's API binds to 127.0.0.1:11434 by default. Setting it to listen on all interfaces exposes it to the local network, and forwarding its port to the internet exposes an unauthenticated model API to anyone who finds it.
- Keep the API bound to localhost unless there is a named reason to share it, and never port-forward 11434, 1234, 1337, or 7860 to the internet. The same rule applies to any other local runtime port: if the API has no authentication, the network boundary is the only access control, so do not widen it casually.
- A local-only setup needs no API key at all, which is a real advantage. Never put an API key in front-end code, in a URL, or in a shipped desktop app; keys live server-side or in the user's own environment or secret store.

## Failure handling, in order

Each failure has a different user-facing message. Handle them in this order, and say which one happened:

1. **No server running** — connection refused on the runtime's port. Tell the user to start the runtime; do not retry silently in a loop.
2. **Model not pulled** — the runtime answers but does not have the requested model. Offer to pull it, with its size shown, or to pick a model that is already present.
3. **Context overflow** — the request is larger than the model's context window. See the context-budgeting guidance in the integration skill linked below; do not silently drop the newest material.
4. **Stream abort** — the stream ends mid-sentence on error or cancellation. Keep the partial text visible, mark it as incomplete, and offer a retry.
5. **Tool-call output that does not parse** — the model returned tool-call JSON the application cannot use. Treat it as a failed generation, not as a tool result, and do not execute anything from it.

## Design checklist

Before calling a local chat setup finished, answer every line:

- [ ] Runtime, interface, model, and base URL are all recorded — not just the app name.
- [ ] The model fits the task and the machine, and the choice is written down with its reason.
- [ ] The base URL and model name live in configuration, not in code.
- [ ] The selected model's inference runs locally, or the hosted exception is named with its reason.
- [ ] The runtime API is bound to localhost, and no local API port is forwarded to the internet.
- [ ] No API key is in front-end code, in a URL, or in a shipped app; a local-only setup uses no key.
- [ ] Each failure in the handling list has a distinct user-facing message.
- [ ] The setup was verified with one test message from the intended model.

## Validation exercises

Use the hub projects below only as exercises — they are tutorial and demo starting points, not deployable systems. Run each exercise against a target you own, in a local-only setup, and compare what happens with this skill's checklist. Do not copy hub code, notebooks, or tutorial text into the vault.

- Run the hub's `local-chatgpt` as a reference implementation of the basic local-chat pattern: record its runtime, interface, model, and base URL, then check each line of the design checklist against it.
- Repeat with the hub's `local-chatgpt with DeepSeek`: swap in the DeepSeek model and note what changes (model name, download, hardware demand) and what stays the same (runtime, interface, base URL, client shape).
- Repeat with the hub's `local-chatgpt with Gemma 3`: same exercise with Gemma 3, and write down the cloud-model trap check for each of the three — which model is selected, where its inference runs, and whether anything in the setup reaches a hosted endpoint.

## State

This skill has not yet been exercised on a real local chat setup. Promote it only after at least one such exercise — runtime, interface, and model recorded, data boundary checked, and the checklist worked through — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
