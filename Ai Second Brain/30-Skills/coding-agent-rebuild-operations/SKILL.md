---
name: coding-agent-rebuild-operations
description: Drive a rebuild engine from the CLI and MCP, connect a coding agent to it, and keep approvals and project records straight. Use when running a rebuild from the command line or through a coding agent, and when setting up, checking, or troubleshooting that connection.
---

# Coding Agent Rebuild Operations

## Outcome

A rebuild engine driven the same way from any front end — desktop app, command line, or coding agent — with the right agent connected, approvals handled by a person where they matter, and every project recorded in a folder a second machine can pick up and continue.

## Supporting skills

Load only what the gap requires:

- [Agent and Tool Safety](../agent-tool-safety/SKILL.md) for bounding agent and tool authority: identity, scopes, validation, confirmation, isolation, budgets, audits, and recovery.
- [Clean Room Rebuild Design](../clean-room-rebuild-design/SKILL.md) for the mode the engine runs in and what each mode refuses.
- [Evidence-Led Software Study Design](../evidence-led-software-study-design/SKILL.md) for the study records the engine keeps.
- [Open Source License Review](../open-source-license-review/SKILL.md) for the engine's licence position in general terms: dual-licensed under two permissive licences, with trademarks and bundled assets keeping their own terms.
- [Desktop App Distribution Design](../desktop-app-distribution-design/SKILL.md) for signed, verified desktop distribution; do not restate its signing guidance here.

## Alpha status

The engine this skill describes is early alpha, and its behaviour changes between releases. The research behind this skill was checked 2026-11-05; re-check the source repository before relying on any detail, command, or limit stated here. Agent support is uneven — which agents have actually been run live is stated below, and anything not listed as run live must not be presented as verified.

## One engine, three ways to drive it

The desktop app, the command line, and the MCP server all drive the same engine. Choose the front end by the job:

- **Desktop app:** the simple path — describe what to make, press start, watch the four steps, answer question and approval cards, and open the result or its folder. An advanced workbench shows every tool, the evidence, the unknowns, the jobs, the logs, and the agent console.
- **Command line:** every inspection tool is also a subcommand, so an agent or a script can study a target or run a whole rebuild without the app, and without any AI for inspection alone.
- **MCP server:** the same tools served to any MCP client, so a coding agent can call them as tools. The server runs in the build's mode; in Deep mode it lists every tool.

A limitation to plan around: a website capture keeps its private browser for one session, so from the command line — where each command is a session of its own — a later capture finds no open site. Run the open and the capture together in an MCP client, in the app, or inside a rebuild.

## Commands and project layout

The public command names to know:

- `rebuild` — study a target and have a coding agent rebuild it in a new project folder. It takes the target (or a dash for a from-scratch request), the request in words, and options for refinement rounds, continuing in an existing folder, editing an existing folder, generating assets for new projects, choosing the agent, choosing the backend, and picking Deep or Clean room mode.
- `mcp` — serve the tools to an MCP client, with options to offer every tool, to post questions and approvals into an inbox folder, and to set the active target.
- `doctor` — check the install, the agent registrations, the engines, the AI backends, and the MCP server, and say what is missing.
- `setup` — connect the engine to coding-agent apps. `uninstall` removes those registrations again.
- `commands` and `capabilities` — list every tool, and what this install can do.
- `triage`, `report`, `chat`, and `ai` — open a file for a first look, write a readable investigation report, ask the agent a question about a target, and manage AI backends.

Each project lives in its own folder, by default under a documents folder for the engine, changeable in settings. A project folder holds:

- `craft.json` — the request, target, status, and history.
- `capture/` — what was recorded from the target.
- `app/` — the generated project.
- `checks/` — each comparison against the original, including a game's self-test record.
- `investigation.cany/` — the evidence for the project.
- `inbox/` — open questions, including the record of how many unchanged builder turns have passed.
- Alongside those: attachments, per-build AI cost and token usage, the builder's conversation transcript, the project feed, a build-activity log, the questions record, pinned builds, and a copy of the builder's session — so a project copied to another computer keeps building with the same agent.

A project can also start in a folder you pick. If that folder already has files, say what they are: the app itself, which the builder edits in place, or material to start from, with the app built beside it. Removing a project from the list only takes it off the list.

## Which coding agent, and what is actually verified

Building needs a coding agent signed in on the computer. `doctor` says what is missing. The agents differ sharply in how much of this has actually been run:

- **Claude Code — supported first.** The engine runs the person's own, unmodified coding-agent program, using their own sign-in; it never sees or handles the account. Before a build it checks the agent is signed in and stops with a sign-in instruction if it is not. In Deep mode its read tools and the engine's tools are pre-allowed; in Clean room only its task-list tool is pre-allowed and reads go through the approval tool too, which refuses anything in the original's folder or on its site, except the project folder. Every other action — writing files, running commands, fetching the web — goes through the approval tool, which allows edits inside the app folder and a fixed list of build commands, refuses long-running dev servers, and asks the person for anything else. Its own question tool is disabled; the agent asks the person through the engine's question card instead.
- **Codex — adapter exists, not verified on a real install.** Setup writes the agent's config with the engine as an MCP server, keeping a backup of the old file. Startup tool discovery was checked with a loopback model, not a real account, and no real-account build has been run. Do not present Codex as a verified builder.
- **Copilot via ACP — partly verified.** The Copilot CLI is installed through ACP and signed in separately; the CLI owns its own authentication and credential store, and the engine does not read it, collect a key, or provide a login flow. Only an explicit allowlist of engine tools is exposed; the agent's native file, shell, web, and delegation tools are not. Authenticated builds and session resume rest on the maintainer's report that the person using the app confirmed them — not on independently observable evidence. Treat them as reported, not verified.
- **Other ACP agents — only Maki has been run live.** Gemini, Qwen, opencode, goose, and Hermes agents can be switched to ACP per backend, but of those only Maki has been run live for a build. Do not present the others as verified builders. OpenCode model discovery works, but running with an explicit model selection is currently refused until native MCP integration exists; local ACP runs require clearing the selection.
- **API-key backends — never run live for builds.** Key-based providers and local compatible servers are available for questions and analysis, and they build with the engine's own loop — but no live API-key build has been run yet. Do not present one as verified. Local-model builds are the largest open gap: repeated runs of a small test program still ended with the build failing its screenshot check at the round limit.

The terms position for orchestrating a person's own agent program is the maintainers' own reading of the agent vendor's published pages as of October 2026, with confirming it with the vendor listed as an open question before any paid offering. Treat it as their position, not settled advice.

## Approvals, Auto mode, and the dependency-install risk

Questions and approvals are a file inbox per project; questions, action approvals, and MCP consent requests become cards in the app for the person to answer.

- **Auto mode** is on by default: builder actions go ahead without asking, except a fixed set that is never done unasked — deleting outside the project, system changes, publishing, and similar. Questions get decided by the agent itself, and asset spending stops at the budget.
- **Approval reach differs by agent.** In Clean room, Claude Code chats start with its own file and changing tools disallowed, so it works only through the engine's tool server. Other agents in chats keep whatever sandbox they have, if any — they are not held to the same rule. Some agents can turn their approvals off entirely, and some plain command forms never ask at all. Never assume an approval rule reaches an agent you have not checked.
- **Installing dependencies runs code.** When a builder installs a project's dependencies, the commands run on the computer, and the packages can run code while they install — install scripts, build scripts, and setup code all run as part of the install. The engine asks before a command of a kind it has not seen in this project. Choosing "always allow" for a package manager lets every later command from it run without asking, so do that only for a project whose dependencies are trusted. Prefer installing without install scripts when that option exists.

## Plugins and licences, in general terms

Any MCP server, local or remote, can add tools without changing code; a plugin added through the tool or the app always asks before each call by default, because it runs someone else's code. Browser-based plugin components can add tools and checks when the optional plugin feature is enabled, with fuel and memory limits and a fresh instance per call.

The engine is dual-licensed under two permissive open-source licences, at the user's option. Trademarks are not covered by that licence: the project's name, wordmark, and logos may only be used unmodified, only as part of the project itself, and never to suggest endorsement of anything else — forks must remove them. Bundled assets keep their own licences, listed file by file in the project's attribution record. State the licence only in these general terms; do not reproduce licence text here.

## Operations checklist

Before driving a rebuild, answer every line:

- [ ] `doctor` has been run and reports the engine, the chosen agent, and the MCP server as ready.
- [ ] The chosen agent is signed in under its own account, and the engine has never been given its credentials.
- [ ] The agent's verification status is stated honestly: Claude Code run live, Codex unverified, Copilot partly verified, only Maki run live among the other ACP agents, API-key builds never run live.
- [ ] The mode (Clean room or Deep) is set for the run, and the person knows Clean room is a refusal rule, not an operating-system sandbox.
- [ ] Auto mode and its never-unasked set are understood, and "always allow" has not been granted for a package manager on an untrusted project.
- [ ] The project folder layout is known, and the inbox is where questions and approvals will appear.
- [ ] Any plugin added asks before each call, and its code is treated as someone else's code.

## State

This skill has not yet been exercised on a real rebuild run driven from the CLI or MCP with a coding agent. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.

Draft pending representative validation.
