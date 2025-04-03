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

- ## Figured out a new recipe for tracking SQLite table history using a JSON audit log and a somewhat terrifying set of nested `json_patch()` SQL functions
- https://twitter.com/simonw/status/1762296697886257267
- Is this to make a crdt table?
  - No, just an audit log - would be interesting if you could use it for full CRDTs though
- This is essentially how the CRDT based sync in @ElectricSQL works in the client SQLite. Triggers record all changes in a oplog table as JSON. These are then synced to/from Postgres over a websocket. We have rules that apply LWW and compensations to maintain referential integrity.
- Am using a similar approach in postgres. Except a function to update json columns rather than a trigger. And implemented in JavaScript (postgres `plv8` extension).

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

# discuss-cdc-sqlite
- ## 

- ## 🤔🆚️ [Tracking SQLite Database Changes in Git | Hacker News _202311](https://news.ycombinator.com/item?id=38110286)
- This approach works by storing the actual SQLite binary files in Git and then using a custom "diff" configuration to dump each file as SQL and compare the result.
  - It's a neat trick, but storing binary files like that in Git isn't as space efficient as using a plain text format.
  - I built my own tooling to solve this problem: https://datasette.io/tools/sqlite-diffable - which outputs a “diffable” copy of the data in a SQLite database, precisely so you can store it in Git and look at the differences later.

- But it's not really a diff no the database itself, just a diff of a full dump that you can use to rebuild the db, but not change an existing one. For example when you do a DELETE the diff does instead have an INSERT less in the dump, which is not exactly a database diff. Depending on the use case that might still be ok.

- 🧩 does no one know about _A tables anymore? This has been a solved thing since the 1970s
  - sometimes called audit or journal tables.
  - Every time something is updated or deleted, the entire previous record is inserted into its corresponding _A table with who did it and when (and optionally for what transaction number)
  - so delete from foo results in an insert into foo_A before the delete occurs.

- I was also exploring something like this a few years back but for Office files. This exact approach seemed like an absolute win to me, but I ended up not using it, because this won't work in the GitHub web UI. This won't be a deal-breaker to many, but people should be aware of it still. In the end I ended up doing this: https://github.com/TomasHubelbauer/modern-office-git-diff/

- is similar approach possible for postgres and MySQL?
  - Not for this technique, because this relies on the fact that SQLite databases are a single file that can be checked into Git.
  - MySQL and PostgreSQL use a whole directory full of files. You could try storing that whole thing in Git and then tiring a custom diff command that can load those directories into a temporary database sever and dump out SQL for comparison, but it would be very slow and brittle if you could even get it to work at all.
  - Instead, a better strategy would be to dump your MySQL or PostgreSQL database to plain SQL and store that in your Git repo. Or use the trick in using here for my PostgreSQL database

- ## [SQLite triggers to track table changes | Hacker News _202410](https://news.ycombinator.com/item?id=41741752)
- Cool solution. I might use it on a small multi tenant web app to generate audit logs.

# discuss
- ## 

- ## 

- ## 🚀 [Stop syncing everything by Graft _202503](https://sqlsync.dev/posts/stop-syncing-everything/)
- Partial replication sounds easy—just sync the data your app needs, right? 
  - But choosing an approach is tricky: logical replication precisely tracks every change, complicating strong consistency, while physical replication avoids that complexity but requires syncing every change, even discarded ones. 
  - What if your app could combine the simplicity of physical replication with the efficiency of logical replication? 
  - That’s the key idea behind Graft, the open-source transactional storage engine I’m launching today.
  - It’s designed specifically for lazy, partial replication with strong consistency, horizontal scalability, and object storage durability.
  - I first discovered the need for Graft while building SQLSync. 

- ## SQLite is not single connection. Even upstream supports multiple processes reading and writing to the same database
- https://x.com/penberg/status/1850522929928311134
- PGLite only supports a single connection. But it provides a way to multiplex queries from multiple clients

- Perhaps he means single writer multiple reader, even though it supports multiple connections.
  - Yes it supports multiple connections but they are queued when they write so that only one had access to the database at a time
- Sure, but I think what you're saying about "single connection" is confusing and not true because the single writer limitation is orthogonal to that. You can have as many connections as you want. Reads are concurrent, writes are not (but there's BEGIN CONCURRENT hopefully some time in the future to lift that limitation).
  - Agree that "single connection" was poorly worded. What matters for concurrency are transactions. While read-only tx can operate concurrently, the read operation itself may not: a read within a tx that writes later can be canceled if there is any concurrent write

- And if you want a distributed DB, powered by SQLite, with read replicas use this: https://github.com/bloomberg/comdb2
  - Sqlite VM SQL engine

- We are using WAL mode with Litestream for backup and it's working well. We have . Net 8.0 API which pulls data from multiple systems e.g CSV, Sql Server and then use Sqlite to keep that data and then it's used by 3rd parties via REST Api.

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

- ## 🔥 mvSQLite: [Turning SQLite into a Distributed Database | Hacker News_202208](https://news.ycombinator.com/item?id=32539360)
  - [Turning SQLite into a distributed database_202208](https://su3.io/posts/mvsqlite)

- This is exactly what the engineers behind FoundationDB (FDB) wanted when they open sourced. 
  - For those who don't know, FDB provides a transactional (and distributed) ordered key-value store with a somewhat simple but very powerful API.
  - Their vision was to build the hardest parts of building a database, such as transactions, fault-tolerance, high-availability, elastic scaling, etc. 
  - This would free users to build higher-level (Layers) APIs/libraries on top.

- This project (mvSQLite) appears to have found a way around the 5s transaction limit as well as the size, so that's really promising. 
- A simple workaround is to store “bulk data” in an external system like blob storage and reference that from the DB.

- 🆚️ What makes this special compared to rqlite or dqlite?
  - rqlite author here.rqlite doesn't implement its own consensus system either. It uses the same Raft consensus code that powers Hashicorp Consul. I don't see how this is any different, in principle, than using Foundation DB's consensus system.
- rqlite's readme seems to indicate that it uses Consul only for service discovery, and runs Raft internally?
  - I think the most important difference here is rqlite runs its "data plane" on a single consensus group/state machine while mvsqlite relies on FDB's distributed transaction system (well at the bottom there's a Paxos but it is only used for metadata coordination). Both approaches have advantages and disadvantages though.
- Correct. What I meant by the reference to Consul is that rqlite uses the Raft implementation at its center and repurposes for use by rqlite. I can make that clearer.
- IIRC rqlite replicates commands, dqlite replicates WAL frames, mvsqlite intercepts file system calls because it's a VFS implementation.

- ## mvSQLite: [Show HN: Distributed SQLite on FoundationDB | Hacker News_202207](https://news.ycombinator.com/item?id=32269287)

- ## 💡🔥 [Cross-Database Queries in SQLite | Hacker News_202102](https://news.ycombinator.com/item?id=26217754)
- 
- 
- 
