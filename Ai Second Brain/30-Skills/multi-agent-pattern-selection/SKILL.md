---
name: multi-agent-pattern-selection
description: Choose between a single call, a fixed workflow, a single agent, and a multi-agent pattern — supervisor, swarm, planner/orchestrator-workers, debate/critic, or sequential crew — and know when multi-agent is not justified. Use when a task has several parts and the question is how many agents it needs, not just which framework to use.
---

# Multi-Agent Pattern Selection

## Outcome

A pattern choice that can be defended in one sentence: the number of agents, what each one owns, how they hand work to each other, and which single-agent or fixed-workflow option was ruled out and why. The choice names its own failure modes before building starts, and it does not add agents to a task that a simpler shape would already answer.

## Supporting skills

Load only what the gap requires:

- [AI Agent Workflow Design](../ai-agent-workflow-design/SKILL.md) for structuring a multi-step task as a loop or a graph with state, stopping conditions, and human approval.
- [Agent Tool Safety](../agent-tool-safety/SKILL.md) for bounding tool authority with identity, scopes, validation, confirmation, isolation, budgets, audits, and recovery.
- [Agent Loop Design](../agent-loop-design/SKILL.md) for the single-agent loop itself — toolset, stopping conditions, and verification steps — before a second agent is added.

## Alpha status

This skill is an early draft, and the frameworks and model behaviours it refers to change between releases. The research behind this skill was checked 2026-11-07; re-check the source documentation for any framework named here — in particular its current maintenance status, version, and docs version — before relying on any detail, capability, or limit stated here. Nothing in this skill is a promise that a particular framework, model, or pattern behaviour exists, works, or stays the same.

## The decision ladder: start simple, earn complexity

Agentic systems trade latency and cost for better task performance, and for many applications optimising a single model call with retrieval and in-context examples is usually enough. Climb the ladder only when the step below has been shown inadequate for the task at hand:

1. **Single call** — one retrieval plus one generation answers the question. Use it when the answer is in the retrieved context and no tools or follow-up steps are needed.
2. **Fixed workflow** — predefined code paths: prompt chaining, routing, parallelisation by sectioning or voting, orchestrator-workers, evaluator-optimizer. Use it when the steps are known in advance, the inputs are structured, and success can be checked deterministically. Workflows offer predictability and consistency; they are the right default for well-defined tasks.
3. **Single agent** — one loop, one toolset, with the model directing its own steps. Use it when the number or order of steps is unpredictable but the task is one coherent job. It is debuggable and the cheapest agentic shape.
4. **Multi-agent** — several agents with separate ownership. Use it only when a specific, nameable need forces it — see "When multi-agent is justified" below — and never as the starting point.

Frameworks often create extra layers of abstraction that obscure the underlying prompts and responses, making them harder to debug, and they can make it tempting to add complexity when a simpler setup would suffice. Treat the ladder as a discipline: every step up must be justified by a need the step below cannot meet.

## When multi-agent is justified — and when it is not

Add more agents only when you need separate ownership, different instructions, different tool surfaces, or different approval policies — and you can name which one before building. The concrete justifications are:

- **Separate ownership:** distinct parts of the task belong to distinct roles with distinct success criteria.
- **Separate tool or approval surfaces:** one role needs a credential or a consequential tool that another role must never hold.
- **Context isolation:** one role's working context would swamp another's, so each needs its own bounded context.
- **Genuine parallelisation:** independent subtasks can genuinely run at the same time and their results can be combined afterwards.

Multi-agent is **not** justified when the task is one coherent job with one toolset, when the steps are known in advance, when the only reason is that the task "feels big", or when no one can say which of the four justifications above applies. If the answer is "it might help", the answer is no — build the single-agent or workflow version first, measure where it actually fails, and let that failure choose the pattern.

## The patterns, with fit and failure modes

### Single agent with tools

One loop, one toolset. The best fit for most tasks: debuggable, cheapest, and the easiest to bound with stopping conditions. Watch out for context bloat as tools and results accumulate, and for the single toolset growing until it holds tools the task never needed.

### Planner / orchestrator–workers

A central model decomposes the task, delegates subtasks to workers, and synthesises the results. A good fit when subtasks are unpredictable in advance — multi-file coding, multi-source research — and the decomposition itself needs judgement. Watch out for the orchestrator becoming a bottleneck and a single point of confusion: if its decomposition is wrong, every worker inherits the error.

### Supervisor

A star shape: one supervisor agent controls all communication flow and task delegation, workers return their results to the supervisor, and the supervisor decides what happens next. A good fit when specialist roles are clear and each worker needs a different tool or approval surface. Watch out for the supervisor prompt being load-bearing — routing errors cascade, and a supervisor that misunderstands the task misroutes every worker.

### Swarm / handoff

Agents dynamically hand off control to one another based on specialisation, with the system remembering which agent was last active. A good fit for conversational triage and peer specialists, where the next agent depends on what the last one found. Watch out for the lack of a central view: loops and ping-pong handoffs, where two agents hand the same task back and forth, and no one owns the outcome.

### Debate / critic (evaluator–optimizer, reflection)

A generator produces an answer and an evaluator or critic checks it, in a loop. A good fit when quality matters and the criteria are checkable — the critic needs something real to check against. Watch out for cost multiplying per round, the evaluator being wrong too, and the loop needing a real stop rule, or it will argue with itself until the budget runs out.

### Sequential crew / pipeline

A fixed order: each step consumes the previous step's output. A good fit when the decomposition is well understood and each step's input and output are defined. Watch out for brittleness: if an early step is wrong, every later step builds on the error, and there is no dynamic replanning to recover.

| Pattern | Shape | Good fit | Watch out for |
|---|---|---|---|
| Single agent + tools | One loop, one toolset | Most tasks; debuggable, cheapest | Context bloat as tools/results accumulate |
| Planner / orchestrator–workers | Central model decomposes, delegates, synthesises | Subtasks unpredictable in advance | Orchestrator becomes a bottleneck |
| Supervisor | Star: one supervisor dispatches to workers | Clear specialist roles, different tool/approval surfaces | Supervisor prompt is load-bearing; routing errors cascade |
| Swarm / handoff | Any agent hands off to any other | Conversational triage, peer specialists | No central view; loops and ping-pong handoffs |
| Debate / critic | Generator + evaluator/critic in a loop | Quality matters and criteria are checkable | Cost multiplies per round; evaluator can be wrong too; needs a real stop rule |
| Sequential crew / pipeline | Fixed order, each step consumes the last | Well-understood decomposition | Brittle if an early step is wrong; no dynamic replanning |

## Handoffs are the shared mechanism — and the shared failure

Handoffs appear in supervisor, swarm, and crew shapes alike: one agent delegates the whole conversation to a specialist, or one agent calls another as a tool. Handoffs fail most often on missing context. A handoff must carry, in the handoff itself and not assumed from shared history: the goal, what is already done, what is still open, and the constraints. Pass a compact brief, not the whole transcript — and pass it explicitly, because the receiving agent does not share the sender's context.

Cascading errors are the multi-agent version of the same failure: one worker's wrong output becomes the next worker's ground truth. Mitigate with verification steps, evaluator or critic checks, and ground-truth checks against the environment at each step — not only at the end, when the error has already propagated through every agent after it.

## Framework choice, with current status warnings

Choose the pattern first and the framework second. A framework does not fix a wrong pattern; it only implements it faster. The frameworks below were checked 2026-11-07 and their status is a snapshot — re-check before adopting any of them:

- **LangGraph** — low-level orchestration: stateful, cyclic, multi-step agent workflows as graphs, with prebuilt supervisor and swarm libraries. The official multi-agent page redirected when checked 2026-11-07, so the supervisor and swarm claims rest on the reference docs and a repo mirror, not the live page. Verify the current docs before building on it.
- **CrewAI** — opinionated role-based orchestration: agents, tasks, and crews, plus Flows for deterministic, event-driven control. The docs' own guidance is to start with a Flow and delegate a complex task to a Crew inside it. Version drift is real: docs URLs seen span several minor versions, and the first-crew tutorial changed from a YAML-first to a JSON-first crew definition. Pin the docs version when following a tutorial.
- **AutoGen (Microsoft)** — conversational multi-agent apps on an event-driven core, with group chat and a reflection pattern (primary agent plus critic). **Status warning: AutoGen is in maintenance mode** on current secondary evidence — multiple secondary sources quoting the project README state it will not receive new features or enhancements and is community managed going forward, and that new users should start with Microsoft Agent Framework instead. The live AutoGen docs site itself does not prominently carry that notice on the pages opened. Treat "use AutoGen for new work" as not recommended on current evidence; verify the README notice directly before advising anyone to adopt it.
- **Microsoft Agent Framework** — the successor to AutoGen and Semantic Kernel, for enterprise multi-agent orchestration with graph-based workflows. **Status warning: its release dates are unverified** — secondary sources conflict on when its public preview and 1.0 releases fell. Do not quote a general-availability date without opening the official Microsoft Learn pages.
- **OpenAI Agents SDK** — a lightweight SDK with few primitives: agents, handoffs and agents-as-tools, guardrails, sessions, tracing, and voice. Its own framing is as a successor to the earlier Swarm experiment, with guardrails and approvals built in.
- **Claude Agent SDK** — the agent loop, tools, and context management of Claude Code as a library, with built-in file tools, a permissions model, subagents, and MCP integration. Subagents provide context management and parallelisation under a main agent.
- **n8n** — visual workflow automation with an AI Agent node (a chat model plus tool sub-nodes, optional memory and output parser) inside a workflow, and a newer standalone Agents feature reported as preview in late 2026. Node-based, not code-first; its AI Agent node can require approval before running a specific tool.

When comparing frameworks, compare what the pattern needs: state handling, handoff mechanics, guardrail and approval support, tracing, and how easily the prompts and tool calls underneath can be inspected when something goes wrong. Do not compare on marketing claims, and do not treat a framework's tutorial as evidence that the pattern fits your task.

## Cost and control multiply with agents

Every additional agent multiplies the single-agent failure catalogue: more turns, more context, more tool calls, more chances for a cascading error, and more cost per completed task. Budget per run, not per agent: a per-run cost cap, a model-routing choice (a smaller model for easy steps), and stop rules that apply to the whole system, not just to one agent. Log handoffs as well as tool calls, so a run can be reconstructed across agents afterwards. And keep the human approval gates where they were for a single agent — consequential tools still require explicit approval, and the approval policy may differ per agent, which is itself one of the reasons to split agents in the first place.

## Validation exercises

Validation is a small, owned-target exercise, not a production build. Pick one task you own, build the single-agent version first, note where it actually fails, and only then choose a multi-agent pattern for that specific failure — then compare the two runs:

- Run the hub project `hotel-booking-crew` as a reference implementation and examine how its crew divides the booking task between agents, what each agent owns, and where a wrong result from one agent would reach the next.
- Run the hub project `flight-booking-crew` as a reference implementation and examine the same division for a booking workflow, and whether a fixed sequential pipeline would have answered the same task with less machinery.
- Run the hub project `autogen-stock-analyst` as a reference implementation of the AutoGen API only, with the maintenance-mode warning above in force — it teaches the AutoGen API, it is not a current recommendation for new work, and any framework choice built on it must be re-checked against the project README first.
- Run the hub project `omnigraph-multi-agent` as a reference implementation and examine how its agents are orchestrated, and where the orchestration itself could become the bottleneck.
- Run the hub project `agent2agent-demo` as a reference implementation and examine agent-to-agent communication as a pattern distinct from MCP: what the agents exchange, and what happens when one side misunderstands the other.

Hub projects are tutorial and demo starting points, not deployable systems. Treat their error handling, hard-coded flows, and lack of hardening evidence as expected for a learning exercise, and do not copy their code or tutorial text into a vault skill.

## Selection checklist

Before building a multi-agent system, answer every line:

- [ ] The single-call and fixed-workflow options were tried or explicitly ruled out, with a reason.
- [ ] The single-agent version was built first, and its actual failure chose the pattern.
- [ ] The justification for multiple agents is named: separate ownership, separate tool/approval surfaces, context isolation, or genuine parallelisation.
- [ ] The pattern is named, with its fit and its failure modes written down.
- [ ] Every handoff carries goal, done, still open, and constraints in the handoff itself.
- [ ] Verification or critic steps sit at each stage, not only at the end.
- [ ] Per-run cost, time, and iteration budgets cover the whole system, not one agent.
- [ ] Human approval gates still apply to consequential tools, per agent.
- [ ] The framework choice was re-checked on the day of the decision, including maintenance status and docs version.
- [ ] The design says what would make you go back to fewer agents.

## State

This skill has not yet been exercised on a real multi-agent choice for a task the user owns. Promote it only after one such exercise — single-agent first, then the chosen pattern, compared on the same task — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
