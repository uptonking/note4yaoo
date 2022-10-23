---
title: lib-collab-crdt
tags: [collaboration, crdt, pattern]
created: 2021-07-23T15:50:09.211Z
modified: 2022-04-05T10:10:08.537Z
---

# lib-collab-crdt

# guide

- crdt的实现思路
  - 基于state
    - yjs
  - 基于operation
    - cabinet
  - ？基于history

- [An introduction to state-based CRDTs_201712](https://bartoszsypytkowski.com/the-state-of-a-state-based-crdts/)

- [Pure operation-based CRDTs_202104](https://bartoszsypytkowski.com/pure-operation-based-crdts/)
- [Operation-based CRDTs: JSON document_202103](https://bartoszsypytkowski.com/operation-based-crdts-json-document/)
# yjs vs automerge

## [yjs Compared to Automerge](https://github.com/yjs/yjs/issues/145)

- You are welcome to ask about the differences. 
- I don't have much experience with automerge. 
  - If I understand correctly, automerge was primarily build for sharing application state. 
  - They decided to make application state immutable, and therefore it nicely integrates into react applications.
- Yjs was primarily build for shared editing on text and rich-text. 
  - Yjs exposes state as mutable data types. 
  - State is mutable by design, because some computations can be done more efficiently on mutable objects.
- I would argue that Yjs is the better choice if you plan to share huge (text / rich-text) documents, 
  - because 1. its algorithm is specifically designed for shared editing and 
  - 2. it encodes its structure very efficiently in a binary format. 
  - Automerge on the other hand might be easier to handle because state changes are just operations on the shared document.
- If you are not working on a shared editing application and you are not hitting any performance problems, then you are probably fine with automerge. 
  - Otherwise you should definitely consider Yjs.
- I created a set of benchmarks to compare Yjs with Automerge
  - https://github.com/dmonad/crdt-benchmarks
# ref
- [KeyValueCRDT](https://bdewey.com/til/2021/08/21/)
  - https://github.com/bdewey/KeyValueCRDT /swift
  - My goal with KeyValueCRDT is to provide a CRDT implementation that can work as a file format for a wide range of applications.
  - KeyValueCRDT uses SQLite for its storage

- [Peritext: A CRDT for Rich-Text Collaboration](https://www.inkandswitch.com/peritext/)
  - supports overlapping inline formatting, and shown how to implement it efficiently.
  - it simply allows two versions of a rich-text document to be merged automatically.
