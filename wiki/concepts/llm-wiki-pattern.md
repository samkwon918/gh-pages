---
title: "LLM Wiki Pattern"
type: concept
tags: [llm, knowledge-management, wiki, pattern, second-brain]
created: 2026-05-16
updated: 2026-05-16
sources: 1
---

# LLM Wiki Pattern

A system architecture where an LLM incrementally builds and maintains a persistent, interlinked wiki of markdown files as a personal knowledge base — replacing the retrieve-and-generate model of RAG with a compile-once, keep-current approach.

## Core Idea

In standard RAG systems, the LLM rediscovers knowledge from scratch on every query. In the LLM Wiki pattern, the LLM instead maintains a structured knowledge base that grows and deepens over time. Each source ingested updates the wiki — not just an index, but actual pages with summaries, cross-references, and synthesis.

The key shift: **knowledge is compiled once and kept current, not re-derived on demand.**

## Three Layers

```
raw/          ← human drops sources here; LLM reads, never writes
wiki/         ← LLM writes and maintains all of this
CLAUDE.md     ← schema / operating contract between human and LLM
```

## Three Operations

**Ingest** — when a new source arrives:
1. Read the source
2. Discuss key takeaways with the human
3. Write a source summary page
4. Update all relevant existing pages (5–15 typical)
5. Create new entity/concept pages as needed
6. Update index + overview + log

**Query** — when the human asks a question:
1. Read the index to find relevant pages
2. Read those pages
3. Synthesize an answer with citations
4. File the answer as a synthesis page if it's substantive

**Lint** — periodic health check:
- Orphan pages (no inbound links)
- Contradictions between pages
- Stale claims superseded by newer sources
- Concepts referenced but lacking their own page

## Why It Works

The bottleneck for personal wikis is maintenance, not reading or thinking. Humans abandon wikis when updating cross-references and keeping pages consistent becomes a chore that outpaces the value. LLMs excel at exactly this kind of bookkeeping — they don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass. The wiki stays maintained because the cost of maintenance is near-zero.

## Comparison to RAG

See [[concepts/rag-vs-wiki]] for a detailed comparison.

## Use Case Breadth

The pattern is domain-agnostic. It works for:
- Personal tracking (goals, health, journal entries)
- Research (building an evolving thesis over weeks/months)
- Reading books (building a companion wiki chapter by chapter)
- Team/business wikis (fed by Slack, meetings, documents)
- Any domain where knowledge accumulates over time

## Historical Antecedent

Conceptually related to Vannevar Bush's Memex (1945) — a vision of a personal, curated knowledge store with associative trails. See [[entities/vannevar-bush-memex]].

## Related

- [[concepts/rag-vs-wiki]] — what this pattern replaces
- [[entities/obsidian]] — recommended IDE for browsing the wiki
- [[entities/vannevar-bush-memex]] — historical antecedent
- [[sources/2026-05-16-llm-wiki-idea]] — founding document that introduced this pattern
- [[overview]] — top-level synthesis
