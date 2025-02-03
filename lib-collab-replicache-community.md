---
title: lib-collab-replicache-community
tags: [collaboration, community, crdt, replicache]
created: 2024-01-07T05:08:43.395Z
modified: 2024-01-07T05:09:14.413Z
---

# lib-collab-replicache-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-author(aboodman)
- ## 

- ## I think it is so interesting how many of the people building sync engines came to it through *UI* development.
- https://x.com/aboodman/status/1871237826333032715
  - You would not naively expect these people to be working on distributed systems. But for all, it was the same thing – we wanted to create better UIs.
  - Over time, we all narrowed in on the same thing: that the traditional way of building software around request/response APIs was the core thing preventing better UX, and the thing that needed to change.
  - Five years ago I started @rocicorp and recruited a team. We made our first sync engine @replicache . Two years agod we built our first attempt at a sync backend @hello_reflect .
  - It was too narrow, so we scrapped it and started @rocicorp_zero - a novel syncing distributed database.
  - It has been a lot of work, and all in pursuit of the same thing – fast clicks. The clicks must be fast.

- And the results are stunning, no doubt. I was wondering how well does it work with existing postgres deployments that use RLS and native ROLES heavily for security?
  - It doesn't. You'll need to port those RLS rules to Zero permissions
  - This is required because Zero has its own streaming query engine to support continuously syncing the results of queries to clients. So we can't make use of PG's query system

- Definitely. My take is that react and these new FRP paradigms actually made the backends and req/resp protocol models feel quite antiquated. the apps suddenly had a more ambitious and useful model for state.

- ## 🔁🆚️🤔 Here is how I think about the local-first/sync space. _20241007
- https://x.com/aboodman/status/184 3041337794576810
- 1️⃣ The first dimension to consider is document vs database sync. 
  - Things like @liveblocks , yjs, Reflect are what I would call 'multiplayer' and things like @replicache , @powersync_ , @ElectricSQL , @instant_db , @triplit_dev and @convex_dev are database sync.
  - The difference is a matter of technical architecture and scale. 
  - The document sync systems are intended for syncing a single document. They are often much faster and run in memory on the server to facilitate super high-rate (mousemovement, 60fps) sync.
  - The database sync engines are not backed by databases not memory, so they are inherently slower. But they can sync a lot more data and are more appropriate for syncing your entire application state not just one document.

- 2️⃣ The second dimension to consider is server-authority vs what I will call "decentralized" here.
  - Examples of server-authority systems are replicache, zero, powersync, electric, convex, instant, triplit, even firebase ...
  - Examples of decentralized systems are yjs, automerge, @jazz_tools , @dittolive , @evoluhq ...
  - The difference is again a matter of technical architecture that affects what is possible to build. 
  - Server authority systems have a central server that all changes go through. This is exactly the same as how basically ~all modern software everyone uses today is built, so it's a lot easier to adopt by industry.
  - In server authoritative systems it's easy to implement authorization -- only certain users can read or write certain data -- because there is a central server that makes those decisions. There is interesting work being done on auth in decentralized systems but it's a lost more explorative IMO.
  - On the other hand the decentralized systems have the advantage that they don't need a central server to sync. One fascinating example is Ditto. 
  - I have also personally recommended things like yjs to people that contacted me from the defense industry. On the battlefield you can't rely on access to the central server so decentralized systems work better.

- 3️⃣ the third dimension is sync engine vs syncing datastore.
  - A syncing datastore is a backend datastore (that also syncs). It takes the place of postgres/mysql/whatever in your stack, and also takes the place of APIs. They *are* the system of record.
  - Examples of datastores are instant, triplit, convex, firebase, liveblocks ...
  - A sync engine is only a data transport layer. It takes the place of GraphQL/REST APIs, but not the place of the database.
  - Examples of sync engines are powersync, electric, replicache, zero, yjs, automerge, jazz tools .... and I guess I might put @tinybasejs in this category too?
  - The difference here is ease of use vs flexibility. The syncing datastores are tightly integrated systems that generally are very easy (almost trivial) to setup. But the downside is that they are their own universes. Hard to integrate with the rest of the tools from the software world.
  - If your sync engine is backed by standard pg, then customers can use it alongside anything that talks to pg. They can easily swap you out for some other sync engine. They can also swap out pg and use a different database.

- 📌 Other important attributes are:
  - partial sync
  - optimistic reads (do reads go to the local device first, or always to cloud)
  - optimistic writes
  - consistency (what invariants about what data clients can see does the system guarantee)

- Fluid is:
  - document sync (no queries, very fast, in-memory, primarily designed for syncing a document not a database)
  - server-authoritative (although the core model is crdt-inspired, there is an authoritative order to all writes)
  - syncing datastore (fluid *is* your backend)
  - has optimistic reads and writes built in, ubiquitously
  - strong consistency
  - no partial sync
- The document sync systems are almost always optimistic read/write, strong consistency, no partial sync. These three questions only come into play when you're syncing a lot more data.

- isn’t Liveblocks more of a sync engine than a datastore? Under the hood it’s either Yjs or Liveblocks Storage (which is similar to Yjs) and you still need to persist data to a database yourself via webhooks. As far as I know, Liveblocks room storage isn’t durable.
  - It is durable. In fact it’s in cf durable objects.
  - Data is persisted in @liveblocks . Our "Realtime APIs" product offer a data store that supports two sync engines: Yjs and Liveblocks Storage.

- I wonder if you'll touch on an important distinction between things like Convex and things like Firebase, Instant, Triplit, etc.
  - Convex syncs the results of query functions down to the client it's syncing to, rather than entities themselves. All mutations are queued and actually executed on the server database, enabling Convex to achieve the strongest possible transactional guarantees on the server. Also this allows for more flexibility around authorization rules.
  - So, Convex is a bit more "online-oriented " today and not truly a local-first solution (yet!). I'm looking forward to Zero and a possible integration in the future
  - This stands in contrast to Firebase, Instant, and Triplit, where every client has full access to the database locally by default. Depending on the product being built, these might be totally reasonable tradeoffs.

- Both Instant and Triplit have permissions, so it's not the case that all clients have access to entire db by default (unless I'm misunderstanding something about what you mean?).
  - Yep! Permissions and partial sync means a client/users only has the data that they're both allowed to see and have queried

- I wrote up some similar thoughts we have on the sync landscape in https://stack.convex.dev/a-map-of-sync 
  - it's *nine* dimensions instead of three (phew), and they're shifted around a bit, but I'm curious what y'all think.
- 比较了linear/dropbox/figma/replicache/automerge/valorant
  - 维度9个: Size, Update Rate, unStructured, Input latency, Offline, Concurrent clients, Centralization, Flexibility-sync-rules, Consistency

- ## Story time... We started Replicache in 2019 and slowly built a niche but passionate community – including @thdxr . _20250123
- https://x.com/aboodman/status/1882323407943123369
  - Replicache is one of the most popular sync engines today. People love how it makes their app respond absolutely instantly (< 1ms) to clicks, and the automatic full-stack reactivity that comes for free. 
  - People also love that Replicache works with existing standard databases like Postgres, and supports partial sync, authorization, and custom server-side code.
  - But Replicache has an achilles heel: It's quite difficult to setup, requiring a lot of fairly intricate server-side code. Worse, the complexity of this code scales very poorly as the app's needs grow more complex.
  - So we started a project called Reflect in 2023. It was a short-lived, fully hosted version of Replicache with a very narrow focus on just single-document high-framerate sync, suitable for things like Figma. It didn't do most of the things that people used Replicache for, but the idea was to do one of them very very well. One day in our channel, @cezar asked "could you get dax to use it?". And I think that was the precise moment Reflect died. What good was it if didn't work for our most passionate existing users?
  - So we scrapped it and started over. Work began on @rocicorp_zero right around Jan 1, 2024. We designed it from the beginning to (a) make Replicache dramatically easier to setup so many more people could use it, and (b) to grow much better as the needs of the app grew.
  - To do so, we had to solve some hairy problems. In particular we built a new streaming query engine that applies ideas from @felderainc and @readysetio to efficiently sync arbitrary queries to the client.
  - We have a ways to go yet, and I'll write more about Zero as we get closer to beta. But it's incredibly gratifying to see this one particular customer make the leap.

- Does it currently only work exclusively on postgres?
  - Yes, only pg for now.

- do you have a pricing model in mind for Zero yet?
  - We imagine that it will be free/oss to self-host. We'll have a SaaS version roughly comparable to what you might pay for database hosting. And we'll offer white-glove help to large enterprises to run Zero within their own VPC.
# discuss-news
- ## 

- ## 

- ## The Zero server was designed from the beginning for horizontal scalability
- https://x.com/aboodman/status/1885496692293984734

- ## AFAIK Zero is the first sync engine based on IVM, and maybe the first application of IVM in UI?
- https://x.com/aboodman/status/1869840603753918701
  - Why are we doing this crazy thing? I think that it is inevitable if you want to build generally useful sync engines.
  - I tried waiting for years for somebody to do this as a library we could reuse, but nobody did so I nerdsniped @tantaman into researching it and he prototyped it in https://github.com/vlcn-io/materialite. Then we ended up hiring him and rebuilding it together from the ground up for Zero.

- Triplit's been doing it since the beginning! And in a sense IVM is basically how all modern web frameworks work when they're updating the DOM

- How would you compare it to Meteor publications and DDP? The engine that implements an SFU there being the mergebox algo, on top of MongoDB oplog/change streams

- ## The most annoying problem for Zero's launch was what bug tracker to use. _20241219
- https://x.com/aboodman/status/1869448123942347128
  - GitHub is way too slow, and Linear doesn't have public bugs or permissions – both required for OSS projects.
  - Yeah, we built a bug tracker. A bug tracker that has *instant* (zero millisecond) UI transitions, live updates, and fine-grained permissions.
  - The *problem* with sync engines, historically, has been that they only work for a narrow class of apps. As soon as you get more data than you'd want to sync to the client, need fast startup, or need fine-grained permissions, they start to fall apart.
  - Today, we're making Zero available for the first time in alpha.
  - It's open source: We plan to offer zero-cache as a service and also help larger businesses run zero-cache on-prem.

- What i don't get is how i would intercept mutations on a server. Let's say i want to have a server part that has to do stuff if resource x is mutated, like sending an email or what not? I only see the frontend talking directly to the zero-cache..
  - we're adding that next

- Is it using indexedDB to store data locally ? Is the local storage limit configurable ?
  - It uses idb yea, or sqlite on mobile.

- What are the longer term plans for replicache now that zero is live? I suspect the bring your own backend approach might still be quite attractive for folks migrating existing apps to local first far into the future. 
  - For me personally, I really liked the idea of replicache over most other local-first solutions specifically because of the flexibility of the protocol based approach that allowed me to use any tech stack/db and in theory freely migrate to different ones in the future
- Zero only supports Postgres *currently* but there is nothing important preventing it from working with most databases. 
  - Powersync and Materialized use the same WAL-tailing technique and they work with many databases.
  - In a sense Zero is *more* compatible than Replicache because it has fewer dependencies on upstream. All it really needs is a commit log. 

- Any ideas how AWS's new DSQL will fare in terms of overall compat and the event trigger thing? I suspect not well since it's not actual postgres.
  - I'll have to wait and see how DSQL shapes out when it's public. I suspect it won't even have any replication log at all at launch but that it will quickly be added since it's such a common thing for databases to need to have.

- In your http://fly.io example for zero-cache it's using 2gb of memory. Is that the minimum recommended or can we make do with less for smaller DBs?
  - I'm not sure why we chose this number. zero-cache is actually pretty lean on memory as it keep most of its working state on SSD. The minimum will depend on your workload.

- I'm also curious what exactly makes the current version "single-node". What's preventing us from deploying multiple instances and load balance between them? Are the nodes not stateless? Do they need to coordinate between each other somehow? Do clients need to stick to 1 mode for the entire session? Or something else entirely?
  - The nodes are definitely not stateless. They maintain replicas on SSD of the upstream database to do efficient sync (any sync engine works this way). 
  - We run zero-cache today with 5 nodes for zbugs, so nothing is preventing you from doing this other than that we haven't documented how to do so. A multinode deployment of zero-cache has one leader node that recies the wal from pg and n followers that serve as endpoints for clients. Coordination is needed when an update happens to smoothly drain clients, avoid thundering herd, ensure only one node is using exclusive resources (like the pg replication slot), etc. Standard stuff. 
  - It all aready works and is being used on zbugs, we just don't like saying stuff is done until it has been documented, tested, APIs cleaned up, etc.
  - if you try and just run multiple copies of zero-cache w/o any changes from instructions all but one will error out saying that the pg replication slot is in use. To do it correctly you need to configure one as the leader and the others as followers.

- ## 🚀🆚️ [Day Zero – Build Good Web Apps with the Zero Sync Engine | Hacker News _20241218](https://news.ycombinator.com/item?id=42453431)
- Will replicache be deprecated? 
  - We'll continue supporting Replicache but won't add new features to it.
  - Even if you don't think you'll need partial sync, our experience is that almost all projects end up needing either it or permissions. Both of which are difficult with Replicache.
  - And if you don't need either of those, the the query-based programming model of Zero is just a lot more fun.

- your closest competitor and most similar in design is InstantDB
  - while both InstantDB and Zero use PostgreSQL as a backend (and add a subscription mechanism in front), the former uses it as a triple store (more similar in practice to something like Triplit), meaning the data is not available in a format comprehensible to other clients, so it is merely an implementation detail. 
  - Zero however allows the database to be accessed simultaneously in other manners, promoting compatibility and reducing lock-in
- Instant is a full database, including the backend. 
  - Zero is not - it connects to some separate authoritative backend db. Currently only Postgres is supported, but our intent is to support other DBs like MySQL, Mongo, Cockroach, and in the fullness of time even custom distributed systems. 
- Instant uses a datalog/triple style data model and a custom query system. 
  - Zero's data model is just relational data, and it uses a SQL-style query system. 
  - In practice the API that instant exposes is very relational-like, but I still think that if you know SQL already there's less to learn with Zero.
- Zero is based on Incremental View Maintenance. 
  - When data that affects a Zero query changes, Zero does only a small amount of work to reflect the change. 
  - To my knowledge, Instant doesn't do this and re-runs the query (correct me if I'm wrong here Instant folks). This was a specific design choice in Zero because ...
- Zero was designed primarily to support 'the linear use case': storing dozens of MB of data client-side and keeping it up to date with permissions and partial sync. 
  - We did not want to have to run these huge queries over and over.
- Zero is very focused on just being a sync engine. 
  - Instant appears to be aiming to take on more of the suite of features Firebase offers like login, email, blob storage, etc.

- zero-cache uses SQLite internally, but the component that’s missing for SQLite support overall is a replication log that zero-cache can subscribe to.

- Zero's "BYODB" approach has some advantages:
  * You don't have to trust us to build a correct backend database (nothing Zero can do can corrupt your data - it's just a fancy cache)
  * If you end up not liking Zero you can easily move to anything else that can run on top of PG.
  * You can adopt Zero incrementally in an existing project by just moving features over to Zero one-by-one.
  * Any code, library, or project that works with PG likely already works with Zero.
  * Zero can coexist with other types of PG users. If some non-Zero client changes PG, Zero clients will see it update live. If Zero clients change PG, other clients will see it when they next read PG.
  * You don't have to wait for us to build features. Admin UI? Use any of the great PG ones. Data export? It's just PG. Backups? Triggers? FKs? Constraints? Schemas? Migrations? Use all the normal PG stuff.
- On the flip side this is a more complicated way to build the system and some of that complexity does leak out into Zero's DX. We're trying to minimize it as best we can, but Zero can probably never be quite as 'sleek' an experience as Instant.

- 
- 
- 
- 
- 
- 
- 
- 

- ## Just got off stage* at @localfirstconf where I shared Zero: https://zerosync.dev
- https://x.com/aboodman/status/1796238294017085593
  - Zero introduces "hybrid queries" – queries that start locally and fall back to the server automatically – to make sync genuinely easy, and scalable enough to handle all kinds of apps.

- I noticed that it says "Reflect will be open sourced...once Zero is ready, we will encourage users to move." Does this mean that Zero is providing the same transactional conflict resolution under the hood?
  - Yeah it does. We have built-in crud mutators because they are so common but we will still support Replicache-style custom mutators for more interesting cases.

- Interesting approach. Thoughts on CouchDB (comes to mind as the pillar database that sync)? I've used it quite extensively with @PouchDB to sync data to devices and works quite nicely. How's Zero different?
  - Zero is not a database. It's a cache that sits in front of a standard relational database like Postgres. No need to adopt a new DB.
  - Zero's hybrid search enables a really intuitive way to partially replicate for perf, then fall back to the server when necessary.
  - This is dramatically more difficult to implement than Replicache. We were scared.

- How does this compare to @ElectricSQL ?
  - Hybrid Queries: Rather than having to tell the system what to sync with shapes (or sync rules as in @powersync_ ) we plan to imply what to sync based on queries. We will keep a 100MB persistent client-side cache and manage it automatically. Queries bridge to the server automatically when necessary. We expect this to be a really nice DX but it also enables things like: (a) searching over a dataset that can't be entirely synced to the client, (b) ~instant startup without having to sync a large amount of data, (c) server-side rendering
  - Not SQLite. Sort of uniquely among the local-first solutions, we use our own custom data layer rather than SQLite. This has pros and cons. Of course SQLite is super flexible and has a huge amount of engineering invested. But given hybrid queries, we don't need (or even want) to store a huge amt of data client-side. We're just storing 100MB. SQLite is designed for far, far, more. Something more purpose-built has advantages: we can run it on the main-thread in memory so it's always instantaneous. We can also build reactivity into it from the ground up which is hard to retrofit into existing applications. We think this enables a different programming model centered on super fine-grained reactivity.
  - custom mutators. I always forget that one. Zero is going to have support for Replicache-style transactional/server-authoritative mutators. Electric advocates a "client-side mutations are final" approach that is more CRDT-style.

- Solid is both a view layer and state management. local-first is an alternative to state management and APIs.  

- 
- 
- 

- https://x.com/matthew_linkous/status/1796548406514761924
  - I want this to work but I’m skeptical, because it’s not a new idea. Every time people get excited but it fails to catch on.
  1. Original Meteor.js was this but with Mongo instead of SQL
  2. There is pouchDB that syncs with couchDB
  - Will this time be different?
- This time is different. PouchDB + CouchDB was bad for collaboration because you would end up with conflicted documents constantly. Plus there was no support for relational querying and no hosted service . @triplit_dev on the other hand has all of that plus great TS support
  - It's already a success in many companies like Linear, Whatsapp, FB Messenger, Superhuman, Google Maps, etc. This is just the beginning of out-of-the-box solutions being good enough
# discuss
- ## 

- ## 

- ## Replicache is closer to a db than you’d think. 
- https://twitter.com/aboodman/status/1743829055827546152
  - We built on what we learned from https://github.com/attic-labs/noms and built Replicache on an immutable b tree. 
  - So technically it’s a fast key value store, which is the basis for many popular dbs.
  - This is also why Replicache is so fast while being backed by idb. 
  - We don’t use idb as a kv store itself. It only stores pages of our custom b tree.

- SQLite is unfortunately too slow in the browser to be used as a reactive database.

- ## 🕹️✨ @hello_reflect is the only multiplayer system that supports database-style interactive transactions.
- https://twitter.com/aboodman/status/1732484354637709507
  - People sometimes ask if they really need that though. Aren't CRDTs or json-patch enough?
  - With a CRDT like Yjs, you could have each row be a map entry. The same approach could work with JSON-patch bases systems.
  - When we were playing with early versions of this demo, I wanted to see a version where you could pick multiple cells (so that you could "draw" songs. But this doesn't work with the data model above, you'd need a different schema where each cell can be selected
  - Note the problem here: With a map CRDT we need an entirely different schema if we change our business logic even slightly. The schema that works for selecting only one cell per row does not work for selecting multiple cells. And vice versa!
- This isn't a problem in Reflect. We start out with a nice flexible schema, a map of enabled cells.
  - We can even choose at runtime with a flag.
  - All easy to implement on this basic schema in Reflect using transactions, but difficult or impossible with other systems.
- So while you can do some things without transactions, when your project gets even a little interesting, you invariably need custom business logic. Where does that logic go? It can't go on the client, for the same reasons we can never rely solely on client-side validation.
  - But it also can't go on the client because there are multiple clients running. A rule like "only one cell in this row can be selected" can't be implemented client-side – two clients could decide they got the only slot at the same time.
  - 💡 Reflect's Transactional Conflict Resolution gives you an elegant way to implement any kind of custom business logic. Your mutators run twice – once on the client, optimistically, for responsiveness, but then again on the server to compute the authoritative result.

- In an op-based CRDT, you can only send the discrete set of ops that are built into that CRDT. In TCR, you can implement any op you want using JavaScript. The core idea of linearization on an authoritative server is a pretty good general purpose sync system.
  - The reason this generalization isn't possible in general in op-based CRDTs is that the system must converge.
  - This implies that the ops on all clients must be (a) pure and (b) identical. But how could this be guaranteed in common programming environments?
  - It can be done in specialized systems. @tanglesync is a very cool exploration of this idea using a rewindable wasm sandbox.
  - @tantaman has also explored this here: https://vlcn.io/blog/crdt-substrate
  - Another challenge with doing this as a pure CRDT is of course finalization. You can never know when the effect of an op is final because some earlier op can always be received.
- I don't really see it as that similar to an op-based CRDT but I guess that's dependent on your point of reference! Other people say "isn't this similar to OT?". And I guess all of these are ideas are not that far apart in the big picture. But the details are why we give things different names
  - The ability to provide your own mutators is a massive different in usability, making it feel like a completely different thing from a crdt from a dx pov.

- ## We are studying @replicache 's awesome blog post at @taktile_org 's internal reading group. We built a somewhat similar linearized serverside reconciliation algorithm. 
- https://twitter.com/tomlarkworthy/status/1727986810238697837
  - Main diff is we send JSON-merge-PATCHes not mutator calls.
  - JSON-merge-patch is the RESTful dual of operational based sync. 
  - Main drawback is it does not work with arrays or nulls and its not as expressive as arbitrary functions, but it has some nice composability when you want a change log or combine writes

- ## 🚀👥 [Reflect – Multiplayer web app framework with game-style synchronization | Hacker News_202310](https://news.ycombinator.com/item?id=37931373)
- Reflect adds a fully managed, incredibly fast sync server.
  - One plus point compared to CRDTs is that you get to decide how you want to deal with conflicts yourself, with simple, sequential code. I'm not up to date with the latest in CRDT-land but I believe it can be complicated to add application specific conflict resolution if the built-in rules don't fit your needs.
- I agree wholeheartedly — we took the same approach for PowerSync with a server reconciliation architecture over CRDTs, which is also mentioned elsewhere in the comments here. For applications that have a central server, I think the simplicity of this kind of architecture is very appealing.

- Congrats! I've been watching this space for a while, having built a couple multiplayer sync systems in the past in private codebases, including a "redux-pubsub" library with rebasing and server canonicity that is (IIUC?) TCR-like. There's a lot to like about this model, and I find the linked article quite clear - thank you for writing and releasing this!
  - Do you have a recommendation for use-cases that involve substantial shared text editing in a TCR system? I'd usually default to Yjs and Tiptap/Prosemirror here (and am watching Automerge Prosemirror with interest). The best idea I've come up with is running two data stores in parallel: a CRDT doc that is a flat key/value identifying a set of text docs keyed by UUID, and a TCR doc representing the data, which occasionally mentions CRDT text UUIDs.
- What does this mean for Replicache development, is the client-side codebase mostly shared and can expect continued updates, or more likely to replace the primary focus for you?
  - The clients are almost entirely shared. We will continue to develop Replicache.
- What is the maximum number of users that can be concurrently in a room?
  - There's no max enforced. Right now, it will fall apart pretty quick around 25-50, depending on how much work is going on. For the GA, we plan to implement a scheme that will allow the room to support up to ~100 concurrent active users (actually doing things) and thousands just watching.

- 🆚️ Curious what your thoughts are on ElectricSQL?
  - It seems really interesting. The key thing to understand is that there are deep architectural choices made in each of these systems that really influence what you can do. There is "mechanical sympathy" with certain kinds of applications.
  - ElectricSQL is a distributed database. It's not going to run anywhere near 60fps with tons of users, because it's not running in memory on the server like Reflect/PartyKit/Liveblocks do. OTOH it will allow you to filter/query interact with much more data at the same time than Reflect/PartyKit/Liveblocks do – Reflect has a limit currently of 50MB per room and it's not practical to have dozens of rooms open at one time to get around this.
  - Systems in the Reflect room/document based model are well suited for applications where you primarily interact with one "document" at a time and you want that to be as realtime as possible. Figma is the canonical example. You want the entire document to move together at 60 FPS, completely fluidly. It's not going to be possible to do this well in the ElectricSQL model IMO. Spreadsheets, presentations and documents are other examples. Systems in the ElectricSQL model are more suited for applications where you are interacting with lots of documents at the same time. Think CRMs, bug trackers, etc.
  - Both types of systems are going to track toward the other to support the needs of real applications.

- 🆚️ Is this in a similar vein to https://partykit.io/?
  - Yes they are in the same space. The key difference is in how opinionated each is.
  - PartyKit is extremely unopinionated. It's essentially lightweight javascript server, that launches fast and autoscales (I don't say this as as a bad thing, it's a useful primitive). Most people seem to run yjs in PartyKit, but you can also run automerge or even Replicache – my company's other project.
  - Reflect is entirely focused on providing the best possible multiplayer experience. We make a lot of choices up and down the stack to tightly integrate everything so that multiplayer just works and you can focus on building your app.

- > One plus point compared to CRDTs is that you get to decide how you want to deal with conflicts yourself, with simple, sequential code. I'm not up to date with the latest in CRDT-land but I believe it can be complicated to add application specific conflict resolution if the built-in rules don't fit your needs.
  - I agree wholeheartedly — we took the same approach for PowerSync with a server reconciliation architecture over CRDTs, which is also mentioned elsewhere in the comments here. For applications that have a central server, I think the simplicity of this kind of architecture is very appealing.
- We had similar conclusions around the implementation of PowerSync (sync engine enabling offline-first applications). Instead of CRDTs we went with the architecture of a central server authority and a form of server reconciliation for consistency.

- ## 🚀 Announcing Reflect – A new way to build multiplayer apps like Figma or Notion._202310
- https://twitter.com/aboodman/status/1714682920495919520
  - Rather than CRDTs, Reflect syncs the way video games do.
  - Reflect isn't open source. We're considering that, but in the meantime a source license and on-prem is available.
  - [Ready Player Two – Bringing Game-Style State Synchronization to the Web_202310](https://rocicorp.dev/blog/ready-player-two)
- Super interesting! One drawback I see is that syncing stops working when the server is down. The extra authority on the server makes all clients dependent. I understood CRDTs enabled p2p syncing, which allows collaboration on a local network.
  - Yes, that's true. Although this approach can continue to work *locally* offline and resync when server comes back, it can't sync just within the local network. That's a tradeoff that matters in some cases, but we find that it is a relatively rare need.
- Looks cool! Is this a framework I can run myself for free on my own infra?
  - No, it's a managed service. We do have an on-prem option and a generous free tier.

- Looks amazing! Client-side prediction technique along with the linearization of transactions by arrival time on the server is exactly how the sync engine of Pitch works.
  - We also greatly benefited from the immutable data structures that you get for free in Clojure(Script) to rollback to the canonical snapshot in a performant way. I think you briefly mentioned on HN that you're  using persistent data structures under the hood as well which is cool

- You picked one CRDT that Yjs didn't implement ; ) But don't worry, here's the implementation that's relatively perf-wise and doesn't loose updates
  - Well it depends on how many clients you have right? Each unique instance of Y. Doc is a client ID. That can really add up over time. And I think this suffers the same problem that it's not really an intuitive solution to a counter.

- ## 🚀 Announcing Reflect – high-performance sync for the multiplayer web_202305
- https://twitter.com/aboodman/status/1658251815929126913
  - This is the next step for @replicache and something we’ve been working on and dreaming of for some time.

- Some background: Our existing product, Replicache, is BYOB (bring your own backend).
  - Customers like this as it provides tons of flexibility and enables them to add sync to their existing apps. 
  - We will continue to support and improve Replicache (it’s an integral part of Reflect).
- But we did get a few bits of consistent feedback over the past year that led us to build Reflect:
  - First, people often ask us how to build experiences “like Figma”. With high-performance drag and drop interactivity and cursors flying around.
  - Second, many people loved Replicache and just wanted a complete stack from us. They didn’t want to run, scale, or monitor servers.
  - So we set out to do that!

- features

- ### **1/ Performance.** 
  - Reflect syncs at 60 FPS (120 FPS with device support).
  - If your multiplayer tech doesn’t deliver this, the UI dev will have to paper it over using interpolation.
  - And your app has much more than mouse motion: Users can move things, resize things, rotate things, group things. All these interactions would have to be interpolated.
  - And every single time you add a new interaction, you’ll have to interpolate that too.

- ### **2/ Built-in Persistence.**
  - Reflect isn't just ephemeral(短暂的；瞬息的) sync. Changes are continuously and automatically saved on our cloud service too.
  - You don’t need to wire anything together, copy data from ephemeral to persistent storage, or worry about how often to save.
  - Just write changes as they happen (yes, every mouse movement) and they are automatically saved and replicated to peers.

- ### **3/ Server Authority**
  - 💡 People are often surprised to learn that **Reflect isn’t a CRDT**. 
  - Although lovely computer science, CRDTs have a number of disadvantages for web apps:
    - There’s no good way to validate or enforce data constraints. In pithy terms: CRDTs converge, but to what??
    - For the same reason, fine-grained auth is difficult. It would be hard to implement inline comments that only the author can edit using a CRDT for example.
    - They turn every problem into a distributed systems problem. In the development of real world apps you often find places where it’s convenient to run code on a central server. Common examples are wanting to initialize data once, migrating data, or choosing a leader.
  - 👉🏻 Instead of CRDTs, Reflect uses a more flexible technique from the video game world known as **Server Reconciliation**
  - [Client-Side Prediction and Server Reconciliation - Gabriel Gambetta](https://www.gabrielgambetta.com/client-side-prediction-server-reconciliation.html)
  - This is a lot harder way to build sync, but it solves the above problems:
    - Validation is built-right in. It’s impossible for clients to make invalid changes.
    - Fine-grained auth comes for free. Write auth in plain JS, consulting any backend systems you want.
    - You get a server! You can run server-only code to coordinate clients whenever you want to.
  - At the same time, it's entirely **possible to run a CRDT inside Reflect**, and we even recommend this for text editing — where well developed libraries exist and do an amazing job.

- ### **4/ On-”Prem”**
  - Finally, and maybe most important, we offer the option to run Reflect within your own Cloudflare account.
  - Although customers do not usually want to build, scale, and maintain multiplayer servers, larger customers do often need control of the code and data.
  - We have carefully designed Reflect to enable this. You give us limited permissions to your Cloudflare account and we run Reflect for you.
  - You even get a source license, so even if we disappear, you can still run Reflect forever and gracefully migrate away.

- ### summing up:
  - We’re building multiplayer infrastructure for the next generation of great multiplayer apps. 
  - Everything you need to forget about sync and focus on your product.

- 🤔 How is it different from FluidFramework ?
  - Reflect is **server authoritative**, enabling easy validation and fine-grained authorization
  - Reflect has a **single general data model** (a map of key-value pairs), rather than specialized data structures for different problems.
  - Reflect has (will have) first-class support for running on-"prem".
  - Reflect provides 60 FPS sync so you don't need to interpolate

- Will you support non web-based clients?
  - We will support JS/non-web like React Native and Electron. But Reflect will be JS-first for the forseeable future.
