---
title: lib-collab-fluid-dev
tags: [collaboration, fluid-framework]
created: 2023-02-11T11:06:16.495Z
modified: 2023-02-11T11:06:50.571Z
---

# lib-collab-fluid-dev

# guide

- pros
  - 灵活可扩展的数据结构dds

- cons
  - The Fluid Framework requires a Fluid service to sync data between clients. 不直接支持p2p
  - 代码抽象较复杂，包括core/runtime/dds/container/view/sequence
# not-yet
- sequence包的原理
# dev
- [@fluidframework/protocol-definitions Package](https://fluidframework.com/docs/apis/protocol-definitions)
  - Fluid protocol interfaces shared between services and clients.

- https://github.com/yjs/y-protocols
  - Binary encoding protocols for syncing, awareness, and history information
  - We use efficient variable-length encoding where possible.

- [Automerge CRDT Sync Protocol](https://automerge.org/docs/how-it-works/sync/)
# more
