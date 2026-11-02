# Vault Design Practices

These practices optimize for retrieval, portability, maintainability, and gradual evolution. They are defaults, not a universal personal-knowledge-management doctrine.

## Choose the Right Structure

Use each structure for the job it handles best:

| Structure | Best use | Warning sign |
|---|---|---|
| Folders | Stable ownership, lifecycle, access, or workflow boundaries | Deep trees that force one note into one meaning |
| Links | Relationships between specific ideas, decisions, people, projects, or sources | Links added only to make the graph dense |
| Properties | Small, consistent fields used for filtering, sorting, validation, or maintenance | Long prose, duplicated facts, or many mostly-empty fields |
| Tags | A small set of cross-cutting states or themes | Synonym drift and large nested taxonomies |
| Maps of content | Curated entry points, sequencing, and context | One giant index that duplicates the whole file tree |
| Bases | Reusable views over consistent properties | Treating a Base as a separate source of truth |
| Canvas | Spatial exploration, planning, and explanation | Durable knowledge stranded in text-only cards |

Do not encode the same category simultaneously in a folder name, tag, property, filename prefix, and map unless each representation serves a distinct retrieval need.

## Grow the Vault from Real Work

1. Start with a small number of stable top-level areas and clear entry notes.
2. Add a folder, property, tag, template, or Base only after repeated use demonstrates a retrieval or workflow need.
3. Prefer one source note and links to it over copied instructions.
4. Archive or retire obsolete material instead of leaving contradictory active notes.
5. Record decisions and evidence close to the work that depends on them.

For this repository, preserve the numbered capability folders and the rule that new top-level areas appear only when they receive real content. Use the existing Vault Map and focused area maps as primary navigation.

## Notes and Names

- Give durable notes descriptive, human-readable names. Avoid encoding facts in filenames when properties carry them more reliably.
- Keep one recognizable purpose per maintained note. Split a note when its parts have independent ownership, lifecycle, or reuse.
- Use headings that make sense as link targets.
- Prefer relative internal links and portable attachment paths.
- Use aliases for stable alternate names; use custom link text for a one-off phrasing change.
- Use block references sparingly because they are Obsidian-specific and fragile when text is heavily reorganized.

## Properties and Tags

Define a property only when its value changes a view, decision, or maintenance action. Before adding one, decide:

- exact name and type
- meaning and allowed values
- which notes should contain it
- who or what maintains it
- whether missing and empty mean different things
- which Base, search, template, or workflow consumes it

Use ISO 8601 dates in stored metadata. Keep status vocabularies short and explicit. Rename a property centrally rather than creating near-synonyms. Do not use tags as a substitute for every typed field.

## Links, Backlinks, and Maps

Create a link when the destination helps a future reader understand, verify, or act on the current note. Prefer contextual links in prose or a small related-notes section over link dumps.

Use backlinks and unlinked mentions as review tools: they can reveal missing relationships, alternate terminology, and stale references. Do not automatically convert every unlinked mention into a link.

Use maps of content when curation adds meaning: a start path, comparison, sequence, owner boundary, or maintenance view. A map should explain why its links belong together rather than reproduce the folder listing.

Use graph view for exploration and anomaly detection, such as unexpected isolates or clusters. Do not optimize the vault for graph aesthetics.

## Templates and Repeated Work

Create a template after a note shape repeats and the repeated fields have proven value. Keep required fields minimal. A template may establish headings, properties, evidence prompts, and completion checks, but should not force irrelevant sections.

When changing a template, decide whether old notes need migration. A template change does not update existing notes automatically.

## Bases

Use a Base when several notes share a stable property schema and a view will answer a repeated question. Keep Markdown notes as the records; use the Base to filter, sort, group, calculate, summarize, or create new records.

Before creating a Base:

1. Write the question the view must answer.
2. Identify the smallest property set needed to answer it.
3. Normalize property names and types on a small sample.
4. Create one useful view before adding alternatives.
5. Verify that editing through the Base updates the expected note properties.

Avoid formula chains that obscure the underlying facts. Document any non-obvious formula or status convention near the owning map or workflow.

## Canvas

Use Canvas for spatial thinking, diagrams, synthesis, and temporary planning. Reference file-backed notes for durable knowledge. Convert important text cards to files so they participate in search, backlinks, maintenance, and ordinary backups as recognizable notes.

Keep a short note beside a long-lived Canvas that states its purpose, owner, and how to interpret it when the layout alone is ambiguous.

## Attachments and External Content

- Choose one documented attachment-location policy and apply it consistently.
- Use meaningful attachment names when they will be referenced or maintained.
- Record source URL, publisher, capture date, and rights or license for imported research when relevant.
- Download remote images only when offline durability and reuse rights justify storing them.
- Do not assume an embedded remote resource is private; viewing rendered content can contact its host.
- Keep original files when a conversion may lose structure, and verify converted links and attachments before deleting the source.

## Daily Notes and Capture

Daily notes are good for chronological capture, logs, and a workbench. They should not become the only location of durable decisions or reusable knowledge. Link or distill durable material into the owning project, catalog, skill, or reference note.

Separate capture from curation. An inbox is useful only when it has a review cadence and a stopping rule.

## Maintenance

Review the vault for:

- broken or unresolved links
- orphaned or duplicate notes
- stale status and review dates
- property name or type drift
- unused tags, templates, Bases, and attachments
- plugin-dependent syntax with no documented exit path
- large or sensitive files unintentionally included in sync or publication

Make maintenance changes in small batches with a backup and observable before/after checks. Prefer renaming and moving files inside Obsidian when link updates matter; verify references after any external batch operation.
