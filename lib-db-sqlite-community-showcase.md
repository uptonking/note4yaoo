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

- ## [WordPress Core to start using SQLite | Hacker News_202307](https://news.ycombinator.com/item?id=36884806)
- Related - WordPress recently released WordPress Playground
  - These utilize WebAssembly (php-wasm) and an SQLite database backend to run a whole WordPress instance in the browser or a local Node.js instance.

- Did you consider using the `temporal_tables` extension? I think it's basically like **version history for tables**. 
  - I haven't used this before personally though. https://pgt.dev/extensions/temporal_tables
  - Temporal Tables Extension requires PostgreSQL 9.2 or higher.

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
