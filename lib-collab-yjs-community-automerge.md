---
title: lib-collab-yjs-community-automerge
tags: [automerge, community, crdt, yjs]
created: 2023-03-07T04:09:57.751Z
modified: 2023-03-07T04:10:13.906Z
---

# lib-collab-yjs-community-automerge

# guide

# discuss
- ## 

- ## 

- ## [Automerge 2.0_202301](https://automerge.org/blog/automerge-2/)
- Earlier versions of Automerge were implemented in pure JavaScript. 
  - Our initial implementations were theoretically sound but much too slow and used too much memory for most production use cases.
  - JavaScript support on mobile devices and embedded systems is limited. 
- Instead of trying to coordinate multiple distinct versions of Automerge, we decided to rewrite Automerge in Rust and use platform-specific wrappers to make it available in each language ecosystem. 
  - This way we can be confident that the core CRDT logic is identical across all platforms and that everyone benefits from new features and optimizations together.
- For JavaScript applications, this means compiling the Rust to WebAssembly and providing a JavaScript wrapper that maintains the existing Automerge API.
