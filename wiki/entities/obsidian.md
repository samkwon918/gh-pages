---
title: "Obsidian"
type: entity
tags: [tool, markdown, knowledge-management, ide]
created: 2026-05-16
updated: 2026-05-16
sources: 1
---

# Obsidian

A local-first markdown note-taking app that functions as the recommended IDE for browsing and navigating an LLM Wiki in real time.

## Role in LLM Wiki

Obsidian is not where the LLM writes (the LLM writes via the filesystem/editor). It's where the human reads and explores. The recommended workflow: LLM agent open on one side, Obsidian open on the other. As the LLM edits files, the human follows along in Obsidian — reading updated pages, exploring the graph view, following wiki-links.

**Key features used:**
- **Wiki-links** (`[[PageName]]`) — Obsidian renders `[[...]]` links natively, matching the cross-reference format used throughout the wiki.
- **Graph view** — visualizes the shape of the wiki: which pages are hubs, which are orphans, what clusters exist.
- **Dataview plugin** — runs queries over YAML frontmatter. Useful for dynamic tables of sources by tag, pages by date, etc.

## Useful Plugins / Features

**Obsidian Web Clipper** — browser extension that converts web articles to markdown. The fastest way to get sources into `raw/`. Outputs clean markdown ready to ingest.

**Download attachments** — in Settings → Files and links, set attachment folder to `raw/assets/`. Bind "Download attachments for current file" to a hotkey (e.g. Ctrl+Shift+D). After clipping an article, this downloads all inline images locally.

**Marp** — Obsidian plugin for markdown-based slide decks. Enables generating presentations directly from wiki synthesis pages.

**Dataview** — query plugin. If wiki pages have YAML frontmatter (tags, dates, source counts), Dataview generates dynamic tables and lists across the vault.

## Limitations

- LLMs can't read markdown with inline images in one pass. Workaround: LLM reads text first, then views referenced images separately.
- Obsidian is a viewer/browser in this workflow, not the editor. The LLM is the editor.

## Related

- [[concepts/llm-wiki-pattern]] — the system Obsidian supports
- [[sources/2026-05-16-llm-wiki-idea]] — founding document that recommends Obsidian
