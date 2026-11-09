---
name: fine-tuning-decision-and-eval
description: Decide prompt vs RAG vs LoRA or full fine-tuning, build the dataset, and prove the tuned model is better on a held-out set — with safety re-checked after every run. Use when a narrow, repeated behaviour needs to be reliable without a long prompt on every call, and when the decision to train weights at all still needs justifying.
---

# Fine-Tuning Decision and Eval

## Outcome

A fine-tuning decision that a builder can defend: the choice between prompting, retrieval, and training is written down with reasons; the dataset is built, deduplicated, and held out before training; the tuned model is compared against the base model on the same held-out set; and safety is re-checked after every run before anything ships.

## Supporting skills

Load only what the gap requires:

- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for the eval method itself — datasets, metrics, graders, human review, and regression evidence.
- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for model and provider selection, and for the cost, latency, and data-boundary trade-offs around the decision.
- [Retrieval Grounding Design](../retrieval-grounding-design/SKILL.md) when the alternative to tuning is retrieval — the decision between the two is the first question this skill answers.

## Alpha status

The provider positions and tooling this skill describes are a snapshot checked 2026-11-07, and they change fast: hosted fine-tuning platforms wind down, model availability changes, and open-weight tooling releases move. Re-check the provider's own documentation and the tooling's own docs before relying on any platform status, model name, or API stated here. Nothing in this skill is a promise that a particular tuning path stays available.

## The decision first: prompt vs RAG vs fine-tuning

Fine-tuning teaches a model *how* to behave. Retrieval supplies it with *what* to say. Prompting does both, one call at a time. Confusing the three is the most common fine-tuning mistake, so decide in this order:

1. **Prompt first.** If a well-written prompt with examples gets the behaviour, stop. Prompting is the cheapest thing to change, the easiest to version, and the first thing to try.
2. **RAG for knowledge.** If the need is knowledge — new, changing, or long-tail facts — it belongs in retrieval or in the prompt, not in weights. A tuned model cannot be updated by editing a document, and it will confidently repeat whatever was true at training time.
3. **Fine-tune for narrow, repeated behaviour.** Fine-tuning is the right tool when the behaviour must be reliable at scale without a long prompt on every call: a consistent style, a fixed response format, a classification, a tool-call shape, or correcting instruction-following failures. It also fits when the same narrow task repeats thousands of times and prompt tokens dominate cost and latency, or when a smaller model can be distilled to match a larger one on that task.

Fine-tuning is the wrong tool when the dataset is small, noisy, or unrepresentative; when there is no held-out eval to prove the tuned model is better; or when the base model will be replaced soon — a tuned model dies with its base version, because a tuned model ID is tied to that base snapshot.

The provider's own ordering, from the supervised fine-tuning guide: good evals first. Only invest in fine-tuning after setting up evals, because without a reliable way to tell whether the tuned model performs better than the base model, the training run proves nothing.

## The hosted landscape has changed — do not plan on it

Two provider positions, checked 2026-11-07, change the shape of any fine-tuning plan:

- **OpenAI is winding down its hosted fine-tuning platform.** The platform is no longer accessible to new users. Eligible existing customers can create training jobs until **January 6, 2027**, unless the base model shuts down earlier. Fine-tuned models remain available for inference until their base model shuts down. Do not plan a new product around OpenAI hosted fine-tuning; existing users have a closing window, and new users cannot start. Any vault guidance written before this change that presents OpenAI fine-tuning as a live option is now stale.
- **Anthropic offers no self-serve fine-tuning on the Claude API.** The provider's own glossary states the Claude API does not currently offer fine-tuning. The alternative it points teams to is prompting, retrieval, and long context — not weight training. A Bedrock-hosted fine-tuning path for an older Claude model was documented in secondary sources, but that base model has retired on the Claude API and its Bedrock model card lists an end-of-life date, so verify live availability in your own account and region before planning anything on it. No newer Claude model was listed for customisation in the sources checked.

The durable paths are prompting and retrieval, distillation into a model you control, or open-weight fine-tuning — see the next section.

## The durable open-weight path

Hugging Face **TRL** (`SFTTrainer`, `DPOTrainer`, `GRPOTrainer`, and similar trainers) plus **PEFT** (LoRA) plus Transformers is the reference stack. Around it:

- **axolotl** — config-driven (YAML) fine-tuning supporting LoRA, QLoRA, and full fine-tuning.
- **unsloth** — speed- and memory-optimised single-GPU LoRA/QLoRA tuning.
- **LLaMA-Factory** — no-code / low-code tuning.

These tools were confirmed for existence and positioning only through secondary summaries in the research behind this skill; their exact current function names, config keys, and version compatibility were not opened line by line. Check their own documentation before use.

Open-weight models can be tuned locally (single GPU with QLoRA for small models; multi-GPU for larger ones) and served locally with Ollama-class, vLLM, or llama.cpp-class tooling. GPU memory is the binding constraint; LoRA rank, sequence length, and batch size trade against it.

## Tuning methods: SFT, DPO, RFT

- **SFT (supervised fine-tuning):** input–output pairs; weights adjust to minimise the difference between predicted and target outputs, and the model replicates features in the pairs. Good for emphasising knowledge already present in the model, customising response structure or tone, generating content in a specific format, teaching complex instructions, and optimising cost or latency. Not good for adding entirely new knowledge, or for tasks with subjective quality.
- **Vision fine-tuning:** SFT extended to text-plus-image pairs.
- **DPO (direct preference optimisation):** pairwise preferred/rejected comparisons; the model learns to favour certain outputs. Good for subjective preferences such as tone and politeness. Not good for learning completely new tasks, or tasks without clear human preference.
- **RFT (reinforcement fine-tuning):** adapts a reasoning model with a programmable grader that scores candidate responses, shifting weights toward high-scoring outputs. It was described as supported on o-series reasoning models only; the exact current model list was not opened on a live page in the research behind this skill, so verify it before planning any RFT work.

## Data: start with 50 good examples

Data quality decides the outcome more than data volume. Smaller amounts of high-quality data generally beat larger amounts of low-quality data.

- **Size.** The hosted platform's minimum is **10 examples**. The vendor's recommendation is to start with **50 well-crafted demonstrations** and evaluate; if 50 have no impact, rethink the task or the prompt before adding more data. The right number varies greatly by use case — 50 is a starting point, not a guarantee.
- **Format.** JSONL, one complete JSON structure per line, in chat-completions format (`messages` with roles); a file must have at least 10 lines. For open-weight work, TRL's `SFTTrainer` supports text, prompt-completion, and conversational datasets and applies the chat template for conversational data.
- **Quality checks.** Every example must contain all the information needed for the response. Balance and diversity matter: if most assistant responses in the data refuse, but only a small share should refuse at inference time, expect an overabundance of refusals. Agreement and consistency cap performance: if annotators agree on only part of the extracted content, the model likely cannot do better. All examples must be in the same format as expected at inference.
- **Dedup and leakage.** Deduplicate near-identical examples. Hold out a test set *before* training and never train on it. Check for train/test overlap — the same prompt, a paraphrase, or the same source document on both sides. Keep a slice of real production traffic (not just curated examples) in the eval set. Version the dataset with the model.
- **Holdout before training.** Carve holdout data out of the same training dataset *before* running the job. Training and holdout should have roughly the same diversity of input types and responses. Compare the fine-tuned model against the base model on that same held-out set.

## LoRA and QLoRA vs full fine-tuning

- **Full fine-tuning** updates every parameter — billions of them. Highest ceiling, highest memory and compute cost, highest risk of forgetting prior abilities.
- **LoRA (Low-Rank Adaptation)** freezes the base model and trains small low-rank adapter matrices injected into (typically) attention layers. Trainable parameters are a small fraction of the total; adapters are small, swappable, and can be merged back into the base weights for serving or kept separate per task.
- **QLoRA** is LoRA on a 4-bit quantised base model — the memory-efficient variant that makes single-GPU tuning of larger models feasible.

For most small teams, LoRA or QLoRA is the default. Full fine-tuning is justified only with a large dataset, ample compute, and a measured quality gap that LoRA cannot close. Rank is a real trade-off: increasing the rank enables more trainable parameters, which may produce a better model at the expense of requiring more memory and time to train.

## Hyperparameters and checkpoints

- If the model does not follow the training data as much as expected, increase epochs by 1 or 2.
- If it becomes less diverse than expected, decrease epochs by 1 or 2.
- If it does not appear to be converging, increase the learning-rate multiplier.
- Checkpoints are created at the end of each epoch; only the last few epochs' checkpoints are saved. Use them when the model improves early and then memorises the dataset (overfitting) — the best checkpoint is often not the last one.

These are starting adjustments from the vendor's best-practices guidance, not a tuning recipe. Every change goes through the held-out eval before it is accepted.

## Eval before and after, on the same held-out set

- Build the eval set before training, from the holdout carved out in advance.
- Run the base model on it first. That is the baseline the tuned model has to beat.
- Run the tuned model on the same set, with the same prompts and the same scoring.
- Keep the eval set out of the index and out of the training data. No eval set means no way to know whether a change helped.
- Expect roughly similar improvement each time the number of training examples doubles — a rough scaling heuristic from the vendor's best-practices page, not a guarantee. If doubling the data does not move the eval, the bottleneck is elsewhere: the task definition, the prompt, the data quality, or the method.

## Distillation, with a provider-terms check

Distillation builds a dataset for a smaller model by tuning a prompt for a larger model until it performs well against eval criteria, capturing its outputs, and training the smaller model on them. It can let a small model perform similarly on a specific task to a larger, more costly model.

Check the provider's terms before distilling one provider's outputs into a model you serve elsewhere. The technique is legitimate; the terms governing the source model's outputs are the constraint. Record the terms check alongside the dataset.

## Serving a tuned model

- Pin the base-model version. A tuned model is tied to its base snapshot, and a base upgrade means re-tuning or re-prompting — plan for it.
- Keep the adapter, the dataset, and the eval results together, versioned as one unit. A tuned model without its dataset and its eval is unreproducible.
- Open-weight LoRA adapters are either merged into the base weights and served as one model, or served with the adapter loaded alongside the frozen base. Either way, re-eval when the base changes.
- A tuned model is not portable to the next base version. Say so in the plan, with the re-tuning cost named.

## Safety: tuning can unlearn guardrails

This is the section that decides whether a tuned model ships at all:

- **Tuning can degrade safety even on benign data.** Fine-tuning an aligned model on additional data can degrade its safety, even when the data is entirely benign, and a small number of harmful samples mixed into benign data can drastically compromise alignment. The mechanism is catastrophic forgetting: learning a new task can erase previously learned behaviour, including safety behaviour.
- **Keep safety examples in the training mix.** Do not train on task data alone; include safety examples that preserve refusal and safe-completion behaviour.
- **Keep a safety eval set, and re-run it after every tuning run.** The eval that proves the task improved is not the eval that proves the model is still safe. Run both, every time, and keep the base model available for comparison.
- **Screen training data.** Poisoned samples in training data are a real attack path: a small fraction of harmful examples can shift behaviour. Screen data with human and automated review, provenance-track every example's source, deduplicate, and hold out eval data the training pipeline cannot see.
- **The hosted safety gate disappears when you self-host.** The hosted platform ran its own safety assessment on completed jobs and blocked deployment on failures. When you tune and serve the model yourself, you own that check. There is no gate unless you build one.
- **Do not treat a visible thinking trace as evidence the answer is correct.** For reasoning models, a plausible-sounding chain of thought is not proof — eval the final answer.

## What a good fine-tuning decision hands over

Before any training starts, the decision should be able to answer, from its own records:

- Why prompting and retrieval were not enough, and what narrow, repeated behaviour tuning is for.
- Which hosted paths were ruled out, and on what dated provider position.
- The dataset: its size, its format, its quality checks, its dedup and leakage controls, and the holdout carved out before training.
- The method (SFT, DPO, or RFT) and the adapter choice (LoRA, QLoRA, or full), with reasons.
- The baseline eval result for the base model on the held-out set.
- The safety eval set and the plan to re-run it after every tuning run.
- How the tuned model will be served, versioned, and re-evaluated when the base changes.

If any of those answers is missing, the decision is not finished — it is paused, and the handover says so.

## Validation exercises

Run these as small exercises on a target the builder owns. Hub projects are tutorial/demo starting points for learning, not deployable systems — study them, adapt them, and do not present them as hardened production components. Nothing in any validation touches another project's UI.

- Run the hub's `DeepSeek-finetuning` as a reference implementation and write the prompt-vs-RAG-vs-tuning decision for it before looking at its training code. Record which option the decision actually justifies.
- Run the hub's `grpo-finetuning-qwen3` as a reference implementation and check which tuning method it uses, and whether the dataset it trains on has a holdout carved out before training. If it does not, write the holdout that is missing.
- Run the hub's `knowledge distillation` as a reference implementation and write down the provider-terms check for the source model's outputs before training a smaller model on them. If the terms cannot be found, the exercise stops there.
- For each exercise, build a small held-out eval set first, run the base model on it, and only then compare the tuned model on the same set. A tuned model that was never compared against its base has not been validated.
- For each exercise, run the safety eval after the tuning run and compare it against the base model. A task improvement that comes with a safety regression is a failed run, not a shipped model.

## Design checklist

Before handing a fine-tuning decision to a builder, answer every line:

- [ ] The prompt-vs-RAG-vs-tuning decision is written down, with fine-tuning justified as narrow, repeated behaviour — not knowledge.
- [ ] The hosted landscape is stated with its dates: no new OpenAI hosted fine-tuning users, jobs only until 2027-01-06, and no self-serve fine-tuning on the Claude API.
- [ ] The eval set exists before training, with a holdout carved out in advance and never trained on.
- [ ] The base model's eval result on the held-out set is recorded as the baseline.
- [ ] The dataset starts from 50 well-crafted examples, in JSONL chat format, with quality, balance, dedup, and leakage checks.
- [ ] The method (SFT, DPO, or RFT) and the adapter choice (LoRA, QLoRA, or full) are stated with reasons.
- [ ] Per-epoch checkpoints are kept, and the best checkpoint is chosen by eval, not by recency.
- [ ] Distillation, if used, has a recorded provider-terms check.
- [ ] The base version is pinned, and the adapter, dataset, and eval results are versioned together.
- [ ] Safety examples are in the training mix, and the safety eval is re-run after every tuning run — with the base model kept available for comparison.

## State

This skill has not yet been exercised on a real fine-tuning decision for a target the user owns. Promote it only after one such exercise — a decision, a dataset with a holdout, a base-vs-tuned eval, and a safety re-check, on a target the user owns — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
