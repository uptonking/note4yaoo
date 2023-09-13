---
title: lib-db-tupledb-dev
tags: [database, tupledb]
created: 2022-12-14T18:26:04.794Z
modified: 2022-12-14T18:26:38.588Z
---

# lib-db-tupledb-dev

# guide

- tuple-database /219Star/NALic/202209/ts
  - https://github.com/ccorcos/tuple-database
  - 依赖fs-extra, lodash, fractional-indexing
  - The architecture of this database draws inspiration from a bunch of different places (although, primarily from FoundationDb).
    - pretty much every database has similar abstractions under the hood — an ordered list (or tree) of tuples and binary search. 
    - This is why DynamoDb and FoundationDb can have frontend abstractions that are compatible with Postgres or MongoDb.
  - https://github.com/maccman/tuple-playground
# docs
- 👉🏻 The local-first, "end-user database" database.
  - When users own all of their data on their devices, it's a natural way of sharding a database and scaling up a platform.
  - As a constraint, this means that I'm interested in building an embedded database, like SQLite or LevelDb, that runs in process and is intended to be single tenant. 
- 👉🏻 All queries are reactive.
  - Polished applications these days require realtime reactivity.
  - And it's not just for collaboration — reactivity necessary when a user has multiple windows or tabs showing the same data.
  - Many systems have record-level or table-level reactivity, but I want all queries to be reactive. I'm tired of having to engineer custom solutions on top of databases with brittle logic where a developer might forget to emit an update event.
- 👉🏻 ✨ Schemaless — schemas are enforced by the application, not the database.
  - It took me some time to realize the the value of maintaining schemas in the application rather than the database. 
  - a schemaless database should be flexible enough to accept incoming data and allow the application to resolve conflicts or schema issues.
  - I want to build apps like Notion and Airtable where end-users define their own schemas. 
- 👉🏻 Asynchronous or Synchronous, Persisted or In-Memory Storage
  - I want to be able to persist data. And most persistence layers are asynchronous: LevelDb or even a cloud database. 
  - But even when persistence is synchronous, like SQLite, you might have to asynchronously cross a process boundary, such as an Electron window interacting with a database on the main process.
  - I want to use a synchronous in-memory database for frontend state management 
  - Works with synchronous and asynchronous storage including SQLite or LevelDb.
- Transactional read/writes written in TypeScript.
- 👉🏻 Directly read/write indexes with the ability to index graph/relational queries.
  - typical applications tend to ask a few unchanging queries many times. 
  - I want to bypass the query optimizer altogether to read and write directly to/from indexes.
  - he logic we've written here for the tuple-database code is exactly what any SQL database is doing under the hood.
- Suitable for frontend state management.

- https://github.com/ccorcos/game-counter
- A simple application for keeping score in games. For example, golf or Settlers of Catan.
- External effects interface through services defined on the Environment.
- TupleDatabase as a UI state management system.
# discuss
- ## 

- ## 

- ## [question: Is adding an rtree still on the roadmap?](https://github.com/ccorcos/tuple-database/issues/27)
- I have no immediate plans to implement this until I pick up a project that needs this
- My plan is more-or-less to consider the storage layer as key-value storage that isn't necessarily ordered. 
  - Then I'll build a durable tree on top of that abstraction. 
  - I've done some similar things before: ccorcos/js-avl-tree 
  - That project is different though because the tree persistent as well (an immutable data structure) inspired by datalog. 
  - But that seems a bit overkill and performance overhead doesn't seem worth it to me.

- ## My goal is to build a database that makes it easier to build local-first software._202206
- https://twitter.com/ccorcos/status/1532185301438738433
  - Embedded, reactive, schemaless, and transactional read/write directly to indexes (inspired by FoundationDb)
- SQLite is great, but it leaves much to be desired. It's mostly just a problem with SQL. 
  - Queries aren't reactive, no multi-valued columns, no indexes across tables for relational queries... All of these currently require bespoke solutions.
- I'm heavily invested in Offline First and have extensively used nanoSQL https://nanosql.io then and have now moved on to http://yjs.dev along with hocuspocus
  - For my client side store I've just switched to https://valtio.pmnd.rs + a modified version of https://github.com/Noitidart/valtio-persist to persist to IndexedDb
  - On the server I'm using MongoDb in an earlier app and RocksDb for the new app.
  - Before yjs I spent considerably time and effort with Logux https://logux.io but hit too many roadblocks.

- Super interesting! May I ask you what you think about the datascript/datomic approach? It does not offer persistence; I'm more particularly asking about the datoms, EAVT/AVET/etc systematic indexes, and it's datalog query engines.
  - The triplestore indexes are great. This database is a lower level abstraction, and I do in fact use datalog queries and EAV indexes most of the time I use this database(tupledb)
- As for general thoughts on Datomic…
  - You cannot construct your own indexes and paginate queries. For example, a contacts app might want to sort by last name, first name, creation time… Only way to do this in Datomic is to manually denormalize into a specific value.
  - It also isn’t exactly schemaless. Attributes are defined with :symbols which are statically defined and held memory. That means “new column” in an Airtable-like application can’t just generate a new UUID for an attribute…
  - The whole time travel thing with the T in EAVT is neat. And it’s useful from a UX perspective to inquire about “when did I change this phone number” etc. But I don’t imagine wanting to query the state of the database in the past…
  - At the end of the day Datomic is awesome. But it is designed for big enterprise consulting workloads (Rich Hickeys day job) and not end-user databases (like Notion, Airtable, Coda, etc) or Local-first software (embedded, smaller amounts of data)…

- Very cool. I've been attacking the same problem from the opposite direction -- a local first & language agnostic ORM(vlcn-orm)
  - Maybe there's some opportunities here. E.g., adding tuple-databases as a backend to Aphrodite for a simpler dx.
  - schemas in the application rather than the database

- I had started down this direction until I realized that I’m basically creating another programming language all over again… For example, a complex query like “get me all scores that are more than twice the lowest score” is hard to represent without a proper programming language.
  - I'm going about it by (1) putting the schema definition language into a DSL but (2) generating the query builders in the target languages (swift/kotlin/typescript/..). Seems to sidestep this problem.
- this is fine to express in SQL with subqueries; if the DSL supports subqueries it's okay.
  - Then you want to hoist subqueries as functions so you can reuse and compose them... Building a DSL is not a "wrong" approach. I just remember in my early programming days getting really frustrated with HTML templating engines because I just wanted a proper programming language.
- I noticed the same thing w.r.t. "reuse and compose subqueries" — that's essentially what the macros in my query language are
- I wonder if we're talking past one another. The query builder is a native api and inspired by https://entgo.io/docs/traversals. During ~8 years of using (and supporting users of) the internal version @Meta , I hit very few walls in terms of unsupported query patterns.
- https://github.com/obi1kenobi/trustfall /rust
  - A query engine for any combination of data sources.
  - databases, APIs, file systems, anything else you can think of + any combination of them.

- Interesting. Are you familiar with Datalog-style queries? 
  - Seems pretty similar, except the edges are traversed recursively without having to define methods to traverse school edge. 
  - SPARQL and Datomic are good examples. And I made a demo too
- This article specifically helped me get started understanding things...
  - Just remember that Datomic also allows you to query into the past so that's why `tx` lands in their indexes.
  - [Indexes | Datomic](https://docs.datomic.com/pro/query/indexes.html)

- ## Where is perspective discussed in software design?
- https://twitter.com/ccorcos/status/1622664703536435201
  - If a chair is always a thing for sitting in, strict schemas and bundling behavior with data makes sense.
  - If perspective matters and a chair changes from a door stop to ram to a thing to sit in, you need something else.
- Lol, I was just about to reply “triplestore!” but looks like you’re already there!
- A similar idea exist in game development called “entity-component system”. 
  - The idea is that the developer often cares about attributes of object as opposed to knowing what kind of object it is. 
  - “This this thing openable? If so, open it”. Doesn’t matter if it’s a door or a chest
  - 偏向于抽象通用性为的接口，而不是定义schema

- ## [Couple of questions](https://github.com/ccorcos/tuple-database/issues/15)
- If I were to query something that returned a bunch of userIds, whats the best way to query users from those userIds? I could scan 1 by 1 but I feel like there would be a better way. 
  - You can basically order the keys and keep track of a min/max for the entire set when doing binary search...
  - I think there's a more efficient way of doing this by getting the first element, and then the last element, and then the items in between... Then you don't need to check and update the batchMax a bunch of times like you do in this implementation...

- If I were to build Notion all over again (I was the first employee), then I would definitely use FoundationDb, but that's just because Notion is a SaaS product. If you're building a local-first app, I would use this library -- its basically an embedded version of FoundationDb with reactivity...

- In my code I've only been using synchronous updates. I like that store get/set are sync, and I can just persist the entire set of changes to an API completely separately in some debounced function after a few seconds or so. So it only fetches from storage when the app first starts. 
  - Yeah, its nice to use sync when building an app, but permanent storage is almost always async. Also, its not great if you have to load all your data in memory at once when you start the app... That approach definitely works for now, but once you end up with collaboration and syncing, this breaks down.
- My plan is keep track of transactions in an append-only log (just an index like `[deviceId, int, WriteOps])` and then when you want to sync between devices, you basically need to sync these logs to each other and resolve the writes.
- syncing abstraction is a different layer.
- you can transactionally read-write to an async database. So if you want write to another remote database, just create a transaction. But if your goal is to sync a local database with a remote one, then transactions are certainly tricky...

- ## [Some questions about tuple-database implementation and design](https://github.com/ccorcos/tuple-database/issues/13)
- For each field that I need to query, I must create an index, right?
  - Sort of. I would say you want to have an index for every query. Translating from a SQL perspective, its more like "an index is a query". 
  - SQL has a query planner which will intelligently figure out what indexes to use. 
  - Tuple Database doesn't have a query planner -- you, the developer, are the query planner. So you can construct indexes and choose how to fetch whatever information you want...

- 👉🏻 Also, indexes become expensive it terms of disk usage at some point, how are you going to deal with it? Or it is by-design
  - That's the case with SQL as well though. When I was at Notion, we had maybe 30 tables and 60-90 indexes. 
  - So in addition to primary keys, you're looking at about 2-3x the amount of data storage. Granted these aren't all full covering indexes...
  - But my point is that, underneath SQL is a system very similar to tuple-database. 
  - SQL isn't magic -- it's going all this same stuff, writing data multiple times in different places, etc. 
  - And so the disk usage problem is the same as any other database. 
  - Only difference is that I haven't implemented any compression or anything like that yet.
  - But storage is cheap - I'm not worried about it yet.

- So my point there is that I can build a SQL layer on top of tuple-database, but why would I do that? I could make my own query language DSL, but why do that either? I find it much more powerful and flexible to use the underlying abstractions directly...
  - 👉🏻 That said, I am keen on using this database(tupledb) to model triplestores. 
  - Similar to RDF/Datomic/Datalog, triple stores are a powerful abstraction for modeling very flexible data.
  - And do I have built up some abstractions on top of this model. But notice those abstractions are all just functions for reading and writing...
  - https://github.com/ccorcos/tuple-database/blob/master/src/examples/triplestore.ts

- don't you think to write the core in Rust? 
  - Totally. I'd love to hire someone to do that. But it's not my main skillset and at the end of the day, this is premature optimization
  - it's fast enough
  - There's also all kinds of weird issues like "can I store a function callback as a value?" Right now you can, because its all JavaScript. Also the interop overhead -- right now all numbers are float64 and that's pretty simple and convenient. In SQLite, all numbers come out as strings!
- if you need, I may give you some advices how it could be done with wasm.
  - I'd love some help! In particular a plaintext (ideally) flat-file storage engine would be great. Since all of the transactional guarantees are outside of the storage engine, it can be implemented fairly simply. 
  - I also really want to implement a Generalized Search Tree (GiST) so that we can support spatial queries. 
  - In particular segment trees would be really useful for reactivity performance and interval trees can be used for date range queries
- There are reasons why async SQLite is not a great idea. SQLite is serialized and synchronous. And so an async api doesn't gain you much. 
- 👉🏻 Optimize last! That's the biggest lesson

- Why do you need async SQLite with an IDB backend??
  - 👉🏻 I was needed in DB that will be fast and not in-memory. I used Dexie before (wrapper around IDB), but it had performance bottleneck by IDB itself — which is slow. And it's crashes/has unexpected behavior very often.
  - I managed to use absurd-sql, and I took x3-x5 performance gain for the same queries! 
  - Reading blocks(ArrayBuffer) from IDB and consuming it by sqlite has much better performance, then just storing business data in IDB itself.
- But absurd-sql has one downside
  - you need to use COOP header that restricts usage of embedded iframe from the other sources (like youtube videos). 
  - But I need the ability to embed iframe in the app. 
  - That's why I'm building asyncify version and trying to achieve the same performance as absurd-sql has.
  - [Making your website "cross-origin isolated" using COOP and COEP](https://web.dev/i18n/en/coop-coep/)
  - Use COOP and COEP to set up a cross-origin isolated environment and enable powerful features like SharedArrayBuffer, performance.measureUserAgentSpecificMemory() and high resolution timer with better precision.
- And, actually, if you need good performance on web with persistency — don't rely on abstractions of IDB. 
  - It's better to build your custom binary format to store data in blocks (like SQLite do).
- we expect that our DB will be growing fast (we are building a note-taking app), and for the note-taking app it's critical to have a fast startup time — that's why in-memory db is not the case
- absurd-sql performance is achieved by raw blocks reading/writing and abstraction over it (abstraction means how SQLite (for ex) store data in those blocks), which is faster than IDB rows getting/putting (which is absurd!).
  - And the good thing, if you will bring this low-level abstraction, you will also can easily port to NodeJS and writing to actual file, not IndexedDB (for ex) block by block.

- Interesting. So it all comes down to avoiding IDB's transactional read/write logic...

- ## [Maybe some misunderstanding of how SQL DB indexes work?](https://github.com/ccorcos/tuple-database/issues/11)
- What you need is an index like `(tag, age, id)` , but there are two challenges: tag and age are in different tables, and a user may have many tags... 
  - You can build this index yourself but you'll have to manage all insertions and deletions yourself... (you can probably use a SQL trigger actually)
- In any case, the tuple-database makes all of this much easier:
  - Write to the index: `tx.set([tag, age, id], null)` ; 
  - Read the index: `tx.scan({prefix: ["engineer"], limit: 10})`
