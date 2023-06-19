---
title: lib-collab-common-examples-editing-whiteboard-anno
tags: [collaboration, editor, examples, sketch, toc, whiteboard]
created: 2022-11-07T15:53:52.142Z
modified: 2022-11-07T17:36:22.236Z
---

# lib-collab-common-examples-editing-whiteboard-anno

# guide
- 实现协作要考虑到切换冲突处理算法
  - 如slate或成熟编辑器都支持binding到不同的协作数据yjs/automerge/sharedb

- [Why CRDT didn't work out as well for collaborative editing xi-editor](https://news.ycombinator.com/item?id=19886883)
  - 研发编辑器不仅要考虑协作，其他功能如find、syntax-highlight对用户体验甚至更重要
  - 所以还是要参考成熟编辑器的可复用功能，如copy-paste、import-export、word-excel
# whiteboard/annotation
- https://github.com/feakin/feakin-web
  - Feakin是一个架构资产可视化管理工具。
  - 基于 图表即代码 的思想体系，支持导入 Mermaid, PlantUML, Excalidraw, Dot 等图形资产格式。

- https://github.com/lovasoa/whitebophir /1.5kStar/AGPLv2/202211/js
  - Online collaborative Whiteboard that is simple, free, easy to use and to deploy

- https://github.com/spacedeck/spacedeck-open
  - a web based, real time, collaborative whiteboard application with rich media support

- https://github.com/cracker0dks/whiteboard
  - NodeJS collaborative Whiteboard/Sketchboard which can easily be customized

- https://github.com/toger5/TheBoard
  - collaborative Whiteboard powered by the [matrix] protocol and infrastructure.

- https://github.com/kriziu/collabio
  - Real-time whiteboard made with Next. JS and Socket. IO
  - 依赖recoil、nextjs、express、socket.io

- https://github.com/muaz-khan/Canvas-Designer /202010/inactive
  - Collaborative, extendable, JavaScript Canvas2D drawing tool, supports dozens of builtin tools, as well as generates JavaScript code for 2D animations.

- https://github.com/nyxtom/drawing-webrtc
  - Simple proof of concept realtime collaborative drawing
  - All the client-side javascript is vanilla javascript and requires no bundling or external dependencies.
  - using Redis PubSub

- https://github.com/gouravanand662/collaborative-whiteboard
  - collaborative whiteboard using socketIO 

- https://github.com/wx-chevalier/web-whiteboard
  - 在线电子白板，你画我猜，图片编辑，网页注解

- https://github.com/givek/sketch-canvas
  - Canvas app lets you create multiple collaborative virtual whiteboards for free-hand sketching.
  - This is the sketch-canvas web client developed to consume the sketch-canvas-api.
  - https://github.com/givek/sketch-canvas-api/
    - 依赖mongoose、zod

- https://github.com/off-by-some/Whiteboard
  - A collaborative whiteboard powered by WebGL + react-fiber

- https://github.com/mitaai/AnnotationStudio
  - Web application for collaborative annotationggg
  - 依赖mongodb

- https://github.com/candiedoperation/floww
  - A collaborative whiteboard and a step to revolutionarize classroom education using Open-Source software.

- https://github.com/JSv4/OpenContracts
  - Open Source collaborative text annotating platform based on React and Django

- grida /104Star/Apache2/202206/ts
  - https://github.com/gridaco/grida
  - https://grida.co/
  - Skia based performant live design collaboration & workspace app - redesigned for both designers and developers

- https://github.com/cloud-annotations/cloud-annotations
  - collaborative open source image annotation tool for teams and individuals.

- https://github.com/UniversalDataTool/universal-data-tool
  - Collaborate & label any type of data, images, text, or documents, in an easy web interface or desktop app.

- https://github.com/ncbi-nlp/TeamTat
  - Text annotation tool for team collaboration

- boardsite /24Star/AGPLv3/202210/ts/画板
  - https://github.com/boardsite-io/boardsite
  - https://boardsite.io/
  - a productivity app for taking notes, annotating documents and collaborating with friends on any device with a browser.
# collab-editing
- https://github.com/convergencelabs/html-text-collab-ext
  - A set of utilities that enhances a normal HTML `<textarea>` element with collaborative editing capabilities. 
  - The enhanced `<textarea>` is able to render the cursor and selection of other collaborators.
  - This library has no dependency on Convergence.
  - 只依赖textarea-caret，不依赖其他

- https://github.com/Rishabh-malhotraa/caucus
  - Realtime Collaborate Editor with Embedded Compiler
  - 类似协作codepen
  - Built With React Material UI yjs Written in TypeScript
  - 依赖knex、pg、yjs、codemirror5

- mute /96Star/AGPLv3/202302/ts/rxjs
  - https://github.com/coast-team/mute
  - https://mutehost.loria.fr/
  - a scalable collaborative document editor with CRDT, P2P and E2EE
  - MUTE implements a CRDT-based consistency algorithm (LogootSplit) for large scale peer-to-peer collaboration on top of a peer-to-peer message layer (netflux and soon libp2p).
  - 示例基于tui-editor.v2、codemirror5、angular
  - https://github.com/coast-team/mute-core
    - 依赖rxjs、dotted-logootsplit
  - https://github.com/coast-team/dotted-logootsplit /MPL
    - a delta-based version of LogootSplit with smaller metadata. We provide both op-based and delta-based synchronizations.

- https://github.com/cchaonie/collaborative-editor /ts/slate+sharedb
  - Learn collaborative softwares by creating a collaborative editor
  - The slate handles the UI part, and the sharedb handles the collaborative part.

- https://github.com/codezri/react-node-websockets-demo /js
  - A simple collaborative document editing app built with React and Node
  - Used the react-use-websocket hook/library instead of directly using the inbuilt WebSockets browser API.
  - 依赖 react-simple-wysiwyg

- https://github.com/SkyGuardian42/piko.space
  - Collaborate at the speed of light and seamlessly sync offline work
  - tiptap的协作示例
  - redis、yjs、tiptap
  - 前端依赖tiptap、radix-ui、tanstack-query、yjs、zustand
  - 后端依赖trpc、express、yjs、zod

- https://github.com/baktiaditya/cother
  - A real-time collaborative code editor and previewer.
  - This project is just for fun and to learn firepad implementation.

- web-editor-markdown /90Star/MIT/202211/ts
  - https://github.com/Ben-love-zy/web-editor-markdown
  - 基于 Web 浏览器，即时渲染的 Markdown 编辑器。它基于 TypeScript 和 vanillajs 打造，并且不依赖任何第三方框架，对中文支持友好
  - 提供源码模式、双屏渲染模式、实时编辑模式和只读模式四种渲染模式。
  - 如果有需要，它的底层同时也支持了协同编辑的能力，提供了原子操作 Operation 用于扩展协同编辑。

- https://github.com/concordant/c-markdown-editor
  - A CRDT based collaborative markdown editor.

- https://github.com/itoumlilt/crdt-md-editor /ts/slate/CouchDB
  - React Typescript CRDT based Collaborative Markdown Editor

- https://github.com/AshAman999/codeBuddy
  - A simple minimalist collabrative code editor
  - 依赖codemirror5
  - WebSocket client for react and Node

- https://github.com/we-miks/collaborative-editor /202108/js/inactive
  - A collaborative editor that supports authorship display, image uploading placeholder and CJK characters composition based on Quill and ShareDB.

- https://github.com/MrFoxPro/bloki
  - https://bloki.app/
  - 支持在文档上放画板，ui设计友好

- https://github.com/vivliostyle/vivliostyle-pub
  - project for a new typesetting system based on web standard technology.
  - Vivliostyle Pub is a sub-project of Vivliostyle for enabling book writing, co-editing and publishing in web browsers.

- https://github.com/KB1RD/matrix-notepad
  - A buggy way to collaborate on text documents using the Matrix protocol. 

- https://github.com/iamlemec/elltwo /js/python
  - a browser-based platform collaborative technical document creation. 
  - Collaborative technical document creation: SQLite backend, browser frontend. 
  - Markdown, math, images, references, citations. Full text search.
  - Articles are written in a simple markup language borrowing elements of Markdown and LaTeX.

- https://github.com/Rowadz/real-time-collaborative-code-editor
  - A real time code editor, with rooms

- https://github.com/hockyy/peertocp
  - Real time collaborative code editor using webrtc

- https://github.com/MyoniM/mirror-code-react-js
  - A collaborative Web IDE with Code Mirror's CRDT Server and Socket.io

- https://github.com/Swanand01/CollabCode
  - A collaborative, real-time, online coding environment for developers.
  - CollabCode Editor: Codemirror and Firepad.
  - Video and audio chat: Agora.

- https://github.com/freeonlineoffice/online
  - a collaborative online office suite, used within a browser and based on LibreOffice technology.
- https://github.com/CollaboraOnline/online
  - a collaborative online office suite based on LibreOffice technolog
# more
- EtherSheet /201Star/BSD/201708/js
  - https://github.com/ethersheet-collective/EtherSheet
  - Online spreadsheet collaboration in real time using node.js. 
  - Similar to etherpad-lite but its a spreadsheet!

- https://github.com/att/rcloud
  - RCloud is an environment for collaboratively creating and sharing data analysis scripts. 
  - RCloud lets you mix analysis code in R, HTML5, Markdown, Python, and others. 
  - RCloud provides a notebook interface that lets you easily record a session and annotate it with text, equations, and supporting images.

- https://github.com/team-watchdog/databank-sri-lanka
  - We are building a collaborative platform to create and collect key datasets.

- https://github.com/slashbaseide/slashbase /ts/go
  - Slashbase is an open-source minimal collaborative IDE for your databases in browser.
  - It's written in Golang and Nextjs React Framework and runs as a single binary.
  - Connect to your database, browse data, run a bunch of queries or share queries within your team, right from your browser. 
  - Works with two types of databases: PostgreSQL and MongoDB.

- https://github.com/mathematicalthinking/vmt
  - Collaborative workspaces for exploring the world of math
  - uses React.js and Redux.js, express and sockets.io. 

- https://github.com/ruyd/fullstack-monorepo
  - Fullstack Canvas Drawing App and TypeScript Starter Template

- https://github.com/markandre13/workflow
  - A collaborative real-time white- and kanban board
  - 依赖knex
