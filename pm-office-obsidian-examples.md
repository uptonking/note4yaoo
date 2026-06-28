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
- https://github.com/Easonnotsing/VaultForge
  - AI agent skill for Obsidian — auto-build atomic note knowledge bases from PDFs and Markdown. Features wikilinks, MOCs, learning roadmaps, …

- https://github.com/coddingtonbear/obsidian-local-rest-api /2.5kStar/MIT/202606/ts
  - https://coddingtonbear.github.io/obsidian-local-rest-api/
  - A secure REST API and Model Context Protocol (MCP) server for your vault.
  - Access your vault through the REST API or the built-in MCP server — both interfaces expose the same core capabilities, so scripts, browser extensions, and AI agents all speak the same language.
  - Read, create, update, or delete notes — full CRUD on any file in your vault, including binary files
  - Surgically patch specific sections — target a heading, block reference, or frontmatter key and append, prepend, or replace just that section without touching the rest of the file
  - Search your vault — simple full-text search or structured JsonLogic queries against note metadata (frontmatter, tags, path, content)
  - Extend the API — other plugins can register their own routes via the API extension interface

- https://github.com/Nystik-gh/ignis /523Star/AGPL/202606/js/svelte
  - Run Obsidian as a self-hosted web app. Not remote desktop, an actual web app.
  - Ignis is a compatibility shim that provides browser-compatible implementations of the Electron APIs used by Obsidian, allowing Obsidian to run in a standard browser while keeping your vault on the server.
  - Ignis provides an alternative for users who want to access their own copy of Obsidian from a browser, in a close-to-native format.
  - the project has grown into a usable browser-based client with multi-vault support, file upload and download, workspaces opened across browser tabs, and live sync between tabs. 
  - Plugin compatibility depends on what APIs a plugin uses; most plugins built on Obsidian's plugin API work, anything requiring Node native modules or child_process doesn't.
  - Ignis currently ships as a self-hosted server but I have plans for a desktop plugin. 
  - All core editor features: markdown, canvas, bases, and the command palette.
  - Most community plugins built on Obsidian's plugin API.
  - What Ignis adds on top of default Obsidian features
    - Custom UI for Obsidian's multi-vault support, allowing create, open, switch, rename, and delete.
    - Different vaults can be loaded in different browser tabs.
    - Live file sync between browser tabs via WebSocket
  - 🐛 What doesn't work
    - Plugins that depend on Node native modules or child_process won't load.
    - Streaming zlib classes (createGzip, createDeflate, etc.) aren't implemented. The synchronous and callback variants work via pako.
    - safeStorage is passthrough by design: isEncryptionAvailable() returns false and encrypt/decrypt are no-ops. Anything plugins store via safeStorage ends up as plaintext on disk. A server-side encrypted option is planned but not yet implemented;
  - 📡 Roadmap
    - Continued shim work to support more community plugins.
    - Multi-user support with OIDC for self-hosted shared deployments.

- https://github.com/atomicstrata/llm-wiki-compiler /1.6kStar/MIT/202606/ts
  - https://llmwiki.atomicstrata.ai/
  - The knowledge compiler. Raw sources in, interlinked wiki out. Inspired by Karpathy's LLM Wiki pattern.
  - llmwiki is now an Open Knowledge Format (OKF) producer and consumer, aligning compiled agent knowledge with Google Cloud's emerging standard for portable knowledge sharing.
  - Compile raw sources into an interlinked, citation-traceable markdown wiki that agents and humans can browse, query, lint, export, and reuse.
  - llmwiki implements the LLM Wiki pattern: instead of re-discovering knowledge from raw files at query time, compile it once into durable pages that accumulate structure, provenance, review state, and retrieval metadata over time.
  - https://github.com/colin4k/obsidian-wiki-compiler
    - plugin that compiles notes into a structured Wiki using LLMs, inspired by Karpathy's LLM Knowledge Bases
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

- https://github.com/rafafields/Obsidian-Base-Hub
  - A modular Obsidian vault leveraging native Bases to replicate Notion-like database functionality for personal project and task management.
  - Obsidian Base Hub is a comprehensive vault template built on the KISS principle (Keep It Simple, Stupid) that transforms Obsidian into a powerful project management system. It provides interconnected databases similar to Notion, specifically designed for managing complex and dynamic work environments.
  - Unlike team management tools, this system focuses on individual workflow optimization while maintaining flexibility for evolving project requirements.

- https://github.com/bgarciamoura/obsidian-notion-bases-plugin /GPL/202603/ts
  - Turn any folder in your vault into a powerful database — right inside Obsidian.
  - [I built a Notion-like database plugin for Obsidian — 6 views, fully local, no external tools : r/ObsidianMD _202603](https://www.reddit.com/r/ObsidianMD/comments/1rtwcja/i_built_a_notionlike_database_plugin_for_obsidian/)

- https://github.com/churnish/dynamic-views /GPL/202605/ts
  - plugin that adds elegant grid and masonry card views for Bases.
  - Display images as covers, thumbnails, posters, or card backdrops
  - Load cards while scrolling rather than all at once
  - https://github.com/maxpower24/bases-card-redirect
    - Override click behaviour in Obsidian Bases card view based on note properties.

- https://github.com/andrewmcodes/obsidian-objects /MIT/202606/ts
  - https://andrewmcodes.github.io/obsidian-objects/
  - Schema-driven, object-based note-taking for Obsidian using native Markdown, Properties, and Bases.
  - Define object types like Person, Project, or Meeting, create structured notes through a modal, and browse them with native Bases. Everything lives in plain Markdown with Properties, so your notes stay fully readable even if you disable or uninstall the plugin.
  - Native Bases: the Generate Bases command writes .base files with table and card views that filter on the type property. Obsidian renders them, so there's no custom view code.
  - Dashboard: a sidebar view lists every object grouped by type for quick browsing.
  - Local-first: no external services and no proprietary storage.  
  - Relationships: link and multilink properties store [[wikilinks]], and the note autocomplete can be scoped to one object type (so a meeting's attendees only suggest people).

- https://github.com/edrickleong/obsidian-feed-bases /MIT/202604/ts
  - Adds a feed layout to Obsidian Bases so you can display notes with their content in an editable feed view.
- https://github.com/edrickleong/obsidian-calendar-bases /MIT/202604/ts
  - Adds a calendar layout to Obsidian Bases so you can display notes with dates in an interactive calendar view.
  - Built with FullCalendar for a robust and feature-rich calendar experience.
  - https://github.com/mtellin/obsidian-bases-calendar
    - multiple time views, Google Calendar colors, timed events, and drag-to-reschedule

- https://github.com/vitalybe/obsidian-advanced-list-bases-view /svelte
  - Adds a advanced list layout to Obsidian Bases so you can display notes as an interactive list view.

- https://github.com/scottTomaszewski/obsidian-folder-bases
  - Open a folder's associated Base by clicking it in the file explorer — like the Folder Notes community plugin, but for .base files instead of notes.
  - https://github.com/Fertion/Bases_Link_Structure
    - plugin for managing link-based note hierarchies. Adds a Structure view for Bases that displays notes as a draggable tree, built on the up property.

- https://github.com/j-palindrome/obsidian-time-ruler /MIT/202606/ts
  - Time Ruler combines the best parts of a nested tasklist and an event-based calendar view. Drag-and-drop tasks to time-block and reschedule, and view tasks on top of read-only online calendars. 
  - Integrates well with the Tasks, FullCalendar, Reminder, and Obsidian Day Planner plugins.
  - Reads and writes tasks in a variety of formats (Dataview inline fields, Tasks plugin emojis, or Full Calendar task-events)

- https://github.com/TfTHacker/group-enhancer-for-bases /MIT/202603/ts
  - Enhances the base functionality of bases group features
  - https://x.com/TfTHacker/status/2035123231628087726
    - group collapsing in Obsidian Bases

- https://github.com/tgrosinger/advanced-tables-obsidian
  - Improved table navigation, formatting, and manipulation in Obsidian.md

- https://github.com/sean2077/obsidian-bases-paginator /BSD/202603/ts
  - adds a paginated table view with column filtering capabilities 
- https://github.com/ghyatt/bases-collapsing-group-table
  - add a Table that supports collapsable groups. Also: on demand, accordion, and collapse all.

- https://github.com/grub-basket/CSV-to-Obsidian-Properties-for-Bases
  - Convert CSV files to individual Markdown Notes with Obsidian-compatible frontmatter properties.

- https://github.com/PlayerMiller109/obsidian-sheets-basic /202408/js
  - merge markdown table cells after Obsidian v1.5.0
  - [小插件 Sheets Basic：合并 Markdown 表格单元格 - Obsidian 中文论坛 _202405](https://forum-zh.obsidian.md/t/topic/35091)

- https://github.com/Cexyz01/obsidian-basecraft /BSD
  - Advanced views, formulas and filters for Obsidian Bases. Built by Hewnpath.

- https://github.com/callumalpass/obsidian-bases-expression /MIT/202606/ts
  - a standalone TypeScript runtime for the expression language used by Obsidian Bases filters and formulas.
  - It is meant for projects that want behavior compatible with the observed Obsidian Bases runtime without depending on Obsidian internals: command-line tools, tests, workflow engines, companion plugins, and Obsidian plugins that need to evaluate or validate user-authored expressions outside the native Bases view.
  - The core package is headless. It does not ship Obsidian view components directly. Use the companion obsidian-bases-expression-builder package when you want a native Obsidian expression-builder UI.

- https://github.com/unxok/obsidian-formula-forge /MIT/202606/ts
  - Render bases formulas in your notes, define global formulas and functions, and more formula-related features.
  - You can render formulas in your notes in inline code or a codeblock. These formulas will automatically re-render when metadata changes.

- https://github.com/xiwcx/obsidian-bases-kanban /MIT/202605/ts
  - A kanban-style drag-and-drop custom view for Obsidian Bases that allows you to organize your notes into columns based on any property.

- https://github.com/samaraliwarsi/obsidian-board /202604/css
  - Simple self contained obsidian markdown kanban board
  - https://github.com/Louai99k/obsidian-board
  - [Markdown Kanban | No Plugin : r/ObsidianMD _202604](https://www.reddit.com/r/ObsidianMD/comments/1slcmgi/markdown_kanban_no_plugin/)
  - https://github.com/EzraMarks/obsidian-bases-css-guide
    - This guide uses the modern html() function introduced in Obsidian 1.10.3+. 
  - https://github.com/mamadaevv/card-columns
    - Kanban-style card view for Obsidian with column grouping, tag filtering, and property chips
  - https://github.com/kotserge/obsidian-bases-kanban
    - kanban board view for Bases. The board is driven entirely by Bases primitives.
  - https://github.com/tyrandel-0/obsidian-para-kanban
    - customizable kanban view for Obsidian Bases: template-based card creation, delete-from-card, board height cap, hideable columns.
  - https://github.com/seventhxiv/obsidian-board-view
    - Interactive board view for obsidian bases, use as Kanban or Gallery, with grouping for rows and columns.

- https://github.com/tu2-atmanand/Task-Board
  - An Obsidian plugin to view and manage your tasks from whole vault using much efficient boards using various methodologies.
  - https://github.com/StepanKropachev/obsidian-pm
    - Project management natively in your Obsidian vault. Table, Gantt, and Kanban views with subtasks, dependencies, time tracking, and custom…

- https://github.com/Trietment/obsidian-kanban /MIT/202606/js
  - A Kanban board for Obsidian that collects tasks from every note in your vault. Tasks are plain markdown checkboxes with optional metadata; the plugin shows them as draggable cards in columns. Works on desktop and mobile.
  - [New plugin - kanban 2.0 : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1uekxse/new_plugin_kanban_20/)
  - Aren't we about to get a native implementation of kanban in Bases?
    - Isn’t that only relevant for linked notes? For some of us, we have a mix between plain text and linked notes within our kanban setup, so I’m unsure if bases will fill the niche I’m looking for (unless I’m mistaken)
  - the outlook sync is something i didn't know i needed until just now

- https://github.com/obsidian-community/obsidian-kanban /GPL/202603/ts
  - Create markdown-backed Kanban boards in Obsidian.
  - https://github.com/ewerx/obsidian-bases-kanban
    - Kanban view for Obsidian Bases. Display notes as draggable cards organized in columns by any property.
  - https://github.com/sleroq/cumban
    - Kanban support for Obsidian bases
  - https://github.com/PythonJobOnline/obsidian-bases-kanban
    - kanban-style drag-and-drop custom view for Obsidian Bases 

- https://github.com/obsidian-tasks-group/obsidian-tasks
  - Task management for the Obsidian knowledge base.

- https://github.com/ebullient/sandbox-customjs /MIT/202606/ts
  - CustomJS scripts for my Obsidian vaults
  - These are the scripts I use in my vault(s) to replace Dataview

- https://github.com/CodyBontecou/obsidian-bases-preview
  - Show inline note content previews inside Obsidian Bases table rows and quickly add new notes.

- https://github.com/Goldius23/obsidian-bases-extended-views
  - Plugin that adds a View option to Bases that displays the notes in a scrollable feed with a thumbnail image.
  - Currently ships with the Timeline view — more views planned.

- https://github.com/TimoBechtel/obsidian-block-view
  - A Bases view for Obsidian that turns your notes into a database of blocks.
  - lets you list and filter the content of your notes - "blocks" - across your entire vault.
  - Because it works as a Bases view, you can still use the standard features like file filtering, sorting, and grouping. Block View then divides each file's content into blocks, so you can filter and display specific sections from multiple notes in the same view.

- https://github.com/Real1tyy/BasesImprovements
  - https://real1tyy.github.io/BasesImprovements/
  - Supercharge your Obsidian Bases workflow with dynamic search filtering — filter any base query instantly

- https://github.com/mymindstorm/obsidian-bases-spotlight-view
  - provides a beautiful, dual-pane "Spotlight" view specifically designed for rapidly browsing, tagging, and managing structured metadata for files in your vault.

- https://github.com/yut0takagi/obsidian-deck-dashboard
  - A Composable dashboard plugin for Obsidian. Compose widgets (tasks, Dataview queries, Bases, calendars) in a draggable grid.

- https://github.com/zobweyt/obsidian-charts /MIT/202606/ts
  - Adds a chart layout to bases so you can display notes as interactive bar or line charts.

- https://github.com/haiqiang-zhang/obsidian-bases-charts
  - Interactive chart views (Data Charts + AI Chart) for Obsidian Bases, powered by Apache ECharts.
  - https://github.com/mkobit/obsidian-bases-charts
    - By leveraging the Obsidian Bases API for data querying and Apache ECharts for rendering, this plugin allows you to create dynamic visualizations driven directly by the properties in your notes.

- https://github.com/mProjectsCode/obsidian-bases-charts-plugin /GPL/202605/ts/svelte
  - adds three new bases views: Scatter Charts, Line Charts, and Bar Charts.
  - https://github.com/PythonJobOnline/obsidian-charts
    - Adds a chart layout to bases so you can display notes as interactive bar or line charts.

- https://github.com/aitorllj93/obsidian-lovely-bases
  - Beautiful, visual bases views for Obsidian. Transform your Obsidian Bases into stunning, interactive visual experiences with smooth animations and intuitive navigation.
  - Smooth Animations: Powered by Motion (formerly Framer Motion) for fluid, performant animations

- https://github.com/vastea/obsidian-task-manager-bases-view
  - Kanban, timeline & weekly‑log calendar views for tasks in your notes — an Obsidian Bases plugin.

- https://github.com/pratikbodkhe/obsidian-bases-timeline
  - isplay notes on a vertical timeline grouped by date

- https://github.com/TfTHacker/timeline-for-bases /MIT/202604/ts
  - A Gantt-style timeline view for Obsidian Bases.
  - https://github.com/sorinbiriescu/obsidian-bases-mermaid-gantt
    - generate mermaid gantt charts
  - https://github.com/sabidurian/timeline-gantt-view
    - Gantt Chart / Timeline Views for Obsidian Bases.
  - https://github.com/lhassa8/obsidian-bases-gantt
    - Gantt chart / timeline view for Obsidian Bases
- https://github.com/xjiaxiang/obsidian-bases-timeline-view
  - timeline view for obsidian bases

- https://github.com/Quorafind/Obsidian-Bases-Canvas 
  - plugin to add obsidian canvas views for bases
  - allows you to create and manage canvas/nodes/use canvas to manage files in your bases.
  - https://github.com/callumalpass/canvas-bases
    - an Obsidian plugin for Bases and Canvas, and a companion plugin for TaskNotes. It turns a live Obsidian Bases view into a canvas-style working board. 
    - Bases still owns the query: filters, sorting, grouping, and visible properties stay in the .base file. 
    - Canvas Bases adds spatial layout, cards, groups, relationship edges, assignment zones, and JSON Canvas export on top of that result set.
  - https://github.com/sabidurian/branches-tree-view
    - Branches adds a "Tree" view to Obsidian's built-in Bases feature, turning flat note collections into navigable, interactive hierarchies. Think family trees, org charts, project breakdowns, taxonomies, or any structure where notes have parent-child relationships.

- https://github.com/dsebastien/obsidian-bookshelf
  - plugin that adds a Bookshelf view type to Obsidian Bases, letting you display notes as a visual bookshelf

- https://github.com/code-of-chaos/ColoredTagsWrangler.obmd /GPL/202606/ts
  - This plugin allows the user to apply different colors to different tags. 

- https://github.com/rafjaf/obsidian-colored-bases-properties 
  - plugin to color property lists in Bases
  - https://github.com/olegbrovchenko/bases-tag-colors
    - Bring life to your tags. Per-base color configs for Obsidian Bases — no global tag soup.

- https://github.com/theol0403/obsidian-bases-new-with-template
  - plugin to automatically apply templates when creating new entries with the Bases plugin
  - a temporary solution to automatically apply templates when creating new entries with the Bases plugin.

- https://github.com/nwbort/vscode-bases
  - VS Code extension that brings Obsidian Bases to VS Code — database-like table, cards, and list views over a folder of Markdown notes, driven by Obsidian-compatible .base files.

- https://github.com/bennyyip/obsidian-bases-toc
  - List headings of filtered files.

- https://github.com/aliou/obsidian-base-rollup
  - plugin that registers a custom Bases table view.
  - The view renders Base query results in a table-like layout and writes an aggregate value back to the note that embeds the Base. 
  - This is useful for keeping frontmatter properties, such as sources, in sync with the current Base result set.

## dataview/datacore

- https://github.com/seburbandev/obsidian-dataview-cheatsheet
  - a handy reference guide for writing powerful queries using the dataview plugin

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
- https://github.com/dsebastien/obsidian-dataview-serializer /MIT/202606/ts
  - https://dsebastien.github.io/obsidian-dataview-serializer/
  - plugin that gives you the power of Dataview, but generates Markdown, making it compatible with Obsidian Publish, and making the links appear on the Graph.
  - 让dataview支持编辑了
  - Thanks to this, the output of your queries is saved in the notes, and the links actually appear on the Graph
  - The Dataview plugin MUST be installed for this plugin to function correctly.
- https://github.com/stevenwcarter/obsidian-dataview-persisted
  - Playing around with using Rust/WASM to create a plugin for obsidian that persists dataview queries as markdown.
- https://github.com/CccJhuan/iCalendar
  - 基于 Dataview 聚合 Markdown 任务，提供月/周/日视图、未安排任务收纳箱、拖拽排程、优先级看板、标签筛选和今日任务提醒。
- https://github.com/rafjaf/obsidian-dataview-singlepagedb /202503/js/inactive
    - a JavaScript Dataview script for Obsidian that creates an in-place editable table interface to modify frontmatter data in your notes.

- https://github.com/RafaelGB/obsidian-db-folder /MIT/202402/ts/inactive
  - plugin is a Notion like database based on folders, links, tags, or dataview queries.
  - Search engine: dataview
  - https://github.com/vanadium23/obsidian-dataview-inlinedb /MIT/202306/js
    - a custom view for dataview plugin in obsidian. It provides an editable table for dataview queries.
    - Inspired by Obsidian DB Folder and custom views from @702573N. Also relies on MetaEdit plugin.

- https://github.com/Mara-Li/obsidian-dataview-properties /GPL/202606/ts
  - automatically copy Dataview inline fields (and their values, even calculated ones!) into frontmatter properties and keep them synchronized.
  - Automatic synchronization based on a configurable interval

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

- https://github.com/caesarloo/render-api
  - plugin: expose dataview/Tasks rendering results via REST API
  - Dataview DQL queries — execute TABLE ... FROM ... queries and return JSON/HTML/text results
  - DataviewJS execution — run arbitrary dv.* code and capture output
  - https://github.com/TuurKeersebilck/obsidian-dataview-graph-sync
    - Plugin that keeps Dataview query results in Obsidian's graph view via hidden wikilinks.

- https://github.com/unxok/dataedit /MIT/202405/ts/inactive
  - plugin that turns your static Dataview queries into dynamic, editable tables. Edit data right where you see it, without needing to leave your current view.
  - This plugin has been abandoned. Being so tightly coupled with Dataview restriced a lot of what I wanted to accomplish and I lost steam. Also, we have the Bases core-plugin now, so you shouldn't really need this plugin anymore.
- https://github.com/udus122/dataview-publisher
  - Output markdown from your Dataview queries and keep them up to date. You can also be able to publish them.

- https://github.com/viethung0823/MoreData /MIT/202504/ts/inactive
  - plugin to enable viewing of CSV files directly within Obsidian, eliminating the need to use a separate application. This plugin will leverage the capabilities of the DataView plugin to query data. 

- https://github.com/stallinger-cx/obsidian-scripts
  - A JavaScript utility library for advanced Obsidian DataView integration.

- https://github.com/Inonvation/obsidian-note-dashboard /202605/ts
  - 笔记统计看板插件：热力图、写作统计、文件夹排行、待办聚合
  - Plugin 版本：Obsidian 原生插件，无需依赖 Dataview 
  - Dataview 版本：基于 DataviewJS 的单文件看板

- https://github.com/s-blu/obsidian_dataview_example_vault /202507/python/js
  - This example vault showcases different usages of the Dataview plugin for Obsidian.md.
  - https://github.com/xDovos/Dataview-Deep-Dive
    - An Obsidian Vault for Dataview and later Datacore examples

- https://github.com/alfredprof3/templates
  - Obsidian templates designed for use with the Templater and Dataview plugins. Some templates contain JavaScript code snippets. 

- https://github.com/Val-49/Obsidian-Dataview-Templates
  - css
# cms
- https://github.com/davidvkimball/obsidian-bases-cms /MIT/202605/ts
  - plugin for Obsidian inspired by Dynamic Views and Multi-Properties that provides CMS-like functionality to bases. 
  - Transform your Obsidian bases into a powerful content management system with card-based views, bulk operations, and smart content management features.
  - Made for Vault CMS

- https://github.com/davidvkimball/vaultcms /MIT/202606/js
  - https://vaultcms.org/
  - Use Obsidian as a content management system for your Astro website.
  - The open-source headless content management system that turns Obsidian into a publishing platform for your Astro website.
  - Detects your Astro routes and content structure automatically.
  - CMS-like homepage: See your content in a visual grid and perform bulk actions.
  - Compatability: Works with almost any Astro theme.
    - 遍历md生成astro相关的配置、主题
  - https://github.com/davidvkimball/vaultcms-website
    - The official website for Vault CMS, built with Astro and Tailwind CSS.
  - https://github.com/davidvkimball/obsidian-vault-cms
    - plugin for setup and configuration management of Vault CMS. Provides a setup wizard, automatic project detection, and plugin configuration management.
  - https://github.com/davidvkimball/vaultcms-presets

- https://github.com/livingpixelio/volcano /MIT/202602/ts
  - Volcano is a JavaScript query API for Obsidian. You can read the contents of your vault as structured data. 
  - The primary use-case is to use Obsidian as a content management system in a Node.js, Deno, or Bun-backed website.

- https://github.com/Abdulkader-Safi/obsidian-crm-plugins /BSD/202606/ts/svelte
  - A lightweight CRM that lives inside Obsidian. 
  - Track clients, deals, and projects, log every interaction, and keep your to-dos, without leaving your vault and without a cloud account.
  - [I built a CRM that lives entirely in your vault as plain markdown notes : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1ue6bfh/i_built_a_crm_that_lives_entirely_in_your_vault/)

- https://github.com/michael-berardi/liberty-crm /202606/ts
  - Obsidian-compatible CRM with CLI, API, and agent integrations for Next.js
  - Obsidian Vault Sync: Connects directly to GitHub-hosted Obsidian vaults
  - Web-Based Editor: CodeMirror 6 markdown editor with block editing
  - Live Preview: Split-pane preview with wikilink support

- https://github.com/CLSherrod/crm-markdown /GPL/202606
  - https://christophersherrod.com/crm/
  - simple, local-first CRM in Markdown for tracking contacts, conversations, follow-ups, and relationships—without SaaS lock-in.
  - The system is intentionally simple: one person = one contact note.
    - Each contact note includes the person’s profile, relationship type, relationship tier, follow-up rhythm, next contact date, and communication log.
  - One Markdown file per person
  - One communication log per person
  - Monthly, quarterly, yearly, and custom follow-up cadences
  - Obsidian Bases dashboards for reminders

- https://github.com/anykeyguru/md-docs-cms-obsidian-plugin /MIT/202604/ts
  - Turn Obsidian into a real CMS for docs-as-code repositories: visual tree with both drafts and public side-by-side, drag-and-drop weight reordering, translation matrix, image picker, draft promotion with preflight, frontmatter form, broken-link health check, VS-Code-style commit / sync panel, schema-driven layout configurable per project, first-run setup wizard, structure-integrity checker with auto-fix, and a settings panel for engine config.

- https://github.com/banisterious/obsidian-draft-bench /MIT/202605/ts
  - https://draftbench.io/
  - A full creative writing workflow for Obsidian: projects, scenes, manuscripts, and versioned drafts. Frontmatter-native and Bases-compatible.
  - inspired by Longform, with added emphasis on per-scene draft history as first-class files, rich metadata via frontmatter, and a compile system that requires no JavaScript knowledge.

- https://github.com/kyoung-jnn/nextjs-obsidian-blog-kit /MIT/202605/ts
  - Next.js blog kit powered by Obsidian as a headless CMS. 
  - Write markdown locally, manage posts with a Notion-like dashboard

- https://github.com/wesswart77/obsidian-cadence /MIT/202606/js
  - A unified Obsidian plugin for CRM, PRM, project management, daily planning, and reminders — all on top of plain markdown. 
  - No server, no sync service, no lock-in. Your vault stays your vault.
  - Most "second brain" plugins do one thing well. Cadence is the opposite: a coherent workspace that brings together the surfaces a working person actually moves between every day — today's tasks, the week ahead, deals in flight, contacts, projects, recurring reminders — and presents them in a single tab with one familiar nav.
  - Module toggles. Turn off CRM, PRM or Planner if you only want some of it.
  - Cadence lets you define custom frontmatter properties for any of your core entities (Contact, Company, Project, Deal, Activity, Partner, etc.) to model your specific business workflows directly inside Obsidian.

- https://github.com/gospecter/specter /AGPL/202606/ts/swift
  - Open-source local sync for CMS content. 
  - SpecterSync DIY syncs Ghost, WordPress, and Shopify content down to a folder of plain markdown files on your hard drive. Run your own editor or AI tools over those files. Push changes back through direct local CMS connections with dry-run preview and conflict detection.
  - SpecterSync DIY (spectersync.diy) is the AGPLv3
  - SpecterSync Pro (spectersync.com) is the official commercial product with signed installers, license activation, automatic updates, managed connectors, hosted AI transformation workflows, and support.
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

- https://github.com/yiiwang118/obsidian-glossa
  - [Glossa：Obsidian的AI agent侧边栏插件 - LINUX DO _202606](https://linux.do/t/topic/2482587)
  - 项目拥有一般ai侧边栏的所有功能，支持api调用模型，也支持调用本地的codex，claude code的能力来达到效果(还不够稳定)，推荐API的形式。
  - 主要的长处在于阅读操作文档，包括obsidian的md文档以及pdf等各种形式的文档，适配划词选中等等。

- https://github.com/Lapis0x0/obsidian-yolo /MIT/202606/ts
  - Agent-native AI assistant for Obsidian — chat, write, knowledge base, and orchestration, all in one place.

- https://github.com/devwhodevs/engraph /rust
  - Local knowledge graph for AI agents. Hybrid search + MCP server for Obsidian vaults.

- https://github.com/glowingjade/obsidian-smart-composer /MIT/202601/ts/inactive
  - AI chat assistant for Obsidian with contextual awareness, smart writing assistance, and one-click edits. Features vault-aware conversations, semantic search, and local model support.

- https://github.com/benoror/obsidianos_work
  - An Obsidian vault wired with AI agent skills — an Agentic Operating System for Thinkers.

## rag/memory

- https://github.com/oomkapwn/enquire-mcp /MIT/202606/ts
  - The most advanced Obsidian MCP — long-term memory for AI agents. H
  - ybrid retrieval (BM25 + ML + BGE rerank, RRF-fused), HNSW live-update, agentic RAG (HyDE + sub-question), Obsidian Bases, PDFs+OCR. For Claude Code/Desktop, Cursor, ChatGPT, Codex, OpenClaw. MCP-native, MIT, SLSA L2.
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
# feat-backlinks/wikilink
- https://github.com/rogerdigital/vault-inspector /MIT/202606/ts
  - An Obsidian vault health checker for finding broken links, orphan attachments, duplicate files, frontmatter drift, stale tags, and large files.
  - Use it before publishing, exporting, migrating, or cleaning up a long-lived vault.
  - Broken Links — Detect wiki links, markdown links, and embeds pointing to non-existent notes or headings.
  - Orphan Attachments — Find images, PDFs, audio/video, and archives not referenced by any note.
  - Duplicate Files — Identify duplicates by name, size, and optional SHA-256 content hash.
  - Large Files — Flag Markdown files and attachments exceeding configurable size thresholds.
  - Scan Progress — Show scanner progress in Obsidian and optional CLI progress on stderr.

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

- https://github.com/SenolIsci/mykg /MIT/202606/python
  - automatically generates a confidence-scored knowledge graph from a set of mixed documents — Markdown, plain text, PDF, Word, PowerPoint, Excel, HTML, and images — grounded in an induced RDFS/OWL ontology.
  - Schema-guided knowledge graph generation — the extracted graph is always grounded in a formal RDFS/OWL schema
  - Bring your own ontology — supply a --base-schema TTL file to lock in classes and properties from an existing formal ontology; the LLM expands it with domain-specific concepts but cannot rename, remove, or contradict your authoritative vocabulary

- https://github.com/kdnk/obsidian-automatic-linker
  - Automatically convert plain text file references into Obsidian wiki links as you write. Keep your knowledge graph connected without manual linking.

- https://github.com/mnaoumov/obsidian-backlink-cache
  - plugin that stores backlink cache to speed up app.metadataCache.getBacklinksForFile().
  - It's mostly useful for users with the large vaults. On smaller vaults the difference might be unnoticeable.
# feat-publish
- pulished-sites
  - [Obsidian Garden Gallery — Sites Built with Obsidian ](https://vaults.obsidian-community.com/)
  - [Quartz Showcase ](https://quartz.jzhao.xyz/showcase)
  - [Digital Garden - Publish Obsidian Notes For Free ](https://docs.forestry.md/)
  - https://github.com/obsidian-pkm-vault/awesome-obsidian-vault

- https://github.com/jackyzha0/quartz /12.6kStar/MIT/202606/ts
  - https://quartz.jzhao.xyz/
  - a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites
  - Quartz is a set of tools that helps you publish your digital garden and notes as a website for free. 
  - Quartz v4 features a from-the-ground rewrite focusing on end-user extensibility and ease-of-use.
  - [Backlinks ](https://quartz.jzhao.xyz/features/backlinks)
    - Links in the backlink pane also feature rich popover previews
  - [Bases Support ](https://quartz.jzhao.xyz/features/bases)
    - .base files as interactive database-like views. 
  - 已合并 [perf: incremental rebuild (--fastRebuild v2 but default) _202503](https://github.com/jackyzha0/quartz/pull/1841)
  - dev-xp
    - ? 似乎未使用ssr
- https://github.com/saberzero1/quartz-syncer /MIT/202606/ts/svelte
  - https://saberzero1.github.io/quartz-syncer-docs/
  - plugin for managing and publishing notes to Quartz, the fast, batteries-included static-site generator that transforms Markdown content into fully functional websites.
  - Multi-provider support: Works with GitHub, GitLab, Bitbucket, Codeberg, Gitea, and self-hosted Git instances.
  - Plugin integrations: Compiles Dataview, Datacore, and Fantasy Statblocks queries into static content.
  - Smart caching: Caches compiled files for faster subsequent publishes. Dynamic content (Dataview/Datacore queries) is automatically detected and recompiled when needed.
  - Diff viewer: Preview exact changes before publishing with split (side-by-side) or unified view.
  - Selective publishing: Choose exactly which notes to publish, update, or remove.
  - CLI support: Automate publishing workflows from the terminal via the Obsidian CLI (requires Obsidian v1.12+).

- https://github.com/oleeskild/obsidian-digital-garden /2.4kStar/MIT/202606/ts/svelte
  - https://docs.forestry.md/
  - Turn your Obsidian vault into a beautiful website. Free, open-source, and entirely yours.
  - This plugin lets you selectively share your thinking while keeping private notes private. 
  - Obsidian Bases
  - Dataview queries (as codeblocks, inline and dataviewjs)

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

- https://github.com/PaiCthulhu/vault-viewer /NC/202606/ts
  - A self-hosted, multi-vault, access-controlled viewer for Obsidian vaults — built to render the plugins and syntax a real vault actually uses.
  - Self-hosted, multi-vault Obsidian viewer with per-user access control — faithfully renders the plugins your vault uses (Dataview, callouts, banners, columns, Canvas, Mermaid, LaTeX), plus graph, backlinks, search and an EN/PT-BR UI.
  - In short: yet another Obsidian publish tool. It exists because the existing ones didn't cover my case: faithful rendering of the plugins I rely on, fully self-hosted, multiple vaults from one instance, and per-user access control.

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

- https://github.com/airenare/inkstone /NC/202606/python
  - https://antonbakulin.com/inkstone
  - Turn your Obsidian vault into a website — no export step, no build pipeline. 
  - Write in Obsidian, push to GitHub, see it live - no export step, no build pipeline, no CMS.
  - A lightweight Python/Flask server that turns an Obsidian vault into a website.
  - Notes placed in the vault root (no subfolder) are served at /slug with no section prefix. 

- https://github.com/secure-77/Perlite /MIT/202602/php
  - A web based markdown viewer optimized for Obsidian Notes
  - Its an open source alternative to obsidian publish.

- https://github.com/andreas13xxx/Slatebase /AGPL/202606/ts
  - Self-hosted Knowledge-Context-Server for Markdown vaults. Browse, edit, and share your Obsidian-compatible notes from any browser.
  - No database — everything is filesystem-based, easy to backup and migrate
  - Multi-user — share vaults with others, with granular read/write permissions
# feat-pdf
- https://github.com/RyotaUshio/obsidian-pdf-plus /MIT/202508/ts/inactive
  - https://ryotaushio.github.io/obsidian-pdf-plus/
  - the most Obsidian-native PDF annotation & viewing tool ever.
# feat-docs/excel/files
- https://github.com/mikes-cafe/obsidian-attachments-autopilot /MIT/202605/ts
  - plugin that auto-creates queryable twin markdown notes for non-markdown attachments (images, PDFs, video, audio) so they appear in Obsidian Bases.
  - attachments (PNG, JPG, PDF, MP4, MP3, …) live in your vault but they're not first-class notes. They don't show up in Dataview queries, they're invisible to Bases, and you can't add metadata to them.
  - Attachments Autopilot fixes this by automatically creating a "twin" markdown note next to every attachment
  - Each twin contains three frontmatter properties pointing at the source and a generated preview

- https://github.com/tescolopio/Obsidian_FolderBridge /MIT/202606/ts
  - adds external folders to your Obsidian vault as seamless, native‑feeling directories. 
  - It creates virtual mount points that map real filesystem paths into the vault, enabling multi‑root workspaces without moving or duplicating files.
  - Zero duplication — files are always read and written from their real locations on disk or on the remote backend
  - Multi-root workspaces — mount as many folders as you want at any virtual path inside one vault
  - Full Obsidian integration — mounted files participate in the file explorer, Quick Switcher, Search, graph-adjacent indexing workflows, embeds, and normal vault commands
  - embedded images and PDFs inside mounted folders render correctly
  - Security allowlist — only explicitly approved real paths can be accessed
  - Mount Types
    - Local folder mounts — mount any directory from your local filesystem, external drive, NAS share, UNC path, or WSL-exposed folder
    - WebDAV mounts — mount folders from Nextcloud, ownCloud, Synology, or any generic WebDAV server
    - S3-compatible mounts — mount Amazon S3, Backblaze B2, MinIO, Cloudflare R2
  - Background file watcher — file changes from mounted folders appear in Obsidian in real time when the backend supports it

- https://github.com/abcamus/obsidian-sync-vault-ce /paid/202606/ts
  - https://sync-vault.com/
  - Professional cloud sync & VFS for Obsidian. Features zero-space VFS, 4K streaming, MCP AI engine, and P2P collaboration. 
  - 连接 TB 级网盘与 Obsidian AI 大脑，跨设备免本地存储轻松同步、链接一切资源。
  - 支持双向同步和单向同步，自动识别文件删除 & 移动操作。
  - 🤔 是否实现成了网盘客户端

- https://github.com/otaviof/obsidian-vfs /apache2/202605/ts
  - Virtual file-system sharing Obsidian notes with VSCode and Claude Code
  - Read-only virtual filesystem exposing an Obsidian vault via the obs:// protocol. 
  - Three entrypoints — a VS Code extension, a Claude Code plugin, and a CLI — built on a shared core engine.
  - allowed and blocked restrict general vault content
    - blocked is evaluated first (deny wins). When a path matches both allowed and blocked, it is blocked. 

- https://github.com/Signynt/virtual-content /MIT/202606/ts
  - Display markdown text (including dataview queries or Bases) at the bottom, top or in the sidebar for all notes which match a specified rule, without modifying them.
  - Set rules to add markdown text to files based on rules. This text gets rendered normally, including dataview blocks or Obsidian Bases. Your notes don't get modified or changed, the given markdown text is simply rendered "virtually". 
    - define rules using folderes, tags and properties
    - Lets you select wether the "virtual content" gets added as a footer (end of file), a header (below properties) or in the sidebar
  - useful if you have many files with the same dataview block. Instead of pasting the dataview codeblock into every note, you can simply add it with this plugin. 
  - Works with Dataview, Datacore and native Obisidan Bases

- https://github.com/ljcoder2015/obsidian-sheet-plus /apache2/202606/ts
  - https://docs.ljcoder.com/
  - A full-featured spreadsheet experience, built on `Univer`, directly inside your Obsidian vault.

- https://github.com/playermiller109/obsidian-sheets-basic /BSD/202606/js
  - Merge markdown table cells in Reading and Live Preview / Editing Mode. 在阅读和实时预览/编辑模式合并表格单元格

- https://github.com/mnaoumov/obsidian-custom-attachment-location /MIT/202606/ts
  - Customize attachment location with variables($filename, $data, etc) like Typora.

- https://github.com/dy-sh/obsidian-consistent-attachments-and-links
  - Obsidian plugin. Move note with attachments.
  - allows you to reorganize your vault to make it more consistent. Next, the plugin will automatically maintain the consistency of your library.
  - Ideally, all attachments should be located in the note folder or its subfolders. It is not necessary, but in this case, you can easily export a note to a separate folder outside of your vault, knowing that all its attachments are with it. By deleting a note, you will know for sure that you will not delete the attachments you need or leave unnecessary garbage in your library.

- https://github.com/kraibse/obsidian-table-sorting
  - allow you to organize your tables non-destructively
  - Sorting by multiple column

- https://github.com/weppos/obsidian-mermaid-view
  - Obsidian plugin for viewing Mermaid files in views.

- https://github.com/ebullient/obsidian-slides-extended
  - Create markdown-based reveal.js presentations in Obsidian

- https://github.com/reorx/obsidian-paste-image-rename /MIT/202512/ts/inactive
  - This plugin is inspired by Zettlr, Zettlr shows a prompt that allows the user to rename the image, this is a great help if you want your images to be named and organized clearly.
  - Paste image rename plugin not only implements Zettlr's feature, but also allows you to customize how the image name would be generated, and eventually free you from the hassle by automatically renaming the image according to the rules.
# feat-search
- https://github.com/achekulaev/obsidian-qmd
  - Local machine Semantic Search plugin for Obsidian based on QMD

- https://github.com/scambier/obsidian-omnisearch /GPLv3/202401/ts/svelte
  - A search engine that "just works" for Obsidian. 
  - Includes OCR and PDF indexing. Images OCR and PDF indexing are only available on desktop
  - it uses the excellent `MiniSearch` library.
  - Automatic document scoring using the BM25 algorithm
  - Note: support of Chinese, Japanese, Korean, etc. depends on https://github.com/aidenlx/cm-chs-patch

- https://github.com/mProjectsCode/obsidian-lemons-search-plugin
  - plugin that offers a fast fuzzy finder based quick switcher with preview.

- https://github.com/MahmoudFawzyKhalil/obsidian-global-search-and-replace /AGPL/202406/ts/inactive
  - A plugin to do a global search and replace in all of your Obsidian vault files.
# feat-sync
- https://github.com/dsnbyte/obsidian-supabase-sync /MIT/202606/ts
  - offline-first, high-performance Obsidian plugin that bidirectionally synchronizes vault notes to a Supabase PostgreSQL database (including frontmatter metadata) and binary attachments to Supabase Storage.
  - Offline-First Architecture: Changes are tracked locally in a robust sync queue and synchronized metadata registry.
  - Rich Postgres & Bidirectional Sync: Notes are structured as Postgres records, and pulls are automatically executed since your last sync.
  - Dual-Channel Sync:
    - Markdown Notes: Synchronized directly with PostgreSQL database rows. Frontmatter properties are parsed into a queryable JSONB column, while tags and titles are indexed in dedicated fields.
    - Binary Attachments: Uploaded to/deleted from a private Supabase Storage bucket, organized securely under your Supabase User ID.
  - Conflict Resolution: When files are edited on multiple devices, conflicts are resolved using robust, safety-first rules (e.g., comparing hashes and timestamps) to prevent data loss
  - https://github.com/ran-codes/obsidian-notion-database-sync /MIT/202602/ts
    - Sync Notion databases and pages into your Obsidian vault as Markdown files.
  - https://github.com/masaoka108/obsidianotion /BSD/202604/ts
    - plugin that syncs your Notion workspace to Obsidian with intelligent folder mapping and file organization.

- https://github.com/brysontang/DeltaTask /MIT/202502/python/inactive
  - A powerful, locally-hosted task management application with Obsidian integration and a Model Context Protocol (MCP) server.
  - Smart Task Management: Create tasks with urgency levels and effort estimates
  - Prioritization Engine: Automatically sorts tasks by urgency and effort
  - Tagging System: Organize tasks with custom tags
  - Local Storage: All data stored locally in SQLite database, 3 tables as todos, tags, todo_tags
  - Obsidian Integration: Bi-directional sync with Obsidian markdown files
  - DeltaTask creates and maintains a structured Obsidian vault:
    - Task files with frontmatter metadata
    - Tag-based views for filtering tasks
    - Statistics dashboard
    - Bi-directional sync between Obsidian markdown and SQLite database

- https://github.com/LiusRay/ClawMd-Hub /MIT/202606/js
  - [[开源] 分享自己开发的一套文件同步系统，主要针对 obsidian 自动文件同步 - LINUX DO _202606](https://linux.do/t/topic/2456710)
  - 定位很简单：这是一个面向 AI 工作流的 Markdown 资料库同步中枢。 你可以把自己的 Obsidian Vault、项目文档、提示词、知识库、上下文文件同步到自己的服务器上。本地文件一修改，它会毫秒级检测变化并自动触发同步。以后不管是 Claude、Codex、OpenClaw，还是 Obsidian 插件，都可以围绕同一份资料库来工作。
  - 我做这个东西最核心的原因不是为了替代 Git，也不是为了做一个复杂网盘。
  - 它解决的是另一个问题：在 AI 时代，我们会有越来越多自己的资料、上下文、项目记忆和工作流文档。这些内容不应该散落在不同软件里，也不应该完全被某个平台绑定。它应该是自己能掌控、能迁移、能备份、能接入不同 AI 工具的一层资料基础设施。
  - ClawMd Hub 现在是 Node.js 服务端加跨平台 Node 客户端，可以跑在 macOS、Linux、Windows 上。后续也可以扩展 iOS、Android、桌面安装包、Obsidian 插件、Codex 插件、Claude/OpenClaw 连接器，甚至 MCP Server。
  - 它支持自动同步、文件监听、服务端索引、冲突副本、软删除和回收站。删除文件的时候，服务端不会直接硬删除，而是标记为软删除并保留记录。不过它不做版本回滚，版本历史和回滚我建议配合 Git 使用，这样更清晰，也更可靠。

- https://github.com/stefandanzl/obsidian-smartsync /202606/ts
  - Plugin to sync files to self hosted Webdav Server based on checksum comparison.
  - Bidirectional Sync – Keep your vault in sync both ways, with intelligent conflict detection
  - Live Sync (Mod Sync) – Automatically sync files as soon as you edit them
  - Auto Sync – Configure interval-based automatic synchronization
  - Push/Pull – Force one-directional sync when needed
  - https://github.com/stefandanzl/smartsyncserver
    - a custom backend that can be easily deployed with Docker.

- https://github.com/Rigter/devitri /MIT/202606/go/ts/svelte
  - Bidirectional sync and self-hosted web dashboard for Obsidian vaults.
  - Devitri keeps your notes synchronized across devices using content hashes (SHA-256) and three-way merge, while giving you a minimal web UI to browse vaults and manage device access. You run the stack; your data stays on your infrastructure.

- https://github.com/xeaser/opencode-obsidian-sync /MIT/202602/ts
  - Sync OpenCode AI conversation sessions to Obsidian as structured Markdown notes with Dataview dashboards, auto-tagging, and real-time sync
  - Dataview community plugin (for dashboard queries)
  - Local REST API community plugin (required)
# feat-code/scripts
- https://github.com/Tzadikimctf/loom /202606/ts
  - Obsidian plugin for executing ordinary fenced Markdown code blocks.
  - loom is intended for research and exploratory notes where code, proofs, solver queries, and runtime output should stay readable in the document. It adds execution controls to normal fenced code blocks and renders transient output beneath the block. The source block is not rewritten into a plugin specific format.
  - loom treats a fenced block as executable when the fence info string resolves to a supported language alias. The parser walks the active Markdown buffer, skips managed loom output sections, normalises the fence language, and creates a stable block descriptor.
  - Languages are grouped into vault level packages. A vault can enable only the packs it needs, then optionally disable individual languages inside those packs.

- https://github.com/mnaoumov/obsidian-codescript-toolkit /MIT/202606/ts
  - allows to do a lot of things with JavaScript/TypeScript scripts from inside the Obsidian itself.
  - formerly known as Fix Require Modules
# feat-data
- https://github.com/chrisgrieser/obsidian-quadro /MIT/202606/ts
  - Plugin for social-scientific Qualitative Data Analysis (QDA). 
  - An open alternative to MAXQDA and atlas.ti, using Markdown to store data and research codes.
# feat-organzing
- https://github.com/Agents365-ai/obsidian-ai-tagger-universe /MIT/202606/ts
  - plugin that leverages AI to automatically analyze note content and suggest relevant tags, supporting both local and cloud-based LLM services.

- https://github.com/jamiefdhurst/obsidian-inbox-organiser /MIT/202606/ts
  - Capture any new notes into an inbox and periodically prompt to organise these into other folders within the vault.
# feat-reading/writing
- https://github.com/chrisgrieser/obsidian-proofreader /30Star/MIT/202512/ts
  - AI-based proofreading and stylistic improvements for your writing. 
  - Changes are inserted as suggestions directly in the editor, similar to suggested changes in word processing apps.
  - Suggested changes are inserted directly into the text: Additions as ==highlights== and removals as ~~strikethroughs~~ .

- https://github.com/zhuzhige123/obsidian-weave-reader /GPL/202606/ts/svelte
  - 如果你希望 Obsidian 不只是笔记仓库，也是你正经读书的地方，可以试试 Weave EPUB Reader。
  - 它适合：边读边把句子记进 Markdown 的人；做专题研究、想把摘录画进 Canvas 的人；用 Weave 做间隔复习、想把书中段落制成卡片的人；同时推进多本书、需要月历排期而不是「开十本读半页」的人。
  - 上手很轻：把 EPUB 放进 Vault，从书架打开，选中文字即可摘录。摘录会带着回到原书的位置信息；你改笔记、删摘录或换颜色，书里的高亮也会跟着变。
  - 更完整的五条工作流（自动摘录、Canvas、制卡、回链、增量阅读）

- https://github.com/DuckTapeKiller/global-book-search /MIT/202606/ts
  - metadata aggregation plugin for Obsidian. It facilitates the creation of comprehensive book notes by consolidating data from multiple international sources, scraping dynamic web content, and applying automated enrichment pipelines.
  - When a book is selected, the plugin initiates a sequential enrichment process
  - To integrate with a local Calibre library, the Calibre Content Server must be active
  - Based on the original https://github.com/anpigon/obsidian-book-search-plugin

- https://github.com/PixeroJan/obsidian-storyline /MIT/202606/ts
  - StoryLine transforms your Obsidian vault into a complete book planning and writing tool. 
  - Organize scenes, build characters, manage locations, track plotlines, and monitor your progress, all inside Obsidian.
# feat-themes/views/ui
- https://github.com/Kigrok/obsidian-library-plugin /MIT/202606/ts
  - plugin that organizes movies, series, and other media as visual cards with automatic metadata.
  - Search and add titles in-app, auto-fetch metadata, track progress, and wire everything into your graph.
  - Version 2 — full rewrite. Library is now a dedicated tab (ribbon icon), with in-app search across multiple sources (OMDb, Open Library), per-category folders
  - Progress Indicators — Visual progress bars on cards and note headers show how much you've watched or read.

- https://github.com/Murchi1k/obsidian-lorebase-plugin /MIT/202606/ts
  - a personal media library for Obsidian, designed to organize and track your favorite content directly inside your vault

- https://github.com/johansan/obsidian-featured-image /MIT/202603/ts
  - plugin that automatically finds and sets thumbnail images for your notes. It detects the first image, YouTube link, or Auto Card Link in each document, downloads external images locally for instant loading, and creates optimized resized thumbnails.
  - The main use case for Featured Image is when you want a property with an image in each markdown file, typically for Bases or Dataviews.
  - Works With Your Favorite Plugins: bases, dataview

- https://github.com/Devon22/obsidian-mediaviewer /MIT/202606/ts
  - plugin designed for Obsidian, aiming to provide an intuitive media browser that allows users to easily view media files (such as images and videos) within their notes.
  - Media Browser: View all media files in a note in full-screen mode.
  - Create Gallery Block: Create a media gallery block to display multiple media files in a grid format within a note.
  - https://github.com/Ephox1/Gallery-Forge
    - Drag-and-drop image galleries for Obsidian, powered by Bases. Thumbnails in your vault, originals stay put.
  - https://github.com/ghyatt/obsidian-bases-image-gallery
  - https://github.com/LucEast/obsidian-bases-image-position
    - Control image positioning in Bases Card Views via frontmatter properties.

- https://github.com/ratiger/obsidian-banyan /GPL/202606/ts
  - A card-based homepage for Obsidian —— browse, organize, and navigate notes effortlessly with multi-tag filtering.

- https://github.com/jillro/obsidian-cards-view-plugin
  - Plugin for Obsidian.md. Displays a card view of your notes.

- https://github.com/anupchavan/obsidian-custom-views
  - Create custom HTML, CSS, and JavaScript views for Obsidian notes based on matching rules.

- https://github.com/obsidianmd/obsidian-maps
  - Map layout for Obsidian Bases. Display your notes as an interactive map view.
  - https://github.com/ccmdi/obsidian-map-plus
    - customizable map layout for Obsidian Bases. This plugin functions similarly to the official Maps plugin, but is more performant for big vaults, adds extensibility with a tag hierarchy, adds thumbnail support to locations, and allows more customizability in general.
  - https://github.com/Requiae/obsidian-leaflet-bases-plugin
    - Interactive map view inside your Obsidian bases.
  - https://github.com/isaiahsarju/map-note
    - Add location notes that the Bases Map view will render.

- https://github.com/saberzero1/quartz-themes
  - Quartz-compatible Obsidian themes.

- https://github.com/Obsidian-TTRPG-Community/fantasy-statblocks /MIT/202601/ts/svelte
  - Create Dungeons and Dragons style statblocks for Obsidian.md
  - Create, manage and view a Fantasy Bestiary in Obsidian.

- https://github.com/johanbook/obsidian-worldbuilding-maps
  - plugin that adds a bases view that plots coordinates from your vault notes on an image-based map. It is intended for TTRPG and worldbuilding.

- https://github.com/InlitX/Obsidian-Dashboard-Gallery
  - Beautiful, ready-to-use dashboard templates for Obsidian PKM
# feat-template
- https://github.com/SilentVoid13/Templater /5.1kStar/AGPL/202606/ts
  - https://silentvoid13.github.io/Templater
  - a template plugin for Obsidian.md. 
  - It defines a templating language that lets you insert variables and functions results into your notes. 
  - It will also let you execute JavaScript code manipulating those variables and functions.

- https://github.com/nates-foo/obsidian-dynamic-templates /202403/ts/inactive
  - plugin for templates that produce Markdown dynamically. Compatible with Dataview.
  - The main goal of this plugin is to offer a templating system where the generated content can be updated when state changes AND exists as plain Markdown. 

- https://github.com/nyinyinyanlin/profile-vault-obsidian
  - A modular Obsidian vault template for professional profile management, career tracking, and AI-assisted application preparation 

- https://github.com/gusbavia/pbi-project-hub
  - Agent skill that builds a complete Power BI project delivery vault in Obsidian: per-client isolation, 6-phase lifecycle, sprint board

- https://github.com/Gchapolin/claude-brain /MIT/202605/python
  - Obsidian setup template for managing multi-project knowledge graphs with iCloud sync, quick capture, and auto-detection of new projects.

- https://github.com/resMagi/obsidian-media-starter-vault
  - Obsidian vault template for tracking films, series, books, games & more.

- https://github.com/groepl/Obsidian-Templates
  - A repository containing templates and scripts for #Obsidian to support the #Zettelkasten method for note-taking.
  - Obsidian is a note-taking and knowledge management app from Shida Li and Erica Xu. It works on top of a local folder of plain text Markdown files and lets you turn a collection of plain text files into a rich network of linked thought.
  - Zettelkasten is a personal tool for thinking and writing created by Niklas Luhmann. It has hypertextual features to make a web of thought possible. The difference to other systems is that you create a web of thoughts instead of notes of arbitrary size and form, and emphasize connection, not a collection.
  - https://github.com/groepl/Obsidian-Zettelkasten-Starter-Kit
    - A Starter Kit for Obsidian with all essential elements to build up your own Zettelkasten system.

- https://github.com/PSPedro176/obsidian-customer-notes-template
  - lightweight Obsidian vault for tracking customer accounts, use cases, meetings and tasks — with daily notes linked to use cases, TaskNotes tasks, customer notes, use case notes, and embedded bases that tie them together. 
  - Flat folder layout, no methodology to learn. 
  - Built with Databricks field work in mind, but generic enough for any account-based note-taking.
  - The plugin's default view bases (tasks, kanban, calendar, agenda, mini-calendar, relationships). The Embedd view in tasks-default.base lists a use case's open tasks and is embedded in each use case.

- https://github.com/brianpetro/obsidian-smart-templates
  - Smart Templates is an AI powered templates for generating structured content in Obsidian. 
  - Works with Local Models, Anthropic Claude, Gemini, OpenAI and more.

- https://github.com/PaperBell-Org/Obsidian-PaperBell
  - An obsidian template vault for tracking your academic life.

- https://github.com/ArtemXTech/claude-code-obsidian-starter
  - Free starter kit: Claude Code + Obsidian. 
  - Pre-configured vault with skills for projects, tasks, clients, and daily routines. Just open and go.
# feat-graph
- https://github.com/zsviczian/excalibrain /MIT/202605/ts
  - A graph view to navigate your Obsidian vault
  - interactive, structured mind-map of your Obsidian Vault generated based on the folders and files in your Vault by interpreting the links, dataview fields, tags and YAML front matter in your markdown files.

- https://github.com/clarkelucianot2-eng/knowledge-graph-cli /MIT/202606/python
  - A versioned, local-first knowledge graph for notes, code, and people.
  - Plain-text nodes, plain-text edges, git-versioned. No SaaS, no LLM required.
  - Obsidian, Notion, and Roam are great for notes — but they don't give you a real graph you can query, version, or own. They're locked in their own formats, behind their own sync, and most "graph" features are an afterthought.
  - This CLI gives you: A real property graph (nodes + typed edges), stored as Markdown + YAML
  - Queryable (Cypher-lite subset, plus plain jq over the JSON export)
  - Obsidian-compatible (every node is a .md file with frontmatter)
# feat-canvas
- https://github.com/mukiwu/canvas-note-preview /MIT/202606/ts
  - A Heptabase-like note preview feature for Obsidian Canvas. 
  - When you click on a note node in Canvas, it automatically displays the note content in a sidebar panel.
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

- https://github.com/mathiasconradt/tektite /apache2/202606/js
  - Minimalistic, lightweight markdown knowledge base app for macOS and Linux. Open source Obsidian alternative.
  - It keeps the core workflow simple: open a local folder, write Markdown notes, preview them live, and see how they connect in the graph.
  - no login, cloud sync service, telemetry, remote storage, account system, or plugin system. Your vault is just a folder on disk, and if you want sync, plain Git works nicely.
  - Click Markdown links and [[wikilinks]] in preview to open linked notes.

- https://github.com/gamosoft/NoteDiscovery /2.6kStar/MIT/202606/python/js
  - https://gamosoft-notediscovery-demo.hf.space/
  - a lightweight, self-hosted note-taking application, all running on your own server.
  - 似乎不支持bases
  - [NoteDiscovery: New free and open source self hosted alternative to Obsidian : r/selfhosted _202511](https://www.reddit.com/r/selfhosted/comments/1opxmud/notediscovery_new_free_and_open_source_self/)
    - For now allows markdown editing, automatic saving, undo/redo, custom themes, plugins (basic support for now)...

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

- https://github.com/loreapp-io-dev/LoreNote
  - open-source alternative to Obsidian. Local-first, lightning fast, and fully extensible. Your data, your control.
# examples-vault
- https://github.com/obsidian-pkm-vault/awesome-obsidian-vault /md
  - Awesome list of obsidian vaults

- https://github.com/owlman/CS_StudyNotes /GPL/202606/js
  - 这是一个面向 CS 学习者与工程实践者 的长期维护型计算机知识笔记库，整体风格倾向于 概念理解、知识结构与可复用判断。
  - 所有笔记均使用 Markdown 编写，可直接在 GitHub 上按目录的自然分类进行阅读
  - 若希望获得更好的体验（双链、反向链接、知识网络），推荐使用 Obsidian或在 VS Code 中配合 Foam 插件，可将项目根目录下的 Obsidian-README.md 当做入口文档进行阅读。

- https://github.com/blueraina/group-vault /202606/ts
  - https://group-vault.pages.dev/
  - 群知识库是一个由群友共同维护的 Obsidian Markdown 笔记库。维护者主要在 Obsidian 中编辑，通过 Obsidian Git 插件同步到 GitHub；网站由 Quartz 构建并发布到 Cloudflare Pages。
  - 不断更新的数学笔记
  - 收录并整理 高等代数白皮书、复旦习题集、谢惠民数学分析 等内容。
  - 支持 Obsidian 双链、局部图谱与全局图谱。
  - 提供评论管理页，方便查看和处理近期评论
  - AI 检索笔记功能：结合 AI查询改写+embedding 检索+BM25F 稀疏检索+PageRank 加权+RRF 融合排序+rerank 精排与对话模型生成报告，帮助你更精准地定位相关笔记和学习路径！

- https://github.com/CLSherrod/crm-markdown /GPL/202606
  - https://christophersherrod.com/crm/
  - simple, local-first CRM in Markdown for tracking contacts, conversations, follow-ups, and relationships—without SaaS lock-in.
  - The system is intentionally simple: one person = one contact note.
    - Each contact note includes the person’s profile, relationship type, relationship tier, follow-up rhythm, next contact date, and communication log.
  - One Markdown file per person
  - One communication log per person
  - Monthly, quarterly, yearly, and custom follow-up cadences
  - Obsidian Bases dashboards for reminders

- https://github.com/CodyLiska/Obfluence-Suite /202510/md
  - Obfluence is a modular, opinionated Obsidian framework designed to bring the structure and scalability of Confluence to your personal knowledge base.
  - This repository contains three main Obsidian vault templates:
  - Obfluence Core: foundational layouts, templates, and best practices
  - Obfluence HomeLab: organize, document, and automate your self-hosted infrastructure
  - Obfluence Personal: track your goals, habits, health, finances, and daily life
  - Each vault is fully modular and extensible — plug them into your own workflows or use them as-is to level up your digital organization.

- https://github.com/stefanimp/obsidian-second-brain-starter
  - clean Obsidian starter kit for building a practical second brain with MOCs, properties, templates, and review workflows.
  - Maps of Content (MOCs) as living indexes; 
  - Dataview/Bases-style queries for review; 
  - an optional AI-friendly project memory layer for focused assistant handoffs.
  - https://github.com/Gleb-Vlasov/obsidian-vault
    - Obsidian vault template (EN + RU). Auto-MOC for new folders, Dataview-driven section maps, Templater-based frontmatter, color-coded graph
  - https://github.com/Gleb-Vlasov/obsidian-vault-skill
    - Claude Code skill that auto-builds a fully automated Obsidian vault: Dataview MOCs, Templater frontmatter, two-layer tags, graph-connecte…

- https://github.com/kepano/kepano-obsidian /MIT
  - https://stephango.com/vault
  - My personal Obsidian vault template. A bottom-up approach to note-taking and organizing things I am interested in.

- https://github.com/obsidian-community/obsidian-hub 
  - https://publish.obsidian.md/hub
  - This is an experimental vault that is maintained by the Obsidian community.
  - For best results we recommend downloading the current version of this vault locally and opening it in Obsidian or browsing it in our publish site.

- https://github.com/bairihai/Obsidian-template-vault /GPL/202606
  - obsidian打包预制模板仓库。样板间，拎包入住。持续更新至今已三年。

- https://github.com/drjliddy-max/worldbuilding-kb-template /MIT
  - Obsidian + Dataview template for citation-grounded worldbuilding knowledge bases.
  - It is, quite literally, a relational database for a fictional world, built as an Obsidian vault
  - This template ships with structure and rules but no world data. You bring your own world.

- https://github.com/pricklywiggles/niamos
  - A personal Obsidian vault running a modified PARA method, plus the templates, queries, and Claude Code skills that make it work day-to-day.
  - https://github.com/rhincodon-studio/obsidian-brain-template
    - Obsidian External Brain template with PARA methodology and Claude Code integration

- https://github.com/tieubao/til 
  - Personal knowledge base following Zettelkasten + LLM Wiki pattern. Obsidian-compatible.
  - A personal knowledge base following the Zettelkasten methodology, maintained by LLMs using the LLM Wiki pattern.

- https://github.com/crouffer/obsidian-bible-vault /MIT/202606/python
  - Obsidian vault for Bible study: 4, 427 interlinked notes for every person, place, and book in the KJV — genealogies, verse references, coordinates, and timelines as plain Markdown.
  - The data is the point. The vault lives in vault/ and is ready to use — no build step required. (A Python script to regenerate it from source is included for the curious)

- https://github.com/Olgafoliolate832/profile-vault-obsidian
  - Manage your career profile in Obsidian with a modular vault for CVs, applications, and professional history

- https://github.com/resMagi/obsidian-media-starter-vault
  - Obsidian vault template for tracking films, series, books, games & more.

- https://github.com/stormyark/Obsidian-Vault
  - https://md.stormyark.de/Obsidian-Vault/Obsidian-Vault
  - a copy of my Obsidian Vault, scrubbed of personal information that you can use as a template or inspiration for your own vault.

- https://github.com/shervinsahba/obsidian-icewind /202604
  - https://icewind.quest/
  - icewind.quest is a hosted Zettelkasten-style notebook. 
# examples
- https://github.com/xnohat/webobsidian /MIT/202606/ts
  - A self-hosted, Obsidian-compatible web app for your Markdown "second brain".
  - Point it at a folder of Markdown files and edit your notes from any browser — with a CodeMirror editor, live preview, wikilinks, an interactive graph, full-text search, GitHub sync (incl. Git LFS), an API for AI agents, and community-plugin support.
  - It is single-user and self-hosted: one master password protects the whole app, all configuration lives in a plain data/settings.json (no database engine), and the entire stack runs from a single docker compose up.
# utils-markdown/yaml
- https://github.com/flowershow/markdowndb /490Star/MIT/202605/ts/sqlite
  - https://github.com/datopian/markdowndb
  - https://markdowndb.com/
  - JS library to turn markdown files into structured queryable database (SQL-based and simple JSON). 
  - It helps you build rich markdown-powered sites easily
  - Parses your markdown files to extract structured data (frontmatter, tags etc) and creates an index in a local `SQLite` database
  - Provides a lightweight javascript API for querying the database and importing files into your application

- https://github.com/intellectronica/mdbasequery /MIT/202602/ts
  - an Obsidian Bases-compatible query engine for Markdown vaults.

- https://github.com/kiwifs/kiwifs /656Star/BSL/202606/go/ts
  - https://docs.kiwifs.com/
  - Markdown filesystem for agents and teams.
  - KiwiFS makes markdown files writable, searchable, queryable, versioned, and human-readable. Files are the source of truth. Everything else is a derivative index you can rebuild.
  - Git versioning: Every write is an atomic commit. Blame, diff, point-in-time restore.
  - DQL queries: SQL-like queries over frontmatter. TABLE, LIST, COUNT, WHERE, SORT, GROUP BY
  - 6 access protocols: REST, MCP, NFS, S3, WebDAV, FUSE. All flow through one storage layer.

- https://github.com/rhsev/grubber /202606/go
  - Data retrieval for Markdown files. Think Dataview without Obsidian. Works on macOS and Linux.
  - A data retrieval tool for Markdown and other text files with metadata. It just grubs fast through a big data field.
  - YAML code blocks in Markdown are usually used as code examples. grubber treats them as structured data records that live next to their context, across an entire directory of files. Think dataview without Obsidian.

- https://github.com/k-lar/dynomark /MIT/202505/go/单文件/inactive
  - Dynomark strives to be a markdown query language engine, similar to obsidian's Dataview plugin.
  - This program can be used with editors like neovim, vscode and emacs to provide a similar experience to Dataview (but very barebones for now).
  - https://github.com/k-lar/vscode-dynomark
    - This extension is a wrapper around that engine, and provides a simple way to query your markdown files.

- https://github.com/eristoddle/mdquery /MIT/202509/python/ts/inactive
  - Universal markdown querying tool with SQL-like syntax for searching and analyzing markdown files across different note-taking systems and static site generators.
  - Full-Text Search: Fast content search with SQLite FTS5
  - Wikilinks, Nested Tags, Frontmatter
  - https://github.com/JMARyA/mdq /202512/rust/inactive
    - command line tool to query markdown documents which have yaml frontmatter.
  - https://github.com/pkarpovich/ovq /rust
    - Query Obsidian vault files by frontmatter properties using Dataview-style syntax. Built for Claude Code integration.

- https://codeberg.org/SebastianRzk/Looksyk /AGPL/202606/rust/ts
  - https://sebastianrzk.codeberg.page/looksyk
  - A simple personal knowledge platform with a focus on clean markdown files, simple queries and a journal.

- https://github.com/sytone/obsidian-queryallthethings /MIT/202602/ts
  - https://sytone.github.io/obsidian-queryallthethings/
  - Query all your data stored in Obsidian, this plugin allows SQL based queries against the data collections available in Obsidian and Dataview. 
  - Output can then be rendered by Handlebars

- https://github.com/mnaoumov/obsidian-nested-properties
  - Obsidian plugin that allows to view/edit nested frontmatter properties.

- https://github.com/sidequery/mdlint /rust
  - A markdown linter for knowledge bases. Supports backlinks, frontmatter, etc.

- https://github.com/Jeff-Kazzee/braincheck
  - A typechecker for Markdown knowledge bases - enforce one schema across all YAML frontmatter (zero-dependency Python CLI).

- https://github.com/dstengle/markdown-queries /MIT/202401/ts/inactive
  - VScode extension to add dynamic frontmatter and content sql queries to markdown previews
  - heavily influenced by Obsidian Dataview
  - This is more POC at this point, but it is possible to put a sql query against a specific sqlite database created by MarkdownDB
    - The extension declares that it extends the `markdown-it` processor in the standard markdown extension.
    - It provides a highlighter plugin to the markdown parser that calls a service object to run queries on the sql.js database that is loaded into memory on initialization from the `markdown.db` file in the workspace.

- https://github.com/AUL-DoX/aul-local-folder-index /MIT/202605/js
  - plugin for indexing local folders into Dataview-compatible notes without moving original files.
  - It reads folders on your computer and creates Dataview-compatible index notes inside your vault. 
  - The plugin is meant to make Obsidian work as an index for files that remain outside Obsidian.

- https://github.com/mfarragher/obsidiantools /BSD/202507/python/inactive
  - a Python package for getting structured metadata about your Obsidian.md notes and analysing your vault
  - Access a networkx graph of your vault (vault.graph)
  - Get summary stats about your notes & files, e.g. number of backlinks and wikilinks, in a `Pandas` dataframe
  - Retrieve detail about your notes' links and metadata as built-in Python types
  - The JSON content of each canvas file is stored as a Python dict in vault.canvas_content_index

- https://github.com/FreeGrid/dataview_site /202511/python/inactive
  - Transform the knowledge base currently managed in the table into individual Markdown files for each line. Display the knowledge table on a webpage and list the notes corresponding to each line. 
  - Take knowledge in csv, convert them to YAML-rich documents, and surface the whole corpus as interactive comparison tables—no Obsidian required.
  - This repo bundles everything needed to go from CSV → Markdown → JSON → MkDocs
  - Render: serve the site with MkDocs + Material, where a Dataview-inspired JS/CSS pair turns fenced dataview blocks into Excel-style tables (search, filters, pagination, CSV export).

- https://github.com/jobindjohn/obsidian-publish-mkdocs
  - A Template to Publish Obsidian/Foam Notes on Github Pages (uses MkDocs)

- https://github.com/h-sphere/sql-seal /MIT/202605/ts
  - https://hypersphere.blog/sql-seal/
  - SQLSeal allow you to query for files, tags and tasks in your vault using familar SQL syntax. It also enables you to preview any CSV file in your vault as a database. It brings fully featured database into your vault!
  - you can use it by creating sqlseal codeblocks in your notes. 
# utils-import/export
- https://github.com/neuralsignal/obsidian-import /MIT/202606/python
  - https://neuralsignal.github.io/obsidian-import/
  - Extract files (PDF, DOCX, PPTX, XLSX, CSV, JSON, YAML, images) into Obsidian-flavored Markdown.
  - The mirror of obsidian-export: where obsidian-export converts Obsidian notes to PDF/DOCX, obsidian-import converts external documents into Obsidian-ready markdown with YAML frontmatter.

- https://github.com/ShrekBytes/advanced-pdf-export /GPL/202606/ts
  - Export Obsidian notes as pixel-perfect PDFs with six style presets, manual page breaks, full layout control, and a live preview — all from a full-screen modal panel.
  - Desktop only — requires the Obsidian desktop app (uses Electron's print pipeline).
  - [I built an Obsidian plugin for proper PDF export — page breaks, live preview, style presets, and full layout control : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1tvtjjt/i_built_an_obsidian_plugin_for_proper_pdf_export/)

- https://github.com/dcanter64/pdf2md
  - A local Python tool that converts folders of PDF files into Markdown files organized as an Obsidian-compatible vault.
  - Extracts text with PyMuPDF.
  - Skips oversized or problematic PDFs instead of crashing.

- https://github.com/hyungyunlim/obsidian-social-archiver-releases /MIT/202606/ts/svelte
  - https://social-archive.org/
  - Archive social media posts from 8 platforms into Obsidian
  - Archive social media posts, web pages, newsletters, podcasts, and other supported sources to your private Social Archiver library, with clients for web, mobile, Chrome, Obsidian, and a macOS desktop app.

- https://github.com/zoni/obsidian-export /BSD/202508/rust/inactive
  - Rust library and CLI to export an Obsidian vault to regular Markdown
  - Recursively export Obsidian Markdown files to CommonMark.
  - Supports [[note]]-style references as well as ![[note]] file includes.
  - Runs on all major platforms: Windows, Mac, Linux, BSDs.

- https://github.com/wikty/obsidian-table-exporter /MIT/202606/ts
  - https://obsidian-plugins.lanternnight.top/plugins/table-exporter/
  - plugin to export rendered Markdown tables and Bases views (Table, Cards, List) to PNG, CSV, Excel, and PDF — with scroll-stitching for virtualized Bases views.
  - t works from the rendered table or Bases view in the active note, so image and PDF exports stay much closer to what you actually see in Obsidian.

- https://github.com/knu/obaq /BSD/202606/ts
  - CLI query processor for Obsidian Bases
  - This tool aims to process Base queries with compatibility against the Obsidian Bases specifications.
  - The tool supports YAML queries

- https://github.com/velviagris/obsidian-local-backup
  - Automatically creates a local backup of the vault.
# utils-cli
- https://github.com/reekta92/clin-rs /GPL/202606/rust/纯tui
  - TUI note management app inspired by Obsidian
  - A TUI reimagination of Obsidian — feature-packed note management in your terminal.
  - clin is a FOSS, minimal(around 2-5~ megabytes of binary) and TUI alternative for the note management app Obsidian. It mainly provides the biggest features of Obsidian(markdown editing and rendering, .canvas files, graph view etc.) in a extremely compact package and really minimal resource usage, written in Rust at a TUI environment.
  - It's goal to provide you a feature-packed note management app right at your terminal while keeping the UI/UX easy and accessible. 
  - It's 90% compatible with Obsidian you can literally copy-paste your Obsidian vault to the clin vault and it just works without a problem, unsupported stuff are image rendering, databases, Obsidian plugins and some small features here and there.
# utils
- https://github.com/Panda-995/obsidian-dashboard /MIT/202606/css
  - Zero-configuration dashboard for Obsidian that auto-scans your vault and displays comprehensive writing statistics & visualizations
  - 必须 Dataview

- https://github.com/philoserf/obsidian-vault-changelog /MIT/202606/ts
  - https://philoserf.github.io/obsidian-vault-changelog/
  - plugin to maintain a changelog of recently edited notes
  - The changelog note is entirely overwritten on each update. Use a dedicated note and embed it elsewhere if you need historical tracking.

- https://github.com/dsebastien/obsidian-update-time /MIT/202606/ts
  - https://dsebastien.github.io/obsidian-update-time/
  - plugin that updates front matter to include creation and last update times
  - a simplified reimplementation of the update-time-on-edit plugin. It was originally created to work around the fact that the original plugin did not integrate well with Obsidian Publish
  - https://github.com/beaussan/update-time-on-edit-obsidian /MIT/202401/ts/inactive
- https://github.com/SmetDenis/obsidian-frontmatter-date-manager /MIT/202606/ts
  - Automatically update created, updated, and viewed dates in YAML frontmatter when editing notes.

- https://github.com/bkyle/obsidian-vault-statistics-plugin /202211/ts/inactive
  - Status bar item with vault statistics such as number of notes, files, attachments, and links.

- https://github.com/tmcw/obsidian-freeform /MIT/202405/js
  - Obsidian freeform plugin. This lets you write arbitrary JavaScript, including importing ESM modules, injecting styles, and much more
  - This brings a taste of Observable to Obsidian. 
  - give you an @observablehq -like experience with editable code blocks that run in isolated iframes.
  - Based on iframes: Everything you write is run within a sandboxed iframe, making it safer to do more creative coding within Obsidian without affecting the surrounding page.

- https://github.com/vsme/astro-obsidian-blog /MIT/202606/ts/astro
  - https://bgo.me/
  - 高性能，使用 Obsidian 进行文章管理，纯自用的博客源码 

- https://github.com/izag8216/mdvigil /MIT/202604/python
  - A CLI toolkit for Obsidian vaults and markdown knowledge bases.
  - Track content freshness. Rename files safely. Generate indexes. Manage tags.
  - Zero API dependency. Works offline. CI-friendly.

- https://github.com/chrisgrieser/shimmering-obsidian
  - Alfred workflow with dozens of features for controlling your Obsidian vault.

- https://github.com/zouxy111/wiki-knowledgebase-share-kit
  - 一套面向 markdown / wiki / Obsidian-style vault 的 10-skill 知识库维护 + 协作包。

- https://github.com/meld-cp/obsidian-encrypt /js
  - Hide secrets in your Obsidian.md vault

- https://github.com/vschroeter/obsidian-virtual-linker /202501/ts/inactive
  - Plugin for obsidian that automatically generates virtual links for text within your notes that match with the titles or aliases of other notes in your vault.
  - create a glossary like functionality
  - works in edit mode and read mode

- https://github.com/ozntel/obsidian-link-converter /202402/ts/inactive
  - This plugin helps you to scan all your links in the vault and convert them to WikiLinks or Markdown format. The plugin also helps you to convert final path to relative, absolute or shortest possible. 
  - You can do link and path conversion at the same time or separately. 

- https://github.com/isaaclyman/novel-word-count-obsidian
  - Obsidian plugin. Displays a word count or other statistic for each file, folder and vault in the File Explorer pane.

- https://github.com/Pr0dt0s/obsidian-html-server
  - Obsidian plugin to serve a vault as an html site.

- https://github.com/husjon/obsidian-file-cleaner-redux
  - helps in removing unused / empty markdown files and attachments based on a few user controlled options.
# integrations
- https://github.com/CinquinAndy/notes-to-strapi-export-article-ai /MIT/202606/ts
  - plugin that streamlines your content creation process by seamlessly exporting your notes to Strapi CMS. With its AI-powered image handling and SEO optimization features

- https://github.com/diegoeis/ghost-writer-manager-plugin /MIT/202605/ts
  - Obsidian plugin to manage and edit Ghost CMS publication directly you Obsidian vault.
  - One-way synchronization from Obsidian to Ghost CMS with post scheduling, YAML metadata control, automatic sync, and an editorial calendar view.
  - One-way sync from Obsidian to Ghost (keeps Ghost as your publishing platform)
  - YAML frontmatter control - Manage all Ghost metadata directly in Obsidian
# okf(open knowledge format)
- https://github.com/yzfly/awesome-okf /MIT/202606/python
  - 开放知识格式(OKF)的中文资料整理, 以及几个把飞书、Obsidian、Notion、GitHub 等转成 OKF 的小工具
  - 开放知识格式（OKF）的中文资料和工具。规范翻译、七个 producer 插件、七个 Claude Code skill、三份向上游的扩展提案。
  - OKF 是 Google Cloud 发布的一份开放规范——把知识定义为一个目录的 Markdown 文件，带 YAML frontmatter，加一小套约定。没有运行时，没有 SDK。
# wiki/knowledgebase
- https://github.com/Ar9av/obsidian-wiki /2.4kStar/MIT/202606/python/js
  - Framework for AI agents to build and maintain a digital brain through Obsidian wiki using Karpathy's LLM Wiki pattern
  - The pattern comes from Andrej Karpathy's LLM Wiki gist: compile knowledge once into interconnected markdown files and keep them current, instead of asking an LLM the same questions over and over (or running RAG every time). Obsidian is how you see the brain. Your AI agent is how you grow it.

- https://github.com/green-dalii/obsidian-llm-wiki /MIT/202606/ts
  - Karpathy's LLM Wiki implementation - multi-page knowledge generation with entity/concept pages and conversational query.

- https://github.com/2233admin/obsidian-llm-wiki /GPL/202606/python/ts
  - LLMwiki turns a team's raw research folder into a reviewed, queryable, self-improving Obsidian wiki. 
  - Headless-first. Cites, doesn't guess.
  - It is not an AI companion. It is a reviewed team memory compiler. Obsidian is the IDE, Git/Gitea review is the ledger, and MCP/CLI tools are the execution surface.
  - Inspired by Andrej Karpathy's LLM Wiki. Markdown is the source of truth; the compiler turns structure into a graph; MCP exposes it.

- https://github.com/GeoffBao/llm-wipa-personal /202606/js
  - Eason's Wikipedia-inspired local web interface for Obsidian knowledge bases — search, graph, canvas, Excalidraw, zero build step
  - A local web app for Obsidian vaults with semantic search, RAG chat, and MCP integration.

- https://github.com/zosmaai/pi-llm-wiki /MIT/202606/ts
  - Self-maintaining, Obsidian-compatible knowledge base for pi. Follows Andrej Karpathy's LLM Wiki pattern.
  - Turn raw sources (URLs, PDFs, markdown, JSON, XML) into a durable, interlinked, LLM-maintained wiki that compounds over time.

- https://github.com/lawyer112/personal-os-wiki /MIT/202606/python/ts
  - Personal OS + Personal Wiki 把收藏夹、语音转写、碎碎念、项目进展和 Agent 产物，变成有人认领、有人提交证据、有人复核的任务。
  - 概念设计美好，但存在lock-in的问题，运行环境较复杂
  - Personal OS + Personal Wiki turns saved links, voice notes, rough ideas, project updates, and agent output into claimed work with evidence.
  - One Product, Two Web Services 
    - This repository is one product and one release package. 
    - At runtime it starts separate services: Personal OS for work state(tasks, projects, agent runs, reviews), Personal Wiki for Markdown knowledge(notes, tags, concepts, graph), and Postgres for OS data.
  - This project sits near the Karpathy-style LLM Wiki, Markdown-as-memory, personal knowledge graph, and agent-memory ecosystem.
    - The difference is the execution layer. Tools in the LLM Wiki space are strong at turning documents into linked knowledge. 
    - If you are exploring LLM Wiki, knowledge graphs, Obsidian-style vaults, or agent long-term memory, this repository is the "what happens next?" layer: turn knowledge into owned work.

- https://github.com/zhuzhaoyun/Molio /apache2+logo/202606/python/ts
  - 本地优先的桌面应用，将知识库管理、AI 写作和多平台发布串联为一体。直接打开你的 Obsidian Vault，通过 Chrome 扩展一键剪藏网页，在 UI 里调用 Claude Code / Codex / Gemini CLI 写文档，扫个码就能在手机微信里跟知识库对话 — 所有内容存在你自己的电脑上，不经过任何第三方服务器。
  - 在 UI 里选 Agent、发消息、看流式输出，自动加载项目 CLAUDE.md 上下文
  - 扫个码就连上个人微信，在手机里跟你的本地知识库对话；发公众号链接还能自动总结并存入知识库
  - 内置 doocs/md 排版 — 微信公众号、知乎等平台格式一键转换，左右分栏实时预览
  - 数据全在本地 — 知识库、AI 对话、微信消息全部存在你自己的电脑上
  - Hono + Node.js + SQLite (better-sqlite3)
  - Electron 40 + electron-builder
  - https://github.com/doocs/md /12.9kStar/MIT/202606/ts/vue
    - 一款高度简洁的微信 Markdown 编辑器：支持 Markdown 语法、自定义主题样式、内容管理、多图床、AI 助手等特性

- https://github.com/bashiraziz/llm-wiki-template /MIT/202604/python
  - A personal knowledge base that compounds over time — maintained entirely by an LLM agent.
  - Inspired by Andrej Karpathy's LLM Wiki pattern (April 2026).

- https://github.com/tteggu87/DocTology /202606/python/ts
  - Obsidian-first LLM Wiki skill pack with ontology-ready bootstrap, canonical JSONL truth layers, and optional graph projection.
  - DocTology is not just a notes repo, not just an ontology toolkit, and not just a graph experiment.

- https://github.com/kytmanov/synto
  - More than just Karpathy’s LLM Wiki, 100% local with Ollama. Drop Markdown notes → AI extracts concepts → your Obsidian wiki auto-links 
# more
- https://github.com/TfTHacker/obsidian42-brat /MIT/202606/ts
  - BRAT - Beta Reviewers Auto-update Tester
  - This is a very special plugin designed to make life much easier for developers and beta-testers of plugins and themes.
  - RAT for short is a plugin that makes it easier for you to assist other developers with reviewing and testing their plugins and themes.
  - Simply add the GitHub repository path for the beta Obsidian plugin to the list for testing and now you can just check for updates. Updates are downloaded and the plugin is reloaded. No more having to create folders, download files, copy them to the right place, and so on. This plugin takes care of all that for you.
