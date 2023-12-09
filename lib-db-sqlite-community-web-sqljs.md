---
title: lib-db-sqlite-community-web-sqljs
tags: [community, sqlite, sqljs]
created: 2023-12-09T10:04:08.790Z
modified: 2023-12-09T10:04:28.663Z
---

# lib-db-sqlite-community-web-sqljs

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [SQL.js: SQLite Compiled to JavaScript | Hacker News_202011](https://news.ycombinator.com/item?id=25008308)
- sql.js uses emscripten to compile SQLite to webassembly (or to javascript code for compatibility with older browsers)
  - By default, sql.js uses wasm

- SQLite has a system that abstracts various low-level storage operations called VFS - this is the layer that allows SQLite to be portable across different operating systems and environments
  - Recently I’ve wondered how possible it would be to implement a SQLite VFS on top of IndexedDB - and, would such a VFS be competitive in speed to using IndexedDB directly? Or, would it be equivalent to use Emscripten’s existing POSIX-ish filesystem backed by IndexedDB?
  - An IndexedDB VFS would allow sql.js to durably persist data in the browser.
- What is interesting about this approach is that at least for Firefox, IndexDB is implemented using SQLite. So ultimately this approach is SQLite running in SQLite with an IndexDB layer in the middle.
