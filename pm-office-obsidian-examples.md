---
title: pm-office-obsidian-examples
tags: [examples, note-taking, obsidian]
created: 2026-04-07T00:47:22.664Z
modified: 2026-04-07T00:47:33.626Z
---

# pm-office-obsidian-examples

# guide

# popular
- https://github.com/kepano/obsidian-skills /MIT
  - Agent skills for Obsidian. Teach your agent to use Obsidian CLI and open formats including Markdown, Bases, JSON Canvas.

- https://github.com/atomicstrata/llm-wiki-compiler /1.6kStar/MIT/202606/ts
  - https://llmwiki.atomicstrata.ai/
  - The knowledge compiler. Raw sources in, interlinked wiki out. Inspired by Karpathy's LLM Wiki pattern.
  - llmwiki is now an Open Knowledge Format (OKF) producer and consumer, aligning compiled agent knowledge with Google Cloud's emerging standard for portable knowledge sharing.
  - Compile raw sources into an interlinked, citation-traceable markdown wiki that agents and humans can browse, query, lint, export, and reuse.
  - llmwiki implements the LLM Wiki pattern: instead of re-discovering knowledge from raw files at query time, compile it once into durable pages that accumulate structure, provenance, review state, and retrieval metadata over time.

- https://github.com/Ar9av/obsidian-wiki /MIT/202606/python/js
  - Framework for AI agents to build and maintain a digital brain through Obsidian wiki using Karpathy's LLM Wiki pattern
  - The pattern comes from Andrej Karpathy's LLM Wiki gist: compile knowledge once into interconnected markdown files and keep them current, instead of asking an LLM the same questions over and over (or running RAG every time). Obsidian is how you see the brain. Your AI agent is how you grow it.
# feat-bases/kanban
- https://github.com/callumalpass/mdbase-spec /MIT/202605/python/js
  - https://mdbase.dev/
  - A specification for treating a folder of markdown files with YAML frontmatter as a typed, queryable data collection.
  - If you use Obsidian (or a similar tool) and you've accumulated notes for meetings, contacts, projects, reading, journal entries, and so on, each with frontmatter fields, your vault is functioning as a database. The property system encourages this: you define fields, assign types, and the tool enforces them across files. But the tooling for managing that structure is limited. 
  - There is no schema file that lives alongside your notes. 
  - This means each tool that touches your vault---Obsidian itself, an editor, a templating plugin, an AI agent---has to independently work out what your types are, or you have to tell each one separately. 
  - mdbase-spec tries to address this. The core idea is that types are defined as files---markdown files in a _types/ folder, where the frontmatter declares the schema and the body can document the type in prose. 
  - Implementations can claim partial conformance. Each level requires all previous levels.
  - https://discord.com/channels/1219902517304098836/1219902517304098841/1507266524291793019
    - Interesting YAML query language for markdown
    - Deriving directly from .base format might still be better for familiarity tho.
  - impl
    - https://github.com/callumalpass/mdbase /ts
    - https://github.com/callumalpass/mdbase-rs /rust
  - examples 🌰
    - https://github.com/callumalpass/mdbase-workouts

- obsidian dataview /9.1kStar/MIT/202504/ts/inactive
  - https://github.com/blacksmithgu/obsidian-dataview
  - https://blacksmithgu.github.io/obsidian-dataview/
  - A high-performance data index and query language over Markdown files, for obsidian
  - Treat your Obsidian Vault as a database which you can query from. 
  - Provides a JavaScript API and pipeline-based query language for filtering, sorting, and extracting data from Markdown pages.
  - **Dataview generates data from your vault by pulling information from Markdown frontmatter and Inline fields** .
  - Markdown frontmatter is arbitrary YAML enclosed by `---` at the top of a markdown document which can store metadata about that document.
  - Inline fields are a Dataview feature which allow you to write metadata directly inline in your markdown document via `Key:: Value` syntax.
  - [Obsidian Dataview: Turn Obsidian Vault into a database you can query from | Hacker News_202205](https://news.ycombinator.com/item?id=31407781)
  - https://github.com/obsidianmd/obsidian-releases
    - Obsidian is not open source software and this repo DOES NOT contain the source code of Obsidian. 
    - However, if you wish to contribute to Obsidian, you can easily do so with our extensive plugin system.
  - https://github.com/blacksmithgu/datacore /2.2kStar/MIT/202606/ts
    - https://blacksmithgu.github.io/datacore/
    - Datacore is a work-in-progress re-imagining of Dataview with a focus on 2-10x better query and rendering performance, as well as fully interactible views.
    - Datacore is fundamentally the same thing as dataview - an index over Markdown files that supports live-updating views and metadata. 
    - However, Datacore focuses on substantial index changes for performance, as well as a new sleek UI which completely replaces traditional Dataview queries. 
    - Datacore supports all query operations that Dataview does, with some extra functionality.
    - WYSIWYG Views: Datacore queries now use a responsive table view and can be manipulated with a table editor much more akin to what you would see in places like Notion and Airtable.
    - Live Editing: Values inside of table views can now be edited; task views include more nuanced rendering of metadata like due date and more operations for manipulating tasks directly.
    - Live Editing: Values inside of table views can now be edited; task views include more nuanced rendering of metadata like due date and more operations for manipulating tasks directly.
  - https://github.com/alas-poor-ophelia/windrose-md /MIT/202605/ts
    - a simple TTRPG-focused mapping tool for Obsidian, built on Datacore. It started as something like graph paper in Obsidian and then... grew? Supports both traditional grid based maps as well as hex maps
    - Windrose supports both grid (square) maps and hex maps — including radial hex grids, nested sub-maps, and definable regions. 
    - Windrose is distributed as a "compiled" Datacore script, which just means it's been all packaged up in a single Markdown file, for nice and easy use.
  - https://github.com/RafaelGB/obsidian-db-folder
    - Obsidian Plugin to Allow Notion like database based on folders

- https://github.com/bgarciamoura/obsidian-notion-bases-plugin /GPL/202603/ts
  - Turn any folder in your vault into a powerful database — right inside Obsidian.
  - [I built a Notion-like database plugin for Obsidian — 6 views, fully local, no external tools : r/ObsidianMD _202603](https://www.reddit.com/r/ObsidianMD/comments/1rtwcja/i_built_a_notionlike_database_plugin_for_obsidian/)

- https://github.com/TfTHacker/group-enhancer-for-bases /MIT/202603/ts
  - Enhances the base functionality of bases group features
  - https://x.com/TfTHacker/status/2035123231628087726
    - group collapsing in Obsidian Bases

- https://github.com/tgrosinger/advanced-tables-obsidian
  - Improved table navigation, formatting, and manipulation in Obsidian.md

- https://github.com/PlayerMiller109/obsidian-sheets-basic /202408/js
  - merge markdown table cells after Obsidian v1.5.0
  - [小插件 Sheets Basic：合并 Markdown 表格单元格 - Obsidian 中文论坛 _202405](https://forum-zh.obsidian.md/t/topic/35091)

- https://github.com/samaraliwarsi/obsidian-board /202604/css
  - Simple self contained obsidian markdown kanban board
  - https://github.com/Louai99k/obsidian-board
  - [Markdown Kanban | No Plugin : r/ObsidianMD _202604](https://www.reddit.com/r/ObsidianMD/comments/1slcmgi/markdown_kanban_no_plugin/)

- https://github.com/obsidian-community/obsidian-kanban /GPL/202603/ts
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/obsidian-tasks-group/obsidian-tasks
  - Task management for the Obsidian knowledge base.
# feat-cli

# feat-ai

- https://github.com/Nexus-JPF/note-companion /MIT/202604/ts
  - https://notecompanion.ai/
  - AI assistant for Obsidian that goes beyond just a chat. (prev File Organizer 2000)
  - transcribe audio/YouTube, chat with your vault, and auto-organize files right inside Obsidian. 
  - Works with Note Companion Cloud, your own AI API keys, or self-hosting.
  - Auto-organize & format notes (folder/tag/title/template suggestions; optional "Inbox" automation)
  - Multiple AI providers: OpenAI, Claude, Ollama/local models, and custom base URLs
  - Self-hosting supported (Docker + service examples)

- https://github.com/dsebastien/obsidian-transcriber /MIT/202604/ts
  - An Obsidian plugin that transcribes images to Markdown using local Ollama vision models.
# feat-ocr/rag
- https://github.com/rootiest/obsidian-ai-image-ocr /MIT/202509/ts/inactive
  - Obsidian plugin for AI-powered text extraction from images

- https://github.com/jritzi/ocr-extractor /MIT/202606/ts
  - Obsidian plugin to extract text from documents, images, etc. and store it as Markdown in notes
  - [OCR Extractor - Now with support for local models : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1u6v7xr/ocr_extractor_now_with_support_for_local_models/)
    - extracts text from PDFs, documents, images, etc. embedded in your notes and inserts it below the attachment as an expandable callout. This means that the text will be searchable via Obsidian's built-in search, other search plugins, and even your operating system's native file search.

- https://github.com/qidianlinjin1990/multi-ocr /NonOpen
  - 一个支持AI OCR和OCR服务商的Obsidian插件
  - [Multi OCR——可能是目前最棒的 Obsidian OCR插件 - 开发调优 - LINUX DO _202601](https://linux.do/t/topic/1433285)
    - 开发原由是因为常用的yolo暂时不支持多模态，而在Obsidian上发现了两个插件ai-image-ocr和ocr-extractor，所以将二者综合了一下。
    - 支持添加多个AI OCR供应商和自动抓取所有模型并进行选择，方便添加，自定义提示词，自定义json参数。
    - 支持四大OCR服务商，包括MinerU、TextIn、Paddle OCR-VL和Mistral OCR。支持OCR服务商OCR参数设置
# feat-backlinks
- https://github.com/AkiSantin/Nodian /MIT/202606/ts
  - plugin that automatically syncs bidirectional relations in YAML frontmatter.
  - When you add a wikilink to a property in one file, the plugin writes a backlink in the target file's corresponding property — and removes it when you delete the link.
  - Relation pairs — define which properties are paired (e.g. Mail ↔ Person, Artist ↔ Songs)
  - Tag-based matching — each pair requires tags; sync only fires when both property and tag match
  - New file support — creating a file from a wikilink auto-adds tags and backlinks
  - Works well with Obsidian Bases

- https://github.com/penfieldlabs/obsidian-wikilink-types /AGPL/202605/ts
  - plugin that adds typed relationships to wikilinks. 
  - Type @ in a wikilink alias to autocomplete relationship types, synced automatically to YAML frontmatter.
  - 给linking添加关系 supports/contradicts
  - https://github.com/jackvaughan09/obsidian-auto-backlink

- https://github.com/brianpetro/obsidian-smart-connections /SrcAval/202606/js
  - https://smartconnections.app/
  - Surface relationships between notes with zero-setup.
  - Find related notes and excerpts while writing. Your link building copilot displays relevant content in graph + list view. A local embedding model powers semantic search. Zero setup. No API key.
  - Smart Connections uses local embeddings and your Smart Environment to surface notes that are semantically related to what you are working on right now. 
  - Ultra-lightweight bundle with minimal third party dependencies

- https://github.com/hans/obsidian-citation-plugin /MIT/202209/ts/inactive
  - This plugin for Obsidian integrates your academic reference manager with the Obsidian editing experience.
  - The plugin supports reading bibliographies in BibTeX / BibLaTeX .bib format and CSL-JSON format.
# feat-publish
- https://github.com/jackyzha0/quartz /12.6kStar/MIT/202606/ts
  - https://quartz.jzhao.xyz/
  - a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites
  - Quartz is a set of tools that helps you publish your digital garden and notes as a website for free. 
  - Quartz v4 features a from-the-ground rewrite focusing on end-user extensibility and ease-of-use.
  - [Backlinks ](https://quartz.jzhao.xyz/features/backlinks)
    - Links in the backlink pane also feature rich popover previews
  - [Bases Support ](https://quartz.jzhao.xyz/features/bases)
    - .base files as interactive database-like views. 

- https://github.com/flowershow/flowershow /1.1kStar/AGPL/202606/ts
  - https://flowershow.app/docs/getting-started
  - https://flowershow.app/
  - Publish markdown (and html) websites, docs, wikis and websites in seconds. Integrates with your AI.
  - https://flowershow.app itself is built and published with Flowershow
  - 类似 git-based cms, 不依赖git
  - 输入文件 ob-vault/github-repo/dnd-upload/cli
  - 🐛
    - 在线编辑不方便
    - 更新是全量
  - https://github.com/flowershow/flowershow/blob/main/apps/flowershow/package.json
    - 依赖mui、@mui/x-data-grid、@trpc/react-query、ag-grid-community、leaflet、mdx-mermaid、nextjs、react-vega、vega-lite、react-plotly.js、rehype-katex、swr、typesense
    - 感觉与portaljs彻底无关了
  - [the Vision of 2025](https://github.com/flowershow/flowershow/blob/main/docs/plans/2025-publish-directly-mvp.md)
    - 🐛 Explicit non-goals (cut aggressively)
    - Versioning or rollback
    - Incremental or differential processing
    - Git integration
    - Bring-your-own storage
    - Presets (docs/blog/etc.)
    - Dataset publishing
    - Search or advanced navigation
    - dashboard
    - [Vision summary](https://github.com/flowershow/flowershow/blob/main/docs/plans/2025-publish-the-vision.md)
  - 已合并pr [Support obsidian new Bases syntax and render the views in the frontend _202508](https://github.com/flowershow/flowershow/issues/861)
  - [Publish Your Obsidian Vault as a Website ](https://flowershow.app/publish-obsidian)
    - Install the plugin, hit publish. Your vault becomes a beautiful website — wikilinks, callouts, math, and all. 
    - Most publishing tools ignore Bases. Flowershow renders them — tables, cards, lists, filters, formulas. Your database views travel with your vault.
  - 🐛 wontfix [Providing updates on syncing progress _202506](https://github.com/flowershow/flowershow/issues/807)
    - I’m syncing a big repo life-itself/second-renaissance@catalog-only and it seems to be taking a long time (like we are now syncing for 40m).
    - this is something that may show up even for smaller syncs where it can take 30s (if larger set of files).
  - [Can Flowershow be used as a headless CMS? _202509](https://github.com/orgs/flowershow/discussions/876)
    - Flowershow can't be used as a headless CMS atm. We don't provide API.
    - I recommend testing Nodify Headless CMS. The Studio can be used entirely on its own without any other tool — it's a complete standalone solution.
  - https://github.com/Glaciercoool/digital_garden /MIT/202511/ts
    - https://digitalgarden-azure.vercel.app/
    - Flowershow template

- https://github.com/qiyangdev/vaultpress /MIT/202606/ts
  - https://vaultpress.qiyang.dev/
  - Publish an Obsidian vault as a documentation site with VaultPress.
  - Keep writing in Obsidian as usual. Run pnpm generate to sync notes into content/, then preview or deploy the site. 
  - The stack is Next.js + Fumadocs, with Obsidian wikilinks, embeds, callouts, Mermaid, and math.
  - [Open-source tool: publish your Obsidian vault as a website (Next.js + Fumadocs) : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1tyahfm/opensource_tool_publish_your_obsidian_vault_as_a/)

- https://github.com/trip2g/trip2g /MIT/202606/go/ts
  - https://trip2g.com/
  - Open-source MCP knowledge mesh - self-host your second brain, expose it to AI agents, federate with peers.
  - Wikilinks ([[note]]), backlinks, outlinks — global resolution, just like Obsidian
  - Obsidian plugin — one-click sync, hash-based diff, only changed files are uploaded.
  - Federation: Peer hubs with trusted people or orgs. Each hub controls access per base. 
  - [2025 Obsidian Publish Alternatives Review : r/ObsidianMD _202506](https://www.reddit.com/r/ObsidianMD/comments/1l02uxc/2025_obsidian_publish_alternatives_review/)

- https://github.com/yoursamlan/pubsidian /MIT/202207/python/inactive
  - https://yoursamlan.github.io/pubsidian
  - An Obsidian-Publish alternative but it's FREE

- https://github.com/oleeskild/obsidian-digital-garden /MIT/202604/ts/Svelte
  - Turn your Obsidian vault into a beautiful website. Free, open-source, and entirely yours.

- https://github.com/secure-77/Perlite /MIT/202602/php
  - A web based markdown viewer optimized for Obsidian Notes
  - Its an open source alternative to obsidian publish.
# feat-pdf
- https://github.com/RyotaUshio/obsidian-pdf-plus /MIT/202508/ts/inactive
  - https://ryotaushio.github.io/obsidian-pdf-plus/
  - the most Obsidian-native PDF annotation & viewing tool ever.
# feat-search
- https://github.com/scambier/obsidian-omnisearch /GPLv3/202401/ts/svelte
  - A search engine that "just works" for Obsidian. 
  - Includes OCR and PDF indexing. Images OCR and PDF indexing are only available on desktop
  - it uses the excellent `MiniSearch` library.
  - Automatic document scoring using the BM25 algorithm
  - Note: support of Chinese, Japanese, Korean, etc. depends on https://github.com/aidenlx/cm-chs-patch
# feat-canvas

# alternatives-ob

- https://github.com/slimhk45/awesome-obsidian-alternatives /md
  - free and open-source Obsidian clones and the technologies used to build them.
  - [I made an awesome list of FOSS apps compatible with the Obsidian vault format : r/PKMS](https://www.reddit.com/r/PKMS/comments/1ro31d0/i_made_an_awesome_list_of_foss_apps_compatible/)
    - I’ve been tracking tools that are compatible with the Obsidian vault format.
    - The idea is to identify FOSS applications that can work with the same vault structure so our notes stay truly portable and future-proof.

- https://github.com/tionis/vulcan /202605/rust
  - A wiki cli to be used with obsidian style knowledge bases
  - Vulcan is a headless Rust toolkit for Obsidian-style vaults and plain Markdown directories. It indexes notes into a rebuildable local SQLite cache, then exposes search, graph queries, Dataview/Bases-style metadata, TaskNotes workflows, static publishing, scripting, MCP tools, and safe note mutations without requiring Obsidian to be running.
  - The long-term shape is a reusable Markdown/vault library stack plus a polished CLI. The current focus is a strong single-vault CLI and MCP server; the next major phase is a multi-vault daemon built on the shared vulcan-core and vulcan-app crates.

- https://github.com/lokus-ai/lokus /FairCode>MIT/202606/js/rust/tauri
  - https://lokusmd.com/
  - A modern, intuitive note-taking application with powerful editing capabilities
  - Database views (Notion-style)
  - Graph view (2D & 3D)(Three.js, D3-force)
  - Infinite canvas (TLDraw)
  - Template system (90+ features)
  - Full-text search
  - Tags & folders
  - TipTap 3, KaTeX, Shiki, Tailwind CSS, Vite 7
  - Tauri 2.0, Tokio

- https://github.com/glyphary/glyphary /202606/ts/rust
  - https://glyphary.github.io/
  - open-source, fast, responsive, macOS-only Markdown workspace for local vaults
  - Obsidian-compatible wikilinks where practical
  - `.canvas` file support
  - vault-local plugins running in a WASM sandbox
  - bases would be a plus, of course, but I could certainly use some input there: I am not sure if I want to re-invent the wheel (trying to make them very friendly) or implement compatibility with Obsidian bases. Hitting both targets would be awesome!
  - [Glyphary: compatible with Obsidian, only fully visual! : r/coolgithubprojects _202606](https://www.reddit.com/r/coolgithubprojects/comments/1uahw3o/glyphary_compatible_with_obsidian_only_fully/)
    - a macOS and Windows Markdown workspace for local folders.
    - it could switch between Obsidian and Glyphary any time, and everything would be local first.
    - The main thing I focused on was making richer notes feel natural to edit. Tables, columns, callouts, collapsible sections, galleries, task lists, and rich links are all things I like having in notes. In Glyphary, those structures are edited visually, while the Markdown stays readable on disk.
    - I also spent a probably unreasonable amount of time on polish: drawers, tabs, split panes, command palette behavior, native menus, search, the way rich blocks save back to Markdown
# examples-vault
- https://github.com/pricklywiggles/niamos
  - A personal Obsidian vault running a modified PARA method, plus the templates, queries, and Claude Code skills that make it work day-to-day.
# examples

# utils

- https://github.com/coddingtonbear/obsidian-local-rest-api
  - A secure REST API and Model Context Protocol (MCP) server for your vault.

- https://github.com/tmcw/obsidian-freeform /MIT/202405/js
  - Obsidian freeform plugin. This lets you write arbitrary JavaScript, including importing ESM modules, injecting styles, and much more
  - This brings a taste of Observable to Obsidian. 
  - give you an @observablehq -like experience with editable code blocks that run in isolated iframes.
  - Based on iframes: Everything you write is run within a sandboxed iframe, making it safer to do more creative coding within Obsidian without affecting the surrounding page.
# import/export
- https://github.com/ShrekBytes/advanced-pdf-export /GPL/202606/ts
  - Export Obsidian notes as pixel-perfect PDFs with six style presets, manual page breaks, full layout control, and a live preview — all from a full-screen modal panel.
  - Desktop only — requires the Obsidian desktop app (uses Electron's print pipeline).
  - [I built an Obsidian plugin for proper PDF export — page breaks, live preview, style presets, and full layout control : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1tvtjjt/i_built_an_obsidian_plugin_for_proper_pdf_export/?sort=top)
# more
- https://github.com/TfTHacker/obsidian42-brat /MIT/202606/ts
  - BRAT - Beta Reviewers Auto-update Tester
  - This is a very special plugin designed to make life much easier for developers and beta-testers of plugins and themes.
  - RAT for short is a plugin that makes it easier for you to assist other developers with reviewing and testing their plugins and themes.
  - Simply add the GitHub repository path for the beta Obsidian plugin to the list for testing and now you can just check for updates. Updates are downloaded and the plugin is reloaded. No more having to create folders, download files, copy them to the right place, and so on. This plugin takes care of all that for you.
