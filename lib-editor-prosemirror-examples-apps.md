---
title: lib-editor-prosemirror-examples-apps
tags: [app, prosemirror, toc]
created: 2022-08-18T16:56:32.322Z
modified: 2022-08-18T16:57:15.296Z
---

# lib-editor-prosemirror-examples-apps

# guide

# office/notebook
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

- noteworthy /166Star/AGPLv3/202207/ts/electron
  - https://github.com/benrbray/noteworthy
  - https://noteworthy.ink/
  - Markdown editor with bidirectional links and excellent math support
  - 依赖solid-js、remark13、prosemirror、electron-window-state、remark
  - 参考了prosemirror、zettlr、vscode、notable
    - Thanks to Fabio Spampinato for releasing the source to an early version Notable!
  - https://github.com/benrbray/prosemirror-math

- tiny-write /4Star/NALic/202208/ts/prosemirror/markdown-it/web版+桌面版
  - https://github.com/dennis84/tiny-write
  - https://tiny-write.pages.dev/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但不支持拖入拖出list item
  - 不支持/斜杠菜单
  - 依赖solid-js、codemirror6、idb-keyval、date-fns、markdown-it、y-prosemirror
  - Just a little writing tool with markdown shortcuts that saves every change to local indexeddb.
  - 跨平台客户端基于tauri实现，tauri部分使用rust实现

- Starboard Notebook /889Star/MPLv2/202206/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.
  - 编辑器已分离，基于rich-markdown-editor和prosemirror
  - 前端基于lit

- notesnook /2.8kStar/GPLv3/202209/js+ts/tiptap
  - https://github.com/streetwriters/notesnook
  - https://notesnook.com/
  - open source & end-to-end encrypted note taking alternative to Evernote.
  - web编辑器和移动端编辑器都依赖tiptap2、zustand、unfurl.js(oembed)、re-resizable、katex
  - @notesnook/streamable-fs: Streaming interface around an IndexedDB based file system
  - Notesnook encrypts everything on your device using `XChaCha20-Poly1305` & `Argon2`.
  - 服务端数据同步代码未找到
  - [Option to add custom server url in notesnook apps_20221010](https://github.com/streetwriters/notesnook/issues/1162)
    - We are planning to open source sync server early next month.
  - [A fully open-source and end-to-end encrypted note taking alternative to Evernote | Hacker News_202209](https://news.ycombinator.com/item?id=32708019)

- bear-plus /5Star/ISC/202008/js/ejs
  - https://github.com/yk9331/bear-plus
  - https://bear-plus.yenchenkuo.com/@bear-plus/features
  - 依赖codemirror.v5、express、markdown-it、sequelize、express、multer
  - A web-based writing application with real-time collaboration and Markdown syntax support for crafting and sharing notes. 
  - Group and find note easily with hashtag and full text search. Inspired by Bear note and HackMD.

- yana /175Star/MIT/202201/ts/electron/atlaskit
  - https://github.com/lukasbach/yana
  - https://yana.js.org/
  - 依赖electron、sqlite3
  - 可选编辑器 atlaskit/monaco
  - 文章内容保存在本地sqlite，而不是markdown文件
  - 产品功能简洁，体验友好
  - note-taking app with nested documents, full-text search, rich-text editor, code snippet editor
  - a powerful notebook app which allows you to manage local workspaces of hierarchically structured taggable and searchable notes.
  - Rich notes editor powered by the Atlassian editor core
  - Multiple local workspaces

- codex /195Star/CC-BY-NC-4.0/202202/js/electron
  - https://github.com/jcv8000/Codex
  - https://codexnotes.com/
  - 依赖 prosemirror、katex、bootstrap4、jquery、highlight.js
  - A free note-taking software for programmers and Computer Science students

- mdSilo-web /208Star/AGPLv3/202309/ts/web+桌面
  - https://github.com/danloh/mdSilo-web
  - https://github.com/mdSilo/mdSilo-web
  - https://mdsilo.com/
  - A local-first mind silo for storing ideas, thought, knowledge with a powerful writing tool, running fully in the browser.
  - 核心编辑器mdsmirror未开源，基于rich-markdown-editor
  - 依赖 react、tauri/rust、localforage、dnd-kit、headlessui-react、popperjs、react-spring、tailwindcss、d3-drag/selection、fuse.js、immer、codemirror.v6、styled-comp、react-virtualized、zustand
  - If your browser doesn't support local file system APIs, you'll still be able to open individual local files or import JSON file 
  - Since mdSilo Web app is running completely within the browser, some experiences will naturally be more constrained
  - Available for Web, Linux, Windows and macOS. 
- mdSilo-app /93Star/AGPLv3/202208/ts/tauri
  - https://github.com/mdSilo/mdSilo-app
  - https://github.com/danloh/mdSilo-app
  - https://mdsilo.com/
  - A mind silo for storing ideas, thought, knowledge with a powerful writing tool. 

- https://github.com/shi-yan/Epiphany /js/tauri
  - A note-taking App with a static blog generator focusing on technical writing, inspiration from Notion

- UreekaBiz-notebook /11Star/MIT/202208/ts/提交多
  - https://github.com/UreekaBiz/notebook
  - ProseMirror, Firebase Collaborative Editor.
  - https://github.com/UreekaBiz/pm-devtool
    - /4Star/MIT/202208/ts/提交多
    - ProseMirror-based Editor
  - https://ureeka.biz/
    - Ureeka is the ultimate small business growth engine built by successful entrepreneurs who know the formula proven to drive growth.

- mnote /1Star/MPL.v2/202208/ts/tauri/提交多
  - https://github.com/gfrancine/mnote
  - Mnote: a desktop app to write notes in more than just text

- neno /365Star/GPLv3/202205/js/svelte
  - https://github.com/openneno/neno
  - https://neno.pages.dev/
  - 使用svelte+tailwindcss 仿照 浮墨 写的pwa应用
  - 支持同步内容到Notion(使用github action)
  - 编辑器迁移到了quill
- https://github.com/juner0608/neno /inactive
  - 仿照浮墨的开源版本
  - svelte+tailwindcss构建的PWA应用
    - 依赖prosemirror、idb
  - 无需后端, 完全使用github进行存储你的所有数据, 文字和图片
  - 支持完全离线使用
  - 支持完整版数据导入导出
# prose-apps
- fiduswriter /455Star/AGPLv3/202209/python/js
  - https://github.com/fiduswriter/fiduswriter
  - https://github.com/fiduswriter/fiduswriter/blob/main/fiduswriter/document/static/js/modules/editor/index.js
  - 依赖@vivliostyle/print、prosemirror、sortablejs、mathlive
  - an online collaborative editor especially made for academics who need to use citations and/or formulas.
  - The editor focuses on the content rather than the layout, so that with the same text, you can later on publish it in multiple ways: On a website, as a printed book, or as an ebook. 
  - 实现了track-changes

- binder /24Star/NALic/202210/ts
  - https://github.com/mpazik/binder
  - https://docland.app/
  - 依赖 prosemirror、linki(自研框架)、pdfjs
  - allows a user to display, organize, search and store all the articles and ebooks a person has ever read, together with personal annotations and comments.
  - The application is right now a distraction-free web reader 
  - PDFs and EPUBs support (in future other formats)
  - data are stored in open formats on a personal cloud drive, so good privacy, no-vendor lock-in

- oak /4Star/MIT/202208/js/提交多/page-builder
  - https://github.com/p3ol/oak
  - 整体上是一个可切换文本编辑器的页面编辑器
  - 页面从上到下由块构成，内容文字默认不可编辑，需要点击悬浮编辑按钮
  - Modern, lightweight & modulable page builder
  - @poool/oak-addon-richtext-field: WYSIWYG text field using Slate
  - @poool/oak-addon-richtext-field-prosemirror: WYSIWYG text field using ProseMirror

- wix-tiptap-editor /260Star/MIT/202008/ts
  - https://github.com/wix/ricos
  - https://wix-rich-content.herokuapp.com/
  - https://ricos.js.org/docs/ricos/ricos-intro
  - 每行前有加号，但每行不支持拖拽block修改顺序
  - A React-based rich content editor with an extensible plugin system
  - wix公司开源了自己的内容编辑器，公开了自己的json schema规范，提供了wix-rich-content-editor、wix-rich-content-viewer
  - 还支持在基于tiptap v2的编辑器中编辑内容，提供了draftToTiptap()转换方法，将ricos-draft的json格式转换成tiptap支持的json格式
  - 内部插件大多严重依赖自研ui库和基础库，如wix-rich-content-ui-components、ricos-content

- mashcard /204Star/Apache2/202208/ts/ruby
  - https://github.com/mashcard/mashcard
  - https://www.producthunt.com/upcoming/brickdoc
  - 旧编辑器tiptap，新编辑器直接使用prosemirror
  - MashCard is an all-in-one workspace and low-code platform with Compound Document at its core. 
  - It's not only an open source alternative to Coda and Notion

- tropy /637Star/AGPLv3/202208/js
  - https://github.com/tropy/tropy
  - https://tropy.org/
  - help to organize and describe your research photos so you can quickly find your sources 
  - use tags and lists to organize your research items
  - annotation tools allow you to transcribe documents, select image details
  - exports your research projects as JSON‑LD, CSV, and even directly to Omeka S. 

- https://github.com/pageboard/client /4Star/MIT/202208/js
  - uses prosemirror to drive HTML wysiwyg editing.

- https://github.com/pierre-lgb/slashwriter
  - 依赖tiptap.v2、redux-toolkit、supabase、express、yjs

- https://github.com/bcc-code/bcc-live-transcriber
  - 依赖tiptap.v2、yjs、vue3
  - A live transcribing app for sharing a meeting with deaf people.
  - The idea is to offer a simplistic keyboard only transcriber app with real time streaming and support for insterting bible verses.

- https://github.com/iojanis/Lity
  - 依赖tiptap.v2、yjs、vue3
  - Graph-based document editor with collaborative features
  - Create nodes by mouse, keyboard shortcuts or using markup (like @ and soon #)

- https://github.com/HarshvardhanMor/online-code-editor
  - 依赖tiptap.v2、vue2

- https://github.com/Privoce/privoce-editor
  - This editor supports markdown, @ and #.
# prose-cms
- alternatives
  - outline

- https://github.com/dasmikko/strapi-tiptap-editor
  - A drop-in replacement for the strapi editor.

- alinea /654Star/MIT/202311/ts
  - https://github.com/alineacms/alinea
  - https://alinea.sh/
  - https://demo.alinea.sh/
  - an open source headless CMS written in Typescript.
  - 非wysiwyg，左侧编辑块数据，右侧预览
  - 依赖dnd-kit、yjs、react-query、tiptap
  - Content is stored in flat files and committed to your repository
  - 👉🏻 Content is easily queryable through an in-memory SQLite database
  - Content is fully typed
  - Content is available during static site generation and when server side querying. Content is bundled with your code and can be queried with zero network overhead.
  - Alinea supports custom backends that can be hosted as a simple Node.js process or on serverless runtimes.
    - Hosting an Alinea backend requires several services such as storing and retrieving drafts, publishing changes and authenticating users

- https://github.com/PelagicCreatures/marlin /202204/js/inactive
  - An ExpressJS CMS for sites with Sequelize db backends
  - Data model driven database (sequelize)
  - Admin data editing UI suite automatically built from data model
  - ACL access control on tables by user role (superuser, admin, etc.)
  - 前端依赖pug，未找到prosemirror
  - https://github.com/PelagicCreatures/marlin-app
    - a boilerplate app that includes many common functions of a web site/app featuring registered users. 
    - we use HIJAX to load pages after the initial load. 
    - 【DOM编程艺术】 Hijax---渐进增强地使用Ajax 
    - 按照老传统，让表单把整个页面都提交到服务器，然后服务器再发回来一个包含反馈的新页面，所有处理操作都在服务器上完成
    - 为了给这个登录表单添加AJAX功能，就需要拦截提交表单的请求,让XMLHttpRequest请求来代为发送

- becomesco-cms /ts/MIT
  - BCMS is a Headless CMS (Content Management System). 
  - It provides a powerful API, best-in-class model builder, and intuitive content editor.
  - https://github.com/becomesco/cms-ui /ts
    - a dashboard for the BCMS and provides UI features.
    - 依赖tiptap.v2、vue3、vuex、markdown-it、uppy/file-uploader、codemirror5、yjs
    - BCMS is a Headless CMS.
  - https://github.com/becomesco/cms-backend /ts
    - 后端基于express自研
    - handles common and custom backend tasks. 
    - Those tasks include communication with the database, database caching, scoping, restrictions and security, object aggregation and relational updates, real-time connection with sockets, and many more.
  - https://github.com/becomesco/cms-sdk
    - a layer of abstraction between the UI and the backend. It handles caching, communication with the backend API, and data synchronization
    - Idea behind this module is to abstract API communication for BCMS UI developers. 
    - Without this module, UI developers would have to implement REST API calls for the Backend module and take care of caching and storing data. 

- https://github.com/primodotso/primo
  - https://primo.so/
  - ui基于svelte
  - Primo is a component-based CMS that makes it easy to build visually-editable static sites

- https://github.com/statamic/cms /php
  - flat-first, Laravel + Git powered CMS 

- https://github.com/erellsworth/overlord
  - CMS built with Nuxt, Express, and Tiptap.

- https://github.com/factly/dega /go
  - lightweight, scalable & high performant CMS written in Go & React. 
  - https://github.com/factly/scooter /js
    - editor built on top of TipTap & Prosemirror.
# more-prosemirror-examples
- https://github.com/devmnj/react-editor-framework-examples
  - This is a set of Editor Example (React) with TinyMCE, RMirror, Draftjs, MuiEditor and Slatejs .
- https://github.com/khirayama/aha
  - 比较多个编辑器 prosemirror、lexical、tinymce

- https://github.com/lawrencecchen/azinaka
  - http://azinaka.vercel.app/
  - Browser based notes.
  - 依赖solidjs

- https://github.com/NoteHub-official/RetroFlux
  - fully-customizable collaborative knowledge management app featuring note-taking, note-sharing, community, knowledge graph functionalities.

- https://github.com/ShenQingchuan/HeteroDoc
  - Heterocube Cloud Collaborative Docs. 
  - Built with Vue3 + TypeScript + ProseMirror + Y.js + DeepKit

- https://github.com/abingham/prosemirror-tauri
  - an experiment to try using the ProseMirror editor widget with the Tauri application framework.

- https://github.com/dec0dOS/standard-notes-ultimate-editor
  - This is a text editor for the encrypted note-taking app https://standardnotes.org/. A mobile-friendly and high-performance editor.

- https://github.com/Bernd-L/DoubleNote /angular
  - https://doublenote.bernd.pw/
  - An Angular note taking app supporting both real-time and async collaboration using Markdown or a WYSIWYG editor, optimised for peer-to-peer usage with optional commit-based versioning

- https://github.com/herrdu/prosemirror /202008/ts
  - 个人使用的prosemirror合集版本，手动ts化

- https://github.com/gamejolt/gamejolt
  - This is the whole frontend for Game Jolt. It powers the site and the desktop app.

- https://github.com/isle-project/isle-editor
  - https://isledocs.com/
  - Editor for ISLE (Integrated Statistics Learning Environment) lessons.
  - A desktop-application that can be used to author and preview integrated statistics learning environment (ISLE) lessons before they are deployed online. 
  - https://github.com/isle-project/isle-server
  - https://github.com/isle-project/isle-dashboard

- https://github.com/blinkk/editor.dev-ui
  - https://editor.dev/example/
  - Provides a rich UI for editing structured data with live previews.

- https://github.com/salmenf/webwriter
  - Web-based authoring tool for open explorables
  - Author open, interactive and multimedial content on Windows/Mac/Linux
  - WebWriter is the product of a dissertation project at RWTH Aachen University’s Learning Technologies Research Group.

- https://github.com/archguard/archguard-frontend
  - ProseMirror as core editor
  - MonacoEditor as a source code editor

- https://github.com/manakuro/project-management-demo-frontend
  - https://project-management-demo.manatoworks.me/
  - ui设计友好

- https://github.com/pipipi-pikachu/PPTist
  - https://pipipi-pikachu.github.io/PPTist/
  - 基于 Vue3.x + TypeScript 的在线演示文稿（幻灯片）应用，还原了大部分 Office PowerPoint 常用功能，实现在线PPT的编辑、演示。支持导出PPT文件。

- https://github.com/stencila/stencila
  - https://stenci.la/
  - a platform for authoring, collaborating on, and publishing executable documents.

- https://github.com/xland/redredstar
  - 个人信息管理工具

- https://github.com/mpazik/docland
  - https://docland.app/
  - an application that allows a user to display, organize, search and store all the articles and ebooks a person has ever read, together with personal annotations and comments.
  - Docland's mission is to give you control over your data. Its design goal is to store all information documents together, forever.

- https://github.com/webxdc/yjs_editor
  - This tool uses yjs (A CRDT tool), Deltachat and Vuejs to provide a WYSIWYG editor which can be used right out of deltachat.

- https://github.com/martinemmert/fleeting-notes-editor

- https://github.com/diffgram/diffgram
  - https://diffgram.com/
  - Modern Training Data platform for machine learning delivered as a single application.
  - Training Data (Data Labeling, Annotation, Catalog, Workflow) for all Data Types (Image, Video, 3D, Text, Geo, Audio, more) at scale.

- https://github.com/lyn-2k1/fullstackReactjs

- https://github.com/gracious-tech/stello
  - A new way to send newsletters 
  - 依赖tiptap.v2
