---
status: approved
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-22
review_by: 2027-04-21
risk: R0
tags: [system, glossary]
sources: []
---

# Glossary

## Core Terms

**ADR — Architecture Decision Record**  
A durable record of a material technical decision, its context, compared options, evidence, consequences, and exit path.

**Catalog entry**  
A reviewed description of a technology or service: where it fits, where it does not, current evidence, security posture, costs, limitations, and lifecycle status.

**Decision-changing requirement**  
An answer that could alter architecture, provider, cost, security controls, delivery approach, or project scope.

**MVP — Minimum Viable Product**  
The smallest usable product that can test the central value proposition with real users. It is not permission to omit essential safety, privacy, or data-integrity work.

**Playbook**  
A reproducible procedure for completing a workflow or integrating a service, including prerequisites, setup, verification, failure handling, cost controls, rollback, and maintenance.

**POC — Proof of Concept**  
A small experiment designed to resolve a specific technical or product uncertainty. A POC is evidence, not automatically production-ready code.

**Primary source**  
Official documentation, specifications, release notes, security advisories, pricing pages, or other first-party material that directly supports a claim.

**Progressive disclosure**  
Loading the root rules and only the skill, project note, or reference needed for the current task instead of loading the entire vault.

**Quality assurance (QA)**  
The preventive, process-oriented part of quality management that provides confidence that defined quality requirements will be fulfilled. It includes planning, responsibilities, controls, evidence, audits, and improvement; it is broader than testing.

**Quality control (QC)**  
The product- or output-oriented part of quality management that evaluates and acts on whether defined quality requirements are fulfilled. For software releases, this includes candidate-specific evidence, defects, exceptions, residual risk, and disposition.

**Risk level**  
The highest applicable operational level summarized in the [Operating Principles](Operating%20Principles.md): R0 static material, R1 local read-only work, R2 execution/writes/network, or R3 credentials, external mutations, money, publishing, production, private data, or destructive behavior.

**Skill**  
A focused set of AI instructions for a recognizable class of requests. It changes decisions or improves reliability without becoming a universal manual.

**Threat model**  
A structured account of valuable assets, trust boundaries, likely threats, affected users, attack paths, and mitigations.

**Total cost of ownership (TCO)**  
The combined cost of service fees, engineering, operations, monitoring, migration, support, and risk over the expected project lifetime.

**Vertical slice**  
A thin, end-to-end implementation of one real user journey across the required frontend, backend, data, integration, and operational layers.

## Economic-System Terms

**Entitlement**  
The durable right for a user or organization to access a feature, product, quota, or service level.

**Idempotency**  
A property that lets the same operation be retried without creating an unintended duplicate effect, especially important for payments and webhooks.

**Ledger**  
An append-oriented record of economic events used to derive balances and support audit, reconciliation, correction, and history.

**Stored value**  
Money-like value or credit retained for later use. It can introduce accounting, consumer-protection, licensing, tax, fraud, and regulatory obligations.

