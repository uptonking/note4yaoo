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

- ## SQL from frontend. Is it heresy or valid architecture? 
- https://x.com/nikitabase/status/1856776727407771901
- I think that makes things get started fast and is great for internal tooling, but you have to deal with migration annoyances like ensuring that frontend and DB changes get deployed at the same time. If it’s an SPA, then you need to do hot reload more often. People may also model their data poorly. Good data model may be different than component data model

- imo the nicest thing about postgREST isn't the rest API, it's the jwt middleware that lets you pool your conns under a common 'authenticator' identity and base the rls/security model on jwt claims that are set and evaluated per api request/transaction using a shared conn role

- PHP has been preaching this for years

- ## [SQL.js: SQLite Compiled to JavaScript | Hacker News_202011](https://news.ycombinator.com/item?id=25008308)
- sql.js uses emscripten to compile SQLite to webassembly (or to javascript code for compatibility with older browsers)
  - By default, sql.js uses wasm

- SQLite has a system that abstracts various low-level storage operations called VFS - this is the layer that allows SQLite to be portable across different operating systems and environments
  - Recently I’ve wondered how possible it would be to implement a SQLite VFS on top of IndexedDB - and, would such a VFS be competitive in speed to using IndexedDB directly? Or, would it be equivalent to use Emscripten’s existing POSIX-ish filesystem backed by IndexedDB?
  - An IndexedDB VFS would allow sql.js to durably persist data in the browser.
- What is interesting about this approach is that at least for Firefox, IndexDB is implemented using SQLite. So ultimately this approach is SQLite running in SQLite with an IndexDB layer in the middle.
