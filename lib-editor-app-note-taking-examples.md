---
title: lib-editor-app-note-taking-examples
tags: [app, cross-platform, examples, note-taking, toc]
created: 2020-10-22T09:55:31.796Z
modified: 2023-02-05T18:05:44.122Z
---

# lib-editor-app-note-taking-examples

# guide
- note-taking solutions
  - web first
  - offline first

- 开发桌面版和vscode扩展的区别
# popular
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

- notesnook /2.8kStar/GPLv3/202209/js+ts/tiptap
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

- Standard Notes /3.6kStar/AGPLv3/202208/ts
  - https://github.com/standardnotes/app
  - https://standardnotes.com/
  - an end-to-end encrypted note-taking app
  - An all-in-one personal knowledge base
  - 提供了多种编辑器，包括代码、markdown
  - markdown-visual-editor基于milkdown，社区还有很多编辑器
    - Standard Notes publishes the source code for its web, desktop, and mobile apps as well as its syncing server and extensions under AGPLv3
  - https://github.com/standardnotes/server
    - 后端依赖express

- notable /16.4kStar/MIT > AGPLv3/202007/ts/桌面版
  - https://github.com/notable/notable
  - https://notable.md/
  - The Markdown-based note-taking app that doesn't suck.
  - 优点: 作者活跃，跨平台读取文件逻辑可复用
  - 不足: 基于文本而不是wysiwyg
  - license
    - `<= v1.3.0` : MIT, 20190131
    - `<= v1.5.1` : AGPLv3, 20190514
    - `>= v1.6.0` : Not open-source
  - [product comparison: notable, bear, boostnote, evernote, joplin, keep, notion](https://notable.app/static/images/comparison.png)
- https://github.com/lmihalkovic/notable /MIT
  - https://github.com/Eastonboy99/notable /v1.3
- https://github.com/dps/notable /MIT
  - fork of notable adding built in Google Drive sync, an omnibox and immersive first UI
- https://github.com/DevTomek-pl/Search-Text-Plugin-for-Notable
  - a simple JS script for the Notable application that allows you to find a search phrase in the current document.
- https://github.com/fabiospampinato/noty
  - Autosaving sticky note with support for multiple notes without needing multiple windows.
  - Deprecated in favor of Notable
- https://github.com/fabiospampinato/electron-about
  - Simple standalone about window for Electron.
- notable-agpl
  - https://github.com/Maxwin-z/notable
  - https://github.com/nicholasbailey/freenotable
  - https://github.com/benrbray/noteworthy

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

- siyuan /6.6kStar/AGPLv3/202208/ts/go/支持协作
  - https://github.com/siyuan-note/siyuan
  - https://b3log.org/siyuan/
  - a local-first personal knowledge management system
  - 思源笔记是一款本地优先的个人知识管理系统，支持完全离线使用，同时也支持端到端加密同步。
    - 所有本地功能都是免费的，云端服务需要年付订阅。
    - 不支持网页版，要使用桌面版或移动版
  - SiYuan is made possible by the Vditor and Lute(golang)
  - 用户自己创建的笔记本文件夹下，.sy 后缀的文件用于保存文档数据，数据格式为JSON

- yn /3.6kStar/AGPLv3/202208/ts/vue/网页版+桌面版
  - https://github.com/purocean/yn
  - https://yank-note.vercel.app/
  - 一款面向程序员的Markdown笔记应用
  - 使用 vscode-Monaco 内核，专为 Markdown 优化
  - 支持历史版本回溯；可在文档中嵌入小工具、可运行的代码块、表格、PlantUML图形、Drawio图形、宏替换等；支持接入 OpenAI 自动补全。
  - 兼容性强：数据保存为本地Markdown文件；拓展功能尽量用 Markdown 原有的语法实现。
  - 支持用户编写自己的插件来拓展编辑器的功能。
  - 加密文件的加密解密操作均在前端完成，请务必牢记自己的密码。一旦密码丢失，只能暴力破解了。

- joplin /31.9kStar/MIT > AGPLv3/202209/ts/web需付费+pc+mobile
  - https://github.com/laurent22/joplin
  - https://joplinapp.org/
  - note taking and to-do application with synchronization capabilities for Windows, macOS, Linux, Android and iOS
  - [Switch license to AGPL-3.0_202212](https://joplinapp.org/news/20221221-agpl/)
  - [Why is there no web UI for Joplin?](https://www.reddit.com/r/joplinapp/comments/xjp9zh/why_is_there_no_web_ui_for_joplin/)
    - 不支持web
    - Joplin server has no ability to view/edit notes from the server with a web client.
    - https://github.com/joplin-vieweb/joplin-vieweb

- https://github.com/zotero/zotero /8.6kStar/AGPLv3/202401/js
  - https://www.zotero.org/
  - a free, easy-to-use tool to help you collect, organize, cite, and share your research sources.
  - Zotero is built on Firefox and depends on many other exceptional open-source projects:
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

- BoostNote /3.1kStar/GPLv3/202209/ts/inactive
  - https://github.com/BoostIO/BoostNote-App
  - https://boostnote.io/
  - a document driven project management tool that maximizes remote DevOps team velocity.
  - [v0.9.0_202008](https://github.com/BoostIO/BoostNote-App/pull/595)
    - Implement converting pouchdb based storage to file system based storage

- Serenity Notes /不支持web
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

- https://github.com/bytemakers/Noteslify /GPL/202211/js
  - A Notes Taking Web App Built With Simplicity.
  - Your Privacy Friendly, Open Source. Alternative to EverNote.
  - 编辑器是简单textarea
  - ui界面和后台功能基本实现

- takenote /2.8kStar/MIT/202108/ts/inactive/数据可选local或github
  - https://github.com/taniarascia/takenote
  - https://takenote.dev/app
  - 依赖react-beautiful-dnd、react-router、@reduxjs/toolkit、redux-saga、react-markdown、axios、codemirror、express、jszip
  - A free, open-source notes app for the web
  - The notes are persisted temporarily in local storage, but you can download all notes in markdown format as a zip.
  - Hidden within the code is an alternate version that contain a Node/Express server and integration with GitHub.
  - 👉🏻 What you see is what you paste. No WYSIWIG, no formatting pasted from the web, and no features you don't need or want. 

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

- vnote /7.5kStar/MIT/202009/cpp
  - https://github.com/vnotex/vnote
  - 依赖Qt5, turndown, markdown-it
  - a note-taking application that knows programmers and Markdown better.

- https://github.com/giuspen/cherrytree /cpp/python
  - A hierarchical note taking application, featuring rich text and syntax highlighting, storing data in a single XML or SQLite file.

- https://github.com/aardappel/treesheets /cpp
  - https://strlen.com/treesheets/
  - A "hierarchical spreadsheet" that is a great replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

- https://github.com/treehousedev/treehouse
  - open source note-taking frontend to extend and customize. 
  - Bring your own backend or configure a built-in backend to get started.
  - Outline editor and repurposable workspace shell.
  - Minimal dependencies, mainly Mithril.js.
  - Built with Deno toolchain. Zero Node.js utilization.

- https://github.com/cybersemics/em /ts/yjs/web/ios/android
  - minimalistic note-taking app for personal sensemaking.
# note-browser-extensions
- note-it /16Star/Apache2/202208/ts/tiptap
  - https://github.com/MuhametSmaili/note-it
  - https://www.youtube.com/watch?v=jxBAMwxbk78
  - 支持截图及批注
  - NoteIt is a feature-packed, note-taking extension with OCR support for chrome.
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

- https://github.com/mgmeyers/obsidian-kanban /GPLv3/202309/ts
  - https://publish.obsidian.md/kanban/
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/obsidian-tasks-group/obsidian-tasks /MIT/202401/ts
  - https://publish.obsidian.md/tasks/
  - Task management for the Obsidian knowledge base.
  - Track tasks across your entire vault. Query them and mark them as done wherever you want. 
  - Supports due dates, recurring tasks (repetition), done dates, sub-set of checklist items, and filtering.


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
  - https://github.com/kkbt0/obcsapi-go /MIT/202401/go/vue
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
# note-utils
- graph /7Star/MIT/202210/ts
  - https://github.com/graphcentral/graph
  - https://graphcentral.github.io/graph
  - Performant graph visualization on the web with WebGL + Webworkers + IndexedDB
  - You can visualize Notion pages on force layout graph using this library
# more-note-app
- simplenote-electron /4.1kStar/GPLv2/202201/ts/inactive
  - https://github.com/Automattic/simplenote-electron
  - https://simplenote.com/
  - Simplenote for Web, Windows, and Linux
  - import notes from Simplenote(.json) exports, Evernote(.enex) export, Plain text files(.txt)
  - node-simperium for Simperium syncing. 服务端未开源
  - Simplenote API features such as sharing and publishing will not work with development
  - ref
    - https://github.com/Automattic/simplenote-android
    - https://github.com/Automattic/simplenote-ios

- https://github.com/codex-team/codex.notes
  - /79Star/MIT/202009/js
  - crossplatform desktop notes application based on Electron and Editor.js

- https://github.com/0xGG/crossnote
  - /404Star/AGPLv3/202009/ts
  - markdown notes reader & editor Progressive Web Application that works offline and supports syncing with arbitrary git repository right inside your browser
  - https://github.com/0xGG/vscode-crossnote

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
