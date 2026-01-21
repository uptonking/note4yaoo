---
title: lib-db-sqlite-community-turso
tags: [community, database, sqlite, turso]
created: 2023-10-28T17:31:09.680Z
modified: 2026-01-03T08:33:17.870Z
---

# lib-db-sqlite-community-turso

# guide

# usage
- All SQL commands must end with a semicolon (; ).

```shell
# start example db
target/debug/limbo database.db

# Show the current values of settings
.show

# To open a database file at path './employees.db'
.open employees.db

# To list all table
.tables

# To import csv file 'sample.csv' into 'csv_table' table
.import --csv sample.csv csv_table

# To display the database contents as SQL
.dump

# To load an extension library:
.load /target/debug/liblimbo_regexp

# To show names of indexes:
.indexes ?TABLE?

```

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

- ## how many features you drop during the rewrite?
- https://x.com/penberg/status/1906001453338030104
- For the SQLite rewrite? Nothing except for some features SQLite itself has deprecated. 

- I have written a JVM (that nobody used), QEMU replacement (before Firecracker). Was part of OSv unikernel and Scylla early teams.

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
# discuss-internals
- ## 

- ## 

- ## 

- ## 👎🏻 现在并没有提供冲突解决的方案，有点半成品的感觉。而且turso 不支持 udf 和 load extension, 改了半天勉强能跑起来，有些失望。
- https://x.com/mayneyao/status/1907287654368219589

- ## How does @tursodatabase diskless architecture work?
- https://x.com/penberg/status/1903381080410861708
  - In the new diskless architecture, WAL writes are synchronous to S3, which means the WAL file is fragmented into lots of small objects. We do this to guarantee durability while allowing fast failover (another compute node can just pick up the work if one machine dies).
  - But the database file itself is also broken into parts -- we call them database file segments to distinguish between the WAL fragments. These are 128 KB blocks right now. This allows us to lazily load even larger database files to the compute node for caching on local disk.
  - The millisecond granularity across different plans comes from us essentially batching WAL writes (we actually have not rolled this into production yet) to essentially keep things cost-effective (S3 PUTs are pretty expensive).
  - Basically, the whole architecture is built around latency vs cost trade-off so that the free tier has higher latency (but is cost-efficient to operate), but for paid tiers, the higher the tier, the lower the latency (because you essentially get more CPU, memory, and disk).

- Do you also write the WAL logs straight to S3? If yes won’t that be  major latency bottleneck? If not how do you guarantee durability in these cases if the nodes are diskless?
  - We write straight to S3 Express, which is bit slower than EBS `fsync()` latency, but not much

- how does the orchestration of all this work? like each db (or group) get's it's own container?
  - We host multiple databases per container to multiplex resources. We ended up building it all the multitenancy in our server, but an alternative might have been @UnikraftSDK -based solution
- so there's a daemon process always active in the container and does the thing to the right container based on the incoming request?
  - Yup, exactly

- What is the latency? And how about if s3 also does the throttling?

- Does each replica maintain its own WAL in S3 ? How do you enforce consistency around replicas
# discuss-agentfs
- draft
  - 针对只读场景，文件到sqlite的同步，是否可以迁移到个人生产数据库到sqlite的同步

- ## 

- ## 

- ## 

- ## 

- ## How does AgentFS fit into the AI agent sandbox stack?
- https://x.com/penberg/status/2013658322038067280
  - The sandbox infrastructure typically uses Firecracker or a similar VM for the agent compute. The integration with AgentFS is straightforward:
  - 1. AgentFS daemon runs on the host, speaking NFS. The VMs connect directly to it for filesystem access, but the guest kernel caches metadata and data locally. This amortizes access costs against a locally running NFS server.
  - 2. On the backend, the AgentFS daemon communicates with Turso Cloud to lazily pull and push SQLite database fragments from S3, which contain your entire agent filesystem. This allows the agent to start working instantly wherever the compute is.
  - That's it, that's the integration. And now you have the benefits of AgentFS, such as snapshotting, resumability, and auditability, as part of the agent sandbox infrastructure.

- The VM gives you isolation for compute, and AgentFS is the safe hands around the filesystem.

- the whole agent in a sandbox thing doesn’t quite make sense to me for some reason. i’d really love to see someone do a whole write up on the tradeoffs around that design and whether it makes sense from first principles or is just a fad caused by claude code being a CLI

- won't the reads and writes go brr when a user does a large copy with a bunch of tiny files and increase the cost for turso cloud?

- ## 🆚🤼 digesting the current “filesystem vs database” debate for agent memory:
- https://x.com/helloiamleonie/status/2013256958535401503
  - currently I'm seeing 2 camps in how we build agent memory.
  - on the one side, we have the “file interfaces are all you need” camp.
  - on the other side, we have the “filesystems are just bad databases” camp.
- 📌 "file interfaces are all you need" camp
  - leaders like anthropic, letta, langchain & llamaindex are leaning towards file interfaces because “files are surprisingly effective as agent memory”.
  - • anthropic’s memory tool treats memory as a set of files (the storage implementation is left up to the developer)
  - • langsmith's agent builder also represents memory in as a set of files (the data is stored in a DB and files are exposed to the agent as a filesystem)
  - • letta that simple filesystem tools like grep and ls outperformed specialized memory or retrieval tools in their benchmarks
  - • llamaindex argues that for many use cases a well-organized filesystem with semantic search might be all you need
- agents are good at using filesystems because models are optimized for coding tasks (including. CLI operations) post-training.
  - that’s why we’re seeing a “virtual filesystem” pattern where the agent interface and the storage implementation are decoupled.
- 📌 "filesystems are just bad databases" camp
  - but then you have voices like dax from opencode who rightly points out that “a filesystem is just the worst kind of database”.
  - swyx and colleagues in the database space warn about accidentally reinventing dbs by solving the agent memory problem. Avoid writing worse versions of: • search indexes, • transaction logs, • locking mechanisms
  - logseq
- trade-offs
- simplicity vs scale
  - > files are simple and CLI tools can even outperform specialized retrieval tools.
  - > but these CLI tools don’t scale well & can become a bottleneck.
- querying and aggregations
  - > grep can be effective and a hard baseline to beat.
  - > and if you want to improve retrieval performance with hybrid or semantic search?
  - > luckily, there are CLI tools available for semantic search.
  - > the question remains: how well they scale & how effective agents are at using them when they are not as common in the training data.
  - > also at some point you might want some aggregations as well.
- plain text vs complex data
  - > file interfaces and native CLI tools are great for plain-text files.
  - > what happens when memory becomes multimodal?
- concurrency
  - > if you have a single agent accessing one memory file sequentially, no need to think about this.
  - > if you have a multi-agent system, you want a DB before implementing buggy lock mechanisms.
- we’re just scratching the surface: security concerns, permission management, schema validation, etc. are more arguments for dbs over filesystems.

- the database is a good place for the artifacts that the agent generates and will consume itself.
  - The filesystem is a good abstraction to get data to and from tools.
  - The main "disadvantage" of the database is the access latency. But SQLite solves that - and can be used as a filesystem as well!!!

- cursor also mentioned that they use files for memory.

- Last we made that filesystem is all you need decision, we ended with the obscure tiers of metadata chaining that is still a nuisance (aka hive iceberg deltalake etc)

- LLMs have the same information needs as humans - humans use file systems and databases and all other systems - why LLMs should have only one true tool?
  - It's very similar to the camera vs lidar argument for self driving cars.

- Perhaps an embeddable dB to satisfy both camps
  - A grep-like text DSL on Sqlite might just be all you need. 

- why can't we just do a perfect blend of both
- maybe filesystem can kind of be like a cache with more recently used stuff being stored there vs more persistent storage in DB? seems like the best of both worlds

- Once we reached hundreds of running agents, we moved everything to object storage and gave each agent its own SQLite database.

- Decide by guarantees: need ACID/joins or fast metadata queries → Postgres/SQLite; need blobs, versioning, audit trails → keep files.

- Both camps are right depending on the failure mode. Files are great for inspectability and cheap iteration, DBs win when you need guarantees: schema, dedupe, TTL, audit trail. “Memory” isn’t storage, it’s the rules for what gets written and what gets trusted later.

- Call me simple but I think the main reason why file system is sufficient right now is because agent is pretty much still in “single player” mode. They don’t really care about any other agents memory except themselves, so they don’t have problems that database help solve like indexing or concurrency.

- Why not both? Am from the filesystem camp. We do use an rebuildable index on top, that covers the multi-modal aspect. With new stuff like LEANN(worth taking a look at) the index/DB can be stored in a compressed format used for the search, build permissions, schema etc there.

- I used a database that held the files as text and vectors related to them…. I think this is a very fine distinction. Also under the hood file systems in operating systems are databases in a way. Just with a database of metadata.

- Fascinating debate, filesystems win simplicity, but dbs scale for concurrency/multimodal. In physical AI (human-robot teams), memory needs relational layers (shared patterns over time), hybrid approach (virtual FS + db backend) could handle trust-critical HRI best. Great breakdown

- Files are more resilient in case of random shutdowns out of memory exceptions and corruption. With a database one bit is flipped and you are done

- ## File-based agent memory: great demo, good luck in prod 
- https://x.com/nicoloboschi/status/2012119323481940119
  - TL; DR: The "file is all you need" movement benchmarks well because benchmarks are small. In production, you'll hit context rot, multi-hop limitations, and temporal query problems. Files are a necessary foundation - but the claim they're sufficient is marketing. (Full disclosure: I sell the opposite, so I'm biased too.
- There's a growing consensus in the agent community: files are the universal abstraction. Store conversations in markdown. Drop API specs into text files. Let agents grep their way to knowledge.
  - LlamaIndex's recent piece articulates this well: instead of building complex tool ecosystems, give agents a filesystem and basic operations (read, write, search). They learn capabilities from files containing instructions. They store history in markdown. They retrieve context through file search.
  - Letta's benchmark shows a filesystem-based approach hitting 74% on LoCoMo (a conversational memory benchmark) - beating specialized memory tools at 68.5%. Their argument: agents are post-trained on coding tasks, so they're good at filesystem operations. Simpler tools = better performance.

- Here's what I notice: every company pushing "files are all you need" happens to sell file processing infrastructure. 
  - LlamaIndex pitches their parsing pipeline (LlamaCloud Parse, Extract, Sheets) as the missing piece. "PDFs and Excel files aren't agent-ready - we make them agent-ready." Conveniently, their solution requires their paid parsing service.
  - Turso's AgentFS proposes treating agent state like a filesystem, implemented as a SQLite database. Guess what they sell? SQLite hosting.
  - Even Harrison Chase (LangChain CEO) is pushing this narrative: "File systems are a natural and powerful way to represent an agent's state." LangChain sells agent infrastructure - and files are simpler to build tooling around than structured memory.
- Full disclosure: I work on Hindsight, a structured memory system for agents. So I have the opposite bias - I'm incentivized to argue files aren't enough. 

- Enterprise codebases have several million tokens. A typical monorepo spans thousands of files. You can't stuff it all in. 
- Agentic retrieval solves this. Give the agent a file map, let it pick what to read. Until
  - Files over 500KB get excluded
  - Your repo has 2, 500+ files and indexing degrades
  - The agent needs multi-hop reasoning across 15 files
  - Your semantic search returns irrelevant matches because code isn't prose

- Context Rot Is Real
  - Even within the "official" context limits, performance degrades. The research calls this "lost in the middle" - models perform best when relevant information is at the beginning or end of context, and significantly worse when it's buried in the middle. 

- The Multi-Hop Problem
  - File-based approaches excel at single-hop retrieval. "Find the function that handles authentication" - grep, done
  - A naive filesystem search finds chunks about Alice OR infrastructure. It can't traverse the relationship chain directly.
- Now, there are file-based solutions to this:
  - Embeddings that capture semantic relationships
  - Hierarchical file structures encoding relationships
  - Agent-driven iterative search (read Alice's file, find Atlas reference, follow it). 
- The iterative approach works - I've used it. The agent reads about Alice, sees "Project Atlas, " searches for that, finds Kubernetes, follows that trail. But it costs multiple LLM calls and search operations per query.
  - With pre-built entity graphs, that traversal is a single lookup. The trade-off is build-time complexity vs query-time cost. Neither is objectively better - it depends on your query patterns and latency requirements.

- File Overhead (One Data Point)
  - Manus reported that their early versions used a todo.md file that got constantly rewritten - roughly 30% token overhead on file management.
  - file-based state management requires constant read-write cycles that consume context budget

- In my experience, the filesystem metaphor works as a foundation. Whether you need more depends on your use case.
- Where files work well:
  - Storing raw conversation history
  - Holding instruction sets and API specs
  - Grep-based retrieval for exact matches
  - Projects under ~100K tokens total context
  - Single-hop queries with clear keywords
- Where I've needed additional structure:
  - Temporal queries ("what happened last week") - files don't parse dates
  - High query volumes where iterative search latency adds up
  - Long-running agents where context compaction matters
  - Cross-session entity consistency

- Start with files. You'll probably add vector search, entity tracking, and compaction eventually. The question isn't whether files work - they do. It's whether "just files" scales past demos. I don't think it does, but I'd love to see benchmarks that prove me wrong.​

- ## The filesystem is important as an abstraction because we have 40+ years of tools trained on it.
- https://x.com/glcst/status/2011790821616386422  
  - For data that you generated and want to recall (like chat history), a database might be better.
  - The beautiful thing about sqlite is that it can give you both, at once.
  - AgentFS goes in that direction.
  - Even in the first version there is a key-value abstraction to store configuration. Not to mention direct access to the sqlite database itself.

- does AgentFS allow for disparete sources of file and objects ? Can i configure it to use some s3 bucket as well as local  storage?
  - no, the underpinning idea of agentfs is that the agent will want to have a unified view of the entire filesystem, and potentially do things like snapshot, rollback, fork. Which is why encapsulating it as a sqlite file works well.

- ## we're starting to hit the limits with keeping all the data for OpenCode as a bunch of flat json files _202601
- https://x.com/thdxr/status/2011631185399857465
  - these are nice for easy readability but obviously doesn't scale super well
  - is anyone particularly depending on this functionality? it'll likely all get moved into sqlite
  - this isn't for config it's for the data - your sessions, messages in them, etc

- One downside: this makes it far more challenging to run in sandboxes with object storage mounts while supporting resume

- I only started using OpenCode yesterday, one problem I often have with sqlite is that it's not diffable, so if I need to store conversations in git for whatever reason, that would mean I'd store an entire copy of the db every time I make a change.
  - we still have `opencode export` which will return the session + all messages + all parts in json format
  - we'll probably build a data explorer into opencode

- I'm building https://burntop.dev, an open source tool to track AI usage that reads from OpenCode JSON files. I think moving to SQLite is a good step forward, and Claude will be happy to update the parser to read from there!

- sqlite is the right call for local-first dev tools
  - claude code did the same. json files work until they don't
  - the migration path is clean anyway. one-time script, done

- Another option could be duckdb which I would prefer. You can natively import json into tables etc

- Please a have a solution for multi-machine sync. You can cobble together one with flat files and git today.

- it doesn’t matter what’s under the hood if i can do full import/export anytime and it will work

- Have you considered a single JSONL file like other agents instead of many JSON files?

- ### second question - would you be mad if every table was id | data (json blob)
- https://x.com/thdxr/status/2011638877933465896
- You won't ever want to do search/slice/etc? Not sure if sqlite has super fast json parsing but most databases slow down if you do deep search in JSON (b/c) they parse it on the fly over and over again).
  - we could do stored generated columns if that pops up

- Should be fine. Zed does that.
  - https://github.com/zed-industries/zed/blob/main/crates/agent/src/thread_store.rs

- EAVT is a strict improvement over this

- SQLite DB per user ala blueskyb

- ## 📃🛢️ seeing how langchain and opencode have made the topic cool again for agent memory/state
- https://x.com/swyx/status/2011984243430236608
  - i present how every filesystem-source-of-truth eventually turns into database

- seen this pattern play out so many times. everyone starts with "just a json file" and ends up reinventing postgres badly. the filesystem-to-database pipeline is inevitable once you need concurrent access or anything beyond key-value. agents just accelerated this realization
  - 🌰 logseq就是例子
  - opencode
- Langchain and opencode highlight a recurring pattern: as data complexity grows, systems evolve from simple storage to structured databases. It's a natural maturation as depth and retrieval efficiency become priorities.

- Tools like Langchain and Opencode simply formalize a truth: what begins as a file system for ease eventually demands database structure for scale.
  - File systems handle data retrieval reactively. As complexity scales, a database becomes essential for efficiency, allowing dynamic queries. That's the evolution.
  - Agent memory/state is evolving fast. Turning filesystems into databases highlights a real shift: data needs to be queryable and persistent to drive intelligent agents.

- lived this exact arc. started with markdown files as source of truth, added metadata files, then indexes, then suddenly you're maintaining a janky database with worse query semantics. the filesystem wants to be a database but fights you the whole way

- Yep—filesystems are the right v1 for agent state because they’re inspectable + diffable. Then you hit concurrency, indexing, permissions, and “who wrote what when”… and congrats, you rebuilt a DB.
- Feels like “agent memory” is replaying the same arc: start w/ files for transparency + diffability, then you need indexes, schema, retention, access control, and concurrency… and you’ve rebuilt a DB. Curious where you draw the line: content-addressed FS + index vs full DB?

- llama index a bit different!
  - unfortunately llamafile is taken
- there’s obviously benefits to adding semantic indexing and some metadata layer in a db for faster initial lookup. And intersperse that with file ops 
  - will ls / grep work as quickly when backed by a db? Unclear

- the filesystem is just a graph database. All of you saying you don't need a graph for agents while using the filesystem are just in denial about using a graph.

- Every filesystem conceived as a source of truth eventually seeks the structure and query efficiency of a database. It's a transition driven by the need for scalable, organized information access—not just storage.

- i think this misses the fact that the benefit of filesystems is that they can be huge in size (which is a requirement for long-horizon, context-heavy tasks). perf for dbs that contain filesystems is bad to the point that it's not useful for large filesystems. try using agentfs from turso with a codebase and you'll see the issues. it's probably that we want a metadata layer over filesystems that make them queryable/(restorable?)/version-able, but agents must work in filesystems

- we went straight to sqlite for agent state and skipped the filesystem-as-memory arc entirely. no regrets. the moment you need transactions or queryable history, you're reimplementing a database with file locks anyway

- ## We launched LangSmith Agent Builder this week as a no-code way to build agents. _20260115
- https://x.com/hwchase17/status/2011834318172422279
  - A key part of Agent builder is it’s memory system. In this blog we cover our rationale for prioritizing a memory system, technical details of how we built it
  - We don’t use an actual filesystem. We use Postgres but have a wrapper on top of it expose it to the LLM as a filesystem

- Similar to agentfs?

- been thinking about doing something with DuckDB because of this. 

- just used an actual filesystem dawg, sandboxes are cheap
  - Until you need replication, additional indexes etc, I think this makes sense
- let’s just decide on sql. everyone loves sql.

- exposing things to llms through familiar interfaces is underrated. filesystem is one of the most universal abstractions. makes sense that it maps well to how agents should think about persistence. postgres under the hood is smart for scale without giving up the mental model

- We should expect that users will throw huge files during agent sessions. it can be video or large images. So this would be very inefficient for that.
- Why not just throw multimedia content in a bucket and store the pointer?
  - It's possible to do it but we have to pay the tax of upload and download to and from sandbox.
  - Because object storage buckets don't have full POSIX support. So the agent loses tons of functionality that is gets when its using local file system. Also reads and writes are extremely slow too.
- But there's a transfer tax either way (Postgres to sandbox or S3 to sandbox). Consider a pattern where metadata + pointers live in Postgres and bytes in object storage. Agent queries DB to see what exists, then tool call fetches into sandbox on-demand. Sandbox has real POSIX once files land. Seems strictly better for the large file case?
  - ya, this block device technique is quite interesting.
- Is blob storage tech good enough to do a lustre like distributed persistent storage where tons of agents can contribute and make dirt cheap snapshots of data as they work on it.

- love that hack. i once mapped s3 calls to sql tables for an “imaginary” fs too. feels like tricking the matrix with a good old postgres paintbrush.

- ## Towards a Disaggregated Agent Filesystem on Object Storage
- https://x.com/penberg/status/2010360708253274513
  - The filesystem abstraction is an effective interface for AI agents, and AgentFS provides exactly that on top of a SQLite database file. But as agent workloads scale with more agents, longer-running tasks, and multi-agent  collaboration, we need to move beyond the single-file-on-local-disk  model. State needs to survive ephemeral compute, move between machines, and scale without requiring persistent volumes to be provisioned. 
  - This  post explores how SQLite's WAL-based architecture, combined with Turso's S3-based diskless architecture, provides a path toward disaggregated agent filesystems on object storage.

- Agents want a filesystem. The filesystem abstraction is an  effective interface for AI agents. The everything-is-a-file philosophy that Unix established over 50  years ago created an ecosystem of thousands of specialized CLI tools, all built around a common abstraction.
- The problem is that real filesystems require real infrastructure.  Running agents with filesystem access means either spinning up  containers, managing VMs, or accepting the security risk of letting  agents run commands directly on your machine
  - Furthermore, in  lightweight environments like serverless or browser-based agents, there  is no filesystem to access to begin with. And even when you do have a  filesystem, operating persistent volumes at scale to host them is just  hard.

- Agents need to be snapshotted and resumed. Autonomous systems are  inherently unpredictable. 
  - Traditional approaches fall short because they involve cobbling together  multiple tools: databases for state storage, logging systems for audit  trails, local filesystems for artifacts, and version control for  history. The inherent fragmentation creates complexity and leaves gaps  in observability. What you actually want is the ability to snapshot an  agent's complete state by copying a single file, then restore it later  to reproduce exact execution conditions or test what-if scenarios.
  - you could pause an agent, inspect its state, then continue  from exactly where it left off. None of this works if the state is tied  to a specific instance or volume.
- You need portability for debugging and collaboration as well. 
  - You wish to diff two runs, or query exactly what happened with SQL.  Having a state that can travel as a single, portable unit, not one  scattered across filesystems, environment variables, and ephemeral  containers, is the key.

- AgentFS is a filesystem abstraction designed for agents. Rather than relying on the host operating system's filesystem, AgentFS stores everything in a SQLite database: files, directories, metadata, key-value state, and an audit log of tool calls. 
- The design provides three core interfaces. 
  - The filesystem interface provides POSIX-like operations on files and directories—read, write, create, rename, and delete. Agents interact with it the same way they  would with any filesystem. 
  - The key-value interface stores agent state  and context as JSON-serialized values, needed for session data, configuration, or intermediate computation results. 
  - The toolcall interface records an append-only audit log of every tool invocation, capturing inputs, outputs, and timing for debugging and compliance.

- Under the hood, the filesystem storage follows a classic inode/dentry  design. The dentry (directory entry) table maps names to locations in  the directory hierarchy, acting as a lookup cache. The inode table  stores actual file contents and metadata (size, permissions, and  timestamps). This separation mirrors how operating system kernels  organize filesystem data, but implemented entirely in SQLite tables.  Deletions in overlay scenarios use a whiteout mechanism: rather than  modifying a base layer, the overlay records deleted paths in a whiteout  table and filters them out on reads.
- The key insight is that SQLite provides exactly the properties agents  need. A single file contains the complete agent runtime, which you can  copy to another machine, check into version control, or attach to a bug  report
  - because everything is structured data, you can query agent behavior  with SQL—find all files modified in the last hour, trace the sequence of  tool calls that led to an error, or extract metrics for analysis.

- For agents that need native tool compatibility, AgentFS provides FUSE  support on Linux (and NFS on macOS) that you mount the SQLite-backed  filesystem as a real POSIX filesystem, allowing you to run git, grep, ffmpeg, or any Unix tool directly without integration code.
  - As shown in Figure 1, the agent invokes bash, which executes commands. The commands interact with the operating  system kernel via system calls. 
  - Filesystem operations such as open and close are delegated to a userspace daemon that AgentFS provides to access the  filesystem metadata stored in a SQLite database file. 
  - Reading from files is very cheap because the kernel page cache amortizes the cost of reading from the FUSE userspace daemon. 
  - Writing to files is also done on the kernel page cache first, then written back asynchronously to the FUSE module.
- For lightweight environments like serverless or browsers where you can't  mount a filesystem, the bash-tool integration provides a TypeScript reimplementation of common shell commands that operate directly on AgentFS.

- The AgentFS design stores everything in a single SQLite database file on  the local disk. The approach works well for single-machine scenarios:  it provides atomicity, durability, queryability, and portability.  
  - However, as agent workloads scale with more agents, longer-running  tasks, or multi-agent workloads, we need a disaggregated model in which  the agent filesystem resides on an object store.
- A decoupled-metadata, object-backed distributed filesystem, such as JuiceFS or HopsFS, solves the problem by separating filesystem metadata and data, storing  them in a key-value or relational database and an object store, respectively. 
  - However, building AgentFS on top of SQLite enables  disaggregation at a different level: the database itself. 
  - SQLite uses a write-ahead log (WAL) that captures all mutations as a sequence of changes before they're checkpointed into the main database file. The database file represents the committed state; the WAL represents in-flight changes.
  - With Turso's sync protocol, local changes are pushed to a remote as  logical mutations, while remote changes are pulled as physical pages.  The object store acts as the source of truth. This means you can  checkpoint the database file to object storage, stream WAL entries  through a coordination layer, and reconstruct agent state on any  machin
- This hybrid approach gives you the best of both worlds. Reads and writes  occur at local-disk speed against an in-memory or locally cached  database. The WAL captures changes with minimal overhead. Background  sync handles durability and replication to object storage without  blocking the agent. And because the remote state is the source of truth, you get automatic conflict resolution when multiple agents modify the  same filesystem, just like you would get with something like Dropbox, for example.

- ## AgentFS copy-on-write overlay in action
- https://x.com/penberg/status/2007533204622770214
  - Multiple AI agents working on the same codebase. Each with isolated changes, zero conflicts. Host files stay untouched.

- how much performance overhead does it add? how much longer would a command like npm install take?
  - For example, ”npx create-react-app” takes 3x longer with agentfs compared to native xfs, but it’s just lack of async which should be fixable. That said, I use agentfs to build agentfs and don’t really notice any slowdown because agents usually work in parallel in the background

- AgentFS is such a nice middle ground between agents on prod and messy git worktrees. Curious how you are thinking about surfacing and merging the best overlay back once 5 agents diverge hard on the same feature.
  - The agent needs to coordinate this because is such a use cases specific thing. However, I think we need an "agentfs apply" (easy) or "agentfs merge" (much harder) commands to assist in the merging of the delta layer to the base filesystem. But figuring out which overlay is best I think is purely agent stuff (we might need some nicer tooling to audit the overlay of course).

- sounds like a recipe for disaster. git branches/worktrees are simply superior. it would be very easy to end up with both agents having broken code that all the time. What happens later, would it merge session files back into host filesystem once done?
  - Nothing happens later unless you explicitly want something to happen. The way i use it is by making the agents push to git remote branch which means the agents never know about each other
- Copying the code is the easy part, the problem is the vendor directories

- I saw the fuse implementation now, that’s impressive, must have a try

- how is this different than GIT worktrees?

- This solves a real pain point. We've been running 5+ Claude instances in parallel and the worktree juggling adds friction. COW at the filesystem level means agents can work truly independently without the git ceremony. Curious if there's a plan for handling npm/node_modules sharing across overlays.

- I am writing a conductor-like TUI tool to run multiple Claude Code and Codex agents in parallel and right now they are using git worktrees. Do you think using fs-agent as a replacement would be too painful?

- ## For the "I just want bash for my AI agent" crowd: AI SDK  + just-bash + AgentFS. That's it. That's the stack.
- https://x.com/penberg/status/2007174813467701337
  - [Building AI agents with just bash and a filesystem in TypeScript _202601](https://turso.tech/blog/agentfs-just-bash)
- Why is this better than a sandbox / container?
  - hey solve different problems and can be used together. 

- ## Bash running on Cloudflare Workers with AgentFS
- https://x.com/penberg/status/2007110953167622292
  - AI SDK + AgentFS integration with just-bash looks pretty slick.
- What do you think of adding durable object SQLite support for agentfs? I was thinking it could be done by adding an optional property “driver” to the constructor. It would default to the existing implementation. But I could also make a durable object sqlite driver. And a driver principally just needs to implement exec, transaction and maybe open/close (at start and end of lifecycle). then your agents sdk agents could use a shell and a filesystem for most tasks and boot a sandbox only when needed!
  - Yeah, I think it makes sense. I think a good integration path would be to add a FileSystem interface to the TypeScript SDK (which we already have in the Rust SDK) and then have a separate Turso and Durable Object implementation of AgentFS as their interfaces are totally different. But sure, totally open to merging something like this if the integration is clean

- Does this mean we could have serverless Claude Code?
  - This uses just-bash which won’t run Claude Code. But you could certainly build a coding agent with it

- This approach will be much less expensive than rolling out a full VM for the agent. It could be a useful pattern for supporting skills files for example. Am I correct?
  - Yes, indeed. I assume you can other sandbox providers for this too. I believe just-bash is Vercel Sandbox compatible, for example.

- ## Here's how I do agentic coding with AgentFS
- https://x.com/penberg/status/2005931121754693713
  - Step 1: Clone the repository
  - Step 2: Start an agentfs session
  - Step 3 (optional): Manual investigation
  - Step 4: Make branch, commit, and push

# discuss
- ## 

- ## 

- ## 

- ## We are writing a massive multitenant database at Turso. A node is capable of running hundreds of thousands of databases, concurrently. 
- https://x.com/iavins/status/1900220354985169332
  - We also decided to write our own asynchronous runtime implementation (instead of using `Tokio` ) for reasons. Now this bad boy is all bare bones, we don't use Rust's `async` yet.
  - For disk or network we use io_uring (of course). Since it's a database, that's pretty much all it does: talk with io. And that requires a state machine. You submit a request, wait for some time to poll or for callback to trigger. That means, a function doesn't always have a result ready; sometimes it says, my friend wait for sometime, I don't have result ready yet: `Ok(None)` . When it's done you get: `Ok(Some(T))` .
  - The entire codebase is pretty much `Result<Option<T>>`

- Fallible Iterators also use Result`<Option<T>>. Ok(Some(T))`: when there's valid next item. Ok(None) when iteration's complete.

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
