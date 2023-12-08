---
title: lib-db-scuttlebutt-dev
tags: [database, scuttlebutt]
created: 2023-09-07T15:56:59.295Z
modified: 2023-09-07T15:57:29.739Z
---

# lib-db-scuttlebutt-dev

# guide

- https://github.com/nichoth/ssb-field-guide
  - A field guide to developing with ssb
# examples
- https://gitlab.com/staltz/manyverse /MPLv2/ts
  - https://manyver.se/
  - A social network off the grid

## extensions

- https://github.com/staltz/ssb-memdb /js
  - Important difference between ssb-memdb and ssb-db2 is a small tweak in ssb.db.add that allows the first message of a feed to be any message. 
  - In ssb-db2 when you call ssb.db.add for the first time for a feed, it validates that it MUST have sequence=1. 
  - In ssb-memdb, the 1st message is inserted with OOO and the remaining are inserted with normal validation. This is to enable sliced replication.

## utils

- https://github.com/mafintosh/hyperlog /201701/js
  - Merkle DAG that replicates based on scuttlebutt logs and causal linking
  - [Hyperlog vs Hypercore?_201709](https://github.com/mafintosh/hyperlog/issues/38)
    - You're right that hyperlog models a DAG (directed acyclic graph). It models a graph, but underneath it is a collection of different users' append-only logs. 
    - hypercore models a single append-only log.
    - Hyperlog is perhaps the less modular one: it builds the append-only log mechanism and the indexes & logic to model a DAG on top, all in a single module.
    - Another distinction is partial sync. Hyperlog's replication mechanism must exchange all data of all append-only log entries in order to function. Hypercore, however, operates fine with only a partial subset of entries replicated. This property is held on the higher level modules built on hypercore, like hyperdrive and hyperdb.
# dev

# more
