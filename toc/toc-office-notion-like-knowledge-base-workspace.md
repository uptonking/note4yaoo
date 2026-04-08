---
title: toc-office-notion-like-knowledge-base-workspace
tags: [knowledge-base, notion-like, workspace]
created: 2022-06-03T21:27:36.001Z
modified: 2022-06-03T21:34:54.893Z
---

# toc-office-notion-like-knowledge-base-workspace

# guide

- 想要分析notion的block架构设计，可以参考clone示例
  - 扩展思路，前端的block通常对应后端的field字段

- 考虑使用epub/docx/docbook这类规范格式存储内容，方便迁移
  - 支持导入通用格式 markdown/csv
  - 偏代码的格式可考虑 rdf/json-ld

- pkm-patterns
  - memex, xanadu, bulletjournal, zettelkasten
  - 参考github，实现 repo + issues-forum + gitter-im + proj-mgmt + pr + cicd
  - npm的优点，支持各版本的文档分别显示
  - 用代码搜索的思路来实现知识库的搜索
  - 代码的ast和block编辑器的ast处理方式类似，代码symbol跳转和双链类似

- resources
  - search: knowledge-base/workspace/wiki/Personal Information Manager (PIM)
  - self-contained, in the browser
  - [17 Confluence Alternatives - Open Source, Free & Paid in 2024](https://rigorousthemes.com/blog/best-confluence-alternatives-free-paid/)
  - https://github.com/awesome-selfhosted/awesome-selfhosted#document-management
# notion-like-knowledge-base
- siyuan /6.6kStar/AGPLv3/202208/ts/go/支持协作
  - https://github.com/siyuan-note/siyuan
  - https://b3log.org/siyuan/
  - a local-first personal knowledge management system
  - 思源笔记是一款本地优先的个人知识管理系统，支持完全离线使用，同时也支持端到端加密同步。
    - 所有本地功能都是免费的，云端服务需要年付订阅。
    - 不支持网页版，要使用桌面版或移动版
  - SiYuan is made possible by the Vditor and Lute(golang)
  - 用户自己创建的笔记本文件夹下，.sy 后缀的文件用于保存文档数据，数据格式为JSON
  - 桌面端实现依赖electron， 但数据操作使用go实现而不是nodejs

- outline /18.3kStar/BSD > BSL/202302/ts
  - https://github.com/outline/outline
  - https://www.getoutline.com/
  - The fastest wiki and knowledge base for growing teams.
  - 依赖rich-markdown-editor、mobx-react、dnd-kit、framer-motion、i18next、markdown-it、reakit
  - 后端依赖postgres、redis、koa、sequelize、yjs、y-prosemirror、y-indexeddb
  - 与slack集成很好
  - 样式与airframe-react dashboard风格类似
  - 📈 [Add Notion-like inline databases _202402](https://github.com/outline/outline/discussions/6507)
    - [Add a spreadsheet-like UI for structured data (no-code RDBMS) _202502](https://github.com/outline/outline/discussions/8476)
  - [Adopt BSL 1.1 license__202003.v0.41.0](https://github.com/outline/outline/pull/1197)
  - [Convert from slate to Prosemirror_202005.v10.0.0](https://github.com/outline/rich-markdown-editor/pull/150)
  - ref
    - https://github.com/ProseWorker/ProseWriter

- https://github.com/suitenumerique/docs /4.8kStar/MIT/202503/python/ts
  - https://docs.numerique.gouv.fr/
  - A collaborative note taking, wiki and documentation platform that scales. 
  - Docs is built on top of Django Rest Framework, Next.js, BlockNote.js, HocusPocus and Yjs.
  - 前端依赖next15、zustand、yjs、BlockNote、@react-pdf/renderer、react-pdf-table、tanstack-query5、cmdk、docx、idb、react-aria-components
  - 后端依赖djangorestframework3、beautifulsoup4、boto3、gunicorn、markdown、pycrdt、requests、python-magic
  - 似乎为设计插件/扩展架构
  - 📡 集成 suite-docs + odoo
  - Easy to install, scalable and secure alternative to Notion, Outline or Confluence
  - Offline? No problem, keep writing, your edits will get synced when back online
  - Built for productivity (markdown support, many block types, slash commands, keyboard shortcuts).
  - Save time thanks to our AI actions (generate, sum up, correct, translate)
  - Granular access control to ensure your information is secure and only shared with the right people
  - Professional document exports in multiple formats (.odt, .doc, .pdf) with customizable templates
  - Running Docs locally using the methods described below is for testing purposes only. It is based on building Docs using Minio as the S3 storage solution but you can choose any S3 compatible object storage of your choice.
  - [Presentation Upload · suitenumerique/meet _202411](https://github.com/suitenumerique/meet/issues/208)
    - Low priorities
  - [Docs – Open source alternative to Notion or Outline | Hacker News _202503](https://news.ycombinator.com/item?id=43378239)
  - 📡 roadmap
  - 🔀 [Why Yjs server in ts when you can use pycrdt instead ?  _202503](https://github.com/suitenumerique/docs/issues/728)
    - it seems that the server is written in Django but there is a special server for Yjs written in ts. Pycrdt is used for real-time collaboration in JupyterLab. Pycrdt is being used quite extensively in Jupyter-Collaboration.
    - The main problem I see is managing a websocket with django. We have to switch to an ASGI application, use django-channels. To scale you have to use the redis backend and there are many issues open about memory leaks. FastAPI is probably a better candidate.
    - my understanding is that it is not trivial to move to Python for Ydoc because the server needs to understand the BlockNotejs syntax which is custom (for blocks etc.)
    - `pycrdt-websocket` should be server-agnostic. We use it in jupyter_server which is based on Tornado, and in jupyverse which is based on FastAPI.
    - 👷 I feel this is a bit outside of my area of expertise tbh. It could be an interesting option - but it might be quite some work (so imo we'd need a strong reason to switch)
      - If you want to do operations on the document (change it's content) through the BlockNote API, or convert it to / from Markdown / HTML - this is easiest in a Node environment indeed.
  - [Document sometimes freezes when sync editing _202412](https://github.com/suitenumerique/docs/issues/440)
    - A user (Alice) without an error in the update method makes a change to the document
    - Bob's update method throws an error
    - Bob resyncs it's prosemirror state to the other user, effectively undoing Alice's change
- https://git.coopcloud.tech/coop-cloud/lasuite-docs /仅运维/无新功能
  - https://docs.coop/
  - Docs (part of La Suite Numerique) for Co-op Cloud
  - [Autonomic launch docs.coop - Co-operativley hosted open source document editing _202506](https://community.coops.tech/t/autonomic-launch-docs-coop-co-operativley-hosted-open-source-document-editing/4439)
    - Building on the great work of Suite Numerique, we are offering an opportunity to be part of a new collaborative Docs platform as a service
    - We are offering managed Docs instances with full support provided by us

- https://github.com/colanode/colanode /1.3kStar/202506/ts
  - https://colanode.com/
  - Open-source and local-first Slack and Notion alternative that puts you in control of your data
  - Colanode is an all-in-one platform for easy collaboration, built to prioritize your data privacy and control. 
  - Designed with a local-first approach, it helps teams communicate, organize, and manage projects—whether online or offline.
  - 🐛 cons: 不支持导出, 不支持undo/redo, 不支持database预览(只能在单独页面打开)
  - 🌹 feat: database支持多种视图board/calendar
  - 前端依赖tiptap、kysely、fractional-indexing-jittered、zod3、ulid、yjs、radix-ui、floating-ui、@tanstack/react-query.v5、@tanstack/react-virtual、cmdk、date-fns、re-resizable、react-dnd、react-hook-form
  - web依赖@sqlite.org/sqlite-wasm
  - desktop依赖@electron-forge、better-sqlite3
  - server依赖fastify、kysely、bullmq、langchain、pg、sharp
  - Rich Text Pages: Create documents, wikis, and notes using an intuitive editor, similar to Notion.
  - Customizable Databases: Organize information with structured data, custom fields and dynamic views (table, kanban, calendar).
  - Colanode includes a desktop app and a self-hosted server. You can connect to multiple servers with a single app, each containing one or more workspaces for different teams or projects. 
  - All changes you make are saved to a local SQLite database first and then synced to the server. A background process handles this synchronization so you can keep working even if your computer or the server goes offline. Data reads also happen locally, ensuring immediate access to any content you have permissions to view.
  - powered by Yjs - to allow real-time collaboration on entries like pages or database records.
  - [Issues with Undo / Markdown Pasting _202505](https://github.com/colanode/colanode/issues/42)
    - We have temporarily disabled the default undo, because of some issues it was causing related with the way syncing/conflict resolution with Yjs works. Will need to implement it in a different way. 
  - [I built Colanode, an open-source & local-first Slack and Notion alternative that you can self-host : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1khpftl/i_built_colanode_an_opensource_localfirst_slack/)

- https://github.com/docmost/docmost /AGPL/202503/ts
  - https://docmost.com/
  - an open-source collaborative wiki and documentation software. 
  - It is an open-source alternative to Confluence and Notion.
  - Diagrams (Draw.io, Excalidraw and Mermaid)
  - Permissions management
  - [Show HN: I am building an open-source Confluence and Notion alternative | Hacker News _202406](https://news.ycombinator.com/item?id=40832146)
    - We are still using Confluence on-prem (behind VPN). To switch, we need the following: 
      - An export function (PDFs). 
      - An integrated diagram editor like Gliffy. 
      - History / diffs.
  - [Feature Request: 'databases' (special tables) with custom views like Notion _202407](https://github.com/docmost/docmost/issues/78)
  - [[FEATURE REQUEST] Notion-style databases to link/ query/ visualise a set of notes by properties _202501](https://github.com/docmost/docmost/issues/595)
    - Docmost is more of a wiki than a project management tool. I don't see us implementing this anytime soon.
  - [Feature Request: Kanban Style Boards _202502](https://github.com/docmost/docmost/issues/455)
    - No plans to introduce Kanban at this time, but you could do Kanban with the Mermaid integration.

- think /1.8kStar/MIT/202304/ts/nestjs/tiptap/inactive
  - https://github.com/fantasticit/think
  - https://think.codingit.cn/
  - 依赖 MySQL/NextJS/nestjs/tiptap
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 前端依赖 @douyinfe/semi-ui、excalidraw、tiptap2、docx、katex、markdown-it、nextjs、react-pdf、react-query3、tippy.js、yjs
  - 后端依赖 nestjs、typeorm、passport、mysql、yjs
  - Think 是一款开源知识管理工具。通过独立的知识库空间，结构化地组织在线协作文档，实现知识的积累与沉淀，促进知识的复用与流通。同时支持多人协作文档。
  - 为什么停止开发了？
    - 对于文档类产品，无法做出独立的 library 或 framework 给不同需求的团队（或个人），这使得我不确定这件事的意义
    - 对于独立编辑器开发，无论最终以何种形态存在，其表现还是为应用，而非框架（或依赖），能做到的也许只是一种示范
    - 作者本身专攻前端，对高性能、扩展性良好的后端架构心有余而力不足
  - https://github.com/fantasticit/sailkit /202407/ts
  - https://github.com/fantasticit/magic-editor /202301/ts

- logseq /15.9kStar/AGPLv3/202208/clojure/ts
  - https://github.com/logseq/logseq
  - https://logseq.com/
  - A local-first, non-linear, outliner notebook for organizing and sharing your personal knowledge base.
  - A privacy-first, open-source platform for knowledge management and collaboration
- https://github.com/athensresearch/athens /EPL/202212/Clojure/ts/inactive
  - https://athensresearch.github.io/athens
  - open-source, collaborative knowledge graph
  - athens-export converts your pages to markdown and a logseq-compatible directory.
  - Built on a graph database, Athens helps map and communicate complex knowledge in complex domains.
  - athens-export converts your pages to markdown and a logseq-compatible directory

- growi /1.2kStar/MIT/202311/ts/remark/偏向文档管理
  - https://github.com/weseek/growi
  - https://docs.growi.org/en/guide/
  - https://demo.growi.org/
  - Team collaboration software using markdown
  - 依赖 express、mongoose、es、redis、swr
  - Simultaneously edit with multiple people by HackMD(CodiMD) integration
  - Create hierarchical pages with markdown
  - Slack/Mattermost, IFTTT Integration
  - 各种集成

- https://github.com/hedgedoc/hedgedoc /AGPLv3/202402/ts
  - https://demo.hedgedoc.org/features?both
  - https://docs.hedgedoc.org/setup/getting-started/
  - 后端依赖nestjs.v8、rxjs.v7、sqlite3、typeorm、passport
  - HedgeDoc is a real-time, multi-platform collaborative markdown note editor.
  - HedgeDoc (formerly known as CodiMD) is an open-source, web-based, self-hosted, collaborative markdown editor.
  - We are currently working on HedgeDoc 2, a complete rewrite of HedgeDoc.
  - [Proposal: Replace OT with CRDTs](https://github.com/hedgedoc/hedgedoc/issues/527)
    - By using y.js we are using CRDTs now.
  - [fork history](https://hedgedoc.org/history/): HedgeDoc is the community-driven fork of CodiMD
- https://github.com/hedgedoc/react-client
  - https://ui-test.hedgedoc.org/intro
  - 前端依赖 react、redux-toolkit、codemirror.v6、bootstrap.v4、flowchart.js、markdown-it.v12、katex、vega、i18next、next.v12、react-bootstrap、yjs
  - 支持markdown的分屏预览，一边源码、一边预览，同步滚动

- affine /7.1kStar/MIT/202208/ts
  - https://github.com/toeverything/AFFiNE
  - https://affine.pro/
  - Affine is a next-gen knowledge base that brings planning, sorting and creating all together. Privacy first, open-source, customizable and ready to use.
  - 🤖 https://github.com/toeverything/AFFiNE/tree/canary/packages/frontend/apps/android
    - android和ios都基于capacitor实现
  - blocksuite /50Star/MPLv2/202210/ts
    - https://github.com/toeverything/blocksuite
    - https://pathfinder.affine.pro/
    - 支持跨block选择部分文字，但不支持跨block加粗快捷键
    - 不支持拖拽block修改顺序，不支持拖入拖出list item
    - 模型层基于yjs、y-indexeddb，渲染层将每个block的数据渲染成一个contenteditable，输入层依赖beforeinput，编辑操作抽象成了command
    - 多编辑器实例的优点
      - 容易实现虚拟滚动
    - 多编辑器实例的缺点
      - 自定义选区的同步和更新变得复杂
      - 跨block的操作变得复杂
    - https://github.com/zzj3720/blocksvite
      - simple Block editor like BlockSuite, based on Vue and @blocksuite/store
    - https://github.com/JhinBoard/jhin
      - Next-Gen Collaborative Knowledge Base, A free replacement for Notion & Miro
  - 🚨 [Announcement: The Evolution of BlockSuite _202412](https://github.com/toeverything/blocksuite/issues/9045)
    - BlockSuite has been the core editor powering AFFiNE, designed initially as a universal editor framework. Over time, as both BlockSuite and AFFiNE evolved, BlockSuite gradually incorporated more and more of AFFiNE’s specific business logic.
    - To realign with our goals and streamline development, we have made the decision to merge BlockSuite's codebase into AFFiNE. 
    - we will extract and rebuild the core elements of BlockSuite into a new, independent project. This will allow us to return to the original mission of BlockSuite—creating a flexible, universal editor framework that can be used beyond AFFiNE.
    - We are currently working on integrating BlockSuite into AFFiNE while simultaneously outlining the roadmap for the new universal editor framework

- https://github.com/TriliumNext/Notes /AGPL/202503/ts
  - https://triliumnext.github.io/Docs/
  - open-source, cross-platform hierarchical note taking application with focus on building large personal knowledge bases.
  - Notes can be arranged into arbitrarily deep tree. Single note can be placed into multiple places in the tree
  - Rich WYSIWYG note editing including e.g. tables, images and math with markdown autoformat
  - Note attributes can be used for note organization, querying and advanced scripting
  - Synchronization with self-hosted sync server
  - REST API for automation
  - [Announcement: Trilium transitions into maintenance mode _202401](https://github.com/zadam/trilium/issues/4620)
    - In short, my time priorities changed and I now have other things on which I want to spend more of my time.
- trilium /23.3kStar/AGPLv3/202311/js/ckeditor5/支持多端
  - https://github.com/zadam/trilium
  - https://github.com/zadam/trilium/wiki/
  - 依赖electron、express、jsdom、turndown、ckeditor.v5、codemirror5、jsplumb、fancytree、bootstrap
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - Synchronization with self-hosted sync server
  - Trilium is provided as either desktop application (Linux and Windows) or web application hosted on your server (Linux). 
    - Mac OS desktop build is available, but it is unsupported.
    - If you want to install Trilium on server,currently only recent Chrome and Firefox are supported (tested) browsers.
  - [Notion like database](https://github.com/zadam/trilium/issues/822)
  - [Can trilium save each note as separate text/md files instead of being stored in a database?](https://github.com/zadam/trilium/issues/244)
    - The reason why Trilium uses database instead of file structure is that filesystem isn't flexible/powerful enough for features I want (mainly cloning/分身的效果-多处引用且同步更新).
  - 🤔 [Why database instead of flat files? - trilium Wiki FAQ](https://github.com/zadam/trilium/wiki/FAQ#why-database-instead-of-flat-files)
    - Using filesystem would mean fewer features with probably more problems.
    - clones are what you might call "hard directory link" in filesystem lingo, but this concept is not implemented in any filesystem
    - filesystems make a distinction between directory and file while there's intentionally no such difference in Trilium
    - Trilium makes links / relations between different notes which can be quickly retrieved / navigated (e.g. for note map).There's no such support in file systems 
    - Filesystems are generally not transactional. While this is not completely required for a note-taking application, having transactions make it way easier to keep notes and their metadata in predictable and consistent state.

- https://github.com/aliscie/odoc /202308/rust/ts/inactive
  - This app is Notion.so clone, roam research clone and obsidian clone. 
  - The main purpose of this app is not to just clone these note-taking apps but to make an all-in-one Open source note-taking app with automation features.
  - make sure to install zstd llvm, clang and openssl, gcc, rocksdb in order for the desktop app to work (surealdb requirements).

- https://github.com/slotDumpling/multibility /202310/ts/inactive
  - https://slotdumpling.github.io/multibility/
  - Collaborative notes and PDF annotations
  - 协同笔记与PDF批注
  - 依赖draft-pad(基于paperjs-canvas)、antd.v4、antd-mobile.v5、immutable.v4、pdfjs、react-beautiful-dnd、socket.io

- https://github.com/appotry/dootask /php/vue
  - https://www.dootask.com/
  - 轻量级的开源在线项目任务管理工具，提供各类文档协作工具、在线思维导图、在线流程图、项目管理、任务分发、即时IM，文件管理等工具。

- https://github.com/mintterteam/mintter /168Star/apache2/202412/go/ts/archived
  - https://mintter.com/
  - a decentralized knowledge collaboration application for open communities powered by a knowledge graph.

- https://github.com/austinvhuang/openmemex /rust/haskell
  - local-first knowledge integration platform optimized for automation (including caching and indexing of content) as well as enabling neural network machine learning integrations.
  - SQLite is the central data storage medium, rather than a collection of markdown documents.
  - Instead of users manually curating a knowledge graph, data is organized automatically by timestamp.

- https://github.com/out-of-cheese-error/gooseberry /MIT/202208/rust
  - A command line utility to generate a knowledge base from Hypothesis annotations
  - made with asciinema, svg-term-cli, and svgembed
  - Gooseberry provides a command-line interface for Hypothesis (a tool to annotate the web) and lets you generate a knowledge-base wiki without you having to actually type your knowledge out.
  - Gooseberry combines the ease of annotation offered by Hypothesis, bulk tagging and organization support in the command line, and a customizable plaintext wiki with HandleBars templating.

- https://github.com/skiff-org/skiff-apps /925Star/NCSA/202312/ts
  - https://skiff.com/
  - a privacy-first, end-to-end encrypted workspace with Mail, Calendar, Pages, and Drive product
  - This monorepo contains all Skiff apps, libraries, and more
  - 编辑器依赖prosemirror
  - 依赖yjs、graphql
  - [Not open-source](https://github.com/skiff-org/skiff-apps/issues/94)
    - This project is advertised as open-source despite that CC BY-NC-SA is clearly not an open-source license

- https://github.com/mayneyao/eidos /2.5kStar/AGPLv3/202503/ts
  - https://github.com/mayneyao/eidos-wiki
  - https://wiki.eidos.space/
  - Eidos 是一个开源的、本地优先的 Web App ，完全运行在浏览器中，无需安装，也不依赖于任何服务器
  - 拥有和 Notion 类似的文档和表格，你可以理解为离线版的 Notion，所有数据都在本地
  - 依赖sqlite-wasm、glide-data-grid、lexical
  - [Roadmap | Eidos Wiki](https://wiki.eidos.space/roadmap)
    - 在 EA 测试后，主体功能稳定的情况下，会开放源码并且公测。我不是那么喜欢 build in public，预期和实现不一致容易消磨耐心
  - [Show HN: Eidos – Offline alternative to Notion | Hacker News _202406](https://news.ycombinator.com/item?id=40746773)
    - built based on sqlite-wasm and runs entirely in the browser
    - A block-styled document editor and an Airtable-like table, built on top of SQLite, where each table is a real SQLite table.
    - A powerful extension system inspired by Figma plugin and Cloudflare worker. You can write scripts in TypeScript directly in the browser. It is easy to manipulate data in docs, tables, and the file system. It also supports API.
    - Eidos deeply integrated with LLM. You can translate, summarize, talk to your data
    - 🛢️ A key idea of Eidos is to make each table a real SQLite table, so users can view and modify it through other software or visualize it with tools like Metabase
    - You can make some adjustments in the settings to store data in a local folder. Then, use iCloud, Git, or your preferred service to back up your data. Just like the web version of VSCode, it can handle local files. The web is just an app and doesn't hold any data.
    - I carefully designed the architecture, which is very flexible. The "backend" is currently running on web worker & service worker. It should be possible to deploy it to a web-standard runtime environment for self-hosting. P2P synchronization based on CRDT is on the roadmap.

- https://github.com/bradwmorris/ra-h_os /MIT/202602/ts
  - TL; DR: Clone this repository and you'll have a local SQLite database on your computer. The database schema is structured so external AI agents can continuously read and write to it, building your knowledge graph externally.
  - Currently macOS only. Linux and Windows support is coming
  - Exposes an MCP server — Claude Code, Cursor, or any MCP client can query and add to your knowledge base
  - [I built and open sourced a local Obsidian alternative (sqlite) : r/PKMS](https://www.reddit.com/r/PKMS/comments/1r7tgl4/i_built_and_open_sourced_a_local_obsidian/)

- https://github.com/superdoc-dev/superdoc /AGPL/202604/ts
  - https://superdoc.dev/
  - Renders, edits, and automates .docx files in the browser, headless on the server, and within AI agent workflows.
  - Works with React, Vue, and vanilla JS.
  - Built on ProseMirror, Yjs, JSZip, and Vite.
  - Real DOCX, not rich text — Built on OOXML. Real pagination, section breaks, headers/footers. Not a contenteditable wrapper with export bolted on.
  - Runs entirely in the browser. 
  - collaboration — Yjs-based CRDT. Multiplayer editing with comments, tracked changes
  - Agentic tooling — Runs headless in Node.js. Bring your own LLM for document automation, redlining, and template workflows.
  - Dual licensed — AGPLv3 for community use. Commercial license for proprietary deployments.
# confluence-like
- MrDoc /2.1kStar/GPLv3/202403/js/python/Django/仅网页版
  - https://github.com/zmister2016/MrDoc
  - https://mrdoc.pro/
  - http://mrdoc.zmister.com/project-20/
  - 个人和小型团队的云笔记、云文档、知识管理私有化部署方案
    - 场景：个人云笔记、在线产品手册、团队内部知识库、在线电子教程等私有化部署场景
  - 后端依赖: Python、Django; 后端代码量很少
  - 前端依赖: LayUI、JQuery、vditor、luckysheet.v2
  - 功能特性: 文档资源管理、书写编辑、阅读分享、站点管理
  - 依赖luckysheet、vditor、editor.md、docdiff-codemirror5

- https://github.com/gitwonk/gitwonk /AGPLv3/202308/ts/inactive
  - The open source GitBook, Confluence, and Archbee alternative. 
  - alternative to GitBook, designed and built focusing on the developer experience.
  - 依赖supabase、@mdx-js/react、nextjs、sharp

- notabase /434Star/AGPLv3/202312/ts/仅网页版/supabase
  - https://github.com/churichard/notabase
  - https://notabase.io/
  - A personal knowledge base for networked thinking.
  - 仅支持网页版，可导出
  - inspired by note-taking apps such as Notion, Obsidian, Typora, and Roam Research.
  - Notabase uses Supabase as the backend (for authentication, database, and storage), so you'll have to make a Supabase account. 
    - https://github.com/churichard/notabase/blob/main/scripts/schema.sql

- rockeseat-ignite-rotion /1Star/ISC/202212/ts
  - https://github.com/wfl-junior/rockeseat-ignite-rotion
  - An alternative to Notion built with Electron
  - 依赖tiptap、electron、radix-ui、tanstack-query

- minddrop /3Star/NALic/202208/ts/提交多/仅桌面版
  - https://github.com/coniel/minddrop
  - https://minddrop.app/
  - 编辑器使用 slate.v0.76，zustand
  - 依赖 radix-ui
  - 页面基于卡片构成，一行3个卡片，卡片不支持调整大小
  - 编辑器仅支持简单文本
  - Where applicable, components are uncontrolled by default but can also be controlled, without needing to create any local states.

- memos /26.4kStar/MIT/202403/ts/go
  - https://github.com/usememos/memos
  - https://usememos.com/
  - 后端依赖 go, 未使用orm而直接用raw-sql
  - 前端依赖 redux-toolkit, dayjs, axios
  - 编辑器使用的是简单 textarea
  - ui高度复刻flomo，中文开发者作品，代码量不大
  - self-hosted knowledge base that works with a SQLite db file.
  - Write in the plain textarea without any burden
  - It has no external dependency.
  - [use orm like https://entgo.io/ instead of writing sqls manually _202401](https://github.com/usememos/memos/issues/2849)
    - currently, memos support sqlite, mysql, postgresql, but writing target sql separately, we could use orm, like entgo.io to simplify the db logic and get rid of manually written sql.
    - Although it's a bit more complicated to write SQL for each driver, but the execution/migration will be open and transparent. IMO, I think writing raw SQL is better then using ORM.
- https://github.com/Rabithua/Rote /MIT/202512/ts/类似twitter
  - https://rote.ink/
  - https://demo.rote.ink/
  - A note repository like Personal Note/blog
  - 默认不渲染markdown
  - Separated Architecture: Frontend and backend use separated architecture design, deploy only the services you need
  - Complete control over your data, free to export data
  - OAuth support, currently supports GitHub and Apple Login, Google is planned
  - S3 storage support, defaults to Cloudflare R2 storage, configuration can be skipped
  - [I have decided to open-source my note-taking project that I have used for two years. : r/opensource](https://www.reddit.com/r/opensource/comments/1pvhvaq/i_have_decided_to_opensource_my_notetaking/)
    - the inspiration came from the open-source project usememos. Earlier, I was a loyal user of usememos and even created an open-source mini-program client for usememos (memos_wmp)
    - However, I gradually felt that the project became bloated and complex, diverging more from my note-taking needs.
    - I started developing Rote from scratch. The web version's interface and interaction design drew more inspiration from designs I liked on Twitter and the Tailwindcss website
    - Although there's an explore page and Reactions, I don't define it as a community. The explore page simply displays some users' public notes

- pervane /200Star/MIT/202205/js/python
  - https://github.com/hakanu/pervane
  - https://hakanu.github.io/pervane/
  - Plain text file based note taking and knowledge base building tool, markdown editor, simple browser IDE.
  - It doubles as simple file server to render given directories files in web browser while it can be used as a cloud IDE too with awesome code highlighting. 
  - It's like python's built-in SimpleHTTPServer but a little bit feature richer like WYSIWYG note taking experience

- https://github.com/jaredly/local-first /191Star/202104/js/inactive
  - This aims to eventually be a fully-featured solution for managing, syncing, and storing application data, in a way that works offline, and collaboratively.

- Metagraph /19Star/NALic/202205/ts/vue
  - https://github.com/Wizard-wen/Metagraph
  - https://metagraph.design/
  - Metagraph是一款知识创作分享工具，Metagraph提供了强大的内容关联能力。

- https://github.com/c2d7fa/thinktool /75Star/AGPLv3/202208/ts
  - https://thinktool.io/
  - https://thinktool.io/demo
  - Novel fusion of hierarchical and graph-based approaches to taking notes, based on ideas from Roam Research, TheBrain and others.
- https://github.com/c2d7fa/nextool /AGPLv3/202206/ts
  - https://nextool.app/
  - GTD-oriented task manager with support for nested tasks and a focus on finding actionable tasks.

- https://github.com/ganskef/mdwiki /202310/js
  - CMS/Wiki using Markdown - 100% client side single-page application 
  - No special software installation or server side processing is required. Just upload the mdwiki.html into the same directory as your Markdown files and you are good to go!
  - This is a fork of the stable Dynalon MDwiki release branch v0.6.x containing updated dependencies with all the beloved features (like Markdown include which is missed in the master branch). The original repository is unmaintained and archived (read-only).
  - 🍴 forks
  - https://github.com/Dynalon/mdwiki /GPLv3/201810/ts/js
  - https://github.com/unmacaque/mdwiki
    - marked was updated to support more GFM syntax
  - https://github.com/stephanedenis/mdwiki

- https://github.com/documize/community /2.3kStar/AGPL/202509/go/emberjs/inactive
  - https://docs.documize.com/
  - 依赖 go、js、handlebars、EmberJS
  - Modern Confluence alternative designed for internal & external docs, built with Golang + EmberJS
  - [Understanding Document Basics](https://docs.documize.com/s/WOzFU_MXigAB6sIH/user-guides/d/WOvEC_MXigAB6sE1/understanding-document-basics)
    - How Documize works: sections, revisions, attachments
    - A document in Documize consists of sections. 
    - Content Sections allow for content to be typed in just like Microsoft Word, Google Docs or wiki software.
      - Rich Text, Markdown, Code Tabular
    - Data Sections allow live-linking and sync'ing of data from popular cloud-based systems
      - Airtable, GitHub, Trello, etc.
    - toc, linking, tagging, attachments, revisions & rollback, doc-lifecycle

- https://github.com/airbnb/knowledge-repo  /data-sci
  - https://knowledge-repo.readthedocs.io/en/latest/
  - A next-generation curated knowledge sharing platform for data scientists and other technical professions.
  - Knowledge Repo project is focused on facilitating the sharing of knowledge between data scientists and other technical roles using data formats and tools 

- https://github.com/andymatuschak/orbit /1.5kStar/apache2/202305/ts/inactive
  - https://withorbit.com/
  - Orbit is an experimental platform for publishing and engaging with small tasks repeatedly over time.
  - [Project: data architecture improvements_202104](https://github.com/andymatuschak/orbit/issues/192)
    - The log-driven state model in the current system is more typically called an “event sourcing” model. The idea is basically: you don't transmit the state of the system; you transmit actions, then compute an effective state locally. State is always just a cache, computed over the action stream.
    - our current model includes several decisions which dramatically increase the complexity
    - We could create a much simpler event sourcing model
    - The salted HLC does seem to be fine for the purposes of our stable listing contracts.
  - https://twitter.com/andy_matuschak/status/1428777459235782660
    - That’s the approach Orbit takes: simple event structures (simpler than CRDTs, sacrificing some of their key guarantees to reduce complexity), with well-defined merge operations, in a SQLite db. Users can write scripts to insert their own events if they like.
    - Orbit’s implementations are quite general (i.e. they have almost no specific knowledge of Orbit’s structures), so perhaps they’ll be of use to others. See store-*, sync, and backend packages here

- Ink-wash-docs /472Star/Apache2/202309/js/inactive
  - https://github.com/huangwei9527/Ink-wash-docs
  - 水墨文档，一款基于egg+vue开发的在线文档管理平台，支持markdown文档， excel文档，原型托管等功能.
  - 依赖vue、element-ui、vditor、egg、x-spreadsheet
  - 依赖vditor、x-data-spreadsheet、vue2、vuex3、element-ui2、egg2

- https://github.com/RealRong/Rendevoz
  - open-source knowledge management application built with React and TypeScript
  - 依赖slate、yjs、rxjs
  - WYSIWYG Block Editor built upon Slate.js, with drag & drop, custom block rendering, etc.
  - Cross platform powered by Electron.

- https://github.com/courajs/referent /202201/js/inactive
  - An offline-first, realtime-collaborative wiki engine

- cryptpad /4.3kStar/AGPLv3/202301/js
  - https://github.com/cryptpad/cryptpad
  - https://github.com/xwiki-labs/cryptpad
  - https://cryptpad.org/
  - CryptPad is a collaboration suite that is end-to-end-encrypted and open-source.
  - 依赖 onlyoffice、netflux-websocket
  - It is built to enable collaboration, synchronizing changes to documents in real time. 

- https://github.com/hyperlink-academy/leaflet /MIT/202505/ts/卡片式风格
  - https://leaflet.pub/
  - Leaflet is a tool for shared writing and social publishing.
  - Next.js for UI and app framework
  - Supabase for db / storage layer
  - Replicache for realtime data sync layer
  - TailwindCSS for styling magic
  - [Show HN: Leaflet.pub – a web app for creating and sharing rich documents | Hacker News _202503](https://news.ycombinator.com/item?id=43269928)
    - We do sync and all our client-side state via Replicache - Data is modeled as a set of facts about entities, a la Datomic, forming a graph. 
    - every text block is a separate ProseMirror instance. This lets us keep the document structure in our database and our schema, without having to dive into ProseMirror's every time we want to modify things.
# TiddlyWiki/in-memory/cms
- TiddlyWiki5 /7.5kStar/BSD/202311/js
  - https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/
  - https://tiddlywiki.com/dev/ Developer documentation
  - A self-contained JavaScript wiki for the browser, Node.js, AWS Lambda etc.
  - a non-linear personal web notebook that anyone can use and keep forever
  - It can be used as a single HTML file in the browser or as a powerful Node.js application. 
  - Except of a micro-kernel written in JavaScript the whole application consist of a own data-structure called tiddlers and a own markup language called wikiText.
  - view层基于tid文件

- https://github.com/Alamantus/FeatherWiki /91Star/AGPLv3/202310/js
  - https://codeberg.org/Alamantus/FeatherWiki
  - extensible tool for creating personal non-linear notebooks, databases, and wikis that is entirely self-contained, runs in your browser, and is only 55 kilobytes. 
  - The idea is that it's like TiddlyWiki but as small as possible.
  - 👉🏻 The app and all of the content you create using it are stored within the single HTML file generated when you save your wiki. 
  - Publishing your content is as simple as uploading that file to a web server, and **updating is as simple as overwriting the file** .
  - Tiddlyhost is a free hosting platform that offers the ability to save your Feather Wiki directly instead of needing to download a copy!
  - [Feather Wiki: app for creating personal non-linear notebooks, databases, wikis | Hacker News_202205](https://news.ycombinator.com/item?id=31474062)

- mdSilo-web /208Star/AGPLv3/202309/ts/web+桌面
  - https://github.com/danloh/mdSilo-web
  - https://mdsilo.com/
  - A local-first mind silo for storing ideas, thought, knowledge with a powerful writing tool, running fully in the browser.
  - 核心编辑器mdsmirror未开源，基于rich-markdown-editor
  - 依赖 react、tauri/rust、localforage、dnd-kit、headlessui-react、popperjs、react-spring、tailwindcss、d3-drag/selection、fuse.js、immer、codemirror.v6、styled-comp、react-virtualized、zustand
  - If your browser doesn't support local file system APIs, you'll still be able to open individual local files or import JSON file 
  - Since mdSilo Web app is running completely within the browser, some experiences will naturally be more constrained

- https://github.com/benweet/stackedit /21kStar/apache2/js/vue
  - https://stackedit.io/
  - Full-featured, open-source Markdown editor based on PageDown, the Markdown library used by Stack Overflow and the other Stack Exchange sites.
  - Scroll Sync feature accurately binds the scrollbars of the editor panel and the preview panel 
  - StackEdit can sync your files with Google Drive, Dropbox and GitHub
  - 🛋️ We have CouchDB workspace provider since v5.7.
  - [Self hosted StackEdit that operates on local files?](https://github.com/benweet/stackedit/issues/192)
    - The new Native File System proposal looks to be a good fit for this request.
- https://github.com/josephernest/writing /202208/js
  - a lightweight distraction-free text editor, in the browser (Markdown and LaTeX supported).
  - no server needed, you can run it offline

- https://github.com/Arlen22/TiddlyServer /202111/ts
  - A static file server that can also save files and mount TiddlyWiki folders
# knowledge-base/wiki
- https://github.com/xwiki-contrib/cristal /LGPL/202507/ts/vue
  - https://cristal.xwiki.org/
  - Cristal is a new project to build a new modular wiki UI using modern web technologies, which will support multiple backends (including of course XWiki to store Wiki data).
  - A wiki UI to rule them all: Provide a UI that can be plugged onto various content backends (XWiki, local file system, GitHub, etc.)
  - Ability to work offline, reconnect, and sync content.
  - Usable in various forms:
    - From a URL in your browser
    - Executable locally on your computer (Electron application).
    - Embeddable in backends. For example, the intent on the long run is to have Cristal be used by XWiki as its native UI

- https://github.com/xwiki/xwiki-platform /1.1kStar/LGPL/202507/java
  - http://platform.xwiki.org/
  - https://www.xwiki.org/xwiki/bin/view/Main/
  - XWiki Platform is a generic wiki platform offering runtime services for applications built on top of it.
  - XWiki Commons, XWiki Rendering, and XWiki Platform are part of the XWiki.org software forge. They are released together and share the same version.
  - Over 600 extensions: applications, macros, skins, plugins, themes, etc.
  - Learn about XWiki's concept and why it's an alternative to Confluence and MediaWiki

- monotome /151Star/AGPLv3/202208/js
  - https://github.com/cblgh/monotome
  - a personal knowledge base system. markdown markup, runs in the browser
  - 依赖 marked
  - 原理是 根据url动态读取解析markdown文件，并渲染显示所有文件名
  - 代码量不大，思路清晰
  - Monotome has support for the common `[[wiki]]` syntax, 
  - Subjects are ordered into a simple directory structure which is mirrored by index.json.

- silverbullet /2.4kStar/MIT/202410/ts
  - https://github.com/silverbulletmd/silverbullet
  - https://silverbullet.md/
  - SilverBullet is an extensible, open source personal knowledge platform. 
  - implemented as an open-source offline-capable web application.
  - written in TypeScript and built on top of the excellent CodeMirror 6, preact
    - The server backend runs as a HTTP server on Deno using and is written using Oak.
  - At its core it’s a clean markdown-based writing/note taking application that stores your pages (notes) as plain markdown files in a folder referred to as a space. 
  - While SB uses a database for indexing and caching some indexes, all of that can be rebuilt from its markdown source at any time. 
  - extensible with plugs, and you can customize it
  - [Silver Bullet: Markdown-based extensible open source personal knowledge platform | Hacker News_202212](https://news.ycombinator.com/item?id=33843009)

- helpkb /8Star/MIT/202209/js
  - https://github.com/mrvautin/helpkb
  - https://docs.helpkb.org/
  - 后端依赖 express、sequelize、gray-matter
  - 前端依赖 nextjs、react-bootstrap、react-markdown、sharp处理图片
  - helpkb is an open-source Next.js knowledge base or FAQ which is super fast, easy to use and quick to develop.
  - You need a Database for your data. You can use either postgres (recommended), mysql2, mariadb, sqlite3 or mssql.

- openKB /636Star/MIT/202205/js/inactive/view层handlebars/nedb
  - https://github.com/mrvautin/openKB
  - https://openkb.markmoffat.com/
  - 体验和helpkb基本一致
  - 依赖nedb、express、jquery、lunr、markdown-it
  - openKB is a Markdown Knowledge base application (FAQ) built with Nodejs and ExpressJS. 
  - The application uses an embedded database (nedb) by default but can also use a MongoDB server by changing the config
  - openKB is a search based Knowledge base (FAQ) backed by Lunr.js indexing 
  - openKB uses the pure Javascript nedb embedded database by default or a MongoDB server.

- hamsterbase /158Star/MIT/202211/ts/仅开源sdk
  - https://github.com/hamsterbase/hamsterbase
  - https://hamsterbase.com/zh/
  - 一个本地优先的网页存档应用。 a self-hosted, local-first web archive application.
  - 本地部署 + 完全离线 + 点对点同步（马上发布了）
  - 储存、管理和预览 HTML, MHTML and Webarchive 格式的文档。
  - 对保存的页面进行高亮、批注。
  - 开源 SDK，目前免费。
  - Full Text Search
  - Open source SDK
  - 推荐使用 SingleFile 保存 html 页面

- https://github.com/Requarks/wiki /22.5kStar/AGPLv3/202310/js/vue
  - https://js.wiki/
  - A modern and powerful wiki app built on Node.js
  - [Wiki.js | Hacker News_202007](https://news.ycombinator.com/item?id=23904193)

- https://github.com/ryanlelek/Raneto /MIT/202311/js
  - https://docs.raneto.com/
  - Markdown powered Knowledgebase Wiki for Node.js
  - 比较典型的问答型知识库
  - a "flat file" CMS, meaning no database problems, no MySQL queries, nothing.
  - Full-text search powered by Lunr
  - [Raneto – Markdown Knowledgebase Platform | Hacker News_201707](https://news.ycombinator.com/item?id=14839371)

- https://github.com/wikimedia/mediawiki /4.8kStar/GPLv2/202511/php
  - https://www.mediawiki.org/
  - open-source wiki software package written in PHP. 
  - It serves as the platform for Wikipedia and the other Wikimedia projects
  - feature-rich and extensible, both on-wiki and with hundreds of extensions; 
  - https://github.com/wbstack/mediawiki /php
    - This ultimately repackages MediaWiki together with its extensions, skins, then creates a new "application" with a much tighter(紧密的) external interface (particularly around configuration).
  - https://github.com/wikimedia/VisualEditor /185Star/MIT/202311/js
    - https://www.mediawiki.org/wiki/VisualEditor
    - https://doc.wikimedia.org/VisualEditor/master/js/lib/ve/demos/ve/desktop-wikimediaui.html
    - Standalone rich HTML5 editor, based on ContentEditable.
    - 依赖自研oojs、oojs-ui、jquery
    - was created by the Editing team for MediaWiki's HTML+RDFa document format (generated by Parsoid) and is available as a MediaWiki extension. 
    - As of 2020, VisualEditor is enabled by default here on mediawiki.org and on most Wikipedia and Wikivoyage language editions.

- https://github.com/wmde/WikibaseDataModel /php
  - http://wikiba.se/
  - PHP implementation of the Wikibase Data Model
  - It is primarily used by the Wikibase MediaWiki extensions, though has no dependencies whatsoever on these or on MediaWiki itself.

- https://github.com/dokuwiki/dokuwiki /4.5kStar/GPLv2/202511/php
  - http://www.dokuwiki.org/
  - a simple to use and highly versatile Open Source wiki software that doesn't require a database
  - Built in access controls and authentication connectors make DokuWiki especially useful in the enterprise context 

- https://github.com/BookStackApp/BookStack /17.7kStar/MIT/202511/php
  - https://www.bookstackapp.com/
  - A platform to create documentation/wiki content built with PHP & Laravel

- https://github.com/OpenKnowledgeMaps/Headstart /js/python
  - a web-based knowledge mapping software intended to give researchers a head start on their literature review
  - It comes with a powerful backend that is is capable of automatically producing knowledge maps from a variety of data, including text, metadata and references.
  - Interactive, web-based knowledge maps based on D3.js, following Shneiderman's principle of "overview first, zoom and filter, then details-on-demand"
  - Integrated PDF viewer and annotation tool, courtesy of Hypothes.is
  - Persistence and versioning system based on SQLite
  - Powerful server component written in PHP and R for the creation of knowledge maps, including algorithms for clustering, ordination and labelling

- https://github.com/elastic/app-search-kb-demo /202005/js/inactive
  - A beautiful, modern customer support/knowledge base search experience for App Search using Search UI.
  - If you wish to test the full stack build locally, you have to boot all the required services (Elasticsearch, App Search)
# vscode-powered
- foam /15.6kStar/MIT/202411/ts/inactive
  - https://github.com/foambubble/foam
  - https://foambubble.github.io/
  - personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - Foam supports link aliasing, so you can have a `[[wikilink]]`, or a `[[wikilink|alias]]`.
  - See how your notes are connected via a graph with the Foam: Show Graph command
  - Foam updates the links to renamed files, so your notes stay consistent.
  - [Add support for VSCodium](https://github.com/foambubble/foam/issues/26)
    - Foam is officially published to OpenVSX as of 0.7.5_202012

- memo /843Star/MIT/202303/ts/vscode/inactive
  - https://github.com/svsool/memo
  - Markdown knowledge base with bidirectional [[link]]s built on top of VSCode
  - Inspired by Obsidian.md and RoamResearch.

- dendron /6.8kStar/AGPLv3 > apache2/202404/ts/vscode/inactive
  - https://github.com/dendronhq/dendron
  - https://wiki.dendron.so/
  - local-first, markdown-based, note-taking tool built on top of VSCode. 
  - Dendron builds on top of the past five decades of programming languages and developer tooling. We apply the key lessons from software to the management of general knowledge. We make managing general knowledge like managing code and your PKM like an IDE.
  - Dendron finds the usable center between the two extremes by supporting backlinks of any two arbitrary notes while also maintaining a canonical hierarchy for every note. 
  - We do this through our hierarchal first approach to note taking that relies on the combination of hierarchies, schemas, and path based lookups.
  - [A Hierarchy First Approach to Note Taking](https://www.kevinslin.com/notes/3dd58f62-fee5-4f93-b9f1-b0f0f59a9b64.html)
    - My primary use for notes is as a cache. Think Redis, but for humans.
    - If I spent more than 5 minutes figuring something out, those are five minutes I never want to spend again figuring out the same problem.
    - But this is difficult to do in practice.
    - My solution is something I call hierarchical note taking.

- https://github.com/TevinLi/amWiki /885Star/MIT/201711/js/NoDeps
  - http://amwiki.org/doc
  - 由 JS 开发、依赖 Atom 或 Nodejs-Npm 的 Markdown 轻量级前端化开源文库系统。
  - 不用数据库，文档使用 .md 格式保存本地文件
  - 无需服务端开发，只需支持http静态访问网页空间
  - 自动更新文库导航目录，支持多级目录
  - 无需服务端的全文库内容搜索与计分排序
# kb-search
- https://github.com/coderabbit214/document-ai
  - go基于向量数据库与GPT3.5的通用本地知识库方案
- https://github.com/GanymedeNil/document.ai
  - 基于向量数据库与GPT3.5的通用本地知识库方案
# wikipedia
- https://github.com/segfall/static-wiki /js
  - http://static.wiki/
  - read-only wikipedia using just static files.
  - 2MB of CSS, JS, WASM; one 43GB SQLite file.
  - A proof-of-concept inspired and enabled by Hosting SQLite Databases on Github Pages and the ensuing Hacker News post. 
  - [Show HN: Static.wiki – read-only Wikipedia using a 43GB SQLite file | Hacker News_202107](https://news.ycombinator.com/item?id=28012829)

- https://github.com/maxlath/wikibase-sdk /202310/ts
  - JS utils functions to query a Wikibase instance and simplify its results

- https://github.com/Nutomic/ibis /AGPLv3/202404/rust
  - ibis is a federated alternative to Wikipedia. 
  - It uses the Activitypub protocol for communication between different servers (instances), similar to Mastodon or Lemmy. 
  - Users can sign up on any instance to read and edit articles, including articles from other instances.
  - First install PostgreSQL 
  - Main objects in terms of federation are the Instance and Article. Each article belongs to a single origin instance
  - Articles have a collection of Edits a custom ActivityPub type containing a diff.
  - ⌛️ The text of any article can be built by starting from empty string and applying all associated edits in order.
  - 🔀 Edits are done with diffs which are generated on the backend, and allow for conflict resolution similar to git. 
  - Editing also works over federation. In this case an activity Update/Edit is sent to the origin instance.

## viewer

- [Modern for Wikipedia](https://www.modernwiki.app/)
  - redesigned user interface for Wikipedia
  - Themes (light, dark, sepia, slate, black)
  - view history (quickly jump to articles you've previously viewed)
  - [chrome-ext](https://chrome.google.com/webstore/detail/modern-for-wikipedia/emdkdnnopdnajipoapepbeeiemahbjcn)
# resource/library-management
- https://github.com/papermerge/papermerge-core /400Star/apache2/202512/python
  - https://papermerge.com/
  - https://demo.papermerge.com
  - open source document management system designed to work with scanned documents (also called digital archives). 
  - It extracts text from your scans using OCR, indexes them, and prepares them for full text search. 
  - It supports PDF, TIFF, JPEG and PNG document file formats
  - ⏳ Document Versioning: Originally uploaded version is always retained. 
  - Custom Fields (metadata) per document type
  - Multi-User & Group ownership
  - Page Management - delete, reorder, cut, move, extract pages
  - OCRed text overlay (you can download document with OCRed text overlay)
  - Full Text Search of the scanned documents
  - Dual panel mode
  - https://github.com/ciur/papermerge /2.8kStar/apache2/202110/legacy

- https://github.com/Mozzo1000/booklogr /435Star/apache2/202511/python/js
  - https://booklogr.app/
  - https://demo.booklogr.app/
  - a web app designed to help you manage your personal book library with ease.
  - Easily look up books by title or isbn. Powered by OpenLibrary
  - Export your data in multiple formats, including CSV, JSON, and HTML.
  - Supports SQLite (default) or PostgreSQL as databases.
  - 功能简单, 专注于阅读

- https://github.com/paperless-ngx/paperless-ngx /34.8kStar/GPLv3/202512/python/ts
  - https://docs.paperless-ngx.com/
  - https://demo.paperless-ngx.com/
  - Paperless-ngx is a document management system that transforms your physical documents into a searchable online archive so you can keep, well, less paper.
  - Paperless-ngx is compatible with many different scanners and scanning tools.
  - Once you've got Paperless setup, you need to start feeding documents into it
    - OCR the Document
    - create an archivable PDF/A document from your document. 
    - performs automatic matching of tags, correspondents and types on the document before storing it in the database.
    - The primary method of getting documents into your database is by putting them in the consumption directory.
  - 🌹
    - 支持删除到trash并恢复, trash中的文件默认会在30天后删除
    - 查看纯文本pdf时，支持选择文字
    - 上传文件后的文件processing是异步的
  - Paperless-ngx is the official successor to the original Paperless & Paperless-ng projects 
  - Utilizes the open-source `Tesseract` engine to recognize more than 100 languages.
  - Documents are saved as PDF/A format which is designed for long term storage, alongside the unaltered originals.
  - Paperless stores your documents plain on disk. Filenames and folders are managed by paperless and their format can be configured freely 
  - [Paperless-ngx – Open source document management system | Hacker News _202310](https://news.ycombinator.com/item?id=37800951)
  - https://github.com/icereed/paperless-gpt /1.4kStar/MIT/202509/go/ts
    - Use LLMs and LLM Vision (OCR) to handle paperless-ngx - Document Digitalization powered by AI
    - paperless-gpt seamlessly pairs with paperless-ngx to generate AI-powered document titles and tags, saving you hours of manual sorting. 
    - Harness Large Language Models (OpenAI or Ollama) for better-than-traditional OCR
    - includes powerful OCR enhancements that go beyond basic text extraction
  - https://github.com/signorecello/paperless-docling /202504/js/inactive
    - A service that automatically processes documents in Paperless using docling and updates their content.
    - [Better OCR with Docling : r/Paperlessngx _202504](https://www.reddit.com/r/Paperlessngx/comments/1jqqsly/better_ocr_with_docling/)
    - [Has anybody tried Readur as a Paperless-ngx alternative? : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/1lw0164/has_anybody_tried_readur_as_a_paperlessngx/)
      - I am personally not a fan of Paperless’s tag-based approach. I have a folder-based approach that has worked well for me for years. I would love it if paperless (or an alternative) would simply interact with an existing folder structure, rather than consuming everything.
    - pr已合并 [Feature: Nested Tags _202509](https://github.com/paperless-ngx/paperless-ngx/pull/10833)
      - uses django-treenode's TreeNodeModel for tags to give them parent/child relationships and applies to documents such that adding a child always adds its parents and removing a parent removes all children. Similarly, if a tag gets assigned a new parent, that parent is added to existing docs.
- https://github.com/clusterzx/paperless-ai /4.6kStar/MIT/202511/python/js
  - https://clusterzx.github.io/paperless-ai/
  - an AI-powered extension for Paperless-ngx that brings automatic document classification, smart tagging, and semantic search using OpenAI-compatible APIs and Ollama.
  - [Paperless-AI: Now including a RAG Chat for all of your documents : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kqbouu/paperlessai_now_including_a_rag_chat_for_all_of/)
  - https://github.com/admonstrator/paperless-ai-next /MIT
    - fork of Paperless-AI for Paperless-ngx, improving AI/OCR reliability with an OCR rescue queue (Mistral), a permanent-failure queue, and ignore filters.
    - Adds history + one-click rescan, MFA, better setup, restore-original-metadata, and Date/Boolean custom fields support

- https://github.com/papra-hq/papra /2.4kStar/AGPL/202509/ts
  - https://demo.papra.app/
  - a minimalistic document management and archiving platform.
  - Papra is a platform for long-term document storage and management, like a digital archive for your documents.
  - no backend, client-side local storage only
  - Search: Quickly search for documents with full-text search.
  - Authentication: User accounts and authentication.
  - SolidJS, shadcn-solid, honojs, drizzle

- https://github.com/stumpapp/stump /1.8kStar/MIT/202510/rust/ts
  - https://stumpapp.dev/
  - open source comics, manga and digital book server with OPDS support (WIP)

- https://github.com/jiisanda/docflow /MIT/202509/python/inactive
  - a powerful Document Management API designed to streamline document handling, including seamless uploading, downloading, organization, versioning, sharing, and more

- https://github.com/Open-Source-Legal/OpenContracts /1.1kStar/AGPL/202512/python/ts
  - https://open-source-legal.github.io/OpenContracts/
  - Open source document platform for document analysis, annotation, and collaboration.
  - Document Processing — Upload PDFs and text files, automatically extract structure with ML-based parsers
  - Annotation & Analysis — Highlight, label, and analyze documents with custom annotation schemas
  - AI Agents — Chat with documents using configurable AI assistants that can search and analyze content
  - Collaboration — Threaded discussions with @mentions, voting, and moderation at corpus and document levels
  - Data Extraction — Extract structured data from hundreds of documents using agent-powered queries
  - Version Control — Track document changes, restore previous versions, soft delete with recovery
# more
- https://github.com/notea-org/notea
  - Self hosted note taking app stored on S3
  - 依赖自己维护的@notea/rich-markdown-editor
  - Support storage in Amazon S3, MinIO, Aliyun OSS, etc

- https://github.com/zhyd1997/DragonLi /202209/ts
  - https://dragon-li.on.fleek.co/
  - a blog platform and alternative to Mirror
  - support favourite writers in seconds stream for readers by integrated with Superfluid instead of one-time payment.

- https://github.com/unigraph-dev/unigraph-dev /664Star/MIT/202306/ts
  - https://unigraph.dev/
  - A local-first and universal knowledge graph, personal search engine, and workspace for your life.
  - Your data is private and never leaves your computer. 
  - Query or sync all of your data in JSON format using a variant of GraphQL.
  - [Subscription support and sample todo app](https://github.com/unigraph-dev/unigraph-dev/pull/10)
    - Subscriptions are implemented with polling + querying after insertion/update/deletion.

- https://github.com/mraht-apps/notie /202201/js/inactive
  - Notion-like workspace with offline mode and encryption
  - Completely offline (online synchronisation by storing encrypted file in cloud folder possible)

- https://github.com/lidotcircle/webdisk
  - 文件管理、Markdown笔记、数据图表
  - 前端采用 Angular
  - 后端采用 Node.js + Express.js + typeorm + sqlite3

- mashcard /204Star/Apache2/202208/ts/ruby
  - https://github.com/mashcard/mashcard
  - https://www.producthunt.com/upcoming/brickdoc
  - 旧编辑器tiptap，新编辑器直接使用prosemirror
  - MashCard is an all-in-one workspace and low-code platform with Compound Document at its core. 
  - It's not only an open source alternative to Coda and Notion

- hash /636Star/MIT+Elastic+AGPL/202211/ts/rust
  - https://github.com/hashintel/hash
  - https://hash.dev/
  - Data management, integration and modeling with blocks
  - The Block Protocol is an open-source standard and registry for sharing interactive blocks connected to structured data.
  - You can build your own blocks, embed them in a website, or allow your users to embed blocks directly within your application.
  - HASH is our forthcoming open-source, all-in-one workspace platform built around structured data and interactive blocks.

- https://github.com/obsidian-tasks-group/obsidian-tasks
  - ask management for the Obsidian knowledge base.

- https://github.com/vikingcms/viking
  - The main repository for Viking CMS. Currently in Development.

- https://github.com/haxzie/snipp.in
  - Notes, Snippet manager and code editor directly inside your browser
  - Built with Vue.js, Dexie and Monaco Editor .
