---
title: lib-db-sqlite-blog-vendors
tags: [sqlite, vendors]
created: 2023-03-01T18:36:34.115Z
modified: 2023-10-26T18:14:17.038Z
---

# lib-db-sqlite-blog-vendors

# guide

# blogs

# blogs-sqlite-powered

## 📝 [SQLSync - Stop building databases_202312](https://sqlsync.dev/posts/stop-building-databases/)

- There comes a time in every frontend engineer’s life where we realize we need to cache data from an API. 
  - storing a previous page of data for that instant back button experience, implementing a bit of undo logic, or merging some state from different API requests
- More feature requests show up, and soon we’re busy implementing data caches, manual indexes, optimistic mutations, and recursive cache invalidation.
- These features bear a remarkable resemblance to the inner workings of databases. Indeed, in any frontend application of sufficient complexity, engineers will necessarily end up building so many data management features that they are essentially creating a domain specific database. 
- Our journey starts in the most humble of ways. Send an API request to the server and store it in a local variable. 
  - The goal of using Redux (or similar) in this way is to centralize cache logic, coordinate refresh, and most importantly share cache results between components.
- One optimization we can leverage in the frontend is to store data cached from the server in an object keyed by ID.
- Recursive Cache invalidation
- SQLSync is a frontend optimized database stack built on top of SQLite with a synchronization engine powered by ideas from Git and distributed systems.
  - SQLSync provides a durable cache, the full power of SQLite (indexes, constraints, triggers, query optimization), optimistic mutations, smart cache invalidation, and reactive queries.
- SQLSync provides optimistic mutations out of the box
  - It does this by handling mutations in a reducer, similar to how Redux works.
  - Using this reducer, SQLSync can execute mutations optimistically on the client, and then run them in a globally consistent order on the server.
  - Finally, the client performs an operation similar to a Git Rebase to synchronize the client with the server.
- One advantage of SQLSync’s architecture is that it eliminates the need for recursive cache invalidation. By writing all the data mutation logic within a reducer that can be easily shared on both the client and the server, all changes made during a mutation are automatically visible. 
  - Even better, due to synchronization working like “Git Rebase”, this approach allows the server to make different changes than what happened on the client - with the guarantee that the client will always reach the same consistent outcome. This is a powerful capability that eliminates the need for developers to spend mental bandwidth on data micromanagement.

## 👥 [Accidental database programming | Hacker News_202312](https://news.ycombinator.com/item?id=38489307)

- With SQLsync he’s made a way for frontend developers to query and update a remote database as if it was completely located right in the browser. Because it basically is. The power of WASM makes it possible to ship a whole SQLite database to the browser. The magic is in how it syncs from multiple clients with a clever but simple reactive algorithm.

- This style of system mostly already exists with old tech, CouchDB+PouchDB. Which works pretty well for some things. 
  - The downsides are that the query system isn't really ideal and the auth and data scoping system is pretty foreign to most people. 
  - The easiest model to work with is when the data is totally owned by a single user, and then you use the out-of-the-box database-per-user model. High data segmentation with CRDTs removes a lot of conflict issues.
  - It has scaling issues though, CouchDB has really high CPU requirements when you're connecting 10k to 100k users. The tech is long in the tooth though it is maintained. On the system design side it gets really complicated when you start sharing data between users, which makes it rather unsuitable as you're just moving the complexity rather than solving it.
  - This approach seems to hit the same target though will likely have similar scaling issues.
- That sounds awfully like Couchbase, which allows you to query/update databases that will sync to remote and the back to peers. And you can control the process (auth/business logic) with sever side JavaScript plugin with ease.

- Reminds me of Meteorjs. It would let you sync a subset of your data to the client and then the client could query it any which way it wanted. They called this “Minimongo”.

- This seems to be one of those problems that entirely disappears by ditching SPAs. Using solutions from the Hotwire or htmx family would mean that a query is just a server query - making those fast is a better-understood problem.
- Only for some class of websites with limited interactivity. On iOS/Android, before all the WebKit apps took over, many apps would use a local SQLite database to support offline edits and implement a syncing protocol to the server. It's a lot of work, but the end product can be quite handy. (This is how you'd expect your email client to work, for example.)

- The problem with databases is actually complexity. Any individual feature is more or less safe, but around the time reliability, caching and indexes get matched together there is a complexity explosion and it doesn't (normally, anyhow) make sense to implement a domain-specific DB (call is a DSD?).
- Really the problem here is SQL's syntax. If using a basic relational database was a pleasant experience that involved some familiar C-like syntax instead of broken English people would be more tempted to go with a DB instead of rolling their own.

- One of my goals is to make the mental model of SQLSync easy to grok for the developers using it. I'm biased, but I find the rebase model much easier to understand than CRDTs.

- 🆚️ How does this compare to using directly an ORM lib that supports browser like TypeORM via SQL.js ?
  - Good question! You can use a ORM with SQLSync. Currently SQLSync doesn't provide an ORM layer for two reasons: 1. there are many that exist, it's better to integrate 2. it's a prototype so I started with the lowest common denominator which is raw SQL.
  - SQLSync is also unique from SQL.js in that it includes a synchronization layer that coordinates with the SQLSync server to provide real time collaboration between users.

- 🆚️ how does it compare to ElectricSQL and PowerSync ?
  - ElectricSQL and PowerSync are both tackling the very hard problem of partial replication. The idea is to build a general solution which allows a traditional centralized db to bidirectionally sync only what's needed on the client side - while still supporting optimistic mutations (and all the consistency/conflict stuff that goes along with that).
  - The downside is implementation complexity. Both require the ability to keep track of precisely the set of data on each client in order to push out changes to only that subset of the overall database. In addition, specifying which subsets of the database state to pull down requires a new DSL and is a new thing to learn (and optimize). That said, I'm stoked they are taking on this extremely hard problem so when SQLSync is ready for partial replication someone will have already figured out the best practices.
  - 👉🏻 SQLSync, on the other hand, only supports full db sync. So every client will see a consistent view of the entire database. You might immediately wonder if this is a good idea - and for some apps, it's not. But consider a personal finance app. The main goal is cross device sync, cloud backup, offline capable, etc. In this case having the entire db stored on every device is probably what you want. Another example is a document oriented data model, such as Airtable. Each Airtable could be a distinct database, thus leaving it up to the client to manage which tables they care about.
  - By focusing on full db sync, the sync engine is much simpler than solutions that support partial replication. One benefit of this is that the backend is very lightweight.

 - I would include optimistic rendering on the list of common patterns that really are a bad idea.
  - Optimistic rendering means your frontend and backend are tightly coupled, error recovery and synchronization is much more complex, and you are locked into (likely heavy) frontend rendering patterns that add even more complexity and coupling.

- My front end db would look a lot different than the back end. A lot of mutations involve submitting work and waiting for distributed jobs to roll up into some kind of partial answer. This worked, That part didn't etc. Long running transactions, workflow that spans months until the final sign off.

- triplit: I'm currently writing a very similar article about "full-stack databases" which highlights the same pattern where many apps end recreating the logic of our backend and database in the frontend client code. The solution we're promoting is to choose a database that can run on both the server and in the client and then sync between them.
  - The reason we aren't using Sqlite for our product is because Sql is frankly not the right tool for querying data for an application. It doesn't easily map to the data-structures you want in your client code and nearly all SQL databases have no way to subscribe to changes to a query without polling the query repeatedly.
- I disagree. Normalizing data is critical for FE reactive applications, keeping data up-to-date basically requires it; all CRUD operations are much easier to handle.
- postgres has some capability to do that/subscription, but does need a server.
  - Yeah you can subscribe to overall changes to the data on a row by row basis but can't subscribe to an actual query. Many apps and libraries imitate reactive queries by just refetching all queries from Postgres when any data changes or just repeatedly polling the query every 10 seconds or so but this puts a lot of strain on the database. You can just subscribe to the replication stream but then you're left trying to reconstruct your queries in your application code which is extremely error prone and painful

- Unless I misunderstood, feels like I’ve been doing this with Ember Data since ~2013.

- Does it needs to download whole database on startup, or can sync only what client queried?
  - Currently it's full db sync. Partial replication is in research.

- do you feel building wrapper over indexedDB instead of sqlite would be better idea?
  - That's a great way to accomplish local storage, but requires a bit of gymnastics to build sync. 
  - By controlling the database entirely, SQLSync can provide very ergonomic sync to the developer and performance for the user.

## [Announcing D1: our first SQL database_202211](https://blog.cloudflare.com/introducing-d1/)

- Meet D1, the database designed for Cloudflare Workers
- D1 is built on SQLite.
