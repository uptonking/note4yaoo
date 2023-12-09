---
title: lib-db-sqlite-blog-vendors
tags: [sqlite, vendors]
created: 2023-03-01T18:36:34.115Z
modified: 2023-10-26T18:14:17.038Z
---

# lib-db-sqlite-blog-vendors

# guide

# blogs

# blogs-sqlite-powered

## 📝 [SQLSync - Stop building databases_202312](https://sqlsync.dev/posts/stop-building-databases/)

- There comes a time in every frontend engineer’s life where we realize we need to cache data from an API. 
  - storing a previous page of data for that instant back button experience, implementing a bit of undo logic, or merging some state from different API requests
- More feature requests show up, and soon we’re busy implementing data caches, manual indexes, optimistic mutations, and recursive cache invalidation.
- These features bear a remarkable resemblance to the inner workings of databases. Indeed, in any frontend application of sufficient complexity, engineers will necessarily end up building so many data management features that they are essentially creating a domain specific database. 
- Our journey starts in the most humble of ways. Send an API request to the server and store it in a local variable. 
  - The goal of using Redux (or similar) in this way is to centralize cache logic, coordinate refresh, and most importantly share cache results between components.
- One optimization we can leverage in the frontend is to store data cached from the server in an object keyed by ID.
- Recursive Cache invalidation
- SQLSync is a frontend optimized database stack built on top of SQLite with a synchronization engine powered by ideas from Git and distributed systems.
  - SQLSync provides a durable cache, the full power of SQLite (indexes, constraints, triggers, query optimization), optimistic mutations, smart cache invalidation, and reactive queries.
- SQLSync provides optimistic mutations out of the box
  - It does this by handling mutations in a reducer, similar to how Redux works.
  - Using this reducer, SQLSync can execute mutations optimistically on the client, and then run them in a globally consistent order on the server.
  - Finally, the client performs an operation similar to a Git Rebase to synchronize the client with the server.
- One advantage of SQLSync’s architecture is that it eliminates the need for recursive cache invalidation. By writing all the data mutation logic within a reducer that can be easily shared on both the client and the server, all changes made during a mutation are automatically visible. 
  - Even better, due to synchronization working like “Git Rebase”, this approach allows the server to make different changes than what happened on the client - with the guarantee that the client will always reach the same consistent outcome. This is a powerful capability that eliminates the need for developers to spend mental bandwidth on data micromanagement.

## [Announcing D1: our first SQL database_202211](https://blog.cloudflare.com/introducing-d1/)

- Meet D1, the database designed for Cloudflare Workers
- D1 is built on SQLite.
