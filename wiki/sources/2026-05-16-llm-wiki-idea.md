---
title: "LLM Wiki — Idea File (Founding Document)"
type: source
tags: [llm, knowledge-management, wiki, rag, personal-knowledge-base]
created: 2026-05-16
updated: 2026-05-16
sources: 1
raw: raw/llm-wiki-idea.md
---

# LLM Wiki — Idea File (Founding Document)

An intentionally abstract design document describing a pattern for building persistent, LLM-maintained personal knowledge bases — the founding document for this wiki system itself.

## Summary

The document introduces the LLM Wiki pattern: instead of RAG (retrieve-and-generate on every query), the LLM incrementally builds and maintains a structured, interlinked wiki of markdown files. Knowledge is compiled once and kept current, not re-derived each time. The human curates sources and asks questions; the LLM does all the bookkeeping.

## Key Claims

- **RAG accumulates nothing.** Every query rediscovers knowledge from scratch. The LLM Wiki pattern is different: knowledge compounds with each source added.
- **The wiki is a persistent artifact.** Cross-references are pre-built, contradictions are pre-flagged, synthesis already reflects everything ingested.
- **Three layers:** raw sources (immutable), the wiki (LLM-written), and the schema (the CLAUDE.md operating contract).
- **Three operations:** ingest (read → discuss → write → update → log), query (read index → read pages → synthesize → optionally file), lint (health-check the wiki for gaps, orphans, contradictions).
- **Index vs. log:** `index.md` is content-oriented (catalog); `log.md` is chronological (event record). Both serve as navigation tools for the LLM.
- **Query answers can be filed back** as new synthesis pages — explorations compound just like ingested sources.
- **Why it works:** LLMs don't get bored doing cross-referencing bookkeeping. The maintenance cost that causes humans to abandon wikis is near-zero for LLMs.
- **Obsidian** is the recommended IDE for browsing the wiki in real time as the LLM edits it.

## Notable Quotes

> "The wiki keeps getting richer with every source you add and every question you ask."

> "The human's job is to curate sources, direct the analysis, ask good questions, and think about what it all means. The LLM's job is everything else."

> "Humans abandon wikis because the maintenance burden grows faster than the value. LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass."

## Use Cases Mentioned

- Personal tracking (goals, health, psychology, journal entries)
- Research (papers, articles → evolving thesis)
- Reading books (chapter-by-chapter, building companion wiki)
- Business/team internal wiki (fed by Slack, meetings, customer calls)
- Competitive analysis, due diligence, trip planning, course notes, hobby deep-dives

## Optional Tooling Mentioned

- **Obsidian Web Clipper** — browser extension, converts web articles to markdown
- **qmd** — local markdown search engine (BM25/vector hybrid, MCP server available)
- **Marp** — markdown slide decks (Obsidian plugin)
- **Dataview** — Obsidian plugin for querying frontmatter
- **Git** — version history, branching, collaboration on the wiki

## Gaps / What's Left Unspecified

The document is intentionally abstract. It does not specify: exact directory structure, page format standards, frontmatter conventions, or specific workflows. These are to be worked out with the LLM in context — which is exactly what this CLAUDE.md + wiki setup is doing.

## Related

- [[concepts/llm-wiki-pattern]] — full concept page for this pattern
- [[concepts/rag-vs-wiki]] — comparison of RAG approach vs. this pattern
- [[entities/obsidian]] — the recommended wiki browser/IDE
- [[entities/vannevar-bush-memex]] — historical antecedent mentioned in the document
- [[overview]] — top-level synthesis
