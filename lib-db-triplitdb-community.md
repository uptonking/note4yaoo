---
title: lib-db-triplitdb-community
tags: [community, triplitdb]
created: 2023-10-11T21:37:14.549Z
modified: 2023-10-11T21:37:25.329Z
---

# lib-db-triplitdb-community

# guide

- forums
  - https://news.ycombinator.com/threads?id=matlin
# roadmap
- resources
  - https://triplit.dev/roadmap
# discuss-author
- ## 

- ## 

- ## why we need fullstack, syncing databases
- https://twitter.com/matthew_linkous/status/1744906002368024585
  - whether it's useFetcher, useSWR, React Query, Apollo, etc you'll eventually run into cache invalidation problem
- You’re just trading off one problem for another. How do you sync a large Notion workspace with 2000 employees concurrently working? Caching might be a better solution in that case…
  - Partial replication! With automatic invalidation and optimistic updates...
- Haha. Sounds like caching to me
- Because it is! Just better than a plain document or normalized cache because it can actually understand evaluate the queries you're trying to cache

- has triplit implemented partial replication?
  - Yep! Data is sent over the network only as needed from queries and subscriptions on the client

- ## We’ve been spending a lot of time thinking about the best way to expose and implement relational querying in Triplit.
- https://twitter.com/triplit_dev/status/1707509447789043760
  - We’ve decided not to introduce any new concepts like “joins”, “links”, or “references”. What we settled on is devilishly simple yet powerful
  - Soon in any query, you'll be able to drop a *subquery* right in where clause next to your other filters
  - You can also arbitrarily nest subqueries to simulate traversing a graph of relations!
- I think this [nesting] is the right way. You can more easily de-compose sub-selects into their own reactive queries than if you were to introduce joins.
  - That's been a big motivation. We feel like this is the best format for both the query compiler and for users/devs

- We're working on predefining relations as subqueries in our schemas then you can just use dot notation to access them in filters
- https://twitter.com/ccorcos/status/1707809858077209070
  - This cool. In my experience, I’ve found it frustrating when APIs return denormalized formats. You end up having to renormalize things yourself and merge with all the data you already have in some kind of client side database. That’s something I never understood about graphql
- Totally agree. We're actually going to limit sub-queries to filtering/where clauses to start and only add them into selects when we have a compelling use case

- ## TriplitDB support for javascript Dates, nullable attributes and default values _202309
- https://twitter.com/triplit_dev/status/1704300302373957767
  - Triplit Client support for fetch policies
  - Triplit now supports using Javascript Dates directly in updates and inserts!

- ## one cool thing we did with Tuple DB is we made a wrapper to allow querying across multiple storage backends and dynamically scoping reads and writes to subsets of those storage layers_202308
- https://discord.com/channels/1138467878623006720/1138870969688150016/1139382908151418990
  - it can let you do cool things like database "forking"
- Interesting. You kind of lose transactional guarantees that way though. What’s your use case?
  - Yeah we tend to only write to single store at once so it's not much of a concern. But we use it to essentially create two layers where one layer is the cache of committed entities and the other layer (called "outbox") is local mutations that need to be synced. That way a rollback can just be clearing outbox storage but from a querying perspective it seems like one unified layer 

- ## Last week we open sourced our database, TriplitDB._202308
- https://twitter.com/triplit_dev/status/1689051390880989185
- Always glad to see a new triplestore on the block!

- ## Big improvements to our update API - much easier to use and less code! Under the hood we use a ES6 proxy, similar to how Immer.js works. _202308
- https://twitter.com/triplit_dev/status/1688638103164981248

# discuss-not-yet
- ## 

- ## 

- ## does triplit db provide utilities to implement undo/redo? 
- https://discord.com/channels/1138467878623006720/1138467879113728033/1223502401609404447
- Not currently but it's on our roadmap triplit.dev/roadmap
  - Triplit does already retain the history of edits made to each attribute.

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 👨🏻‍🏫 [An interactive intro to CRDTs | Hacker News_202310](https://news.ycombinator.com/item?id=37764581)
- In practice, most apps will only need Last-Writer-Wins registers and not the more complicated sequence CRDT's that you find in Y.js and Automerge.
  - We've built a auto-syncing database that uses CRDTs under the hood but never exposes them through the API. So if you want all of the benefits of CRDTs e.g. offline-first user experience, checkout our project, Triplit!
- 🤔 why didn't/don't you build Triplit on cr-sqlite?
  - We're aware of cr-sqlite and I've talked to the author, Matt, a few times. 
  - Short answer: SQLite has serious shortcomings when it comes to reactivity and we think we can be as fast as SQLite for the application-type queries we aim to support. 
  - The long answer would be about supporting all of features we don't need in SQLite and all of the quirks that come with it like having `null` as a primary key
  - We also recently came up with a relational-style querying system without joins

# discuss
- ## 

- ## 🗑️ is it possible to delete a database?
- https://discord.com/channels/1138467878623006720/1138467879113728033/1197135462607888465
- If you're running locally and using the SQLite adapter, you can just delete the SQLite files. 
  - If you're running on Triplit Cloud, you can delete the database from the Dashboard.

- https://discord.com/channels/1138467878623006720/1138467879113728033/1197351110285991947
- You are correct, that schema modifying methods on the database only effect the underlying schema definitions but doesn't delete the underlying data like you would expect with a SQL `drop table ...` . 
  - Instead you can/must query the entities in that collection and delete in that transaction to achieve what you're going for
  - I can see how those methods are confusing. We might be better off with refactor

- `client.db.clear()` should do what you want (it also removes schemas as well iirc)
  - The caveat is that it's a local-only operation so it won't cause deletes to sync to the server or other connected clients

- If you want to delete just from the client you can do it in a transaction

```JS
await client.transact(async (tx) => {
  for (const name of collectionsArray) {
    console.log("dropping collection", name);
    const entitiesToDelete = await client.fetch(client.query(name));
    for (const entityId of entitiesToDelete.keys()) {
      await client.delete(name, entityId);
    }
    await tx.dropCollection({ name });
  }
});
```

- ## A sneak preview of a simpler way to define relationships between collections in Triplit
- https://twitter.com/matthew_linkous/status/1745203037210030565
  - The key reason we can make this so nice and concise is actually our direct support for Sets as attributes (look at 'postIds'). 
  - In SQL world, you'd need an extra table like `user_posts` and a three-way join to make this relation possible

- ## 🚀 [Triplit: Open-source DB that syncs data between server and browser in real-time | Hacker News_202401](https://news.ycombinator.com/item?id=38977516)
- I use pouchdb/couchdb right now and I think my biggest issue at the moment is the amount of time it takes to sync up the app when you open it. It's possible to load the app straight from local data, but then it might be out of sync which could be jarring/confusing for the user.
  - Is this named after a triple store (e.g EAV) like in datomic? If so this is looking very close to my dream database.
- 🛋️ The problem with couchdb is that it does one request per document which makes the protocol slow for browser based applications also it has no http2 support. 
  - Also storing the full rev tree of the documents is what makes pouchdb slow. 
  - 👉🏻 This is why RxDB moved away from pouchdb/couchdb to a replication which works on bulk operation and resolves conflicts directly when they happen, not afterwards.
- Yes great catch! One of the inspirations for Triplit's name is exactly from our use of a triple store under the hood. Datomic also has been a major influence in how we've designed the internals of Triplit

- How does this handle multi-user conflicting updates, e.g. OT, CRDT?
  - I believe individual fields are last-writer-wins. Fancier CRDTs like text/lists are not directly supported, but I found that you can layer them on top
- Yep exactly. We also include a Set CRDT you can add to any entity.

- 🐛 Ideally, your app would be server-rendered on the first load, instead of first loading all data, and then filling a SPA from that.
  - We're working on exactly this. You can already do this with Triplit but it's challenging to make an out of the box solution because each framework passes context/data different from server to client differently. There's a cool project called [Vike](https://github.com/vikejs/vike) that generalizes this pattern across SSR'd UI frameworks

- This looks super useful for anything requiring optimistic updates, but how do you get data from triplit into another db? Perhaps for analytics or audit purposes.
  - With something like electric-sql you can just use one of the many Postgres tools, and other local-first options like https://ably.com/livesync have database adaptors for replication. I think this is an important requirement whenever you build your own database
- Currently, You can accomplish this by pulling from Triplit with either a JS client that just subscribes to each collection or with the REST API but we're currently working on a way to define custom "triggers" on your Triplit Server so you could directly push into any other database as you'd like
- 🔁 Is “triggers” a change-data-capture like thingy? Having an easy to connect to CDC stream seems like a great feature to offer. Is your trigger concept like DynamoDB Stream + triggers?
  - Yes that's pretty much what we're going for. I'm less familiar with DynamoDB Streams but we're taking inspiration from Postgres triggers
- I recommend having a pre-built integration that dumps all changes to the database in a Debezium CDC compatible format. Not sure how you'd normalize Triplit changes into Debezium updates, but something to think about. Debezium CDC format lets you pipe changes from one DB into a stream system like Kafka, and then out of Kafka into another DB on the other end. It's handy.
  - For example, the original method for connecting Postgres to Materialize.com was using a Debezium stream

- 🪶 Are there any examples showing how to use Sqlite? I'm developing a notes app and will be using sqlite's full text search extension a lot
  - Triplit is pretty opinionated about how things get stored so it doesn't work with existing SQLite schemas. We support basic `like` operators for searching but are definitely interested in supporting full text search. 
  - 👉🏻 If you want to try that out, we use Sqlite in our server implementation so you can see an example there

- 🪶 Is the underlying db using wasm SQLite in the browser? 
  - Triplit can basically bind to any storage capable of providing ordered key values so we have bindings for SQLite but in the browser you're best of doing either in-memory or IndexedDB (both of which are built-in)
- Regarding similar projects there are a few you can find on https://localfirstweb.dev/, but Triplit stands out in a few ways: 
  - Support for an authoritative server 
  - Provides an optional hosted cloud service 
  - Relational querying without SQL 
  - Partial replication (this is a big one)
  - Typescript schemas and type hinting in queries in return types

- If I already have an app that uses firebase, do you have some migration guidelines? Perhaps a tutorial for migration? That would help.
  - We don't have any written docs
- I just switched from firebase realtime to pouchdb. I was getting concerned about firebase "local first" not really working how I expected and pouch fit the bill nicely. I like the idea of field level sync and wonder if triplit would be faster than pouch.

- 🆚️ Why would I use this over POST and server side update db or websockets?
  - I’d suggest Triplit if you want to make a rich web app similar to Notion. 
  - Under the hood this thing is doing POST and websocket subscriptions. 
  - You can skip all the manual work to wire up optimistic updates, subscription, local storage, pending transaction queue by adopting someone else’s implementation. 
  - Also after doing it enough times, adding a POST endpoint per record type in your app to create/read/update/delete that type gets old.
- if you're building a highly interactive app (especially on mobile), you can't wait for network after each action before showing feedback to the user.
  - Triplit does this all for you automatically with the mental model that your database queries automatically update when any data changes happen even if you're offline. Triplit takes care of reconciling this whether the request succeeds on the server and with concurrent changes from other users.
- I don't 100% know in the case of triplit, but pouchdb does what you describe for "free" (i.e. you don't need to code it). firebase uses a websocket, pouch uses (I believe) long polling.

- 🆚️ How would this compare to RxDB?
  - RxDB is just provides clientside querying and a sync protocol. 
  - Triplit is full stack in that it's designed to run on both client and server and will "just work" out of the box for end to end syncing, querying, and persisting data. Triplit supports relational querying.

- how does this compare to https://electric-sql.com/
- https://news.ycombinator.com/item?id=38977049
  - I think our goals are pretty similar but Triplit offers more flexible storage options (Durable Objects, IndexedDB, SQLite), deeper Typescript integration, and is probably a good deal simpler to operate--we are closer to Firebase/Firestore in that regard. 
  - ElectricSQL instead builds on the robustness of Postgres and SQLite.

- ## 🚀 [Show HN: Triplit – The Full-Stack Database | Hacker News_202312](https://news.ycombinator.com/item?id=38805423)
- Triplit is designed to make building collaborative and local-first web apps a lot simpler.
  - It works by running an instance of TriplitDB both in your client-side app and also on the server then efficiently syncs any queries you run on the client in real-time from the server over WebSockets. 
  - And because you have a complete database instant on the client, it works completely offline. 
  - Handling collaboration is a lot easier with Triplit because each entity you store gets split into its individual properties so 🔀 conflicts that may occur when multiple users are editing concurrently are solved granularly **on a per-attribute basis** rather than the entire JSON document.
  - We're in the process of building out a Firebase-like service (in private beta currently) but in the meantime you run the entire Triplit stack locally with our CLI.

- Looks promising, this would be awesome for flutter.
  - We're focusing on JS environments first but this is not the first time we've heard this

- ## What I want from my sync engine:
- https://twitter.com/kylemathews/status/1738805645284118857
  - local writes land locally
  - writes elsewhere in the system are replicated in real-time to clients
  - each client has a database of synced data that it can query anyway it wants
- 100% agree. We're building @triplit_dev with this mod. Hard parts are handling conflicts and authorization which we've opted for Last-Writer-Wins on the property level of an entity and authorization enforced by server
  - Getting the engine to sync is also only one piece of the puzzle. Having good hooks into the state of sync is also import to surface in the UI about being online/offline, pending changes, which items in the UI are optimistic rather than confirmed by server, etc

- ## Ever wonder what it would take to make your app feel faster? Let’s speed-run optimizing a typical web app so we can see how challenging it actually is. 
- https://twitter.com/matthew_linkous/status/1724501205701783899
- You have your local database setup and you've re-implemented every endpoint on your backend server as a client-side query. You app is running seamlessly even when disconnected from the network but you still need to figure out how to sync data between the frontend and backend
- On first blush, you think all you need to do is insert data from your backend when your app starts and then read from the SQLite database exclusively, but soon you realize it's much more complicated than you thought...
- For starters, how do you even subscribe to changes on your remote database? As you unravel(解开，拆开) the challenge ahead of you you're left with more questions than answers:
  - How do you keep a schema in sync between your local and remote database? 
  - How do you rollback changes on the client when they're rejected by the server? 
  - How do you handle conflicting changes from different users?
  - Are you polling the remote database too often?

- ## 🌰 [Some notes on local-first development | Hacker News_202309](https://news.ycombinator.com/item?id=37488034)
- One common misconception with local-first, is that it's essentially local-only. 
  - But I believe the best experience is where the server and client are equally capable and only a partial set of data is stored on the client. The server still maintains authority but the client is always snappy(迅速的) when updated data or changing queries/views. 
  - We basically call this a full-stack database and we're building that at Triplit.

- 1. What to do with stale user data? What happens if a user doesn't open the app for a year? How do you handle migrations?
  - Just don't delete the old cases. Refuse to run sync if device is not on the latest schema version.
  - I can take a DB dump from 2018, migrate it, and have the app run against master, without any manual fixes.
- 2. What about data corruption? What happens if the user has a network interruption during a sync? How do you handle partial states?
  - Run the sync in a transaction.
- 3. What happens when you have merge conflicts during a sync? CRDT structures are not even close to enough for this.
  - CRDTs are probably the best we have so far, but what you should do depends on the application. You may have to ask the user to pick one of the possible resolutions. "Keep version A, version B, or both?"
- 4. What happens when the user has millions of items? How do you handle sync and storage for that?
  - Every system has practical limits. Set a soft limit to warn people about pushing the app too far. Find out who your user with a million items is. Talk to them about their use cases. Figure out if you can improve the product, maybe offer a pro/higher-priced tier.
- Mobiles are really bad with memory. iOS and Android have insane level of restrictions on how much memory an app can consume, and for good reason because most consumer mobile phones have 4-6 gbs of RAM.
  - You don't load up your entire DB into memory on the backend either. 
- You're asking very broad questions, and I know these are very simplistic answers - every product will be slightly different and face unique trade-offs.
- I think you misunderstand. My intention was not to say local-first is bad or impossible; it's not. We have been local-first at Notesnook since the beginning and it has been going alright so far.
  - Just a few weeks back a user came to us after failing to migrate GBs of their data off of Evernote. This, of course, included attachments. In short, we had not considered someone syncing 80K items. To be clear, 80K is not a lot of items even for a local-first sync system, but you do have to optimize for it. 
  - The solution consisted of extensively utilizing batching & parallelization on both the backend & the users' device.
- The problem was about the phone fetching 80k new items from the server. If the phone just shows the item you're looking at, one at a time, and doesn't try to sync everything, there's no such problem.
  - There's no restriction inherent to CRDTs/local-first around a partial sync. You are not required to sync everything.

- 💡 Query-based sync to partially replicate is an absolute must. This was a key feature with Ditto: https://www.ditto.live
- 👉🏻 Query-based replication works when you know what the user probably wants to have in advance (e.g. a device in a warehouse needs records for that stock in that warehouse, not others). But that's still push.
  - You still need pull on demand access when a user opens any random item where we don't know in advance what they probably want (e.g. a discussion board scenario).

- Partial replication is a problem I haven't seen many people solving but it is definitely the next frontier in this space.

- 🗣️ I am the developer of RxDB, a local-first javascript database, and I made multiple apps with it and worked with many people creating local first apps. The problems you describe are basically solved.
- > What to do with stale user data?
  - Version/Schema migration in RxDB (same for IndexedDB and watermelonDB) can be done in simple javascript functions.
- > What about data corruption?
  - Offline first apps are built on the premise that internet connections drop or do not exist at all. The replication protocols are build with exact that purpose so they do not have any problems with that
- > What happens when you have merge conflicts during a sync?
  - You are right, CRDTs are not the answer for most use cases. Therefore RxDB has custom conflict handlers, which are plain javascript functions. 
- > What happens when the user has millions of items?
  - There is a limit on how much you can store on a client device. If you need to store gigabytes of data, it will just not work. You are right at that point.
- > How do you handle backups? How do you handle exports?
  - live backups; json export/import  
