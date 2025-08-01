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

- https://github.com/wangfupeng1988/collab-demo-prosemirror /202408/js
  - using prosemirror and yjs

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

- https://github.com/filipe-freire/live-collaboration-editor-fe /202501/ts
  - An implementation of a live collaboration feature in a Rich Text Editor environment, using Web Sockets
  - Persisted changes across sessions (leveraging SQLite's power and might).
  - https://github.com/filipe-freire/live-collaboration-editor-be
    - An Express backend built to support a live collaboration environment through Web Sockets
    - Express-WS

- https://github.com/scenaristeur/noosphere /202210/js/vue
  - https://scenaristeur.github.io/noosphere
  - 依赖milkdown.v6、vue2、bootstrap-vue.v2、remark-directive、three、yjs
  - https://github.com/scenaristeur/noosphere2 /202306/js/vue
    - A simple example for using milkdown with vue.

- https://github.com/cwwojin/CRDT-text-editor /MIT/202501/ts
  - Real-time document editor based on Yjs, Prosemirror, MongoDB, Redis, Next.js
# diff/track-change
- https://github.com/handlewithcarecollective/prosemirror-suggest-changes /28Star/MIT/202507/ts
  - https://handlewithcarecollective.github.io/prosemirror-suggest-changes/
  - A ProseMirror library for enabling Google Docs-style suggestions
  - This library provides three mark types: insertion/deletion/modification

- https://github.com/davefowler/prosemirror-suggestion-mode /22Star/MIT/202503/ts
  - A ProseMirror plugin that implements a "suggestion mode" method to track and show changes similar to Google Docs and Word. 
  - This plugin allows users to make suggested edits that can be reviewed, accepted, or rejected later.
  - https://github.com/davefowler/prosemirror-suggestion-mode-examples

- https://github.com/Atypon-OpenSource/manuscripts-track-changes-plugin /202311/ts
  - ProseMirror plugin to track inserts/deletes to nodes and text.

- https://github.com/TeemuKoivisto/prosemirror-track-changes-example /202108/ts/inactive
  - https://teemukoivisto.github.io/prosemirror-track-changes-example/
  - simple track-changes example with prosemirror-changeset
  - [Question about track-changes with prosemirror-changeset](https://discuss.prosemirror.net/t/question-about-track-changes-with-prosemirror-changeset/3801)

- https://github.com/milahu/prosemirror-track-changes-demo /CC-1.0/202409/js/inactive
  - https://milahu.github.io/prosemirror-track-changes-demo/
  - add a "track changes" feature to prosemirror

- https://github.com/newsdev/prosemirror-change-tracking-prototype /201609/js
  - ProseMirror change tracking proof-of-concept

- https://github.com/nytimes/prosemirror-change-tracking-prototype /23Star/apache2/201609/js/inactive
  - a basic implementation of change tracking for ProseMirror
  - This project is a prototype built to explore the possibility of porting track changes to ProseMirror. 

- https://github.com/chenyuncai/tiptap-track-change-demo /vue
  - https://track-change.onrender.com/
  - [Implement new track changes in current document, just lice office review mode](https://discuss.prosemirror.net/t/implement-new-track-changes-in-current-document-just-lice-office-review-mode/4890)
  - https://github.com/chenyuncai/tiptap-track-change-extension /MIT/202308/ts/inactive

- https://github.com/bsachinthana/tiptap-diff-suggestions /MIT/202507/ts
  - A TipTap extension for inline comparison of content with suggested revisions, including interactive controls.
  - This extension provides a way to visualize and interact with suggested changes within a TipTap editor. 
  - It bridges the gap between static diff viewers and actionable content editing, allowing users to evaluate, accept, or reject suggestions directly in the editor.
  - Interactive Diff Visualization: Inline comparison with accept/reject controls
  - Framework Agnostic: Leverages TipTap's framework-agnostic architecture

- https://github.com/hamflx/prosemirror-diff /202207/js/inactive
  - 支持保留新版本状态的标记
- https://github.com/pubpub/prosemirror-diff /201907/ts/inactive
- https://codesandbox.io/p/sandbox/prosemirror-diff-forked-9trmjq

- https://github.com/ItaZure/TiptapBasedRichtextDiff /202507/js
  - 基于 Tiptap 的富文本差异对比工具，支持文本内容和格式变化的可视化对比，以及文档评注功能。
  - 字符级别对比：精确到每个字符的差异检测
  - 将 Tiptap 的 JSON 文档结构展平为字符数组，每个字符携带格式信息。
  - 差异检测: 使用最长公共子序列（LCS）算法进行基础差异检测
    - 目前只支持段落（paragraph）节点的对比
    - 不支持列表、表格等复杂结构
# versioning
- https://github.com/inkandswitch/upwelling-code /ts
  - https://upwelling-prototype.netlify.app/
  - [Upwelling: Combining real-time collaboration with version control for writers](https://www.inkandswitch.com/upwelling/)
  - 依赖@atjson/document、@atjson/renderer-react、prosemirror

- https://github.com/dipesh162/Versioned-Rich-Text-Editor /202505/ts
  - https://versioned-rich-text-editor.vercel.app/
  - A full-featured, collaborative document editor built using React, TypeScript, and TipTap (ProseMirror), designed to support version control and branching timelines. 
  - This project demonstrates advanced state management, real-time UI updates, and a creative approach to document versioning and branching workflows in the browser.

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
- https://github.com/saranrapjs/prosemirror-json-patch-demo /MIT/202301/ts/inactive
  - illustrating a ProseMirror-unaware approach to generating JSON patch patches, given only an input doc and a set of ProseMirror steps applied to that doc.

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

- https://github.com/dev-badace/live-text-crdt /202307/ts/inactive
  - https://livetext-delta.vercel.app/
  - A Text Crdt implementation on top of the liveblocks platform, and tiptap (prosemirror) text editor
# collab-tiptap
- https://github.com/ueberdosis/y-tiptap /MIT/202507/js
  - Tiptap Binding for Yjs
  - This binding maps a Y. XmlFragment to the ProseMirror state.
  - We forked `y-prosemirror` to create a Tiptap-specific package with changes we needed for Tiptap-related features. 
    - These modifications were too specific to be merged upstream 
  - Shared Undo / Redo (each client has its own undo-/redo-history)
  - Successfully recovers when concurrents edit result in an invalid document schema

## tiptap.v1、vue2 实现协作的示例

- https://github.com/dekunma/tiptap-collaboration
  - 包含client+server
- https://github.com/powlaa/text-editor
  - 包含client+server
- [A simple implementation of prosemirror-collab for tiptap.v1](https://discuss.prosemirror.net/t/a-simple-implementation-of-prosemirror-collab/1930)

- https://github.com/naept/tiptap-collab-server /MIT/202011/js/inactive
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

- https://github.com/fadiquader/prosemirror-collaborative-editor /202303/js/inactive
  - collaborative editor for React built with Prosemirror + Yjs + mongodb

- https://github.com/tororosoba0534/collab-note-yjs-wsserver
  - Collab-Note-YJS is a multi-repo project which divided by two repositories (frontend and backend). 

- https://github.com/loro-dev/loro-prosemirror /MIT/202406/ts
  - Prosemirror Binding for Loro
  - Sync document state with Loro
  - Sync cursors with Loro's Awareness and Cursor
  - https://x.com/loro_dev/status/1798722084342018282
    - I have a question regarding Loro - and maybe CRDTs in general: Is it common to have (whatever kind of) state handling that then syncs with Loro and back (that's how you do it for the tldraw example, but of course that's because that's "on top" of an existing app) or would you recommend building your state with Loro from the get go?
    - For example, I'm working on an image editor that uses mobx-state-tree - that has support for listening to, replaying and applying patches following the JSON Patch spec, which should, I think, work well with Loro (haven't tried yet, though). 
    - I think both modes are feasible. However, if I had to choose, I would prefer to use Loro CRDT as the source of truth, with writes also being made directly to Loro CRDT.  This would establish a unidirectional data flow from CRDTs to other application states.
    - Currently, we don't have more complex open-source projects based on Loro to refer to; the most complex one at the moment seems to be this ProseMirror binding.

- https://github.com/automerge/automerge-prosemirror /108Star/MIT/202507/ts
  - Collaborate on rich text documents which follow the rich text schema using ProseMirror.
  - This library provides a plugin which maps between Automerge documents and ProseMirror documents. 
  - This plugin relies on two things: 
    - firstly that the schema you use be a very specific subset of the ProseMirror schema which is mapped to the Automerge rich text schema (more on this later), 
    - and secondly that you initialize the ProseMirror document from the Automerge document.
  - https://github.com/automerge/prosemirror-quickstart

- https://github.com/saranrapjs/prosemirror-automerge /201904/js/inactive
  - experiment with wiring automerge up to ProseMirror
  - The basic idea is to have a ProseMirror plugin that works similarly to the collab plugin: steps which originate from the editor are translated to an Automerge document, and changes to a "remote" Automerge document are translated back to the ProseMirror document as steps.
  - https://github.com/alexjg/automerge-prosemirror-demo

- https://github.com/ShenQingchuan/HeteroDoc /202305/ts/inactive
  - Heterocube Cloud Collaborative Docs. Built with Vue3 + TypeScript + ProseMirror + Y.js + DeepKit
  - https://github.com/zhoujiangang0911/HeteroDoc

- https://github.com/get-convex/prosemirror-sync /apache2/202507/ts
  - Sync prosemirror documents with Convex for server-authorized collaborative editing

- https://github.com/soumith2105/collab.md /202503/ts
  - A realtime collaborative markdown editor built with React, Yjs, and Prosemirror.
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
   - https://github.com/mms-gianni/prosemirror-collaborationserver
    - https://github.com/mms-gianni/tiptap-collaboration-demo
    - 依赖 tiptap.v1、vue2
# more-collab
- https://github.com/sakheli/sync-doc
  - 未实现实时协作
