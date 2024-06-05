---
title: lib-editor-prosemirror-examples-collab
tags: [collaboration, examples, prosemirror]
created: 2022-10-04T23:32:13.096Z
modified: 2022-10-04T23:32:30.824Z
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
# collab-starter

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
# collab-examples
- https://github.com/stepwisehq/prosemirror-collab-commit /MIT/202307/ts/inactive
  - 💡 Commit-based collaborative editing plugin for ProseMirror.
  - This solves two key problems with `prosemirror-collab` through server-side rebasing without the use of CRDTs:
    - Throughput: 200 active clients per 1s of commit delay is feasible depending on backend implementation and edit characteristics.
    - Fairness: Users with high latencies will not have their edits blocked by users with low latencies. This will greatly smooth the collab experience on documents with high levels of concurrent edits.
  - [ProseMirror Collab Performance | Blog _202307](https://stepwisehq.com/blog/2023-07-25-prosemirror-collab-performance/)

- https://github.com/TeemuKoivisto/prosemirror-track-changes-example
  - https://teemukoivisto.github.io/prosemirror-track-changes-example/
  - simple track-changes example with prosemirror-changeset
  - [Question about track-changes with prosemirror-changeset](https://discuss.prosemirror.net/t/question-about-track-changes-with-prosemirror-changeset/3801)

- https://github.com/milahu/prosemirror-track-changes-demo /js
  - https://milahu.github.io/prosemirror-track-changes-demo/
  - add a "track changes" feature to prosemirror

- https://github.com/Atypon-OpenSource/manuscripts-track-changes-plugin /202311/ts
  - ProseMirror plugin to track inserts/deletes to nodes and text.

- https://github.com/newsdev/prosemirror-change-tracking-prototype /201609/js
  - ProseMirror change tracking proof-of-concept
  - https://github.com/nytimes/prosemirror-change-tracking-prototype

- https://github.com/dxos/editor  /1Star/AGPLv3/202101/js/archived
  - Collaborative editor
  - 依赖 react、material-ui、remark-rehype、yjs、prosemirror、hightlight.js

- https://github.com/dmonad/Yed /js
  - A collaborative editor built with ProseMirror - demo

- https://github.com/dlemrry/editor
  - real time collaborative documents using web socket
  - Web application for editing texteditor and painting canvas in real-time collaboration.
  - 展示了 quill、draftjs、canvas+mousemove 几个示例
  - 提供了client+server，可作为通用协作方案

- https://github.com/scenaristeur/noosphere /202210/js/vue
  - https://scenaristeur.github.io/noosphere
  - 依赖milkdown.v6、vue2、bootstrap-vue.v2、remark-directive、three、yjs
  - https://github.com/scenaristeur/noosphere2 /202306/js/vue
    - A simple example for using milkdown with vue.
# versions
- https://github.com/inkandswitch/upwelling-code /ts
  - https://upwelling-prototype.netlify.app/
  - [Upwelling: Combining real-time collaboration with version control for writers](https://www.inkandswitch.com/upwelling/)
  - 依赖@atjson/document、@atjson/renderer-react、prosemirror

- https://gitlab.com/peer/doc /AGPLv3/202110/js/vue
  - https://github.com/peer/doc
  - [PeerDoc – Scaling real-time text editing](https://mitar.tnode.com/post/peerdoc-scaling-real-time-text-editing/)
  - PeerDoc is a collaborative real-time rich-text editor with undo/redo, cursor tracking, inline comments, permissions/sharing control over documents, a change history. 
  - 依赖meteor、vuetify、prosemirror
  - it provides two types of collaboration:
    - real-time collaboration between collaborators on the draft of the document (push-based collaboration).Push-based collaboration is collaboration where a change can be made directly (pushed).
    - fork and merge request style of collaboration with others, allowing collaboration to scale beyond a small group of collaborators (pull-based collaboration). Pull-based collaboration works by offering a change that must be approved before it is integrated (pulled). 
  - PeerDoc is a stable prototype. It has been already used in production.
  - Rebasing requires branches to have a shared base
  - When a fork is merged, it can no longer be edited and changes from the parent document are not propagated to it. When a fork is merged, it can no longer be edited and changes from the parent document are not propagated to it. 
  - PeerDoc does not have all the answers (yet) about how exactly to best use a combination of these two types of collaboration.
  - PeerDoc currently rebases all changes and maintains a linear history of all documents, but would a branched history without rebasing be better when trying to understand how documents came about?
  - https://twitter.com/mitar_m/status/1465439429867286536
    - merging real-time editing with forking/proposing/merging back. 
    - We managed to do it without CRDT though
  - https://github.com/peer/db
# collab-solutions
- https://github.com/saranrapjs/prosemirror-v8-perf /202311/ts
  - ProseMirror's support for collaborative editing requires an "authority server". 
  - The reference implementation of an authority server stores the current document and steps in-memory, and uses functions exported by ProseMirror libraries to apply steps to a document. 
  - This repo tries to evaluate alternatives to running an authority server in node. 
  - This repo has a node.js and Go implementation of an HTTP endpoint that receives a ProseMirror document and array of steps, hydrates them using a specific ProseMirror schema, applies the steps to the document, and returns the results. 
  - The benchmark scripts start each server, and send requests to them, collecting latency information.
  - Results: 

- https://gitlab.com/emergence-engineering/blog/-/tree/master/articles/prosemirror-sync-1 /202101/ts
  - using a sync database ( PouchDB, but it works with firebase ) as a communication layer between client and server.
  - [Article / code about prosemirror collab & PouchDB_202007](https://discuss.prosemirror.net/t/article-code-about-prosemirror-collab-pouchdb/3045)
  - [Collaborative text editor with ProseMirror and a syncing database_202007](https://emergence-engineering.com/blog/prosemirror-sync-1)

- https://gitlab.com/mpapp-public/manuscripts-sync
  - https://gitlab.com/mpapp-public/library-sync
  - https://gitlab.com/mpapp-public/pouchdb-replication
  - tests for a Couchbase Sync Gateway instance configured to act as a realtime synchronisation backend, from the frontend application interacted with using RxDB / PouchDB.

- https://github.com/microsoft/FluidFramework/tree/main/examples/data-objects/prosemirror
  - An experimental implementation of how to take the open source ProseMirror rich text editor and enable real-time coauthoring using the Fluid Framework.
  - Fluid Framework is a library for building distributed, real-time collaborative web applications using JavaScript or TypeScript.
# tiptap.v1、vue2 实现协作的示例
- https://github.com/dekunma/tiptap-collaboration
  - 包含client+server
- https://github.com/powlaa/text-editor
  - 包含client+server
- [A simple implementation of prosemirror-collab for tiptap.v1](https://discuss.prosemirror.net/t/a-simple-implementation-of-prosemirror-collab/1930)

- https://github.com/naept/tiptap-collab-server
  - https://github.com/naept/tiptap-extension-collaboration
  - A socket.io server for tiptap collaboration module. Handles multi-documents, users's cursors, and hooks for programmers.
  - [Build a multi-document collaborative text editor with Tiptap and Socket.io_202009](https://www.naept.com/en/blog/build-a-multi-document-collaborative-text-editor-with-tiptap-and-socket-io/)
# crdt/yjs
- https://github.com/yjs/y-prosemirror
  - ProseMirror editor binding for Yjs

- https://github.com/reactivepad/use-yjs-prosemirror /apache2/202212/ts/inactive
  - use-yjs-prosemirror

- https://github.com/idealjs/chao-feng
  - 依赖 yjs

- https://github.com/nandit123/crdt-text-editor-2
  - https://github.com/FleekHQ/crdt-text-editor
  - A p2p decentralized text-editor based on CRDTs
  - 依赖y-prosemirror、lit-html

- https://github.com/mweidner037/list-positions-demos/tree/master/websocket-prosemirror-log /MIT/202404/ts
  - A basic collaborative rich-text editor using list-positions, a WebSocket server, and ProseMirror. 
  - It supports arbitrary schemas and works similarly to ProseMirror's built-in collaboration system, using a server-authoritative log of changes.

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

- https://github.com/ShenQingchuan/HeteroDoc
  - Heterocube Cloud Collaborative Docs. Built with Vue3 + TypeScript + ProseMirror + Y.js + DeepKit
# ot-like/prosemirror-collab
- bear-plus /5Star/ISC/202008/js/ejs/inactive
  - https://github.com/yk9331/bear-plus
  - https://bear-plus.yenchenkuo.com/@bear-plus/features
  - 依赖codemirror.v5、express、markdown-it、sequelize、express、multer
  - A web-based writing application with real-time collaboration and Markdown syntax support for crafting and sharing notes. 
  - Group and find note easily with hashtag and full text search. Inspired by Bear note and HackMD.

- https://github.com/li-yechao/paper-collab
  - Backend of the rich editor paper-editor.

- https://github.com/stepwisehq/prosemirror-collab-commit /MIT/202307/ts/inactive
  - Commit-based collaborative editing plugin for ProseMirror
  - [ProseMirror Collab Performance | Blog _202307](https://stepwisehq.com/blog/2023-07-25-prosemirror-collab-performance/)

- https://github.com/benaubin/prosemirror-collab-plus /202008/ts/inactive
  - Improvements over prosemirror-collab:
    - Server-side rebasing drastically reduces network round-trips
    - Steps are queued and sent as commits, reducing overhead
    - When possible, steps are merged prior to network transport

- eg
   - https://github.com/mms-gianni/prosemirror-collaborationserver
    - https://github.com/mms-gianni/tiptap-collaboration-demo
    - 依赖 tiptap.v1、vue2
# more-collab
- https://github.com/sakheli/sync-doc
  - 未实现实时协作
