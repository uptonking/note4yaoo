---
title: lib-db-rxdb-community
tags: [community, rxdb]
created: 2023-10-08T10:54:41.535Z
modified: 2023-10-08T10:54:57.575Z
---

# lib-db-rxdb-community

# guide

- forums
  - https://news.ycombinator.com/from?site=rxdb.info
  - https://news.ycombinator.com/threads?id=realPubkey
# discuss-stars
- ## 

- ## [Transactions + Nested Subdocuments - Yjs Community_202301](https://discuss.yjs.dev/t/transactions-nested-subdocuments/1602)
- RxDB is an offline-first database that does not support transactions and instead offers revisions and conflict handling. Not sure if the points made there also apply to YJS, at least in a general sense.

# discuss-sync/collab
- ## 

- ## 

- ## hello everyone, is premium memory can sync with couchdb ?_202303
- https://discord.com/channels/969553741705539624/1059149217718861935/1089138975538675722
- Since v13, all storages are able to replicate with a CouchDB endpoint. They only use the RxDB replication protocol, not the couchdb protocol. But it is compatible with a CouchDB endpoint.
  - The memory storage is NOT premium, you can use it for free.

- ## Hello, does RxDB provide crdt out of the box, or should I use the RxDDcrdtPlugin. _202303
- https://discord.com/channels/969553741705539624/994606235141800047/1090892342191468654
  - Additionally, I tested it with the vue example, using couchdb for replication, and I did some conflict changes, but the problem is solved and there is no crdt code inside.
- CRDT are not in the core package, you need to use the crdt plugin for that.
  - RxDB has a conflict resolution by itself, you do not need crdts for that, but you might benefit from using crdts. 

- ## Did you also consider of pushing assumed master hash to the server instead of the full document? _202308
- https://discord.com/channels/969553741705539624/1050381589399470160/1143498532217688085
  - That would save the amount of data transferred to the server.
  - It could be something like stable stringified md5 hash which server would compare with it's own state

- Yes, I know. That is why couchdb has the hash of the data inside of the revision and pouchdb only does a revision check
  - I had ideas to let the user strip whatever is not required from the assumed master state
  - and then only store stuff like the revision or a hash
  - but most users would never use this
  - and for those who it is important to save the bandwidth, can strip the additional data in the pull/push handlers

- ## I've realised that all documents in the replication collection has the same revision value, is that intentional?
- https://discord.com/channels/969553741705539624/1050381589399470160/1143816861427978320
  - And also, for the assumed masters

- there is no problem in this. Also normal documents can have same revision strings for different document ids
  - RxDB does not use a hash as revision (like couchdb does) for performance reasons

- ## what is the easiest way to sync RxDB to cloud or local server?_202312
- https://discord.com/channels/969553741705539624/994606235141800047/1185755090557091961
- I think using a couchdb server is the easiest to setup
  - or the websocket remote storage with rxdb on the server and on the client

# discuss
- ## 

- ## 

- ## 

- ## 🎯↩️ [ANNOUNCEMENT: Plans for the next major version 15.0.0 _202310](https://github.com/pubkey/rxdb/issues/4994)
- One thing we have come across that would be useful to be able to have a TTL on records stored locally. In our use case there are certain forms of data we only need to know about the last 14 days.
  - This is the big tradeoff. RxDB choose to have a simple-as-possible replication protocol, so that it can be implemented on top of any infrastructure. 
  - To make this possible, we do not have cross-document transactions and it is not possible to enforce coordinated replications. 
  - Most users do not have this problem because they pack everything that belongs together, into the same document. 
  - Your code should assume that a linked document can exist, but also might not be there (yet).

- In order to keep track of document changes in scenarios like Undo/Redo stacks or version control in general, it would be a very pleasant DX if we could have a native checkpoints plugin. 
  - RxDB only stores the latest known document state. We stored all changes in the past (aka event-sourcing) when RxDB was build on pouchdb. But experience has shown that event-sourcing requires too much performance for client side databases. This is why RxDB resolves conflicts directly on replication, not afterwards so that it only has to store the latest state.
  - But maybe what you describe can make sense for the CRDT plugin. There we could "undo" operations by calculating the opposite CRDT operation to any given step.
- totally agree it's a good fit for the CRDT plugin, I think building this on top of the CRDT plugin can also help with even more complex scenarios, for example: a multiplayer undo stack where each user can undo their own actions, not affecting changes made by others.

- ## 💡 [rxdb: Offline First_202109](https://news.ycombinator.com/item?id=28690427)
- what's a good solution for syncing with the main database after the device goes back online?
- 👉🏻 CouchDB/PouchDB(the JS compatible cousin) make use of a global sequence counter to track which documents have changed between sync.
- Each database uses an arbitrary byte string to mark a position in a sequence of updates to the database. 
  - Each document has the sequence counter of when it was created/updated/deleted. 
  - This sequence counter only matters to that particular database (it does not need to be mirrored, it's just a local ref. of WHEN the doc was modified in that particular database).
- **Syncing is then a process of looking up the last read sequence counter from a checkpoint document** (i.e. what was the last modification) and passing that sequence counter to the `changes` endpoint to get a list of all documents with a sequence counter AFTER that, and then pulling/pushing those documents to the local/remote database, and saving the new latest sequence counter.

- Earlier this year I experimented with combining CRDTs using the incredible yjs with PouchDB. It worked really well, completely magic syncing with full automatic handling of sync conflicts! 
  - [(Alpha) PouchDB integration for Yjs](https://gist.github.com/samwillis/1465da23194d1ad480a5548458864077)

- Check out WatermelonDB 
- pouchdb is mostly unmaintained and issues are just closed by the state bot instead of being fixed.
  - So in the last major RxDB release, I abstracted the underlaying pouchdb in a way that it can be swapped out for a different storage engine. 
  - This means you could in theory use RxDB directly on SQLite or indexeddb. 
  - In practice of course someone has to first create a working implementation of the RxStorage interface.

- Meteor uses `minimongo` on the client which sync's with the server; effectively doing the same thing. It's actually amazing how much better the UX is when you have spotty coverage.
- I think Oracle APEX works on the same premise? Store locally in indexedDB and sync up when the connection is back on-line. No need for difficult programming, APEX does this out of the box .
  - Anyhow, a way to force this behaviour in APEX is to make every user interaction a write action on the DB. This way you either save locally or to the backend (but you don't have to worry about the sync between the two).

- ## 🔥 [RxDB – a real-time database on top of PouchDB | Hacker News_202009](https://news.ycombinator.com/item?id=24340802)

- The concept or RxDB, being able to iterate observables of your change stream, is great. 
  - Centering on schemas and typescript is as well. 
  - The broadcast channel based leader election also solved the common issue with Pouch where you can’t respond to real-time changes and update your UI if a separate tab was watching too.

- I always loved how Rx composes with IO on the client side, this looks like the missing half. I hope it survives.
- 👉🏻 Subscribe-on-update databases are, almost by definition, problematic to use at scale as a generic storage solution. 
  - The fundamental problem is that they do not solve many real world problems efficiently enough to warrant the significantly higher running cost. 
  - Of course there are exceptions but it'll be hard to launch a MongoDB type of product that uses a subscription only model(see Firebase RTDB and its problems and lack of adoption in this space)
- The reason developers gravitate towards subscription/rx based paradigms is because it results in very clean architecture and code. Unfortunately it comes at a cost which increases rather than decreases per client/user when volume increases. Some companies or projects can absorb that cost but not all, and typically less so when the project or its userbase grows.
- A subscription based model will do work whenever data changes for each subscriber whereas more traditional pull based architectures only do work when a client specifically needs the data. This can be mitigated to some extent by being micromanaging subscriptions but that kills most of the value of the model.
- There are also plenty of issues with this model if multiple clients are allowed to write to the same data which every single example project seems to try and do. There's a reason master-master updates, consensus algorithms and CRDTs all come at significant cost. It's usually hard. And when it's easy you probably don't need it subscribe-on-update in the first place.

- In fact the pull based approach is doing work all the time to process all the polling. A push based approach only does work when needed (when data changes).
  - I’m not saying it’s not new or hard to scale. I’m just saying objectively(客观地) that push based is more efficient at least in terms of raw data sent down the wire

- What's the advantage of this over triggers in a relational database? Or even notify/listen in PostgreSQL? (assuming these triggers are connected to the API, of course). I guess it's probably a matter of scale, but I really don't know.
  - It runs fully on the client and is offline first. A listener to PostgreSQL will not work when the device goes offline.
- so what about triggers on a sqlite db on the client?
  - There is a big difference between having a changestream of writes to the database, and observing results of multiple queries.

- I don't see any authentification related suff like pouchDB have, like create an user with password hash, auto handle cookie in the browser, restrict document to user or group.

- ## 🔥 [Rxdb: A reactive database where you can subscribe to the result of a query | Hacker News_201910](https://news.ycombinator.com/item?id=21353020)

- I have been developing something that provides this functionality for PostgreSQL: https://github.com/supabase/realtime /Elixir
  - It's very similar to Debezium (mentioned in another comment), but it's built with Phoenix (elixir), so great for listening via websockets.
  - Basically the Phoenix server listens to PostgreSQL's replication functionality and converts the byte stream into JSON which it then broadcasts over websockets. This is great since you can scale the Phoenix servers without any additional load on your DB. Also it doesn't require wal2json (a Postgres extension). 
  - The beauty of listening to the replication functionality is that you can make changes to your database from anywhere - your api, directly in the DB, via a console etc - and you will still receive the changes via Phoenix.
- There is a big difference between the changestream of many SQL and noSQL databases, and what RxDB does. Having a stream of changes is useful but not the whole solution. 
  - RxDB is capable of using single document changes of a stream and recalculate the new results of an existing query. This saves you not only much IO performance but makes developing much easier
  - It is implemented with something called QueryChangeDetection 
  - This is based on meteors oplog-observe-driver
  - So basically when a change-event comes, RxDB does not run the query against the database again, but instead uses the old results together with the event to calculate the new results.

- If you want a change-stream out of your regular MySQL or PostgreSQL database systems, check out Debezium: https://debezium.io/
  - It basically registers itself as a fake replica server so that it can get updates from the master (like binlog in case of MySQL) and then it forwards those updates to Kafka. The possibilities are endless what you can do with those updates as Kafka consumers.

- Having client state just be a replica of server state solves so many problems I don't understand why the concept never caught on. Pouchdb/couchdb are still the only ones doing it afaik. Instead we have a bajillion layers of CRUD all in slightly different protocols just to do the same read or write to the database.
  - When your data is public and immutable, this approach is very pleasant. The client becomes just another caching layer and worst case it's presenting a historical version of the truth. You can even extend this across tabs with things like local storage. This breaks down quickly once you have data that could become private or mutate rather than append.
- The "one db per user" model for private data made using other features like views etc more difficult when you have to upgrade, edit, remove them.
  - Yeah, couchdb more or less requires you to replicate data for individual users if you need complex permissions and want the user to access the couchdb directly.
  - Permissions in general need to be handled by custom reconciliation functions (dropping unauthorized changes) or some kind of nanny system that can react to changes.
  - The much simpler solution of course is to not let the users have any write access to the couchdb and just use a REST API. But then you loose much of the benefits of couchdb...
- I think the Firebase Realtime Database and Firestore have a good model for offline and being able to have private and mutable data. It does get complex but the Firebase SDKs do the heavy lifting for you here.
  - You do need to have you ACL data also stored in the database, which can be a hassle if you have existing ACL system already built outside of Firebase.

- You do need to have you ACL data also stored in the database, which can be a hassle if you have existing ACL system already built outside of Firebase.

- Data security is a huge issue, Facebook.com has very specific whitelisted access patterns encoded as CRUD endpoints. 

- General question about reacting to database events: It seems like when responding to DB events it would be easy to accidentally create an infinite loop. Is that an issue with this pattern, or is it easy to avoid? Do any of these data subscription tools have safeguards in place to prevent this?
  - This is where command and query (with subscribe) must be neatly separated. An event A launches an updates of the DB, that launches the query part to react, then stop. There is the risk of having an infinite loop, if the event A is launched by the query part, which is very related to the behavior of your app.

- Meteor do this since inception with MongoDB on server and MiniMongo in client.
  - Yes, mongodb and meteor and minimongo do something similar but with much more restrictions on what you can do.
  - RxDB does exactly one thing which is being a client side database. You are not tied to a specific ecosystem or backend database.
- Yeah, with RxDB, we are tied with RxJS, PouchDB and CouchDB.

- I have made something similar trying to match more the concept of a materialized view, but just on the client instead of inside the database: https://github.com/tozd/node-reactive-postgres

- ## [RxDB – Local JavaScript-Database | Hacker News_201701](https://news.ycombinator.com/item?id=13507367)
- Before I started creating RxDB, I used pouchdb, minimongo, gunJS and lokiDB and had just too many things to handle by myself. RxDB is an approach to create a database which is easier to use and does not create discussing-point when using it in a big team.

- 🤔 Possible replacement for Meteor's minimongo?
  - It depends. **RxDB can be used completely serverless, while minimongo always needs a stream to the server**. But minimongo is better integrated into your meteor-server-side. The approach of RxDB is to fullfill the principles of offline-first
