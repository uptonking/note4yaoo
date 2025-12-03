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
  - Publishing your content is as simple as uploading that file to a web server, and **updating is as simple as overwriting the file**.
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
# kb-ai/chatgpt
- https://github.com/upstash/context7 /34kStar/MIT/202510/ts
  - https://context7.com/
  - Context7 MCP - Up-to-date Code Docs For Any Prompt
  - Context7 MCP pulls up-to-date, version-specific documentation and code examples straight from the source — and places them directly into your prompt.
  - require Context7 API Key (Optional) for higher rate limits and private repositories 
  - [Feature Request: Option to Self-Host Documentation Backend _202504](https://github.com/upstash/context7/issues/59)
    - interesting idea. I will think about this. the biggest obstacle would be licensing. we aim to make this service free for developers and open source projects. but we want to commercialize if a company like cursor needs it.
    - but we can keep parser private and web backend open.
    - maybe you can store all the docs in a public database, that way anyone can self-host.
    - Another option is to allow companies to host their documentation on context7's servers privately, and support authentication.

- https://github.com/mintlify/writer /MIT/202305/ts/inactive
  - https://www.mintlify.com/writer
  - AI powered documentation writer
  - We never store your code, but your code does leave your machine.
  - [Mintlify raises $18M Series A led by Andreessen Horowitz - Mintlify _202409](https://mintlify.com/blog/series-a)

- https://github.com/KnowledgeCanvas/knowledge /apache2/202401/ts/inactive
  - a tool for saving, searching, accessing, exploring and chatting with all of your favorite websites, documents and files.

- https://github.com/khoj-ai/khoj /31.6kStar/AGPLv3/202511/python/ts
  - https://khoj.dev/
  - Khoj is an application that creates always-available, personal AI agents for you to extend your capabilities
  - Your AI agents have access to the internet, allowing you to incorporate realtime information.
  - Khoj is accessible on Desktop, Emacs, Obsidian, Web and Whatsapp.
  - Khoj is open-source, self-hostable. Always.
  - 支持私有化部署、本地模型、与 Obsidian 无缝整合
  - 支持 github、pdf/markdown、notion 等内容源

- https://github.com/RapidAI/RapidLayoutRecover /apache2/202409/python
  - 针对文档类图像，整合版面分析、文字识别、表格识别和公式识别结果，还原版面布局信息。
  - 输入：文档类图像, 输出：TXT或Word
  - A[/文档图像/] --> B([文档方向分类 rapid_orientation]) --> C([版面分析 rapid_layout])

- https://github.com/Cinnamon/kotaemon /23kStar/apache2/202507/python
  - https://cinnamon.github.io/kotaemon/
  - https://huggingface.co/spaces/cin-model/kotaemon-demo
  - open-source clean & customizable RAG UI for chatting with your documents. Built with both end users and developers in mind.
  - This project serves as a functional RAG UI for both end users who want to do QA on their documents and developers who want to build their own RAG pipeline.
  - Minimalistic UI: A user-friendly interface for RAG-based QA.
  - Support for Various LLMs: Compatible with LLM API providers (OpenAI, AzureOpenAI, Cohere, etc.) and local LLMs (via `ollama` and `llama-cpp-python`).
  - Framework for RAG Pipelines: Tools to build your own RAG-based document QA pipeline.
  - Customizable UI: See your RAG pipeline in action with the provided UI, built with Gradio

- https://github.com/shaheryaryousaf/fastapi-docgpt
  - 一个PDF文档GPT项目：fastapi-docgpt，可以对PDF文档内容进行对话问答 
  - 上传PDF，系统自动提取PDF文本内容，并将文档内容转换为向量存储 
  - 可通过Swagger在 /docs 获取自动API文档

- https://github.com/pingcap/autoflow /apache2/202411/python
  - https://tidb.ai/
  - pingcap/autoflow is a Graph RAG based and conversational knowledge base tool built with TiDB Serverless Vector Storage.
  - An open source GraphRAG (Knowledge Graph) built on top of TiDB Vector and LlamaIndex and DSPy.
  - UI交互类似chatgpt
  - https://x.com/9hills/status/1862522244527972625
    - RAG Demo 到 RAG Application 难度的完美表现，其实功能不算丰富（增加了 Graph RAG和 Agent RAG 的思想），
    - 代码却不得不做的非常复杂，大部分其实是应用逻辑。 P. S. 代码已经成熟到可以直接抄了，直接复刻就完了

- https://github.com/casibase/casibase /4.2kStar/apache2/202511/go
  - https://casibase.org/
  - https://ai-admin.casibase.com/
  - https://ai.casibase.com/
  - Open-source enterprise-level AI knowledge base and MCP (model-context-protocol)/A2A (agent-to-agent) management platform with admin UI, user management and Single-Sign-On
  - Golang + Beego + Python + Flask + MySQL

## etl-doc

- https://github.com/NanoNets/docext /1.8kStar/apache2/202508/python/inactive
  - An on-premises, OCR-free unstructured data extraction, markdown conversion and benchmarking toolkit

- https://github.com/run-llama/llama_index /45.5kStar/MIT/202511/python
  - https://developers.llamaindex.ai/
  - LlamaIndex (GPT Index) is a data framework for your LLM application.
  - [[Bug]: PDF parsing does not happen with `SimpleDirectoryReader`](https://github.com/run-llama/llama_index/issues/19260)
    - I guess the default pdf reader (`pypdf`) couldn't parse your document? Feel free to swap it with anything else (like llama parse, docling, etc)
    - The unreadable PDF content happens because `SimpleDirectoryReader` relies on external libraries to extract text from PDFs, but these dependencies (`PyMuPDF/fitz` or `pdfminer.six`) are not installed by default. When they're missing, you get raw PDF markup instead of extracted text details.
  - [Add in-memory loading for non-default filesystems in PDFReader _202404](https://github.com/run-llama/llama_index/pull/12659)
    - Loading documents for large PDF files in external file systems was taking a long time. After investigation, we found that we were making a lot of requests to the external filesystem in the process. To avoid this, we first load the content in-memory and then pass it to pypdf.
    - Interesting, so this is because passing the file directly was making way too many requests, so now we fully download the file into memory and then pass it in? Is this only an issue for PDFReader?
      - We've only run into that issue with pypdf as of now.
      - it's way faster now. That's also what pypdf does if you pass it a path instead of a stream, but that only supports the default filesystem

- https://github.com/google/langextract /15.5kStar/apache2/202509/python
  - https://pypi.org/project/langextract/
  - a Python library that uses LLMs to extract structured information from unstructured text documents based on user-defined instructions.
  - Precise Source Grounding: Maps every extraction to its exact location in the source text, enabling visual highlighting for easy traceability and verification.
  - Reliable Structured Outputs: Enforces a consistent output schema based on your few-shot examples
  - Optimized for Long Documents by using an optimized strategy of text chunking, parallel processing, and multiple passes for higher recall.
  - Flexible LLM Support: Supports your preferred models, from cloud-based LLMs like the Google Gemini family to local open-source models via the built-in Ollama interface.
  - 🐛 [Proposal: Add Docling Integration for End-to-End Document Extraction  _202508](https://github.com/google/langextract/issues/184)
    - LangExtract today works only on raw text strings. In real-world workflows the source is usually a PDF , DOCX or PPTX. Users currently have to: Manually convert the file to text (losing layout & provenance).
    - Proposed Solution: Integrate Docling library as an optional front-end
  - 🐛 [Is it able to work on large PDF files? ](https://github.com/google/langextract/issues/178)
    - 👷 202508: PDF support is not available yet but it's something that I'm interested in. I have a small prototype running on my local and as the library has core aspects stabilized will work on adding this in.
  - [Question: Does Langextract work better on full documents or chunks? _202508](https://github.com/google/langextract/issues/206)
    - From my current tests it seems to work better when using docling to chunk it (at least in terms of building a knowledgegraph). I guess its due to contexual / visual chunking vs naive chunking.

- https://github.com/Unstructured-IO/unstructured /10.5kStar/apache2/202503/python
  - https://www.unstructured.io/
  - provides open-source components for ingesting and pre-processing images and text documents, such as PDFs, HTML, Word docs, and many more.

- https://github.com/PragmaticMachineLearning/docai /MIT/202409/python
  - Extract structured data from unstructured documents using Answer. AI's Byaldi, OpenAI gpt-4o, and Langchain's structured output.
  - 基于Answer. AI的Byaldi、OpenAI的gpt-4o和Langchain 做结构化数据输出
  - 支持从PDF等非结构化文档中提取结构化信息，比如损失历史记录、基本应用程序信息等

- https://github.com/yobix-ai/extractous /1.6kStar/apache2/202412/rust/inactive
  - Fast and efficient unstructured data extraction. 
  - Written in Rust with bindings for many languages.
  - Extractous offers a fast and efficient solution for extracting content and metadata from various documents types such as PDF, Word, HTML, and many other formats. 
  - Extractous is 25x faster than the popular unstructured-io library
  - 高性能非结构化数据提取工具：extractous，比unstructured-io快25倍，支持微软Office、PDF、网页、图片、电子书、邮件等多种格式
  - Extractous was born out of frustration with the need to rely on external services or APIs for content extraction from unstructured data. 
    - unstructured-io stood out as the popular and widely-used library for parsing unstructured content with in-process parsing. 
    - unstructured-io wraps around numerous heavyweight Python libraries, resulting in slow performance and high memory consumption
  - efficient solution for extracting content and metadata from various documents types such as PDF, Word, HTML, and many other formats.
  - solution in Rust with bindings for many programming languages.
  - Extractous maintains a dedicated focus on text and metadata extraction. It achieves significantly faster processing speeds and lower memory utilization through native code execution.
  - For file formats not natively supported by the Rust core, we compile the well-known Apache Tika into native shared libraries using GraalVM ahead-of-time compilation
  - Extracts text from images and scanned documents with OCR through `tesseract-ocr`.
  - 〰️ Extract a content of a file(URL/ bytes) to a `StreamReader` and perform buffered reading
- https://github.com/bzsanti/oxidizePdf /AGPL/202511/rust/NoDeps
  - A pure Rust PDF generation and manipulation library with zero external PDF dependencies.
  - Production-ready for basic PDF functionality with validated performance of 3, 000-4, 000 pages/second for realistic business documents
  - Pure Rust Core - No C dependencies for PDF operations (OCR feature requires Tesseract)
  - CJK Text Support - Chinese, Japanese, and Korean text rendering and extraction with ToUnicode CMap
  - AI/RAG Integration - Document chunking for LLM pipelines with sentence boundaries and metadata (v1.3.0+)
  - Low memory usage - Efficient streaming for large PDFs

- https://github.com/ucbepic/docetl /3.1kStar/MIT/202511/python
  - https://docetl.org/
  - DocETL is a tool for creating and executing data processing pipelines, especially suited for complex document processing tasks. 
  - It offers a low-code, declarative YAML interface to define LLM-powered operations on complex data.
  - DocETL is the ideal choice when you're looking to maximize correctness and output quality for complex tasks over a collection of documents or unstructured datasets.

- https://github.com/whyhow-ai/knowledge-table
  - 结构化数据提取工具，它可以以自然语言查询的方式从非结构化文档中提取结构化数据，并以表格或图表的形式展现
  - 文档数据的结构化入库，比如从合同里提取关键交易信息，然后结构化展示

- https://github.com/Goldziher/kreuzberg /2.4kStar/MIT/202509/python
  - https://kreuzberg.dev/
  - Kreuzberg is a modern Python library for text extraction from documents, designed for simplicity and efficiency
  - It provides a unified async interface for extracting text from a wide range of file formats including PDFs, images, office documents, and more.
  - Local Processing: No external API calls or cloud dependencies required
  - Modern Python: Built with async/await, type hints, and current best practices
  - Kreuzberg was created to solve text extraction needs in RAG (Retrieval Augmented Generation) applications, but it's suitable for any text extraction use case. 
  - Built on established open source foundations including Pandoc, PDFium, and Tesseract.
  - OCR Integration: Tesseract OCR with markdown output (default) and table extraction from scanned documents. Tesseract is Google's OCR engine for text recognition
  - PDFium: Google's PDF rendering engine for accurate PDF processing
  - Python-docx/pptx: Native Microsoft Office format support
  - Extensibility: Plugin architecture for custom extractors via the Extractor base class
  - API Design: Synchronous and asynchronous APIs with consistent interfaces
  - Type Safety: Complete type annotations throughout the codebase

## web-etl

- https://github.com/mendableai/firecrawl /AGPLv3/202502/python/rust/ts
  - https://firecrawl.dev/
  - Turn entire websites into LLM-ready markdown or structured data. 
  - Scrape, crawl and extract with a single API.
  - The hard stuff: proxies, anti-bot mechanisms, dynamic content (js-rendered), output parsing, orchestration
  - Batching (New): scrape thousands of URLs at the same time with a new async endpoint.
  - open-version: scrape, extract, map, formats, sdk
  - cloud-version: anti-bot, dashboard, actions, browserless, enterprise
  - This project is primarily licensed under AGPLv3
    - However, certain components of this project are licensed under the MIT 
    - The SDKs and some UI components are licensed under the MIT License. 
- https://github.com/OpenAISpace/ai-trend-publish /MIT/202502/ts
  - 一个基于 AI 的趋势发现和内容发布系统，支持多源数据采集、智能总结和自动发布到微信公众号
  - 多源数据采集: Twitter/X, 网站内容抓取 (基于 FireCrawl)
  - 使用 DeepseekAI 进行内容总结
  - 定时发布任务
  - 定时任务: node-cron
  - 模板引擎: EJS

- https://github.com/opendatalab/MinerU /AGPLv3/202407/python
  - MinerU 是一款一站式、开源、高质量的数据提取工具
  - Magic-PDF 是一款将 PDF 转化为 markdown 格式的工具。支持转换本地文档或者位于支持S3协议对象存储上的文件。
  - Magic-Doc 是一款支持将网页或多格式电子书转换为 markdown 格式的工具。
    - 支持176种语言的准确识别
  - https://huggingface.co/spaces/opendatalab/MinerU

- https://github.com/getmaxun/maxun /AGPL/202503/ts
  - https://www.maxun.dev/
  - Open-source no-code web data extraction platform. 
  - Maxun lets you create custom robots which emulate user actions and extract data. A robot can perform any of the actions: Capture List, Capture Text or Capture Screenshot. Once a robot is created, it will keep extracting data for you without manual intervention
  - BYOP (Bring Your Own Proxy) lets you connect external proxies to bypass anti-bot protection. Currently, the proxies are per user. Soon you'll be able to configure proxy per robot.

- https://github.com/NanoNets/docstrange /460Star/MIT/202508/python
  - https://docstrange.nanonets.com/
  - Extract and convert data from any document, images, pdfs, word doc, ppt or URL into multiple formats (Markdown, JSON, CSV, HTML) with intelligent content extraction and advanced OCR.
  - Cloud Processing (Default): Instant free conversion with cloud API 
  - Local Processing: CPU/GPU options for complete privacy - no data sent anywhere
  - 🐛 代码中未看到流式处理文件的逻辑, 对处理大文件不友好
  - Universal Input: PDFs, Word docs, Excel, PowerPoint, images, URLs, and raw text
  - URL Processing: Direct conversion from web pages
  - Smart Output: Markdown, JSON, CSV, HTML, and plain text formats
  - Advanced OCR: Multiple OCR engines with automatic fallback
  - MCP Server: Integrate with Claude Desktop for intelligent document navigation
  - [Package for converting PDF, images and docs to structured data like JSON, markdown, HTML : r/node _202509](https://www.reddit.com/r/node/comments/1nqxada/package_for_converting_pdf_images_and_docs_to/)
    - I've published a Node.js client for DocStrange 
# office
- https://github.com/paperless-ngx/paperless-ngx /GPLv3/202412/ts/python
  - https://docs.paperless-ngx.com/
  - https://demo.paperless-ngx.com/
  - Paperless-ngx is a document management system that transforms your physical documents into a searchable online archive so you can keep, well, less paper.
  - Paperless-ngx is compatible with many different scanners and scanning tools.
  - Once you've got Paperless setup, you need to start feeding documents into it
    - OCR the Document
    - create an archivable PDF/A document from your document. 
    - performs automatic matching of tags, correspondents and types on the document before storing it in the database.
    - The primary method of getting documents into your database is by putting them in the consumption directory. 
  - Paperless-ngx is the official successor to the original Paperless & Paperless-ng projects 
  - Utilizes the open-source `Tesseract` engine to recognize more than 100 languages.
  - Documents are saved as PDF/A format which is designed for long term storage, alongside the unaltered originals.
  - Paperless stores your documents plain on disk. Filenames and folders are managed by paperless and their format can be configured freely 
  - [Paperless-ngx – Open source document management system | Hacker News _202310](https://news.ycombinator.com/item?id=37800951)
  - https://github.com/icereed/paperless-gpt /1.4kStar/MIT/202509/go/ts
    - Use LLMs and LLM Vision (OCR) to handle paperless-ngx - Document Digitalization powered by AI
    - paperless-gpt seamlessly pairs with paperless-ngx to generate AI-powered document titles and tags, saving you hours of manual sorting. 
    - Harness Large Language Models (OpenAI or Ollama) for better-than-traditional OCR
  - https://github.com/signorecello/paperless-docling /202504/js/inactive
    - A service that automatically processes documents in Paperless using docling and updates their content.
    - [Better OCR with Docling : r/Paperlessngx _202504](https://www.reddit.com/r/Paperlessngx/comments/1jqqsly/better_ocr_with_docling/)
- https://github.com/clusterzx/paperless-ai /4.6kStar/MIT/202511/python/js
  - https://clusterzx.github.io/paperless-ai/
  - an AI-powered extension for Paperless-ngx that brings automatic document classification, smart tagging, and semantic search using OpenAI-compatible APIs and Ollama.
  - [Paperless-AI: Now including a RAG Chat for all of your documents : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kqbouu/paperlessai_now_including_a_rag_chat_for_all_of/)

- https://github.com/papra-hq/papra /2.4kStar/AGPL/202509/ts
  - https://demo.papra.app/
  - a minimalistic document management and archiving platform.
  - Papra is a platform for long-term document storage and management, like a digital archive for your documents.
  - no backend, client-side local storage only
  - Search: Quickly search for documents with full-text search.
  - Authentication: User accounts and authentication.
  - SolidJS, shadcn-solid, honojs, drizzle

- https://github.com/microsoft/markitdown /MIT/202411/python
  - Python tool for converting files and office documents to Markdown.
  - a utility tool for converting various files to Markdown (e.g., for indexing, text analysis, etc.)
  - supports: PDF (.pdf) PowerPoint (.pptx) Word (.docx) Excel (.xlsx) Images (EXIF metadata, and OCR) Audio (EXIF metadata, and speech transcription) HTML (special handling of Wikipedia, etc.) Various other text-based formats (csv, json, xml, etc.)
  - [PDF performance (PDFMiner) _202505](https://github.com/microsoft/markitdown/issues/1276)
    - I've been using MarkItDown for conversion of some PDF files in a project I'm working on and I've noticed it performs really poorly with larger documents.
    - This is in stark contrast to other libraries like PyMuPDF and specifically its markdown variant (PyMuPDF4LLM) which in my tests performed much faster.
  - [[Feature Request] Magika Dependency Optional ](https://github.com/microsoft/markitdown/issues/1234)
    - I'm trying to use MarkItDown in the browser via Pyodide and Magika's dependency on ONNX is causing trouble.
  - https://msftmd.replit.app/
    - Powered by Microsoft MarkItDown, this tool converts various file formats to clean, structured Markdown for easy analysis and indexing.
    - https://x.com/mattppal/status/1867703377888784880
      - If you're wondering how I did this so fast, it was Agent + Assistant + deploy on Replit
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
