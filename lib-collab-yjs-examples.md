---
title: lib-collab-yjs-examples
tags: [collaboration, examples, toc, yjs]
created: 2022-09-21T15:47:19.673Z
modified: 2022-09-21T15:47:41.340Z
---

# lib-collab-yjs-examples

# guide

# yjs-examples
- https://github.com/jaqarrick/yjs-lab
  - This repo serves as an in-depth explanation of Yjs.

- https://github.com/ToolJet/yjs-crdt-game
  - [Building a realtime multiplayer game using React & Yjs + y-webrtc](https://blog.tooljet.com/multiplayer-tic-tac-toe-using-react-crdt-yjs/)

- https://github.com/dairyisscary/syn
  - Syn is a demo box drawing application that utilizes CRDTs, in this case Yjs.

- https://github.com/jaqarrick/yjs-canvas
  - Collaborative canvas using Yjs CRDT
# yjs-utils

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
# yjs-bindings
- https://github.com/joebobmiles/y-react
  - React bindings for Yjs.

- https://github.com/joebobmiles/yjson
  - YJSON wraps yjs to make using Yjs as simple as working with Plain Data Objects.

- https://github.com/YPAKK/crdt-backend
  - Example of horizontally scalable websocket backend for y-js to be used with y-websocket provider with persitence to postgresql using knex.

- https://github.com/sanalabs/collaboration-kit
  - packages that facilitate working with arbitrary JSON structures in Yjs
  - @sanalabs/y-redux Two-way sync of Redux and Yjs
- ref-redux-yjs
  - [Yjs Redux binding](https://discuss.yjs.dev/t/yjs-redux-binding/755)
  - https://github.com/lscheibel/redux-yjs-bindings

- https://github.com/joebobmiles/zustand-middleware-yjs
  - Zustand middleware that enables sharing of state between clients via Yjs.
- ref-zustand-yjs
  - https://github.com/tandem-pt/zustand-yjs
# yjs-more

# collaborative
- https://github.com/yjs/yjs
  - https://docs.yjs.dev/
  - Yjs is a CRDT implementation that exposes its internal data structure as shared types. 
  - Shared types are common data types like Map or Array with superpowers: changes are automatically distributed to other peers and merged without merge conflicts.

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
  - [hypercore and Yjs : how to make them work together](https://github.com/hypercore-protocol/hypercore/issues/296)
    - the y-dat implementation does not actually use the core feature of the hypercore’s append only merkle tree signed log, due to the mutable nature of the Yjs CRDT implementation.
