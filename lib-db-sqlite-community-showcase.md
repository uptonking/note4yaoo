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

- ## 🔥 [Show HN: WarcDB: Web crawl data as SQLite databases | Hacker News_202206](https://news.ycombinator.com/item?id=31799147)
- 
- 
- 

- ## 🔥 [Wp-SQLite: WordPress running on an SQLite database | Hacker News_202205](https://news.ycombinator.com/item?id=31396732)
- 
- 
- 

- ## [WordPress Core to start using SQLite | Hacker News_202307](https://news.ycombinator.com/item?id=36884806)
- Related - WordPress recently released WordPress Playground
  - These utilize WebAssembly (php-wasm) and an SQLite database backend to run a whole WordPress instance in the browser or a local Node.js instance.

- Did you consider using the `temporal_tables` extension? I think it's basically like **version history for tables**. 
  - I haven't used this before personally though. https://pgt.dev/extensions/temporal_tables
  - Temporal Tables Extension requires PostgreSQL 9.2 or higher.

- ## Announcing Deno KV: A Global Database for Global Apps! Built on FoundationDB and SQLite_202304
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

- ## 🚀🔥 [D1: Our SQL database | Hacker News_202205](https://news.ycombinator.com/item?id=31339299)
- [Announcing D1: our first SQL database](https://blog.cloudflare.com/introducing-d1/)
  - D1 is built on SQLite. 
- 
- 
- 

- ## Here is Harika. The offline-first note-taking app on top SQLite (using absurd-sql for web version)
- https://twitter.com/quolpr/status/1558848201771319298
  - It uses LWW per field CRDT and stores all changes on the server, so time travel is possible to implement.
  - And SQLite allows storing huge amount of data with the instant startup time 
  - I managed to pause work on it because I don't have enough resources (money/time) to keep working on it
- 👉🏻 What do you use for text editing?
  - it's mobx-keystone. I partially load data from SQLite into mobx-keystone. Then all the changes are happening in-memory and after short delay are dumped back to SQLite
  - It's just textarea that render to just HTML on unfocus. To parse input to AST I use pegjs
- How does the sync work?
  - Very roughly — every 500ms it collect all the changed that were done to the doc, and saves to the changes table. Then, when you are back only, all of these changes will be sent to the server.
  - The server will have a collection of all changes from all clients, so he will be able to calculate the final view of each entity, and send back to the clients.
  - If some changes came from the past (like you used offline mobile, and you also used desktop online) — it will recalculate the snapshot with the new changes came from phone, so you will never lose your data
  - Change = the diff of the doc between new and old state
- What is your experience with absurd-sql. would you recommend it ?
  - right now, absurd-sql has race condition bug in multi tab usage, and require using COOP headers (that restricts to embed YouTube video, for example)
  - And right now I am working on asyncify version of wasm SQLite, and it will have the same performance as absurd-sql has, but without multi-tab bug and COOP header requirement. I hope my company will open-source it 🙂 Cause then we will be able to use SQLite without any limits
- With it, I was able to unlock x5-20 performance boost, but it's pretty raw to use. I wrote a simple wrapper around absurd-sql  
  - https://github.com/kikko-land/kikko
  - It supports transactions, middlewares, and guide how to set up absurd-sql for CRA/vite
  - if you have performance issues, and don't like IndexedDB — just use absurd-sql (or trong-orm hehe 😜)

- ## 🔥 [Show HN: WunderBase – Serverless OSS database on top of SQLite, Firecracker | Hacker News_202209](https://news.ycombinator.com/item?id=32852478)
- 
- 
- 
