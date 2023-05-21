---
title: lib-db-sqlite-community-showcase
tags: [community, showcase, sqlite]
created: 2023-04-30T16:50:54.098Z
modified: 2023-05-21T14:54:15.817Z
---

# lib-db-sqlite-community-showcase

# guide

# discuss
- ## 

- ## 

- ## Announcing Deno KV: A Global Database for Global Apps! Built on FoundationDB and SQLite
- https://twitter.com/deno_land/status/1651972190965837825
  - ACID transactions

- Or, with similar or better levels of performance, you can make the database appear to disappear, and end up with persistent JS objects
  - https://github.com/robtweed/glsdb
    - Global Storage Database Abstraction for Node.js

- Is there a way to create tables / collections with this? It looks like every key is on the same table.

- https://twitter.com/zen0wu/status/1652372212379418626
  - the array-based JSON keys looks a lot like @ccorcos 's tuple-database, and it's also FoundationDB based
  - It’s quite similar. I wonder why Deno opted for manual consistency checks rather than it being automatic on reads though.
- It seems common in distributed KV stores to allow clients to choose a low-latency-but-weak-consistency read or a high-latency-but-strongly-consistent read. It seems like reads default to “strong”
