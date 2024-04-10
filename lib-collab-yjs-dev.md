---
title: lib-collab-yjs-dev
tags: [collaboration, yjs]
created: 2022-04-05T10:10:40.177Z
modified: 2022-04-05T10:10:59.826Z
---

# lib-collab-yjs-dev

# guide

- pros
  - good ecosystem: docs, bindings, examples
  - common data types
  - undo/redo
  - versions/revision-history
  - track-changes(suggestion mode)
  - offline-editing
  - awareness
  - network-agnostic
  - bindings for editors/apps
  - persistence

- cons
  - yata冲突处理算法不如rga/fractional-index/logoot/lseq主流
  - 数据传输基于二进制，高性能，但开发调试很不方便，需要devtools
  - 文本格式的添加清除较繁琐

- features
  - Automatic Syncing and no conflicts
  - Offline Support
  - support Peer-to-Peer

- who is using #yjs
  - jupyter
  - gutenberg
  - apps: linear, Gitbook, Evernote, Appflowy(yrs), AppMaster
  - more: Serenity Notes, Skiff
  - [Yjs in the Wild | Yjs Docs](https://docs.yjs.dev/yjs-in-the-wild)

- bindings
  - prosemirror, quill, slate, codemirror, monaco
  - immer, valtio, mobx, SyncedStore

- providers
  - y-websocket, y-webrtc, y-redis, y-sweet
  - Tinybase
  - PartyKit, @liveblocks/yjs
  - Matrix-CRDT

- tips
  - 协作只有文本部分需要YText这类复杂的crdt，表格使用llw-map足够
  - 协作类研发可考虑与event-sourcing结合，状态数据可视为oplog的materialized-view

- 实现协作要考虑到切换冲突处理算法, 如slate-yjs/automerge/sharedb

- https://github.com/yjs/y-protocols
  - Binary encoding protocols for syncing, awareness, and history information
  - We use efficient variable-length encoding where possible.

- [Automerge CRDT Sync Protocol](https://automerge.org/docs/how-it-works/sync/)

- resources
# 🎞️ [cs-repeat: How Yjs works from the inside out with Joseph Gentle & Kevin Jahns __202009](https://www.youtube.com/watch?v=0l5XgnQ6rB4)
- 17:30
- an item is the representation of a linked list
  - list crdt is built on this
  - a tree structure also links to parent

- 19:05
- for a list of strings, a abstract list
- list contains items
  - each item contains contents 
  - content is like 2 objects reference each other
  - so item in list reference the string, and the string.item property is back to the item/value

- Item.id refers to content id
- ID.clock uses lamport timestamp
  - use js number
- id: cliendId + clockNumber从0开始

- one item can represents multi chars
  - for copy paste, not create multi items

- del not generate new clock
  - yjs is specific
  - del in yjs is tombstone property
- at the beginning of the session, you're just gonna send all the del ops 
- yjs is a mix of delta crdt, but deletions are state crdt
- for huge doc, yjs makes del not operations, del is not structure of doc
- deletions are just collections of id numbers
- for ot, op is retain+insert, no delete
- for yjs, add insert, minus delete
- if encode deletions as a separate set, it's more efficient

- for insert
  - yjs insert item between origin and right
  - rga insert to the left/prev item
- rga downsides
  - if u prepend many chars, it slows
  - insert string of length N, the parse and insert is slow
    - parse takes same time as apply insert 
    - before insert, sort takes time

- fast search marker / skip list
  - a skip list refer to positons
  - it index a few positons
  - when apply insert, find pos in skip list, then insert
- yjs use skip list to index most recent 10 pos
  - whenever doc update, skip list is updated

- integrate
  - define an item, insert and resolve conflict
- the chance of 2 users conflict is rare
  - high clientId wins
  - low clientId insert at left

- yjs uses 
  - binary encoding for doc
  - variable-length encoding for all integers

- for crdt, store all operations, but encoding is efficient

- google wave composes operations on local pc, then send to server
  - transform in one go

- transaction/tx
- change needs to happen in tx
- after tx, get a new state afterState
- del op stores deleteSet in tx

- gc struct can merge, then exec gc
- u can disable gc.

- stateVector(from encoding)
  - it's lamport timestamps of all clients
  - like a map from clientId to clock
- snapshots
  - stateVector with deleteSet
- use stateVector and deleteSet, u can revert to any point and time
- if u want to revert to any doc history, u need to store all stateVectors
- create a snapshots, u can revert.
- versions-slider vs time-slider

- structStore
  - a ordered of list
  - use binary search
- the clock of first item is always 0
- deleted property
- always append to list
- if receive item
  - before insert, use binary search to search the new.id === listItem.left
- when insert, not scan whole doc
- 2 ways to insert
  - integrate with skip list
  - use store and binary search
- when sync, slice part of items in store and encode

- why use array to impl structStore
  - automerge uses btree 
- btree doesnot allow u to refer to index positions
- index data and append items is easy when use array
- in the future, I may use red black tree
- joseph
  - jumprope: skip list
  - xi-rope: btree

- all the crdt papers test random insertions
  - but in practice, insert is mostly continuous, use cache maybe better for text editing

- yjs rust maybe use btree, instead of fast-marker
- but for text editing, use cache maybe better because insert mostly is not random, but continuous

- create tx create an update message

- sync in 2 steps
- step1 send my stateVectors
- step2 is deleteSet
- snapshots also contain deleteSet

- del flag seldom toggles back to false
  - so represent concurrent del by merging del
- not encoding del as part of document

- syncing is already efficient

- testing
- simulation is generated using random number generator
- joseph uses fuzzier

- how to use ymap to index js object
- map indexed items with an linked list
- the last item of linked list is current value of map
  - we mark every item not the last item as deleted
- why I prefer this method
  - history is unique
  - overhead is not that important
  - it is not most efficient

- hard to get diff if to support move op

- idea is to set priority property to data
  - move items by redefining priority
  - all these interleaving crdt does this
  - figma does this

- yjs move should support rich text

- y-protocol
  - contains step 1 and 2

- presence is using different
  - cursor sync is not using yjs, but like automerge
- awareness
  - use state-based crdt
- u propagate current state to all clients
  - u assign a clock to your state

- single op perf doesnot matter
  - consider batch operations
  - benchmark tests should contain this
# draft

- 
- 
- 
- 
- 
- 

# dev

# more
