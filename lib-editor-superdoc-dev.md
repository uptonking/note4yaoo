---
title: lib-editor-superdoc-dev
tags: [docx, editor, ooxml, superdoc]
created: 2026-04-20T00:34:45.089Z
modified: 2026-04-20T00:35:08.788Z
---

# lib-editor-superdoc-dev

# guide

- pros
  - virtualized render
  - track-change / redline
  - 支持多种layout: print/web, multi-column
  - headless(renders, edits, and automates .docx files)
  - supports browser and nodejs
  - framework-agnostic: Works with React, Vue, and vanilla JS
  - collaboration — Yjs-based CRDT. Multiplayer editing with comments, tracked changes, and automatic conflict resolution.
  - Agentic tooling — Runs headless in Node.js. Bring your own LLM for document automation, redlining, and template workflows.
    - 提供了MCP
    - risk-rater, playbook, clarity, bulk-updater

- cons
  - license: AGPL, Self-hosted — Runs entirely in the browser or nodejs
  - 不支持元素: task-list, custom syntax
  - 对markdown支持度待改进: Tables, footnotes, task lists, custom syntax extensions
  - 打开多栏布局的.docx文件时, 分页模式下直接打不开， 单页模式下显示为普通单栏文档
  - multi-column布局未提供示例

- features
  - Built on OOXML. Real pagination, section breaks, headers/footers. Not a contenteditable wrapper with export bolted on.
    - As you type, you write to the XML. 
  - Keep your exact document formatting. We preserve complex lists, pages, headers, advanced tables, tracked changes, and much more
  - Template Builder: Create and manage document templates with structured fields using Word’s SDT system.
  - Spell Check & Proofing: you provide a proofing provider and SuperDoc handles the UI: inline spelling markers, direct right-click replacement suggestions, and local ignore flows.
  - Render PDFs in SuperDoc. 基于pdfjs渲染
    - Whiteboard: annotation layer for documents. Supports drawing, text, and stickers.
    - Whiteboard currently works only with PDF documents. 
  - convert(后端api未开源)
    - docx to pdf
    - md to docx
    - html to docx
  - Annotate: Populate fields inside a DOCX template using SuperDoc annotations.
  - Sign a PDF or DOCX document with a cryptographic signature.

- tips
  - ?
# issues
- 如何解决同一个 .docx 文件在不同软件如 word/wps/onlyoffice/libreoffice 中的分页换行位置不同
# draft
- 类似word的多种视图: print/web/outline/draft
- multi-column布局示例
# dev-xp

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

- Public access to ProseMirror is being removed. Internal implementation still uses ProseMirror.
  - Rendering engine: already not ProseMirror-based visually. The visible DOM is rendered through pm-adapter -> FlowBlock -> layout-engine -> DomPainter -> DOM
  - Editing engine: still ProseMirror-based internally.
  - Public API direction: move consumers to editor.doc so they stop depending on PM internals. Internal code continues to use the raw Editor.
- The public programmatic API is being made engine-agnostic.
  - The layout model itself is largely independent. The contracts package exports layout- oriented types like FlowBlock, tab stops, table contracts, z-index helpers, etc. That is a real decoupling layer between “document model” and “rendered pages”.
- The actual editing engine today is still ProseMirror. The architecture docs say PresentationEditor wraps a hidden ProseMirror editor.
  - Commands are still transaction/view based. CommandService is built around ProseMirror Transaction, EditorState, view.dispatch
  - The internal editor core is still ProseMirror types all the way down. The main editor class imports EditorState, Transaction, Plugin, EditorView, Schema, Node, Transform, and y-prosemirror
  - All 86+ extensions use PM Marks, Nodes, Plugins
  - So Core Editor v2 is not here yet as the active runtime.

## devops

```sh
# classic editor example
pnpm dev:docs

```

# devlog

# changelog
- resources
  - [SuperDoc - Changelog](https://www.superdoc.dev/changelog)

- [v1.0.0_202512](https://www.superdoc.dev/changelog/2025-12-25-superdoc-v1-0)
  - The v0 rendering pipeline relied on CSS for pagination. It was clever, but it hit a wall: table layouts broke across pages, images shifted unpredictably, and multi-column sections were impossible to get right. Every edge case required another CSS hack. The more complex the document, the more it fell apart.
  - v0 was also JavaScript-only. No typed commands or events, and
  - v1 replaces the CSS pagination layer with a purpose-built layout engine. It computes page geometry, measures content, and paints the result — the same approach Word and Google Docs use internally.
  - tables paginate correctly, images respect anchoring rules, multi-column sections work, and headers/footers render per-section — just like Word.
  - Headless mode foundation — run SuperDoc without a DOM for server-side processing
  - Provider-agnostic collaboration: working examples for Hocuspocus, Liveblocks, TipTap Cloud, and Y-Sweet.
  - v1 strips non-essential rendering in headless mode, batches decoration updates, and defers layout work until idle. Editing performance on large documents improved 5-10x.
  - Vector shapes and shape groups — SVG rendering for OOXML shapes
  - Search results highlighting — configurable highlight behavior
  - Markdown serialization — editor.getMarkdown() support
  - [Breaking Changes v1.0.0 _202512](http://localhost:3001/guides/migration/breaking-changes-v1)
    - A new layout engine is now the default rendering system
    - Pagination, lists, and paragraph formatting were reimplemented
    - Selection, comments, and tracked-changes behavior changed
# more
