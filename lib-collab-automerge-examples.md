---
title: lib-collab-automerge-examples
tags: [automerge, collaboration, examples]
created: 2023-09-01T10:18:00.949Z
modified: 2023-09-01T10:18:14.842Z
---

# lib-collab-automerge-examples

# guide

# popular

# examples
- https://github.com/jonfk/text-crdt-experiment-automerge-ts /ts
  - http://jonfk.github.io/text-crdt-experiment-automerge-ts
  - Small experiment project to test out Automerge text features to see if it would be a usable for the core data structure of an offline first syncing text editor.
  - 依赖automerge.v0.12、diff-match-patch、react-redux

- https://github.com/richardanaya/crdt-todo
  - An example application using CRDT library Automerge to make a TODO app

- https://github.com/andrewinci/free-retro
  - https://retroapp.amaker.xyz/
  - A retro board inspired by retrium
  - 依赖automerge.v2、mantine、react-dnd、emotion

- https://github.com/pvh/automerge-prosemirror-workbench
  - testbed for automerge/prosemirror

- https://github.com/block-based-editors/automerge-tree
  - https://block-based-editors.github.io/automerge-tree/
  - (real-time) collaboration on blocks with automerge saved in a tree

- https://github.com/ben-ryder/automerge-encryption-demo
  - A proof of concept using Automerge in a React app with client-side encryption, multi device sync via a server and more.

## automerge-hypercore

- https://github.com/extendedmind/peermerge /rust
  - Peer protocol (hypercore or p2panda) + Automerge in Rust

- https://github.com/Ruulul/automerge_hypercore_demos /js
  - local_sync_textareas
# automerge-v1
- https://github.com/automerge/hypermerge /MIT/ts/archived
  - Hypermerge is deprecated. 
  - Hypermerge is a Node.js library for building p2p collaborative applications without any server infrastructure. 
  - It combines Automerge, a CRDT, with hypercore, a distributed append-only log.
  - Hypermerge is a distributed document store. It draws inspiration from databases like CouchDB and PouchDB
  - hypermerge document is built up by applying a series of changes generated on different clients. 
    - Every time you open a hypermerge document, the system replays all the logs of changes from every client to recreate the document state. 
    - This can be slow and expensive for large documents, but has excellent history-preserving properties and guarantees clients can always return to earlier states or merge new changes as they arrive.
  - Hypermerge stores an automerge document as a set of separate Hypercores, one per actor ID. Each actor ID in the document is the discovery key of a Hypercore, which allows recursive lookup.
  - This strategy works for a small number of documents, but is very slow to synchronize due to the vast number of Hypercores required for a large collection.
  - [Every opened hypercore keeps a file handle open permanently](https://github.com/automerge/hypermerge/issues/69)

- https://github.com/jonfk/text-crdt-experiment-automerge-ts
  - test out Automerge text features to see if it would be a usable for the core data structure of an offline first syncing text editor.

- https://github.com/nornagon/autowiki
  - a tool for creating networked documents.
# utils

# more
