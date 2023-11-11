---
title: toc-office-notion-like-knowledge-base-workspace
tags: [knowledge-base, notion-like, workspace]
created: 2022-06-03T21:27:36.001Z
modified: 2022-06-03T21:34:54.893Z
---

# toc-office-notion-like-knowledge-base-workspace

# guide

- 想要分析notion的block架构设计，可以参考clone示例

- 考虑使用epub/docx/docbook这类规范格式存储内容，方便迁移
  - 支持导入通用格式 markdown/csv
  - 偏代码的格式可考虑 rdf/json-ld

- resources
  - search: knowledge-base/workspace/wiki
  - self-contained, in the browser
# notion-like-workspace
- siyuan /6.6kStar/AGPLv3/202208/ts/go/支持协作
  - https://github.com/siyuan-note/siyuan
  - https://b3log.org/siyuan/
  - a local-first personal knowledge management system
  - 思源笔记是一款本地优先的个人知识管理系统，支持完全离线使用，同时也支持端到端加密同步。
    - 所有本地功能都是免费的，云端服务需要年付订阅。
    - 不支持网页版，要使用桌面版或移动版
  - SiYuan is made possible by the Vditor and Lute(golang)
  - 用户自己创建的笔记本文件夹下，.sy 后缀的文件用于保存文档数据，数据格式为JSON

- outline /18.3kStar/BSD > BSL/202302/ts
  - https://github.com/outline/outline
  - https://www.getoutline.com/
  - The fastest wiki and knowledge base for growing teams.
  - 依赖rich-markdown-editor、mobx-react、dnd-kit、framer-motion、i18next、markdown-it、reakit
  - 后端依赖postgres、redis、koa、sequelize、yjs、y-prosemirror、y-indexeddb
  - 与slack集成很好
  - 样式与airframe-react dashboard风格类似
  - [Adopt BSL 1.1 license__202003.v0.41.0](https://github.com/outline/outline/pull/1197)
  - [Convert from slate to Prosemirror_202005.v10.0.0](https://github.com/outline/rich-markdown-editor/pull/150)
  - ref
    - https://github.com/ProseWorker/ProseWriter

- think /1kStar/MIT/202208/ts/nestjs/tiptap
  - https://github.com/fantasticit/think
  - https://think.codingit.cn/
  - 依赖 MySQL/NextJS/nestjs/tiptap
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 前端依赖 @douyinfe/semi-ui、excalidraw、tiptap2、docx、katex、markdown-it、nextjs、react-pdf、react-query3、tippy.js、yjs
  - 后端依赖 nestjs、typeorm、passport、mysql、yjs
  - Think 是一款开源知识管理工具。通过独立的知识库空间，结构化地组织在线协作文档，实现知识的积累与沉淀，促进知识的复用与流通。同时支持多人协作文档。

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

- growi /1.1kStar/MIT/202301/ts/remark
  - https://github.com/weseek/growi
  - https://docs.growi.org/en/guide/
  - https://demo.growi.org/
  - Team collaboration software using markdown
  - 依赖 express、mongoose、es、redis、swr
  - Simultaneously edit with multiple people by HackMD(CodiMD) integration
  - Create hierarchical pages with markdown
  - Slack/Mattermost, IFTTT Integration
  - 各种集成

- affine /7.1kStar/MIT/202208/ts
  - https://github.com/toeverything/AFFiNE
  - https://affine.pro/
  - Affine is a next-gen knowledge base that brings planning, sorting and creating all together. Privacy first, open-source, customizable and ready to use.
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

- trilium /17.1kStar/AGPLv3/202208/js/ckeditor5/支持多端
  - https://github.com/zadam/trilium
  - https://github.com/zadam/trilium/wiki/
  - 依赖electron、express、jsdom、turndown、ckeditor.v5、codemirror5、jsplumb、fancytree、bootstrap
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - Synchronization with self-hosted sync server
  - Trilium is provided as either desktop application (Linux and Windows) or web application hosted on your server (Linux). 
    - Mac OS desktop build is available, but it is unsupported.
    - If you want to install Trilium on server,currently only recent Chrome and Firefox are supported (tested) browsers.
  - [Notion like database](https://github.com/zadam/trilium/issues/822)

- https://github.com/aliscie/odoc /rust/ts
  - This app is Notion.so clone, roam research clone and obsidian clone. 
  - The main purpose of this app is not to just clone these note-taking apps but to make an all-in-one Open source note-taking app with automation features.
  - make sure to install zstd llvm, clang and openssl, gcc, rocksdb in order for the desktop app to work (surealdb requirements).

- https://github.com/slotDumpling/multibility /ts/协同笔记与PDF批注
  - https://slotdumpling.github.io/multibility/
  - Collaborative notes and PDF annotations

- https://github.com/appotry/dootask /php/vue
  - https://www.dootask.com/
  - 轻量级的开源在线项目任务管理工具，提供各类文档协作工具、在线思维导图、在线流程图、项目管理、任务分发、即时IM，文件管理等工具。

- https://github.com/mintterteam/mintter /go/ts
  - https://mintter.com/
  - a decentralized knowledge collaboration application for open communities powered by a knowledge graph.

- https://github.com/austinvhuang/openmemex /rust/haskell
  - local-first knowledge integration platform optimized for automation (including caching and indexing of content) as well as enabling neural network machine learning integrations.
  - SQLite is the central data storage medium, rather than a collection of markdown documents.
  - Instead of users manually curating a knowledge graph, data is organized automatically by timestamp.
# confluence-like
- MrDoc /2.1kStar/GPL.v3/202208/js/python/仅网页版
  - https://github.com/zmister2016/MrDoc
  - https://mrdoc.pro/
  - http://mrdoc.zmister.com/project-20/
  - 个人和小型团队的云笔记、云文档、知识管理私有化部署方案
    - 场景：个人云笔记、在线产品手册、团队内部知识库、在线电子教程等私有化部署场景
  - 后端依赖: Python、Django
  - 前端依赖: LayUI、JQuery、vditor、luckysheet.v2
  - 功能特性: 文档资源管理、书写编辑、阅读分享、站点管理

- notabase /434Star/AGPLv3/202208/ts/仅网页版/supabase
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

- memos /260Star/NALic/202206/ts/go
  - https://github.com/usememos/memos
  - https://usememos.com/
  - 后端依赖 go
  - 前端依赖 redux-toolkit, dayjs, axios
  - 编辑器使用的是简单 textarea
  - ui高度复刻flomo，中文开发者作品，代码量不大
  - self-hosted knowledge base that works with a SQLite db file.
  - Write in the plain textarea without any burden
  - It has no external dependency.

- https://github.com/infobsmi/bsmi-kb
  - https://kb.bsmi.info/
  - 后端依赖 go
  - 样式过于简单
  - 这个项目诞生的原始驱动，是因为对“语雀” 知识库的不满。一直不喜欢语雀的目录，发布流程。

- https://github.com/hedgedoc/hedgedoc /AGPLv3
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
  - https://github.com/c2d7fa/nextool
    - GTD-oriented task manager with support for nested tasks and a focus on finding actionable tasks.

- https://github.com/documize/community
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

- https://github.com/andymatuschak/orbit /1.5kStar/apache2/202305/ts
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

- Ink-wash-docs /472Star/Apache2/202010/js
  - https://github.com/huangwei9527/Ink-wash-docs
  - 水墨文档，一款基于egg+vue开发的在线文档管理平台，支持markdown文档， excel文档，原型托管等功能.
  - 依赖vue、element-ui、vditor、egg、x-spreadsheet
  - 依赖vditor、x-data-spreadsheet、vue2、vuex3、element-ui2、egg2

- https://github.com/RealRong/Rendevoz
  - open-source knowledge management application built with React and TypeScript
  - 依赖slate、yjs、rxjs
  - WYSIWYG Block Editor built upon Slate.js, with drag & drop, custom block rendering, etc.
  - Cross platform powered by Electron.

- https://github.com/courajs/referent /js
  - An offline-first, realtime-collaborative wiki engine
# TiddlyWiki/in-memory
- TiddlyWiki5 /7.5kStar/BSD/202311/js
  - https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/
  - https://tiddlywiki.com/dev/ Developer documentation
  - A self-contained JavaScript wiki for the browser, Node.js, AWS Lambda etc.
  - a non-linear personal web notebook that anyone can use and keep forever
  - It can be used as a single HTML file in the browser or as a powerful Node.js application. 
  - Except of a micro-kernel written in JavaScript the whole application consist of a own data-structure called tiddlers and a own markup language called wikiText.
  - view层基于tid文件
  - https://github.com/TiddlyWiki/TiddlyWiki
    - the Classic version (2.x.x) of TiddlyWiki

- https://github.com/TiddlyWiki/TiddlyDesktop /202307/js
  - A custom desktop browser for TiddlyWiki 5 and TiddlyWiki Classic, based on nw.js

- https://github.com/tiddly-gittly/TidGi-Desktop /1.2kStar/MPLv2/202309/ts
  - https://tidgi.fun/
  - 「 太记 」是一个基于「 太微 TiddlyWiki 」的知识管理桌面应用，能保护隐私内容、高级自动化、自动Git云备份、部署为博客，且可通过RESTAPI与Anki等应用连接。
  - 太微的NodeJS版本有无缝的自动保存体验，这是利用 SyncAdaptor 技术（而不是 Saver ）带来的的优势，太记对 NodeJS wiki 有更好的支持，而 TD 主要支持 HTML 版单文件 WIKI，各有优势

- https://github.com/jokroese/tiddlyroam /202005/html/inactive
  - TiddlyRoam is a TiddlyWiki with bi-directional links and graph maps.
  - The project aims to provide a free and open source alternative to the popular Roam.

- https://github.com/abesamma/TW5-editions
  - A (still growing) collection of useful editions of Tiddlywiki5(TW5) that I use.
  - Empty edition: The "empty" edition of TiddlyWiki is a vanilla distribution, with only maarfapad plugin
  - JD Whitespace: a beautiful edition with a sidebar that has extended functionality with a UI that focused on whitespace
  - Streambook: a RoamResearch-esque edition with a 2 panel story view and outline system
- https://github.com/abesamma/oneplaybook-app /MPLv2/202105/js/inactive
  - https://oneplaybook.app/
  - a web app that allows you to quickly get started building federated internal wiki systems with TiddlyWiki
  - helps you capture, organize and share knowledge better with TiddlyWiki5.
  - offline-ready
  - This webpage runs on Gatsby, Reactjs, TailwindCSS and Material-UI.

- https://github.com/OokTech/TW5-Bob /202311/js
  - A plugin that makes tiddlywiki a multi-user wiki on node
  - Multi-User support for using/editing the same wiki(s) simultaneously
  - Two-way real-time syncing between the browser and file system
  - Inter-server federation. Different Bob servers can communicate to share tiddlers and as chat servers/relays

- https://github.com/postkevone/tiddlystudy
  - https://postkevone.github.io/tiddlystudy
  - note-taking tool based on tiddlywiki

- https://github.com/Alamantus/FeatherWiki /91Star/AGPLv3/202310/js
  - https://codeberg.org/Alamantus/FeatherWiki
  - Feather Wiki is a lightning fast infinitely extensible tool for creating personal non-linear notebooks, databases, and wikis that is entirely self-contained, runs in your browser, and is only 55 kilobytes. 
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

- https://github.com/benweet/stackedit /apache2/js/vue
  - https://stackedit.io/
  - Full-featured, open-source Markdown editor based on PageDown, the Markdown library used by Stack Overflow and the other Stack Exchange sites.
- https://github.com/josephernest/writing /202208/js
  - a lightweight distraction-free text editor, in the browser (Markdown and LaTeX supported).
  - no server needed, you can run it offline

- https://github.com/Arlen22/TiddlyServer /202111/ts
  - A static file server that can also save files and mount TiddlyWiki folders
# knowledge-base/wiki
- monotome /151Star/AGPLv3/202208/js
  - https://github.com/cblgh/monotome
  - a personal knowledge base system. markdown markup, runs in the browser
  - 依赖 marked
  - 原理是 根据url动态读取解析markdown文件，并渲染显示所有文件名
  - 代码量不大，思路清晰
  - Monotome has support for the common `[[wiki]]` syntax, 
  - Subjects are ordered into a simple directory structure which is mirrored by index.json.

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

- https://github.com/Requarks/wiki /AGPLv3/202310/js/vue
  - https://js.wiki/
  - A modern and powerful wiki app built on Node.js
  - [Wiki.js | Hacker News_202007](https://news.ycombinator.com/item?id=23904193)

- https://github.com/ryanlelek/Raneto /202208/js
  - https://docs.raneto.com/
  - Markdown powered Knowledgebase Wiki for Node.js
  - 比较典型的问答型知识库
  - Raneto is a "flat file" CMS, meaning no database problems, no MySQL queries, nothing.
  - Full-text search powered by Lunr
  - [Raneto – Markdown Knowledgebase Platform | Hacker News_201707](https://news.ycombinator.com/item?id=14839371)

- https://github.com/wikimedia/mediawiki /GPL/php
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

- https://github.com/dokuwiki/dokuwiki /GPL/php
  - http://www.dokuwiki.org/
  - a simple to use and highly versatile Open Source wiki software that doesn't require a database
  - Built in access controls and authentication connectors make DokuWiki especially useful in the enterprise context 

- https://github.com/BookStackApp/BookStack /php
  - https://www.bookstackapp.com/
  - A platform to create documentation/wiki content built with PHP & Laravel

- https://github.com/xwiki/xwiki-platform /java
  - XWiki Platform is a generic wiki platform offering runtime services for applications built on top of it.
  - XWiki Commons, XWiki Rendering, and XWiki Platform are part of the XWiki.org software forge. They are released together and share the same version.
  - Over 600 extensions: applications, macros, skins, plugins, themes, etc.
  - Learn about XWiki's concept and why it's an alternative to Confluence and MediaWiki

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
- foam /12.5kStar/MIT/202208/ts/vscode
  - https://github.com/foambubble/foam
  - https://foambubble.github.io/foam/
  - Foam is a personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - core基于remark

- memo /613Star/MIT/202208/ts/vscode
  - https://github.com/svsool/memo
  - Markdown knowledge base with bidirectional [[link]]s built on top of VSCode
  - Inspired by Obsidian.md and RoamResearch.

- dendron /4.3kStar/AGPLv3/202208/ts/vscode
  - https://github.com/dendronhq/dendron
  - https://wiki.dendron.so/
  - local-first, markdown-based, note-taking tool built on top of VSCode. 
  - Dendron finds the usable center between the two extremes by supporting backlinks of any two arbitrary notes while also maintaining a canonical hierarchy for every note. 
  - We do this through our hierarchal first approach to note taking that relies on the combination of hierarchies, schemas, and path based lookups.
  - [A Hierarchy First Approach to Note Taking](https://www.kevinslin.com/notes/3dd58f62-fee5-4f93-b9f1-b0f0f59a9b64.html)
    - My primary use for notes is as a cache. Think Redis, but for humans.
    - If I spent more than 5 minutes figuring something out, those are five minutes I never want to spend again figuring out the same problem.
    - But this is difficult to do in practice.
    - My solution is something I call hierarchical note taking.

- https://github.com/TevinLi/amWiki  /885Star/MIT/201711/js/NoDeps
  - http://amwiki.org/doc
  - 由 JS 开发、依赖 Atom 或 Nodejs-Npm 的 Markdown 轻量级前端化开源文库系统。
  - 不用数据库，文档使用 .md 格式保存本地文件
  - 无需服务端开发，只需支持http静态访问网页空间
  - 自动更新文库导航目录，支持多级目录
  - 无需服务端的全文库内容搜索与计分排序

- https://github.com/silverbulletmd/silverbullet /MIT/ts
  - https://silverbullet.md/
  - SilverBullet is an extensible, open source personal knowledge platform. 
  - implemented as an offline-first PWA
  - At its core it’s a clean markdown-based writing/note taking application that stores your pages (notes) as plain markdown files in a folder referred to as a space. 
  - While SB uses a database for indexing and caching some indexes, all of that can be rebuilt from its markdown source at any time. 
  - extensible with plugs, and you can customize it
  - [Silver Bullet: Markdown-based extensible open source personal knowledge platform | Hacker News_202212](https://news.ycombinator.com/item?id=33843009)
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
# more
- https://github.com/notea-org/notea
  - Self hosted note taking app stored on S3
  - 依赖自己维护的@notea/rich-markdown-editor
  - Support storage in Amazon S3, MinIO, Aliyun OSS, etc

- https://github.com/zhyd1997/DragonLi /202209/ts
  - https://dragon-li.on.fleek.co/
  - a blog platform and alternative to Mirror
  - support favourite writers in seconds stream for readers by integrated with Superfluid instead of one-time payment.

- https://github.com/unigraph-dev/unigraph-dev /
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
