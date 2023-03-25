---
title: lib-collab-crdt-examples
tags: [collaboration, crdt, examples]
created: 2022-01-22T16:14:32.323Z
modified: 2022-04-05T10:08:25.947Z
---

# lib-collab-crdt-examples

# guide

- ref
  - https://github.com/alangibson/awesome-crdt
  - [CRDTs for Non Academics - YouTube](https://www.youtube.com/watch?v=vBU70EjwGfw)
# popular
- https://github.com/pubuzhixing8/awesome-collaboration
  - Collaborative editing of technical resources, article translation
  - [OT 与 CRDT 的Battle，堪称神仙打架](https://github.com/pubuzhixing8/awesome-collaboration/blob/master/fairy-fight/collaborative-editing.md)

- evolu /101Star/GPLv3/202210/ts
  - https://github.com/evoluhq/evolu
  - https://www.evolu.dev/
  - React Hooks library for local-first software with end-to-end encrypted backup and sync using SQLite and CRDT
  - writing local-first software has been challenging because of the lack of libraries and design patterns. I personally failed several times, and that's why I created Evolu.
  - Evolu architecture is almost a clone of James Long CRDT for mortals. Rewritten and improved
  - Evolu uses end-to-end encryption and generates strong and safe passwords for you. 
    - Evolu sync and backup server see only timestamps. Nothing more. 
    - We plan to do at least two security audits.
  - Evolu is not pure P2P software. For syncing and backup, there needs to be a server. 
  - Evolu CRDT has no support for transactions because CRDT transactions are still an unsolved issue. 

- FluidFramework /4.2kStar/MIT/202302/ts
  - https://github.com/microsoft/FluidFramework
  - https://fluidframework.com/
  - Library for building distributed, real-time collaborative web applications
  - 示例未渲染协作鼠标
  - 依赖中心服务器转发op及定顺序
  - 不支持长时间的offline
  - [Does Fluid use CRDT?](https://fluidframework.com/docs/faq/#does-fluid-use-crdt)
    - Fluid does not use Conflict-Free Replicated Data Types (CRDTs), but our model is more similar to CRDT than OT. 
    - The Fluid Framework relies on update-based operations that are ordered using our Total Order Broadcast to prevent conflicts. 
    - This allows us to have non-commutative operations because there is an explicit ordering.
    - [Doc: Is Fluid OT or CRDT?_202201](https://github.com/microsoft/FluidFramework/issues/8920)
    - The service part of Fluid is OT/CRDT agnostic and possibly of interest to CRDT developers looking for a managed backend solution.
    - Some of the built-in Fluid DDS implementations may be of general interest to CRDT researchers.
  - What kind of support is there for real-time editing of text?
    - This is the scenario that Fluid was first designed to support. 
    - Consequently, the Fluid Framework is an ideal foundation for rich text editors that support simultaneous editing by multiple clients. 
    - The `SharedString` DDS is tailor-made for this scenario.
  - [Microsoft introduces Loop: A new collaboration tool built on Fluid Framework_202111](https://www.zdnet.com/article/microsoft-introduces-loop-a-new-collaboration-tool-built-on-fluid-framework/)

- xi-editor /19.7kStar/apache2/202206/rust
  - https://github.com/xi-editor/xi-editor
  - https://xi-editor.io/
  - A modern editor with a backend written in Rust.
  - The xi-editor project is currently discontinued. 
  - CRDT: This approach follows WOOT.

- https://github.com/atom-archive/xray /rust
  - Text is stored in a copy-on-write CRDT.
    - We use a variant of RGA called RGASplit
  - Our current understanding is that in Xi, the buffer is stored in a rope data structure, then a secondary layer is used to incorporate edits. 
  - In Xray, the fundamental storage structure of all text is itself a CRDT.
    - It's similar to Xi's rope in that it uses a copy-on-write B-tree to index all inserted fragments, but it does not require any secondary system for incorporating edits.
  - [Xray – An experimental next-generation Electron-based text editor | Hacker News](https://news.ycombinator.com/item?id=16525735)

- https://github.com/zkpranav/crdt-sync-client /未完成
  - https://github.com/zkpranav/crdt-sync-server
  - Implementation of a CRDT based networking layer for a collaboration tool.
  - heavily inspired by Figma's implementation of their networking layer.
  - A Document consists of a set of objects structured in a hierarchical tree-like structure. 
    - Each Object has an associated ID which is globally unique, and a set of property-value pairs. 
    - Parent-Child relationships are maintained as a link from the child to its parent.

- harika-note /111Star/AGPLv3/202208/ts
  - https://github.com/quolpr/harika
  - Harika is an offline-first, performance-focused note taking app for organizing your knowledge database.
  - Synchronization with server. It's done with LWW CRDT per field on top of SQLite. 
    - It also stores all changes locally and sends them to server. 
    - Server also store all the changes and recalculate snapshots on new received changes and send those snapshots back to the client. 
    - Due to we store all the changes at server, it is also planned to add time travel, when CRDT is not what user expect at some cases.

- https://github.com/Horusiath/crdt-examples
  - An example implementations of various CRDTs，实现语言为F#
  - It serves mainly academic purposes (the implementations are meant to be simple and easy to understand, not optimized)

- https://github.com/josephg/crdt-benchmarks
  - The goal of this repository is to provide some standard benchmarks that we can use to compare the performance of various OT/CRDT implementations.
  - This repository contains some editing histories from real world character-by-character editing traces. 
    - [bench npm jumprope](https://gist.github.com/josephg/bcb2e74e52dc9c4651249fdffc48d1cf)
    - [bench-automerge.js code from blog post](https://gist.github.com/josephg/13efc1444660c07870fcbd0b3e917638)

- https://github.com/dmonad/crdt-benchmarks
  - A collection of reproducible CRDT benchmarks.
  - B1: No conflicts
  - B2: Two users producing conflicts
  - B3: Many conflicts
  - B4: Real-world editing dataset

- https://github.com/streamich/json-joy
  - JSON utilities for joy and collaborative editing with OT and CRDT approaches. 

- https://github.com/inkandswitch/peritext
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - Peritext builds upon RGA, which is similar to Causal Trees, although our algorithm could use any of these plain text CRDTs with minor adaptations. 
  - This repo includes:
    - A Typescript implementation of the core Peritext CRDT algorithm
    - A prototype integration with ProseMirror editor
    - An interactive demo UI where you can try out the editor
    - A test suite
  - forks
  - https://github.com/philschatz/peritext

- https://github.com/supabase/pg_crdt /rust
  - pg_crdt is an experimental extension adding support for conflict-free replicated data types (CRDTs) in Postgres.
  - It supports Yjs/Yrs and Automerge.
  - Our goal was to evaluate if we could leverage a Postgres-backed CRDT and Supabase's existing Realtime API for change-data-capture to enable development of collaborative apps on the Supabase platform.
  - pg_crdt extension is a proof-of-concept that wraps rust's yrs and automerge libraries using the pgx framework to add a Postgres native CRDT, crdt.ydoc.

- liveblocks /1.5kStar/apache2/202302/ts/服务端未开源
  - https://github.com/liveblocks/liveblocks
  - https://liveblocks.io/
  - The all-in-one toolkit to build collaborative products like Figma, Notion, and more.
  - 三大类数据：storage、presense、analytics
  - our Storage block is CRDTs based, but we're making different trade-offs.
    - our CRDTs are not "pure" so we solve some conflicts on the server. 
    - Also, we don't support Text CRDTs yet.
  - [Is the backend open source?_202211](https://github.com/liveblocks/liveblocks/discussions/570)
    - The backend is not open source. It might at some point, but not in the short term.
  - [Liveblocks: Add real‑time collaboration to your product in minutes_202107](https://news.ycombinator.com/item?id=27994480)
  - User permissions and privileges in a collaborative app are much easier to handle with a centralised server

- https://github.com/composablesys/collabs /ts
  - Collabs is a collections library for collaborative data structures. 
  - These are data structures that look like Set, Map, Array, etc., except they are synchronized between multiple users
  - https://github.com/composablesys/collabs-e2e-benchmark
  - [Collabs: Composable Collaborative Data Structures_2022](https://arxiv.org/abs/2212.02618)
  - https://twitter.com/matthewweidner3/status/1444475869121110017
    - Collabs is directly inspired by Automerge and Yjs, and uses similar techniques (network-agnostic CRDTs).  
    - The main difference is its API: we try to mimic a non-replicated collections library, with flexibility, composition tools, and strong typing.
# crdt-rewrite
- https://github.com/josephg/crdt-examples
  - CRDT examples from a DWEB talk

- https://github.com/jlongster/crdt-example-app  /201912/js
  - https://crdt.jlongster.com/client/
  - https://github.com/clintharris/crdt-example-app_annotated
  - A full implementation of CRDTs using hybrid logical clocks and a demo app that uses it
  - This is a demo app used for my dotJS 2019 talk "CRDTs for Mortals(普通人)"
  - It contains a full implementation of hybrid logical clocks to generate timestamp for causal ordering of messages. 
  - Using these timestamps, CRDTs can be easily used to change local data that also syncs to multiple devices. 
  - This also contains an implementation of a merkle tree(默克尔树) to check consistency of the data to make sure all clients are in sync.
  - It provides a server to store and retrieve messages, so that clients don't have to connect peer-to-peer.
  - Server: 132 lines of JS
  - Client: 639 lines of JS

- https://github.com/ipfs-shipyard/peer-crdt /js
  - collection of operation-based CRDTs that are meant to work over a p2p network.
  - 提供了多种类型，代码不复杂，无服务端
  - not maintained. Superseded by delta-crdts
  - [implement a delta state-based RGA sequence type](https://github.com/peer-base/js-delta-crdts/issues/3)
  - https://github.com/ipfs-shipyard/peer-crdt-example
    - nodejs
  - https://github.com/ipfs-shipyard/peer-crdt-textarea-binding
    - Bind a PeerCRDT treedoc-text object to a textarea.
  - https://github.com/ipfs-shipyard/peer-crdt-bind-codemirror

- https://github.com/peer-base/js-delta-crdts /js
  - Delta state-based CRDTs in Javascript.
  - https://github.com/itoumlilt/CRDT-Spreasheet
  - https://github.com/eugene-eeo/crunch-crdt-benchmarks
  - https://github.com/jimpick/delta-crdt-ordering-demo
  - https://github.com/jimpick/causual-playground
  - https://github.com/JMLX42/rust-delta-crdts
    - Delta state-based CRDTs in Rust.

- https://github.com/siliconjungle/delta-crdt /单文件
  - A simple delta CRDT implementation.

- https://github.com/streamich/json-joy
  - json-crdt中提供了rga、lww-object

## woot

- https://github.com/phedkvist/crdt-sequence
  - CRDT Sequence is a very basic collaborative text editing implementation
  - 自己实现了 history、activeUsers
  - quill的功能使用得很少
  - 依赖 react-quill
  - [Creating a Collaborative Editor_201906](https://pierrehedkvist.com/posts/1-creating-a-collaborative-editor)
    - This solution doesn't support interleaving
    - A better solution that is based of CRDT WOOT
  - https://github.com/PHedkvist/crdt-server

- https://github.com/phedkvist/crdt-woot /202204/ts
  - Implementation of collaborative editing algorithm CRDT WOOT.
  - 示例使用react-quill
  - https://github.com/phedkvist/crdt-server
  - [Collaborative Editing Using CRDTs](https://pierrehedkvist.com/posts/collaborative-editing-using-crdts)
  - [Introduction to Conflict Free Replicated Data-type](https://medium.com/swlh/introduction-to-conflict-free-replicated-data-type-959a944098c4)

- https://github.com/ryankaplan/woot-collaborative-editor
  - A real time collaboration toy project based on WOOT. Implemented with node.js and ws.
  - 编辑器使用textarea
  - When a textarea-change is detected, diff the textarea content against the last known content. 
  - With the help of WootTypes. WString, turn that diff into `WStringOperations` and broadcast those operations to the server.
  - When we receive operations from the server, apply those operations to our WString instance and apply them to the text in #collab-doc.

- https://github.com/t-mullen/woot-crdt
  - Replicate text or sequences over networks.
- https://github.com/t-mullen/logoot-crdt
  - Optimized Logoot CRDT implementation.
  - Implemented as a tree for fast character position lookups.
- https://github.com/kana-sama/edita
  - https://github.com/kana-sama/edita-server
  - 示例监听span文字的crud，未使用编辑器框架

- https://github.com/bcherny/crdt-demo
  - WOOT-style CRDT implementation
  - 👉🏻 提供了server，编辑器使用draftjs
  - WOOT propagates identifier-based operations defined on the internal object
- https://github.com/cindywu/baby-crdt
  - 基于woot

- https://github.com/phedkvist/crdt-server /ts/单文件
  - A text based CRDT server storing, sending and receiving updates using Express and Websockets
  - 基于ws创建连接，用数组存放changes
  - 初次连接发送所有changes
  - 后续只发送单次change的msg

## logoot

- https://github.com/mkdynamic/logoot
  - 👉🏻 包含服务端，编辑器使用textarea
  - Collaborative text editor using Logoot CRDT algorithm. 
  - Adds an informal versioning scheme based on state vectors to ensure casual ordering of operations is maintained.

- https://github.com/Martinn1996/Fonto-CRDT
  - Bachelor Project: CRDT for Fonto
  - Our CRDT is based on a logoot

## rga/causal-tree

- usecase
  - automerge
  - peritext

- https://github.com/maca/ace-crdt /js/rga
  - Collaborative text editor proof of concept using CRDT
  - 提供了server
  - [Question: how to create an RGA CRDT on server](https://github.com/maca/ace-crdt/issues/1)
- https://github.com/jorendorff/peeredit /201611/js/rga
  - Peeredit is a simple Web app that lets you edit some text online with friends.
  - This is example code for a talk on CRDTs.
  - 示例使用ace.v1编辑器
  - RGA - Replicated Growable Arrays
    - Operation-based CRDTs: arrays
    - where LSeq virtual pointers use byte sequences, in RGA it's just a combination of a single monotonically increasing number and replica identifier

- https://github.com/josephg/simple-crdt-text /ts
  - This implements automerge's underlying algorithm (RGA)
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.
  - [automerge-and-yjs-minimal.ts](https://gist.github.com/josephg/26ade72d5ced0470485c734fb1ebb6ca)
  - [yjs-minimal.ts](https://gist.github.com/josephg/dcb1bce2ceb0f0b50ffcac0245a55907)
  - [yjs_testcase.ts](https://gist.github.com/josephg/88c006724435a61afaec5ff3f1bacd87)

- https://github.com/josephg/reference-crdts
  - This repository contains simple proof-of-concept reference implementations of yjs, automerge and sync9's list types - all implemented in the same codebase. 

- https://github.com/jaredly/local-first/tree/master/packages/text-crdt
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.

## crdt-more

- https://github.com/dglittle/shelf
  - Here is a shelf: [VALUE, VERSION_NUMBER]
  - [josephg/shelf.ts](https://gist.github.com/josephg/c433d3bcc078d911e7696c6d64381bf1)

- https://github.com/gritzko/citrea-model /201712/js
  - A CRDT-based collaborative editor engine of letters.yandex.ru (2012, historical)
  - https://news.ycombinator.com/item?id=28018129
    - About a decade ago, I implemented the Causal Tree CRDT (aka RGA, Timestamped Insertion Tree) in regular expressions using a Unicode string as a storage. Later we made a collaborative editor for Yandex based on that code.
    - Recently(202107) I greatly improved CTs by introducing the Chronofold data structure
    - I remember seeing that (regex CTs) and immediately thinking "wtf, why would anyone want to do that". Took me quite a while to understand that it's actually a pretty clever way to write fast state machines in browserland. So thank you for this work!
- https://github.com/gritzko/swarm
  - Swarm is like "git for data" except it's real-time and never has a merge conflict. 
  - Swarm is based on Replicated Object Notation (RON), a distributed live data format.
  - RON is based on CRDT
- https://github.com/decentralized-hse/collab-edit /kotlin
  - the state of text and cursor positions are stored as Chronofold on each client. 
  - When the user updates the text or the cursor position on one client, it calculates diff via `diff-match-patch`, updates its Chronofold, and sends new operations to another client. 
  - Another client adds these operations to its Chronofold and updates the text and cursor positions accordingly.

- https://github.com/wangdashuaihenshuai/crdt-edit /201810/vue/js
  - [我自己从零实现的一个文本文档的协同编辑demo，上面是输入框，下面是数据结构的可视化](https://zhuanlan.zhihu.com/p/48229762)
  - 每个操作都是依赖前一个操作的结果，这样的数据结构就是有操作依赖生成的一颗 因果树
  - 依赖konva的画图app

- https://github.com/siliconjungle/tiny-merge
  - State-based CRDT with a Tiny footprint.
  - 包含server、client，服务端依赖supabase

- https://github.com/eugene-eeo/crunch-crdt-benchmarks /js
  - some crdt benchmarks
  - 比较了woot/logoot/lseq/rga/treedoc
- https://github.com/fdionisi/deno-crdt
  - Collection of CRDT written in TypeScript
  - 测试了 woot + logoot + rga
  - rga使用tree+doubly-linked-list+vector-clock
- https://github.com/orbitdb/crdts
  - 提供的都是简单类型
- https://github.com/dominictarr/crdt
  - Commutative Replicated Data Types for easy collaborative/distributed systems.
  - 提供了简单和复杂多个示例
  - https://github.com/adelriosantiago/easy-crdt
    - up-to-date real-time collaborative editor sample based on dominictarr/crdt
- https://github.com/liaujianjie/crdt
  - I will be using this repo to experiment with CvRDTs
- more-crdt-impl
  - https://github.com/streaver/crdt-examples

- https://github.com/patreu22/react-crdt
  - part of a bachelor thesis dealing with conflict-free data types in web development.
  - I implemented a shopping cart driven by a set of CRDTs 
  - You can use a toggle for setting a LWW-Register, increment/decrement a PN-Counter and add or remove elements to/from a Observed-Removed set.
  - 提供了服务端，依赖redux

- https://github.com/todo-tree/CRDT-Todo-Server
  - https://github.com/todo-tree/CRDT-Todo-Client
  - sync-database-front(use indexedDB + dexie + workbox)
  - sync-database-back(use mongoDB)

- https://github.com/llendo/crdt-app-server
  - https://github.com/llendo/crdt-app
  - 同步通过post operations
  - server基于mongoose

- https://github.com/mohe2015/crdt
  - yjs' implementation is probably quite good. maybe we can store less in memory? 
  - 基于cmrdt

- https://github.com/aizatto/crdt-prototype
  - Prototype to test implementing CRDT
  - 只搭建了测试结构，然后测试了diff，未引入crdt算法

- https://github.com/siliconjungle/crdt-likes
  - A simple example of how to build offline-first likes using CRDT's.
- https://github.com/siliconjungle/recycle-list-crdt
  - A crdt that recycles tombstones.
- https://github.com/siliconjungle/cabinet 
  - https://github.com/siliconjungle/cabinet-client
  - operation-based crdt，也提供了state-based的版本
  - 未提供服务端实现
  - A key value store & subscriptions wrapping a json blob crdt (shelf).
  - https://twitter.com/JungleSilicon/status/1504446998329499653
    - It's operation based but it's very easy to consume and cull(cull sth from sth 选出，挑出) those operations.
    - For anyone interested in collaborative editing, I've implemented a new approach to the shelf CRDT.

- https://github.com/coast-team/dotted-logootsplit
  - Most of the CRDT embeds metadata in order to avoid conflicting edits. The challenge is to keep these metadata as small as possible.
  - LogootSplit is a sequence CRDT which reduces the metadata of preceding sequence CRDT; to do so it aggregates elements
    - LogootSplit is an operation-based CRDT. 
    - Hence, it is necessary to use a network layer to deliver exactly-once the operations. 
    - It requires also to deliver removals after insertions. In practice, this is difficult to implement.
  - Delta-based CRDT have less assumptions. 
    - Most of delta-based CRDT simply assume a FIFO delivery (deltas from a same replica, are merged in-order). 
    - They also enable to merge two states.
  - Dotted LogootSplit offers a delta-based version of LogootSplit with smaller metadata. We provide both op-based and delta-based synchronizations.
  - Dotted LogootSplit is a replicated data structure designed for collaborative editing. The data structure combines a search tree and a rope.

- https://github.com/SDharan93/replicated-document
  - A replicated document that allows collaborative editing. 
  - This document is built on the CRDT algorithm "Logoot". 

- https://github.com/nkohari/kseq
  - KSeq is an implementation of a simple CRDT that represents an ordered sequence of items. 
  - KSeq is an operations-based, continuous sequence CRDT based on the Logoot and LSEQ systems.
  - Designed for use in collaborative editors, it allows various contributors to concurrently alter the sequence, while preserving both data and intent.

- https://github.com/Timothy-Harianja/CRDT-Collaboration-App
  - This project is aimed to experiment on the capabilities of CRDT and OT. 
  - One of the practical uses out these concepts is offline collaboration feature.
  - 依赖automerge

- https://github.com/tobiasbrodd/crdt
  - 编辑note，每次发送全量数据
  - 只实现了socket.io的传输过程，本地未先执行

- https://github.com/marcello3d/trimerge-sync
  - implement synchronization using the trimerge algorithm.
  - Conflicts are resolved on the client side (as in @mweststrate's “Distributing state changes using snapshots, patches and actions”)
  - Data structure design can limit conflicts (as in CRDT)
  - Limitations:
    - Assumes application is built on immutable data structures
    - Does not scale to high number of concurrent edits (conflict thrashing)
    - Requires the full document model to be in all clients' memory
  - https://github.com/marcello3d/trimerge
    - Three-way merge JSON structures
    - 三路归并
  - https://github.com/marcello3d/collabodux
    - library for realtime collaboration on JSON structures. 
    - It is a client-oriented, declarative-functional approach to shared application state.

- https://github.com/hyperhyperspace/hyperhyperspace-core
  - HHS uses an immutable typed-objects local storage model. 
    - Objects are both retrieved and cross-referenced using a structural hash of their contents as their id (a form of content-based addressing).
  - Mutability is implemented using CRDTs. Identities and data authentication are cryptographic.
  - Objects and their references form an immutable DAG, a fact that is used for data replication in HHS p2p mesh.

- https://github.com/twfarland/count-them-beans
  - Displays use of a GCounter conflict-free replicated data type (CRDT), web workers, signals, and virtual dom.
- https://github.com/pietro909/webworkers-crdt
  - Open the file index.html with a modern browser.
- https://github.com/anton-kotenko/crdt
  - CRDT-counter based video hosting visits counter
  - the choice is State-based
  - 使用了redis和mq，过于复杂

- https://github.com/hldb/welo
  - peer-to-peer, collaborative states using Merkle-CRDTs
# crdt-editing
- https://github.com/KristoferSundequist/Collaborative-texteditor
  - Collaborative texteditor based on a Conflict free replicated datatype(CRDT) with a NodeJS client/server. 
  - 数据结构是 treedoc，编辑器使用textarea
- https://github.com/matanbroner/Text-Editor-CRDT
  - Basic text editor CRDT based on the the TreeDoc data structure

- https://github.com/AdarshNaidu/CollabEdit
  - Collaborative text editor built using CRDT data structure
  - 依赖express、handlebars、mongoose
  - 编辑器使用textarea

- https://github.com/Xuzhiqian/WYJPad
  - 基于CRDT的多人实时协作编辑器
  - 依赖codemirror5，提供了服务端，实现简单

- https://github.com/Dhulshette89/BroncoEditor-A-Distributed-collaborative-editor
  - a real time collaborative editor with group chat option. 
  - This is implemented using sequence CRDT approach. 
  - 编辑器依赖ace
  - 服务端依赖mongodb

- https://github.com/drstarry/A-Tour-of-Colleberative-Editing
  - A simple list-based CmRDT to implement collaborate editor
  - 依赖mongodb

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

- https://github.com/geetesh-gupta/py-crdt-collab-editor
  - CRDT based collaborative code/text editor.
  - 依赖flask，requests

- https://github.com/rehnarama/MALTE /rga+split
  - https://rehnarama.github.io/MALTE/index.html
  - Multi-access live text editor
  - An in-browser collaborative coding environment, in which one can edit and compile code a server using an built-in shell.
  - rga作为单独包，并带有测试
  - includes optimisation to the RGA called "block-wise RGA" which allows for chunk insertions.

- https://github.com/prSquirrel/crdt-demo /rga
  - A collaborative text editor demo based on Causal Tree CRDT (variant of RGA).
  - 编辑器基于textarea
  - currently no STUN/TURN servers are configured, so it only works with local peers
  - Uses WebSockets for signaling and WebRTC Data Channels for p2p communication. 

- https://github.com/ROKAF-ResourceManagementSystemDeveloper/crdt /ts/go/rga
  - Simple demo of CRDT(Conflict-free Replicated Data Types)

- https://github.com/mountainflo/collaborative-text-editor /js/go
  - Collaborative realtime texteditor with gRPC using RGAs (Replicated Growable Arrays).
  - using a variant of RGAs (Replicated Growable Arrays). 
  - The RGA-protocol is implemented as Timestamped Insertion Tree (TI Tree) 

- https://github.com/munhitsu/CRAttributes /swift
  - Enables colaboration on text field (and other fields) across multiple iOS devices.
  - A nearly vanilla implementation of CRDT RGA (operation per character).

- https://github.com/ritzyed/ritzy /201509/js/inactive
  - Ritzy editor is a rich text, real-time character-by-character collaborative embeddable browser-based editor. 
  - It shuns(避免) use of the `contentEditable` attribute in favor of a custom editor surface and layout engine, exactly like the approach implemented by Google Docs.
  - Ritzy is built with real-time collaborative editing support from the ground up, underlying mechanism for this is a causal tree CRDT.

- https://github.com/conclave-team/conclave /202106/js/inactive
  - CRDT and WebRTC based real-time, peer-to-peer, collaborative text editor
  - 示例使用simplemde、rxjs、peerjs
  - Intrigued by collaboration tools like Google Docs, we set out to build one from scratch. 
  - Conclave uses (CRDT) to make sure all users stay in-sync and WebRTC to allow users to send messages directly to one another. 

- https://github.com/nybblr/LSEQTree
  - provide an implementation of a CRDT-based array  with an underlying exponential tree and the allocation strategy LSeq

- https://github.com/widmogrod/js-crdt
  - explore applications of data structure called CRDT in context of real time collaboration 
  - https://github.com/widmogrod/notepad-app
    - Collaborative notepad app (demo).
    - 依赖quill

- https://github.com/MatherLyn/co-editing-engine
  - A co-editing engine based on crdt written in JavaScript.

- https://github.com/bazed-editor/bazed /rope
  - the baz editor.
  - The editor consists of a backend including the core data structure on which modifications are made consistent through CRDT and plugin engine (stew).
# last-write-win/llw
- https://github.com/ymlsam/lww-element-dict
  - a LWW key-value store, a conflict-free replicated data type (CRDT)
  - State-based or operation-base replication
  - Abstraction of clock (e.g. unix timestamp clock or vector clock)
  - Abstraction of data store (e.g. in memory via Map or object literal, cookie, local storage, database, etc.)

- https://github.com/hesselbom/crdtmap
  - a simple key-value map that can sync between different clients by letting latest timestamp always win.
  - Key is always a string but value could be anything as long as it's just primitive values.
  - Inspired by yjs and the CRDT-variant LWW-Element-Set
  - 依赖yjs工具方法，但可移除
  - https://github.com/hesselbom/crdtmap-websocket
  - https://github.com/hesselbom/crdtmap-indexeddb

- https://github.com/dominwong4/LWW-Element-Dictionary
  - state-based

- lww+map
  - https://github.com/organicdesign/crdt-map-synchronizer

- https://github.com/siliconjungle/last-writer-wins-registers
  - An example with a few different last-writer-wins registers.

- https://github.com/mazsam/Last-Write-Wins-Element-Set
  - LWW Element Set 
  - https://github.com/petukhov/GN-LWWSet
  - https://github.com/ywchan2005/conflict-free-replicated-data
- https://github.com/3rnii/crdt-lww
  - create a CRDT (conflict free replicated data type) LWW (last write wins) set.

- https://github.com/broswen/ring
  - CRDT LWW Register cluster with gossip
  - a proof of concept for a LWW Register CRDT cluster running on Cloudflare Workers with Durable Objects.

- https://github.com/benhhooxx/LWW-state-based
  - LWWDictionaryStateBased which implements a state-based two-phase set. 
# crdt-string/text
- https://github.com/mweidner037/uniquely-dense-total-order
  - Uniquely Dense Total Orders for List/Text CRDTs
  - This is a concept similar to fractional indexing, but resilient to concurrent insertions.
  - [Plain Tree: A Basic List CRDT](https://mattweidner.com/2022/10/21/basic-list-crdt.html)
    - The rest of this post introduces a basic UniquelyDenseTotalOrder that I especially like. 
    - I have not seen it in the existing literature, although it is similar enough to Logoot, Treedoc, and others that I wouldn’t be surprised if it’s already known. For now, I call it Plain Tree.

- https://github.com/atom-editor/teletype-crdt
  - String-wise sequence CRDT powering peer-to-peer collaborative editing in Teletype for Atom
  - https://github.com/atom/teletype-crdt /js/archived
    - String-wise sequence CRDT powering peer-to-peer collaborative editing in Teletype for Atom.
  - https://github.com/atom/teletype

- https://github.com/kindone/text-versioncontrol
  - provides version and concurrency control for text editing 
  - utilizes Quill's Delta representation in JSON.

- https://github.com/disordinary/crdtstring
  - A CRDT string manipulation library for concurrent editing.
  - Stores a CRDT as a double linked list.
  - Offsets within a string is the ID of the object, insertions are given an index of a fraction of an offset. 

- https://github.com/disordinary/crdt_tree
  - A CRDT String represented as a binary tree
  - Rather than the WOOT approach to CRDT (With Out Operational Transformations) in which every character has it's own ID this approach only splits the string as required for the CRDT operation.
# crdt-json
- https://github.com/carlreinecken/legible-mergeable
  - basic JSON / Javascript Object CRDT
  - The main goal for driving this project was readability: The serialized JSON you get when saving the document on disk or to sent it somewhere over the network, looks almost like the foundational object representation, with just a little meta data.
  - Only complete states are saved and merged, there is no sense of a "diff". 
  - Conflicts are resolved by Last-Write-Wins (LWW).

- https://github.com/crdt-ibm-research/json-delta-crdt
  - DSON - JSON CRDT Using Delta-Mutations
  - Prototype implementation of delta based CRDTs supporting JSON data using Javascript.

- https://github.com/jackyzha0/bft-json-crdt /202211/rust
  - the first JSON-like Byzantine Fault Tolerant CRDT in Rust
  - [Building a BFT JSON CRDT](https://jzhao.xyz/posts/bft-json-crdt/)

- https://github.com/streamich/json-joy/tree/master/src/json-crdt
  - CRDT implementation of a JSON type.

- more-json-crdt
  - https://github.com/JonasKruckenberg/json-patch-crdt
  - https://github.com/samuel-christian/json-crdts
    - 提供了 state+delta 2种
# crdt-tree
- https://github.com/ymlsam/lww-element-dict
  - a LWW key-value store, a conflict-free replicated data type (CRDT) implemented in Typescript/Javascript
  - State-based or operation-base replication
  - Abstraction of clock (e.g. unix timestamp clock or vector clock)
  - Abstraction of data store (e.g. in memory via Map or object literal, cookie, local storage, database, etc.)

- https://github.com/crdteam/causal-tree-ts
  - causal tree replicated data type (RDT) in Typescript.

- https://github.com/codesandbox/crdt-tree
  - A highly-available move operation for replicated trees and distributed filesystems
# crdt-utils
- https://github.com/danielstaleiny/CRDT-sqlite
  - 依赖 idb
- https://github.com/awmuncy/sqlite-crdt
  - 使用sql.js、wasm的示例

- https://github.com/SerenityNotes/naisho
  - an architecture to relay end-to-end encrypted CRDTs over a central service.
  - End-to-end encrypted document using Yjs incl. Cursor Awareness
  - End-to-end encrypted todo list using Automerge

- https://github.com/yorkie-team/yorkie /go
  - Yorkie is an open source document store for building collaborative editing applications. 
  - Yorkie uses JSON-like documents(CRDT) with optional types.
  - Clients can have a replica of the document representing an application model locally on several devices.
  - Each client can independently update the document on their local device, even while offline

- https://github.com/cudr/scto
  - Strings Comparing To Operations (OT model)
  - This package is similar to jsdiff, but generates OT-friendly operations.

- https://github.com/Haotian-Yang/CRDTree
  - 服务端基于ws
# apps-examples
- https://github.com/Sambigeara/fuzzynote /go
  - Terminal-based, hyper-fast, CRDT-backed, collaborative note-taking tool

- https://github.com/courajs/referent
  - An offline-first, realtime-collaborative wiki engine

- https://github.com/markandre13/workflow
  - A Collaborative Real-Time White- and Kanban Board
  - 偏向画板

- https://github.com/itoumlilt/CRDT-Spreasheet
  - CRDT based collaborative Spreadsheet
  - 依赖concordant-crdtlib、delta-crdts

- https://github.com/Roffelchen/spreadsheet-crdt
  - /yjs
# state-management-crdt
- https://github.com/HerbCaudill/crdx
  - CRDX is a state container for JavaScript apps.
  - It is also a CRDT, allowing you to create a local-first application that syncs state directly with peers, with no need for a authoritative central server. 
  - If you’ve used a state container like Redux before, there’s a lot about CRDX that will be very familiar. 
  - We already have excellent JavaScript CRDT libaries such as Automerge and Yjs. So what does this project bring to the table?
    - Automerge and Yjs define a conflict as two peers assigning different values to the same property, and they resolve conflicts by choosing one of the two values as the "winner", in an arbitrary but predictable way.
    - But what a conflict involves more than one property? Or what if you have your own rules for resolving conflicts? 
    - Detecting conflicts may be more subtle than just noticing when two users concurrently modify a property. 
    - And resolving conflicts may involve requirements that won't let us just resolve conflicts in an arbitrary way.
    - To support peer-to-peer replication, we need to deal with concurrent changes, which means a simple append-only list of actions won’t be sufficient. Instead, we arrange actions in a directed acyclic graph (DAG).
# more-crdt
- https://github.com/netopyr/wurmloch-crdt
  - Experimental implementations of conflict-free replicated data types (CRDTs) for the JVM

- https://github.com/anshulahuja98/python3-crdt
  - A python library for CRDTs (Conflict-free Replicated Data types)
- https://github.com/junjizhi/lww-element-set
  - Last-Writer-Wins Element Set(lww-set) data structure implemented in Python

- https://github.com/aphrodite-sh/cr-sqlite
  - Convergent, Replicated SQLite. Multi-writer and CRDT support for SQLite
  - This project implements CRDTs and CRRs in SQLite, allowing databases that share a common schema to merge their state together.
  - crsqlite works by adding metadata tables and triggers around your existing database schema. 
  - crsqlite only keeps an extra int per column and a clock per row.

- https://github.com/orda-io/orda
  - Orda: A client and server written in Go. CRDT-based data synchronization supporting document database.
  - Orda project is a multi-device data synchronization platform based on MongoDB (which could be other document databases such as CouchBase). 

- https://github.com/hughfenghen/rtc-live-show
  - 基于WEB RTC + rrweb实现的页面“直播”demo

- https://github.com/decentraland/crdt-scene
  - test scene for CRDT protocol
  - https://github.com/decentraland/sdk-ws
    - CRDT Websocket Server

- https://github.com/KlonD90/crdt-server
  - 实现简单
- https://github.com/decentraland/crdt
  - 服务端api的定义很标准

- https://github.com/AntidoteDB/crdt-visualizer
  - https://www.antidotedb.eu/crdt-visualizer/
  - Visualized CRDT executions in a web page to explain their semantics

- https://github.com/theJian/crdt-todo-app
  - sync未实现

- https://github.com/telamon/tic-tac-nano
  - storing the full history of a Tic-tac-toe game session occupying only 20bits of binary space.

- https://github.com/apoos-maximus/crdt-client
  - client-side implementation for a java based crdt implementation

- https://github.com/danieljharvey/webaudio-crdt
  - Collaborative webaudio

- https://github.com/dbranizor/crdt-svr
  - 依赖nestjs、ejs

- https://github.com/lecocococo/peer-to-peer-connection-test
  - Using peerjs, A Collaborative Text Editor using CRDT
