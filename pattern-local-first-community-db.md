---
title: pattern-local-first-community-db
tags: [community, database, local-first]
created: 2023-12-01T09:08:04.006Z
modified: 2023-12-01T09:08:18.316Z
---

# pattern-local-first-community-db

# guide

- local-first-db的案例
  - 常用chat作为示例: scuttlebutt > manyverse/MPLv2, hypercore > keet/NonOpen, triplitdb > beeper, kappa > cabal/AGPLv3

- local-first-db
  - pouchdb, minimongo

- resources
  - https://github.com/pubkey/client-side-databases
  - [Alternatives - ElectricSQL](https://electric-sql.com/docs/reference/alternatives)
  - [In Search of a Local-First Database | Jared Forsyth.com_202004](https://jaredforsyth.com/posts/in-search-of-a-local-first-database/)
# discuss-stars
- ## 

- ## Almost everything needed to build a real-time, multiplayer, #LocalFirst, offline enabled database is actually just "incremental view maintenance"...
- https://twitter.com/samwillis/status/1743193008164458588
  - Partial sync to users device ✔️
  - User permission changes ✔️
  - Reactive UI queries ✔️

- ## [What makes synceddb a good offline-first database?_201801](https://github.com/paldepind/synceddb/issues/47)
- One of the distinguishing features of SyncedDB is that it attempts to be a very lightweight wrapper around IndexedDB. 
  - It's essentially IndexedDB + migrations + promises + syncing.

# discuss-interoperability
- ## 

- ## 

- ## Just demo'd: Using DeepSeek to search AFFiNE workspace in VSCode! ( @thankscline as MCP client) _202502
- https://x.com/ewind_dev/status/1886334272803663915
  - At @localfirstconf last year, I demoed mapping CRDT to WebDAV filesystem, enabling AFFiNE doc editing in VSCode. This feature never made it to production because sharing content through traditional OS files was too cumbersome and clunky.
  - MCP, however, significantly simplifies cross-app and cross-LLM data source sharing—you don't need to expose your workspace as markdown files on disk anymore. MCP servers can automatically map them as multi-modal resources, opening up broader interaction possibilities.

# discuss-skdb
- ## 

- ## 

- ## 

- ## @JulienVerlaguet has started @skiplabs to work on SKDB, a reactive DB built from the ground up (like, literally, they have their own sklang programming language). 
- https://twitter.com/joygao/status/1749228059360960569
  - A lot of companies and OS projects have built subset/variation of this (us at Figma included!), however seeing this being tackled from the ground up is quite refreshing.

# discuss
- ## 

- ## 

- ## 我没服务器，我的 blog 存哪里比较好 
- https://x.com/ayingott319/status/1902729976895656334
- neon/vercel/cloudfare/GitHub

- 静态博客：cloudflare pages
  - 动态博客：去看看 vps 圈子有哪些好商家

- ## Exposing database tables directly to client code strikes again. It’s the bad design pattern that never quits.
- https://x.com/jamesacowling/status/1895970943631327460
- Tbf, the issue was a vulnerable build pipeline exposing an admin key.  If that was an AWS key, that could have exposed the same issue on a segregated DB
- i've never liked this paradigm; so many issues around abstraction, auth, split-brain, etc.

- ## I need a reactive local database; what's the frontend tech to use?
- https://twitter.com/meijer_s/status/1753354109548204495
  - I'll fetch multiple pages (offset based pagination) of data from remote
  - listen to create, update, delete events from remote, and sync those changes into local db
  - subscribe to that db to render items
- I'm using react native, so sqlite becomes an option.
  - I think AsyncStorage works too
  - react query + async storage had crossed my mind. I was hoping for something that requires less work on my end though.

- ## [What is the best DB for offline-first? : reactnative_202309](https://www.reddit.com/r/reactnative/comments/16f42gz/what_is_the_best_db_for_offlinefirst/)
- Realm is open sourced? My understanding it was closed and to use it you need to pay for MongoDB. Is this not the case?
  - Yeah, both are open source, mongo and realm SDKs. What you pay for is the hosting service, MongoDB Atlas.

- I use realm, its convenient but I encountered a couple of issues:
  - It does not have cascading delete unless you use embedded objects
  - The change listeners have a limitation. Lets say you have a deeply nested object and you add a listener to it. It can only detect a change upto 3rd level of nesting if I recall correctly. I had upto 6 levels and it didn't work. You can however, use workarounds for it. So if you don't have deeply nested objects and don't need cascading delete, realm is a good option

- ## with local-first your front end code is interfacing with the DB. The sync layer handles permissions.
- https://twitter.com/tantaman/status/1743309463837102188
- Dbs still lack some abstractions. RLS is half the battle. Other pieces:
  - supporting live migrations / migrations without downtime 
  - supporting old clients that never upgrade to be compatible with a new schema
- With Electric, migrations go via the replication stream so clients all move forward as they sync. Obviously there are considerations at the app layer with that, but it makes things simpler. Only have additive migration for now, but that should change.

- I'd like to see someone explore a db that has a record of all schemas that have ever been applied to it. Where a client that queries it can provide their schema version in the query and the DB can project results back down to that schema.

- ## 👥 [Accidental database programming | Hacker News_202312](https://news.ycombinator.com/item?id=38489307)
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

- I was surprised you didn't mention watermelonDB. It sounds like what you are building but specifically for react native. I tried to use it but there were lots of really annoying api choices regarding how the querying works in the front end and their choices on how their ORM works. But the sync methodology they use seems to be sound, and as they say, they've thought long and hard about.

- ## 🚀 Meet SQLSync: Application development is a lot easier when you're building on top of a frontend-optimized database stack. _20231201
- https://twitter.com/carlsverre/status/1730288131419861420
  - I’m building SQLSync because I want to make client-side applications easier to build without us having to reinvent the wheel each time.
- How do you think about:
  - a) Changing a row's visibility per user (e.g. more granular  RBAC than segmenting access to sync'd databases per org)
  - b) State that a user could see that's too large to fit in the browser
- Good questions!
  - a) I think any sub-db segmentation will have to wait for partial two-way replication, have some ideas but nothing in code yet
  - b) partial replication; or lazy sync: retrieve pages lazily, sync invalidation sets

- Currently SQLSync moves the entire database to every client and keeps them all in sync. This means that it's suited for smallish sets of relational data - ideally per-user or per-document. This is made easier as each db is very cheap to create.
  - this model works very well with @tursodatabase , since we can offer 10k databases for $29 - and more on enterprise plans. We are drooling for an integration here!

- ## for @recall_wiki we are going with WatermelonDB.
- https://twitter.com/paulrchds/status/1483416223425650691
- I've had a great experience with CouchDB + PouchDB. I wonder what were the deciding factors in favor of WatermelonDB?
  - IIRC, it was because I wanted to put some custom logic between the pouchdb and couchdb which didn't seem possible without reimplementing the syncing.
  - yes indeed!

- I had quite a few issues with the syncing from indexedDb and DynamoDb, it was in April last year so I am not sure if has improved by now. 

- ## 🛢️ [WatermelonDB, a database for React and React Native apps | Hacker News_201809](https://news.ycombinator.com/item?id=17950992)
- 🤔 Why not use SQLite directly instead of this extra layer?
  - SQLite gives you just the "data fetching" part. But if you're building a React/RN app, you probably also want everything to be automatically observable.
  - Watermelon is an observable abstraction on top of SQLite (or an arbitrary database), so that you can connect data to components and have them update automatically
- So is it fair to say its a React specific ORM, that automatically makes the mapped objects observable (an OORM, if you will)? Just trying to understand the level of abstraction that you're going for.
  - That's a fair description, yeah!
- Does that mean that if user A makes an update to the database, then user B (on a different computer) will see the update?
  - No, Watermelon is a local app database. But you can plug it into a sync engine to synchronize with the server (and then from the server to another device) — it's up to you

- When SQLite is not available in the browser, can it fallback to using use an Adapter which just implements a (low performance) DB in memory or storage?
  - Yep, if you can support some (relatively basic) queries, and CRUD operations, you can plug in essentially any database, and bridge on any platform. Think Electron, SQLite on native macOS, heck, you could use Realm as the underlying database if you so preferred

- 🆚️ How does WatermelonDB compare to Realm?
  - I'm not an expert at Realm, so I might get some details wrong, but briefly:
  - You can't run Realm on the web (not as a database, offline), but you can with Watermelon
  - Realm is _a_ database, Watermelon is a more universal database framework that can be backed by any underlying database via an adapter
  - Realm is more than just a database, it's also a whole app development platform. And it's designed to sync with a proprietary Realm cloud service. 👉🏻 Watermelon is just a local database, but it tracks changes in the database so you can plug it in and synchronize with an arbitrary backend
  - I heard that Realm (on React Native at least) doesn't perform super well when you get to many thousands/tens of thousands of records, but i haven't tested it yet myself, so take it with a grain of salt. Watermelon always does lazy loading so it doesn't really affect performance how many records total there are.

- Looks like it's just an ORM for SQLite. Isn't SQLite too large to be included in the web?
  - Yeah :/ There used to be this thing called Web SQL 
  - on the web, Watermelon uses LokiJS, which isn't perfect, but still works well.

- There's a very promising attempt to get WebSQL-like features to browsers: Relational Database Proposal. Proposal tries to solve limitations Lovefield library authors had to deal with. (Lovefield powers GMail Inbox if I'm not mistaken.)

- Would it be possible to write an adapter to use this with postgresql on the web?
  - It's possible, but Watermelon is specifically designed to be a local database, not meant to run on a server.

- Sync is mostly there, but undocumented

- https://news.ycombinator.com/item?id=28998272
- IndexedDB is a _bad_ API, and making many small read/write operations on it is absurdly slow. This is one of the reasons why WatermelonDB on web only uses IDB as a dumb storage medium but actually 👉🏻 does all the database'y things in memory. You won't reasonably scale to gigabytes this way, but for most PWAs this is plenty enough and MUCH faster in practice. Certainly far faster than network.
- I've used watermelondb and found it quite nice to use. I mainly chose it because it has observable queries. I can live without conflict resolution and transactions on the client side because it's an electron app. Having a sqlite backend (via the electron process) would overcome some of the shortcoming wrt to the in memory database (and still allow in memory via sqlite if speed is desired). I wrote a backend sync for it which was quite easy although I haven't fully implemented support for everything because I don't need it (notably deletes).
- The problem is that Watermelon assumes a consistent view of the entire database, so you can't have multiple writers - at least not without synchronous notifications from IndexedDB (not a thing), leader election (cannot be made reliable), or some design sacrifices. To be reconsidered in the future...

- ## [ObjectBox: Fast object-oriented database for Go | Hacker News_201811](https://news.ycombinator.com/item?id=18568029)
- SQLite is a very nice embedded DB indeed. If you like SQL. ObjectBox enables you to work with Go structs and gives you additional performance.

- It's ACID compliant, and thus not not in-memory. https://golang.objectbox.io/faq covers that in detail. In the FAQ, there is a section on comparing to JSON; I guess the same would hold true for CSV.

- ## [IndexedDB, WebSQL, LocalStorage – what blocks the DOM?_201509](https://nolanlawson.com/2015/09/29/indexeddb-websql-localstorage-what-blocks-the-dom/)
- there are only three ways of storing data in the browser:
  - LocalStorage
  - WebSQL
  - IndexedDB
- Every “database” listed above uses one of those three under the hood (or they operate in-memory). 
- LocalStorage is a lightweight way to store key-value pairs. 
  - The API is very simple, but usage is capped at 5MB in many browsers. 
  - Plus the API is synchronous, so as we’ll see later, it can block the DOM.
- IndexedDB is the successor to both LocalStorage and WebSQL, designed to replace them as the “one true” browser database. 
  - It exposes an asynchronous API that supposedly avoids blocking the DOM, but as we’ll see below, it doesn’t necessarily live up to the hype
- JavaScript is a single-threaded programming environment, meaning that synchronous operations are blocking. 
  - And since the DOM is synchronous, this means that when JavaScript blocks, the DOM is also blocked. 
  - So if any operation takes longer than 16ms, it can lead to dropped frames
  - This is the reason that JavaScript has so many asynchronous APIs.
- since any synchronous code is blocking, in-memory operations are also blocking. 
- LocalStorage fully blocks the DOM while you’re writing data. 
  - The blocking is a lot more noticeable than with in-memory, since the browser has to actually flush to disk.
  - This is pretty much the banner reason not to use LocalStorage
  - I assume this is because these browsers cache LocalStorage to memory and then batch their write operations (here’s how Firefox does it), but in any case the UI still ends up looking janky.
- IndexedDB is slower than LocalStorage for basic key-value insertions, 
- IndexedDB works swimmingly well in a web worker, where it runs at roughly the same speed but without blocking the DOM. 

- IndexedDB works swimmingly well in a web worker, where it runs at roughly the same speed but without blocking the DOM. 

- ## 🛢️ [Lovefield – A relational database for web apps | Hacker News_201509](https://news.ycombinator.com/item?id=10197672)
- Interesting. At first I was thinking this might be part of their cross-platform (iOS/Android/web) architecture that they use for Inbox, Sheets, and a few other things.
  - E.g. they assert that, despite having pure-native views (e.g. no Swing-style "one UI for all platforms"), they share ~70% of the client-side code across iOS/Android/web.
  - Which to me insinuates(暗指, 暗示; 逐渐取得) the reused code is probably things like the domain models, validation rules, and also online/offline data storage/sync logic.
  - E.g. maybe Lovefield was part of that cross-platform client-side storage architecture. But probably not since it's Javascript. 
- iOS/Android have SQLLite, LoveField is kind of like an SQL-lite for the Web.

- Lovefield is still relatively new and immature. When I tried to use it I ran into some strange errors. The situation might have improved now but I personally would still recommend PouchDB instead.
- It's like having PouchDB -> CouchDB but with SQL not NoSQL
  - Also, without the replication and conflict detection.
