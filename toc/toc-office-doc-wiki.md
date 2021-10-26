---
title: toc-office-doc-wiki
tags: [documentation, office, toc, wiki]
created: '2021-07-23T08:38:26.538Z'
modified: '2021-07-23T08:38:53.805Z'
---

# toc-office-doc-wiki

# guide

- 文章集合的设计
  - 文章pages、知乎专栏、掘金小册、文集
# github-wiki-confluence-like
- MrDoc /1.4kStar/GPLv3/202107/js/python
  - https://github.com/zmister2016/MrDoc
  - http://mrdoc.zmister.com/project-20/
  - MrDoc是基于Python开发的在线文档系统，适合作为个人和小型团队的私有云文档、云笔记和知识管理工具
  - 后端: Python + Django
  - 前端: LayUI + JQuery
  - 功能特性: 文档资源管理、书写编辑、阅读分享、站点管理
  - 使用场景: 笔记、文档、手册、教程、私有化部署

- outline /12.5kStar/BSD > BSL/202109/js
  - https://github.com/outline/outline
  - The fastest wiki and knowledge base for growing teams.
  - 依赖rich-markdown-editor、postgres、redis
  - 与slack集成很好
  - 样式与airframe-react dashboard风格类似
  - [Adopt BSL 1.1 license__202003.v0.41.0](https://github.com/outline/outline/pull/1197)

- foam /10.4kStar/MIT/202109/ts
  - https://github.com/foambubble/foam
  - https://foambubble.github.io/foam/
  - Foam is a personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - core基于remark

- https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/
  - a unique non-linear notebook for capturing, organising and sharing complex information

- https://github.com/zadam/trilium
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - 依赖 electron、express、jsdom、turndown、ckeditor、codemirror、fancytree、bootstrap

- https://github.com/hedgedoc/hedgedoc /AGPLv3
  - https://docs.hedgedoc.org/setup/getting-started/
  - https://demo.hedgedoc.org/features
  - 后端依赖nestjs.v8、rxjs.v7、sqlite3、typeorm、passport
  - HedgeDoc is a real-time, multi-platform collaborative markdown note editor.
  - HedgeDoc (formerly known as CodiMD) is an open-source, web-based, self-hosted, collaborative markdown editor.
  - We are currently working on HedgeDoc 2, a complete rewrite of HedgeDoc.
  - [fork history](https://hedgedoc.org/history/): HedgeDoc is the community-driven fork of CodiMD
- https://github.com/hedgedoc/react-client
  - https://ui-test.hedgedoc.org/intro
  - 前端依赖 react、redux、codemirror.v5、bootstrap.v4、flowchart.js、markdown-it.v12、katex、vega

- https://github.com/jaredly/local-first
  - This aims to eventually be a fully-featured solution for managing, syncing, and storing application data, in a way that works offline, and collaboratively.

- https://github.com/documize/community
  - https://docs.documize.com/
  - Modern Confluence alternative designed for internal & external docs, built with Golang + EmberJS
  - [Understanding Document Basics](https://docs.documize.com/s/WOzFU_MXigAB6sIH/user-guides/d/WOvEC_MXigAB6sE1/understanding-document-basics)
    - How Documize works: sections, revisions, attachments
    - A document in Documize consists of sections. 
    - Content Sections allow for content to be typed in just like Microsoft Word, Google Docs or wiki software.
      - Rich Text, Markdown, Code Tabular
    - Data Sections allow live-linking and sync'ing of data from popular cloud-based systems
      - Airtable, GitHub, Trello, etc.
    - toc, linking, tagging, attachments, revisions & rollback, doc-lifecycle

- https://github.com/airbnb/knowledge-repo
  - https://knowledge-repo.readthedocs.io/en/latest/
  - A next-generation curated knowledge sharing platform for data scientists and other technical professions.
  - Knowledge Repo project is focused on facilitating the sharing of knowledge between data scientists and other technical roles using data formats and tools 

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

- https://github.com/siyuan-note/siyuan /CodeNA
  - https://b3log.org/siyuan/
  - a local-first personal knowledge management system
  - SiYuan is made possible by the Vditor and Lute(golang)
  - 用户自己创建的笔记本文件夹下，.sy 后缀的文件用于保存文档数据，数据格式为 JSON

- https://github.com/logseq/logseq
  - 依赖clojure
  - A local-first, non-linear, outliner notebook for organizing and sharing your personal knowledge base.
  - A privacy-first, open-source platform for knowledge management and collaboration
- https://github.com/andymatuschak/orbit
  - Orbit is an experimental platform for publishing and engaging with small tasks repeatedly over time.

- https://github.com/crowi/crowi
  - http://demo.crowi.wiki/
  - The Markdown Wiki 
  - URL Based Page Tree
  - pages that end with slashes (/) are automatically generated as list views. 
  - 功能和样式都很普通

- https://github.com/TevinLi/amWiki  /NoDeps
  - http://amwiki.org/doc
  - 由 JS 开发、依赖 Atom 或 Nodejs-Npm 的 Markdown 轻量级前端化开源文库系统。
  - 不用数据库，文档使用 .md 格式保存本地文件
  - 无需服务端开发，只需支持http静态访问网页空间
  - 自动更新文库导航目录，支持多级目录
  - 无需服务端的全文库内容搜索与计分排序

- https://github.com/huangwei9527/Ink-wash-docs
  - 水墨文档，一款基于egg+vue开发的在线文档管理平台，支持markdown文档， excel文档，原型托管等功能.
  - 依赖vue、element-ui、vditor、egg、x-spreadsheet
# wiki-like
- https://github.com/wikimedia/oojs-ui
  - https://www.mediawiki.org/wiki/OOUI
  - OOUI is a modern JavaScript UI library with strong cross-browser support. 
  - It is the standard library for MediaWiki and Wikipedia. 
- https://github.com/wikimedia/WikimediaUI-Style-Guide
  - https://design.wikimedia.org/style-guide/
  - Wikimedia Design Style Guide with user interface focus
- https://github.com/wikimedia/wikimedia-ui-base
  - https://gerrit.wikimedia.org/g/wikimedia-ui-base/
  - Wikimedia Foundation basic user interface style values. 
  - 提供了wikimedia-ui-base.css/less

- https://github.com/Mithesh14/Wikipedia-clone
  - https://mithesh14.github.io/Wikipedia-clone/
  - 只重新设计了主页和搜索页，不包含文章页

- https://github.com/claudioc/jingo
  - A git based wiki engine written for node.js
  - No database: Jingo uses a git repository as the document archive
  - Jingo uses Codemirror or Markitup as the markup editor, with a nice (ajax) preview 
- https://github.com/gollum/gollum
  - Git-powered wiki with a sweet API and local frontend.
  - 依赖 ruby
- https://github.com/kawasima/rotom
  - Git based Wiki system (Gollum clone)
- https://github.com/dijs/wiki
  - https://dijs.github.io/wiki/
  - WikiJs is a node.js library which serves as an interface to Wikipedia (or any MediaWiki).
  - Search wiki articles
  - Fetch article content
  - Find all links/images/categories in a article page
  - Get parsed information about articles
  - Find articles by geographical location

- https://github.com/microsoft/PowerBI-JavaScript
  - A client side library for embedding Power BI using JavaScript or TypeScript into your apps.

- https://github.com/MisaOgura/wiki-react-node-sqlite
  - Wiki-like app with React, React Router, Express and SQLite

- https://github.com/Drassil/git-wiki-theme
  - http://drassil.github.io/git-wiki/
  - https://github.com/Drassil/git-wiki
  - Git-wiki is a modular and full featured wiki powered by Git, GitHub/Gitlab Pages and pull requests!

- https://github.com/tomayac/wikipedia-tools-for-google-spreadsheets
  - A Google Spreadsheets add-on that makes working with data from Wikipedia and Wikidata a joy.
- https://github.com/hackerkid/Wikifeedia
  - Wikipedia turned into a newsfeed
  - As of now there is no API for getting a list of featured articles that changes each time one make a request. 
  - To facilitate this I had to to make a new API server along with some Javascript tweaks
  - https://github.com/hackerkid/Wikifeedia-backend /php
