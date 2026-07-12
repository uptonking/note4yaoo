---
title: toc-office-markdown
tags: [doc, markdown, toc]
created: 2020-10-05T09:49:50.474Z
modified: 2021-01-04T17:26:25.032Z
---

# toc-office-markdown

# guide

# popular
- marktext /42.5kStar/MIT/202403/js/vue/inactive
  - https://github.com/marktext/marktext
  - https://www.marktext.cc/
  - simple and elegant markdown editor, available for Linux, macOS and Windows.
  - MarkText uses virtual DOM to render pages
  - 依赖electron-store、codemirror.v5、dragula、vue2、vuex、element-ui.v2、snabbdom
  - https://github.com/marktext/muya /549Star/MIT/202404/ts
    - markdown editor for web browser applications development
    - 依赖fuse.js、marked、katex、ot-json1、prismjs、snabbdom、turndown、vega-lite
    - Muya originated from MarkText, which was originally used in the MarkText and provides Markdown editing support for MarkText. Today, Muya is available as a stand-alone library 
    - What is the relationship between MarkText's version and the Muya's version? None

- https://github.com/Harry-Hopkinson/markdown-editor
  - A markdown editor written in Typescript.
  - Vite+Electron

- https://github.com/ahmedsaheed/Leaflet /CC-BY-NC-SA/202305/ts/inactive
  - https://leaflet.saheed.codes/
  - A minimal distractionless markdown editor designed to quickly navigate between multiple `.md` files in a directory and its sub directories.
  - 依赖codemirror6、@uiw/react-codemirror、electron
  - It features a clean mathematical typesetting, chemical equation rendering, code blocks highlighting and writing statistics 

- https://github.com/foambubble/foam /14.6kStar/MIT/202401/ts
  - https://foambubble.github.io/
  - personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - [Add support for VSCodium](https://github.com/foambubble/foam/issues/26)
    - Foam is officially published to OpenVSX as of 0.7.5_202012

- https://github.com/atom-community/markdown-preview-plus
  - a fork of Markdown Preview that provides a real-time preview of markdown documents.

- markdoc /7.6kStar/MIT/202508/ts
  - https://github.com/markdoc/markdoc
  - https://markdoc.dev/
  - Markdoc is a Markdown-based syntax and toolchain for creating custom documentation sites and experiences.
  - 依赖markdown-it
  - We designed Markdoc to power Stripe's public docs
  - Markdoc extends Markdown with a custom syntax for tags and annotations
  - Markdoc uses `markdown-it` as a tokenizer, building an Abstract Syntax Tree (AST) from the array of tokens emitted by markdown-it.
    - The logic that parses the tag syntax is generated from a `peg.js` grammar.
  - **Markdoc has its own dedicated rendering architecture rather than relying on markdown-it to generate its output** . 
    - Developing an independent rendering system was necessary in order to handle Markdoc's custom tags and support multiple output formats.

- https://github.com/jackyzha0/quartz /12.6kStar/MIT/202606/ts
  - https://quartz.jzhao.xyz/
  - a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites
  - Quartz is a set of tools that helps you publish your digital garden and notes as a website for free. 
  - Quartz v4 features a from-the-ground rewrite focusing on end-user extensibility and ease-of-use.
  - [Backlinks ](https://quartz.jzhao.xyz/features/backlinks)
    - Links in the backlink pane also feature rich popover previews

- https://github.com/microsoft/markitdown /MIT/202411/python
  - Python tool for converting files and office documents to Markdown.
  - a utility tool for converting various files to Markdown (e.g., for indexing, text analysis, etc.)
  - supports: PDF (.pdf) PowerPoint (.pptx) Word (.docx) Excel (.xlsx) Images (EXIF metadata, and OCR) Audio (EXIF metadata, and speech transcription) HTML (special handling of Wikipedia, etc.) Various other text-based formats (csv, json, xml, etc.)
  - https://msftmd.replit.app/
    - Powered by Microsoft MarkItDown, this tool converts various file formats to clean, structured Markdown for easy analysis and indexing.
    - https://x.com/mattppal/status/1867703377888784880
      - If you're wondering how I did this so fast, it was Agent + Assistant + deploy on Replit
  - https://x.com/kepano/status/1867664671446381017
    - https://www.getmarkdown.com/
      - Someone turned the Microsoft conversion tool into a webapp that runs on your device.
    - Very nice. But from a business point hard to understand. Microsoft‘s whole business model is based on ecosystem lock-in, not the quality of products.
    - Markdowns may be easier on ai.

- https://github.com/zcaceres/markdownify-mcp /MIT/202501/ts
  - Markdownify is a Model Context Protocol (MCP) server that converts various file types and web content to Markdown format. 
  - It provides a set of tools to transform PDFs, images, audio files, web pages, and more into easily readable and shareable Markdown text.

- https://github.com/MarkPDFdown/markpdfdown /1.5kStar/apache2/202507/python
  - 一款基于大模型视觉识别的高质量PDF转Markdown工具
  - By utilizing advanced multimodal AI models, it can accurately extract text, preserve formatting, and handle complex document structures including tables, formulas, and diagrams.
  - Customizable Model: Configure the model to suit your needs
# md-parser-generator
- remark 
  - https://github.com/remarkjs/remark/tree/main/packages/remark-parse
  - Parses Markdown to mdast syntax trees. 
  - Built on micromark and mdast-util-from-markdown

- marked /31.5kStar/MIT/202402/ts/NoDeps
  - https://github.com/markedjs/marked
  - https://marked.js.org/
  - A markdown parser and compiler. Built for speed.
  - light-weight while implementing all markdown features from the supported flavors & specification
  - works in a browser, on a server, or from a command line interface (CLI)
  - Marked can be extended using custom extensions. This is a list of extensions that can be used with `marked.use(extension)`.
  - Warning: Marked does not sanitize the output HTML
  - `const html = marked.parse('# Marked in Node.js\n\nRendered by **marked** .');`; 
  - `marked-highlight`语法高亮基于highlightjs实现

- markdown-it /16.8kStar/MIT/202401/js
  - https://github.com/markdown-it/markdown-it
  - https://markdown-it.github.io/markdown-it/
  - https://markdown-it.github.io/
  - Markdown parser done right. Fast and easy to extend.
  - Follows the CommonMark spec + adds syntax extensions & sugar (URL autolinking, typographer).
  - Community-written plugins and other packages on npm.
  - `const md = markdownit(); const html = md.render('# markdown-it rule\n');`; 
  - a fork of https://github.com/jonschlinkert/remarkable /MIT/202505/js/inactive
  - [Lazy highlighting _202408](https://github.com/markdown-it/markdown-it/issues/1045)
    - The current render code seems to do everything in one sequential flow. As soon as it finds a fenced block it passes it though the highlight function. Which works fine if the highlighter being used is ready for it.
    - Loading them all in memory at once (like `highlight.js` allows) results in a MB big minified js file which i very much like to prevent.
    - But the render mechanism in markdown-it seems to be not so happy about a on-demand highlighter.
    - I fixed this by, at parse time, "remembering which fenced blocks" went through the parser and then, once parsed, go over those blocks again and load the syntax highlighting files. That works as lazy enough. It's quite a bit more involved then this but it works. 
- https://github.com/serkodev/markdown-exit /1kStar/MIT/202511/ts
  - https://markdown-exit.pages.dev/
  - A TypeScript rewrite of markdown-it with first-class typings, modern tooling, and enhancements.
  - Async rendering for all rules includeing syntax highlighting and more.
  - Extend the markdown syntax, custom rendering with Plugins.
  - Compatible with markdown-it v14.1.0 and plugin API.
- https://github.com/Simon-He95/markdown-it-ts /MIT/202511/ts
  - A modern, type-safe rewrite of markdown-it in TypeScript: pluggable rules, split parse/render, CommonMark-compatible; fast one-shot parsing and even faster streaming/incremental updates.
  - A TypeScript migration of markdown-it with modular architecture for tree-shaking and separate parse/render imports.
  - Ruler-based rule system
  - API compatibility with original markdown-it
  - https://x.com/simon_he1995/status/1986315649031995633

- snarkdown /2kStar/MIT/202201/js/单文件
  - https://github.com/developit/snarkdown
  - pass a Markdown string, get back an HTML string
  - it's basically one regex and a huge if statement

- https://github.com/eczn/down-parse /ts/2019
  - markdown parser with a wonderful plugin system
# md-database
- https://github.com/flowershow/markdowndb /490Star/MIT/202605/ts/sqlite
  - https://github.com/datopian/markdowndb 
  - https://markdowndb.com/
  - JS library to turn markdown files into structured queryable database (SQL-based and simple JSON). 
  - It helps you build rich markdown-powered sites easily
  - Parses your markdown files to extract structured data (frontmatter, tags etc) and creates an index in a local `SQLite` database
  - Provides a lightweight javascript API for querying the database and importing files into your application
  - 在github code search搜索使用场景，很少用
    - 用在了 portaljs 的启动脚本 `"dev": "npm run mddb && next dev"` .
  - https://github.com/evalscience/deepgov-wiki-poc
    - DeepGov Wiki Proof-of-Concept
    - MDX (Markdown) for project pages
    - MarkdownDB to index markdown files

- https://github.com/timlrx/contentlayer2 /MIT/202505/ts/inactive
  - https://contentlayer.dev/
  - Contentlayer turns your content into data - making it super easy to import MD(X) and CMS content in your app
  - Live reload on content changes
  - Fast and incremental builds
  - Simple but powerful schema DSL to design your content model (validates your content and generates types)
  - Supported Content Sources: Local content (Markdown, MDX, JSON, YAML), Contentful, (later: notion, sanity)
  - Supported env: nextjs, (later: astro, sveltekit)
  - a maintained Contentlayer fork  of https://github.com/contentlayerdev/contentlayer

- https://github.com/sdorra/content-collections /1.2kStar/MIT/202606/ts
  - https://content-collections.dev/
  - Transform your content into type-safe data collections. Eliminate the need for manual data fetching and parsing.
  - Type-safe: Your content is parsed and validated during the build process, guaranteeing accuracy and currency. Content Collections offers a type-safe API to access your content.
  - Transformation: Content Collections allows you to transform your content before it enters your app. You can use it to modify your content, join two collections or even fetch data from a server.

- https://github.com/zce/velite /787Star/MIT/202606/ts
  - http://velite.js.org/
  - Turns Markdown / MDX, YAML, JSON, or others into app's data layer with Zod schema.

- https://github.com/mbailey/sqldown /MIT/202511/python/inactive
  - Bidirectional markdown-sqlite converter - query your docs with SQL, export results as markdown.
  - Bidirectional markdown ↔ SQLite conversion - Load markdown files into SQLite, query with SQL, and export back to markdown.
  - Dynamic schema generation from YAML frontmatter and markdown structure
  - Import markdown collections into queryable SQLite databases
  - Export database rows back to markdown files
  - Watch mode for auto-refresh on file changes
  - Gitignore-aware file filtering
  - Smart change detection (skip unchanged files)

- https://github.com/mpazik/binder /MIT/202605/ts
  - https://binder.do/
  - Headless knowledge base with bidirectional Markdown sync
  - Binder stores your data as a graph of entities: each one a flexible collection of field-value pairs classified by a type like Task, Decision, or Contact. Fields are defined once and reused across types. References link entities directly, forming the graph. Types and fields are defined in .binder/types.yaml
    - Editors, scripts, and agents all write to the same data. 
    - Binder records every change as an immutable transaction, attributed to its source. Full history, undo and redo, replay to any past state.
  - Markdown files are a view over this graph. Navigation rules define where each entity lives on disk. Change a field value and Binder moves the file automatically
  - Open any Markdown file in your coding editor to read, adjust, and review. Binder's LSP provides validation, autocomplete, and navigation across all entity files.
  - Roadmap
    - Full-text and semantic search
    - Transaction log compaction
    - Cross-device synchronisation
    - E2E encrypted backup
    - Encrypted fields
    - Web / Mobile UI

- https://github.com/mdcms-ai/mdcms /MIT/202606/ts
  - https://www.mdcms.ai/
  - https://docs.mdcms.ai/
  - open-source CMS that's Markdown-first.
  - MDCMS treats a PostgreSQL database as the source of truth. Content files are synced between the database and your local filesystem via CLI commands (mdcms push / mdcms pull), keeping your repository clean and your content workflow independent of your deployment pipeline.
  - Developers define schemas in code and sync via CLI. Editors get a visual Studio they never have to leave. AI agents process content through the same API. 
  - Author content in Markdown or MDX with custom component support
  - ⏳ Versioning and publishing: Full draft/publish lifecycle with immutable version history
  - Extensible modules	First-party module system for extending server and CLI behavior
  - Code-first schema: Define content types, fields, and references in TypeScript with Zod validation
  - Embeddable React admin interface with a rich document editor, schema browser, and environment management
  - Auth and RBAC	Session auth, OIDC/SAML SSO, API keys, and role-based access control
  - 📡 roadmap
    - Live preview - Real-time content preview in your frontend
    - Live collaboration - Live co-editing with conflict resolution
    - Media management - Upload, organize, and serve media assets via MinIO/S3
    - Full-text search - Search across content with indexing and ranking
    - Bulk operations - Batch publish, unpublish, and delete actions
  - [Self-Hosting - MDCMS ](https://docs.mdcms.ai/guide/self-hosting)
    - starts the MDCMS server along with PostgreSQL, Redis, MinIO, and Mailhog. Migrations run automatically on first boot.

- https://github.com/Dhravya/notty /MIT/202606/ts/rust
  - https://notty.page/
  - minimal notes app that syncs everywhere.
  - Editor — Built on Novel (TipTap/ProseMirror). Slash commands, bubble toolbar
  - Real-time sync — Every note is a Yjs CRDT document. Edits sync over WebSocket in real time between all your devices and collaborators
  - Offline-first — Notes persist to IndexedDB locally. 
  - Desktop app — Native macOS app via Tauri. Local SQLite database, bidirectional markdown sync to `~/Documents/Notty/`, and cloud sync when available. Works fully offline.
    - 手动 export + import
    - Notes export as .md files with TipTap JSON-to-markdown conversion, and external markdown files can be imported back
  - Cloud sync — When a cloud URL is configured, the desktop app merges local and cloud state bidirectionally (local-first, prefer newer timestamps)
  - Note locking — Lock sensitive notes behind passkey (WebAuthn) verification. Locked notes require biometric/PIN authentication to view or edit

- https://github.com/auxclawdbot/taskflow /MIT/202603/js/inactive
  - Structured project and task management for OpenClaw agents — markdown-first, SQLite-backed, zero dependencies.
  - syncs your markdown files, and optionally installs a macOS LaunchAgent for automatic 60-second sync.
  - Markdown-first — PROJECTS.md and `tasks/<slug>-tasks.md` are the source of truth; edit them directly in any editor or agent session
  - SQLite-backed — bidirectional sync keeps a derived index for fast querying, dashboards, and exports
  - Bidirectional sync — files-to-db and db-to-files modes; check for drift with sync check
  - JSON export — full project/task snapshot to stdout, ready for dashboards and integrations
  - LaunchAgent (macOS) — automatic 60s background sync via launchctl; Linux cron instructions included
  - Zero dependencies — pure Node.js, uses the built-in node:sqlite module (no npm install)

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

- https://github.com/fictorial/gg /201903/js
  - Markdown-backed database with queries, user-defined actions, validators, variable expansion, and reporters in JavaScript
  - gg is a CLI to import, query, act on, and report on local Markdown files with support for user-defined JavaScript extensions.
  - gg supports a subset of Markdown for parsing: headers, paragraphs (the "type-inferred values"), and un-nested bullet lists 

- https://github.com/daeh/zotero-markdb-connect /MIT/202401/ts
  - Zotero plugin that links your Markdown database to Zotero. 
  - Jump directly from Zotero Items to connected Markdown files.
  - Supports various Markdown databases, including Obsidian, logseq, and Zettlr
  - Supports various Markdown databases, including Obsidian, logseq, and Zettlr

- https://github.com/subramanya1997/markdownfs /MIT/202604/rust
  - A high-performance, in-memory virtual file system for Markdown files. Unix-like commands, Git-style versioning, content-addressable storage, and multi-user permissions — built in Rust.
  - Only Markdown (.md) files are supported by design: mdfs only stores .md files. Every file you create must have the .md extension
  - MarkdownFS gives agents a fast in-memory filesystem with built-in commits, permissions, and a REST API 
  - mdfs is also a strong fit for agent workspace use cases: durable markdown memory, inspectable artifacts, search, permissions, commits, and rollback in one shared surface.

- https://github.com/lukesrw/md-database /GPL/202109/ts/inactive
  - Middleware for producing SQL queries from Markdown
  - Currently only SQLite is fully supported, with support for MySQL being worked on.

- https://github.com/edochi/mdvs /MIT/202607/rust
  - https://edochi.github.io/mdvs/
  - in-process validation & search engine for markdown documents — schema inference, frontmatter validation, and local semantic search.
  - mdvs is useful when you have a markdown corpus with structured frontmatter. 
  - Some common cases: Obsidian vaults, Docs-as-code repos (Hugo, MkDocs, Astro)
  - Multi-format frontmatter. YAML (---), TOML (+++), or JSON ({...}), auto-detected per file. Mix freely within one vault.
  - Hybrid search. Vector similarity + BM25 full-text + RRF fusion. 
  - Runs entirely in-process. Local files, single binary. No API keys, no vector-DB cluster, no GPU.
  - Incremental builds. Only changed files are re-embedded; the Lance write itself is also incremental (delete + append + optimize, not a full overwrite). If nothing changed, the model isn't loaded and the index isn't rewritten.
# tools
- monotome /151Star/AGPLv3/202208/js
  - https://github.com/cblgh/monotome
  - a personal knowledge base system. markdown markup, runs in the browser
  - 依赖 marked
  - 原理是 根据url动态读取解析markdown文件，并渲染显示所有文件名，切换文件时会触发fetch
  - 代码量不大，思路清晰
  - Monotome has support for the common `[[wiki]]` syntax
  - Monotome keeps track of backlinks, or incoming links from one article inside monotome to another. 
  - Subjects are ordered into a simple directory structure which is mirrored by index.json.
  - You can fill index.json's subjects by hand if you want to avoid running a script. You can also run node monotome/bin/generate.js, which will update index.json for you.

- NextBook /168Star/MIT/202206/js/inactive
  - https://github.com/amiroff/NextBook
  - https://next-book.vercel.app/
  - 依赖 next11、next-mdx-remote、react、remark、tailwindcss
  - 若屏幕很窄，官方文档会显示水平滚动条，此时滚动会有严重的漂移感
  - easy way to build technical books or documentation with markdown or MDX

- https://github.com/Kffhi/markdown-reader
  - 一个简单的markdown文件解析服务，可以读取服务器指定目录下的md文件并返回相关数据用于前端展示

- https://github.com/shuding/nextra
  - 依赖next、nextra-core、react
  - powerful and flexible site generation framework with everything you love from Next.js.
  - Any change to example/docs will be re-rendered instantly.
  - Nextra first collects all your Markdown files and configurations from the pages directory, and then generates the “page map information” of your entire site, to render things such as the navigation bar and sidebar 
    - By default, the page map contains all .md and .mdx filenames and the directory structure, sorted alphabetically.
    - You can have an `_meta.json` file in each directory, and it will be used to override the default configuration of each page

- https://github.com/plantain-00/simple-doc
  - A Server-less and Build-less markdown document application.
  - 默认显示README.md

- https://github.com/plantain-00/markdown_to_pdf
  - A CLI tool to convert a markdown to a pdf file.

- silverbullet /1.5kStar/MIT/202401/ts
  - https://github.com/silverbulletmd/silverbullet
  - https://silverbullet.md/
  - SilverBullet is an extensible, open source personal knowledge platform. 
  - implemented as an open-source offline-capable web application.
  - At its core it’s a clean markdown-based writing/note taking application that stores your pages (notes) as plain markdown files in a folder referred to as a space. 
  - While SB uses a database for indexing and caching some indexes, all of that can be rebuilt from its markdown source at any time. 
  - extensible with plugs, and you can customize it
  - [Silver Bullet: Markdown-based extensible open source personal knowledge platform | Hacker News_202212](https://news.ycombinator.com/item?id=33843009)

- https://github.com/RICHQAQ/PasteMD /MIT/202512/python
  - 一个常驻托盘的小工具： 从 剪贴板读取 Markdown，调用 Pandoc 转换为 DOCX，并自动插入到 Word/WPS 光标位置。
  - 智能识别 Markdown 表格，一键粘贴到 Excel
  - 智能识别 HTML富文本，方便直接复制网页上的ai回复，一键粘贴到 Word/WPS
# streaming
- https://github.com/vercel/streamdown /4.9kStar/apache2/202509/ts
  - https://streamdown.ai/
  - A drop-in replacement for react-markdown, designed for AI-powered streaming.
  - Streamdown powers the AI Elements Response component but can be installed as a standalone package for your own streaming needs.
  - Drop-in replacement for react-markdown: It supports all of the same props
  - Streaming-optimized - Handles incomplete Markdown gracefully
  - 基于redis实现中断与恢复
  - GitHub Flavored Markdown - Tables, task lists, and strikethrough support
  - Unterminated block parsing - Styles incomplete bold, italic, code, links, and headings
  - Math rendering - LaTeX equations via KaTeX
  - Mermaid diagrams - Render Mermaid diagrams as code blocks with a button to render them
  - Code syntax highlighting - Beautiful code blocks with Shiki
  - Security-first - Built on harden-react-markdown for safe rendering
  - [Introducing Streamdown: Open source Markdown for AI streaming - Vercel _202508](https://vercel.com/changelog/introducing-streamdown)
  - 🍴 forks
  - https://github.com/phaserjs/streamdown-lite
    - A lightweight drop-in replacement for react-markdown, designed for AI-powered streaming with code highlighting.
- https://github.com/goutham-subramanyam/streamdown-poc /202510/ts
  - An interactive playground for Vercel Streamdown - a markdown renderer optimized for AI streaming.

- https://github.com/Simon-He95/vue-markdown-renderer /430Star/MIT/202510/ts/vue
  - https://vue-markdown-renderer.netlify.app/
  - A Vue 3 renderer specifically built for AI-powered streaming Markdown: Monaco incremental, Mermaid progressive, and KaTeX formula speed, with real-time updates and no jitter, ready to use out of the box.
  - Streaming diff code blocks: show diffs as they arrive for instant feedback.
  - Built for scale: optimized DOM updates and memory usage for very large documents.
  - Streaming-first rendering: render partial or incrementally-updated Markdown content without re-parsing the whole document each time. 
  - [Show HN: Vue-Markdown-render – up to 100× faster streaming Markdown for Vue 3 | Hacker News _202509](https://news.ycombinator.com/item?id=45238350)
    - Streamdown targets server-side streaming; our results are for client rendering. Ideal for AI chatbot UIs.
  - https://github.com/Saluana/streamdown-vue
    - Streamdown style streaming Markdown to Vue 3 & Nuxt 3

- https://github.com/beynar/svelte-streamdown
  - Svelte port of Streamdown

- https://github.com/thetarnav/streaming-markdown /266Star/MIT/202505/js
  - https://thetarnav.github.io/streaming-markdown/
  - Experiment making a streaming makdown parser à la ChatGPT.
  - It's single argument is a `Renderer` object, which is an interface to render the parsed markdown tokens to the DOM.

- https://github.com/rossrobino/robino/tree/main/packages/md /MIT/202506/ts
  - An extended markdown-it instance 
  - Syntax highlighting with shiki using the CSS variables theme to style
  - `stream` function to render and highlight a stream of markdown
    - stream streams the result of a markdown stream through the renderer/highlighter.
    - The result will come in chunks of elements instead of by word since the entire element needs to be present to render and highlight correctly.

- https://github.com/lixpi/markdown-stream-parser /MIT/202509/ts
  - https://markdown-stream-parser.lixpi.org/
  - A library designed to incrementally parse Markdown text from a stream of tokens.
  - It's built to handle the ambiguities of LLM-generated streams, which often produce imperfect or invalid Markdown.
  - It combines a finite state machine with regex patterns to determine the best match for each segment.
  - [Evaluate whether continuing with completely custom parser implementation is reasonable, or shall we leverage lexers? _202505](https://github.com/Lixpi/markdown-stream-parser/issues/5)
    - My initial implementation was extremely naive. Currently working on a complete reimagined version that uses `Tree-sitter` for parsing, but provides the same interface for the stream of parsed chunks.

- https://github.com/karminski/streaming-json-js /MIT/202409/js/inactive
  - This library allows for the parsing of JSON as it is being streamed (this means JSON stream can stops at any position), significantly cutting down the time-to-first-token.
  - https://github.com/karminski/streaming-json-go
  - https://github.com/karminski/streaming-json-py
  - handling multiple blobs or JSON with interspersed non-JSON strings can be quite tricky. This library is more focused on handling JSON strings themselves, so users need to manually separate JSON blobs for input or filter out non-JSON structured strings.
  - [I Created a Library to Streamline JSON stream Handling: Introducing streaming-json : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1e9m5wh/i_created_a_library_to_streamline_json_stream/)
    - We wrote a similar algorithm in rust (that have bindings to Python/TS/Ruby) as well ( https://github.com/BoundaryML/baml ) if anyone is interested in a rust implementation.

- https://github.com/ddaras/melony /202510/ts
  - https://melony.dev/
  - Generate React UIs from AI responses in real-time.
  - Zero Latency - Components render progressively during streaming
  - Smart Parsing - Identifies component JSON with delimited blocks
  - Built-in Components - 20+ ready-to-use UI components
  - Markdown Support - Built-in GFM rendering
  - 使用时需要使用 MELONY_UI_GUIDE system prompt

- https://github.com/brillout/react-streaming /MIT/202510/ts
  - HTML Streaming with React — batteries-included and made easy
  - The React team is working on high-level APIs that will eventually make parts of react-streaming obsolete

- https://github.com/nikomatt69/streamdown-tty /MIT/202510/ts
  - Streamtty is inspired by Streamdown but built specifically for terminal/TTY environments using blessed.
  - It handles the unique challenges of streaming Markdown content from AI models in terminals, providing seamless formatting even with incomplete or unterminated Markdown blocks
  - Advanced Tables - Full table support with alignment, borders, and navigation
  - Plugin System - Remark/Rehype compatible plugin architecture
# ui
- https://github.com/BlueprintLabIO/markdown-ui /412Star/MIT/202509/ts/inactive
  - https://markdown-ui.blueprintlab.io/
  - https://markdown-ui.com/
  - An open standard for rendering interactive widgets in plain Markdown
  - Readable everywhere: Preview rich UI, but if unsupported, it's still legible Markdown
  - Zero lock-in: Pure spec—works with any Markdown parser + any UI framework
  - [Show HN: Turn Markdown into React/Svelte/Vue UI at runtime, zero build step | Hacker News _202508](https://news.ycombinator.com/item?id=45024532)
# apps
- https://github.com/motifland/markprompt
  - Markprompt is a platform for building GPT-powered prompts. 
  - It scans Markdown, Markdoc and MDX files in your GitHub repo and creates embeddings that you can use to create a prompt

- https://github.com/rhiokim/haroopad /201606/js
  - Haroopad is a markdown enabled document processor for creating web-friendly documents.

- https://github.com/amitmerchant1990/electron-markdownify /923Star/MIT/202111/js/inactive
  - minimal Markdown Editor desktop app built on top of Electron.
  - Sync Scrolling
# import/export
- https://github.com/liyown/marknative /MIT/202604/ts
  - https://liyown.github.io/marknative/
  - A Markdown rendering engine that generates paginated PNG and SVG output — no browser, no Chromium, no DOM.
  - Most Markdown rendering pipelines go through a browser: Markdown → HTML → DOM/CSS → browser layout → screenshot
  - marknative takes a different path. It parses Markdown directly into a typed document model, runs its own block and inline layout engine, paginates the result into fixed-size pages, and paints each page using a native 2D `canvas` API.
  - The result is deterministic, server-renderable, and completely headless.
  - https://x.com/axiaisacat/status/2039561953358565679
    - 服务端直接跑，零浏览器依赖; 
    - 分页结果完全确定性，每次输出一模一样; 
    - 批量渲染，速度快到飞起
  - Markdown是支持插入HTML的，它支持？
    - 支持的呀，你试试看

- https://github.com/mark-magic/mark-magic /MIT/202402/ts
  - 一个基于 markdown 的数据连接与转换工具，解决不同工具之间数据转换以及部分常用工具之间的协调。
  - joplin => hugo 生成 blog

- https://github.com/LetTTGACO/elog /MIT/202401/ts
  - https://elog.1874.cool/
  - Markdown 批量导出工具、开放式跨平台博客解决方案
  - 随意组合写作平台(语雀/飞书/Notion/FlowUs)和部署平台(Hexo/Vitepress/Halo/Confluence/WordPress等)
  - Elog支持了在生成MD文件之前，将扫描到的图片上传到图床上，并对文档中的图片链接进行替换。 当前支持的图床有： 本地/阿里云oss/腾讯云cos/Github图床
  - https://github.com/LetTTGACO/elog-docs
    - Elog 的使用文档

- https://github.com/kscript/markdown-download /MIT/202401/js
  - 谷歌浏览器插件: 将掘金、知乎、思否、简书、博客园、微信公众号、开源中国、CSDN的文章转为markdown文档并下载 

- https://github.com/gcui-art/markdown-to-image /apache2/202412/ts
  - https://readpo.com/poster
  - This React component is used to render Markdown into a beautiful poster image, with support for copying as an image
  - The project also includes a built-in web editor that can be used as an online Markdown-to-poster editor with a simple one-click deployment.
# utils
- https://github.com/dahlia/hongdown /GPL/202601/rust
  - A Markdown formatter that enforces Hong Minhee's Markdown style conventions
  - implemented in Rust using the Comrak library for parsing
  - [Hong Minhee's Markdown style convention](https://github.com/dahlia/hongdown/blob/main/STYLE.md)
    - Reference-style for external URLs: 类似footnote
    - Use Setext-style (underlined) headings for document titles (H1) and major sections (H2)
    - Use ATX-style (###, ####, etc.) for subsections within a section
# more-md
- https://github.com/mgmeyers/obsidian-kanban /GPLv3/202309/ts
  - https://publish.obsidian.md/kanban/
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/rstudio/rmarkdown
  - rmarkdown package helps you create dynamic analysis documents
