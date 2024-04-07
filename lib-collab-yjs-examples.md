---
title: lib-collab-yjs-examples
tags: [collaboration, examples, toc, yjs]
created: 2022-09-21T15:47:19.673Z
modified: 2022-09-21T15:47:41.340Z
---

# lib-collab-yjs-examples

# guide

# popular
- https://github.com/closeally/yjs-server
  - An extensible, y-websocket-compatible server. Written in TypeScript. Supports authentication. ESM-only.
  - server included in y-websocket is limited in its capabilities: it is difficult to extend from the outside, tests are missing, authentication is not easy to implement

- https://github.com/kapv89/yjs-scalable-ws-backend
  - This repo is a slightly reworked websocket server found in the y-websocket repo
  - Example of horizontally scalable websocket backend for y-js to be used with y-websocket provider with persistence to postgresql using knex. 
  - Uses redis-pubsub for horizontal scaling and uses redis-queues to provide eventual-consistency and better behaviour when users join a document being edited by other users.
  - https://github.com/kapv89/yjs-scalable-ws-backend-test

- https://github.com/dev-badace/textrdt /202304/ts
  - a basic implementation of a text crdt based on the yata this is not meant to be used in production

- https://github.com/yousefed/SyncedStore
  - https://syncedstore.org/docs/
  - SyncedStore CRDT is an easy-to-use library for building live, collaborative applications that sync automatically.
  - SyncedStore builds directly on Yjs and Reactive. 
  - It's also inspired by and builds upon the amazing work by `MobX` and NX Observe.
  - mobx是可选的
  - SyncedStore is built as part of TypeCell.
  - So far, we've focused mostly on how to change to state on a synced store, and how to listen (react to) changes and display them in your application.
    -  When you update data on the store, an incremental change, or update is captured and can be shared between users. These updates can be shared between users of your application with different Sync Providers. 
  - y-indexeddb for offline storage​
    - persists document updates to the browsers indexeddb database. 
    - The document is immediately available and only diffs need to be synced through the network provider.
  - https://github.com/YousefED/reactive
    - A super simple, yet powerful and performant library for State Management / Reactive Programming.

- https://github.com/ueberdosis/hocuspocus
  - server

- https://github.com/BitPhinix/slate-yjs
  - https://docs.slate-yjs.dev/
  - Slate-yjs aims to be the goto collaboration solution for slate. 
  - Slate-yjs will overwrite the current editor value with the state contained in the shared type.

- https://github.com/WindrunnerMax/Collab
  - 初探富文本之OT协同实例 sharedb+quill
  - 初探富文本之CRDT协同实例 yjs+quill

- https://github.com/jaqarrick/yjs-lab
  - This repo serves as an in-depth explanation of Yjs.

- https://github.com/ToolJet/yjs-crdt-game
  - [Building a realtime multiplayer game using React & Yjs + y-webrtc](https://blog.tooljet.com/multiplayer-tic-tac-toe-using-react-crdt-yjs/)

- https://github.com/pengx17/yjs-textarea-demo
  - A nearly full featured YJS demo on textarea
- https://github.com/Jlg1128/yjs-textarea-react
  - Yjs在textarea上的应用，基于vite和React

- https://github.com/dairyisscary/syn
  - Syn is a demo box drawing application that utilizes CRDTs, in this case Yjs.

- https://github.com/jaqarrick/yjs-canvas
  - Collaborative canvas using Yjs CRDT

- https://github.com/hockyy/peertocp /202211/js
  - Electron Project for WebRTC Based Code Editor, Compiler, and C++ runner
  - CRDT Peer-to-Peer Branch using modified y-webrtc
  - CRDT Client-Server Branch using modified y-websocket
  - Operational Transformation Client-Server Branch using `@codemirror/collab` OT, based on Codemirror Collab Website Example for code editor

- https://github.com/drifting-in-space/y-sweet /MIT/rust/ts
  - https://y-sweet.dev/
  - A standalone yjs server with persistence to S3 or filesystem.
  - building on the excellent y-crdt library
  - Persists document data to a network filesystem or S3-compatible storage, inspired by Figma’s infrastructure.
  - Scales horizontally with a session backend model.
  - Provides document-level access control via client tokens.
# utils
- https://github.com/WaiSiuKei/yjs-devtools-formatter /MIT/202401/ts
  - A Chrome DevTools formatter for Yjs.
  - It makes the Yjs data types printed in the Chrome DevTools console easier to read and inspect, allowing developers to inspect Yjs data types just as they do with primitive data types.

- https://github.com/rozek/y-lwwmap /MIT/202307/ts/inactive
  - Yjs provides a complete ecosystem for (persisting and) sharing "Conflict-free replicated data types" (CRDT) among multiple clients using a variety of persistence and communication providers. 
  - The shared data types include arrays and maps, with shared maps becoming inefficient in most practical cases, which is why there is an alternative implementation based on shared arrays in the `y-utility` package.
  - Being compatible to the Yjs ecosystem, LWWMaps can be shared as part of a Y. Doc using y-websocket, y-webrtc
  - Its implementation is based on that of `YKeyValue` but uses a "last-write-wins" strategy during synchronization

- https://github.com/samwillis/yjs-sqlite-test
  - http://samwillis.co.uk/yjs-sqlite-test/
  - This is a test project to combine yjs and sqlite wasm, it lets you store yjs documents in a sqlite database, update them in place and query the content. 
  - Perfect for building a local first web app.

- https://github.com/maxpert/sqlite-y-crdt /MIT/202212/rust/js/inactive
  - WIP for wrapping Y-CRDT for SQLite

- https://github.com/pluv-io/pluv /MIT/202403/ts/yjs
  - https://pluv.io/
  - allows you to build real-time collaborate features with a fully end-to-end type-safe api.
  - Inspired by trpc, Built with yjs
  - @pluv/io, @pluv/client, @pluv/crdt-yjs and @pluv/react all require yjs as a peer dependency.
  - https://github.com/pluv-io/pluv-example

- https://github.com/JonnysCode/y-solid
  - An experimental Solid protocol provider for Yjs

- https://github.com/jupyter-server/pycrdt /MIT/202312/python/rust
  - https://davidbrochart.github.io/pycrdt
  - CRDTs based on Yrs
# apps
- https://github.com/cybersemics/em /ts/yjs/web/ios/android
  - minimalistic note-taking app for personal sensemaking.
# examples
- yboard /301Star/MIT/202206/js/vue
  - https://github.com/felipeleivav/yboard
  - https://yboard.lol/
  - Yboard is a multiplayer desktop-like workspace based on Yjs
  - Yboard is a frontend-only project. Only requisite is a [websocket server](https://github.com/yjs/y-websocket).
  - Yboard directly connects to websocket server
  - There is no authentication mechanisms nor additional backend logic implemented
  - All the rooms are publicly accessible (only protected by a random unique id, thanks nanoid)
  - Since a room is basically a shared document, any user could eventually rewrite the whole document by writing their own client application

- https://github.com/Rishabh-malhotraa/caucus
  - Realtime Collaborate Editor with Embedded Compiler
  - 类似协作codepen
  - Built With React Material UI yjs Written in TypeScript
  - 依赖knex、pg、yjs、codemirror5

- https://github.com/Motif-Archived/yfs /MIT/202301/ts/inactive
  - https://yfs.vercel.app/
  - Synchronize text files between the browser and the file system using the File System Access API and Yjs.
  - 依赖yjs.v13、idb-keyval、diff、react
  - 前端示例依赖 @monaco-editor/react、next

- https://github.com/benfoxall/ycode
  - Edit your local files with remote people.
  - yjs + monaco-editor + file-system-access api

- https://github.com/jackyzha0/cursor-chat
  - Built on top of yjs and perfect-cursors

- https://github.com/nimeshnayaju/yjs-tldraw
  - multiplayer implementation on tldraw using yjs.

- https://github.com/malte-j/piko.space /202312/ts/inactive
  - https://piko.space/
  - Collaborate at the speed of light and seamlessly sync offline work

- https://github.com/haggen/hindsight
  - Hindsight is a retrospective board for Scrum practitioners.
  - No back-end. Data is encrypted and shared directly between connected browsers.
# yjs-bindings
- https://github.com/joebobmiles/y-react
  - React bindings for Yjs.
  - a set of React components and React hooks for working with Yjs in an idiomatic way.

- https://github.com/joebobmiles/yjson
  - YJSON wraps yjs to make using Yjs as simple as working with Plain Data Objects.
- https://github.com/boourns/y-pojo
  - Syncronize a YJS document to/from a plain old javascript object

- https://github.com/sanalabs/collaboration-kit
  - packages that facilitate working with arbitrary JSON structures in Yjs
  - @sanalabs/y-redux Two-way sync of Redux and Yjs
- ref-redux-yjs
  - [Yjs Redux binding](https://discuss.yjs.dev/t/yjs-redux-binding/755)

- https://github.com/lscheibel/redux-yjs-bindings
  - This very small (roughly 1kB) bridge to connect Redux with a Yjs, allows you to use the synchronization features of Yjs with the data management capabilities of Redux. 
  - It works with any Redux store, whether you use Redux Toolkit or not, and even supports initial values. 
  - Values that are transmitted over the network can be any JSON serializable value, from primitives to deeply nested object structures.

- https://github.com/YousefED/nostr-crdt
  - an experiment to run decentralized, collaborative (multiplayer) apps over nostr. 
  - CRDT application updates are sent as Nostr events.

- https://github.com/joebobmiles/zustand-middleware-yjs
  - Zustand middleware that enables sharing of state between clients via Yjs.

- yjs-state-management
  - https://github.com/tandem-pt/zustand-yjs
  - https://github.com/dai-shi/valtio-yjs
  - https://github.com/astahmer/jotai-yjs

- https://github.com/YPAKK/crdt-backend
  - Example of horizontally scalable websocket backend for y-js to be used with y-websocket provider with persitence to postgresql using knex.
# yjs-crdt
- https://github.com/yjs/yjs
  - https://docs.yjs.dev/
  - Yjs is a CRDT implementation that exposes its internal data structure as shared types. 
  - Shared types are common data types like Map or Array with superpowers: changes are automatically distributed to other peers and merged without merge conflicts.
  - 🍴 forks
  - https://github.com/sthagen/yjs-yjs

- https://github.com/josephg/reference-crdts
  - This repository contains simple proof-of-concept reference implementations of yjs, automerge and sync9's list types - all implemented in the same codebase. 

- https://github.com/YousefED/reactive-crdt
  - It's built on top of Yjs, a proven, high performance CRDT implementation.

- https://github.com/yjs/y-codemirror.next
  - https://demos.yjs.dev/codemirror/codemirror.html
  - Collaborative extensions for CodeMirror6
# collab-non-yjs
- https://github.com/hypercore-protocol/hypercore /202211/js
  - a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data
  - [hypercore and Yjs: how to make them work together](https://github.com/hypercore-protocol/hypercore/issues/296)
    - the y-dat implementation does not actually use the core feature of the hypercore’s append only merkle tree signed log, due to the mutable nature of the Yjs CRDT implementation.
