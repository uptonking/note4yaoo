---
title: lib-office-joplin-examples
tags: [examples, joplin, note-taking, toc]
created: 2024-01-28T21:36:57.066Z
modified: 2024-01-28T21:37:15.191Z
---

# lib-office-joplin-examples

# guide

# popular
- joplin /31.9kStar/MIT > AGPLv3/202209/ts/web需付费+pc+mobile
  - https://github.com/laurent22/joplin
  - https://joplinapp.org/
  - note taking and to-do application with synchronization capabilities for Windows, macOS, Linux, Android and iOS
  - 依赖react-redux、sqlite3、@electron/remote、electron-window-state、async-mutex、tinymce.v5【GPL】、codemirror.v5、immer、mark.js、moment、re-resizable、styled-components
  - 服务端依赖koa、knex、markdown-it、mustache、sqlite3
  - [Switch license to AGPL-3.0_20221221](https://joplinapp.org/news/20221221-agpl/)
    - [最后的MIT版本 v2.9.17/v2.10.2](https://github.com/laurent22/joplin/releases/tag/v2.9.17), v2.10.3为AGPL
  - https://github.com/laurent22/joplin/commits/dev/packages/server?after=07ee20a0ff13fff779617beb39a79d5ba19fbc3c+769
    - server最后一个MIT在 v20210510_0b67446
  - [Why is there no web UI for Joplin?](https://www.reddit.com/r/joplinapp/comments/xjp9zh/why_is_there_no_web_ui_for_joplin/)
    - ~~Joplin server has no ability to view/edit notes from the server with a web client~~ .
    - https://github.com/joplin-vieweb/joplin-vieweb
  - 🍴 forks
  - https://github.com/ken1kob/joplin /202212
    - A branch of Joplin: quick-slim-note
    - Joplin 2.9.17+quick-slim-note 
  - https://github.com/genneko/joplin
    - run Joplin on FreeBSD with this fork
  - https://github.com/sdip15fa/joplin /202309
  - https://github.com/XilinJia/Xilinota /AGPL/202403
    - a fork from Joplin v2.13.4.

- https://github.com/joplin/website-plugin-discovery /MIT/202401/ts/mustache
  - https://joplinapp.org/plugins/
  - https://joplinapp.org/help/api/get_started/plugins/
  - The official plugin repository website
  - 依赖codemirror.v6、highlight.js、markdown-it、mustache、webpack
  - 详情页会显示Minimum app version、下载量
  - 搜索没有单独的页面
  - build时会请求`https://github.com/joplin/plugins/blob/master/manifests.json`文件的内容作为所有插件元数据，打包出来的产物是普通spa
  - npm install -g yo generator-joplin
    - The `src/` directory contains a `manifest.json` file, which contains the various information about the plugin
    - You should test your plugin in Development Mode. Doing so means that Joplin will run using a different profile, so you can experiment with the plugin without risking to accidentally change or delete your data.
  - https://github.com/joplin/plugins /202402
    - This is the official Joplin Plugin Repository. 
    - 包含所有plugin的jpl逻辑代码和manifest.json
    - It is updated every 30 minutes on the hour and half-hour.

- https://github.com/ylc395/joplin-plugin-pages-publisher /202208/ts/vue
  - A Joplin plugin to generate static blog website from picked notes, and publish it as Github Pages

- https://github.com/abort-retry-ignore/joplock /202607/js
  - fast web client for Joplin Server.
  - Joplock runs as a sidecar alongside an unmodified Joplin Server instance, sharing the same Postgres database, sessions, notes, folders, and resources. It gives you a lightweight browser-based interface to your Joplin notes without modifying Joplin Server itself.
    - reads Joplin data directly from the shared Postgres database
    - writes notes, folders, and resources through stock Joplin Server APIs
  - Full Joplin compatibility -- desktop, mobile, CLI, and Joplock all work with the same account and data simultaneously
  - Fast search -- searches titles and note bodies directly in Postgres
  - autosave: debounced saves with conflict detection, hash-based deduplication, and an undo ring buffer with full note history snapshots
  - PWA support -- installable as a home screen app on mobile and desktop with splash screens, offline indicator, and service worker shell
  - Server-side rendering -- SSR with htmx for minimal client-side JavaScript; CodeMirror editor for markdown, rich preview mode with WYSIWYG editing
  - [Introducing Joplock, a Joplin Web Client : r/joplinapp _202604](https://www.reddit.com/r/joplinapp/comments/1subrcd/introducing_joplock_a_joplin_web_client/)
    - Does this work with custom Joplin back ends such as self hosting the Joplin server instance?
    - Yep! Just go to the settings and select any of the normal sync options. I use it with my selfhosted Joplin server instance all the time.
    - Its quite different than the existing clients, it does not store notes in a local database and all local data is deleted when you log out. It uses a different editor and markdown renderer. This should allow for rapid plugin development and auto-complete. 
    - Joplock does not work offline, and does not store notes in a local database. Notes stay on the server until you edit them. All local data (including notes and attachments) are cleared when you log out. I personally don't want my notes sitting around so I made it from a slightly paranoid(类偏执狂的) perspective.
    - AI used to make this

- https://github.com/ThibaultJanBeyer/joplin-sheets /202201/ts/inactive
  - Plugin to write excel like spreadsheets in Joplin like a pro

- https://github.com/rxliuli/joplin-utils /MIT/202312/ts
  - https://joplin-utils.rxliuli.com/
  - joplin-blog: export blog/wiki from Joplin as data source
  - joplin-search-integration: Integrate joplin notes search results in Google/Bing/Baidu search
  - joplin-api: api wrapper for Joplin for web/nodejs, and the basis for the above results

- https://github.com/markerikson/joplin-plugin-vscode-style-search /202403/ts
  - A Joplin plugin that provides a search UI panel patterned after VS Code, with matches per note and per-match hit highlighting
  - Search for text, and matches will be shown grouped by file, one line per match, with the match text highlighted. 
  - Both plain text and regular expression syntax should work.
  - todo
    - Scroll to a specific match line when clicked

- https://github.com/joplin/plugin-templates /MIT/202311/ts
  - This plugin allows you to create templates in Joplin and use them to create new notes and to-dos.
# examples

# plugins

- https://github.com/ylc395/joplin-plugin-note-link-system /202211/ts
  - A complete Link System for Joplin. Referrer(aka. backlink), Quick Link, Copy Anchor, Hover To Preview, and much more feature
  - [Plugin: Note Link System - Plugins - Joplin Forum _202111](https://discourse.joplinapp.org/t/plugin-note-link-system/21768)

- https://github.com/treymo/joplin-link-graph /MIT/202204/ts/inactive
  - plugin provides a UI for viewing all links between Joplin notes.
# utils
- https://github.com/pansinm/joplin-server-plantuml /MIT/202207/js
  - render plantuml diagram in share page

- https://github.com/QuantiusBenignus/NoteWhispers
  - Voice memos recorded from the microphone, transcribed offline to text and converted to Joplin notes
  - This repository, while (hopefully) still providing some utility, was a proof of concept and is now superceded by Spoken, which improves on the same functionality but also adds support for Joplin To-Dos (in a sepparate, standallone executable). 
- https://github.com/QuantiusBenignus/Spoken /202303/shell
  - Voice memos recorded from the microphone, transcribed offline to text and converted to Joplin notes or To-Do tasks with automatic notifications
  - This repository expands on the older NoteWhispers by bringing new tools and functionality, such as recording Joplin to-do tasks with automatic alarms and the ability to transcribe multiple voice-memo/to-do files.
# more
