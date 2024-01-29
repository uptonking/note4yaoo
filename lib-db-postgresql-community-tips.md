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

# discuss
- ## 

- ## 

- ## 

- ## i wonder when "PostgresLite" will become a thing
- https://twitter.com/jarredsumner/status/1751967157884432652
  - SQLite's single-file embedded no-server model makes getting started easy, but backends often need a database like Postgres
  - A reasonable alternative is to use SQLite in development and Postgres in production, but that often causes subtle issues. Some queries only work in Postgres. Some queries run very slowly in tests/development. The differences between the two is big enough to matter

- There would be a number of significant technical challenges in adapting Postgres to be single-file, embedded, no-server.
  - The biggest is probably that it currently has a 1:1 relationship between connection and processes. And requests within a request are processed serially. There has been a long standing debate about moving to multi-threaded but they always settle in staying multi-process onto.
  - Last time I scanned the mailing list it sounded like they were pretty determined to give it another go but I don't know how that developed after that.
  - Even if that got working it would almost certainly be more resource heavy than SQLite but that might be a good tradeoff for many use cases.
  - I have thought about what it would take to lift just like the SQL handling stuff, the query planner, on disk record format etc and then bolting that onto something like LMDB but I never got that far with it.

- This is why I think @deno_land created the KV abstraction. Would love to see something similar in Bun.

- Have you seen @tursodatabase ?  They created a fork of SQLite that contains a server mode and replication protocol to help you serve a SQLite database.

- ## How to use subtransactions in Postgres
- https://twitter.com/samokhvalov/status/1719228501658882268
  - TL; DR Don't use subtransactions, unless absolutely necessary.
  - A subtransaction, also known as "nested transaction", is a transaction started by instruction within the scope of an already started transaction 
- As a bottom line:
  - 1. If you can, don't use subtransactions
  - 2. Keep an eye on pgsql-hackers threads related to them and if you can, participate (help test and improve)
  - 3. If absolutely necessary, use them in lower-TPS systems only
  - avoid deep nesting

- ## [Things I hate about PostgreSQL (2020) | Hacker News_202104](https://news.ycombinator.com/item?id=26709019)
- 
- 
- 

- ## [Common mistakes in PostgreSQL | Hacker News_201905](https://news.ycombinator.com/item?id=19817531)
- 
- 
- 
