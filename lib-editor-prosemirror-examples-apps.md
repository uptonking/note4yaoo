---
title: lib-editor-prosemirror-examples-apps
tags: [app, prosemirror, toc]
created: 2022-08-18T16:56:32.322Z
modified: 2022-08-18T16:57:15.296Z
---

# lib-editor-prosemirror-examples-apps

# guide

# prosemirror-starter
- https://github.com/syfxlin/tiptap-starter-kit
  - Tiptap编辑器的非官方套件，包含了常见的扩展集合，以及斜杠菜单，浮动菜单，Markdown解析、序列化等功能。

- https://github.com/mfoitzik/prosemirror-breakout-starter-kit
  - This is a ProseMirror starter kit that uses Webpack.
  - https://github.com/buzz-software/prosemirror-webpack-project
    - 只有单文件，过于简单
- https://github.com/KyleMit/prosemirror-sample
  - https://prosemirror-sample.netlify.app/
  - Interactive view of the basic example from the ProseMirror website.

- https://github.com/ccorcos/prosemirror-examples
  - https://ccorcos.github.io/prosemirror-examples/
  - ProseMirror rich text editor with @mentions with autocomplete and nested inline nodes.

- https://github.com/TeemuKoivisto/prosemirror-bug-template
  - Github template to reproduce ProseMirror bugs in simplest form possible

- DoX /5Star/NALic/202208/js
  - https://github.com/AlbertCerfeda/DoX
  - https://doxeditor.herokuapp.com/
  - 依赖 express、passport、socket.io、bootstrap4
  - DoX Editor aims to be a web text editor application that allows users to create, edit, store and share several documents.
  - A web text editor application that allows users to create, edit, store and share several documents, with support for real-time collaborative editing.
  - DoX is clearly inspired to well known online word processors such as Google Docs

- https://github.com/vivaxy/examples/tree/master/libraries/prosemirror
  - https://vivaxy.github.io/examples/libraries/prosemirror/
  - 日常积累的各种demo，包括prosemirror/yjs/算法

- https://github.com/edp1096/hello-prosemirror
  - https://edp1096.github.io/hello-prosemirror/
  - 测试
# office/notebook
- noteworthy /166Star/AGPL.v3/202207/ts/electron
  - https://github.com/benrbray/noteworthy
  - https://noteworthy.ink/
  - Markdown editor with bidirectional links and excellent math support
  - 依赖solid-js、remark13、prosemirror、electron-window-state、remark
  - 参考了prosemirror、zettlr、vscode、notable
    - Thanks to Fabio Spampinato for releasing the source to an early version Notable!
  - https://github.com/benrbray/prosemirror-math

- Starboard Notebook /889Star/MPLv2/202206/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.
  - 编辑器已分离，基于rich-markdown-editor和prosemirror
  - 前端基于lit

- codex /195Star/CC-BY-NC-4.0/202202/js/electron
  - https://github.com/jcv8000/Codex
  - https://codexnotes.com/
  - 依赖 prosemirror、katex、bootstrap4、jquery、highlight.js
  - A free note-taking software for programmers and Computer Science students

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

- mdSilo-web /208Star/AGPL.v3/202208/ts
  - https://github.com/danloh/mdSilo-web
  - https://mdsilo.com/
  - 核心编辑器mdsmirror未开源，基于rich-markdown-editor
  - 依赖 react、tauri/rust、dnd-kit、headlessui、popperjs、react-spring、tailwindcss、d3-drag/selection、fuse.js、immer、codemirror.v6、styled-comp、react-virtualized、zustand
  - A mind silo for storing ideas, thought, knowledge with a powerful writing tool.
  - Available for Web, Linux, Windows and macOS. 
- mdSilo-app /93Star/AGPL.v3/202208/ts
  - https://github.com/danloh/mdSilo-app
  - https://mdsilo.com/
  - A mind silo for storing ideas, thought, knowledge with a powerful writing tool. 

- notebook /11Star/MIT/202208/ts/提交多
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
# prosemirror-apps
- oak /4Star/MIT/202208/js/提交多
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

- tropy /637Star/AGPL.v3/202208/js
  - https://github.com/tropy/tropy
  - https://tropy.org/
  - help to organize and describe your research photos so you can quickly find your sources 
  - use tags and lists to organize your research items
  - annotation tools allow you to transcribe documents, select image details
  - exports your research projects as JSON‑LD, CSV, and even directly to Omeka S. 

- https://github.com/pageboard/client /4Star/MIT/202208/js
  - uses prosemirror to drive HTML wysiwyg editing.
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

- https://github.com/PelagicCreatures/marlin /inactive
  - An ExpressJS CMS for sites with Sequelize db backends
  - This package implements a relational typed admin backend built from sequelize model definitions with granular access control for editing tables using ACLs for users and roles.
  - https://github.com/PelagicCreatures/marlin-app

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

- https://github.com/pierre-lgb/slashwriter
- https://github.com/martinemmert/fleeting-notes-editor
