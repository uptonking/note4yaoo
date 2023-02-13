---
title: lib-collab-yjs-examples
tags: [collaboration, examples, toc, yjs]
created: 2022-09-21T15:47:19.673Z
modified: 2022-09-21T15:47:41.340Z
---

# lib-collab-yjs-examples

# guide

# popular-yjs
- https://github.com/closeally/yjs-server
  - An extensible, y-websocket-compatible server. Written in TypeScript. Supports authentication. ESM-only.
  - server included in y-websocket is limited in its capabilities: it is difficult to extend from the outside, tests are missing, authentication is not easy to implement

- https://github.com/kapv89/yjs-scalable-ws-backend
  - This repo is a slightly reworked websocket server found in the y-websocket repo
  - Example of horizontally scalable websocket backend for y-js to be used with y-websocket provider with persistence to postgresql using knex. 
  - Uses redis-pubsub for horizontal scaling and uses redis-queues to provide eventual-consistency and better behaviour when users join a document being edited by other users.
  - https://github.com/kapv89/yjs-scalable-ws-backend-test

- https://github.com/yousefed/SyncedStore
  - https://syncedstore.org/docs/
  - SyncedStore CRDT is an easy-to-use library for building live, collaborative applications that sync automatically.
  - SyncedStore builds directly on Yjs and Reactive. 
  - It's also inspired by and builds upon the amazing work by MobX and NX Observe.
  - SyncedStore is built as part of TypeCell.
  - So far, we've focused mostly on how to change to state on a synced store, and how to listen (react to) changes and display them in your application.
    -  When you update data on the store, an incremental change, or update is captured and can be shared between users. These updates can be shared between users of your application with different Sync Providers. 
  - y-indexeddb for offline storage​
    - persists document updates to the browsers indexeddb database. 
    - The document is immediately available and only diffs need to be synced through the network provider.
  - https://github.com/YousefED/reactive
    - A super simple, yet powerful and performant library for State Management / Reactive Programming.

- https://github.com/ueberdosis/hocuspocus
  - 

- https://github.com/BitPhinix/slate-yjs
  - https://docs.slate-yjs.dev/
  - Slate-yjs aims to be the goto collaboration solution for slate. 
  - Slate-yjs will overwrite the current editor value with the state contained in the shared type.

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
# yjs-utils
- https://github.com/pluv-io/pluv
  - Multi-platform, E2E type-safe realtime packages
  - Pluv. IO allows you to build real-time collaborate features with a fully end-to-end type-safe api.
  - Inspired by trpc, Built with yjs

- https://github.com/JonnysCode/y-solid
  - An experimental Solid protocol provider for Yjs
# yjs-apps
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

- https://github.com/motifland/yfs
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

- https://github.com/josephg/reference-crdts
  - This repository contains simple proof-of-concept reference implementations of yjs, automerge and sync9's list types - all implemented in the same codebase. 

- https://github.com/YousefED/reactive-crdt
  - It's built on top of Yjs, a proven, high performance CRDT implementation.

- https://github.com/inkandswitch/peritext
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - This repo includes:
    - A Typescript implementation of the core Peritext CRDT algorithm
    - A prototype integration with the [Prosemirror](http://prosemirror.net/) editor library
    - An interactive demo UI where you can try out the editor
    - A test suite

- https://github.com/yjs/y-codemirror.next
  - https://demos.yjs.dev/codemirror/codemirror.html
  - Collaborative extensions for CodeMirror6
# collab-non-yjs
- https://github.com/hypercore-protocol/hypercore /202211/js
  - a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data
  - [hypercore and Yjs : how to make them work together](https://github.com/hypercore-protocol/hypercore/issues/296)
    - the y-dat implementation does not actually use the core feature of the hypercore’s append only merkle tree signed log, due to the mutable nature of the Yjs CRDT implementation.
