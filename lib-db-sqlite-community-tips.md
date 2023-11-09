---
title: lib-db-sqlite-community-tips
tags: [community, dev-xp, sqlite]
created: 2023-10-28T13:37:34.769Z
modified: 2023-10-28T13:38:46.522Z
---

# lib-db-sqlite-community-tips

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-license-sqlite
- ## 

- ## 

- ## [Making a change to SQLite source code | Hacker News_202210](https://news.ycombinator.com/item?id=33339634)
- Not mentioned is that the full test sqlite test suite is proprietary and you need a super expensive sqlite foundation membership to get access to it. That means (unless you get that membership), your patched/forked version will be less extensively tested than the official version. So sqlite is in reality very difficult to fork. Sqlite is very solid, but bugs do sometimes show up in it despite all that testing, and more relevantly, some bugs in development are presumably caught by the testing, which outsiders don't have access to.

- ## [SQLite's proprietary test suite is its secret sauce that has kept it closed to contributions... | Hacker News](https://news.ycombinator.com/item?id=33083993)
- SQLite's proprietary test suite is its secret sauce that has kept it closed to contributions and kept forks from happening. It is the thing that made the SQLite Consortium a going business proposition. It is the thing that makes it possible to fund an open source infrastructure project with a small, cohesive team.
  - Any fork will instantly lose the benefits of that private test suite. This is what keeps the SQLite team able to reject external contributions, and what keeps forks from taking hold.
  - I believe a Rust re-write would have much less trouble w.r.t. the private test suite, owing to Rust's memory safety. But any fork that remains C-coded will have trouble getting public acceptance, and will have to have amazing features -or a new public test suite- to get acceptance.

- The private suite is about (among others) MCDC ie extremely stringent test coverage constraints at the binary level - what does this have to do with rust vs c?
# discuss-sqlite-server
- ## 

- ## [I'm all-in on server-side SQLite (2022) | Hacker News_202309](https://news.ycombinator.com/item?id=37613747)
- 
- 
- 

- ## [I'm all-in on server-side SQLite | Hacker News_202205](https://news.ycombinator.com/item?id=31318708)
- 
- 
- 

# discuss-sqlite-rust
- ## 

- ## [SQLite with a Fine-Toothed Comb (2016) | Hacker News_201807](https://news.ycombinator.com/item?id=17506000)
- Richard Hipp (creator of SQLite) had this to say about Rust and SQLite in the comments:
  - > Rewriting SQLite in Rust, or some other trendy “safe” language, would not help. In fact it might hurt.
  - Prof. Regehr did not find problems with SQLite. He found constructs in the SQLite source code which under a strict reading of the C standards have “undefined behaviour”, which means that the compiler can generate whatever machine code it wants without it being called a compiler bug. That’s an important finding. But as it happens, no modern compilers that we know of actually interpret any of the SQLite source code in an unexpected or harmful way. We know this, because we have tested the SQLite machine code – every single instruction – using many different compilers, on many different CPU architectures and operating systems and with many different compile-time options. So there is nothing wrong with the sqlite3.so or sqlite3.dylib or winsqlite3.dll library that is happily running on your computer. Those files contain no source code, and hence no UB.

- ## 👉🏻 Nobody is feasibly going to rewrite Sqlite in Rust.
- https://news.ycombinator.com/item?id=25464846
  - Is making a file based database that hard, compared to creating new programming language for example ?

- If you gave me two year I'm not sure I could implement a filesystem API that correctly did something as simple as "atomically append to a file". See also Dan Luu's writing on the topic of filesystems

- The problem is to write a reliable file database. 
  - Firefox got a lot of bugs related to history file corruption until it was replaced with SQLite. 
  - The same story was with Subversion where they replaced Berkeley key DB due to reliability issues.
  - This reliability comes from a very deep knowledge of OS API and all their corner cases. 
  - Creating a programming language typically involves less corner cases and the bugs in the compiler/runtime are much simple to reproduce (again, typically).
# discuss
- ## 

- ## 

- ## 🤔 [Why you should probably be using SQLite | Hacker News_202310](https://news.ycombinator.com/item?id=38036921)
- 
- 
- 

- ## 🔥 [Why SQLite succeeded as a database (2016) | Hacker News_202301](https://news.ycombinator.com/item?id=34258858)
- 
- 
- 

- ## 🔥 [Why SQLite succeeded as a database (2016) | Hacker News_202002](https://news.ycombinator.com/item?id=22367104)
- 
- 
- 

- ## 🤔 [Why isn't SQLite more commonly used for save files or for other user-facing application file formats? : programming](https://www.reddit.com/r/programming/comments/h86v81/why_isnt_sqlite_more_commonly_used_for_save_files/)
- What did SQLite gave us? SQL.
  - XML schemas are gnarly, SQL schemas are easy.
  - Primary keys are great. Foreign keys are gorgeous.
  - Constraints on columns are handy.
  - :memory: is awesome for unit-tests.
- A lot of user applications store some or all their state in sqlite, firefox being a prominent example. That is what embeddable databases are designed for. It is not frequently used as an exchange format though, because it is no designed to be a good exchange format.
- Why is it not a good exchange format? Relational tables are an excellent exchange format, and SQLItes is specifically designed to be portable across time and architectures.
  - It's only unportable if you do something like use platform serialization to store your data structures in blobs. Don't do that, or serialize them to JSON/XML/etc before putting them in a blob.

- Also most data in iPhone apps is stored in sqlite files. Rip apart an iphone backup some time and peek at the contents.
