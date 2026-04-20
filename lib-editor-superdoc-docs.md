---
title: lib-editor-superdoc-docs
tags: [docs, superdoc]
created: 2026-04-20T00:35:21.162Z
modified: 2026-04-20T00:35:28.189Z
---

# lib-editor-superdoc-docs

# guide

# overview

# docs

# more

# blogs

## [Document Engine  _202603](https://www.superdoc.dev/changelog/2026-03-22-document-engine)

- A Word document isn't a file you can read and write like JSON. It's a zip archive of interconnected XML files built on OOXML — a specification with thousands of pages (6, 755 to be precise). 
- Most tooling either strips this complexity (convert to Markdown, edit, convert back) or tries to manipulate the XML directly. Both approaches lose formatting, break comments, or produce files that Word opens with repair warnings.

- SuperDoc Document Engine makes programmatic .docx editing reliable.
- Four surfaces, same operations: Four ways to read and edit .docx files — from the browser, backend, terminal, or AI agents.

- LLMs are good at deciding what should change in a document. But actually modifying a .docx file is a different problem. If you ask a model to generate OOXML, you're asking it to understand the full spec — relationship graphs, formatting rules, Word-specific expectations.
  - Document Engine turns this from a generation problem into a tool-use problem
  - The model decides what should change. Document Engine performs how it happens. The operation is deterministic — same input, same result, every time.
- tools
  - Find and replace across documents while preserving formatting
  - Add comments and tracked changes programmatically
  - Format text — bold, italic, styles, alignment, spacing
  - Create structure — paragraphs, headings, lists
  - Batch operations — group multiple edits into a single atomic mutation
  - Diff documents — compare two .docx files and produce a tracked-changes result
  - Build AI agents that edit real Word documents reliably

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
