---
title: "RAG vs. LLM Wiki"
type: concept
tags: [rag, llm, knowledge-management, comparison]
created: 2026-05-16
updated: 2026-05-16
sources: 1
---

# RAG vs. LLM Wiki

A comparison of two approaches to giving LLMs access to a personal document collection: Retrieval-Augmented Generation (RAG) and the LLM Wiki pattern.

## RAG (Retrieve-Augmented Generation)

In RAG systems (NotebookLM, ChatGPT file uploads, most document Q&A tools):

1. Source documents are chunked and embedded into a vector store
2. At query time, relevant chunks are retrieved
3. The LLM generates an answer from the retrieved chunks

**What works:** fast to set up, handles large document collections, no manual curation.

**What doesn't:**
- Nothing is accumulated. Every query starts from scratch.
- Multi-document synthesis is hard — the retriever may miss relevant chunks.
- Subtle questions requiring reasoning across 5+ documents often fail.
- No persistent representation of "what we know so far."
- Contradictions between sources go unresolved.

## LLM Wiki Pattern

In the LLM Wiki approach:

1. When a source arrives, the LLM reads it and **integrates it into the existing wiki**
2. Entity/concept pages are updated; contradictions are flagged; cross-references are built
3. At query time, the LLM reads the already-synthesized wiki pages

**What works:**
- Knowledge compounds — every source makes the whole wiki richer.
- Contradictions are flagged at ingest time, not left unresolved.
- Cross-references are pre-built — queries read synthesis, not raw chunks.
- The wiki is human-readable — you can browse it in Obsidian independently.
- Scales well to ~100s of sources with just an index file (no vector infrastructure).

**What doesn't:**
- Requires LLM involvement at ingest time (not fully automated).
- Less suitable for massive corpora (thousands of documents) without adding search tooling.
- The LLM must touch many files per ingest — more expensive per source than embedding.

## When to Use Which

| Scenario | Prefer |
|---|---|
| Quick Q&A over a large fixed document set | RAG |
| Building knowledge over weeks/months | LLM Wiki |
| Need human-readable, browsable knowledge base | LLM Wiki |
| Want synthesis and cross-references pre-built | LLM Wiki |
| Fully automated ingestion at scale | RAG |
| Team wiki that stays current | LLM Wiki |

## Related

- [[concepts/llm-wiki-pattern]] — the pattern in full
- [[sources/2026-05-16-llm-wiki-idea]] — source that introduced this distinction
