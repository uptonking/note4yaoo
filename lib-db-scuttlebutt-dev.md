---
title: lib-db-scuttlebutt-dev
tags: [database, scuttlebutt]
created: 2023-09-07T15:56:59.295Z
modified: 2023-09-07T15:57:29.739Z
---

# lib-db-scuttlebutt-dev

# guide

# examples

## extensions

- https://github.com/staltz/ssb-memdb /js
  - Important difference between ssb-memdb and ssb-db2 is a small tweak in ssb.db.add that allows the first message of a feed to be any message. 
  - In ssb-db2 when you call ssb.db.add for the first time for a feed, it validates that it MUST have sequence=1. 
  - In ssb-memdb, the 1st message is inserted with OOO and the remaining are inserted with normal validation. This is to enable sliced replication.
# dev

# more
