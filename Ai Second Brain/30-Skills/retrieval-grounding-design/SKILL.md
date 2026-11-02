---
name: retrieval-grounding-design
description: Design or review retrieval-augmented generation and grounded-answer systems across corpus authority, ingestion, parsing, chunking, metadata, access filtering, retrieval, reranking, citations, freshness, deletion, poisoning defense, and evaluation. Use when an AI answer must rely on external knowledge; use search-architecture-selection for non-generative search alone.
---

# Retrieval and Grounding Design

## Outcome

Produce a retrieval pipeline that returns authorized, current, attributable evidence and lets the application abstain when that evidence cannot support a safe answer.

## Required Inputs

- user questions, decision impact, answer freshness, evidence and citation requirements, languages, modalities, and latency budget
- source owners, authority tiers, licenses, collection method, update cadence, deletion duties, and canonical identifiers
- users, tenants, groups, resource permissions, regional constraints, and access-change latency
- content formats, size, structure, tables, images, code, duplicates, versions, and adversarial or user-controlled sources
- baseline search, expected query distribution, relevance labels, answer rubric, cost, scale, and recovery objectives

## Safety and Permission Constraints

- Treat every document and retrieved passage as untrusted data, never as higher-priority instructions. Retrieval does not neutralize prompt injection or content poisoning.
- Enforce authorization before retrieval and again before presentation. Do not retrieve a broad corpus and ask the model to hide unauthorized results.
- Preserve source provenance, rights, version, and deletion lineage. Embeddings, indexes, caches, traces, and evaluation sets must honor the source's access and deletion state.
- Do not claim grounding because a citation is present. Verify that cited evidence entails the answer and that unsupported claims are absent.
- Indexing private data in an external service, changing production corpus or access rules, or generating consequential answers from sensitive sources is R3 and requires authorization and tested deletion and rollback.

## Workflow

1. Decide whether retrieval is needed. Compare deterministic lookup, database query, curated reference, ordinary search, retrieval-assisted generation, and expert escalation. Use [Search Architecture Selection](../search-architecture-selection/SKILL.md) for the retrieval engine decision.
2. Define source authority and answer policy. Rank canonical, secondary, user, and untrusted sources; establish conflict, recency, citation, refusal, and escalation behavior.
3. Create a corpus manifest with owner, license, purpose, region, sensitivity, tenant, access policy, stable document and revision IDs, checksum, effective dates, ingestion state, and deletion lineage.
4. Build a deterministic ingestion path. Validate type and size, isolate parsers, preserve headings and structure, extract tables and metadata, detect duplicates, record transformations, quarantine failures, and make reprocessing idempotent.
5. Test segmentation against real questions. Compare structural chunks, windows, parent-child retrieval, and table or code handling; retain document and location anchors rather than using one arbitrary chunk size.
6. Establish lexical or structured baselines before dense retrieval. Evaluate hybrid retrieval and reranking only where they improve measured relevance enough to justify cost, latency, and operational complexity.
7. Apply tenant and resource filters inside the retrieval query. Bind cached results to the authorization context and verify deny, revocation, group-change, and shared-resource cases.
8. Construct context with source labels, trust boundaries, minimal necessary passages, deduplication, token budgets, and explicit separation of instructions from evidence. Never concatenate uncontrolled content into privileged prompts without controls.
9. Require answer-to-evidence attribution and abstention. Validate structured citations against returned passages, make conflicts visible, and route high-impact or unsupported cases to a deterministic or human path.
10. Evaluate retrieval and generation separately and end to end. Measure recall at a fixed depth, ranking quality, access leaks, freshness, deletion propagation, answer support, citation correctness, abstention, latency, and cost across representative slices.
11. Rehearse poisoning, parser failure, stale revision, deleted document, permission revocation, tenant collision, index loss, embedding or reranker change, no-result query, provider outage, and full rebuild from the canonical corpus.

## Required Output

- retrieval-necessity decision, question classes, source authority, and answer policy
- corpus manifest, rights and sensitivity controls, lineage, and lifecycle design
- ingestion, parsing, segmentation, index, query, filter, rerank, and context design
- prompt-injection, poisoning, access, citation, freshness, deletion, and recovery controls
- retrieval and answer evaluation set, metrics, thresholds, results, and blind spots
- versioning, rollout, monitoring, rebuild, migration, and exit plan

## Completion Gate

Do not call a grounded-answer system ready until access filters survive negative tests, citations are checked for actual support, stale and deleted content stops appearing within the declared window, hostile documents cannot expand authority, representative retrieval and answer thresholds pass, and the index can be rebuilt from authoritative sources.

## Conditional Reference

Read [Retrieval and Grounding Evidence](references/retrieval-grounding-evidence.md) when selecting retrieval baselines, provenance, adversarial cases, or evaluation dimensions.
