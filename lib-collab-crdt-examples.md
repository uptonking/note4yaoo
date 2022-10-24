---
title: lib-collab-crdt-examples
tags: [collaboration, crdt, examples]
created: 2022-01-22T16:14:32.323Z
modified: 2022-04-05T10:08:25.947Z
---

# lib-collab-crdt-examples

# guide

- state-based和operation-based没必要二选一
  - 两者的主要区别是节点间交换的数据和数据更新策略，两种可转换
  - 对于业界成熟的yjs，是结合两种实现来优化性能的
# popular
- https://github.com/pubuzhixing8/awesome-collaboration
  - Collaborative editing of technical resources, article translation
  - [OT 与 CRDT 的Battle，堪称神仙打架](https://github.com/pubuzhixing8/awesome-collaboration/blob/master/fairy-fight/collaborative-editing.md)

- https://github.com/Horusiath/crdt-examples
  - An example implementations of various CRDTs
  - 实现语言为F#
  - It serves mainly academic purposes (the implementations are meant to be simple and easy to understand, not optimized)

- https://github.com/dmonad/crdt-benchmarks
  - A collection of reproducible CRDT benchmarks.
  - B1: No conflicts
  - B2: Two users producing conflicts
  - B3: Many conflicts
  - B4: Real-world editing dataset

- https://github.com/josephg/crdt-benchmarks
  - The goal of this repository is to provide some standard benchmarks that we can use to compare the performance of various OT/CRDT implementations.
  - This repository contains some editing histories from real world character-by-character editing traces. 

- https://github.com/streamich/json-joy
  - JSON utilities for joy and collaborative editing with OT and CRDT approaches. 
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

- https://github.com/wangdashuaihenshuai/crdt-edit /201810/vue/js
  - [我自己从零实现的一个文本文档的协同编辑demo，上面是输入框，下面是数据结构的可视化](https://zhuanlan.zhihu.com/p/48229762)
  - operation-based crdt
  - 依赖konva的画图app

- https://github.com/siliconjungle/cabinet 
  - https://github.com/siliconjungle/cabinet-client
  - operation-based crdt
  - 也提供了state-based的版本
  - 未提供服务端实现
  - A key value store & subscriptions wrapping a json blob crdt (shelf).
  - https://twitter.com/JungleSilicon/status/1504446998329499653
    - It's operation based but it's very easy to consume and cull(cull sth from sth 选出，挑出) those operations.
    - For anyone interested in collaborative editing, I've implemented a new approach to the shelf CRDT.

- https://github.com/siliconjungle/tiny-merge
  - State-based CRDT with a Tiny footprint.
  - 包含server、client，服务端依赖supabase

- https://github.com/xcesiv/crdt.js
  - This module provides a set of Conflict-Free Replicated Data Types for your JavaScript programs. 
  - All CRDTs in this library, except G-Counter, are currently operation-based.
  - https://github.com/orbitdb/crdts

- https://github.com/ipfs-shipyard/peer-crdt
  - An extensible collection of operation-based CRDTs that are meant to work over a p2p network.
  - https://github.com/peer-base/js-delta-crdts
    - Delta state-based CRDTs in Javascript.

- https://github.com/siliconjungle/crdt-likes
  - A simple example of how to build offline-first likes using CRDT's.

- https://github.com/josephg/simple-crdt-text
  - This is a simple CRDT implementation for the CRDT I want to efficiently implement in rust. 
  - This implementation is intentionally not optimized. 
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.
  - This implements automerge's underlying algorithm (RGA)

- https://github.com/siliconjungle/recycle-list-crdt
  - A crdt that recycles tombstones.
- https://github.com/siliconjungle/delta-crdt
  - A simple delta CRDT implementation.

- https://github.com/dglittle/shelf
  - Here is a shelf: [VALUE, VERSION_NUMBER]

- https://github.com/nkohari/kseq
  - KSeq is an implementation of a simple CRDT that represents an ordered sequence of items. 
  - KSeq is an operations-based, continuous sequence CRDT based on the Logoot and LSEQ systems.
  - Designed for use in collaborative editors, it allows various contributors to concurrently alter the sequence, while preserving both data and intent.

- https://github.com/Timothy-Harianja/CRDT-Collaboration-App
  - This project is aimed to experiment on the capabilities of CRDT and OT. 
  - One of the practical uses out these concepts is offline collaboration feature.
  - 依赖automerge

- https://github.com/bcherny/crdt-demo
  - WOOT-style CRDT implementation
  - 提供了server
  - 前端依赖draftjs
  - WOOT propagates identifier-based operations defined on the internal object 

- https://github.com/phedkvist/crdt-woot
  - Implementation of collaborative editing algorithm CRDT WOOT.
  - [Introduction to Conflict Free Replicated Data-type](https://medium.com/swlh/introduction-to-conflict-free-replicated-data-type-959a944098c4)

- https://github.com/phedkvist/crdt-server
  - A text based CRDT server storing, sending and receving updates using Express and Websockets

- https://github.com/phedkvist/crdt-sequence
  - CRDT Sequence is a very basic collaborative text editing implementation
  - 依赖 quill-cursors
# yjs-crdt
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

- https://github.com/inkandswitch/peritext
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - This repo includes:
    - A Typescript implementation of the core Peritext CRDT algorithm
    - A prototype integration with the [Prosemirror](http://prosemirror.net/) editor library
    - An interactive demo UI where you can try out the editor
    - A test suite
# crdt-repos
- https://github.com/netopyr/wurmloch-crdt
  - Experimental implementations of conflict-free replicated data types (CRDTs) for the JVM

- https://github.com/anshulahuja98/python3-crdt
  - A python library for CRDTs (Conflict-free Replicated Data types)
- https://github.com/junjizhi/lww-element-set
  - Last-Writer-Wins Element Set(lww-set) data structure implemented in Python

- https://github.com/orda-io/orda
  - Orda: A client and server written in Go. CRDT-based data synchronization supporting document database.
  - Orda project is a multi-device data synchronization platform based on MongoDB (which could be other document databases such as CouchBase). 

- https://github.com/hughfenghen/rtc-live-show
  - 基于WEB RTC + rrweb实现的页面“直播”demo
