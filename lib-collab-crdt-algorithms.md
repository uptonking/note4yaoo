---
title: lib-collab-crdt-algorithms
tags: [algorithms, collaboration, crdt]
created: 2023-03-07T04:43:40.023Z
modified: 2023-03-07T04:43:58.713Z
---

# lib-collab-crdt-algorithms

# guide

- who is using #logoot
  - mute
  - [DTNDocs: A delay tolerant peer-to-peer collaborative editing system_201801](https://ieeexplore.ieee.org/document/8343092)
    - DTNDocs Android application uses IBR-DTN to communicate over a delay tolerant network and a modified LogootSplit algorithm for ensuring consistency in shared contents.

- Oster
  - [Publications – Gérald OSTER](https://members.loria.fr/goster/publications/)
  - 2005年发布WOOT
  - 2017年发布Mute

- tips
  - 学术界的代码大多都是玩具，经过业务产品验证过的更可靠
# crdt-algorithms

## Logoot/LogootSplit

- [A simple approach to building a real-time collaborative text editor - Digital Freepen](https://digitalfreepen.com/2017/10/06/simple-real-time-collaborative-text-editor.html)
  - I adapted Logoot

## WOOT

- 业务产品并不多，参考fro scala.js

- [WOOT](https://github.com/d6y/wootjs) is a collaborative text editing algorithm, 
  - allowing multiple users (`sites`) to insert or delete characters (`WChar`) from a shared document (`WString`). 
  - The algorithm preserves the intention of users, and ensures that the text converges to the same state for all users.
  - Its key properties are simplicity, and avoiding the need for a reliable network or vector clocks (it can be peer-to-peer).

- https://github.com/ryankaplan/woot-collaborative-editor
  - When a textarea-change is detected, diff the textarea content against the last known content. 
  - With the help of WootTypes. WString, turn that diff into `WStringOperations` and broadcast those operations to the server.
  - When we receive operations from the server, apply those operations to our WString instance and apply them to the text in #collab-doc.

## TreeDoc

- https://github.com/mweidner037/uniquely-dense-total-order
  - [Plain Tree: A Basic List CRDT](https://mattweidner.com/2022/10/21/basic-list-crdt.html)
    - The rest of this post introduces a basic UniquelyDenseTotalOrder that I especially like. 
    - I have not seen it in the existing literature, although it is similar enough to Logoot, Treedoc, and others that I wouldn’t be surprised if it’s already known. For now, I call it Plain Tree.

## RGA

- [Operation-based CRDTs: arrays (part 1)](https://www.bartoszsypytkowski.com/operation-based-crdts-arrays-1/)
# discuss
- ## 

- ## 

- ## 

- ## 
