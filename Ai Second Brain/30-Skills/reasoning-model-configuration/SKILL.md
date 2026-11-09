---
name: reasoning-model-configuration
description: Configure reasoning effort and verbosity per task for a reasoning model — thinking budgets, cost and latency tradeoffs, and when extra thinking wastes tokens — so a task gets the lowest effort that passes its evals and no more.
---

# Reasoning Model Configuration

## Outcome

A reasoning setting chosen deliberately for each task: the model thinks as much as the task needs, the cost and latency of that thinking are visible before the change ships, and the choice is recorded with the eval result that justified it — not copied from another model's guide or left at a default nobody examined.

## Supporting skills

Load only what the gap requires:

- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for the eval set and the before/after comparison that decides whether a higher effort actually helped.
- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for whether a reasoning model is the right choice for the feature at all, versus a simpler call, retrieval, or a different model.
- [Fine-Tuning Decision and Eval](../fine-tuning-decision-and-eval/SKILL.md) when the behaviour needed is narrow and repeated enough that tuning, rather than more thinking per call, is the cheaper fix.

## Alpha status

The controls this skill describes change between model releases: effort names, defaults, minimum budgets, and which models accept which control all move. The research behind this skill was checked 2026-11-07; re-check the model page for the exact model in use before relying on any value, default, or limit stated here. Nothing in this skill is a promise that a particular control exists, works, or stays the same.

## Test-time compute, in plain terms

A reasoning model spends extra work at answer time — test-time compute — generating intermediate thinking tokens before it produces its visible answer. More thinking can improve accuracy on multi-step work such as maths, code, and planning, where the answer is reached by a chain of steps. It does not add knowledge the model does not have, and it does not make a lookup, a greeting, or a formatting job better. The thinking is work the caller pays for in tokens and in waiting time, whether or not it improves the answer.

Think of it as a dial, not a switch: the question is never "reasoning on or off" but "how much thinking does this task justify, and how will I know if it helped?"

## The controls differ by provider — check the model page

There is no single standard control. Each provider names its own, and the accepted values differ by model, not just by provider. Never copy an effort value from one model's guide into a call to another model.

- **OpenAI:** `reasoning.effort`, with values that include `minimal`, `low`, `medium`, `high`, and `xhigh` on newer models, and `none` as the lowest setting on some newer models. Defaults differ by model — one model's default is another model's lowest setting — so read the default off the model page for the model actually in use. Lower effort means faster answers and fewer reasoning tokens; higher effort means more planning and more tokens.
- **Anthropic:** extended thinking takes a `thinking` object with `budget_tokens`, with a minimum of 1,024 tokens, and the budget must be less than `max_tokens`. Newer Claude models move to adaptive thinking, with effort levels such as `low`, `medium`, and `high` (or `adaptive`), and manual `budget_tokens` is rejected on some newer models — check the model page for the exact model in use before choosing which form to send.
- **Google:** Gemini models use a thinking budget or level control — `thinkingBudget` on Gemini 2.5 generation models and `thinkingLevel` on Gemini 3 generation models. Verify per model, as with the others.

Record the provider, the model ID, the control name, and the value used, on every eval run. A reasoning result without the model ID and the effort value attached is not reproducible, because the same prompt at a different effort is a different configuration.

## Reasoning tokens are billed on top — and what you see is not all there is

Reasoning tokens are in addition to input and output tokens, and they are billed. A request that looks cheap by its visible answer can be expensive in thinking tokens underneath. Budget by total tokens per task — input plus reasoning plus output — not by visible answer length.

What the caller can see of the thinking also differs by provider. Some providers hide the raw reasoning tokens entirely; others return the thinking in full, or return a summary of it. A summary is not the actual reasoning, and the billed tokens are the full thinking tokens, not just the summarised part. Do not log or display raw thinking content to end users without checking what the provider returns and whether it can leak prompt or tool data. Treat thinking output as internal working material, not as part of the answer.

## Diminishing returns and the latency cost

Accuracy gains from more thinking diminish as the budget grows: the first step up from minimal effort on a hard task is usually worth more than the next step up, and on easy tasks extra thinking buys nothing at all. Thinking also costs time — every extra thinking token delays the first visible token and the finished answer, which matters most in interactive or voice settings where the user is waiting.

The shape of the tradeoff is task-dependent, which is why this skill never states a universal budget or a universal latency figure. Measure it per task: run the same eval set at two or three effort levels and compare quality against tokens per task and latency per task on the same view. If a higher effort does not move the eval score, it is waste, however impressive the thinking trace looks.

## Verbosity is a separate dial

`text.verbosity` — low, medium, or high — controls the length of the visible answer. It is a different dial from reasoning effort: verbosity controls how much the model says, reasoning effort controls how much it thinks before saying it. Prefer the verbosity control for the default detail level of an answer, then use the prompt for required content, structure, and length. Do not raise reasoning effort to get a longer answer, and do not lower verbosity expecting the model to think less — the two dials do different jobs, and conflating them produces a configuration nobody can explain or reproduce.

## The start-low rule

Start at the lowest effort that passes the task's evals, and raise it only on measured failure:

- **Start low.** Use the lowest effort for extraction, routing, classification, routine rewrites, simple lookups, greetings, and short confirmations.
- **Raise on evidence.** Move up only when the eval set shows a failure that more thinking fixes — diagnosing a problem, comparing options, writing a plan, reasoning through code. One failing case is a hint; a pattern of failures at one level that clears at the next is evidence.
- **Give it a stop condition.** For genuinely complex work, state what "done thinking" looks like — an explicit stop condition and a single fast self-check — rather than leaving the model to think until the budget runs out.
- **Never raise effort to fix a knowledge gap.** If the model does not know the fact, more thinking will not find it. That is a retrieval or data problem, not a reasoning-budget problem.

## Never treat a visible thinking trace as evidence the answer is correct

A reasoning model can produce a plausible-sounding but wrong chain of thought, and a summary of the thinking is not the thinking itself. A tidy-looking trace proves the model wrote tidy-looking thinking, nothing more. Judge the final answer: check it against the retrieved source, the computed result, or the eval's expected output, exactly as you would judge an answer from a model that showed no thinking at all. In a user interface, showing the thinking trace is a transparency choice, not a correctness claim — and it must never be presented as one.

## Validation exercises

These exercises use hub projects only as practice targets. They are tutorial and demo starting points, not deployable systems, and nothing from them is copied into the vault.

- Run the hub's `Build-reasoning-model` project as a reference implementation and note where its reasoning behaviour is a property of its training setup, not of the effort control — then configure effort on a hosted reasoning model separately and compare what each layer actually controls.
- Use the hub's `deepseek-thinking-ui`, `qwen3-thinking-ui`, and `gpt-oss-thinking-ui` projects to observe visible thinking traces in a chat UI. For each one, write down what the UI shows, what it hides, and whether anything shown could be mistaken for evidence the answer is correct.
- Pick one multi-step task with a small eval set (ten or so cases with known-good answers). Run it at two or three effort levels on one model, record quality, tokens per task, and latency per task for each level, and apply the start-low rule: keep the lowest effort that passes, and write down the failure that would justify raising it.

## Design checklist

Before shipping a reasoning configuration, answer every line:

- [ ] The model ID, provider, control name, and effort value are recorded — read off the model page for that exact model, not copied from another model's guide.
- [ ] The choice was made from an eval run at two or more effort levels, with quality, tokens per task, and latency per task compared on the same view.
- [ ] The lowest effort that passes the evals is the one shipped, and the failure that would justify raising it is written down.
- [ ] Verbosity is set as its own dial, separately from reasoning effort, and the two are not conflated.
- [ ] Reasoning tokens are included in the cost budget for the task, not hidden behind the visible answer length.
- [ ] No thinking trace — full or summarised — is shown to users as evidence the answer is correct, and raw thinking is not logged or displayed without checking what the provider returns.
- [ ] Simple tasks (lookups, greetings, extraction, routine rewrites) run at low effort, and a knowledge gap is routed to retrieval, not to more thinking.

## State

This skill has not yet been exercised on a real reasoning configuration with a measured eval comparison across effort levels. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.

Draft pending representative validation.
