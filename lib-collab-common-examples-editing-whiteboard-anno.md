---
title: lib-collab-common-examples-editing-whiteboard-anno
tags: [collaboration, editor, examples, sketch, toc, whiteboard]
created: 2022-11-07T15:53:52.142Z
modified: 2022-11-07T17:36:22.236Z
---

# lib-collab-common-examples-editing-whiteboard-anno

# guide

# whiteboard-blogs
- [Excalidraw: Building Excalidraw's P2P Collaboration Feature_202003](https://blog.excalidraw.com/building-excalidraw-p2p-collaboration-feature/)
  - 协作编辑同一个shape时，协作算法并未特殊处理，可能会有数据丢失，但versionNonce保证了最终一致
  - We did not want to store anything server-side. Therefore, we opted for a pseudo-P2P model, where a central server relays end-to-end encrypted messages to all the peers in the room, but does no centralized coordination.
  - our encrypted messages can be passed between the client and the server back to other clients as `ArrayBuffer`, so we don’t need to convert them to other data structures at any point in the transit.
  - when elements were added, we adopted an architecture of merging states when we receive them. 
    - local client A looks at all the ExcalidrawElement.ids it has locally, and all of the incoming ExcalidrawElement.ids, and creates a new ExcalidrawElement array containing the union of both the local and incoming set.
  - Peers would set `isDeleted` field to `true` to delete an element, and would filter the deleted elements out of the array at runtime.
    - we do remove any element with `isDeleted` set to `true` when saving to persistent storage, so long-lived drawings where this may become a problem are cleaned up.
  - Concurrent edits will still be lost, as our merge algorithm only looks at new elements being added or removed, and not changes to existing elements themselves.
    - when we merge multiple peers state together, we throw out old versions of each element and just keep the latest ones.
    - This algorithm is simple but effective, and solved most of our collaboration problems.
  - The version number only solves race conditions when players are editing different elements concurrently. What if they’re editing the same element concurrently?
    - For Excalidraw, we don’t really care! We think this will be a pretty rare situation, and that users will tolerate some jankiness if it happens.
    - With that said, it is important that all peers converge on the same state. 
    - Any time we increment the version of an element, we set `versionNonce` to a random integer. 
    - At merge time, if we encounter two elements with the same version number but different data (i.e. two players editing the same element at the same time), we break the tie by favoring the one with the lower `versionNonce`. 
    - This ensures that one player will deterministically “win” on every peer.
  - One problem we haven’t solved yet is implementing multiplayer undo/redo. 
    - Our hack around this was to clear the undo/redo stack whenever you receive an update from a new peer.

- [Excalidraw: End-to-End Encryption in the Browser_202003](https://blog.excalidraw.com/end-to-end-encryption/)
  - Web Cryptography APIs are now widely available to all the browsers that let us implement this. 
  - That said, the APIs to deal with encryption, keys and binary data are not the most straightforward

- [Excalidraw: Deprecating Excalidraw Electron in favor of the Web version_202012](https://blog.excalidraw.com/deprecating-excalidraw-electron/)
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

- https://github.com/muaz-khan/Canvas-Designer
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
# collab-editing
- https://github.com/convergencelabs/html-text-collab-ext
  - A set of utilities that enhances a normal HTML `<textarea>` element with collaborative editing capabilities. 
  - The enhanced `<textarea>` is able to render the cursor and selection of other collaborators.
  - This library has no dependency on Convergence.
  - 只依赖textarea-caret，不依赖其他

- https://github.com/cchaonie/collaborative-editor /ts/slate+sharedb
  - Learn collaborative softwares by creating a collaborative editor
  - The slate handles the UI part, and the sharedb handles the collaborative part.

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

- https://github.com/itoumlilt/crdt-md-editor /ts/slate
  - React Typescript CRDT based Collaborative Markdown Editor

- https://github.com/AshAman999/codeBuddy
  - A simple minimalist collabrative code editor
  - 依赖codemirror5
  - WebSocket client for react and Node

- https://github.com/we-miks/collaborative-editor
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

- https://github.com/slashbaseide/slashbase
  - Slashbase is an open-source minimal collaborative IDE for your databases in browser.
  - It's written in Golang and Nextjs React Framework and runs as a single binary.
  - Connect to your database, browse data, run a bunch of queries or share queries within your team, right from your browser. 
  - Works with two types of databases: PostgreSQL and MongoDB.

- https://github.com/mathematicalthinking/vmt
  - Collaborative workspaces for exploring the world of math
  - uses React.js and Redux.js, express and sockets.io. 
