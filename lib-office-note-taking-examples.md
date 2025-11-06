---
title: lib-office-note-taking-examples
tags: [app, cross-platform, note-taking, office, toc]
created: 2020-10-22T09:55:31.796Z
modified: 2024-01-30T20:56:45.773Z
---

# lib-office-note-taking-examples

# guide

- web版 vs 桌面版 vs vscode扩展版
  - 现有插件生态、编辑器切换
  - 要在侧重web(no-server)和侧重本地(c/s或b/s)的架构上做取舍，主要考虑数据源、数据量、性能
  - 还要在csr/ssr上做选择，没有大而全的架构

- files-first vs database-first
  - 若要实现web版产品，files-first的抽象在数据访问和查询时会很不方便

- note-solutions
  - web-first: TiddlyWiki
  - database-first: joplin, trilium, siyuan
  - files-first: notable, marktext, zettlr, typora, obsidian
  - ide: vscode-with-ext
  - interactive: jupyter, observablehq
  - offline-first: typora
  - 其他产品参考: pdf标注、电子书epub
# popular
- TiddlyWiki5 /7.5kStar/BSD/202311/js
  - https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/
  - https://tiddlywiki.com/dev/ Developer documentation
  - A self-contained JavaScript wiki for the browser, Node.js, AWS Lambda etc.
  - 笔记数据基本内存，需要导出
  - a non-linear personal web notebook that anyone can use and keep forever
  - It can be used as a single HTML file in the browser or as a powerful Node.js application. 
  - Except of a micro-kernel written in JavaScript the whole application consist of a own data-structure called tiddlers and a own markup language called wikiText. 
  - view层基于tid文件
  - https://github.com/TiddlyWiki/TiddlyWiki
    - the Classic version (2.x.x) of TiddlyWiki
  - https://github.com/TiddlyWiki/TiddlyDesktop /BSD

- joplin /31.9kStar/MIT > AGPLv3/202212/ts/web需付费+pc+mobile
  - https://github.com/laurent22/joplin
  - https://joplinapp.org/
  - note taking and to-do application with synchronization capabilities for Windows, macOS, Linux, Android and iOS
  - 依赖react-redux、sqlite3、@electron/remote、electron-window-state、async-mutex、tinymce.v5【GPL】、codemirror.v5、immer、mark.js、moment、re-resizable、styled-components
  - 笔记数据基于sqlite，可批量导出md
  - [Switch license to AGPL-3.0_20221221](https://joplinapp.org/news/20221221-agpl/)
    - [最后的MIT版本 v2.9.17/v2.10.2](https://github.com/laurent22/joplin/releases/tag/v2.9.17), v2.10.3为AGPL
  - [Why is there no web UI for Joplin?](https://www.reddit.com/r/joplinapp/comments/xjp9zh/why_is_there_no_web_ui_for_joplin/)
    - 不支持web
    - Joplin server has no ability to view/edit notes from the server with a web client.
    - https://github.com/joplin-vieweb/joplin-vieweb

- StandardNotes /4.7kStar/AGPLv3/202401/ts
  - https://github.com/standardnotes/app
  - https://standardnotes.com/
  - an end-to-end encrypted note-taking app
  - An all-in-one personal knowledge base
  - 笔记数据支持sqlite/mysql
  - 提供了多种编辑器，包括代码、markdown
  - markdown-visual-editor基于milkdown，社区还有很多编辑器
    - Standard Notes publishes the source code for its web, desktop, and mobile apps as well as its syncing server and extensions under AGPLv3
  - https://github.com/standardnotes/server
    - 后端依赖express

- notesnook /7.9kStar/GPLv3/202401/js+ts/tiptap
  - https://github.com/streetwriters/notesnook
  - https://notesnook.com/
  - open source & end-to-end encrypted note taking alternative to Evernote.
  - web编辑器和移动端编辑器都依赖tiptap2、zustand、unfurl.js(oembed)、re-resizable、katex
  - @notesnook/streamable-fs: Streaming interface around an IndexedDB based file system
  - Notesnook encrypts everything on your device using XChaCha20-Poly1305 & Argon2.
  - 不支持协作，需要投票
  - 服务端数据同步代码使用c#
  - [Allow for 3rd party syncing](https://github.com/streetwriters/notesnook/issues/168)
    - 202306: 3rd party syncing is out of scope for Notesnook. We will add support for self hosting but that's it.
  - [Formula support in tables _202402](https://github.com/streetwriters/notesnook/issues/4221)

- trilium /17.1kStar/AGPLv3/202208/js/ckeditor5/支持PC+web
  - https://github.com/zadam/trilium
  - https://github.com/zadam/trilium/wiki/
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - 依赖electron、express、jsdom、turndown、ckeditor.v5、codemirror5、jsplumb、fancytree、bootstrap
  - 笔记数据基于sqlite
  - Synchronization with self-hosted sync server
  - Trilium is provided as either desktop application (Linux and Windows) or web application hosted on your server (Linux). 
    - Mac OS desktop build is available, but it is unsupported.
    - If you want to install Trilium on server,currently only recent Chrome and Firefox are supported (tested) browsers.
  - [Notion like database](https://github.com/zadam/trilium/issues/822)
  - [tag system suggest](https://github.com/zadam/trilium/issues/760)
  - [Use interwiki like links to facilitate a long-term proof way to link to file based files _202005](https://github.com/zadam/trilium/issues/1015)
    - I keep thinking about some reasonable ways to integrate with the file system as well - my ideal solution would be to sort of "mount" some directory into trilium 
    - This gets complicated with possible filename conflicts, the fact Trilium also supports versioning etc. In the end it would also create a mess - directory full of files which would need to at least contain some UUID. The benefits compared to just storing them in SQLite get smaller

- simplenote /4.6kStar/GPLv2/202201/ts/inactive/服务端未开源
  - https://github.com/Automattic/simplenote-electron
  - https://simplenote.com/
  - Simplenote for Web, Windows, and Linux
  - import notes from Simplenote(.json) exports, Evernote(.enex) export, Plain text files(.txt)
  - node-simperium for Simperium syncing. 
  - Simplenote API features such as sharing and publishing will not work with development
  - https://github.com/Automattic/simplenote-android
  - https://github.com/Automattic/simplenote-ios
  - [iOS, Android, and macOS Apps Now Open Source _201608](https://simplenote.com/2016/08/11/ios-android-and-macos-apps-now-open-source/)

- notable /22.2kStar/MIT > AGPLv3/201905/ts/桌面版
  - https://github.com/notable/notable
  - https://notable.md/
  - The Markdown-based note-taking app that doesn't suck.
  - 优点: 作者活跃，跨平台读取文件逻辑可复用
  - 不足: 基于文本而不是wysiwyg
  - license
    - `<= v1.3.0` : MIT, 20190131
    - `<= v1.5.1` : AGPLv3, 20190514
    - `>= v1.6.0` : Not Open, 最后一个开源版v1.7.3_201908附带的源码是 v1.5.1
  - [comparison: notable, bear, boostnote, evernote, joplin, keep, notion](https://notable.app/static/images/comparison.png)
  - [Show HN: Notable – A Markdown-based note-taking app that doesn't suck | Hacker News_201812](https://news.ycombinator.com/item?id=18765482)
  - 🍴 forks
  - https://github.com/Eastonboy99/notable /202001/MIT/v1.3
    - https://github.com/lmihalkovic/notable /201902/MIT
    - add RxJS to the dependencies
    - remove CodeMirror and replace it with monaco
  - https://github.com/dps/notable /201901/MIT
    - fork of notable adding built in Google Drive sync, an omnibox and immersive first UI
  - https://github.com/Maxwin-z/notable /201911/AGPLv3
    - feat: allow git sync, try to run sync background
  - https://github.com/bojjenclon/notable /201901/MIT
    - Added statusbar widget with word count and position support
  - https://github.com/nicholasbailey/freenotable /1commit
- https://github.com/meinto/notable-mobile /AGPLv3/201907/ts/react-native
  - a native app inspired by notable/notable
- https://github.com/redsolver/noteless /MIT/202106/dart/inactive
  - markdown-based note-taking app for Android
  - Compatible with notes saved in Notable
- https://github.com/madeindjs/vscode-notable /MIT/202202/ts
  - https://marketplace.visualstudio.com/items?itemName=madeindjs.notable
  - VSCode plugin to take Markdown notes following Notable format.
  - update modified front mater on save note
- https://github.com/DevTomek-pl/Search-Text-Plugin-for-Notable /202004/js
  - a simple JS script for the Notable application that allows you to find a search phrase in the current document.
- https://github.com/fabiospampinato/noty /201901/ts/archived
  - Autosaving sticky note with support for multiple notes without needing multiple windows.
  - Deprecated in favor of Notable
- https://github.com/pavkum/notable-todoist /202106/js/inactive
  - Todoist integration with Notable note talking application.
- https://github.com/andyljones/zonotable /AGPLv3/202105/js/inactive
  - An interface between Zotero's translators and Notable
  - This is a local webserver which makes it easy to add research papers to Notable. This turns Notable into a paper library where note-taking is front and center.
  - Most of the code in this repo comes from Zotero, and in particular it's translation server.
- https://github.com/thinkaliker/note-publish /MIT/202112/js
  - a small Notable.app interceptor to take in a POST request from the "Share via Link..." function and publish a file directly to a Github repository, designed for easy blog posting.
  - This can be run locally or anywhere that can run node.js 

- noteworthy /166Star/AGPLv3/202207/ts/桌面版
  - https://github.com/benrbray/noteworthy
  - https://noteworthy.ink/
  - Markdown editor with bidirectional links and excellent math support
  - 依赖solid-js、remark13、prosemirror、electron-window-state、remark
  - 参考了prosemirror、zettlr、vscode、notable
    - Thanks to Fabio Spampinato for releasing the source to an early version Notable!
- https://github.com/vicjohnson1213/Medley /GPL/202007/inactive
  - 依赖angular7、hightlight.js、marked、monaco-editor、rxjs、subsink、zone.js
  - A tag-based note taking app using Markdown for formatting.
  - I drew some design inspiration (specifically the tag-based organization) from Notable

- siyuan /14.3kStar/AGPLv3/202401/ts/go/支持协作
  - https://github.com/siyuan-note/siyuan
  - https://b3log.org/siyuan/
  - a local-first personal knowledge management system
  - 思源笔记是一款本地优先的个人知识管理系统，支持完全离线使用，同时也支持端到端加密同步。
    - 所有本地功能都是免费的，云端服务需要年付订阅。
    - 不支持网页版，要使用桌面版或移动版
  - SiYuan is made possible by the Vditor and Lute(golang)
  - 用户自己创建的笔记本文件夹下，.sy 后缀的文件用于保存文档数据，数据格式为JSON

- marktext /42.5kStar/MIT/202203/js/vue/inactive
  - https://github.com/marktext/marktext
  - https://www.marktext.cc/
  - simple and elegant markdown editor, available for Linux, macOS and Windows.
  - MarkText uses virtual DOM to render pages
  - 依赖marked.v1、prismjs、electron-store、codemirror.v5、dragula、vue2、vuex、element-ui.v2、snabbdom
  - 不支持添加tag
  - 🆚️ [MarkText + Zettlr _201907](https://github.com/marktext/marktext/issues/1130)
    - Zettlr knowledge management features are what sets it apart from Mark Text
      - Files can have identifiers (the default is a timestamp, but the user can define a custom format using regexp).
      - Zettlr has a syntax to easily type links to other files [[fileId]]. 
      - Support for tags: Zettlr recognizes the typical syntax for hashtags #tag.
    - Mark Text is really just a markdown editor. It will not add the features of note taking, such as tags, metadata, etc. 
  - issues-not-yet
    - [Manage Tags](https://github.com/marktext/marktext/issues/641)
      - Mark Text is a pure markdown editor, there is no storage function, and no notebook function is added
    - [What do you want to do with plugins?](https://github.com/marktext/marktext/issues/375)
      - 现有parser代码仍有扩展上的困难，希望以marked为原型，以插件方式实现每个标记，让每个标记实现rule,renderer
      - marktext 在编辑器内部的渲染不是依赖 marked的，是通过snabbdom 来进行渲染的，所以其是marked 只是提供了block 的解析（不包含inline语法）以及输出markdown 时候会用到（包含block 和 inline 语法）。
    - [Document is modified when opened/Markdown formatting_202006](https://github.com/marktext/marktext/issues/2189)
    - [Mark Text performance improvement](https://github.com/marktext/marktext/issues/511)
  - 🍴 forks
  - https://github.com/jacobwhall/marktext /202401
    - fork of marktext, seeking to modernize our favorite markdown editor
    - Add .mdx extension support
  - https://github.com/mostrub/marktext /202401
  - https://github.com/renerocksai/marktext /202312
  - https://github.com/pencilheart/marktext /202310
  - https://github.com/jgwill/warktext /202311
    - customizable markdown editor, designed for easy distribution across multiple platforms
  - https://github.com/bigshans/marktext /202204
    - 支持了中文，并且修改了主题。
- https://github.com/topabomb/marktext-specialedition /MIT/202302/js
  - marktext0.17.1分叉的中文特别版
  - 增加 Mermaid mindmap的支持
  - 类似于vscode工作区，打开不同的目录可以应用不同的设置
- https://github.com/625781186/marktext2web /201906/js
  - try to make it into a web editor

- Zettlr /9.3kStar/GPLv3/202401/ts/vue/偏学术
  - https://github.com/Zettlr/Zettlr
  - https://www.zettlr.com/
  - https://docs.zettlr.com/
  - Your One-Stop Publication Workbench
  - 依赖electron-forge、codemirror.v6、@lezer/highlight、d3.v7、katex、remark-math、vue3、vuex4、pinia
  - exports with Pandoc, LaTeX, and Textbundle
  - support LaTeX and Word template
  - Citations made easy: Tight and ever-growing integration with your favourite reference manager (Zotero, JabRef, and many others)
  - Support for state of the art knowledge management techniques (Zettelkasten)

- https://github.com/mb21/panwriter /GPLv3/202310/ts
  - https://panwriter.com/
  - 分屏显示源码和预览
  - a distraction-free markdown editor with two unique features
  - Tight integration with pandoc for import/export to/from plenty of file formats (including HTML, docx, LaTeX and EPUB).
  - Preview pane that can show pages – including page breaks etc. Layout adjustments are immediately reflected in the preview.

- yn /3.6kStar/AGPLv3/202501/ts/vue/网页版+桌面版
  - https://github.com/purocean/yn
  - https://yank-note.vercel.app/
  - 一款面向程序员的Markdown笔记应用
  - 使用 vscode-Monaco 内核，专为 Markdown 优化
  - 支持历史版本回溯；可在文档中嵌入小工具、可运行的代码块、表格、PlantUML图形、Drawio图形、宏替换等；支持接入 OpenAI 自动补全。
  - 兼容性强：数据保存为本地Markdown文件；拓展功能尽量用 Markdown 原有的语法实现。
  - 支持用户编写自己的插件来拓展编辑器的功能。
  - 加密文件的加密解密操作均在前端完成，请务必牢记自己的密码。一旦密码丢失，只能暴力破解了。
  - https://github.com/purocean/yank-note-registry /MIT/202401/js
    - Yank Note 扩展的注册中心, fork+pr
  - https://github.com/purocean/yank-note-extension /AGPLv3/ts/vue
    - Yank Note 支持 “JavaScript 插件” 和 “自定义 CSS 样式” 功能。

- BoostNote /3.1kStar/GPLv3/202209/ts/inactive
  - https://github.com/BoostIO/BoostNote-App
  - https://boostnote.io/
  - a document driven project management tool that maximizes remote DevOps team velocity.
  - [v0.9.0_202008](https://github.com/BoostIO/BoostNote-App/pull/595)
    - Implement converting pouchdb based storage to file system based storage

- Serenity Notes /AGPLv3/202401/不支持web
  - https://github.com/SerenityNotes/Serenity
    - End-to-end encrypted collaborative notes
    - [Why is there no web client on the roadmap?](https://www.serenity.re/en/notes/support)
      - We might build one in the future, but first we want to focus on mobile and desktop client.
  - https://github.com/SerenityNotes/serenity-notes-clients
    - Serenity Notes iOS/Android/macOS
    - 依赖prosemirror
    - [Serenity Notes](https://www.serenity.re/en/notes/technical-documentation)
      - end-to-end encryption must using the Olm & Megolm cryptographic ratchets
  - https://github.com/SerenityNotes/serenity-notes-backend
    - End-to-end encrypted collaborative notes app
  - https://github.com/SerenityNotes/naisho
    - architecture to relay end-to-end encrypted CRDTs over a central service.
    - It was created out of the need to have an end-to-end encrypted protocol to allow data synchronization/fetching incl.

- takenote /2.8kStar/MIT/202108/ts/inactive
  - https://github.com/taniarascia/takenote
  - https://takenote.dev/app
  - A free, open-source notes app for the web
  - 依赖react-beautiful-dnd、react-router、@reduxjs/toolkit、redux-saga、react-markdown、axios、codemirror、express、jszip
  - 笔记数据可选local或github
  - The notes are persisted temporarily in `localStorage`, but you can download all notes in markdown format as a zip.
  - Hidden within the code is an alternate version that contain a Node/Express server and integration with GitHub.
  - 👉🏻 What you see is what you paste. No WYSIWYG, no formatting pasted from the web, and no features you don't need or want. 

- https://github.com/bytemakers/Noteslify /GPL/202211/js
  - A Notes Taking Web App Built With Simplicity.
  - Your Privacy Friendly, Open Source. Alternative to EverNote.
  - 编辑器是简单textarea
  - ui界面和后台功能基本实现

- bear-plus /5Star/ISC/202008/js/ejs
  - https://github.com/yk9331/bear-plus
  - https://bear-plus.yenchenkuo.com/@bear-plus/features
  - A web-based writing application with real-time collaboration and Markdown syntax support for crafting and sharing notes. 
  - Inspired by Bear note and HackMD.
  - 依赖codemirror.v5、express、markdown-it、sequelize、express、multer
  - Group and find note easily with hashtag and full text search. 

- https://github.com/0xGG/crossnote-app /1kStar/AGPLv3/202111/ts/inactive
  - https://crossnote.app/
  - markdown notes reader & editor Progressive Web Application that works offline and supports syncing with arbitrary git repository right inside your browser.
  - 依赖isomorphic-git、material-ui.v4、automerge.v0.14、codemirror.v5、d3.v6、graphql、pouchdb、minisearch、tesseract、peerjs

- https://github.com/quillpad/quillpad /GPLv3/202401/kotlin
  - https://quillpad.github.io/
  - a fork of an original app called Quillnote.
  - Take beautiful markdown notes whenever you feel inspired. Place them in notebooks and tag them accordingly. 
  - Stay organized by making task lists, set reminders and keep everything in one place by attaching related files.

- vnote /7.5kStar/MIT/202009/cpp
  - https://github.com/vnotex/vnote
  - 依赖Qt5, turndown, markdown-it
  - a note-taking application that knows programmers and Markdown better.

- https://github.com/giuspen/cherrytree /cpp/python
  - A hierarchical note taking application, featuring rich text and syntax highlighting, storing data in a single XML or SQLite file.

- https://github.com/aardappel/treesheets /cpp
  - https://strlen.com/treesheets/
  - A "hierarchical spreadsheet" that is a great replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

- https://github.com/cybersemics/em /ts/yjs/web/ios/android
  - minimalistic note-taking app for personal sensemaking.
# notes-webapp
- https://github.com/encryptic-team/encryptic /MPLv2/202305/js/deprecated
  - An encryption-focused open source note taking application
  - https://github.com/daed/laverna /MPLv2/201810/js
    - lightweight alternative to Evernote that keeps your notes encrypted.
  - https://github.com/Laverna/laverna /201802
    - a JavaScript note taking application with Markdown editor and encryption support. 
    - Consider it like open source alternative to Evernote.

- https://github.com/notea-org/notea /MIT/202305/ts
  - Self hosted note taking app stored on S3
  - 依赖自己维护的@notea/rich-markdown-editor
  - Support storage in Amazon S3, MinIO, Aliyun OSS, etc
  - Why not use Database? the data stored in Notea is mainly files (such as text or pictures) but the database is not good at reading and writing these type of files; S3 can generate a signed URL to access the remote files, but the database cannot do it.
  - Why not use filesystem storage? I couldn't find an APP that supports both self-hosted and easy to manage the synchronized data

- https://github.com/batnoter/batnoter /MIT/202210/ts/inactive
  - https://batnoter.com/
  - open source, markdown-based, self-hosted note taking webapp.
  - https://github.com/batnoter/batnoter-api /go

- https://github.com/treehousedev/treehouse /MIT/202308/ts/Mithril/inactive
  - https://treehouse.sh/
  - open source note-taking frontend to extend and customize. 
  - Bring your own backend or configure a built-in backend to get started.
  - Treehouse is a frontend written in TypeScript made to be rendered in a browser or webview
  - It is a "thick" frontend in that it holds most application state in-memory and executes user triggered commands to mutate that state.
  - Even without a backend adapter, the Treehouse frontend is still a fully functional application packaged as a JavaScript library that can be loaded onto any HTML page.
  - Outline editor and repurposable workspace shell.
  - Minimal dependencies, mainly Mithril.js, codemirror
  - Built with Deno toolchain. Zero Node.js utilization.
  - By default, data is stored in your browser’s `localStorage`.
  - If you choose to log in with GitHub, we’ll create a repository and store your data there.
  - The Treehouse frontend uses its backend adapter to store the state of your workspace into a JSON document. 
  - The "document" for Treehouse is the Workspace, which is mostly a container for nodes. nodes build a tree-like structure where each node can be extended with components. 
  - Treehouse will index your workspace for full-text search using Minisearch

- https://github.com/dullage/flatnotes /MIT/202312/ts/vue
  - https://demo.flatnotes.io/
  - A self-hosted, database-less note-taking web app that utilises a flat folder of markdown files for storage.
  - No folders, notebooks or anything like that. Just all of your notes, backed by powerful search and tagging functionality.
  - Log into the demo site and take a look around. Note: This site resets every 15 minutes.
  - Wikilink support to easily link to other notes (`[[My Other Note]]`).
  - TOAST UI Editor 

- https://github.com/penxio/penx /AGPLv3/202401/ts
  - A structured note-taking app for personal use
  - Privacy-First - Use End-To-End Encryption to sync data
  - Version control - GitHub-Based Version control Out-of-box
  - 依赖tRPC、Prisma、Next.js、NextAuth、Slate.js、IndexedDB
# notes-apps
- https://github.com/tagspaces/tagspaces /3.3kStar/AGPLv3/202401/ts
  - https://www.tagspaces.org/
  - an offline, open source, document manager with tagging support
  - no backend, no login, file manager, organizer and browser
  - available for Windows, Linux, Mac OS and Android. 
  - provide a web clipper extension for Firefox, Edge and Chrome
  - supports two ways for tagging files. The default one embeds the tags directly in the name of the file, the other one uses a so called sidecar files for persisting the tags.
  - has integrated basic media player functionalities.
  - does not require an internet connection and any kind of online registration or service provider.
  - Note Taking - you can create and edit notes in plain text, markdown and html file formats
  - [Unable to use local folder on Self hosted Web version _202311](https://github.com/tagspaces/tagspaces/issues/2000)
    - The web version support location pointing to object storage (AWS S3, minio, S3proxy, Wasabi, R2) only
    - Yes it is technical, TagSpaces is a front-end application, which can connect to S3 back ends. For you use case you can use S3Proxy to expose a shared folder for example on a NAS and connect it with TagSpaces as S3 location.
  - https://github.com/tagspaces/tagspaces-extensions /MIT/202404/js
    - This repository contains the viewer and editor extensions delivered by default with TagSpaces products.

- https://github.com/codexu/note-gen /MIT/202505/ts
  - https://codexu.github.io/note-gen/
  - a cross-platform Markdown note-taking application dedicated to using AI to bridge recording and writing, organizing fragmented knowledge into a readable note.
  - Cross-platform: Supports Mac, Windows, Linux, and thanks to Tauri2
  - Native offline usage with Markdown(.md) as the storage format, while also supporting real-time synchronization to private GitHub repositories with history rollback.
  - AI-enhanced: Configurable with ChatGPT, Gemini, Ollama, LM Studio, DeepSeek, and other models, with support for custom third-party model configuration.
# notes-browser-extensions
- note-it /16Star/apache2/202412/ts/tiptap
  - https://github.com/MuhametSmaili/note-it
  - https://www.youtube.com/watch?v=jxBAMwxbk78
  - NoteIt is a feature-packed, note-taking extension with OCR support for chrome.
  - 支持截图及批注
  - 依赖React、Tiptap、tesseract.js、pdfmake、html-to-pdfmake
  - You can take notes, convert images to text, download notes to pdf, and more.

- placenoter /30Star/MIT/202211/ts
  - https://github.com/sereneinserenade/placenoter
  - This extension replaces your new tab with a note taking app
  - 依赖dnd-kit、tiptap
  - 支持写笔记和添加链接

- my-notes /198Star/MIT/202211/ts
  - https://github.com/penge/my-notes
  - note-taking in Chrome with Google Drive support.
  - Chrome extension for simple and fast note-taking
  - Back up notes to Google Drive; Auto Sync notes to Google Drive
  - Drag and drop image with automatic image upload to Google Drive
  - Works offline

- https://github.com/mpkelly/journal
  - https://mpkelly.github.io/journal
  - Embeddable Wiki available as Chrome extension, PWA or React component.
  - 依赖slate二开、dexie3

- mdtab /8Star/MIT/202209/ts
  - https://github.com/shaoruu/mdtab
  - Write quick notes in Markdown on any new tabs!
  - Save to local storage/browser sync
  - Vim mode

- https://github.com/wizardion/chrome-notes /202201/ts/非tab而是弹出框
  - Work-Note - save your notes where you are. 

- https://github.com/braydenwerner/Atlas /202203/ts
  - A comprehensive tool for drawing, taking notes, and staying organized all on your chrome homepage.

- https://github.com/plibither8/markdown-new-tab /202101/js
  - https://mdnt.mihir.ch/
  - Take down notes spiral_notepad, save reminders alarm_clock, paste links link, create checklists ballot_box_with_check or tables, all using markdown... directly in your 'New Tab' page! 

- https://github.com/wildskyf/tab-notes /202203/js
  - Open new tab and write anything.

- https://github.com/qiweiii/markdown-sticky-notes /202110/js
  - Auto save content and position
  - I am using Manifest version 2, because version 3 is new and doc is not complete and not much tutorials exist yet, but i will switch to MV3 later on.

- https://github.com/chenzhiwei/chrome-markdown-editor /202202/js/自用
  - A Github Flavored Markdown Editor.
  - Repackage of markdown-editor with some modifications
  - 不支持多文件

- https://github.com/simov/markdown-viewer /202101/js/自用
  - Markdown Viewer/Browser Extension
  - Full control over the compiler options (marked or remark)
  - Renders local and remote URLs

- https://github.com/volca/markdown-preview /202207/js
  - Markdown Preview Plus -- Enables Chrome to render markdown files as HTML

- https://github.com/md-reader/md-reader /202210/ts
  - A markdown reader extension for Chrome.

- https://github.com/kbravh/table-to-markdown /202101/js
  - convert an HTML Table to Markdown for easy export.

- https://github.com/zhuowenli/githuber /202011/js/vue
  - 帮助 GitHub 开发者每日发现优质内容的浏览器主页拓展。

- https://github.com/WorldBrain/Memex /4.2kStar/MIT/202311/ts
  - https://worldbrain.io/
  - Browser extension to curate, annotate, and discuss the most valuable content and ideas on the web
  - Its name and functionalities are heavily inspired by Vannevar Bush's vision of a Memex.

## more-note-editor

- https://github.com/deathau/markdownload /202210/js
  - an extension to clip websites and download them into a readable markdown file. 
  - Turndown is used to convert the simplified HTML (from Readability.js) into markdown.

- https://github.com/m19e/memorandum /202007/ts
  - Chrome/Edge Extension: Memorandum provides Markdown WYSIWYG Editor.

- https://github.com/mpkelly/journal
  - Embeddable Wiki available as Chrome extension, PWA or React component.

- https://github.com/hediet/browser-ext-github-monaco
  - Chrome/Firefox extension brings the famous Monaco editor to GitHub!
  - This extension replaces all GitHub text areas for authoring markdown with a monaco editor.
  - 替换issues编辑器

- https://github.com/willklein/markdown-menu
  - for github readme.md, This extension will automagically generate and add navigation menu with a table of contents.

- https://github.com/lvxianchao/confluence-markdown-editor /202207/js
  - 为 Confluence Wiki 页面提供一个 Markdown 编辑器。

- https://github.com/siebevd/Moment
  - simple chrome new tab extension combining notes with pictures

- https://github.com/shuowu/yi-note /202110/js
  - YiNote, aka TurboNote Chrome Extension, is an effective tool to take and share notes while watching online videos.
  - Take time-stamped note while watching online video, currently supported video formats/platform: youtube/html5-video
  - Send notes to popular note platforms:google-docs/evernote
- https://github.com/ahmedelq/NattyNote
  - Take time-stamped YouTube notes
- https://github.com/hidao80/fast-logbook
  - Time-stamped work notes Chrome Extension

- https://github.com/dfhoughton/amanuensis
  - This project is a browser extension to facilitate taking notes on web pages. It was originally conceived as a language learning aid

- https://github.com/KeithLRobertson/markdown-viewer
  - Markdown (.md file) Viewer WebExtension for firefox

## non-open

- TabNotes
  - https://chrome.google.com/webstore/detail/tabnotes/omgomlnnfccahaaicaphjjgkjplfkjai
  - https://github.com/bansal-io

- OFFLINE-NOTE
  - https://chrome.google.com/webstore/detail/offline-note/naobhcifpdffdokgdboppeldefdnooic
# obsidian
- obsidian dataview /5.8kStar/MIT/202312/ts
  - https://github.com/blacksmithgu/obsidian-dataview
  - https://blacksmithgu.github.io/obsidian-dataview/
  - A high-performance data index and query language over Markdown files, for obsidian
  - Treat your Obsidian Vault as a database which you can query from. 
  - Provides a JavaScript API and pipeline-based query language for filtering, sorting, and extracting data from Markdown pages.
  - **Dataview generates data from your vault by pulling information from Markdown frontmatter and Inline fields**.
  - Markdown frontmatter is arbitrary YAML enclosed by `---` at the top of a markdown document which can store metadata about that document.
  - Inline fields are a Dataview feature which allow you to write metadata directly inline in your markdown document via `Key:: Value` syntax.
  - [Obsidian Dataview: Turn Obsidian Vault into a database you can query from | Hacker News_202205](https://news.ycombinator.com/item?id=31407781)
  - https://github.com/obsidianmd/obsidian-releases
    - Obsidian is not open source software and this repo DOES NOT contain the source code of Obsidian. 
    - However, if you wish to contribute to Obsidian, you can easily do so with our extensive plugin system.
  - https://github.com/blacksmithgu/datacore /MIT
    - Datacore is a work-in-progress re-imagining of Dataview with a focus on 2-10x better query and rendering performance, as well as fully interactible views.
    - Datacore is fundamentally the same thing as dataview - an index over Markdown files that supports live-updating views and metadata. 
    - However, Datacore focuses on substantial index changes for performance, as well as a new sleek UI which completely replaces traditional Dataview queries. 
    - Datacore supports all query operations that Dataview does, with some extra functionality.
    - WYSIWYG Views: Datacore queries now use a responsive table view and can be manipulated with a table editor much more akin to what you would see in places like Notion and Airtable.
    - Live Editing: Values inside of table views can now be edited; task views include more nuanced rendering of metadata like due date and more operations for manipulating tasks directly.
    - Live Editing: Values inside of table views can now be edited; task views include more nuanced rendering of metadata like due date and more operations for manipulating tasks directly.
  - https://github.com/RafaelGB/obsidian-db-folder
    - Obsidian Plugin to Allow Notion like database based on folders
  - https://github.com/s-blu/obsidian_dataview_example_vault /202311
    - https://s-blu.github.io/obsidian_dataview_example_vault/
    - A example vault to collect and showcase various dataview queries
    - the vault is deployed as a mkdocs page: Online Version of the Obsidian Example Vault

- https://github.com/mgmeyers/obsidian-kanban /GPLv3/202309/ts
  - https://publish.obsidian.md/kanban/
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/obsidian-tasks-group/obsidian-tasks /MIT/202401/ts
  - https://publish.obsidian.md/tasks/
  - Task management for the Obsidian knowledge base.
  - Track tasks across your entire vault. Query them and mark them as done wherever you want. 
  - Supports due dates, recurring tasks (repetition), done dates, sub-set of checklist items, and filtering.

- https://github.com/trey-wallis/obsidian-dataloom /MPLv2/202401/ts
  - https://dataloom.xyz/
  - DataLoom is an Obsidian.md plugin for desktop and mobile. 
  - It allows you to create databases similar to Notion.so.
  - Inspired by Excel spreadsheets and Notion.so.

- https://github.com/scambier/obsidian-omnisearch /GPLv3/202401/ts/svelte
  - A search engine that "just works" for Obsidian. 
  - Includes OCR and PDF indexing. Images OCR and PDF indexing are only available on desktop
  - it uses the excellent `MiniSearch` library.
  - Automatic document scoring using the BM25 algorithm
  - Note: support of Chinese, Japanese, Korean, etc. depends on https://github.com/aidenlx/cm-chs-patch

- https://github.com/vrtmrz/obsidian-livesync /2.8kStar/MIT/202401/ts
  - 社区实现的在线同步插件
  - 注意: 本插件与官方的 "Obsidian Sync" 服务不兼容。
  - 接近实时的多设备双向同步
  - 可使用 CouchDB 以及兼容的服务，如 IBM Cloudant
  - 支持端到端加密
  - 插件同步 (Beta)
  - 从 obsidian-livesync-webclip 接收 WebClip (本功能不适用端到端加密)
  - 请勿与其他同步解决方案（包括 iCloud、Obsidian Sync）一起使用。在启用此插件之前，请确保禁用所有其他同步方法以避免内容损坏或重复。
  - [Obsidian 各种同步方式体验](https://irithys.com/obsidian-sync-exp/)
    - 我使用中认为体验最好的同步方式，但是缺点是不能当做备份使用。所以 Webdav 同步方案依然存在一定的价值
  - https://github.com/kkbt0/obcsapi-go /MIT/202403/go/vue
    - 基于 WebDAV，S3 存储或 CouchDb 的后端 API ，Obsidian 笔记的 API
    - 可借助 Obsidian 插件 Remotely-Save 插件，或者 Self-hosted LiveSync (ex:Obsidian-livesync) 插件 CouchDb 方式，保存消息到 Obsidian 库
    - 一个简易图床，附带命令行上传工具

- https://github.com/remotely-save/remotely-save /apache2/202401/ts
  - Yet another unofficial Obsidian plugin allowing users to synchronize notes between local device and the cloud service. 
  - Supports S3, Dropbox, OneDrive, webdav.
  - Vaults can be synced across mobile and desktop devices with the cloud service as the "broker".
  - End-to-end encryption supported.
  - Scheduled auto sync supported. 
  - Sync Algorithm open for discussion.
  - No Conflict resolution. No content-diff-and-patch algorithm. All files and folders are compared using their local and remote "last modified time" and those with later "last modified time" wins.
  - [Is this project abandoned?_202304](https://github.com/remotely-save/remotely-save/issues/280)
    - Admittedly I was too busy and too lazy to update the plugin in the past few years
    - livesync and obsidian-git doesn't meet my needs because the first one needs a db server and the second one is too complicated for non-tech. 
  - [被 Remotely Save 劝退：：木木木木木](https://immmmm.com/off-remotely-save/)
    - 同步机制没有 “文件保存触发同步” 不够 “丝滑”；
    - 定时同步时有一串（8 条）通知条，同步后笔记还会 “闪烁”（重载）一下，不够 “无感”；
    - 同步冲突以文件的最后时间为准，而非 “局部增量” 同步，若多端在 “定时同步” 时间间隔内对同一文件进行操作，那就直接错乱

- https://github.com/denolehov/obsidian-git /MIT/202401/ts
  - Plugin that allows you to back up your Obsidian.md vault to a remote Git repository (e.g. private repo on GitHub).
  - Automatic vault backup every X minutes
  - Pull changes from remote repository on Obsidian startup

- https://github.com/acheong08/obi-sync /GPLv2/202312/go
  - Reverse engineering of the native Obsidian sync and publish server
  - The plugin is broken on obsidian >= 1.4.11. This is intentional by the official ObsidianMD team. They have made clear their dissatisfaction with this project. 
  - We are in the early stages of designing an alternative plugin that does not make use of existing code by ObsidianMD team.
  - [Show HN: Open-source obsidian.md sync server | Hacker News_202308](https://news.ycombinator.com/item?id=37247767)
    - Obsidian is a small company, we're not VC backed (100% user-supported), so the Sync pricing helps us stay in business and keep the lights on. 

- https://github.com/gamosoft/NoteDiscovery /MIT/202511/python/js
  - a lightweight, self-hosted note-taking application, all running on your own server.
  - [NoteDiscovery: New free and open source self hosted alternative to Obsidian : r/selfhosted _202511](https://www.reddit.com/r/selfhosted/comments/1opxmud/notediscovery_new_free_and_open_source_self/)
    - For now allows markdown editing, automatic saving, undo/redo, custom themes, plugins (basic support for now)...
# zotero
- https://github.com/zotero/zotero /8.6kStar/AGPLv3/202401/js
  - https://www.zotero.org/
  - a free, easy-to-use tool to help you collect, organize, cite, and share your research sources.
  - [Zotero is built on Firefox and depends on many other exceptional open-source projects](https://www.zotero.org/support/credits_and_acknowledgments):
    - [ace](https://ace.c9.io/)
    - Monaco Editor
    - ProseMirror
    - pdf.js
    - katex
    - Citation Style Language
    - epub.js
  - https://github.com/windingwind/zotero-better-notes /AGPLv3/202401/ts
    - 📝 Everything about note management. All in Zotero.
    - a plugin for Zotero.
    - Keep in sync with your Markdown files. Two-way, automatically
  - https://github.com/windingwind/zotero-pdf-translate /AGPLv3/202401/ts
    - Translate PDF, EPub, webpage, metadata, annotations, notes to the target language. 
    - Support 20+ translate services.
  - https://github.com/argenos/zotero-mdnotes /GPLv3/202103/js
    - A Zotero plugin to export item metadata and notes as markdown files.
  - [Zotero 6 | Hacker News _202203](https://news.ycombinator.com/item?id=30714121)
    - Zotero has a novel build system where instead of using XULRunner, which is no longer available, the build scripts download a release version of Firefox and then replace the browser-specific modules and other assets with Zotero's bundle.
  - [Zotero: Free, easy-to-use tool to collect, organize, cite, and share research | Hacker News _202201](https://news.ycombinator.com/item?id=29774097)
    - Zotero is a plug-in for the Firefox Web browser

- https://github.com/dvanoni/notero /MIT/202401/ts
  - a Zotero plugin for syncing items and notes into Notion. 
  - The Notero plugin watches for Zotero items being added to or modified within any collections that you specify in the Notero preferences. 

- https://github.com/Future-Scholars/paperlib /GPL/202412/ts/vue
  - https://paperlib.app/
  - An open-source academic paper management tool.
  - Why not Zotero, Mendely? A good metadata scraping capability is one of the core functions of a paper management tool. Unfortunately, no software in this world does this well, not even commercial software.
  - Scrape paper’s metadata with many scrapers. Support writing your metadata scrapers. Tailored for many disciplines.
# note-ai
- https://github.com/reorproject/reor /8.2kStar/AGPL/202505/ts/inactive
  - https://reorproject.org/
  - Private & local AI personal knowledge management app for high entropy((熵(平均信息量))) people.
  - an AI-powered desktop note-taking app: it automatically links related notes, answers questions on your notes and provides semantic search.
  - Everything is stored locally and you can edit your notes with an Obsidian-like markdown editor.
  - The hypothesis of the project is that AI tools for thought should run models locally by default. 
  - Reor stands on the shoulders of the giants Ollama, Transformers.js & LanceDB to enable both LLMs and embedding models to run locally
  - Reor interacts directly with Ollama which means you can download and run models locally right from inside Reor.
  - Reor works within a single directory in the filesystem. You choose the directory on first boot.
# note-android
- https://github.com/gsantner/markor /apache2/202503/java
  - Text editor - Notes & ToDo (for Android) - Markdown, todo.txt, plaintext, math, ..
# note-mac/ios
- https://github.com/glushchenko/fsnotes /MIT/202503/swift
  - modern notes manager for macOS and iOS.
  - Markdown-first. Also supports any plaintext files.
# note-utils
- graph /7Star/MIT/202210/ts
  - https://github.com/graphcentral/graph
  - https://graphcentral.github.io/graph
  - Performant graph visualization on the web with WebGL + Webworkers + IndexedDB
  - You can visualize Notion pages on force layout graph using this library
# note-encryption
- https://github.com/harshsbhat/sealnotes /MIT/202412/ts
  - https://sealnotes.com/
  - Open-source lightweight encrypted notepad
  - End-to-End Encryption: Your text is encrypted using AES-256 before being stored on our servers, and even the name of your notepad is securely hashed before being saved in our database.
  - No Account Required: Access your notes using a unique URL and password combination.
# more-note-app
- https://github.com/codex-team/codex.notes /79Star/MIT/202009/js/inactive
  - crossplatform desktop notes application based on Electron and Editor.js

- codimd /8kStar/AGPLv3/202401/js
  - https://github.com/hackmdio/codimd
  - Realtime collaborative markdown notes on all platforms.
  - HackMD helps developers write better documents and build active communities with open collaboration
  - CodiMD is the free software version of HackMD, developed by the HackMD team with reduced features (without book mode)
- https://github.com/hedgedoc/hedgedoc
  - HedgeDoc (formerly known as CodiMD) is an open-source, web-based, self-hosted, collaborative markdown editor.
  - [Proposal: Replace OT with CRDTs](https://github.com/hedgedoc/hedgedoc/issues/527)
    - By using y.js we are using CRDTs now.

- https://github.com/FoxUSA/OpenNote /201802/js/inactive
  - built to be an open web-based alternative to Microsoft OneNote(T) and EverNote.
  - OpenNote is a progressive web application(PWA)/HTML5 offline app, web based text editor/note taking software
  - 依赖angular.v1、pouchdb、jquery
  - This project has received the kiss of death. That is, I myself don't use it anymore. I have switched to using a text editor with markdown support, Git, and Syncthing for my journaling/note taking.

- https://github.com/gsantner/markor /apache2/java
  - a TextEditor for Android.
  - utilizes simple markup formats like Markdown and todo.txt for note-taking and list management
  - Created files are interoperable with any other plaintext software on any platform. 
