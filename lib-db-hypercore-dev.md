---
title: lib-db-hypercore-dev
tags: [database, hypercore]
created: 2023-09-07T15:57:40.496Z
modified: 2023-09-07T15:58:04.082Z
---

# lib-db-hypercore-dev

# guide

- pros
  - mutable and versioning
  - support streaming large-data/subset
  - network agnostic

- cons
  - few showcases

- features
  - Uses append-only log
  - dat offers mutability whereas IPFS doesn't
  - No block-level dedup. 
    - Change in one byte, creates a new version of the file. 
    - File-level dedup can be achieved with additional management level, called corestore.

- who is using #hypercore
  - Tradle

- 选择与比较
  - data model
  - mutable
  - persistence
  - sync and networking
  - conflicts
  - auth and permissions
  - ecosystem/layers/stacks
# dev
- Dat was renamed to Hypercore in 2020
# more
