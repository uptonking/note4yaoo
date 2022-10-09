---
title: lib-editor-prosemirror-examples-collab
tags: [collaboration, examples, prosemirror]
created: '2022-10-04T23:32:13.096Z'
modified: '2022-10-04T23:32:30.824Z'
---

# lib-editor-prosemirror-examples-collab

# guide

- 基于yjs
  - tiptap.v2
  - outline
  - milkdown

- 基于prosemirror-collab
  - atlaskit-editor
  - dox
  - paper-editor
# collab-starter-simplified

## 基于y-prosemirror实现协作的示例

- https://github.com/alihesari/prosemirror-demo
  - https://demos.yjs.dev/prosemirror/prosemirror.html
  - collaborative with Yjs & y-prosemirror + y-websocket
- https://github.com/ocavue/y-prosemirror-playground
  - 依赖 yjs, y-webrtc, y-prosemirror

## 基于prosemirror-collab + websocket实现协作的示例

- https://github.com/mehri-amin/meditor
  - 根据官方文档的最精简示例，基于socket.io而不是轮询
- https://github.com/raydwaipayan/collaborate
  - 官方示例client/server代码未改动，替换了启动代码
  - an project to build a multi user online editor based on ProseMirror
- https://github.com/Yxwww/prosemirror-collab-example
  - 官方示例client/server代码未改动，替换了启动代码
  - Stripped out prosemirror website collab example into a stand alone environment for learning and toying around.
- https://github.com/TeemuKoivisto/prosemirror-react-typescript-example/tree/master/packages/api-collab
  - an example collaboration server based on prosemirror-collab

## tiptap.v1、vue2 实现协作的示例

- https://github.com/dekunma/tiptap-collaboration
  - 包含client+server
- https://github.com/powlaa/text-editor
  - 包含client+server
- [A simple implementation of prosemirror-collab for tiptap.v1](https://discuss.prosemirror.net/t/a-simple-implementation-of-prosemirror-collab/1930)
# crdt/yjs
- https://github.com/yjs/y-prosemirror
  - ProseMirror editor binding for Yjs

- https://github.com/idealjs/chao-feng
  - 依赖 yjs

- https://github.com/nandit123/crdt-text-editor-2
  - https://github.com/FleekHQ/crdt-text-editor
  - A p2p decentralized text-editor based on CRDTs
  - 依赖y-prosemirror、lit-html

- https://github.com/pamphlets/editorial
  - https://github.com/pamphlets/pamphlet /pm-editor
  - 依赖y-prosemirror、yjs、y-webrtc
  - collaboratively edit texts without relying on a central server. 
  - Each user has a copy of the collaborative document on their own device stored inside IndexedDB. 
  - Editorial then uses WebRTC to make a direct connection between the browsers of different users to exchange changes to the document.

- https://github.com/fadiquader/prosemirror-collaborative-editor
  - collaborative editor for React built with Prosemirror + Yjs + mongodb

- https://github.com/tororosoba0534/collab-note-yjs-wsserver
  - Collab-Note-YJS is a multi-repo project which divided by two repositories (frontend and backend). 

- https://github.com/saranrapjs/prosemirror-automerge /201904/js/inactive
  - experiment with wiring automerge up to ProseMirror
  - The basic idea is to have a ProseMirror plugin that works similarly to the collab plugin: steps which originate from the editor are translated to an Automerge document, and changes to a "remote" Automerge document are translated back to the ProseMirror document as steps.
# ot-like/prosemirror-collab
- bear-plus /5Star/ISC/202008/js/ejs/inactive
  - https://github.com/yk9331/bear-plus
  - https://bear-plus.yenchenkuo.com/@bear-plus/features
  - 依赖codemirror.v5、express、markdown-it、sequelize、express、multer
  - A web-based writing application with real-time collaboration and Markdown syntax support for crafting and sharing notes. 
  - Group and find note easily with hashtag and full text search. Inspired by Bear note and HackMD.

- https://github.com/li-yechao/paper-collab
  - Backend of the rich editor paper-editor.

- https://github.com/benaubin/prosemirror-collab-plus /202008/ts/inactive
  - Improvements over prosemirror-collab:
    - Server-side rebasing drastically reduces network round-trips
    - Steps are queued and sent as commits, reducing overhead
    - When possible, steps are merged prior to network transport

- eg
  - https://github.com/naept/tiptap-extension-collaboration
  - https://github.com/naept/tiptap-collab-server

- eg
   - https://github.com/mms-gianni/prosemirror-collaborationserver
    - https://github.com/mms-gianni/tiptap-collaboration-demo
    - 依赖 tiptap.v1、vue2
# collab-using-database
- https://gitlab.com/emergence-engineering/blog/-/tree/master/articles/prosemirror-sync-1
  - using a sync database ( PouchDB, but it works with firebase ) as a communication layer between client and server.
  - [Article / code about prosemirror collab & PouchDB](https://discuss.prosemirror.net/t/article-code-about-prosemirror-collab-pouchdb/3045)
# collab-examples
- https://github.com/dlemrry/editor
  - real time collaborative documents using web socket
  - Web application for editing texteditor and painting canvas in real-time collaboration.
  - 展示了 quill、prosemirror、draftjs 几个示例
  - 提供了client+server，可作为通用协作方案
# more-collab
- https://github.com/sakheli/sync-doc
  - 未实现实时协作

- https://github.com/microsoft/FluidFramework/tree/main/examples/data-objects/prosemirror
  - An experimental implementation of how to take the open source ProseMirror rich text editor and enable real-time coauthoring using the Fluid Framework.
  - Fluid Framework is a library for building distributed, real-time collaborative web applications using JavaScript or TypeScript.
