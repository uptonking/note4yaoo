---
title: lib-db-sqlite-community-examples
tags: [community, examples, sqlite]
created: 2022-11-27T18:05:24.364Z
modified: 2022-11-27T18:06:10.599Z
---

# lib-db-sqlite-community-examples





# guide

# discuss
- ## 

- ## 

- ## 

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
