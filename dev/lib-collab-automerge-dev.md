---
title: lib-collab-automerge-dev
tags: [automerge, crdt]
created: 2023-09-01T10:15:40.319Z
modified: 2023-09-01T10:16:03.555Z
---

# lib-collab-automerge-dev

# guide

- pros
  - rust/js/binding
  - team-work

- cons
  - 与同团队的loro/pretext定位相同，前景不明确
  - 使用案例不如yjs多

- features
  - ?

- [Automerge CRDT Sync Protocol](https://automerge.org/docs/how-it-works/sync/)
# not-yet

# draft
- 将https://github.com/automerge/hypermerge迁移到v2
# dev

# tiny-essay-editor

- https://github.com/inkandswitch/tiny-essay-editor /NALic/202405/ts
  - https://tee.inkandswitch.com/
  - simple markdown editor w inline comments, on latest automerge stack
  - a simple collaborative Markdown editor built in React, with inline format preview and inline commenting.
  - built on automerge and automerge-repo for CRDT-based storage and sync. 
  - 依赖automerge2、codemirror6、@lezer/highlight、@radix-ui、tldraw2、@xstate/react、cmdk
  - https://x.com/geoffreylitt/status/1752379702377873894
    - Just gave a talk about Tiny Essay Editor, a collaborative markdown editor we're using at @inkandswitch based on Automerge _202401
    - We wanted a nice local-first editor for writing our research essays, so we built one
    - automerge as core CRDT
    - automerge-repo for networking/storage
    - codemirror for markdown editing, automerge-codemirror for editor integration
    - For TEE we just store a string for the contents, plus some JSON data for comments.
    - One feature that's *lovely* to build w/ Automerge: attaching comments to text.
    - TEE is local-first, meaning clients are source of truth and there's no central authority.
# more
