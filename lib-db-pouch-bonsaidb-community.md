---
title: lib-db-pouch-bonsaidb-community
tags: [bonsaidb, community, couch-like]
created: 2024-01-04T06:35:35.015Z
modified: 2024-01-04T06:36:06.762Z
---

# lib-db-pouch-bonsaidb-community

# guide

- dev-xp
  - couchdb/couchstore/replication/protocol/lsm
# discuss-stars
- ## 

- ## 

- ## 🚀🎯 [Introducing Nebari, a key-value data store written using an append-only file format_20210929](https://community.khonsulabs.com/t/introducing-nebari-a-key-value-data-store-written-using-an-append-only-file-format/81)
- Nebari is an append-only database implementation loosely inspired by Couchstore. 
  - It is not ready to be used in anything except experiments – the file format will likely change multiple times before its first stable release.
- Why would you want an append-only database implementation?
  - Database files are plain files that can be copied and backed up through regular file copies. The file format is guaranteed to always be consistent, since once the bytes are written to disk, they will never change.
  - Because whatever process is writing to the file will be adding bytes to the end of the file, readers are never blocked by an in-process write operation.
  - With a little extra information written, full version history can be exposed for the database.
- Why wouldn’t you want an append-only database implementation?
  - If your database is write-heavy, your database over time will contain a lot of data that isn’t in use anymore. 
  - A “compaction” process is needed to reclaim disk space. This process isn’t as bad as it sounds, since it can be done without blocking the database, but it adds IO overhead while it is happening.
- Why not to use Nebari instead of Sled?
  - After reading other people’s comments on Sled having high memory usage, I tried to narrow down the strange test failure I had on my Mac related to massive memory usage.
- What caused the uncontrolled memory usage?
  - Now that I was 100% sure it wasn’t cause by Sled, I tried in earnest to reproduce it on my Linux PC. By increasing the test-treads to a larger number, I was able to reproduce it occasionally on my PC.
  - With that problem solved, I had a real dilemma: keep pushing on Nebari or revert back to Sled.
- Why still develop Nebari?
  - One of the biggest selling points to me personally is that I understand it. It’s simple enough that I feel confident that other people could safely contribute without needing to feel like a database engineer. By using Nebari, I am in better control of the full destiny of BonsaiDb.
  - Nebari is maintaining a transaction log, and so is BonsaiDb. BonsaiDb does it by using a tree in Sled/Nebari to store the transactions. Thus, when running this benchmark with Nebari, the transaction data is being stored twice. This makes fair benchmarks hard to do – disabling this chunk of code when executing against Nebari is one of the benefits of using Nebari. 
  - the flexibility is the strongest argument I have for developing Nebari for BonsaiDb. I will be able to custom-tailor Nebari to solve the usage patterns of BonsaiDb, including: Opt-in full version history for collections
- With all those things in mind, I’m currently of the mindset that Nebari has its place in the Rust ecosystem as well as in BonsaiDb. Unfortunately, I don’t think it’s tenable(守得住的; 站得住脚的, 合理的:) to support multiple storage layers for BonsaiDb.

- ## 🚀 [Short Update: PliantDb is now known as BonsaiDb_202107](https://community.khonsulabs.com/t/short-update-pliantdb-is-now-known-as-bonsaidb/74)

# discuss
- ## 

- ## 

- ## 

- ## Nebari is still on my "old" data model which requires two fsyncs per transaction. _202401
- https://discord.com/channels/578968877866811403/833332909808025610/1197197774509314078
  - It'll scream when I eventually get it onto the new storage system. (I've been feeling the itch to dust this off, so I'm hopeful I'll get back to it sometime this year)

- Is compression implemented or planned for sediment/nebari?
  - I wasn't originally planning it for Sediment, since to me it's a bit of a low-level building block type library. And Nebari was designed around the idea of a vault which is given the opportunitty to perform any operations on all blocks stored and loaded from the database. This is how BonsaiDb implements compression and encryption in Nebari.

- ## What's the status of sediment + nebari looking like? I've been interested to see how it performs_202312
- https://discord.com/channels/578968877866811403/833332909808025610/1188641694300786789
- From my memory, I got a bit frustrated realizing there was no easy way forward to keep backwards compatibility between old nebari and new nebari. Once I realized how much work was going to be required to finish it up, I decided I should instead focus on getting a BonsaiDb update out the door.
  - After shipping the BonsaiDb update, I really wanted to use it. That ended up evolving into another take on Gooey which I just released the first alpha of. I'm currently a bit more interested in continuing to try to build something with BonsaiDb + Gooey for the near future.
  - But, never fear, I have been craving dusting off the project and finishing it up. I haven't lost interest, I'm just a crazy person who is tackling too much for his own good!

- Another thing: any plans for eventual/near real-time durability? Fsync'ing after every write is not needed for every workload; this may actually affect okayWAL too, haven't checked. JammDB has the same problem of me not being able to turn off aggressive fsyncing.
  - In short, I'm primarily only interested in ACID compliant workloads. If PostgreSQL can't keep up with your hypothetical workload, then the databases I'm building won't be able to either.
  - With that being said, there's one workflow where I do plan on supporting "delayed" fsyncing: BonsaiDb's views. The view updaters never need to wait for an fsync. The data is still being written in isoliation inside of a transaction, but once it's written, since the views are dynamically generated, it's ok for data loss to occur. I don't remember having a specific plan on how to still occasionally fsync without blocking for fsync.
  - 👉🏻 OkayWAL/Sediment are designed to batch fsync operations so that many transactions happen per fsync. This helps get the actual data ingestion rate closer to the actual write speed of the disk.
- I would have to benchmark that because you are still doing synchronous flushes that way. Having a way to turn that off and adding a Nebari::flush or OkayWal::flush would allow the user to determine when to flush, which seems quite important for a low level building block like that. That's one reason I couldn't consider okayWAL
  - I would welcome comparisons in benchmarks. From my best ability to benchmark PostgreSQL's write performance, OkayWAL is very close in performance. (in the situations I've observed it, ymmv) 
  - Unless your workload is purely single threaded -- in a single threaded environment, you're right, everything is sequential.
- Have you compared with RocksDB as well? 
  - Yes, sediment's benchmark suite had rocksdb in it for a long time until it broke my ci 
- That's for an ACID workload though right? Not a bulk loading or high insertion workload? Cause 2ms is too slow for either. I mean like timeseries data; 10/50/100k+ inserts per second, but low consistency requirements 
  - Adding a caching frontend that does periodic commits solves that in a way without adding a need for a more complex storage layer
  - In fact, I'd argue that architecture will lead to a more optimal IO load because instead of streaming 100 writes to the same key to disk with eventual consistency, it would only update the key once every time its threshold of time or number of changes was met.
  - This is how the BonsaiDB Key-Value store is designed today, and it's how it gets close to redis's performance. From my profiling results, the main issue preventing it from meeting Redis's performance is that tokio-tungstenite doesn't offer an API for getting the socket messages without copying the data new to vec's -- not database related, purely networking related.

- ## I just released v0.5.5 of Nebari, which removes one more block for me releasing an update to BonsaiDb_202302
- https://discord.com/channels/578968877866811403/833332909808025610/1079789837122535535
  - Last fall, after seeing the wall of tasks left to complete to finish up the storage rewrite, I thought about trying to get a new release of BonsaiDb without the storage rewrite going.
  - In my state of burnout at the time, this ended up being just one more blow -- I wasn't getting any good information, and each time I tried, I had to wait an hour for it to fail.
  - main has a lot of breaking changes that are geared up for the BonsaiDb storage revamp. So I back-ported the change atop v0.5.4 to create an update without any breaking changes that addresses this issue.

- ## Whats the state of bonsai? I really like the idea of bonsai with the schema written in rust and would like to contribute?_202302
- https://discord.com/channels/578968877866811403/833332909808025610/1071088384602284132
- It's usable in its current form, but a bit slow to write transactions. In terms of development, I've been working on rewriting the storage layer, and haven't been using it in projects until very recently, so the high-level BonsaiDb crate really hasn't seen much improvement in the past few months. 
- So sediment is currently what you are focusing on?
  - Yes, although I'm about ready to integrate it into Nebari
- you doing that on the sediment branch of Nebari?
  - Maybe? I've rewritten sediment since I last started integrating it, and I haven't had a chance to see how bad the branch is in its current state. I think I kept the API fairly similar, so I think I can salvage the work I've already done
- Ah I see, what else do you need done on sediment before your ready to integrate?
  - The main missing feature is rollback on the main data store when a power outage or crash occurs.
- commit log is already implemented I assume> I mean i see it here but is it complete? also where will tests be written?
  - Yes, and pretty thoroughly tested although I want to throw a fuzzer at the whole thing soon. The tests are all written in the repository
- The format is designed to allow me to write to multiple files, then queue up all the fsync operations for the files that were touched. In the event of a crash or power outage, it could happen at any point (before write, mid-write, mid-sync, post sync) on any file being updated.
  - Since the index file could be fully synced yet some stratum wasn't fully synced, we need to be able to roll back to the previous header if we detect that the last commit wasn't fully written. That's why the other copy of the header(s) exists.

- 🐛 Ugh, this is the second day I've been trying to look at Nebari's Sediment branch, and I'm realizing how much I changed in Sediment's architecture. It really might be better to redo most of the Sediment integration than use this branch afterall.

- ## BonsaiDb really could be built atop any key-value store that supports ACID transactions. In that other pull request I linked, that isn't true anymore -- I'm fully leveraging my specific key-value store Nebari. _202301
- https://discord.com/channels/578968877866811403/833332909808025610/1064590847292747837
  - But even then, the truly low-level bits are hidden in Nebari.
  - 🎯 My goal with the rewrite of how Nebari works (Sediment/OkayWAL) is to end up with something that's documented well enough that anyone else could dive into it. I don't feel like any one particular thing I'm doing is that complex, and I feel like with some good documentation guiding how it all fits together, almost anyone could understand how it all works.
  - One other thing that I wanted to mention is that the new storage rewrite will alleviate the need to periodically compact your database -- Nebari currently is implemented using an append-only file format. If you're not doing much updates or deletes, there won't be as much junk data being accumulated, but there will still be some extra space that can be reclaimed by compacting the database.

- That's awesome, I was already starting to think ahead about compactions and what to do about that. Actually, I hadn't considered this but compaction doesn't happen in memory does it? Like it's not loading the entire DB to memory? (as I'm saying this it seems increasingly unlikely that this is the case - it wouldn't make sense for large databases just the same as it doesn't make sense for a database on limited hardware)
  - Nope, compaction is handled by Nebari and streams the data intelligently with very minimal ram required.
- Even when you run out of space... you can manually remove the view files inside of the database safely while it's shut down. They'll just rebuild when needed again.

- ## 🎯 [Project Status_202301](https://github.com/khonsulabs/bonsaidb/issues/262)
- It is still in active development, but it's definitely had its progress slowed. There is a pending file format redesign that I plan on offering at least migration tools
  - July 2022: I wrote an overview of my goals of Sediment, a storage layer I am planning on sitting below Nebari, which BonsaiDb uses for the underlying database implementation.
  - August 2022: I get Sediment to the point of benchmarking, I went and did the same benchmark against PostgreSQL and discovered that PostgreSQL outperformed them all. Why? It turns out Write-ahead logging is the fastest way to get incoming writes to disk.
  - September 2022: I wrote my own WAL implementation, inspired in-part by sharded-log. What I found shocked me -- PostgreSQLs much simpler single-writer-at-a-time WAL design outperformed my implementation and sharded-log significantly, even with a large number of threads all competing to write at the same time. I scrapped the blog post and began rewriting my implementation to be inspired by PostgreSQL instead.
  - October 2022: I finished my rewrite of OkayWAL, and I saw the mountain of work ahead of me to get everything tied back together. I was a bit burned out, and I needed a break.
  - December 2022: I've begun a rewrite of Sediment due to changing some of my goals now that there is a WAL in front of the storage layer. It's still early in development.
- One serious thought I still have is whether Nebari should exist, or whether BonsaiDb should just use another database format. 
- There are two main arguments for pursuing my new format are:
  - BonsaiDb/CouchDB were designed with the idea of being able to embed extra information inside of the B+Tree structures. This is how the map/reduce is powered -- the reduced values can be stored directly in the B+Tree so that a reduce query doesn't need to visit all of the nodes in the tree to come up with an aggregate result. From what I could find, no other database engine that is written in Rust supports embedding extra information inside of the B+Tree structure itself, while it's a key-feature of Nebari.
  - Nearly every other embedded database engine does not utilize a write-ahead log. In my testing, a write-ahead log is absolutely critical for insert performance. A developer can always use a write-ahead log manually in front of the database, but having it built-in seems like a very valuable feature.
- That annotated B+ Tree is a really neat innovation, certainly not something I'd stumbled onto before.
- The new format I'm designing will have some increased memory usage to keep track of various on-disk state, but it should still be able to be used comfortably in a low-memory environment.

- ## do you recommend a way to monitor the changes in bonsaidb database ?_202207
- https://discord.com/channels/578968877866811403/833332909808025610/994152982457364511
- For real-time monitoring, right now the best way would be to use PubSub, but that will require manually publishing a message each place you are modifying the database. In the future, I want to allow subscribing to changed document notifications without manually implementing it yourself.
  - For being able to monitor changes over time, there isn't a good solution right now. In v0.5, I am changing the storage format which will help me get closer to https://github.com/khonsulabs/bonsaidb/issues/186, which should also bring along the ability to get a list of all changes to any specific collection. This "feed" of changes is what replication will be powered by.

- ## 🔁 Does remote clients are able to automatically reconnect to the database if the connection is lost?_202202
- https://discord.com/channels/578968877866811403/833332909808025610/944650087085268992
- Yes, the Client is designed to automatically reconnect the next time it is used. The way it works is that if a disconnect happens, all pending operations in all threads/tasks will return an error. If any thread/task chooses to try to recover by trying again, the Client will attempt to reconnect automatically. 

- 🆚️ What are the differences between the WebSocket based protocol and the QUIC based protocol? Which one should be preferred?
  - If you're operating on a private network with low latency, the websocket protocol doesn't require TLS and the downsides of TCP are less noticeable without latency.
  - Over the internet, QUIC should provide better overall reliability and performance, especially with higher latency or any packet loss. However, it's driven by UDP and some ISPs/networks are overly restrictive on UDP traffic, so it may not always be available.
  - You can use BonsaiDb to listen for TLS websocket connections if you want TLS on your websockets, or you can offload the TLS with websockets to a proxy like nginx if you are using it that way.

- ## Are there resources for learning how to properly structure data and collections?_202205
- https://discord.com/channels/578968877866811403/833332909808025610/971440316580253746
- Not yet, sadly! It could be helpful to look at some best practice guides for CouchDB -- while there may be specific bits of information that aren't the same as BonsaiDb, overall the basic concepts about how to organize data will be similar.

- ## have you seen lmdb?
- https://discord.com/channels/578968877866811403/833332909808025610/961617480923635723
- I have seen lmdb, but I've never used it. When evaluating options to use, we wanted a pure-Rust implementation, so it wasn't really considered heavily in the process. 
  - Originally we used Sled, but I eventually built Nebari to more closely match what CouchDB does -- and simplify our dependencies significantly.

- ## A couple of questions about Views._202204
- https://discord.com/channels/578968877866811403/833332909808025610/969641936338169988
  - 1. How reduces are called internally?
  - 2. reduce() function takes [(key, value)] but I would expect it to take (key, [value]) since all the keys are the same. 
- I was looking into changing the reduce() signature, and I figured out why it takes an array of key-value pairs: reduce() can operate across a range of key/value pairs. For example, you can reduce the entire view.
  - The current design is 100% a mirror of CouchDb's design. I have a bit more of a type-forward approach in Nebari, which allows for there to be a separate value and reduced value type. It calls reduce() with an array of values which produces a reduced value type. Then it calls re-reduce as needed to convert an array of reduced values into a single reduced value.

- ## I'm part of the CouchDB community so was super interested and excited when you mentioned that BonsaiDb took some ideas from CouchDB._202203
- https://discord.com/channels/578968877866811403/833332909808025610/956907468724764702
- it's always great to meet people that helped build CouchDB and related projects! It's such a lovely concept. BonsaiDb is pretty far away from a REST-based database, but the architecture is guided by how I knew CouchDB behaved/was designed
- Cool. Also happy to tell you things we got wrong so you don't make the same mistakes
  - Yes please. Especially with regards to any pitfalls with replication. I have a good idea of how I want to write it at this point, and it's heavily inspired by how CouchDB did it.
- How do you keep track of document revisions? Is it a tree?
  - Yes it's a tree. My version of CouchStore creates 2 B-Trees in the same file, one with a sequence of each write and one that is ordered by-id/by-key. 
- If you were to look at BonsaiDb currently, it is using a SHA revision rather than the sequence id. I only realized over the past month I forgot to change that when I swapped out my storage layer with my version of CouchStore (Nebari). 
  - That's my next highest priority refactor. Remove sha256 from Revision

- ## Would there be a way to make List and View be able to skip a certain amount of elements thinking about my pagination thing._202203
- https://discord.com/channels/578968877866811403/833332909808025610/953604306177773598
  - I can limit them and ascending them but apparently not say, skip the first 40 entries and give me the next 10. Is that something that would make sense to have in the API?
- No, that's not possible. I haven't thought about the idea of how to do a multi-collection view -- I'm also not sure what the "source" would be on the resulting view mapping
- It's technically possible, but I chose this pattern to match what CouchDb supported. One benefit to using the approach I outlined with pseudocode before is that you're guaranteed to never receive the same row twice. If you have a non-incrementing primary key and you use an offset instead of "after" and a document has been inserted that has its id within the range of documents you already retrieved, using an offset will mean that the first record returned will be the last record you already fetched due to the new document being counted as a "skipped" item. 

- ## We're looking for a multi-master (MM) first database (or kv storage) that would allow us to seamlessly sync embedded client_202203
- https://discord.com/channels/578968877866811403/833332909808025610/951082540184260668
  - Our eyes were first looking towards couchdb, but it doesn't offer embedded db (I would have to host a couchdb server locally). Then it turned out that PouchDB wants to achieve that, but it's a JS library whilst our app (a library in fact) will be written in rust
- BonsaiDb doesn't currently offer anything beyond a single-server model. Long-term, replication will be able to support a similar setup to how PouchDB/CouchDB work, allowing bi-directional replication on a per-database basis with hooks for conflict resolution. It's something I'm hoping to get started later this year. There's still a lot of features I'm wanting to tackle both as pre-requisites (persistent job system) as well as just basic missing functionality that users are running up against.

- ## [Consider adding support for huge blobs_202203](https://github.com/khonsulabs/bonsaidb/issues/222)
- BonsaiDb has a 4GB document size limit, which comes from Nebari's "chunk size" limit. More importantly, however, Nebari treats chunks as whole pieces of information that must be loaded completely in memory to be returned. The side effect is that while BonsaiDb has a 4GB document size limit, the practical limit is the available RAM. Even if Nebari's limit were increased, it would require so much RAM, it wouldn't be practical.
  - MongoDB offers an easy abstraction that allows storing larger files in segments. 
  - CouchDB supports an attachments API which allows associating one or more blobs of data with a document. 
  - Both of these ideas seem like good starting points for considering how to enable handling of large blobs, including the ability to stream the blobs without loading the entire blob in to memory.
  - 已实现

- ## I'm the original author of Couchstore - its really cool to see Nebari and BonsaiDB_202201
- https://discord.com/channels/578968877866811403/833332909808025610/930746813995180053
  -  I really like the CouchDB model but as you might expect also think there's tons of value in embeddable, use-what-you-need versions of it that don't bring all the original CouchDB constraints along
- thank you for writing Couchstore! I don't think I would have succeeded in building Nebari without it 
  - I like the fundamental concepts of CouchDB, and originally my design mirrored it very closely with a few changes to make things a bit more Rusty. But as we started thinking about all the possibilities, I just decided it was best to use CouchDB for inspiration but build my own thing.

- ## [Implementing a new storage layer for BonsaiDb_202109](https://community.khonsulabs.com/t/implementing-a-new-storage-layer-for-bonsaidb/78)
- [Introduce new storage layer_202109](https://github.com/khonsulabs/bonsaidb/pull/73)
- A detail that I had been keeping to myself is that I couldn’t actually run my test suite on my Macbook Air M1. The reason was memory usage.
- I began by creating an abstraction between tokio-uring and tokio::fs.
- I’m still wanting to work on Gooey to get to the point of building BonsaiDb administration tools in it.

- ## 💡 PliantDb looks great! Here's what I'd like to know:_20210624
- https://discord.com/channels/578968877866811403/833332909808025610/857619903010701323
  1. It's stated in many places that CouchDB inspired PliantDb, but compatability is not a goal. Does PliantDb have conflict resolution for when multiple databases sync with different updates, or is it just "Last update wins."?
  2. The type name Schematic seems to be used for schemas. I believe that schematic and schemas are 2 different  things. Was this intentional?
  3. The current version is not yet at 1.0, and messages are everywhere to not use it, yet. What features aren't yet implemented or trusted?

- 🛋️ In CouchDB, the replication model supports two servers operating independently and resolving using a tree model 
  - I personally have not had the need for this sort of functionality, and it makes implementation much harder. 
  - So, I opted for a much simpler strategy but it's similar. The first writer will succeed, but just as in CouchDb, the revision ("_rev" in couch) is updated. 
  - That means that the in-flight second writer will no longer be able to save, and will instead get a conflict error returned 
  - For Schema and Schematic, Schema is a high level plan, in a way. You could use it to look up all the information needed, but it's not as efficient. I needed a word to describe an instance of that Schema but with other functionality such as looking up a view without needing to query every collection. When hunting for a name, I saw Schematic
  - In terms of what's trusted: everything. I feel confident in this implementation because of the code coverage. It's not perfect, and I'm sure there are some bugs, but the biggest concern to me is storage formats.

- ## Is it supposed to be a database with servers (like Mongo, MySQL etc) or like local file database (like sqlite) ?_202104
- https://discord.com/channels/578968877866811403/833332909808025610/833354209624719441
  - You have already mentioned about CouchDB but I am still confused
- It's both. If you want to just use it locally, you can just use the local implementation. If you want to go further, you should be able to grow from the local database implementation to a full server. It's meant to be flexible and grow with you as your project grows.

- A significant amount of functionality is already implemented, enough to use it in a project with a minimal feature set. I still need a little more functionality to fully replace Redis in Cosmic Verge, but I'm very close to updating Cosmic Verge to using PliantDB.
  - That being said, there's a lot of things I still want to do with PliantDB. The biggest unwritten feature is clustering support -- the ability to run multiple PliantDB servers as if they're one server, and the load is shared between them. But, there's a lot of small features too, some which are already in the Issues list on GitHub, others that are still in my head.
