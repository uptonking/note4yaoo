---
title: lib-db-postgresql-community-tips
tags: [community, devops, postgresql]
created: 2023-10-28T17:51:55.607Z
modified: 2023-10-28T17:52:17.942Z
---

# lib-db-postgresql-community-tips

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## I was today years old when I learned about the "\watch" option of psql for repeatedly running a query and examining its changing output.
- https://twitter.com/gunnarmorling/status/1693868171931914288
  - `SELECT * from foo; \watch 1`

- In PG16 you will have a count option to stop it after n runs. Even better

- ## 🔥 [Tips for a healthier Postgres database (2021) | Hacker News_202302](https://news.ycombinator.com/item?id=34734021)
- 
- 
- 

- ## 🔥 [Tips for a Healthier Postgres Database | Hacker News_202201](https://news.ycombinator.com/item?id=29858083)
- 
- 
- 

# discuss-pg-rust
- ## 

- ## 

- ## [PL/Rust 1.0: now a trusted language for Postgres | Hacker News_202304](https://news.ycombinator.com/item?id=35501065)
- why would anyone want to use PL/Rust over PL/PQSL? what is the use case?
  - > PL/Rust is a loadable procedural language that enables writing PostgreSQL functions in the Rust programming language
  - Use to write PostgreSQL functions in Rust. Also
  - > The top advantages of PL/Rust include writing natively-compiled functions to achieve the absolute best performance, access to Rust's large development ecosystem, and Rust's compile-time safety guarantees.

- A crucial facet of optimization for computational triggers in PostgreSQL pertains to the implementation of event triggers, which enable operations to be executed in bulk (per DML statement) rather than on a per-row basis. It appears that, at present, PL/Rust has not incorporated support for event triggers. According to the documentation
  - Event Triggers and DO blocks are not (yet) supported by PL/Rust.

- ## [RustgreSQL | Hacker News_201701](https://news.ycombinator.com/item?id=13354099)
- I would suggest that the author creates a clone of a "simpler" DB like SQLite or Redis. Those have, as far as I understand, good C codebases, so understanding the system should be much easier.

- 

# discuss
- ## 

- ## 

- ## [Things I hate about PostgreSQL (2020) | Hacker News_202104](https://news.ycombinator.com/item?id=26709019)
- 
- 
- 

- ## [Common mistakes in PostgreSQL | Hacker News_201905](https://news.ycombinator.com/item?id=19817531)
- 
- 
- 
