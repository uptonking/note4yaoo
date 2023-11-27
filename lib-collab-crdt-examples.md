---
title: lib-collab-crdt-examples
tags: [collaboration, crdt, examples]
created: 2022-01-22T16:14:32.323Z
modified: 2022-04-05T10:08:25.947Z
---

# lib-collab-crdt-examples

# guide

- requirements
  - **extensible-data-structure**
  - undo/redo
  - sync protocol
  - 实时协作
  - 离线合并
  - 冲突处理算法 + 网络通信

- not-yet-基于crdt实现text文本协作的问题
  - 对不同分支的文档在相同位置粘贴相同的文本时，crdt会保留重复的文本

- crdt-text
  - 能不能将协作的粒度从字符提升为句子
  - 或者crdt-text-by-lines, still sequence crdt，参考typewriter-quill

- crdt-db: search repos + issues/discussions
  - indexeddb-crdt, db-crdt
    - 💡 db很可能只是持久化的位置，计算逻辑仍发生在内存，计算逻辑中的crdt可复用
  - js-db: rxdb, tinybase

- versions
  - 将git自动生成的.git文件夹改为自定义database，将snapshot改为crdt-changes，似乎可以实现支持时间旅行和协作合并的新工具

- tips
  - 不必执着于hlc的使用案例，可对成熟案例在业务逻辑不变的情况下将其他clock替换成hlc

- resources
  - [Comparison of CRDT Libraries - hyoo/automerge/yjs](https://github.com/hyoo-ru/crowd.hyoo.ru?tab=readme-ov-file#comparison-of-crdt-libraries)
  - [crdt Code (Implementations)](https://crdt.tech/implementations)
  - https://github.com/alangibson/awesome-crdt
  - [Alternatives · ElectricSQL](https://electric-sql.com/docs/reference/alternatives)
  - [CRDTs for Non Academics - YouTube](https://www.youtube.com/watch?v=vBU70EjwGfw)
  - https://github.com/doodlewind/crdt-and-local-first
  - https://github.com/topics/crdt?l=typescript&o=desc&s=updated
# popular
- https://github.com/pubuzhixing8/awesome-collaboration
  - Collaborative editing of technical resources, article translation
  - [OT 与 CRDT 的Battle，堪称神仙打架](https://github.com/pubuzhixing8/awesome-collaboration/blob/master/fairy-fight/collaborative-editing.md)

- evolu /101Star/GPLv3/202210/ts/hlc
  - https://github.com/evoluhq/evolu
  - https://www.evolu.dev/
  - React Hooks library for local-first software with end-to-end encrypted backup and sync using SQLite and CRDT
  - 依赖fp-ts、protobuf、kysely(sql-builder)、murmurhash、~~zod~~
  - 提供了dbworker.worker
  - [Release evolu@5.0.0](https://github.com/evoluhq/evolu/releases/tag/evolu%405.0.0)
    - For now, Evolu is using a synchronous version of SQLite. 
    - But soon, we will also use asynchronous SQLite for other platforms where synchronous SQLite is not available. 
    - With Effect, the code is the same.
    - Without Effect, we would always use Promises, even for synchronous code. Or we would have to write the same logic twice. 
  - All table columns except for ID are nullable by default. It's not a bug; it's a feature. Local-first data are meant to last forever, but schemas evolve. 
  - writing local-first software has been challenging because of the lack of libraries and design patterns. I personally failed several times, and that's why I created Evolu.
  - Evolu architecture is almost a clone of James Long CRDT for mortals. Rewritten and improved
  - Evolu uses end-to-end encryption and generates strong and safe passwords for you. 
    - Evolu sync and backup server see only timestamps. Nothing more. 
    - We plan to do at least two security audits.
  - Evolu is not pure P2P software. For syncing and backup, there needs to be a server. 
  - Evolu CRDT has no support for transactions because CRDT transactions are still an unsolved issue. 
  - All table columns except for ID are nullable by default. It's not a bug; it's a feature. Local-first data are meant to last forever, but schemas evolve.

- triplit /AGPLv3/202310/ts/crdt/llw/eav
  - https://github.com/aspen-cloud/triplit
  - https://triplit.dev/
  - [Triplit Roadmap](https://aspencloud.notion.site/7362bdf6512243fcbdfe03c9d56a5998?v=acd301c4bd3942b9b30a15f636cecd00)
  - Triplit is a complete solution to data persistence, state management, and realtime synchronization for web applications
  - TriplitDB - Designed to run in any JS environment (browser, node, deno, React Native, etc) and provide expressive, fast, and live updating queries while maintaining consistency with many writers over a network.
  - Client - Browser library to interact with local and remote TriplitDBs.
  - React - React bindings for @triplit/client
  - ✨ https://github.com/aspen-cloud/triplit/tree/main/packages/db
  - 依赖tuple-database、sorted-btree、zod、idb
  - the embedded database that powers Triplit, a complete solution to data persistence, state management, and realtime synchronization for web applications 
  - Built-in storage providers for in-memory, IndexedDB, and Sqlite
  - Automatic indexing of object properties for fast querying
  - Combine multiple storage layers in the same DB with granular scoping on reads and writes
  - Transactions with rollback
  - Schema for validation, type hinting and enhanced CRDT-based storage.
  - A schema can comprise multiple ‘collections’ (similar to a table in SQL). Using a schema with TriplitDB will enable type checking and the full the benefit of our CRDT-based data structures, like sets.
  - By default your data will be stored ephemerally in memory and not persist through page refreshes
  - Under the hood, TriplitDB utilizes a timestamped Triple Store to support efficiently merging changes from multiple sources whether that’s multiple writers or multiple storage layers. 
  - Each object that’s inserted is decomposed into a EAV triple of Entity (ID), Attribute (path in the object), and a Value. 
  - Each triple is stored with a Lamport Timestamp and treated as a Last Writer Wins Register (LWW). 
  - To support its tuple based storage system, TriplitDB uses Tuple Database as a generic querying interface and transaction manager.

- https://github.com/logux/core /202209/js/提供了ts声明
  - https://logux.io/
  - https://github.com/logux/server
  - https://github.com/logux/client
  - https://github.com/logux/examples
  - Logux is an WebSocket client/server framework to make: collaborative apps; realtime apps; offline-first
  - Logux is a new way to connect client and server. Instead of sending HTTP requests (e.g., AJAX and GraphQL), it synchronizes log of operations between client, server, and other clients.
  - 官方交流方式是 [gitter](https://gitter.im/logux/logux)
  - when multiple users work with the same document. Logux has features inspired by CRDT to resolve edit conflicts between users. 
  - Time travel to keep actions order the same on every client. A distributed timer to detect the latest changes.
  - offline first: Logux saves Redux actions to IndexedDB and has a lot of features to merge changes from different users.
  - Logux combines WebSocket with modern reactive client architecture. It synchronizes Redux actions between clients and servers, and keeps the same order of actions.
  - Optimistic UI to improve UI performance by updating UI without waiting for an answer from the server. Time travel will revert changes later if the server refuses them.
  - Compatible with modern stack: Redux, Vuex and pure JS API, works with any back-end language and any database.

- FluidFramework /4.2kStar/MIT/202302/ts
  - https://github.com/microsoft/FluidFramework
  - https://fluidframework.com/
  - Library for building distributed, real-time collaborative web applications
  - 示例未渲染协作鼠标
  - 依赖中心服务器转发op及定顺序，依赖server的clock，未使用分布式时钟
  - 不支持长时间的offline
  - [Does Fluid use CRDT?](https://fluidframework.com/docs/faq/#does-fluid-use-crdt)
    - Fluid does not use Conflict-Free Replicated Data Types (CRDTs), but our model is more similar to CRDT than OT. 
    - The Fluid Framework relies on update-based operations that are ordered using our Total Order Broadcast to prevent conflicts. 
    - This allows us to have non-commutative operations because there is an explicit ordering.
    - [Doc: Is Fluid OT or CRDT?_202201](https://github.com/microsoft/FluidFramework/issues/8920)
    - The service part of Fluid is OT/CRDT agnostic and possibly of interest to CRDT developers looking for a managed backend solution.
    - Some of the built-in Fluid DDS implementations may be of general interest to CRDT researchers.
  - The Fluid Framework requires a Fluid service to sync data between clients. 
    - The role of the server is very simple: it orders operations and broadcasts them to all clients. 
    - It’s also responsible for saving operations to persistent data storage
  - What kind of support is there for real-time editing of text?
    - This is the scenario that Fluid was first designed to support. 
    - Consequently, the Fluid Framework is an ideal foundation for rich text editors that support simultaneous editing by multiple clients. 
    - The `SharedString` DDS is tailor-made for this scenario.
  - [Microsoft introduces Loop: A new collaboration tool built on Fluid Framework_202111](https://www.zdnet.com/article/microsoft-introduces-loop-a-new-collaboration-tool-built-on-fluid-framework/)

- harika-note /111Star/AGPLv3/202208/ts
  - https://github.com/quolpr/harika
  - Harika is an offline-first, performance-focused note taking app for organizing your knowledge database.
  - Synchronization with server. It's done with LWW CRDT per field on top of SQLite. 
    - It also stores all changes locally and sends them to server. 
    - Server also store all the changes and recalculate snapshots on new received changes and send those snapshots back to the client. 
    - Due to we store all the changes at server, it is also planned to add time travel, when CRDT is not what user expect at some cases.

- xi-editor /19.7kStar/apache2/202206/rust/woot
  - https://github.com/xi-editor/xi-editor
  - https://xi-editor.io/
  - A modern editor with a backend written in Rust.
  - The xi-editor project is currently discontinued. 
  - CRDT: This approach follows WOOT.
  - https://github.com/lapce/lapce
    - written in pure Rust with a UI in Floem
    - designed with Rope Science from the Xi-Editor which makes for lightning-fast computation, and leverages Wgpu for rendering

- https://github.com/atom-archive/xray /201904/rust/js/RGASplit/archived
  - [Xray – An experimental next-generation Electron-based text editor | Hacker News](https://news.ycombinator.com/item?id=16525735)
  - Text is stored in a copy-on-write CRDT.
    - We use a variant of RGA called RGASplit
  - Our current understanding is that in Xi, the buffer is stored in a rope data structure, then a secondary layer is used to incorporate edits. 
  - In Xray, the fundamental storage structure of all text is itself a CRDT.
    - It's similar to Xi's rope in that it uses a copy-on-write B-tree to index all inserted fragments, but it does not require any secondary system for incorporating edits.
  - zed.dev is by ex Atom devs and sound like successor to Xray philosophy

- https://github.com/atom-editor/teletype-crdt /201810/js/woot
  - String-wise sequence CRDT powering peer-to-peer collaborative editing in Teletype for Atom
  - https://github.com/atom/teletype-crdt /js/archived/与上面仓库相同
  - it adopts splay trees and several other optimizations to improve the asymptotic complexity of common operations.
  - [Atom-teletype代码协同编辑原理详解_202011](https://mp.weixin.qq.com/s?src=11&timestamp=1686732708&ver=4589&signature=8ifZN03y4mobAX0Mn0CnG1Pv3oT5RHfMds3ZQX4IbFMeBLv6di-WBPRSMDXf-4Y6DW5u6nzCQGw3KZuKTap-bdOPzO9bZQpRKQWI6uo9RAdEmPiihZ2be3lwelV-LT4V&new=1)
    - 本文主要介绍 TELETYPE-CRDT中如何设计 WOOT算法来保证文本类型数据的最终一致性，并使用复合的数据结构（称之为 IDTree）来优化代码的运行效率。
  - [Resolve conflicts during remote insertion integration in O(log n)_201711](https://github.com/atom/teletype-crdt/pull/4)
    - This pull-request proposes a modification to the current O(k2) insertion integration algorithm, where k represents the number of insertions that occurred concurrently to the insertion that is being integrated.
    - The previous approach was entirely based on the algorithm proposed by Yu in 2014, which was a revisitation of the original `WOOT` algorithm discovered in 2006.
  - [Can teletype-crdt work with other wysiwyg editor ?](https://github.com/atom/teletype-crdt/issues/6)
    - Probably not. This CRDT is for text. A wysiwyg editor’s underlying model isn’t text, it’s a tree (with nodes and properties to represent rich text).
    - teletype-crdt is a CRDT that exposes APIs that work only with plain text and markers. A WYSIWYG editor has a more complex structure than just text, so you will need to enhance it in such a way that can support your use case.
  - https://github.com/atom/teletype
  - https://github.com/jure/rgass /js
    - A JS implementation of RGASS, a CRDT synchronization algorithm
    - No longer in development, for similar use cases (and using the same basic approach) take a look at `teletype-crdt`

- https://github.com/Horusiath/crdt-examples /F#
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

- https://github.com/josephg/editing-traces
  - This repository contains some editing histories from real world character-by-character editing traces
  - The goal of this repository is to provide some standard benchmarks that we can use to compare the performance of rope libraries and various OT / CRDT implementations.

- https://github.com/streamich/json-joy/tree/master/src/json-crdt
  - json-crdt中提供了rga、lww-object
  - [Block-wise RGA algorithm implementation for json-joy_202305](https://jsonjoy.com/blog/performant-rga-list-crdt-algorithm)
  - [Benchmarking json-joy against Automerge v2 and Y-libraries_202305](https://jsonjoy.com/blog/list-crdt-benchmarks)
  - [Fuzz Testing RGA CRDT_202306](https://jsonjoy.com/blog/fuzz-testing-rga-crdt)
    - using fuzz testing you can make sure your collaborative editing algorithms are 100% correct

- https://github.com/inkandswitch/peritext /MIT/ts
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - Peritext builds upon RGA, which is similar to Causal Trees, although our algorithm could use any of these plain text CRDTs with minor adaptations. 
  - This repo includes:
    - A Typescript implementation of the core Peritext CRDT algorithm
    - A prototype integration with ProseMirror editor
    - An interactive demo UI where you can try out the editor
    - A test suite
  - [Peritext algorithm may attach deleted mark to new inserted text](https://github.com/inkandswitch/peritext/issues/32)
  - [What could be the direction for making Peritext support block elements](https://github.com/inkandswitch/peritext/issues/27)
    - I helped design a convergent data model for tables at Notion recently that would work well using 3 convergent data types: Map (to group and address fields), Ordered Set (for defining the order of rows and the order of columns), and Rich Text (for defining the contents of cells).
  - forks
  - https://github.com/philschatz/peritext
    - 更新了版本、迁移到vite、基于automerge-wasm

- https://github.com/loro-dev/crdt-richtext /169Star/MIT/202305/rust
  - https://crdt-richtext-quill-demo.vercel.app/
  - Rich text CRDT that implements Peritext and Fugue
  - This CRDT lib combines Peritext and Fugue's power, delivering impressive performance specifically tailored for rich text. 
  - It leverages the `generic-btree` library to boost speed, and the `serde-columnar` simplifies the implementation of efficient columnar encoding.
  - loro-wasm and fugue only support plain text for now
  - [富文本 CRDT crdt-richtext 开源啦 - 知乎](https://zhuanlan.zhihu.com/p/629580388)
  - [The Art of the Fugue: Minimizing Interleaving in Collaborative Text Editing](https://arxiv.org/abs/2305.00583)
  - [Feat richtext ](https://github.com/loro-dev/crdt-richtext/pull/1)
    - This PR implements an RGA CRDT + Peritext. It's also optimized for high speed with a relatively low memory footprint.
    - Under the hood, it uses the generic-btree crate to store the text content, the text ops, and the Peritext range anchors in a unified way.

- https://github.com/loro-dev/loro /MIT/202311/rust
  - https://loro.dev/
  - a CRDTs(Conflict-free Replicated Data Types) library that makes building local-first apps easier.
  - Support for `List` for ordered collections, LWW(Last Write Win) `Map` for key-value pairs,  `Tree` for hierarchical data, and `Text` for rich text manipulation, enabling various applications.
  - Drawing inspiration from Peritext, Loro manages rich text CRDTs that excel at merging concurrent rich text style edits
  - Moveable Tree: For applications requiring directory-like data manipulation
  - track changes effortlessly as it records the editing history with low overhead.
  - https://github.com/loro-dev/loro-examples-deno

- https://github.com/loro-dev/loro-time-travel-demo /202311/ts
  - https://loro-dev.github.io/loro-time-travel-demo/
  - demonstrate Loro's high performance and time travel capabilities. 
  - The entire code is only about 100 lines.

- https://github.com/serenity-kit/secsync /ts
  - https://www.secsync.com/
  - Is an architecture to relay end-to-end encrypted CRDTs over a central service.
  - It was created out of the need to have an end-to-end encrypted protocol to allow data synchronization/fetching incl. real-time updates to support local-first apps in combination with a web clients without locally stored data.
  - eg: End-to-end encrypted document using Yjs incl. Cursor Awareness
  - eg: End-to-end encrypted todo list using Automerge
  - Why use a central relay service?
    - The main reason is to exchange data asynchronously.
  - https://github.com/serenity-kit/Serenity /ts
    - End-to-end encrypted pages for your team

- https://github.com/composablesys/collabs /ts
  - https://collabs.readthedocs.io/
  - Collabs is a collections library for collaborative data structures. 
  - These are data structures that look like Set, Map, Array, etc., except they are synchronized between multiple users
  - Collabs is a library for collaborative data structures, not just a menu of built-in options (but we provide those too). So if our data structures don’t meet your needs, you can create your own
  - [Collabs: A Flexible and Performant CRDT Collaboration Framework_202212](https://arxiv.org/abs/2212.02618)
  - [Text and List Optimizations_202203](https://github.com/composablesys/collabs/pull/218)
    - Replaces RgaDenseLocalList with ListPositionSource. This uses the same underlying CRDT design (Double RGA)
  - [Network and Storage Providers](https://collabs.readthedocs.io/en/latest/guide/providers.html)
    - Collabs documents don’t come with networking or storage built-in. 
    - you should configure 可选 ws-client/tab-sync/indexeddb/local-storage
    - Collabs documents don’t come with networking or storage built-in. Instead, you should configure 
  - https://github.com/composablesys/collabs-e2e-benchmark
  - [Collabs: Composable Collaborative Data Structures_2022](https://arxiv.org/abs/2212.02618)
  - https://twitter.com/matthewweidner3/status/1444475869121110017
    - Collabs is directly inspired by Automerge and Yjs, and uses similar techniques (network-agnostic CRDTs).  
    - The main difference is its API: we try to mimic a non-replicated collections library, with flexibility, composition tools, and strong typing.

- https://github.com/TopGunBuild/topgun /ts/gundb
  - https://gun.eco/docs/
  - Reimplementation of gunDB in TypeScript
  - A graph data synchronisation engine for building realtime, offline-first, secure and scalable applications.
  - [recently started TopGun. TopGun is still at an early stage](https://matrix.to/#/!apmkrFyPwFRRvQgtEw:gitter.im/EXselrV0t3CAC9wC8pYiNaom57VTS_JU-PXXVscXpmY?via=gitter.im&via=matrix.org&via=matrix.thisisjoes.site)
    - does the version number 1.x mean the first stable release has already been done?
    - Unfortunately TopGun isn't stable yet, this is my first attempt at using semantic-release and I missed the point when the auto-upgrade was over 1.x
    - I tried awaiting a .put in the for-loop, but then I guess something starting hanging in GUN and it stopped calling the .put callbacks

- https://github.com/okdistribute/piratedb /js/inactive
  - A multiwriter peer-to-peer database with a last-writer-wins CRDT.
  - 依赖subleveldown、unordered-materialized-kv、randombytes
  - 测试用例使用kappa-core、memdb、random-access-memory

- https://github.com/partykit/partykit /ts
  - https://partykit.io/
  - partykit is an SDK designed for creating real-time collaborative applications.
  - The fundamental components of a partykit application are the server and the client. 
    - The server is a simple JavaScript module exporting an object that defines how your server behaves, primarily in response to WebSocket events. 
    - The client connects to this server and listens for these events.
  - First-class integrations with popular collaboration frameworks and libraries. Y.js, automerge, replicache, they all Just Work
  - `y-partykit` is an addon library for partykit designed to host backends for Yjs
  - [automerge backend](https://github.com/partykit/partykit/issues/97)
  - PartyKit is extremely unopinionated. It's essentially lightweight javascript server, that launches fast and autoscales 
  - Most people seem to run yjs in PartyKit, but you can also run automerge or even Replicache

- https://github.com/supabase/pg_crdt /rust
  - pg_crdt is an experimental extension adding support for conflict-free replicated data types (CRDTs) in Postgres.
  - It supports Yjs/Yrs and Automerge.
  - Our goal was to evaluate if we could leverage a Postgres-backed CRDT and Supabase's existing Realtime API for change-data-capture to enable development of collaborative apps on the Supabase platform.
  - pg_crdt extension is a proof-of-concept that wraps rust's yrs and automerge libraries using the pgx framework to add a Postgres native CRDT, crdt.ydoc.

- https://github.com/electric-sql/electric /ts+elixir
  - Local-first software platform for developing web and mobile apps with instant reactivity, realtime multi-user collaboration and conflict-free offline.
  - With active-active replication between Postgres and SQLite.
  - ElectricSQL gives you instant local-first for your Postgres. 
  - Elixir sync service that manages active-active replication between Postgres and SQLite

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

- https://github.com/convergencelabs/javascript-examples /202105/js/inactive
  - Examples for the Convergence Real-time Collaboration Engine
  - https://github.com/convergencelabs/input-element-bindings
  - https://github.com/convergencelabs/html-text-collab-ext

- https://github.com/PsychoLlama/graph-crdt /201707/js/inactive
  - Designed for serializing arbitrary data structures, making offline edits, and seamlessly merging changes back in. All data is observable and event driven.
  - graph-crdt is a modified version of a LWW-E-Set with inline garbage collection using lamport clocks and JavaScript's lexicographic comparison on deterministically serialized JSON for the predetermined conflict resolution bias.
  - This library implements a delta graph CvRDT.
- https://github.com/PsychoLlama/mytosis /202003/js/基于graph-crdt
  - A peer-to-peer data sync framework
  - Mytosis organizes data as one massive object which contains other objects. The root is called the graph, and its children are called nodes.
  - [Mytosis Redesign](https://github.com/PsychoLlama/mytosis/wiki)
  - [The data structures and merge algorithms implemented by Mytosis](https://github.com/PsychoLlama/mytosis/wiki/CRDTs)

- https://github.com/hockyy/peertocp /202211/js
  - Electron Project for WebRTC Based Code Editor, Compiler, and C++ runner
  - CRDT Peer-to-Peer Branch using modified y-webrtc
  - CRDT Client-Server Branch using modified y-websocket
  - Operational Transformation Client-Server Branch using `@codemirror/collab` OT, based on Codemirror Collab Website Example for code editor
  - https://github.com/hockyy/peertocp-web /unfinished

- https://github.com/zkpranav/crdt-sync-client /未完成
  - https://github.com/zkpranav/crdt-sync-server
  - Implementation of a CRDT based networking layer for a collaboration tool.
  - heavily inspired by Figma's implementation of their networking layer.
  - A Document consists of a set of objects structured in a hierarchical tree-like structure. 
    - Each Object has an associated ID which is globally unique, and a set of property-value pairs. 
    - Parent-Child relationships are maintained as a link from the child to its parent.

- https://github.com/andykswong/mithic /MIT/ts
  - https://andykswong.github.io/mithic/
  - Modular library for real-time isomorphic JavaScript applications
  - mithic provides the building blocks for creating real-time, offline-first client-server or decentralized applications, using CQRS architecture with CRDT eventsourcing for storage and data replication.
  - minimal example to get started. Uses the Redux store preset
  - crdt基于自己实现的lseq
  - Linear sequence of values based on `ORMap` of base64 fractional index to values
  - timestamp基于逻辑时钟

- https://github.com/p2panda/aquadoggo /rust
  - https://p2panda.org/
  - aquadoggo is a reference node implementation for p2panda. 
  - It is a intended as a tool for making the design and build of local-first, collaborative p2p applications as simple as possible
  - aquadoggo can run both on your own device for local-first applications, or on a public server when acting as shared community infrastructure. 
  - Stores operations of the network in an SQL database of your choice (SQLite, PostgreSQL).
  - Materializes views on top of the known data.
  - Answers filtered, sorted and paginated data queries via GraphQL.
  - Awaits signed operations from clients via GraphQL.
  - [P2panda: P2P protocol for secure, energy-efficient local-first web applications | Hacker News_202308](https://news.ycombinator.com/item?id=37212462)
    - We're using our own CRDT called "Operations" giving us multi-writer conflict-free editing. It's a simple key/value map with a last-write win rule while we keep some sort of vector clock for every write to understand what every peer has seen when they updated the Document.
    - we could model many applications already with such simple CRDT. It is also possible to add your own or already existing CRDT frameworks on top of p2panda.
    - The basic data sync is based on an append only log. 
    - Check out our section on "Operations", this is the data type we've built on top of the append-only log structure for multi-writer and conflict free data editing

- https://github.com/KyleAMathews/trpc-crdt /MIT/ts
  - tRPC integrations for CRDTs: CRDT-native RPC calls
  - the goal is to support all CRDT implementations, including yjs/automerge/jazz
  - [Announcing trpc-crdt _202311](https://bricolage.io/announcing-trpc-crdt/)
  - https://twitter.com/kylemathews/status/1723006206032101875
    - trpc-crdt includes integrations for tRPC for Yjs and ElectricSQL w/ two more almost finished for Automerge and Jazz.
    - The big advantage of this approach is that the server can write directly to the CRDT data so all server mutations get replicated immediately to clients.
# crdt-rewrite
- https://github.com/josephg/crdt-examples /js
  - CRDT examples from a DWEB talk
- https://github.com/genderev/crdt-examples /js
  - Practical examples of CRDTs that you can reference for your p2p app.

- https://github.com/jlongster/crdt-example-app /201912/js
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
- https://github.com/daaku/kombat /ts/hlc+merkle-tree
  - Infrastructure for CRDT powered applications.
  - Timestamp for Hybrid Logical Clocks.
  - https://github.com/daaku/kombat-indexed-db
    - Kombat storage implemented using IndexedDB.
  - https://github.com/daaku/kombat-firestore
    - Kombat storage implemented using Firebase Firestore Database.

- https://github.com/ipfs-shipyard/peer-crdt /js/deprecated
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
- https://github.com/rust-crdt/rust-crdt /rust/只提供了基础类型
  - a collection of well-tested, serializable CRDTs for Rust
  - A family of CRDT's supporting both State and Op based replication.
  - List is based on the LSEQ and LOGOOT
  - [Support for recursive data types (e.g. JSON) ?](https://github.com/rust-crdt/rust-crdt/issues/51)
    - Yep, Map is indeed recursive, but it has the limitation that every value in the map is of the same type so it does not behave like a JSON CRDT where values may have different structures if that's what your goal is.
    - you don't need an RGA for strings, just a LWW register. In the Riak DT map (and other proprietary JSON like CRDTs I have worked on). Strings have been LWW registers. **If you think of CRDTs as containers (Array, Map, Set) and values (Counter, Register) then you can make a JSON like thing with those alone (you don't even need the Set)**.
    - I still wonder how the ops should be structured though. I can't see a way to have document level CRDT ops that would not store some kind of a path to the target inner field. Since ops are serializable, that path must be serializable too. AFAIK, ditto did it using JSON pointers and I still see no better way to do that.
- https://github.com/JMLX42/rust-delta-crdts
  - Delta state-based CRDTs in Rust.

- https://github.com/siliconjungle/delta-crdt /单文件
  - A simple delta CRDT implementation.

## woot

- https://github.com/ryankaplan/woot-collaborative-editor /201601/ts
  - A real time collaboration toy project based on WOOT. Implemented with node.js and ws.
  - 编辑器使用textarea，依赖diff-match-patch
  - This is a server and client for a real-time collaborative document editor (aka a drastically simplified Google Docs).
  - When a textarea-change is detected, diff the textarea content against the last known content. 
  - With the help of WootTypes. WString, turn that diff into `WStringOperations` and broadcast those operations to the server.
  - When we receive operations from the server, apply those operations to our WString instance and apply them to the text in #collab-doc.
  - WOOT, as an approach, gets really slow unless you implement tombstone garbage collection (aka getting rid of text that users have deleted) which can only happen when everyone has disconnected from a document.

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

- https://github.com/t-mullen/woot-crdt
  - Replicate text or sequences over networks.
- https://github.com/t-mullen/logoot-crdt
  - Optimized Logoot CRDT implementation.
  - Implemented as a tree for fast character position lookups.
- https://github.com/kana-sama/edita
  - https://github.com/kana-sama/edita-server
  - 示例监听span文字的crud，未使用编辑器框架

- https://github.com/bcherny/crdt-demo /ts
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

- https://github.com/coast-team/dotted-logootsplit /MPL/ts
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

## rga/causal-tree

- usecase
  - automerge(v1使用js，v2使用rust)
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

- https://github.com/josephg/simple-crdt-text /ts/rga
  - This implements automerge's underlying algorithm (RGA)
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.
  - [automerge-and-yjs-minimal.ts](https://gist.github.com/josephg/26ade72d5ced0470485c734fb1ebb6ca)
  - [yjs-minimal.ts](https://gist.github.com/josephg/dcb1bce2ceb0f0b50ffcac0245a55907)
  - [yjs_testcase.ts](https://gist.github.com/josephg/88c006724435a61afaec5ff3f1bacd87)

- https://github.com/josephg/reference-crdts /ts
  - This repository contains simple proof-of-concept reference implementations of yjs, automerge and sync9's list types - all implemented in the same codebase. 

- https://github.com/jaredly/local-first/tree/master/packages/text-crdt
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.
  - Your approach seems to resemble RGASplit which I believe is bases for

- https://github.com/rehnarama/MALTE /ts/rga+block
  - https://rehnarama.github.io/MALTE/index.html
  - Multi-access live text editor
  - An in-browser collaborative coding environment, in which one can edit and compile code a server using an built-in shell.
  - rga作为单独包，并带有测试
  - includes optimisation to the RGA called "block-wise RGA" which allows for chunk insertions.

- https://github.com/streamich/json-joy/blob/master/src/json-crdt/types/rga-array/ArrayRga.ts
  - 提供了 rga-array, rga-string, rga-binary
  - [JSON CRDT text split 待实现](https://github.com/streamich/json-joy/issues/215)

- https://github.com/slightknack/together /rust
  - [Thinking about efficient backing stores for CRDTs — Isaac Clayton](https://slightknack.dev/blog/backing-crdt-store/)
  - Today, we’re going to focus on creating out an efficient backing store for a particular family of algorithms known as Replicated Growth Arrays (RGA).
  - Under RGA, we represent documents as trees of strings. although conceptually RGA operates on trees, implementation-wise, it’s not a requirement
  - The merging algorithm behind RGA is pretty elegant. Each character in the tree points to the one before it.

- https://github.com/el10savio/rga-crdt /go
  - RGA CRDT Implemented in Go

## rewrite-more

- https://github.com/dglittle/shelf
  - Here is a shelf: [VALUE, VERSION_NUMBER]
  - [josephg/shelf.ts](https://gist.github.com/josephg/c433d3bcc078d911e7696c6d64381bf1)

- https://github.com/gritzko/citrea-model /201712/js/rga/causal-tree
  - A CRDT-based collaborative editor engine of letters.yandex.ru (2012, historical)
  - https://news.ycombinator.com/item?id=28018129
    - About a decade ago, I implemented the Causal Tree CRDT (aka RGA, Timestamped Insertion Tree) in regular expressions using a Unicode string as a storage. Later we made a collaborative editor for Yandex based on that code.
    - Recently(202107) I greatly improved CTs by introducing the Chronofold data structure
    - I remember seeing that (regex CTs) and immediately thinking "wtf, why would anyone want to do that". Took me quite a while to understand that it's actually a pretty clever way to write fast state machines in browserland. So thank you for this work!
- https://github.com/gritzko/swarm /2.7kStar/MIT/201805/js/inactive
  - Swarm.js is a JavaScript client for the Swarm database.
  - Swarm is like "git for data" except it's real-time and never has a merge conflict. 
  - Swarm is based on Replicated Object Notation (RON), a distributed live data format.
  - RON is based on CRDT
  - https://github.com/Empia/swarm/blob/master/swarm-protocol/src/Clock.js
    - Swarm is based on the Lamport model of time and events in a distributed system, so Lamport logical timestamps are essential to its functioning.
    - Still, in most of the cases, it is useful to know the actual wall clock time of an event.
    - Hence, we use logical timestamps that match the wall clock time numerically.
    - A similar approach was termed "hybrid timestamps"
    - this is logical clock that tries to be as close to wall clock as possible

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

- https://github.com/wangdashuaihenshuai/crdt-edit /201810/vue/js
  - [我自己从零实现的一个文本文档的协同编辑demo，上面是输入框，下面是数据结构的可视化](https://zhuanlan.zhihu.com/p/48229762)
  - 每个操作都是依赖前一个操作的结果，这样的数据结构就是有操作依赖生成的一颗 因果树
  - 依赖konva的画图app

- https://github.com/siliconjungle/tiny-merge
  - State-based CRDT with a Tiny footprint.
  - 包含server、client，服务端依赖supabase

- https://github.com/dkellner/chronofold /rust
  - Chronofold is a conflict-free replicated data structure (a.k.a. CRDT) for versioned text.
- https://github.com/decentralized-hse/collab-edit /kotlin
  - the state of text and cursor positions are stored as Chronofold on each client. 
  - When the user updates the text or the cursor position on one client, it calculates diff via `diff-match-patch`, updates its Chronofold, and sends new operations to another client. 
  - Another client adds these operations to its Chronofold and updates the text and cursor positions accordingly.

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

- https://github.com/hyperhyperspace/hyperhyperspace-core /MIT/ts
  - https://www.hyperhyperspace.org/
  - A library to create p2p applications, using the browser as a full peer.
  - An offline-first shared data library for creating p2p apps that work in the browser (and now also NodeJs).
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

- https://github.com/concordant/c-crdtlib /kotlin
  - CRDT library in Kotlin for the Concordant platform API. 
  - This project is based on Kotlin multiplatform feature.
  - The Kotlin code is compiled to both JVM Bytecode and Javascript/Typescript

- sync9 /js
  - https://github.com/braid-org/braidjs/tree/master/sync9
  - Sync9 is interesting given that it stores actual character indices in the CRDT so appending new writes does not require any lookups of parent events and constructing a doc from the event log is trivial. 
  - Sync9 also solves the same interleaving problems as Fugue.

- https://github.com/zackradisic/learning-crdts-rust /rust
  - CRDT implementations I write as I learn more about them
  - Following along and porting the code from convergent CRDT half of Bartosz Sypytkowski's blog post series in F# to Rust
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

- mute /96Star/AGPLv3/202302/ts/rxjs/logootsplit
  - https://github.com/coast-team/mute
  - https://mutehost.loria.fr/
  - a scalable collaborative document editor with CRDT, P2P and E2EE
  - MUTE implements a CRDT-based consistency algorithm (LogootSplit) for large scale peer-to-peer collaboration on top of a peer-to-peer message layer (netflux and soon libp2p).
  - 示例基于tui-editor.v2、codemirror5、angular
  - https://github.com/coast-team/mute-core
    - 依赖rxjs、dotted-logootsplit
  - https://github.com/coast-team/dotted-logootsplit /MPL/ts
    - a delta-based version of LogootSplit with smaller metadata. We provide both op-based and delta-based synchronizations.

- https://github.com/ritzyed/ritzy /201509/js/inactive
  - https://github.com/ritzyed/ritzy-demo
  - Ritzy editor is a rich text, real-time character-by-character collaborative embeddable browser-based editor.
  - 依赖react、swarm.v0.3
  - 采用flux架构，暴露了state/action
  - It shuns(避免) use of the `contentEditable` attribute in favor of a custom editor surface and layout engine, exactly like the approach implemented by Google Docs.
  - Ritzy is built with real-time collaborative editing support from the ground up, underlying mechanism for this is a **causal tree CRDT**.
  - Unlike Google Docs, Ritzy does not (currently) support complex page-based layout needed to build a word processor.

- https://github.com/conclave-team/conclave /202106/js/lseq/inactive
  - https://conclave-team.github.io/conclave-site/
  - CRDT and WebRTC based real-time, peer-to-peer, collaborative text editor
  - 示例使用simplemde、rxjs、peerjs
  - Intrigued by collaboration tools like Google Docs, we set out to build one from scratch. 
  - Conclave uses (CRDT) to make sure all users stay in-sync and WebRTC to allow users to send messages directly to one another.
  - We implemented an “adaptive allocation strategy for sequence CRDT” called LSEQ(exponential tree).
  - Similar non-academic implementation with optimizations and tweaks - based on Logoot/LSEQ.

- https://github.com/geetesh-gupta/py-crdt-collab-editor
  - CRDT based collaborative code/text editor.
  - 依赖flask，requests

- https://github.com/prSquirrel/crdt-demo /ts/rga
  - A collaborative text editor demo based on Causal Tree CRDT (variant of RGA).
  - 编辑器基于textarea
  - currently no STUN/TURN servers are configured, so it only works with local peers
  - Uses WebSockets for signaling and WebRTC Data Channels for p2p communication. 
  - use a Splay tree implementation

- https://github.com/ROKAF-ResourceManagementSystemDeveloper/crdt /ts/go/rga
  - Simple demo of CRDT(Conflict-free Replicated Data Types)

- https://github.com/mountainflo/collaborative-text-editor /js/go
  - Collaborative realtime texteditor with gRPC using RGAs (Replicated Growable Arrays).
  - using a variant of RGAs.
  - The RGA-protocol is implemented as Timestamped Insertion Tree (TI Tree) 

- https://github.com/munhitsu/CRAttributes /swift
  - Enables colaboration on text field (and other fields) across multiple iOS devices.
  - A nearly vanilla implementation of CRDT RGA (operation per character).

- https://github.com/peer-base/peer-pad /201907/js
  - Online editor providing collaborative editing in really real-time using CRDTs and IPFS.
  - 依赖codemirror5、quill.v1、remark.v10

- https://github.com/nybblr/LSEQTree
  - provide an implementation of a CRDT-based array  with an underlying exponential tree and the allocation strategy LSeq

- https://github.com/widmogrod/js-crdt /ts/201711
  - explore applications of data structure called CRDT in context of real time collaboration 
  - https://github.com/widmogrod/notepad-app
    - Collaborative notepad app (demo).
    - 依赖quill

- https://github.com/MatherLyn/co-editing-engine
  - A co-editing engine based on crdt written in JavaScript.

## rust

- https://github.com/bazed-editor/bazed /rust/rope/inactive
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
- https://github.com/mweidner037/position-strings
  - implements a list/text CRDT with a "lightweight" API based on lexicographically-sorted strings.
  - You can also think of position-strings like fractional indexing, but with a few extra features: global uniqueness, non-interleaving, and slower (logarithmic) length growth in sequences.
  - ["Position Strings" for Collaborative Lists and Text](https://mattweidner.com/2023/04/13/position-strings.html)
    - position-strings is supposed to make it easy to add list/text CRDT functionality to an existing data model, such as a database table. 
    - The example app uses it to build a collaborative text editor on top of Firebase RTDB.
- https://github.com/mweidner037/firebase-text-editor
  - Collaborative plain text editor using CRDTs on top of Firebase (Realtime Database).
  - 依赖position-strings，不依赖quill
  - https://github.com/mweidner037/firebase-rich-text-editor
    - 依赖quill.v1

- https://github.com/mweidner037/vlcn-rich-text
  - Collaborative rich text editor over vlcn.io

- https://github.com/nomad/cola /rust
  - A text CRDT for real-time collaborative editing
  - [cola: a text CRDT for real-time collaborative editing_202309](https://nomad.foo/blog/cola)
    - It’s about as fast as (if not faster than) the fastest rope libraries in both directions, and it’s currently the fastest text CRDT implementation I know of.

- https://github.com/mweidner037/uniquely-dense-total-order
  - Uniquely Dense Total Orders for List/Text CRDTs
  - This is a concept similar to fractional indexing, but resilient to concurrent insertions.
  - [Plain Tree: A Basic List CRDT](https://mattweidner.com/2022/10/21/basic-list-crdt.html)
    - The rest of this post introduces a basic UniquelyDenseTotalOrder that I especially like. 
    - I have not seen it in the existing literature, although it is similar enough to Logoot, Treedoc, and others that I wouldn’t be surprised if it’s already known. For now, I call it Plain Tree.

- https://github.com/josephg/simple-crdt-text /ts/rga
  - This implements automerge's underlying algorithm (RGA)
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.
  - [automerge-and-yjs-minimal.ts](https://gist.github.com/josephg/26ade72d5ced0470485c734fb1ebb6ca)
  - [yjs-minimal.ts](https://gist.github.com/josephg/dcb1bce2ceb0f0b50ffcac0245a55907)
  - [yjs_testcase.ts](https://gist.github.com/josephg/88c006724435a61afaec5ff3f1bacd87)

- https://github.com/kindone/text-versioncontrol
  - provides version and concurrency control for text editing based on OT(Operational Transformation) and CRDT(Conflict-free Replicated Data Type) ideas
  - Text-VersionControl utilizes Quill's Delta representation in JSON. 
  - Text-VersionControl borrows Quill Delta's representation and many of its method names but does not behave the same in a few cases.

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

- https://github.com/crdt-ibm-research/json-delta-crdt /js/inactive
  - JSON CRDT Using Delta-Mutations
  - Prototype implementation of delta based CRDTs supporting JSON data using Javascript.

- https://github.com/jackyzha0/bft-json-crdt /202211/rust/rga
  - the first JSON-like Byzantine Fault Tolerant CRDT in Rust
  - An RGA-like list CRDT
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

- https://github.com/codesandbox/crdt-tree /ts
  - A highly-available move operation for replicated trees and distributed filesystems
  - https://github.com/maidsafe/crdt_tree /rust
# crdt-table/spreadsheet/excel
- https://github.com/Horusiath/crdt-table /5Star/GPLv3/202309/js
  - This is proof of concept for Conflict-free Replicated Data Type representing 2-dimensional table
  - Insert or update existing rows (conflict resolution timestamp per cell basis)
  - Insert new series of rows in between existing rows.
  - Row/column inserts are resolved using `LSeq` - while it has interleaving issues, we believe its not that important on that field as when it comes to ie. collaborative text editing.
    - Cell updates and cell updates against row/column deletions are resolved using Last-Write-Wins semantics.
    - There's a minimal overhead related to keeping tombstone information when entire rows/columns are deleted. This could also be shifted to partially ordered log for keeping info about commutative updates.
  - This implementation uses a combination `{HybridLogicalTimestamp,PeerID}` as a means of conflict resolution, which on positive side is quite lightweight, but otherwise is pretty cumbersome: possible clock drifts on client devices; no ability to recognize concurrent updates ie. conflict resolution for things like update cell / delete column now depends on the clock timestamp
    - Easiest proposal is to switch to vector versions, with optional clock timestamps where useful, but they can be quite heavy (especially if used on per cell basis). 
    - Another proposal is to use partially-ordered log to detect concurrent conflicts (which would be also usefull ie. for undo/redo feature).
  - Selections represents focused areas within a table/grid. In this PoC selections defined by user API using similar `{row:number,col:number}` pairs of opposite corners, however as row and column numbers can change under concurrent updates, **the internal representation of selection uses fractional keys (keys used internally by `LSeq` to establish order)**.
    - Quite often we need to react on changes happening within the boundaries of the selection.This requires efficient way to find selections that contain given cell or intersect with range of changed cells (ie. when we copy paste multiple rows/columns).
    - For small number of selection brute(纯体力的) force over all known selections wouldn't be an issue. 
    - For bigger number, we could modify indexing structures for 2-dimensional data such as R-Trees (used ie. to index geospatial data).

- @fluid-example/table-view /MIT/ts
  - https://github.com/microsoft/FluidFramework/tree/main/examples/data-objects/table-view
  - Table View is a basic table/grid view built on top of the @fluid-example/table-document data object. 
  - Since Table View uses the data model provided by Table Document it only uses it's DDS to store a reference to the created Table Document.
  - Table View uses the following distributed data structures: SharedDirectory - root

- https://github.com/itoumlilt/CRDT-Spreasheet /ts
  - CRDT based collaborative Spreadsheet
  - 依赖concordant-crdtlib、delta-crdts
  - This demo app shows a collaborative application developed using a draft implementation of the `Concordant` API.
  - The application uses the C-Service API which currently supports two eventual consistency backends: revision-based and CRDT-based

- https://github.com/Roffelchen/spreadsheet-crdt /js/yjs
  - /yjs

- https://github.com/fabian-gubler/cellster 
  - Local-first collaborative spreadsheet editing: Harnessing CRDTs for seamless offline formula merges.
# crdt-utils
- https://github.com/mweidner037/fugue /ts
  - Code and benchmarks for the paper "The Art of the Fugue: Minimizing Interleaving in Collaborative Text Editing"
  - Tree-Fugue Simple, List-Fugue Simple

- https://github.com/danielstaleiny/CRDT-sqlite
  - 依赖 idb
- https://github.com/awmuncy/sqlite-crdt
  - 使用sql.js、wasm的示例

- https://github.com/SerenityNotes/naisho
  - an architecture to relay end-to-end encrypted CRDTs over a central service.
  - End-to-end encrypted document using Yjs incl. Cursor Awareness
  - End-to-end encrypted todo list using Automerge

- https://github.com/jakobivarsson/neuron /js/inactive
  - Neuron is a replicated real-time collaborative data store
  - Replicated: Data should automatically be synced across participants.
  - Real-time: Synchronization should be efficient and fast, updates should be applied optimistically (optimistic replication)
  - Collaborative: Concurrent edits should be merged and conflicts automatically handled
  - Data store: Support basic data types such as Map, List, String, Number and Bool as well as embedding in Map and List
  - Ordered list based on the RGA CRDT.

- https://github.com/mitkury/toy-crdt-js /js
  - ReplicatedTreeOfBlocks is based on the CRDT algorithm called RGA

- https://github.com/yorkie-team/yorkie /apache2/go
  - Yorkie is an open source document store for building collaborative editing applications. 
  - Yorkie uses JSON-like documents(CRDT) with optional types.
  - Clients can have a replica of the document representing an application model locally on several devices.
  - Each client can independently update the document on their local device, even while offline
  - Yorkie provides SDKs for Go, JavaScript, iOS, and Android

- https://github.com/cudr/scto
  - Strings Comparing To Operations (OT model)
  - This package is similar to jsdiff, but generates OT-friendly operations.

- https://github.com/Haotian-Yang/CRDTree
  - 服务端基于ws

- https://github.com/slashdotted/libmelda /rust
  - A General Purpose Delta State JSON CRDT
  - Melda natively supports the JSON data format and provides a way to synchronize changes made to arbitrary JSON documents.
  - In the Kibi w/Melda repository you can find a fork of the original Kibi text editor with collaboration features implemented using Melda.
  - https://github.com/slashdotted/kibi
    - In this fork, simple collaboration features based on Melda have been implemented. 
    - The implemented paradigm is save and refresh: when the user saves the local copy, changes from other users are merged.

- https://github.com/soundcloud/roshi /3.1kStar/bsd/go/soundcloud
  - Roshi implements a time-series event storage via a LWW-element-set CRDT with limited inline garbage collection. 
  - Roshi is a stateless, distributed layer on top of Redis and is implemented in Go. 
  - It is partition tolerant, highly available and eventually consistent.
  - [Roshi: a CRDT system for timestamped events | SoundCloud Blog_201405](https://developers.soundcloud.com/blog/roshi-a-crdt-system-for-timestamped-events)

- https://github.com/hyoo-ru/crowd.hyoo.ru /ts
  - Delta based CRDT with additional abilities.
  - Total Available Real-Time Causal Consistency.
  - Merge result is independent of merge order (except auth units).
  - Merge is semilattice.
  - Wiped data inside some Head stays tombstone to hold place.
# crdt-db
- https://github.com/AntidoteDB/antidote /erlang
  - A planet scale, highly available, transactional database built on CRDT technology
  - [Antidote: CRDT-based distributed database | Hacker News_201712](https://news.ycombinator.com/item?id=15862895)
# crdt-rust
- https://github.com/josephg/diamond-types /rust
  - This repository contains a high performance rust CRDT for text editing. 
  - This is a special data type which supports concurrent editing of lists or strings (text documents) by multiple users in a P2P network without needing a centralized server.
  - This version of diamond types only supports plain text editing. 
    - Work is underway to add support for other JSON-style data types. 
  - [diamond-types/INTERNALS](https://github.com/josephg/diamond-types/blob/master/INTERNALS.md)
  - [Question: some question about 《5000x faster CRDTs: An Adventure in Optimization》](https://github.com/josephg/diamond-types/discussions/9)
    - RGA conceptually forms a tree. My contribution is that we can represent that tree using a list.
    - Yjs uses a different CRDT algorithm than RGA. (It uses YATA). 
    - `left` in YATA is semantically equivalent to the `parent` field in Yjs. 
    - Yjs has no `seq` field. RGA has no `right` field.

- https://github.com/RhizomeDB/rs-rhizome /MIT/rust
  - https://fission.codes/ecosystem/rhizomedb/
  - an in-development database for use in building local-first applications over a content addressable store, like IPFS.
  - RhizomeDB employs our PomoDB protocol to execute a local-first edge database for querying decentralized data. 
  - It extends support for concurrent access to structured and unstructured data distributed in content-addressable networks and enables the creation of decentralized, collaborative applications.
  - [Ship TodoMVC as an example app later](https://github.com/RhizomeDB/rs-rhizome/issues/83)
  - [Rhizome on top of RDF?](https://github.com/RhizomeDB/rs-rhizome/discussions/107)
    - One way of looking at Rhizome is "RDF without the RDF" bits
    - We use quads and SPOC for example — though we think about it more as EAVC instead of SPOC
    - We don't use any of the "Resource Description" parts of RDF, and are focused on things like incremental view maintenance for collaborative docs, row-level encryption, and , which the RDF community has historically not needed / explored. 
    - Rhizome more focused on providing a database and CRDT primitives — despite the surface similarity of being a tuplestore, it's is **closer to something like Datomic or Automerge than RDF**.
    - I see, incremental view maintenance is a powerful concept. Crucial to make CRDTs at Datalog-level efficient / practical.

- https://github.com/iambriccardo/causal /rust/Operation-based
  - a simple Reliable Causal Broadcast (RCB) protocol written in Rust that implements several CmRDTs.
  - The operations are commutative. However, they are not necessarily idempotent. The communications infrastructure must therefore ensure that all operations on a replica are delivered to the other replicas, without duplication, but in any order.
# apps-examples
- https://github.com/josephg/statecraft /ISC/201911/ts/inactive
  - Statecraft is a protocol and set of tools for interacting with data that changes over time. 
  - It is the spiritual successor to Sharedb.
  - The store guarantees that the data is immutable with respect to time. (So if the data changes, the version number goes up).
    - Stores can choose how much historical data to store and return.
  - Stores provide a standard set of methods to interact with the data: fetch/mutate/subscribe
  - A Statecraft store is more than just a database abstraction
    - Unlike traditional transactional databases, Statecraft stores compose together like LEGO. Stores wrap one another
  - The philosophy of Statecraft is to "ship the architecture diagram". 
    - The API is designed to make it easy to re-expose a statecraft store over the network.
  - [Show FDB: A scalable realtime text editor on top of foundationdb_201901](https://forums.foundationdb.org/t/show-fdb-a-scalable-realtime-text-editor-on-top-of-foundationdb/1082)
    - I’m working on a realtime data processing pipeline / event sourcing system lately called statecraft 45. Over the last few days I’ve added foundationdb backend support.
    - The current code also re-stores the whole text document with every edit, but this is just because I haven’t tuned it. 

- https://github.com/Sambigeara/fuzzynote /AGPLv3/go
  - Terminal-based, hyper-fast, CRDT-backed, collaborative note-taking tool

- https://github.com/courajs/referent
  - An offline-first, realtime-collaborative wiki engine

- https://github.com/markandre13/workflow
  - A Collaborative Real-Time White- and Kanban Board
  - maintain drawing in the browser's permanent storage using IndexedDB
  - export/import drawing to/from local file encoded in ISO/IEC 19500-2
  - 偏向画板
  - 依赖knex
# state-management-crdt
- redux-crdt
  - logux
  - local-first-web/state: automerge
  - CRDX

- https://github.com/HerbCaudill/crdx
  - CRDX is a state container for JavaScript apps.
  - It is also an operation-based CRDT. Each operation in the CRDT is signed and encrypted. 
  - This library started life as the internal data store for @localfirst/auth
  - We already have excellent JavaScript CRDT libaries such as Automerge and Yjs. So what does this project bring to the table?
    - Automerge and Yjs define a conflict as two peers assigning different values to the same property, and they resolve conflicts by choosing one of the two values as the "winner", in an arbitrary but predictable way.
    - But what a conflict involves more than one property? Or what if you have your own rules for resolving conflicts? 
    - Detecting conflicts may be more subtle than just noticing when two users concurrently modify a property. 
    - And resolving conflicts may involve requirements that won't let us just resolve conflicts in an arbitrary way.
    - To support peer-to-peer replication, we need to deal with concurrent changes, which means a simple append-only list of actions won’t be sufficient. Instead, we arrange actions in a directed acyclic graph (DAG).

- https://github.com/grrowl/redux-scuttlebutt /201701/js
  - [redux-scuttlebutt; eventually consistent shared state among peers](https://medium.com/@grrowl/redux-scuttlebutt-eventually-consistent-shared-state-among-peers-191d48102079)
  - Self-replicating, self-ordering log of actions shared between peers
  - When we encounter actions with a (one or more actions ago), we rewind and replay history in the correct order.
  - While redux-scuttlebutt facilitates action sharing and enhancing the store, it's the responsiblity of the app's reducers to apply actions. 
  - implement CRDT helpers for reducers to easily implement complex shared data types.
  - `Timestamps are logical (not wall-clock based) and are in the format <logical timestamp>-<source>`.

- https://github.com/hldb/welo /ts
  - peer-to-peer, collaborative states using Merkle-CRDTs
  - HLDB implementation in Typescript
  - [Welo Version 3 tasks-list](https://github.com/hldb/welo/issues/102)
  - https://github.com/hldb/hldb
    - A peer-to-peer database protocol
    - There is no encryption built into the protocol yet.
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

- https://github.com/collabserver/collabserver-grapheditor /cpp
  - a command line graph editor for realtime collaboration using the CollabServer Framework
  - https://github.com/collabserver/collabserver-server /cpp

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
