# Obsidian Capability Map

Verified 2026-10-21 against official Obsidian documentation and the public 1.14.4 desktop release. This is a decision map, not a substitute for the current Help site or an exhaustive command reference.

## Product Model

Obsidian is a local-first desktop and mobile application. A vault is a folder on the local filesystem. Notes are Markdown files; configuration normally lives in `.obsidian/`. Obsidian watches for external file changes, so the vault can also be edited with ordinary filesystem and text tools.

Native file types include Markdown (`.md`), Bases (`.base`), JSON Canvas (`.canvas`), common image, audio, and video formats, and PDF. Obsidian 1.14 can also open an individual Markdown file outside a vault, but vault-wide relationships and configuration remain vault concepts.

## Writing and Reading

Obsidian supports Reading view plus Live Preview and Source editing modes. Its Markdown surface includes:

- headings, paragraphs, emphasis, lists, tasks, tables, code, block quotes, horizontal rules, and comments
- internal links to notes, headings, and blocks; aliases and custom display text
- embeds or transclusion of notes, headings, blocks, images, audio, video, PDFs, Bases, and search results where supported
- callouts, footnotes, mathematical notation, diagrams, and syntax highlighting
- typed YAML properties for text, lists, numbers, checkboxes, dates, date-times, and tags
- export of a rendered note to PDF

Some syntax is Obsidian-specific. Block references, wikilinks, comments, callouts, embedded searches, and other extensions may not behave the same in another Markdown tool. Prefer standard Markdown where portability matters; use Obsidian-specific syntax when its value is explicit.

## Relationships, Discovery, and Navigation

- **Internal links** express durable relationships and update when Obsidian renames files if automatic link updates are enabled.
- **Backlinks** show links and unlinked mentions pointing to the active note.
- **Outgoing links** show destinations referenced by the active note.
- **Search** supports phrases, Boolean expressions, exclusions, groups, property comparisons, and operators for files, paths, content, tags, lines, blocks, sections, and tasks.
- **Quick switcher** opens or creates notes with fuzzy matching.
- **Graph view** visualizes links globally or locally; it is exploratory, not an information architecture by itself.
- **Outline, Tags view, Properties view, Bookmarks, File explorer, Page preview, and Workspaces** provide navigation and reusable layouts.

## Structured and Visual Work

**Properties** store small, typed, queryable facts on notes. Property names are vault-wide types. Current native limitations include no first-class nested properties, no Markdown rendering in properties, and limited bulk editing.

**Bases** creates database-like views over files and their properties without moving the underlying data out of Markdown. A Base can be saved as `.base` or embedded in a note. Native view types documented for the 1.14 baseline include table, list, cards, and kanban. Formulas, filters, grouping, sorting, summaries, and multiple views support dashboards and catalog views. Map is an official Obsidian-maintained community plugin and therefore still requires the repository's third-party review gate before activation.

**Canvas** is a spatial workspace for notes, text cards, media, Bases, folders, and web pages. It uses the open JSON Canvas format. Text-only cards do not become normal linked notes or backlinks until converted to files.

## Capture and Reuse

- **Daily notes** creates date-based notes.
- **Templates** inserts predefined content and merges template properties into a note.
- **Unique note creator** creates time-coded note names.
- **Audio recorder** records audio into the vault.
- **Web Clipper** is a separate official browser extension for highlighting, reading, and saving web content with templates, variables, filters, and logic. Remote images may remain remote until downloaded.
- **Importer** is an official Obsidian-maintained community plugin for migrating supported apps and formats, including CSV. Installation and import are separate review and change boundaries.
- Ordinary paste, drag-and-drop, filesystem copy, Obsidian URI actions, and CLI commands can also capture or create content.

## Core Plugins

Core plugins are shipped and supported by Obsidian and can be enabled per vault. Use the current Settings screen as the authority for what the installed app provides.

| Need | Core plugins |
|---|---|
| Navigate and retrieve | File explorer, Search, Quick switcher, Bookmarks, Random note, Outline |
| Understand relationships | Backlinks, Outgoing links, Graph view, Page preview |
| Structure data | Properties view, Bases, Tags view |
| Compose and capture | Daily notes, Templates, Unique note creator, Note composer, Audio recorder, Footnotes view |
| Think or present visually | Canvas, Slides |
| Operate efficiently | Command palette, Slash commands, Workspaces, Word count, Editor status |
| Recover, synchronize, or share | File recovery, Sync, Publish |
| Browse | Web viewer |

The official list may change. Confirm the installed version before asserting that a plugin or command exists.

## Appearance and Extension

- Themes change the overall presentation; CSS snippets make narrower local presentation changes.
- Community plugins can add views, commands, formats, integrations, and automation through the Obsidian API.
- The custom `obsidian://` URI scheme can open, create, append, search, or navigate from other applications.
- Obsidian CLI controls a running Obsidian application and exposes everyday, Bases, search, Sync, and developer commands. Its required installer version and command set are version-sensitive.
- Obsidian Headless is a separate open-beta client for Obsidian Sync without the desktop app. It is executable software, requires a Sync subscription, and must be reviewed and tested before use.
- Developers can build plugins and themes with the official API and documentation.

Extensions are not sandboxed to fine-grained permissions. Read [safety and operations](safety-and-operations.md) before recommending any executable extension.

## Devices, Sync, Collaboration, and Publishing

Obsidian supports Windows, macOS, Linux, Android, iPhone, and iPad. Interface details and filesystem access differ by platform.

**Obsidian Sync** is an optional paid service for synchronizing local vault copies across devices. It supports selective file and configuration syncing, version history, shared vaults, encryption choices, regions, conflict handling, and settings profiles. It is not a backup system.

Shared vaults do not provide live collaborative editing or fine-grained permissions at the current baseline. All collaborators have broad vault access, and concurrent edits are resolved through file synchronization and conflict behavior.

**Obsidian Publish** is an optional paid hosting service for selectively publishing notes as a website, wiki, documentation set, or digital garden. It supports customization, domains, permalinks, search, graph, analytics integration, and access controls documented by the service. Publish does not run most community-plugin rendering logic, so plugin-dependent notes may not render as they do locally.

## Selection Shortcuts

| User need | Start with | Avoid by default |
|---|---|---|
| Find text or task states | Search and saved bookmarks | A new plugin for ordinary queries |
| Connect concepts | Links, backlinks, small maps of content | Tagging every noun |
| Track consistent records | Properties plus a Base | Duplicating data into a separate table note |
| Explore a messy problem | Canvas, then convert durable conclusions to notes | Leaving important knowledge only in text cards |
| Repeat a note shape | Templates | Large speculative metadata schemas |
| Capture web research | Web Clipper after extension review, with source metadata | Copying without provenance or retaining only remote images |
| Use multiple devices | One sync method plus an independent backup | Two services syncing the same vault |
| Public knowledge site | Publish after a content-boundary review | Assuming linked or plugin-rendered content will publish safely |
| Automation | URI for simple actions; CLI for verified local workflows | Unreviewed scripts or bulk writes without a backup |

## Primary Sources

Use [official sources](official-sources.md) to re-verify the relevant capability before version-sensitive guidance or consequential changes.
