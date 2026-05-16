# LLM Wiki — Schema & Operating Rules

This file is the authoritative schema for this wiki. Read it at the start of every session and follow it exactly. Every interaction in this repo follows this scheme.

---

## What This Is

This is a **persistent, compounding personal knowledge base** maintained entirely by Claude. You (the LLM) write and maintain the wiki. The human curates sources, directs exploration, and asks questions. Raw sources are never modified. The wiki grows and deepens with every source added and every question asked.

The three layers:
- `raw/` — immutable source documents (articles, papers, notes, images). Human drops them here; LLM reads but never edits them.
- `wiki/` — LLM-generated and maintained markdown files. All pages here are owned and written by Claude.
- `CLAUDE.md` — this file. The operating contract between human and LLM.

---

## Directory Structure

```
/
├── CLAUDE.md                  # This schema (you are here)
├── raw/                       # Immutable source documents
│   ├── assets/                # Downloaded images referenced in sources
│   └── <source-files>.md      # Clipped articles, notes, papers
└── wiki/
    ├── index.md               # Master catalog of all wiki pages
    ├── log.md                 # Append-only chronological event log
    ├── overview.md            # Big-picture synthesis of everything so far
    ├── concepts/              # Idea, framework, and topic pages
    ├── entities/              # People, tools, orgs, places, works
    ├── sources/               # One summary page per ingested raw source
    └── synthesis/             # Comparisons, analyses, answers to big questions
```

---

## Page Format

Every wiki page must follow this template:

```markdown
---
title: "<Page Title>"
type: concept | entity | source | synthesis | overview
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 0            # number of raw sources that informed this page
---

# <Page Title>

<One-sentence summary of the page.>

## <Section>

...body...

## Related

- [[PageName]] — why it's related
- [[PageName]] — why it's related
```

**Rules:**
- Always include frontmatter. Keep it accurate.
- The first body line (after the title) is always a one-sentence summary/definition.
- The last section is always `## Related` with wiki-link style references `[[PageName]]`.
- Page filenames: `kebab-case.md`. Match the title closely.
- Never leave a page stub with only a title. Every page must have at least one substantive section.

---

## Naming Conventions

| Type | Location | Filename pattern |
|---|---|---|
| Concept/topic | `wiki/concepts/` | `kebab-case-topic.md` |
| Person | `wiki/entities/` | `firstname-lastname.md` |
| Tool/product | `wiki/entities/` | `tool-name.md` |
| Organization | `wiki/entities/` | `org-name.md` |
| Source summary | `wiki/sources/` | `YYYY-MM-DD-slug.md` (use ingest date) |
| Synthesis/analysis | `wiki/synthesis/` | `descriptive-name.md` |
| Overview | `wiki/` root | `overview.md` |

---

## Operation: Ingest

When the human says "ingest [source]" or drops a file in `raw/`:

1. **Read** the source document fully.
2. **Discuss** with the human: what are the key takeaways? Any surprises? What questions does it raise?
3. **Write a source summary page** in `wiki/sources/YYYY-MM-DD-slug.md`. Include: one-para summary, key claims (bulleted), notable quotes, gaps/limitations, related wiki pages.
4. **Update existing wiki pages** that this source touches — add new information, note where it confirms or contradicts existing claims, strengthen cross-references. A single source may update 5–15 pages. Be thorough.
5. **Create new pages** for any entity or concept that doesn't have a page yet and is substantive enough to deserve one.
6. **Update `wiki/index.md`** — add the new source summary and any new pages created.
7. **Update `wiki/overview.md`** — revise the synthesis if the source shifts the big picture.
8. **Append to `wiki/log.md`** — use the format `## [YYYY-MM-DD] ingest | <Source Title>` followed by a 2–3 line summary of what was added/changed.
9. **Report back**: tell the human what changed — pages created, pages updated, anything notable.

---

## Operation: Query

When the human asks a question:

1. **Read `wiki/index.md`** first to identify relevant pages.
2. **Read those pages** in full.
3. **Synthesize and answer** with page citations using `[[PageName]]` links.
4. **Decide whether the answer deserves to be filed**: if the answer is substantive (a comparison, an analysis, a new connection), write it as a new page in `wiki/synthesis/` and add it to the index and log.

Query answers that reveal important connections or flag contradictions should always be filed.

---

## Operation: Lint

When the human says "lint" or "health check":

1. Read all pages in `wiki/index.md`.
2. Check for:
   - Pages mentioned in body text but not linked in `## Related`
   - Orphan pages (no inbound links from other pages)
   - Contradictions between pages (flag with `> **Contradiction flagged**: ...`)
   - Stale claims that newer sources may have superseded
   - Important concepts referenced on multiple pages but lacking their own page
   - Missing frontmatter or malformed pages
3. Produce a lint report (can be filed to `wiki/synthesis/lint-YYYY-MM-DD.md`).
4. Fix obvious issues (broken links, missing Related sections). Flag substantive contradictions for the human.

---

## Operation: Update Schema

When the human says "update schema" or wants to change how the wiki works:

1. Discuss the change.
2. Edit this file (`CLAUDE.md`) to reflect the new convention.
3. Log the schema change in `wiki/log.md` with type `schema`.

---

## Index Maintenance Rules

`wiki/index.md` is a content-oriented catalog. Format:

```markdown
## Sources
- [[sources/YYYY-MM-DD-slug]] — one-line description

## Concepts
- [[concepts/page-name]] — one-line description

## Entities
- [[entities/page-name]] — one-line description

## Synthesis
- [[synthesis/page-name]] — one-line description
```

Update it on every ingest. Keep entries sorted within each section (alphabetical or chronological — pick one per section and stick to it).

---

## Log Format Rules

`wiki/log.md` is append-only. Prepend new entries (newest at top). Each entry:

```markdown
## [YYYY-MM-DD] <type> | <title>

<2–3 sentences: what happened, what changed, what was notable.>

Pages created: [[page1]], [[page2]]
Pages updated: [[page3]], [[page4]], [[page5]]
```

Valid types: `ingest`, `query`, `lint`, `schema`, `session-start`.

The header format `## [YYYY-MM-DD] type | title` is parseable with: `grep "^## \[" wiki/log.md | head -10`

---

## Cross-Reference Rules

- Use `[[PageName]]` syntax for all internal links (Obsidian-compatible).
- When you update a page to add information from a new source, add the source to the `sources:` frontmatter count.
- Every non-trivial claim should trace back to at least one source. Use `(→ [[sources/slug]])` inline if precision matters.
- When a new source contradicts an existing claim, do not silently overwrite. Instead, add a `> **Note**: Source X says Y, but Source Z says W. See [[sources/...]] for both.` block.

---

## Session Start Protocol

At the start of any new session in this repo:

1. Read `CLAUDE.md` (this file).
2. Read `wiki/log.md` (last 5 entries) to understand recent activity.
3. Read `wiki/index.md` to re-orient to the current wiki state.
4. Greet the human with a 2–3 sentence summary of where things stand and what's in the wiki.

---

## What Claude Does / Does Not Do

**Does:**
- Write and maintain all wiki pages
- Update index and log on every change
- Surface contradictions and gaps proactively
- File substantive query answers as wiki pages
- Suggest new sources or questions during lint

**Does not:**
- Modify files in `raw/`
- Delete wiki pages without explicit human approval
- Omit the log entry for any operation
- Leave wiki pages in a stub state

---

*Schema version: 1.0 — created 2026-05-16*
