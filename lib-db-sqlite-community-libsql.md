---
title: lib-db-sqlite-community-libsql
tags: [community, database, libsql, sqlite]
created: 2023-10-28T17:31:09.680Z
modified: 2023-10-28T17:31:26.535Z
---

# lib-db-sqlite-community-libsql

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## Browser -- do you mean database server? libSQL in WAL mode compiles to #Wasm now. Lots of amazing stuff coming soon
- https://twitter.com/sarna_dev/status/1729404441495814244
  - and here it is: WAL in a browser

- ## I used to think forking sqlite (e.g., @libsqlhq ) was crazy but I'm on board now. 
- https://twitter.com/tantaman/status/1684917032096030722
  - While SQLite is great, I just don't think it is ready for the demands of the coming years.
- What do you mean specifically? The weak update hook?
  1. weak update hook / subscriptions 
  2. lack of write concurrency 
  3. lack of pluggable storage engines (eg custom btree rather than vfs or vtab)
  4. limited types
  5. lack of tiered storage
  - Now abandoned SQLite 4 had fixed 3, SQLite hc-tree might fix 2

- Agree about update hook. BEGIN CONCURRENT is not enough write concurrency? I guess not if you want update hook anyway I wonder how long until libsql has a rocksdb backend
- Notion is using SQLite on mobile, correct? How do you guys deal with reacting to mutations?
  - `sqlite3_update_hook` works for us

- Yeah let’s do it and add cell-level reactivity while we are at it.

- ## Folks, if somebody is interested in contributing to libSQL but finds the main code base too complex for their first contribution, we're kickstarting a new shell, written from scratch in Rust: _20230314
- https://discord.com/channels/1026540227218640906/1026540227218640909/1085099589633331221
  - https://github.com/libsql/libsql/tree/main/src/rust/libsql-shell .
  - It still has lots of missing features and our goal is that it's 100% compatible with the original shell (and beyond).

- ## 🚀🔥 [LibSQL is an open source, open contribution fork of SQLite | Hacker News_202210](https://news.ycombinator.com/item?id=33099222)
- This fork has exactly zero new code, but they already managed to change the license and the code of conduct. Their plans include io_uring, Rust and WASM functions - the first two negate the "single-.c-and-.h multi-platform" paradigm that made SQLite what it is, the third thing seems like a feature very few people would care about. They also want to make SQLite distributed for some reason (uh, just use Postgres?)

- 
- 
- 
