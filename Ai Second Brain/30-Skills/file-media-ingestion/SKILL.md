---
name: file-media-ingestion
description: Design or review uploads, remote imports, storage, transformation, serving, moderation, retention, and deletion for user or partner files and media. Use when an application accepts or fetches documents, images, audio, video, archives, or other binary content.
---

# File and Media Ingestion

## Outcome

Produce a least-privilege ingestion and delivery design that treats every byte and metadata field as hostile until validated, isolates risky processing, and preserves authorization, privacy, availability, and deletion guarantees.

## Required Inputs

- file sources, actors, purposes, allowed types, maximum sizes, volume, and burst rate
- public, private, tenant, regional, retention, moderation, and legal requirements
- upload, remote-fetch, transformation, preview, download, and sharing journeys
- latency, durability, availability, cost, accessibility, and device constraints
- storage, CDN, scanner, parser, transcoder, and operator trust boundaries

## Safety and Permission Constraints

- Do not trust filenames, extensions, declared media types, URLs, archive contents, image dimensions, or parser output. Validate independently and fail closed.
- Apply request limits before multipart parsing where possible, post-decompression limits, pixel or duration limits, rate limits, quotas, and bounded processing time.
- Store untrusted content outside the executable web root with generated identifiers. Serve it through authorization-aware handlers or narrowly scoped expiring references.
- Remote import is an SSRF boundary. Restrict schemes and destinations, resolve and recheck addresses, block local and metadata networks, cap redirects and bytes, and isolate egress.
- Scanning, transcoding, previewing, content moderation, or external analysis can disclose private data and execute complex parsers. Review providers, destinations, retention, telemetry, and failure behavior first.
- Production deletion, public release, moderation action, legal retention change, or transfer of private content to a third party is R3 and requires authorization, evidence, and rollback where feasible.

## Workflow

1. Map the byte flow from client or remote source through edge, temporary storage, validation, quarantine, processing, durable storage, delivery, backup, and deletion.
2. Define a narrow allow-list by business need. Specify byte, count, expansion, dimension, page, duration, and processing limits before selecting tooling.
3. Use generated object keys and preserve the original name only as escaped display metadata. Bind every object to owner, tenant, purpose, state, checksum, schema version, and retention policy.
4. Validate structure and content using isolated, patched components. Quarantine until required checks succeed; make each transition idempotent and auditable.
5. Separate ingestion, processing, storage, and delivery identities. Disable execution, directory listing, active-content rendering, and public access by default.
6. Design asynchronous processing with bounded concurrency, timeouts, retries, dead-letter handling, duplicate detection, cancellation, and overload shedding.
7. Serve correct media types, safe disposition, range behavior, cache policy, security headers, and authorization. Prevent cross-tenant enumeration and cached-data leakage.
8. Define abuse reporting, moderation appeal, malware response, copyright or legal escalation, privacy export, retention, tombstones, derived-asset deletion, and backup expiry.
9. Test spoofed metadata, polyglots, malformed files, decompression bombs, oversized dimensions, parser crashes, SSRF, duplicate uploads, interrupted transfers, stale links, unauthorized reads, and complete deletion.

## Required Output

- data-flow and trust-boundary map
- allow-list and enforceable resource limits
- object states, metadata, authorization, quarantine, and processing design
- storage, delivery, caching, retention, moderation, and deletion plan
- threat cases, test evidence, observability, cost controls, and incident response
- provider boundaries, rollback, export, and migration plan

## Completion Gate

Do not call ingestion ready until limits are enforced before expensive work, untrusted content cannot execute or bypass authorization, risky parsers and remote fetches are isolated, and deletion is verified across originals, derivatives, indexes, caches, and backups according to policy.

## Conditional Reference

Read [File and Media Evidence](references/file-media-evidence.md) when defining validation, remote imports, storage, or browser delivery behavior.
