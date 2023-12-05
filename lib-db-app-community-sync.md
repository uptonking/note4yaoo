---
title: lib-db-app-community-sync
tags: [community, data-sync, database, synchronization]
created: 2023-09-17T17:35:30.868Z
modified: 2023-09-17T17:35:53.774Z
---

# lib-db-app-community-sync

# guide

- partial-sync
  - 参考sqlite+http-range的部分下载示例(sql.js-httpvfs)
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 👨🏻‍🏫 Database replication isn’t magic. there are different replication techniques at play.
- https://twitter.com/ProgressiveCod2/status/1731210162462216558
- ✅ Statement-Based Replication
  - One of the oldest replication techniques. 
  - It was used by databases like MySQL. 
  - But over the years, it has largely fallen out of favor. Why? Let's say you are going for leader-based replication and there are one or more followers under a single leader node. 
  - With Statement-based replication, two things happen: 
  - The leader logs every write request or statement that it executes 
  - It also sends that statement log to its followers 
  - This means that every INSERT, UPDATE & DELETE statement is forwarded to followers. Followers parse and execute the SQL statement as if they had received it directly from a client.
- Advantages of statement-based replication
  - Highly efficient in terms of network bandwidth. Only SQL statements are sent to the followers
  - Higher portability across database versions
- it feel out of favor because of some critical limitations:
  - Statements calling non-deterministic function (such as NOW() or UUID()) will generate different value on each replica.
  - Auto-incrementing columns need to follow same order on each replica.
  - Triggers and stored procedures can have unpredictable effects on the replica.
- ✅ Shipping the Write-Ahead Log
  - Write-ahead log or WAL is an append-only sequence of bytes containing all writes to the database. Databases create a WAL to safeguard against potential crashes. 
  - But the WAL can also be shipped to other nodes to build an exact replica of the data. 
  - However, there was one glaring(怒视；恶狠狠的注视) disadvantage. WAL describes the data at a very low level such as which particular bytes were changed on which particular disk blocks. 
  - This is dependent on the storage engine. 
  - So, if a database changes its storage format from one version to another, WAL can provide unpredictable results. This makes it hard to implement a zero-downtime upgrade with WAL.
- ✅ Row-Based Replication
  - This technique gets around the WAL issue by using different log formats for replication and storage engine.
  - A logical log is created i.e. a sequence of records showing all the writes to the database in row format.
  - This includes:
  - INSERT (new values)
  - DELETE (identification for the deleted row)
  - UPDATE (unique id and new values of modified columns)
  - Row-based replication is not tightly coupled with the storage engine and can support backward compatibility.
  - Also, leaders and followers can run different versions of the database.

- ## [Ask HN: What's the state of P2P database sync? | Hacker News_202001](https://news.ycombinator.com/item?id=21960366)
- We've created a peer to peer database at https://www.ditto.live . It runs on servers, WASM, and mobile all with a shared code base. Each row in the database is a robust CRDT that can sync deltas (or diffs) very efficiently.
- I‘ve found researching CRDTs (Conflict-free Replicated Data-Types) very enlightening. It‘s what a lot of databases use these days for multi-master replication. 

- ## [Kb: A minimalist hacker-oriented knowledge base manager | Hacker News_202009](https://news.ycombinator.com/item?id=24506280)
- For me this kind of tool needs to provide a way to sync between devices to be useful, and ideally be available on mobile. As it's using sqlite3 to store documents, it's probably not trivial to sync with something like Dropbox.
- 🤔 Why would a sqlite3 DB file not be trivial to sync with Dropbox or Syncthing? Are there platform-specific nuances to decoding or something?
  - Syncing at db-file level would create false sync conflicts when making edits while offline. You may even lose data, depending on how Dropbox/Syncthing resolve file-level conflicts. For fully automatic sync, you need to operate at the level of records.
- You may even lose data, depending on how Dropbox/Syncthing resolve file-level conflicts.
  - It's even worse - Dropbox can corrupt the database file even without conflicts - it's not safe to copy database file which is currently open in some process since it can change within the reading operation. I mean, the original file stays OK, but the copy will be likely corrupt (and in this corrupt state synced into another instance).
  - For safe copy, Dropbox would have to force some FS-level snapshotting, but that would halt all database operations. I have received few bug reports for my app which were eventually traced into attempts to sync it with Dropbox and similar services.
