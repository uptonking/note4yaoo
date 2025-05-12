---
title: lib-office-saas-tiddlywiki-examples
tags: [examples, tiddlywiki]
created: 2023-11-14T16:20:13.442Z
modified: 2023-12-15T17:50:41.213Z
---

# lib-office-saas-tiddlywiki-examples

# guide

- fans-tiddlywiki
  - https://github.com/abesamma/TW5-editions
  - https://github.com/danielo515/tiddlypouch
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

- https://github.com/TiddlyWiki/TiddlyDesktop /202307/js/BSD
  - A custom desktop browser for TiddlyWiki 5 and TiddlyWiki Classic, based on nw.js

- https://github.com/tiddly-gittly/TidGi-Desktop /1.2kStar/MPLv2/202309/ts
  - https://tidgi.fun/
  - 「 太记 」是一个基于「 太微 TiddlyWiki 」的知识管理桌面应用，能保护隐私内容、高级自动化、自动Git云备份、部署为博客，且可通过RESTAPI与Anki等应用连接。
  - 太微的NodeJS版本有无缝的自动保存体验，这是利用 SyncAdaptor 技术（而不是 Saver ）带来的的优势，太记对 NodeJS wiki 有更好的支持，而 TD 主要支持 HTML 版单文件 WIKI，各有优势

- https://github.com/jokroese/tiddlyroam /202005/html/inactive
  - https://tiddlyroam.org/
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
  - 依赖gatsby2、material-ui.v4
  - https://github.com/abesamma/Maarfapad /202002/js
    - Maarfapad was my attempt at learning Expressjs back in 2016 while building a CRUD app to handle TiddlyWiki html files. 
    - retired in favor of another project of mine Oneplaybook

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

- https://github.com/NoteSelf/NoteSelf.github.io /119Star/BSD/202005/js/inactive
  - https://noteself.org/
  - https://NoteSelf.github.io
  - built on top of TiddlyWiki, a powerful, free, highly customizable and open-source personal wiki.
  - 依赖tiddlywiki5、tw-pouchdb
  - We took the best of it, it's powerful customization system, and mixed it with one of the best embedded databases available, PouchDb, to bring in the synchronization capabilities you need.
  - This TiddlyWiki-variant stores documents in the browser (pouchdb) and can sync to a couchdb-server.
- https://github.com/danielo515/tiddlypouch /202005/js
  - tiddlypouch plugin for tiddlywiki. 
  - This plugin adds a layer between pouchdb and tiddlywiki to store tiddlers as documents on a pouchdb database. 
  - This plugin is a key and core part of the NoteSelf project.
  - 依赖 https://github.com/danielo515/tw5-pouchdb /202001/js

- https://codeberg.org/valpackett/tiddlypwa /BSD/202310/ts
  - https://tiddly.packett.cool/
  - TiddlyPWA turns TiddlyWiki into an offline-first Progressive Web App with encrypted local persistent storage and efficient synchronization with a server that can easily be hosted for free.
  - [Introducing TiddlyPWA: putting TiddlyWiki on modern web app steroids_202307](https://val.packett.cool/blog/tiddlypwa/)
    - There has actually been one good attempt at bringing this kind of sync to TiddlyWiki: NoteSelf, which integrated PouchDB for storage. 
    - I liked the sound of it, but in practice it wasn’t up to my standards. It’s a heavyweight modification of TiddlyWiki that doesn’t keep up with latest core updates, PouchDB/CouchDB feel a bit heavy themselves, there’s no encryption, and the offline support is just “run it from your hard drive”.
    - The server was initially written with SQLite as it is now, but when Deno KV was announced I got excited and rewrote it to use KV,
  - [TiddlyPWA: putting TiddlyWiki on modern web app steroids | Hacker News_202307](https://news.ycombinator.com/item?id=36885753)

- https://github.com/balazsgrill/tw-pouchdb-sync /202309/js
  - TiddlyWiki synchronizer plugin for CouchDB/PouchDB
  - https://github.com/OokTech/TW5-PouchDBAdaptor /201912/js
    - syncer adaptor that stores tiddlers in a local pouchdb

- https://github.com/ThaddeusJiang/Projectify /202206/js
  - https://thaddeusjiang.github.io/Projectify/
  - a project management app for TiddlyWiki, inspired by products like Todoist and Basecamp.

- https://github.com/tiddly-gittly/tiddlywiki-whiteboard /MIT/202403/ts
  - https://tiddly-gittly.github.io/tiddlywiki-whiteboard/
  - Tiny little drawing app in TW, using tldraw. 
  - Providing diagram widget and whiteboard view.
  - This project is based on TLDraw, and some of its components are inspired by toeverything/AFFiNE. I choose TLDraw because it is DOM based, which makes integration with tiddlywiki much easier.
# sync/collab
- https://github.com/qiushihe/tiddlywiki-remote-filesystem-syncadaptor /202201/ts
  - A `syncadaptor` module for TiddlyWiki to synchronize tiddlers with remote filesystem (i.e. AWS S3).

- https://github.com/fiatjaf/tiddlywiki-remotestorage /201810/js
  - a syncadaptor plugin that saves tiddlers on custom remoteStorage directories

- https://github.com/joshuafontany/y-tiddlywiki /202202/js/inactive
  - Tiddlywiki5 binding for Yjs
  - maps a Y. Doc to a Tiddlywiki 5 instance. 
  - It optionally supports shared cursors via the quill-cursors module.

- https://github.com/bmann/drift-tiddlywiki-template /202005/html/inactive
  - https://github.com/akhater/akhater.github.io
  - Drift TiddlyWiki Template
# examples

# plugins
- https://github.com/BurningTreeC/tiddlywiki-multi-columns /202310/js
  - https://burningtreec.github.io/tiddlywiki-multi-columns
  - multi-columns layout

- https://github.com/BurningTreeC/tiddlywiki-codemirror-6
  - https://burningtreec.github.io/tiddlywiki-codemirror-6/
  - adds the CodeMirror 6 editor to TiddlyWiki

- https://github.com/felixhayashi/TW5-TiddlyMap /bsd/202302/js
  - a TiddlyWiki plugin that turns your favourite personal note taking software in a wiki-concept-map hybrid.
  - Vis.js is used for graph visualization and manipulation

- https://github.com/tiddly-gittly/slate-write /32Star/MIT/202310/ts
  - https://tiddly-gittly.github.io/slate-write/
  - WYSIWYG editor for TiddlyWiki. (WIP)
  - 一个用于 太微TiddlyWiki 的所见即所得编辑器
  - [Demo of a new WYSIWYG editor: slate-write (unstable alpha stage) - Plugins - Talk TW_202203](https://talk.tiddlywiki.org/t/demo-of-a-new-wysiwyg-editor-slate-write-unstable-alpha-stage/2788)
    - It is based on tw-react plugin, and use the powerful SlateJS editor and tons of keyboard shortcut plugins from udecode/plate
    - And I write some transformers to convert wikitext from/to SlateJS state JSON on saving, every 1s.

- https://github.com/tiddly-gittly/tw-react /202309/ts
  - https://tiddly-gittly.github.io/tw-react/
  - This is a dependency of slate-write WYSIWYG editor and flowtiwi-sidebar and many other dynamic widgets. 
  - This plugin enable powerful data operation and UI operation of those plugins, thus become a prerequisite of those plugins

- https://github.com/danielo515/TW5-contextPlugin /202307/js
  - http://contextplugin.tiddlyspot.com/
  - A plugin to allow preview with word highlight within searches but not limited to that. 
  - Actually this widget looks for a word inside a tiddler and shows the result with the searched word highlighted with some of its context.

- https://github.com/EvanBalster/TiddlyWikiFormula /MIT/202012/js
  - A TiddlyWiki plugin for functional formulas, combining the power of Excel and Google Sheets with TiddlyWiki's processing idioms.
  - [Formula: Spreadsheet-like mathematics for TiddlyWiki_201712](https://groups.google.com/g/tiddlywiki/c/bfInUWhAtzo)
# utils
- https://github.com/jimpick/dat-tiddlywiki /201806/js
  - Multiwriter Dat + TiddlyWiki
  - I hooked up Dat multiwriter and the Automerge CRDT for my own personal use... I’ve been using it for several months and it works well.

- https://github.com/ssg/ourobs /html
  - an experiment about a self-hosted, fully decentralized social platform
  - ourobs stores everything in the URL, so, you can share your content by sharing the URL with others. 

- https://github.com/abesamma/giscus-for-tiddlywiki-demo /202302/js
  - Demo of a commenting system for TiddlyWiki powered by Github discussions via Giscus app

- https://github.com/Arlen22/TW5-storage-plugin /202002/ts
  - I have a working prototype for the client-side data folders. 
# usecase-examples
- https://ramirosalas.com/
# more
