---
title: thread-db-web
tags: [db, thread, web]
created: '2022-02-19T10:25:11.502Z'
modified: '2022-02-19T10:25:22.934Z'
---

# thread-db-web

# discuss

- ## 

- ## 

- ## 

- ## #idea: Compile #SQLite to #WASI to work in a #WebWorker with automatic (!) synchronisation with #IndexedDB. Or wait for #WebSQL to become a standard. Or wait for IndexedDB to become usable. 
- https://twitter.com/vladfaust/status/1523653689050734592


- ## Here's an interesting browser state solution: A database, written in JS, called TinyBase.
- https://twitter.com/housecor/status/1492859757941637126
  - Tables, rows, cells, indexes, relationships, undo, and more. 
  - Persist the data to the browser, files, or a server.
- what sense makes database on client when you need to transfer the data? also all data is public by default
  - You can use it offline.
- Interesting for client-first apps!
  - I'm using Dexie.js on top of IndexedDB, but it has its limitations wrt/ queries (and performance).
  - Another crazy experiment on my list of things to try is @jlongster 's Absurd SQL
- I wonder if theres a world where you use absurdSQL (or raw SQLite wasm) as custom persistor with it? 
  - Currently persistence is just "where can you save and load a JSON string?" at a Store-wise level. So sure! 
  - But I once had an experiment for sharded persistence per table or row. 
  - At that point, keeping it in sync with a 'real' database might be quite scalable and interesting.
