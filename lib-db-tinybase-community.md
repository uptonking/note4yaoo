---
title: lib-db-tinybase-community
tags: [collaboration, community, database, tinybase]
created: 2023-01-12T15:51:52.243Z
modified: 2023-04-21T11:42:46.575Z
---

# lib-db-tinybase-community

# guide

- pros
  - reactive data store for local‑first apps
  - Easily sync your data to browser storage, IndexedDB, SQLite, CRDTs, PartyKit, ElectricSQL
  - 支持undo/redo, 需使用checkpoint，似乎不是基于delta的方案
  - 提供了collaboration的示例

- cons
  - 未采用插件式架构

- features
  - ?

- 变更树的计算方法比较
  - tinybase直接diff两颗hlc-tree，能准确计算出最小变更树
    - Adding Merkel hashing to the tree would be slower but would allow the negotiation to bail out (or identify tree diffs) much sooner.
  - actual-merkle-tree虽然能快速计算上次变更节点，❓(待确认)但之后从上次变更节点计算需要发送给本地的变更树时，可能包含已经执行过的op，传输不必要的数据

- tinysync的示例存在一定问题
  - 在同步的同时产生的新op因为listening为0而被忽略

- alternatives
  - sql.js
  - datascript
# dev
- [Closing The Gap Between Your Users And Their Data using tinybase_202211](https://tripleodeon.com/2022/11/closing-the-gap-between-your-users-and-their-data)

## [lofi-meeting-tinybase_20230725](https://www.youtube.com/watch?v=sshvBCK5NDs&t=1140s)

- no deps
- opinionated data structure: table/row/cell

- roadmap
  - auth and permissions
  - sharding: sync partial data
  - local-first and ai
  - we lack the killer local-first app

## [lofi-meeting-crsqlite_20230725](https://www.youtube.com/watch?v=sshvBCK5NDs&t=2400s)

- problem1: partial-sharing
  - share a doc or a whole repository
  - edit permitted sections/rows of a doc
  - comment only
- solutions
  - implement rules in the client
    - all data of doc available
    - doc contains acl
    - view rendered/hidden based on acl
    - not so safe
  - encrypt sections of the doc
    - each shareable unit in a doc requires a key to decrypt
    - maybe another key to sign edits
    - edits get rejected if not verified
    - not so good
- solutions above are not perfect
  - users have to got entire doc even if they only need subset
  - transclusion(嵌入、引用): include on doc inside another and changes update both
- solutions
- doc slicing
  - single doc
  - share a query result of data
  - cons: complex to impl privacy
- doc atomization
  - atomize a doc to pieces 
  - each shareable unit is its own doc/permissions
  - read checked on send
  - write checked on receive
- it's a database problem

- problem2: tiered(分层的) storage
  - each layer(ui > memory > disk > cloud) is a different view of the base data
  - views are expressed as queries
  - give devs power to explicitly hydrate and sync each layer

- challenges
  - auth
  - schema evolution
  - compute over data
  - consistency: causal, strong, cache-only
# changelog
- [v3.0.0_20230130](https://github.com/tinyplex/tinybase/releases/tag/v3.0.0)
  - adds key/value store functionality to TinyBase
# examples
- https://github.com/brentvatne/example-tinybase
  - I want to use it in React Native apps

- https://github.com/circadian-risk/tinybased
  - An experiment for an opinionated typesafe wrapper for TinyBase
# docs
- [Using Checkpoints | TinyBase](https://tinybase.org/guides/relationships-and-checkpoints/using-checkpoints/)
  - the checkpoints module gives you the ability to create and track changes to a Store's data for the purposes of undo and redo functionality
# discuss-news
- ## 

- ## 

- ## 

- ## v5 is going to be a big release. The whole idea is that TinyBase becomes a CRDT and you can merge stores together.
- https://twitter.com/tinybasejs/status/1769781789403300020
  - This will give us the native ability to synchronize data between clients or with a server.
  - It does this by adding an extended class `MergeableStore` , that carries with it the timestamps and hashes used to merge instances together cleanly.
  - Generally you’ll be able to just replace all your current Store instances with MergeableStore instances.
- 🧮 The CRDT magic comes from the use of a Hybrid Logical Clock mechanism that provides global sortable timestamps between clients. 
  - Then there’s a Merkel-like hashing that can identify which parts of two `MergeableStore` instances are out of sync.
  - These MergeableStore instances can be persisted locally as well as synchronized remotely. So for example you can keep data in localStorage while someone is offline and then merge with the server once they reconnect.

- We have three things to finish:
  - 1/ the sync protocol
  - 2/ documentation
  - 3/ templates and examples

- The sync protocol is for two (or more) MergeableStores to chat about what changes need to be sent over the wire.
  - The scaffolding for this is in place and hopefully the magic will hide behind the same `Persister` interface you know and love from TinyBase today.
# discuss-not-yet
- ## 

- ## 

- ## 

- ## Tinybase is a memory database, while my database may contains large amounts of data. 
- https://twitter.com/imsingee/status/1779267973666205937
  - Is it possible to instruct Tinybase to only read/write a part of  (partitioned by a column) the data of the electricsql db? 

- ['Pagination' for SQLite persistence ](https://github.com/tinyplex/tinybase/issues/143)
# discuss
- ## 

- ## 

- ## 

- ## 🧮 Merkle CRDTs look really interesting and I'm considering them for TinyBase. _20240203
- https://twitter.com/jamespearce/status/1753783959417155746
- My previous company built Noms and prolly trees. Replicache started out based on Noms, but we moved away from it. Neither are CRDTs, but closely-related. 

- I’m starting to like a rebase model over a crdt model 
- What is rebase model?
  - In the limit they’re equivalent. Rebasing would mean that you keep a mutation log and each peer is able to rebase new mutations into their logs such that everyone eventually processes all mutations in the same order.
- So linear history with some kind of ordering consistency once all peers have the same changes?
  - Yeah. I wrote a bit about how one might do this in SQLite
  - You could also have a non linear history if you can flag branches and version the database

- ## TinyBase v3 is going to have two demos to showcase CRDT synchronization.
- https://twitter.com/jamespearce/status/1608520684795465728
  - One will be P2P (over WebRTC), and one will be multi-party (via a central server). 
  - But even P2P requires a server to set up the signaling.

- I like using Replit for when I need a low usage multiplayer backend. Interested to hear about a good stateful simple deployment solution. 
  - Cloudflare workers for sure is a good option as evidenced by an increasing use of it for multiplayer backends.

- ## HLCs & CRDTs are easy! The harder part is shrinking them into tiny negotiable P2P payloads...
- https://twitter.com/jamespearce/status/1604304923247939584
- Each HLC entry is a 16 digit radix-64 string comprising 42 bits for time in ms, 24 bits for the counter, 30 bits for hash of unique client id. They're string-sortable.
- Every change that a database knows about (whether local or remote) is put into this Patricia-like trie.
  - Each HLC is split into four parts (3 + 4 + 4 + 5 chars) to address the nodes, and the leaf is the [table, row, cell, value] change.
  - `undefined` is a cell deletion.
- For shipping over the wire, the tree is encoded in three parts:
  1. an array of JSON-encoded table Ids, row Ids, cell Ids, and cell values.
  2. an array of radix-64 safe strings (which don't need quoting!) for the trie vertices.
  3. a tightly packed serialization of the tree.
- Because the tree's shape is well-known, this encodes and decodes pretty quickly.
  - It's quite easy to merge and diff these trees. So when a client makes a request to a peer for changes, it sends its own changes in the request. The peer's response is just then the new changes.
- Adding Merkel hashing to the tree would be slower but would allow the negotiation to bail out (or identify tree diffs) much sooner.
  - Or perhaps the tree could be progressively negotiated. 
  - (The trickiest thing might be version-controlling an evolving protocol!)
- Warning! This is all still in 'hacker space'. There's no concrete implementation in the TinyBase repo yet. But it might be worth rolling out an experimental branch soon. We'll see.
- You can use “pako” to compress and decompress your payload to make it smaller over the wire
  - https://github.com/excalidraw/excalidraw/blob/master/src/data/encode.ts
  - It would be interesting to compare pako running over flabby JSON vs running it over a pre-packed and pre-deduped encoding

- ## RFC! TinyBase HLC format. Needs to be small and fast for packing into binary tries & CRDTs
- https://twitter.com/jamespearce/status/1599796118014918658
- 11 byte(88 bits) bigint of
  - 42 bits, millis (~139 years)
  - 14 bits, counter (~16k)
  - 32 bits, hash of client id (~4 billion)
- You may want to consider using a `TypedArray` with `DataView` instead of `BigInt` to store the data if you really care about in memory size and layout. 
  - I wouldn't trust that bigint for such small sizes would not have a lot of additional memory overhead.
- Interesting. I was more worried about performance initially but that seems within 10% of Number (at least for the operations I need like shift, xor, gt, lt). I should check memory though - good point.
- Also I should mention I ideally need this as a key for a Map (or member of a Set).
  - You can use the index in the typedarray for key
  - Not sure I follow. If I have two HLCs coming from different systems with the same binary value, I'll want them to key the same value from a local map. (I'd need to convert to BigInt to do by value rather than differing reference, no?)
  - If it's coming from different system, just ignore me
  - Otherwise, whenever you generate a bigint key, you would use the index as reference going forward. But it may not be practical in many cases.
  - One thing I could do is use an array of two 53-bit or three 32-bit Numbers, and then have a map of maps (or map of map of maps)

- ## [CRDTs for tinybase_202209](https://github.com/tinyplex/tinybase/discussions/31)
- I've had to do a bunch of background reading. Still not sure of quite the right strategy yet... 
  - but in our favor we have the fact that TinyBase can listen and update on a cellular granularity, reducing the likely conflicts per row or table.

- We're close to releasing crdt support in SQLite itself
  - https://github.com/vlcn-io/cr-sqlite
  - If you just want some background, the original design is described in the readme. we've landed on something that doesn't require vector clocks recently, however
- [Do LWW Registers Need Vector Clocks or Causal Graphs?](https://tantaman.com/2022-10-18-lamport-sufficient-for-lww.html)
  - Short answer: No. When it comes to a LWW register, Lamport clocks offer all the guarantees we need. Guarantees provided by other clock types are discarded during the merge phase of LWW.
  - A last write wins register is a register where the "last" write always wins. Determining when a write happens is usually done via a logical clock. Lamport clocks, vector clocks and causal graphs are a few options here. 
  - 👉🏻 Lamport clocks being the simplest option.

- The current checkpoints module is an example of keeping a sequence of cell-level changes like that (and it handles deletes a charm). 
  - But I need to think about what a flexible API to get or replay such a log in a CRDT context would look like.
- I've started a dedicated disposable repo for these half-baked ideas. 
  - https://github.com/tinyplex/tinysync

- ## 🎯 [TinyBase v2.0: reactive data store for local-first apps | Hacker News_202209](https://news.ycombinator.com/item?id=32871392)
- what is a "reactive data store"?
  - By "reactive" I mean... if the data changes, the UI does (or at least, an event is fired, and then you can drive a React render, for example, from that). In contrast, you expect to have to poll an RDBMS for updates.
  - With "data store", rather than "database", I'll admit I am hedging my bets. Through one lens, this library can look more like an app-level store in a classic React sort of way. Through another (most notably the table/row/cell structure), it looks like an RDBMS. I'm not ready to go all-in and declare it's a database yet. Such nomenclature comes with Assumptions™.

- I was whining(抱怨, 嘀咕; 发牢骚) in the surrealdb thread for new advances in this space over couch/pouch (which we have been using for over a decade). Would be great to see comparisons, especially in areas where couch/pouch are bad and new solutions are better. 
  - We have not moved anywhere yet because couch/pouch, when you are used to it development wise, is automatic. You do nothing and it works. 
  - Other solutions we tried require way too much domain knowledge (which we have but don't want to think about when doing things we think should just automatically work, like synching; like replicache which is just too much work for us on our existing datasets) or are very hacky, as in, lose data and require you to write code to fix that.
- Interesting to hear that Couch/Pouch “just work”. I’ve been looking at using them and I find there’s a lot to wrap your head around. In particular for apps where different users should see different sets of shared records.
  - Yes, that’s correct, but we have been used to thinking that way for a decade. I don’t remember how painful it was in the first place, but once you think in that way, things fall in place.

- From what I can see in 2 mins of reading, it looks like it's more relational which should be a plus, 
  - but then on the downside there's much less of a story on the sync side, with remote persistence ending at offering you interfaces to persist your data but not an actual data store that works. By comparison, PouchDB connected to a server side CouchDB makes an amazing combo.
- I didn't have much trouble binding PouchDB into a Vue reactive data store so the reactive part didn't seem as novel to me. What does seem novel is supporting a proper relational schema for this, whereas all the other options I know in this space are schemaless / key-value type approaches.
- I wonder if it might be a high-value / low effort proposition to come up with an out-of-the-box setup with something like PostgREST that would then work end to end? This was the super compelling part for me with the Pouch/Couch combo, as with a couple of configs and barely any code your browser localStorage is suddenly sync'd and saved remotely in real time 
- I actually love it when people invent things without full knowledge of prior art - a lot of innovation happens only when people aren't biased by what is already there. Perhaps if you knew all about PouchDB you might not have had enough motivation to do this, and then this gap of a relational reactive store would not have been explored. What you have done looks really great!!!

- RxDB with PouchDB has support for typescript, json schema, and binary attachments. Moving the attachments to the file system will be up to you.

- I’m my limited experience, a reliable CRDT implementation necessitates a CRDT-first design baked into the core of any data / transaction model. Like I’ve heard some game developers say- multiplayer needs to come first because tacking it onto a single player game is a nightmare.

- 🤔 What are the gaps relative to something like PouchDB?
  - Honestly, just my personal confidence currently. There's very basic locking and store-wide read-write. I really aspire(渴望, 有志于) to some sort of CRDT implementation that can be considered a bit more state-of-the-art and tolerant to the innumerable challenges of that problem.
- I think that CRDT and OTs are a bit overkill for TinyBase. Most apps are not text editors or figma. Most apps are just forms. 
  - The general solution for forms is to track which fields on a record have been modified by the user. 
  - The user’s change is the source truth and never gets overwritten by the network. 
  - Other fields are free to be updated collaboratively from the network. Once the user has synced that field it is free to be updated by the network. 
  - This kind of solution can be built on top of TinyBase without CRDTs.

- The main limitation I see with tiny base is that it has to load all data in one batch and modifying any record results in the whole data store being persisted to disk. Surely this can’t scale well…
  - The data is in memory, and the persistence strategy is kind of up to you. So it would scale reasonably if you put the sync/persist on a different schedule to the UI - perhaps when the browser is idle.

- Wait so can you actually connect tiny base to SQLite?
  - No, there's no _actual_ RDBMS involved. The query engine uses a functional style of query that has similar concepts to SQL, but all the evaluation (and reactivity) is first party, in the library itself.
  - Of course it would be pretty easy/fun to persist your TinyBase content into a SQLite database, or pull a dataset from it

- is this web based, built on top of IndexedDB?
  - No, there are no dependencies. It has its own in-memory data structure, and ways to serialize it to other, more persistent, formats. I could imagine an option for more fully fledged RDBMSs being those persistence layers though.

- ## Here's an interesting browser state solution: A database, written in JS, called TinyBase._202202
- https://twitter.com/housecor/status/1492859757941637126
  - Tables, rows, cells, indexes, relationships, undo, and more. 
  - Persist the data to the browser, files, or a server.
- what sense makes database on client when you need to transfer the data? also all data is public by default
  - You can use it offline.
- Interesting for client-first apps!
  - I'm using Dexie.js on top of IndexedDB, but it has its limitations wrt/ queries (and performance).
  - Another crazy experiment on my list of things to try is @jlongster 's Absurd SQL
- I wonder if theres a world where you use absurdSQL (or raw SQLite wasm) as custom persistor with it? 
  - Currently persistence is just "where can you save and load a JSON string?" at a Store-wise level. So sure! 
  - But I once had an experiment for sharded persistence per table or row. 
  - At that point, keeping it in sync with a 'real' database might be quite scalable and interesting.

- ## 🚀 [TinyBase: A JavaScript library for structured state | Hacker News_202201](https://news.ycombinator.com/item?id=29945748)
- I used to use `redux-orm` which offered a similar promise. 
  - My app is still alive and kicking and I ended up implementing many of the ideas here myself, in a less reusable fashion. A primary motivator was that **as the use cases evolve, a storage model optimized for application specific access patterns becomes compelling**.
  - The convenience of having properly implemented relational semantics and performance enhancements of Indices is huge, but the risk of hitting assumptions that don't fit your use case is also non-trivial
- I agree with your very final point. The same might be true of the undo stack implementation too - at some point the usage patterns might invalidate some of my performance assumptions.
- I'd been using an early version of Redux-ORM on a project
  - We did eventually add a createEntityAdapter API to Redux Toolkit 

- Pro and Contro vs existing similar projects?
  - TinyBase lets you set up event handlers with arbitrary data granularity, making the data store reactive.

- The codebase is quite something. 
  - I thought the author had lost his mind, declaring dozens of new functions to simply wrap inbuilt functions and religiously not using classes. 
  - Then I realized it probably cuts the bundle size by 2/3rds to remove every "this.longBuiltinFnName()" and replace it with a minified function call.
- Quite possible. This was a journey
  - When I first started thinking about this project, classes still meant a bunch of transpilation overhead (which dates the origin story!). I persuaded myself that plain old objects with TypeScript interfaces would strike a better balance between performance, size, and developer experience.

- Web apps are so over-complicated because of piecemeal client side data stores and the need to sync with the latest fashion in api protocol.
  - Imagine how simple apps would be if your data model and query interface was exactly the same on the server and client. With automatic caching and fetching logic.
  - What we lack is a good client-side relational+graph database that has an identical server-side implementation.
- The requirements on clients are fundamentally different than on the server.
  1. Batching, to avoid network waterfalls (a consequence of network use being more expensive on clients than on the server).
  2. Data dependencies, so the framework knows how to stitch queries together when batching them.
  3. Consistency, so all UIs update when an update comes in (a consequence of SPAs being long-lived, as opposed to the typical stateless server request).
  - These all take some code/framework overhead. It’s valuable to pay that cost on clients, but is unnecessarily verbose for the server.
  - People have been trying to unify local and remote function calls for years, and it’s a similar problem: the two are fundamentally different.
- "code/framework overhead" is fine as long as its hidden in a library. Too many people re-implement a data layer client-side that is always a poor mapping to the server data model. My frontend should act as if its running off a local database and sync with the server. It could batch together all requests made to this database that it cannot fulfil or that are stale.

- SQLite on WASM is absolutely what you are looking for. There is also “Absurd SQL” which extends it to use indexedDB as a VFS for storage allowing proper atomic transactions and not loading the whole thing into memory.
- Absurd is really cool. I've always thought it would be great to have an SQL db implemented in native JS though.
  - With the database running in the same process as your app, you could store native JS Objects of your table rows in the cache, which you could bind events to. So if you modify a row in a table in the db, events could be instantly propagated to the UI. Haven't thought it through fully yet.
  - SQL is also a bit cumbersome for things like deeply nested data, hierarchies, trees, graphs which a lot of client-side application state ends up being.

- There's Datascript[0] and Datomic[1]. While not "identical", they are definitely complimentary. There's a (now defunct) library[2] for keeping them in sync too.

- PouchDB has offered something like that for close to a decade now, if I'm not mistaken. Might be worth looking into. 
  - It is **document-based, though, rather than relational+graph**, though I suppose you could build graph utilities on top of it.
- PouchDB is incredible, so much respect for the devs that built it. The trouble is though, it is now quite an ageing codebase with relatively little maintenance.
- rxdb is the best client side database. RxDB syncs with GraphQL and Pouch/CouchDBs.
  - There's WatermelonDB which uses IndexedDB on web and SQLite on native, it's nice for syncing to custom backends.
  - There's GUN and Orbit for distributed graph databases.
  - TinyBase looks really really nice, fills the gap in-between hefty client side databases and state system solutions like Redux + Persist. I'd like to see Redux middleware integration for time travel debugging, event lots, and snapshotting if possible. The analytics and rollback APIs are a nice touch. Size is enticing.

- Orbit.js does some of these things and coordinates client with a variety of data sources through a standard set of interfaces and using normalized data structures.
  - Orbit.js does some of these things and coordinates client with a variety of data sources through a standard set of interfaces and using normalized data structures.

- 
- 
- 
- 
- 
- 
- 
