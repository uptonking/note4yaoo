---
title: lib-db-sqlite-community-sync-collab-distributed
tags: [collaboration, community, distributed, sqlite, synchronization]
created: 2023-10-26T19:02:54.110Z
modified: 2023-10-26T19:03:22.063Z
---

# lib-db-sqlite-community-sync-collab-distributed

# guide

# discuss-stars
- ## 

- ## 
# discuss-SQLSync
- ## 

- ## 

- ## 💡 [snapshot replication system_202401](https://github.com/orbitinghail/sqlsync/issues/45)
- A more efficient replication system that only tracks page indexes rather than page contents in the log. 
  - The insight is that clients only need to fast forward to the latest snapshot. 
  - This can be computed by comparing the client and server versions and unioning all page changes in-between them. 
  - Then just serve pages from the current snapshot.
  - Note, that if concurrent writes are desired in this model, this does require some kind of actual snapshot functionality on the send side. To this extent, I've been researching copy-on-write systems to understand various ways to build this in a performant way.

- ## Is SQLSync compatible with https://turso.tech/libsql ?_202401
- https://discord.com/channels/1149205110262595634/1149205111885799436/1195800771871121458
- Not currently, but I suspect it wouldn't be too hard to do. 
  - Are there other features from libsql that you'd like to use along with SQLSync?

# discuss-sqlite-sync
- ## 

- ## 🔥 [LiteSync – Easy synchronization of SQLite databases | Hacker News_202301](https://news.ycombinator.com/item?id=34265261)
- 
- 
- 

# discuss
- ## 

- ## 

- ## [Marmot: Multi-writer distributed SQLite based on NATS | Hacker News_202312](https://news.ycombinator.com/item?id=38600743)
- If you're interested in this, here are some related projects that all take slightly different approaches:
  - `LiteSync` directly competes with Marmot and supports DDL sync, but is closed source commercial (similar to SQLite EE): https://litesync.io
  - `dqlite` is Canonical's distributed SQLite that depends on c-raft and kernel-level async I/O: https://dqlite.io
  - `cr-sqlite` is a Rust-based loadable extension that adds CRDT changeset generation and reconciliation to SQLite
- Slightly related but not really (no multi writer, no C-level SQLite API or other restrictions):
  - `comdb2` : (Bloombergs multi-homed RDBMS using SQLite as the frontend)
  - `rqlite` : RDBMS with HTTP API and SQLite as the storage engine, used for replication and strong consistency (does not scale writes)
  - `litestream/LiteFS` : disaster recovery replication
  - `liteserver` : active read-only replication (predecessor of LiteSync)
- Also Expensify's Bedrock, which powers their widely-circulated "Scaling SQLite to 4M QPS" article
- Don't forget Turso's libsql which uses a local node+reconciliation
- SQLSync: collaborative offline-first wrapper around SQLite

- ## Has anyone built something like a distributed (write-back) page cache that sits above S3? 
- https://twitter.com/criccomini/status/1721918972604682362
  - Idea would be to reduce read latency and API calls? Similar to WarpStream’s mmap.
- Arguably libSQL and LiteFS are just that. The only gotcha is that you can only access the page cache with SQL
  - What if I want multiple simultaneous readers and writers?
- Write-back is a bit scary no, or maybe I'm missing something? I think those systems should be write-through (or read-through, with cache expiry)
  - Yes, write-back requires its own replication and stuff. But you get batching. I think you want write-back if the API is a KV store. If the API is just S3 compatible, I think write-through is fine. Main advantage for write-back would be batching (which you want in KV stores).
- Ah yes, I get what you're saying now. For a sophisticated implementation you do need the WAL-memtable-type thingy you're describing, or it'll be very expensive. Or, if you're lucky... your clients do most of their updates in big batches
- I'd be super interested if such a thing exists. We want to move our materialized view stores to S3 at @responsive_apps , but the write latency is prohibitive(贵得用不起（或买不起）的).
- Not sure it fits your need, but have a look at fsspec/s3fs. It has caching options that may help

- ## There are so many exciting local-first projects around SQLite 
- https://twitter.com/penberg/status/1719779549766934545
  - such as @ElectricSQL , CR-SQLite (by @tantaman ), SQLSync (by @carlsverre ), and @evoluhq , but I fear API fragmentation might be holding back adoption. 
  - As an application developer, which one do you pick and why?
- How do they handle authentication and authorization ? I can’t seem to find how access controls are done with local-first without a server being involved
  - If there isn’t a server involved it’s more of a “will send” and “will accept” type of model. A node will send a row to you if you pass its auth checks for the row. A node will accept a write from you if you pass it’s auth checks to write the row.

- RxDB used PouchDB under the hood for a while, but now there's a bunch of storage drivers to pick from. The problem for me seems to stem from trying to sync too much data at a time, and the sync chokes. I have a podcast app with thousands of episodes and 100+MB of data.
- Since RxDB v13 or so, the sync works in parallel in both directions for better performance. So maybe there should be a throttle when much data is synced.
  - [FIX Throttle calls to forkInstance on push-replication to not cause m…](https://github.com/pubkey/rxdb/pull/5194) 

- ## 🪶🔁 [dqlite: Embeddable, replicated and fault tolerant SQL engine based on Sqlite | Hacker News_202202](https://news.ycombinator.com/item?id=30135401)
- What I found to be the biggest problem with SQLite is concurrent write operations. WAL helps for concurrent read but not for concurrent write. On a moderate use case (< 20 write operations per s) I kept getting timeouts so I first devised a quick fix system using RQ jobs passing writes to a single process and migrated to postgres as fast as I could. Does this software help with concurrent write operations?
  - I have no problem with concurrent writes and wal mode on a recent build of SQLite. Perhaps you are standing up a new sqlite connection per operation or otherwise sharing between separate processes? With exclusive access using a single connection in WAL mode, I can insert tens of thousands of rows per second on flash storage no problem.
  - 💡 Something that is not widely announced is the fact that SQLite serializes all writes by default, so you should share the same connection instance as often as possible.
- SQLite does have a branch that solves the concurrent write issue - not sure if this dqlite uses it
  - [The "server-process-edition" Branch](https://sqlite.org/src/doc/754ad35c/README-server-edition.html)
  - The "server-process-edition" branch contains two modifications to stock(供应, 供给) SQLite that work together to provide concurrent read/write transactions using pessimistic page-level-locking.

- 🆚️ when would someone choose this or rqlite over something like Postgres?
  - rqlite has limitations on "safe" SQL statements. As dqlite replicates the pages and not the SQL statements over raft, which means dqlite doesn't have _that_ problem. Using random() and now() are classified as non-deterministic
- Yes, that's correct. rqlite does statement-based replication, which means it has the limitation you outlined. This could be solved by parsing the entire SQLite statement passed into rqlite before it's written to the Raft log, but I haven't got around to that yet.

- is there any similar database that allows offline replicas or delayed synchronization? I.e. allow for copies to have local offline writes and be brought up to synchronize? There is couchdb, but that seems to have fallen out of favor. I'm totally fine with having to explicitly handle collisions or prevent collisions client-side. Both dqlite and rqlite seem to use raft which requires an online quorum (I assume).
  - The SQLite built-in changeset and patchset extensions might be what you're looking for:

- Using CRDTs requires that you define all the relevant operations as monoids. A lot of work has to go into the choices of monoids to yield usable results. Monoids work fantastically well for things like upvotes on videos or whatever (so you'll notice that's always the first example given), but they don't really work for things like primary / unique keys, yet primary/unique keys are a critical requirement of most RDBMSes and schemas. Ergo, CRDTs don't work that well for relational databases. The situation is very different for collaborative text editing as there's no primary keys nor schema there, and humans are able to detect and correct nonsensical results.

- I've read about couchdb every few years, and people in the last ~5 years were complaining about an awkward query syntax, slow embedded JS engine (IIRC), client-side complexity of the document data model and effort to maintain.

- ## 🔥 [mvSQLite: Turning SQLite into a Distributed Database | Hacker News_202208](https://news.ycombinator.com/item?id=32539360)
  - [Turning SQLite into a distributed database_202208](https://su3.io/posts/mvsqlite)

- 
- 
- 

- ## 💡🔥 [Cross-Database Queries in SQLite | Hacker News_202102](https://news.ycombinator.com/item?id=26217754)
- 
- 
- 
