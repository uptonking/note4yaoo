---
title: toc-app-note-taking
tags: [app, note-taking]
created: 2020-10-22T09:55:31.796Z
modified: 2020-10-22T10:03:50.526Z
---

# toc-app-note-taking

# guide
- notes-solutions
# popular
- TiddlyWiki5 /6.9kStar/BSD/202209/ts
  - https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/dev/
  - A self-contained JavaScript wiki for the browser, Node.js, AWS Lambda etc.
  - view层基于tid文件

- Standard Notes /3.6kStar/AGPL.v3/202208/ts
  - https://github.com/standardnotes/app
  - https://standardnotes.com/
  - an end-to-end encrypted note-taking app
  - An all-in-one personal knowledge base
  - 提供了多种编辑器，包括代码、markdown
  - https://github.com/standardnotes/server
    - 后端依赖express

- notesnook /2.8kStar/GPL.v3/202209/js+ts/tiptap
  - https://github.com/streetwriters/notesnook
  - https://notesnook.com/
  - open source & end-to-end encrypted note taking alternative to Evernote.
  - web编辑器和移动端编辑器都依赖tiptap2、zustand、unfurl.js(oembed)、re-resizable、katex
  - @notesnook/streamable-fs: Streaming interface around an IndexedDB based file system
  - Notesnook encrypts everything on your device using XChaCha20-Poly1305 & Argon2.
  - 服务端数据同步代码未找到

- notable /16.4kStar/MIT > AGPLv3/202007/ts/桌面版
  - https://github.com/notable/notable
  - https://notable.md/
  - The Markdown-based note-taking app that doesn't suck.
  - license
    - `<= v1.3.0` : MIT 
    - `<= v1.5.1` : AGPLv3
    - `>= v1.6.0` : Not open-source
    - v1.0.0..v1.3.0: These initial releases have been published under MIT
    - v1.4.0..v1.5.1: These later releases have been published under AGPL-v3
    - The source code for newer versions of the app is unavailable
  - [product comparison: notable, bear, boostnote, evernote, joplin, keep, notion](https://notable.app/static/images/comparison.png)

- noteworthy /166Star/AGPL.v3/202207/ts/桌面版
  - https://github.com/benrbray/noteworthy
  - https://noteworthy.ink/
  - Markdown editor with bidirectional links and excellent math support
  - 依赖solid-js、remark13、prosemirror、electron-window-state、remark
  - 参考了prosemirror、zettlr、vscode、notable
    - Thanks to Fabio Spampinato for releasing the source to an early version Notable!

- siyuan /6.6kStar/AGPL.v3/202208/ts/go/支持协作
  - https://github.com/siyuan-note/siyuan
  - https://b3log.org/siyuan/
  - a local-first personal knowledge management system
  - 思源笔记是一款本地优先的个人知识管理系统，支持完全离线使用，同时也支持端到端加密同步。
    - 所有本地功能都是免费的，云端服务需要年付订阅。
    - 不支持网页版，要使用桌面版或移动版
  - SiYuan is made possible by the Vditor and Lute(golang)
  - 用户自己创建的笔记本文件夹下，.sy 后缀的文件用于保存文档数据，数据格式为JSON

- yn /3.6kStar/AGPL.v3/202208/ts/vue/网页版+桌面版
  - https://github.com/purocean/yn
  - https://yank-note.vercel.app/
  - 一款面向程序员的Markdown笔记应用
  - 使用 vscode-Monaco 内核，专为 Markdown 优化
  - 支持历史版本回溯；可在文档中嵌入小工具、可运行的代码块、表格、PlantUML图形、Drawio图形、宏替换等；支持接入 OpenAI 自动补全。
  - 兼容性强：数据保存为本地Markdown文件；拓展功能尽量用 Markdown 原有的语法实现。
  - 支持用户编写自己的插件来拓展编辑器的功能。
  - 加密文件的加密解密操作均在前端完成，请务必牢记自己的密码。一旦密码丢失，只能暴力破解了。

- joplin /31.9kStar/MIT/202209/ts/web需付费+pc+mobile
  - https://github.com/laurent22/joplin
  - https://joplinapp.org/
  - note taking and to-do application with synchronization capabilities for Windows, macOS, Linux, Android and iOS

- BoostNote /3.1kStar/GPLv3/202209/ts
  - https://github.com/BoostIO/BoostNote-App
  - https://boostnote.io/
  - a document driven project management tool that maximizes remote DevOps team velocity.

- vnote /7.5kStar/MIT/202009/cpp
  - https://github.com/vnotex/vnote
  - 依赖Qt5, turndown, markdown-it
  - a note-taking application that knows programmers and Markdown better.

- takenote /2.8kStar/MIT/202108/ts/数据可选local或github
  - https://github.com/taniarascia/takenote
  - https://takenote.dev/app
  - 依赖react-beautiful-dnd、react-router、@reduxjs/toolkit、redux-saga、react-markdown、axios、codemirror、express、jszip
  - A free, open-source notes app for the web
  - The notes are persisted temporarily in local storage, but you can download all notes in markdown format as a zip.
  - Hidden within the code is an alternate version that contain a Node/Express server and integration with GitHub.
  - 👉🏻 What you see is what you paste. No WYSIWIG, no formatting pasted from the web, and no features you don't need or want. 

- trilium /17.1kStar/AGPL.v3/202208/js/ckeditor5/支持多端
  - https://github.com/zadam/trilium
  - https://github.com/zadam/trilium/wiki/
  - 依赖 electron、express、jsdom、turndown、ckeditor.v5、codemirror、fancytree、bootstrap
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - Synchronization with self-hosted sync server
  - Trilium is provided as either desktop application (Linux and Windows) or web application hosted on your server (Linux). 
    - Mac OS desktop build is available, but it is unsupported.
    - If you want to install Trilium on server,currently only recent Chrome and Firefox are supported (tested) browsers.
  - [Notion like database](https://github.com/zadam/trilium/issues/822)
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

- my-notes /198Star/MIT/202211/ts
  - https://github.com/penge/my-notes
  - note-taking in Chrome with Google Drive support.
  - Chrome extension for simple and fast note-taking
  - Back up notes to Google Drive; Auto Sync notes to Google Drive
  - Drag and drop image with automatic image upload to Google Drive
  - Works offline

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
# note-utils
- graph /7Star/MIT/202210/ts
  - https://github.com/graphcentral/graph
  - https://graphcentral.github.io/graph
  - Performant graph visualization on the web with WebGL + Webworkers + IndexedDB
  - You can visualize Notion pages on force layout graph using this library
# more-note-app
- https://github.com/dvstechlabs/Noteslify /202211/js
  - A Notes Taking Web App Built With Simplicity.
  - Your Privacy Friendly, Open Source. Alternative to EverNote.
  - 编辑器是简单textarea
  - ui界面和后台功能基本实现

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

- https://github.com/hackmdio/codimd
  - /8kStar/AGPLv3/202208/js/inactive
  - Realtime collaborative markdown notes on all platforms.
  - HackMD helps developers write better documents and build active communities with open collaboration
  - CodiMD is the free software version of HackMD, developed by the HackMD team with reduced features (without book mode)
- https://github.com/hedgedoc/hedgedoc
  - HedgeDoc (formerly known as CodiMD) is an open-source, web-based, self-hosted, collaborative markdown editor.

- https://github.com/vicjohnson1213/Medley /202007/inactive
  - 依赖angular7、hightlight.js、marked、monaco-editor、rxjs、subsink、zone.js
  - A tag-based note taking app using Markdown for formatting.
  - I drew some design inspiration (specifically the tag-based organization) from Notable
