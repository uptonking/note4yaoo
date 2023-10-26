---
title: lib-db-sqlite-blog-xp
tags: [database, dev-xp, sqlite]
created: 2023-10-26T17:27:38.927Z
modified: 2023-10-26T17:27:56.470Z
---

# lib-db-sqlite-blog-xp

# guide

# blogs

## 📝 [3 things that surprised me while running SQLite in production_202307](https://www.joseferben.com/posts/3-things-that-surprised-me-while-running-sqlite-in-production/)

- In-memory SQLite is not too exciting
  - At least not in my JavaScript benchmarks where I compared SQLite in-memory and SQLite backed by a file.
  - Similarly, when I switched my Django tests from file to in-memory, there wasn't much of a difference.
- SQLite is surprisingly fast
  - At least compared to native JavaScript data structures. 
  - I ran some benchmarks for inserting and updating entities stored as JSON blobs. 
  - The builtin JavaScript `Map` was only 1-2 orders of magnitude faster
- SQLite feels surprisingly concurrent
  - SQLite is not truly concurrent. No matter what you do, there can only be a single writer process.

## 👥 [Things that surprised me while running SQLite in production | Hacker News_202307](https://news.ycombinator.com/item?id=36579347)

- There are massive performance gains to be had by using transactions. 
  - In other RDBMSs transactions are about atomicity/consistency. 
  - But in SQLite, transactions are about batching inserts for awesome speed gains. Use them!

- 👉🏻 SQLite is unlike other RDBMS in that **you typically do NOT want to create a new connection per logical unit of work**, because that means opening an actual file on disk each time. The more you can re-use a SQLite connection instance the better.
  - SQLite is internally handling the locking for you under most providers. Any sort of external attempts at the same will just make things go slower. The only thing that could really beat the internal SQLite mutex is to put a very high performance MPSC queue in front of your single SQLite connection and take resulting micro batches of logical requests into transactions as noted above, or some more consolidated form of representation.
# more
