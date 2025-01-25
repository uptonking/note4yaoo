---
title: lib-db-sqlite-community-limbo
tags: [community, database, limbodb, sqlite]
created: 2023-10-28T17:31:09.680Z
modified: 2024-12-13T15:12:55.861Z
---

# lib-db-sqlite-community-limbo

# guide

# discuss-stars
- ## 

- ## 

- ## [Limbo: A complete rewrite of SQLite in Rust | Lobsters _202412](https://lobste.rs/s/hl73hl/limbo_complete_rewrite_sqlite_rust)
- Deterministic Simulation Testing is a paradigm made famous by the folks at TigerBeetle

- SQLite has three test suites. Two are freely available. One, TH3, which was developed to ensure especially thorough testing, is not freely available. Supposedly, it can be licensed for some amount of money, but the libSQL authors never received a reply when they wrote asking about this.

- ## 🚀 [Limbo: A complete rewrite of SQLite in Rust | Hacker News _20241210](https://news.ycombinator.com/item?id=42378843)
- The SQLite3 business model is that SQLite3 is open source but the best test suite for it is proprietary, and they don't accept contributions to any of either. This incentivizes anyone who needs support and/or new features in SQLite3 to join the SQLite Consortium. It's a great business model 
- In case anyone else was wondering, SQLite is about 156k lines of code with 92, 000k lines of test code.

- > It uses Asynchronous I/O, considers WASM as first class, and has Deterministic Simulation Testing support from the beginning.

- author here: fully compatible at the language and file format level.
  - If you "intend to get rid of some of the baggage" you won't be fully compatible.
  - libSQL already isn't fully compatible: as soon as you add a RANDOM ROWID table, you get "malformed database schema" when using the (e.g.) sqlite3 shell to open your file (also Litestream doesn't work, etc).

- Large chunks of the test suite are open source, committed to the repo and easy to run with a `make test`.

- The standard TPC-C and TPC-H benchmarks are available online at https://www.tpc.org/tpc_documents_current_versions/current_s... They aren’t fully open source but are free to use, including use with open source software. They may be a bit on the complex side though

- One killer feature I miss from SQLite is table compression. Especially important on various embedded devices where you collect data from sensors or logs.

- ## 🌲💡 How do Turso/libSQL replicate database schema and data replication?
- https://twitter.com/penberg/status/1766031437919138218
  - The short answer is that it replicates the SQLite write-ahead log (WAL).
  - tl; dr; Turso replicates database schema and data by making copies of the write-ahead log (WAL) that stores all the changed data, which allows fast consistent snapshot reads at the replicas.
  - SQLite, which powers Turso, is a relational database management system, like Postgres or MySQL, in which the database stores data as tables that contain rows. You then model your application domain model as a set of tables to represent your data
  - In SQLite (and many other databases), a table is represented as a b-tree, which stores the rows of a table in a deterministic order using your table primary key for efficient queries. 
  - Internally, the b-tree places multiple rows in a fixed-size storage called a page.
  - So why the detour talking about relational model, b-trees and pages? Because as it turns out, that is the fundamental model of replication, pioneered by Litestream and LiteFS, that we also use in Turso/libSQL!
  - When you write to an SQLite database, the database engine appends updated pages (called frames) affected by the write the WAL. For example, if you insert a new row, SQLite creates a new page with that row and appends it to the WAL. The same applies to updates and deletions.
  - Before we get to replication, the final step to understand is that when you read from SQLite database that has a WAL, the database always checks the WAL if there are more up-to-date pages than the database itself has there and uses them.
  - There is also a checkpointing mechanism that essentially writes back the WAL to the main database file, but that's a topic for another thread.
  - In Turso/libSQL, writes always happen in a single place called the primary. If you have replicas available, writes are always delegated to the primary. This ensures that there are no conflicting updates on the WAL.
  - You might have already guessed that replication is now simply a matter of getting the primary WAL to the replicas and now SQLite actually does all the work for us. There's some tricks involved to inject WAL frames to a SQLite database file, but that's all transparent to you.
  - What this model means to an application is that you can read from your local SQLite database file, which gives you a consistent snapshot in time because the WAL also includes transaction boundaries. You are always observing the latest consistent view of your data that you have.
  - However, there always is some replication lag, depending on how far the replica is from the primary. 
  - In the @flydotio infrastructure that we use today, you're going to see replication lag in the order of 100 to 300 milliseconds if replicas are far away geographically.
  - But we have one more trick that we use. Your application can write to a replica and it will transparently delegate your write to the primary. But won't you now be subject to the replication lag?
  - The answer is: yes, but we hide that. When a replicate delegates a write to the primary, it will wait for the affected frames to replicate back before acknowledging the write to the client. This means that the replica guarantees an important property of read-your-writes.
  - When you put all of this together, Turso/libSQL gives a single URL, which gives an illusion of a single database to applications, although the data can be replicated in many different locations for lower access latency.
  - Finally, one source of confusion folks have is around how schema is replicated. The answer is surprisingly simple: it happens through the WAL. That's because schema is represented as internal table in SQLite, which gets stored in the WAL all the same.

- Does the client decide where to issue queries to? Or is it via done middle-aged which decides primary or replica?
  - We use @flydotio ’s infrastructure to route queries to the nearest replica server.

- Does D1 by @CloudflareDev use the same technique? What’s the difference with Google Spanner? (ignoring spanner sharding).
  - I unfortunately don't know how D1 works internally because there doesn't seem to be public information about that.
  - Spanner layers relational model on top of key-value store like I think CockroachDB and YugaByte do. So the technique is different because I think they're replicating the data, not the changes like WAL does. But I am not an expert on those systems so don't take me too seriously.

- 
- 
- 

- [libSQL: Diving Into a Database Engineering Epic _202307](https://compileralchemy.substack.com/p/libsql-diving-into-a-database-engineering)
# discuss-author
- ## 

- ## 

- ## 

- ## What is the compatibility plan in Limbo with SQLite?
- https://x.com/penberg/status/1879430213337018423
  - Long term plan is that Limbo is drop-in replacement for SQLite. Of course, "drop-in" is always bit of a lie because only the original is 100% compatible (although sometimes incompatible with previous versions of itself) and you can only realistically get to 99% or whatever. But at the end of the day, when you reach an acceptable level of compatibility, it makes no practical difference to developers.
  - We will of course add opt-in features that SQLite does not have. For example, we will have built-in vector search, which is unlikely to ever be part of SQLite. We will also work towards features that SQLite might have, but does not have yet, like `BEGIN CONCURRENT` , which lifts single-writer limitation in SQLite.

- Are triggers and webhooks in the plans?
  - Triggers yes. Webhooks -- do you mean like they have in SQLite Cloud?

- just curious, is "loadable sqlite extensions" support planned for limbo? Would love to help contribute/test if so!
  - Yes it in scope and some plumbing already exists for it. Hop on to our Discord (link in readme badge) if you want to hack on it!

- ## I was exploring ways to make SQLite async and picked Zig initially because I thought I could just reuse large chunks of SQLite by re-writing just the VDBE. 
- https://x.com/penberg/status/1869426876797624350
  - The more I kept digging into it, the less convinced I became of keeping any of SQLite because (1) the front-end is a bit hairy to be honest and (2) async eventually bubbles up to most layers.
  - As I figured I'd be rewriting the whole thing, Zig was just slowing me down as I was learning the language, while trying to figure out how to build everything. I also ended up sending much more time in `gdb` than usual and I never really understood why people love comptime. People tell me this is a skill issue, and they're probably right.
  - Anyway, I then simplified the problem to just rewriting SQLite and went with Rust, which I already knew well, and which I think is an excellent fit for systems programming.

- ## It's indeed true that there is this misconception that the SQL over HTTP support Turso has is the only mode, which is not true. 
- https://x.com/penberg/status/1842964199284036091
  - The feature called "embedded replicas" gives you all the benefits of in-process SQLite  for reads, and we're currently working towards offline writes, which gives the same benefit for writes too. 
  - The HTTP mode is there to unlock environments such as Cloudflare Workers and Vercel, where it is not practical to bring over the whole database query engine over to the app.

- 🆚️ what benefits are there with Turso over just plain SQLite!
- For starters, how do you @liltechnomancer deal with backing up your database file? 
  - Do you, for example, use Litestream for that? Or do you have something custom. 
  - This is one of the most important basic quality of life things Turso brings to the table: point in time recovery for your databases, which is pretty cool.
- Another thing people use Turso for is replication. 
  - This is actually something SQLite does not really support. There's a project called LiteFS that does this by implementing a special-purpose filesystem in userspace, that monitors writeahead log (WAL) updates and replicates them to the server. 
  - We took a different route: we actually forked SQlite to add a "virtual WAL" interface that we can use to do similar style replication.
- Litestream is great! We used in the early days of Turso before we had our own point in time restore wired up.

- ## SQLite’s read and write paths are slower than they need to be because SQLite supports multiple processes accessing the same database file concurrently.
- https://x.com/penberg/status/1819779262511018068
  - Because of the work on Limbo, the SQLite compatible in-process OLTP database, I have been digging into the SQLite read and write paths. And they're much more slower than you’d think by design.
  - SQLite supports reads and writes from multiple concurrent processes. Every read transaction has to take a POSIX advisory lock on the database file (kernel-crossing overhead) to make sure reads are consistent and to coordinate with writers.
  - This means that read transactions take a microsecond or so whereas with pure in-process (like in Limbo) you can get to hundred nanoseconds.
  - Writes has similar problems too. To support multiple processes writing to the WAL, every write transaction has to take a a lock to get exclusive access to the WAL. The lock uses shared memory via `mmap` , but checkpointing takes the same exclusive lock blocking all writers for the duration of the checkpoint operation, which can take a while.
  - 🤔 tl; dr; once you stop supporting multiple processes writing to the same database file, you can make things much faster, which is the path we’re taking for Limbo.

- How would locking work then, given that other processes can in fact access the file? Would it silently corrupt? Would you keep a lock the entire life of the process?
  - We lock for the lifetime of the process.
- What’s the timeline on removing the process lock? Do you have benchmarks that show the results? Very interested in this.
  - You can get 2x read performance out of SQLite if you use "pragma locking_mode=EXCLUSIVE". It still leaves some performance on the table, not sure why yet.
- The problem of allowing more than one process to access the DB is that you cannot cache things in RAM: the file becomes the channel through which different processes communicate.
  - For instance, ‘single process + multiple threads’ is the trade off taken by @duckdb . RAM caching is even more relevant for OLAP as the files tend to be much larger than SQLite files.
- How does that compare to SQLite's exclusive locking mode that locks for the lifetime of the process?
  - Essentially the same
  - Good to know. We enabled it for most of Firefox's SQLite databases many many moons ago and saw a decent perf boost from it. Entirely possible things have changed since we last measured it though.

- does this mean only one instance of a REST API would be able to interact with a Limbo DB? As in, in a Kubernetes instance with 2 pods, only one would be able access it because they’re each a different process?
  - Yes, right now that's exactly how it would work. For shared databases, you probably want storage disaggregation (a separate "page server" process), which should be more efficient too. (That's one reason why I/O in Limbo is async.)
  - If there is a page server process, then access does not even have to be exclusive. You can have data cached in your client memory space, but also shared between multiple clients. At least that’s the theory, did not build it yet 

- Multi-process is always going to be slower than multi-threaded, which SQLite already supports. And if you switch to exclusive file locking, you can get something like 0.5 million reads per second on a single core. If your traffic is heavier than that, you probably want sharding.

- What are the pros/cons of synchronizing via:
  1. lock on some mutex in a MAP_SHARED mmap region
  2. using an external flock
  3. using a posix semaphore
  - Any idea why sqlite synchronizes reads via flock (2) but writes via shared lock (1)?
- Shared memory is faster because it does not require a kernel crossing. Of course, using a POSIX mutex means that you enter the kernel on contention, but still better. Don’t know the reason for different schemes, likely historical
- If shared memory lock is faster, then doesn't synchronizing reads via flocking make no sense?
  - Yeah, so I don't know why SQLite is so heavy on the advisory lock by default. Maybe just historical.
# discuss-news
- ## 

- ## 

- ## 

- ## limbo, Today we have decided to make @penberg 's experimental project, an official Turso project _20241210
- https://x.com/glcst/status/1866508345731088759
- Will you keep the same code of ethics as SQLite though?
  - NO
- Does libSQL already have a build feature to enable Limbo?
  - There's no build feature, and at this point limbo was kept entirely separate, even on Pekka's github, instead of Turso's. I was really just him working on it for fun. It went very well and we decided to promote it.
  - The long term plan depends on what happens next. It is still very experimental and non-committal from my PoV.
-  the plan is towards full compatibility for modern SQLite features. For example, no plans to do journal mode, we're all in the WAL mode, and hoping to later move towards WAL2 or even something that could do `BEGIN CONCURRENT` .
- will your first step be to add experimental limbo support in libSQL through an optional build feature? This looks like the best way to put it in the hands of people already using libSQL
  - Yes, indeed. But I think there's still bit more work to do on Limbo for this to be useful.
- SQLite supports data change notifications, but doing so requires bindings that are not available in most wrappers, libraries, etc.
  - I'm very interested in finding a way to make this happen because SQLite can be used virtually everywhere. That also means I want to make sure that whatever method I use to enable this, would also have to work in environments a user may want to use.
- Don’t fall into the trap of adding every feature people ask for. The reason SQLite is popular is because it’s SMALL. If you want this to succeed, you need to say NO to a lot of requests

- because of io_uring will this be linux only for now? forever?
  - Not Linux only. Limbo also supports traditional syscall I/O and runs on macOS fine. Don’t know the state of Windows port but ran there fine too at some point.

- Do y’all plan to pay for the commercial SQLite test suite?
  - We tried to pay for it when we forked libSQL but never heard back… I think doubling down on DST but also the open test suite (Limbo has the same TCL tester) is the way to go!

- ## Limbo is now self-hosting! You can create and access databases from Limbo, with file format compatibility with SQLite _202411
- https://x.com/penberg/status/1858496941417484757
  - There's also now a "limbo-wasm" package with Limbo core compiled into Wasm and I/O using Node's filesystem APIs.
- Do I correctly understand that you're rebuilding SQLite in pure Rust?
  - Yes, with two architectural changes: (1) I/O is asynchronous and (2) the core is built for deterministic simulation testing.

- ## In Limbo, I am implementing the SQLite C API with Rust. 
- https://x.com/penberg/status/1857406118277836856
  - Right now I have the whole of SQLite API in a single file (https://buff.ly/3URtylE ) and like to split it up. But I seem to be unable to convince cbindgen to pick up symbols from other files. What am I doing wrong?
- rust is so comfy. cargo, cargo-watch, rust-analyzer, arbtest, closures, multi-line comments, clippy... compiler warnings...

- ## SQLite and MySQL are quite different, and it won't work for all of you.
- https://twitter.com/glcst/status/1765852342627246402
- I’ve never used SQLite. What are the differences or situations where a migration from MySQL doesn’t make sense?
  - sqlite is a way simpler database. Technically, it suffers with write heavy workloads. (Think more than 1k writes per second) Aside from that, it is mostly around whether you adapt well to its simplicity.
- Does this 1k write/s also apply if I have multiple databases?
  - that is per database.

- Can I use update with returning but get the value of a row before the update, not after?
  - Everything in Turso is transactional, so if you do a select for the value right after in a batch, you should get the value of the row before the update.

- ## Our goal with libSQL is to make SQLite production ready. _202402
- https://twitter.com/glcst/status/1760030875494813928
  - We started with replication, and are now adding encryption-at-rest. 
  - SQLite doesn't have encryption at rest as an Open Source feature, meaning you have to rely on your own infrastructure to do it.
  - Today, we are adding encryption-at-rest natively to libSQL. It is fully OSS, and all you have to is to add a key parameter to the constructor. This works for local files, and you don't even have to be a Turso user for that. 

- I think its inevitable that we have to move to everything encrypted at rest and everything encrypted in transit.

- We rely on SQLite internally in a rather extreme way: every program is in itself an SQLite file that holds the entire JavaScript heap, among other things. We should definitely write a Turso connector though, I think it would be super useful to our users. Added to our roadmap.
# discuss
- ## 

- ## 

- ## 

- ## If you'd rather watch @ThePrimeagen break down @penberg 's Limbo rewrite of SQLite in Rust than read the article - and I recommend it (way more entertaining) - here's the vid
- https://x.com/tursodatabase/status/1869412566054977555

- ## Working on Limbo is not just about catching up with SQLite, sometimes you get to improve on it. 
- https://x.com/penberg/status/1869718985018847694
  - For example, SQLite's API only supports cancelling all queries, but with async it's important to support per query cancellation. So we added that to Limbo!

- A feature that I am looking for _right now_ in sqlite is per-connection malloc/free control. You can configure it at the process level, but I want to create arenas per connection.

- Do you think using Rust's unsafe is inevitable for a database like this? I noticed there are some unsafe uses in the repo for sqlite3.
  - I don’t know if it’s inevitable, but useful at least. Unsafe just makes sense in some cases

- ## running a database in production is much more than just doing reads and writes.
- https://twitter.com/glcst/status/1759670019443577324
- libSQL needs a PostgREST/supabase equivalent. Major value unlocks when a single Javascript developer can build a whole application without worrying about servers.

1) Some form of support for nosql document storage on top of turso.
2) Something around search indexes 
3) Pricing remains serverless but dedicated vms become an option.

- Migrations? Something like this? Does Turso perform vacuum on SQLite automatically?

- Queue net triggers

- Some kind of eventual consistency multi-master

- ## 🪶 SQLite takes multitenancy to the next level. 
- https://twitter.com/sarna_dev/status/1735673953396338999
  - Just tested @tursodatabase 's libsql-server hosting 100k databases, querying them all in a loop. It used 1.6GiB of RAM.
- Are you going to have managed schema updates too then? :) Or will we have to manage 100k partial updates (due to some of them failing) manually?
  - The scenario tested here is "database per user", so there's no common schema to coordinate - each user can store whatever they wish in the db
- 💡 Coordinating schema changes is indeed something I would love to do and we have some ideas how to do that. No ETA for that yet though
  - (1) leverage SQLite ATTACH and have a template database storing the schema (suggested by @sarna_dev ) 
  - (2) record the schema delta history and apply it incrementally to the individual databases.

- 🤔 How does one handle high availability when the database is SQLite? That's fairly impressive, but I wonder how easy it would be to auto-manage for customers with backup/restore, database upgrades and rollbacks, etc. What protocol is used over the wire to talk to the database?
  - Turso speaks over HTTP or websockets, 
  - as for availability, we have replicas and regular backups for disaster recovery
- Do I currently understand that libSQL can do regular file-based SQLite where the application directly loads the database file, but can then be adapted to use the same SQLite database file through your server and one of the above wire protocols, giving the best of both worlds?
  - Yessir, our drivers generally let you pick if you want to use a local file or a remote connection, and the app code stays the same
  - 👆🏻 pouchdb也这样

- ## What cipher do folks expect from encryption at rest in SQLite? 
- https://twitter.com/penberg/status/1745747106285985889
  - @sarna_dev is integrating SQLite3MultipleCiphers into libSQL and there's many to choose from. 
  - We now have enabled AES-256 in CFB mode, but I see the proprietary SQLite extension uses AES-256 in OFB mode with HMAC
- Pluggable ciphers

- ## 🔀 Here's the same ergonomic libSQL fast local reads with transparent remote writes in JavaScript. 
- https://twitter.com/penberg/status/1737459047392006517
  - You write your application like you'd be using a local database, but get your writes delegate to a remote server (where they're durable and replicated).
- how do you resolve write conflicts in turso? Or do you try to avoid them altogether?
  - There’s always a single writer at a primary server so no conflicts
  - Writes are not async in the model we have. 
  - They're always going to one and same primary server, which means there are no concurrent updates that would happen during a network partition.

- ## Browser -- do you mean database server? libSQL in WAL mode compiles to #Wasm now. Lots of amazing stuff coming soon
- https://twitter.com/sarna_dev/status/1729404441495814244
  - and here it is: WAL in a browser
- what's the point of a "virtual" WAL? A write ahead log is only useful if its persisted. Or does this PR allow the user to save the WAL file wherever?
  - "virtual" as in SQLite's "virtual file system", so you can bring your own implementation and persist the WAL frames however you wish. @tursodatabase 's replication and embedded replica layers are built upon virtual WAL

- what storage engine in the browser? is this on opfs?
  - In-memory by default, but it also supports OPFS

- the log is the database.  sqlite-wasm 支持 WAL 后，应该可以做流式数据备份了。官方的 sqlite-wasm 还不支持 WAL

- ## I used to think forking sqlite (e.g., @libsqlhq ) was crazy but I'm on board now. 
- https://twitter.com/tantaman/status/1684917032096030722
  - While SQLite is great, I just don't think it is ready for the demands of the coming years.
- What do you mean specifically? The weak update hook?
  1. weak update hook / subscriptions 
  2. lack of write concurrency 
  3. lack of pluggable storage engines (eg custom btree rather than vfs or vtab)
  4. limited types
  5. lack of tiered storage
  - Now abandoned SQLite 4 had fixed 3, SQLite hc-tree might fix 2

- Agree about update hook. BEGIN CONCURRENT is not enough write concurrency? I guess not if you want update hook anyway I wonder how long until libsql has a rocksdb backend
- Notion is using SQLite on mobile, correct? How do you guys deal with reacting to mutations?
  - `sqlite3_update_hook` works for us

- Yeah let’s do it and add cell-level reactivity while we are at it.

- ## Folks, if somebody is interested in contributing to libSQL but finds the main code base too complex for their first contribution, we're kickstarting a new shell, written from scratch in Rust: _20230314
- https://discord.com/channels/1026540227218640906/1026540227218640909/1085099589633331221
  - https://github.com/libsql/libsql/tree/main/src/rust/libsql-shell .
  - It still has lots of missing features and our goal is that it's 100% compatible with the original shell (and beyond).

- ## 🚀🔥 [LibSQL is an open source, open contribution fork of SQLite | Hacker News_202210](https://news.ycombinator.com/item?id=33099222)
- This fork has exactly zero new code, but they already managed to change the license and the code of conduct. Their plans include io_uring, Rust and WASM functions - the first two negate the "single-.c-and-.h multi-platform" paradigm that made SQLite what it is, the third thing seems like a feature very few people would care about. They also want to make SQLite distributed for some reason (uh, just use Postgres?)

- 
- 
- 
