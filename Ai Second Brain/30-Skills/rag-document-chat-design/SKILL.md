---
name: rag-document-chat-design
description: Build document chat over your own documents — ingest and chunk, choose the vector store, run hybrid search plus reranking, show app-constructed citations, enforce permissions at retrieval time, and measure recall and faithfulness. Use when an AI answer must be grounded in documents the user can check.
---

# RAG Document Chat Design

## Outcome

A document-chat application that answers from the documents it was given, shows the sources for each answer so a human can check them, says "not in the documents" when the answer is absent, and can prove — with a labelled eval set — whether a change to chunking, embedding, or reranking helped or hurt.

## Supporting skills

Load only what the gap requires:

- [Retrieval Grounding Design](../retrieval-grounding-design/SKILL.md) — the RAG design authority for this skill. It covers corpus authority, ingestion, parsing, chunking, metadata, access filtering, retrieval, reranking, citations, freshness, deletion, poisoning defence, and evaluation. This skill is its operational companion: it wires the pipeline, picks the store, and runs the chat. Where the two disagree, the design authority wins; this skill does not restate it.
- [Search Architecture Selection](../search-architecture-selection/SKILL.md) for the retrieval-engine decision — exact, full-text, vector, semantic, or hybrid search, including indexing, relevance evaluation, authorisation, freshness, deletion, scaling, and migration.
- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for eval method — datasets, metrics, graders, human review, adversarial cases, regression evidence, and release gates.

## Alpha status

This skill is early draft material, and the tools it names change between releases. The research behind this skill was checked 2026-11-07; re-check the vector-store, embedding-model, and reranker documentation before relying on any detail, capability, limit, or default stated here. Model names, version numbers, and defaults are a 2026-11-07 snapshot and will date fast. Nothing in this skill is a promise that a particular store, model, or retrieval behaviour exists, works, or stays the same.

## What RAG is, and what document chat adds

Retrieval-augmented generation answers a question in two steps: first retrieve the handful of passages from your own data most relevant to the question, then generate an answer with a language model told to use only those passages and to cite them. The model never learns your data permanently in RAG — updating the knowledge means re-indexing documents, not retraining a model. That is the core reason RAG is the default for knowledge-heavy applications whose content changes.

Document chat is the user-facing form of the same pattern: upload or point at documents, ask questions, get answers grounded in those documents, with sources shown. The operational work of this skill is everything between the documents and the answer: ingest, chunking, embedding, storage, retrieval, reranking, citation construction, permission filtering, and evaluation. The grounding policy — what counts as a trustworthy corpus, how citations must behave, how poisoning is defended against — belongs to the design authority linked above.

## Ingest, chunk, embed, store

Ingest is a pipeline, and each step's output is the next step's input. A failure early in the pipeline shows up later as a wrong answer with a confident citation, so record what each step did:

1. **Load documents.** PDF, Markdown, HTML, code, and spreadsheets each need their own parser. A parser that silently drops a table, a code block, or a page is a retrieval miss waiting to happen; note which parser handled each document type.
2. **Extract and clean text.** Remove what is not content — headers, footers, navigation, repeated boilerplate — and keep what is: the text, its structure, and its provenance.
3. **Split into chunks.** Chunks too large dilute the embedding with unrelated text and waste prompt space; chunks too small lose context and split answers across boundaries. Common starting points in the guides reviewed are roughly 200–1,000 words, or about 400–800 tokens, with 10–20% overlap — rules of thumb, not standards. Strategies in use: fixed-size with overlap, structure-aware (split on headings, sections, or paragraphs), semantic (split where embedding similarity drifts), and hierarchical (chunk at several granularities). Start with fixed-size chunks with overlap plus heading metadata, and measure retrieval on your own questions before adding fancier chunking. Chunking is repeatedly described as the highest-leverage tuning knob in RAG.
4. **Attach metadata to every chunk.** Source file, page or section, date, owner or permissions, version. Metadata is not decoration: it is what makes citations, filtering ("only these docs"), freshness checks, and permission enforcement possible later. A chunk without a source pointer cannot be cited and cannot be permission-checked.
5. **Embed each chunk.** An embedding model maps text to a vector of numbers, placed so texts with similar meaning end up close together. Retrieval is nearest-neighbour search: embed the query with the same model and find the closest chunk vectors, usually by cosine similarity. The rule that must not be broken: query and documents must use the same embedding model and the same dimensions. Mixing models in one collection silently breaks retrieval, because vectors from different models live in different spaces and are not comparable. Record the embedding model and its version with the index, and re-embed on change.
6. **Index both the vectors and the text.** The store needs the vector for similarity search and the text for keyword search and for showing the passage to the user. Indexing is a one-time cost per document, plus re-indexing on change.

## Store choice by constraint

Do not pick a vector store from benchmark tables. Pick it from what is already running, what must be self-hosted, and what must be filtered by tenant or permission. The stores verified in the research behind this skill, as checked 2026-11-07:

| Store | Shape | Choose it when |
|---|---|---|
| pgvector | Open-source Postgres extension: adds a vector type, distance operators, and HNSW/IVFFlat indexes, so Postgres itself does vector search, with transactions, joins, and filters in one query | Postgres is already in the stack and you want vectors beside relational data |
| Chroma | Open-source embedding database; collections hold documents, embeddings, metadata, and IDs; in-memory, persistent local, client-server, or hosted | You want the fastest start locally or in a notebook, for a prototype or small-to-medium document chat |
| Qdrant | Vector search engine written in Rust; stores embeddings with JSON payloads and searches by similarity combined with filters on that payload | You want vector search with payload filtering as a standalone service |
| Weaviate | Open-source vector database storing objects and vectors together, with built-in vectoriser modules and hybrid search | You want vectorisation, hybrid search, and generative search in one API rather than wiring them yourself |
| Milvus | Open-source vector database with a scale ladder: Lite (embedded, small scale), Standalone (single container, medium scale), Distributed (Kubernetes, large scale), same client API across all three | You want to prototype small and scale without rewriting client code; note the Milvus docs open timed out in the research run, so this entry is graded secondary, not confirmed on a primary page |
| Pinecone | Fully managed, serverless vector database, proprietary service, API-key authenticated, with namespaces and metadata filtering | You want no database to operate — a deliberate trade: vendor bill, and data leaves your network |
| Elasticsearch | Search engine with keyword and vector search in one store, merging with reciprocal rank fusion | The corpus is already in Elasticsearch, or exact-keyword plus semantic search in one query with one set of filters is the requirement |

The recommendation from the research: default to pgvector if Postgres is already in the stack, Chroma or Qdrant if it is not, and treat managed options as "no operations, vendor bill, data leaves your network" — a deliberate trade, not a default.

## Hybrid search, reranking, and the retrieval shape

Neither keyword search nor vector search alone is enough on technical or code-heavy corpora: vectors miss exact identifiers, keyword search misses paraphrases. Run both and merge:

- **Keyword retrieval (BM25):** the standard keyword ranking function, for exact terms, codes, names, and numbers.
- **Dense-vector retrieval:** nearest-neighbour search over chunk embeddings, for paraphrase and meaning.
- **Merge with reciprocal rank fusion (RRF):** the simplest dependable merger, from Cormack, Clarke and Büttcher (2009). It merges by rank, not by score, so it needs no calibration between two systems whose scores are on incomparable scales. The usual constant is k = 60.
- **Rerank:** first-stage retrieval is a bi-encoder — fast over millions of chunks, because query and document never see each other. A cross-encoder reranker reads the query and one candidate chunk together and outputs a relevance score — far more accurate, far too expensive to run over the whole corpus. The converged pattern is: hybrid retrieval, then the top 20–50 candidates, then cross-encoder rerank, then the top 3–5 into the prompt.
- **Query rewriting (optional, measured):** rewrite, expand, or decompose the user's question before retrieval, or generate several queries and fuse the results. It adds a model call and latency, and a bad rewrite can hurt — measure it on your eval set before keeping it.

Keep the retrieved set small. Too many or too long chunks stuffed into the prompt means the model ignores the middle, or the request exceeds the window. Rerank to the top 3–5, keep chunks short, and order by relevance.

## Citations the application constructs

Grounding means the answer is built from retrieved passages and each claim can be traced to a passage. In practice that requires three things:

1. The prompt instructs the model to answer only from the supplied context and to say "not in the documents" when the answer is absent.
2. Each chunk carries a source pointer — document, page or section, version or date.
3. The user interface shows those sources next to the answer so a human can check.

A citation the model invents is worse than no citation: it looks verified and is not. **Citations must be constructed by the application from the retrieved chunks actually sent to the model** — chunk IDs mapped to displayed sources — never copied from the model's free text. Stream the answer if you like, but only attach citations once the cited chunks are known; do not stream a citation before the model has committed to it.

Document-chat behaviour that follows from this: show sources with document name and location, clickable to the source; let follow-up questions reuse the same retrieved context and narrow it ("only in the 2026 handbook"); show uncertainty — "not found in your documents" is a correct and valuable answer, and a chat UI that always produces a fluent answer trains users to trust it when it is wrong.

## Permission filters at retrieval time

Enforce permissions as a filter at retrieval time — a metadata or tenant filter applied when the chunks are fetched — never as a prompt instruction. The model cannot be the access control. A user must never retrieve, or be shown, chunks from documents they should not see, because retrieval filtered on similarity only and not on access. Test with a low-privilege user, not only with an admin: the admin's test cannot see the leak.

The same boundary applies to the index itself. A document in the corpus can contain hidden instructions, and the model can follow them when the chunk is retrieved — indirect prompt injection through the index. Treat retrieved text as data, mark its provenance, keep tools least-privilege, and require human approval for actions. See the design authority for the full poisoning defence; the operational rule here is that cleaning and permission-filtering happen before retrieval, not after generation.

## Failure-mode table

| Failure | What happens | What helps |
|---|---|---|
| Retrieval miss | The right passage exists but is not in the top-k | Hybrid search, reranking, better chunking, query rewriting |
| Stale docs | The index holds an old version; the answer cites superseded content | Version and date metadata, re-index on change, show the document date in the UI |
| Chunk-boundary loss | The answer is split across two chunks and only one is retrieved | Overlap, larger chunks for that doc type, parent/child chunking (retrieve small, show the larger parent) |
| Hallucinated citations | The model invents a source, page, or quote | App-constructed citations from retrieved chunk IDs only; never let the model free-text a citation |
| Embedding drift | The embedding model is changed or upgraded and old vectors are not re-embedded, or query and documents use different models | One model per collection, record the model and version with the index, re-embed on change |
| Permission leakage across docs | A user retrieves chunks from documents they should not see | Enforce permissions as a filter at retrieval time; test with a low-privilege user |
| Indirect prompt injection via the index | A document in the corpus contains hidden instructions and the model follows them | Treat retrieved text as data, mark provenance, least-privilege tools, human approval for actions |
| Context overload | Too many or too long chunks are stuffed into the prompt; the model ignores the middle or the request exceeds the window | Rerank to the top 3–5, keep chunks short, order by relevance |

## Evaluation: recall and faithfulness, measured separately

Measure retrieval and generation separately. A good answer with bad retrieval is luck; a bad answer with good retrieval is a generation or prompt problem. Build a small, labelled eval set first — around 20–50 real questions with the right source passages — run it on every change to chunking, embedding model, or reranker, and keep the eval set out of the index. No eval set means no way to know whether a change helped.

- **Recall@k / hit rate@k:** of the relevant documents that exist, how many appear in the top k (recall@k), or whether at least one does (hit rate). This needs labelled ground truth — a set of questions with the documents that answer them.
- **Faithfulness:** is the answer grounded in the retrieved documents? Check the answer's claims against the retrieved context, claim by claim.
- **Answer relevancy and context precision:** does the answer address the question, and are the retrieved chunks relevant and well-ranked? These sit alongside recall and faithfulness in the RAGAS family of measures, and under different names in the TruLens RAG Triad (context relevance, groundedness, answer relevance).

Do not put threshold numbers for these measures in a design as if they were standards. Practitioner summaries quote threshold figures, but they are practitioner consensus in secondary write-ups, not vendor or standards-body thresholds, and judge scores cannot catch a wrong-but-plausible answer in a specialised domain without domain calibration. Calibrate any pass mark from your own baseline on your own eval set, and report it as your calibration, not as a standard. See the evaluation skill linked above for the full method.

## When not to use RAG

- **Use structured search instead** when the question is really a lookup: an exact code, date, name, or a filter over fields. Keyword search or SQL will beat vectors and is explainable.
- **Use long context instead** when the whole corpus fits comfortably in the context window and changes rarely. Stuffing the documents in directly is simpler than building and maintaining an index, and avoids retrieval misses entirely — at the cost of more tokens and latency per request, and the model's tendency to ignore the middle of very long contexts.
- **Use fine-tuning instead** when the need is a persistent style, format, vocabulary, or behaviour — not knowledge. Fine-tuning teaches the model how to answer; RAG supplies what to answer from.
- **Do not use RAG at all** when there is no corpus worth retrieving from, when the documents are untrusted and cannot be cleaned or permission-filtered, or when a wrong answer is worse than no answer and no human will check it.

## Design checklist

Before calling a document-chat design finished, answer every line:

- [ ] Ingest, chunking, embedding, and indexing are recorded per document type, with the parser and chunking choice named.
- [ ] Every chunk carries metadata: source, page or section, date, owner or permissions, version.
- [ ] Query and documents use the same embedding model and dimensions; the model and version are recorded with the index.
- [ ] The store was chosen by constraint (already running, must self-host, must filter by tenant or permission), not from a benchmark table.
- [ ] Retrieval is hybrid (BM25 plus dense vectors, merged with RRF), retrieving 20–50 candidates, reranked to the top 3–5 into the prompt.
- [ ] Citations are constructed by the application from retrieved chunk IDs only, never copied from model free text.
- [ ] Permissions are enforced as a filter at retrieval time, and tested with a low-privilege user.
- [ ] The failure-mode table has been checked against the actual corpus, not just read.
- [ ] A labelled eval set (20–50 real questions with the right source passages) exists, is kept out of the index, and is run on every retrieval change, measuring recall@k and faithfulness separately.
- [ ] No threshold figure is presented as a standard; any pass mark is calibrated from the project's own baseline.

## Validation exercises

Use the hub projects below only as exercises — they are tutorial and demo starting points, not deployable systems. Run each exercise against a target you own and compare what happens with this skill's failure-mode table and checklist. Do not copy hub code, notebooks, or tutorial text into the vault.

- Run the hub's `simple-rag-workflow` as a reference implementation of the minimal RAG pipeline (ingest, embed, retrieve, generate): record its chunking, embedding model, and store, then run a small labelled question set against it and report recall@k.
- Run the hub's `document-chat-rag` as a reference implementation of chat-with-documents: check how it shows sources, whether its citations are app-constructed from retrieved chunks, and what it answers when the question is not in the documents.
- Run the hub's `fastest-rag-stack` as a speed-focused stack example: note that its "fastest" name is the hub's claim, not a measured result verified here, and record what actually changes versus the minimal pipeline — hosted inference plus Qdrant — and what does not.
- Run the hub's `trustworthy-rag` as a grounding demonstration over complex documents: check its citation behaviour and failure modes against the table above.
- Run the hub's `notebook-lm-clone` as a full document-chat product shape, as a tutorial: check its RAG, citations, and source display end to end, and list which parts are demo-grade rather than hardened.

## State

This skill has not yet been exercised on a real document-chat build. Promote it only after at least one such exercise — a labelled eval set run against a real corpus, with retrieval and generation measured separately — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
