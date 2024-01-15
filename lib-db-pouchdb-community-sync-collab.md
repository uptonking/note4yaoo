---
title: lib-db-pouchdb-community-sync-collab
tags: [collaboration, community, data-sync, pouchdb, synchronization]
created: 2023-10-29T02:22:33.200Z
modified: 2023-10-29T02:22:57.939Z
---

# lib-db-pouchdb-community-sync-collab

# guide

# discuss-stars
- ## 

- ## [First class conflict handling · apache/couchdb_201808](https://github.com/apache/couchdb/issues/1507)
- tldr
  - rev-tree -> rev-graph (more git like)
- As a bit of background, our current revision model is a standard tree. 
  - The biggest issue we've seen customers have with using CouchDB "normally" is when they have a work load that generates conflicts with regularity. This ends up creating revision trees with many thousands of revisions with no general bound on growth of the tree. Eventually a single document can take many seconds to minutes to update as the tree has to be read from disk, updated, and then written back to disk. 
  - The only effective solution to this currently is to have an operator manually purge revisions from the document.
- The best solution I've come across to this issue would be to change our revision model to be a graph. Then instead of resolving conflicts by deleting a revision, the conflict is resolved by making an update that references two or more revisions. In this way a customer that generates a large number of conflicts can easily resolve the situation during their normal conflict resolution process. 
  - While this approach is fairly straight forward in theory, the difficult part is how we'd want to handle backwards compatibility with replication. So far I could see having a replicator that could translate new revision graphs to old revision trees by "undoing" merge changes and created the equivalent of the old "deleted revision" logic. However, I don't see a way that we could go from the old format back to the graph (ie, think about replicating a new style graph doc through an old CouchDB version back to a new graph doc and end up with the same doc).
- I finally had time to read the automerge JSON CRDT paper. It is certainly very promising, but not production ready yet. The algorithm doesn’t account for a few unbounded lists happening. And it currently skips of required tombstone removal.
  - The biggest caveat so far is that it requires all replicas to eventually converge towards the same state. While that might be a good enough limitation for many cases, it is less general than what CouchDB supports today. The authors promise continued work and we should keep watching this closely.

- ## [Automerge: A JSON-like data structure (a CRDT) that can be modified concurrently_202202](https://news.ycombinator.com/item?id=30412550)
- I think CouchDB/PouchDB do this similarly, the winner is deterministic though?
  - CouchDB and PouchDB have no idea how to merge a conflict, if two copies are edited prior to syncing, one version it marked as the 'winner' and the other as a conflict version. 
  - As the developer you can then either chose to dispose(丢掉; 处理) of conflicts or have your own way of merging them.
  - This is actually a perfect use case for CRDTs such as Automerge and Yjs, I actually built a proof of concept combining Yjs with PouchDB to handle the conflicting edits

- ## [Why the CHT uses CouchDB - Product - Community Health Toolkit_202208](https://forum.communityhealthtoolkit.org/t/why-the-cht-uses-couchdb/2113)
- A lot has changed in the CHT since it launched over 10 years ago. However one thing that has remained the same is the use of CouchDB as the primary database. While there are many database options available each with different strengths and weaknesses, CouchDB meets many of the requirements for the CHT.

- 🌹 Benefits of CouchDB
- Offline first applications
  - One of the main advantages of CouchDB is it provides a robust master-to-master replication protocol out of the box
  - This works seamlessly with PouchDB
- Schemaless
  - The CHT has always been highly configurable, particularly with the structure of the data being collected.
- Clustering
  - CouchDB natively supports clustering to balance the load over multiple machines. While the CHT doesn’t yet support database clustering 
- APIs
  - Virtually anything is possible with their extensive list of APIs, and using REST means there are a wide range of tools to make scripting and integration easy.

- 🐛 Downsides of CouchDB
- Filtered replication
  - CHWs should only see a portion of the data on the server database. This is for two reasons; the phone can’t physically store as much data as the server, and for privacy reasons the user should only be able to access the information required for their job. 
  - To accomplish this the CHT filters the replication to just a specific list of document IDs. Unfortunately this doesn’t perform well at scale. 
  - The reason is quite technical but essentially every user has to skip over all the documents uploaded by other users to get to just the data they should sync. 
  - As filtered replication makes up the majority of requests to the server this is a significant limitation. 
  - Incremental improvements have been made to improve how filtering is done but more improvements are now needed to reach the increasing scale of CHT deployments.
- Data queries
  - The other main limitation is it’s very difficult to do certain queries on CouchDB, for example for bespoke investigations or data dashboards. 
  - To mitigate this it is recommended to sync the data to a data warehouse which better supports these sorts of queries.
- Views are slow to build
  - CouchDB uses map/reduce views which are indexed by executing a function on every document in the database and caching the result, which makes them quick and easy to query. 
  - However if a new view is created, or an existing view is updated with a new index function, then the cache needs to be updated for every document in the database, which can take a very long time. 
  - This limitation is mitigated in the CHT by querying by ID when possible, by reusing views in preference to creating new ones, and by implementing view warming on upgrade so the reindexing can happen without any downtime.
- The future
  - In the near term the CHT will a) support clustering, b) be upgrade to use the latest version of CouchDB, and c) undergo investigation to further improve the filtered replication algorithm that is currently limiting scale. 
  - Additionally work is ongoing to develop a data pipeline product which will sync data to PostgreSQL for easy to develop and efficient to execute queries. 
  - These changes will help mitigate the two downsides listed above.
- Further in the future it’s quite possible the CHT will be modified to use a different database altogether. This would be a large project requiring a significant amount of code changes and have inherent risks, but this will be weighed against the benefits it would bring.

- Which would be a good way to sync data between couchDB and a data warehouse like big query without the postgresql instance ?
  - Actually we are ingesting data to bigquery from postgresql views and matviews in a daily basis, but we get often our ingestions tasks refused by the postgresql server ‘too many connexion for user’ even if we dont use any paralelisme , I mean, we ingest data from one view, once finished we ingest from another one, one by one
- Getting data out of couchdb is reasonably straightforward using the changes API. This then needs to be directed to your data warehouse. The next generation version of this for the CHT → PG is cht-sync which should be reasonably easy to modify for whatever data store you want.

- ## [PouchDB differential sync speed very slow_201812](https://github.com/pouchdb/pouchdb/issues/7578) 
- CouchDB replication is pretty chatty yeah, though there were some serious improvements in the 1. X -> 2. X upgrade.
  - If you were sideloading the data i'd expect it to be chatty (see protocol)
- The reality about using PouchDB is that most applications can take shortcuts, that we avoid for the general replication case, that aims to be a working thing for all kinds of use cases. For example if you're only loading data one way, or if you have a large initial load, you can make an `allDocs` request and then write the first checkpoint manually.

- ## [RFC: ideas for replication performance improvements · pouchdb/pouchdb_201703](https://github.com/pouchdb/pouchdb/issues/6316)
- CouchDB 2 only slightly improves perf over CouchDB 1, because _bulk_get is actually only used in cases of conflicts now (edit: also attachments and non-gen-1 docs, thanks @willholley), since we use _all_docs whenever possible. In my test set of npm skimdb docs, the vast majority of docs can be fetched with _all_docs rather than _bulk_get.
- H2 does not seem to improve much over HTTP1, because we're not extremely chatty and we're not hitting 6-parallel-requests-per-origin limits or other standard H1 problems.
- conclusion: So overall, I don't see HTTP/2 as a magic pill that's going to fix all our performance problems (sadly). No doubt it removes the overhead of HTTP headers, connection latency, etc., but to really get good replication perf I think we need to overhaul the replication algorithm itself.

- I also think we could make a new replication protocol that is vastly less chatty, its still just a thought and havent fleshed it out, unlikely to do so until idb-next is done but briefly outlined it 

- ## [Selective sync · janl/couchdb-next_201702](https://github.com/janl/couchdb-next/issues/14)
- I wonder if replication via view vs _changes might something to consider here. I know we have some view based replication stuff on 1.6 but AFAIK that was basically just to only replicate things in a view. I'm thinking more along the lines of that we just follow the key order in a view and then clients can specify a view and any complex logic they want. Last 90 days for instance could be something like emit(doc.date, null) and then replicate using a start_seq of now() - 90 days

- Anything that requires create view is fairly prohibitive imo, both in terms of performance of view generation and for the amount of work developers need to go through to get it working, there are quite a lot of replication improvements we can do via clever filtering already and they arent done because setting up a filter (and understanding the replication protocol enough to know what to do) is hard enough.
  - We are moving away from views / map reduce in pouchdb in general so I would like to avoid them being further depended on in core functionality

- That's fair. And in hindsight a view doesn't really give us a whole lot over a filter anyway. I'd agree with you that looking at improving filters would likely be the better approach.
# discuss-sync-non-couch
- ## 

- ## 

- ## [oracle support_201606](https://github.com/pouchdb/pouchdb/issues/5283)
- Yep, you could write a custom adapter ala pouchdb-adapter-node-websql and using the node-websql custom API. However I doubt very much it would work since the adapter uses SQLite and not generic SQL, e.g. it even reads from the sqlite_master database which does not exist in Oracle.
  - And in general: no, I don't think this is a good idea. I think most people who try to get MySQL/Postgres/Oracle/etc. working with PouchDB actually just want an easy and familiar way to query their database using SQL (since CouchDB views are so complicated by comparison). For that, you can just write a cron job to periodically dump CouchDB to a SQL database in whatever format you want, and then you have a nice queryable view on your data. Piece of cake! 

- ## [Feature request: Redis adaptor_201401](https://github.com/pouchdb/pouchdb/issues/1242)
- I suspect pouch as it is in the current iteration will only ever be able to sync with couchdb compatible servers, a 'high performace node.js cluster' would be possible with improvements to the leveldb implementation of pouchdb + pouchdb-server.
  - I can see a lighter version of pouchdb that doesnt have support for being a full peer, or the opposite which doesnt require the server to be a full peer and can sync over redis / mysql etc, however that starts chipping(削下，凿下) at a lot of assumptions and implementation details of what pouchdb is, I think they would be best started as separate projects

- The usage case for this is primarily for low-latency queries. The advantage of Redis is that it is a memory store, so data can be queried much faster, with much higher through-put. 
  - To my knowledge LevelDB stores data on disk, so it is not likely to have performance benefits over a vanilla CouchDB server.
  - I'm not suggesting that PouchDB sync with Redis, I am proposing that it could be used instead of LevelDB to persist the data of the PouchDB instance -- and that the same Redis instance can be shared across hundreds of Node workers.

- As an aside, this sounds like a perfect candidate for a PouchDB plugin. I foresee lots of cool backend adapters being written for Pouch: Redis, S3, localStorage - why not? But I imagine the core will always be couch/websql/idb/leveldb

- ## [Support For Sync Between MyServer and CouchDb_201606](https://github.com/pouchdb/pouchdb/issues/5301)
- PouchDB cant sync with MongoDB/MySQL/my current non-CouchDB database as backend needs to speak the CouchDB replication protocol.
  - However there is a way to replicate the changes made in couchDb with mysql npmjs.com/package/couchdb-to-mysql
  - My Question is; Is there a way to replicate the changes made in mysql to replicate within couchDb?

- It isnt something that is or will be supported by pouchdb / couchdb in the short term, mysql has no concept of revisions, it will be possible to have PouchDB <-> CouchDB <-> My custom couch to mysql sync that handles business / revision logic <-> MySQL, and there may be some tools around to help you do that although unlikely to be generic as they are fundamentally different data models. Closing this out as its something that isnt going to be tracked by us, but feel free to continue discussing in here

- Check out kesla/mysqldown although your mileage may vary because we've never tested it.
  - https://github.com/kesla/mysqldown /201307/js
    - An drop-in replacement for LevelDOWN that works in mysql

- ## [pouchdb without couchdb / replication_201504](https://github.com/pouchdb/pouchdb-server/issues/96)

- MongoDOWN/DynamoDOWN/etc. are neat, but you probably don't want them for a production server. 👉🏻 They're pretty inefficient due to everything being through the key-value LevelUP API. And yeah, as Dale said, you can't actually use those databases directly; you still have to use the Pouch API.
  - If you want massive scaling, then you're in luck, because by design CouchDB/pouchdb-server can scale horizontally almost infinitely. Run out of capacity? Just spin up another instance and replicate to it. It's master-master, so you never have a single server being your bottleneck.
- The LevelDOWN API assumes a basic key-value store, which is perfectly suited for LevelDB. But when you use such an API over MongoDB (i.e. MongoDOWN), it's not making the best use of Mongo's API because it's only using a tiny subset of it. It's basically ignoring the entire API and using the database as a simple Btree.
  - To be clear: anybody who wants to use a *DOWN database with pouchdb-server is absolutely welcome to, but I have not found one that gives any real benefit over the built-in LevelDOWN engine, except MemDOWN for obvious reasons.

- We've been using Couch/Pouch with provision(供应, 提供) couch per user, works well. Some issues with sync state, but mostly very solid. 
  - And then in ExpressJS, you can mount Couchdb and get the data into Mongo via express. 
  - That way, Couchdb and the Pouch clients are just there to keep the "truth" datastore data, mongodb in our case, replicating to clients. 
  - So Couch/Pouch are sort of like a better version of AWS Cognito or a replicating datastore, but we use Mongo/Express to hold the data for real and permanently.

- I'm going to close this; it is definitely not our roadmap. SQLite is an embedded database, hence makes perfect sense as an underlying backing store. 
  - Postgres and MySQL backend doesn't make sense for various reasons including pouchdb.com/faq.html#sync_non_couchdb and also the fact that it doesn't solve the problem people really want to solve, which is that they want to use the SQL API to their favorite database and have PouchDB magically sync it, which is not possible due to CouchDB's revision semantics.

- ## [Using PouchDB with MongoDB - Stack Overflow_201508](https://stackoverflow.com/questions/24384803/using-pouchdb-with-mongodb)
- The short answer is: no, there's no way to get a PouchDB that you can just plug into your existing MongoDB database. You might want to try Meteor.js instead.
  - The long answer is that CouchDB and MongoDB are not equivalent, and in particular CouchDB is designed from the bottom-up to be used for synchronization. There's a good write-up by Jan Lenhardt that explains how it works. Part of the magic of PouchDB/CouchDB sync comes from this design, which Mongo does not have.
  - In fact, 👉🏻 even if PouchDB used Mongo as a backend (which is not outside of the realm of possibility; we already support Redis and Riak), you would not be able to use your existing database as-is, since PouchDB would need to reconstruct this revision-handling schema over Mongo. Hence you would have to rewrite your app to use the PouchDB/CouchDB API.
- Redis and Riak are "supported" in the sense that PouchDB can use them as a storage engine. It's only really interesting for academic reasons, though; you wouldn't want to actually use it in production, 👉🏻 because PouchDB is basically using them as dumb key-value stores, and you can't actually directly use those databases - instead you need to use PouchDB's abstraction over them. 

- I saw the minimongo project. I didn't try it yet. As far as I understand it's the same minimongo that is used in the meteor project. The project description says that it has server sync over http. But it doesn't have persistence, indexes.

- ## 🍃 [pouchDb + MongoDB_201809](https://github.com/pouchdb/pouchdb/issues/7466)
  - how can I use the frontend in the pouchDb with synchronization, for my MongoDb backend database?

- PouchDB won’t sync with Mongodb. You need to run CouchDB on the backend.

- how the final solution looks is extremely tied to the rest of your app, but in general:
- you wanna listen to the changes feed on the couchdb
  - there are 2 ways to do this:
  - read at a for example 5 minute interval, and store the last_seq that you read somewhere. Then on next read you need to start from the last checkpoint you read.
  - read via a live changes feed. if you do this, you need to prepare for what happens if you need to read changes from the start. That means, you have to have a way to make sure you don't write everything to your MongoDB once again (so you dont get duplicate data)
- On every change you need to decide what to do with it. Can you look up if something is already written? do you need to update it or do you need to write something new?
- From experience, it's helpful to design this in a way that you can re-run the import and get the same results from the same data. If you have a production system with MongoDB data and you run the import from sequence number 0 again, what happens then?
# discuss
- ## 

- ## [Syncing PouchDB offline to PostgreSQL - Stack Overflow](https://stackoverflow.com/questions/38371590/syncing-pouchdb-offline-to-postgresql)
- Short answer: You can't. It's impossible. Give up. You need CouchDB.
- Long answer: You have two options:
  - you can implement a custom replicator for PouchDB (it is just a PouchDB plugin -- that can get complicated, but not necessarily --, see the default Pouch-Couch replicator source code)
  - you can set up a backend service that acts as a proxy between PouchDB and Postgres, that will basically require you to understand and implement the CouchDB replication protocol, i.e., you'll need a server with a bunch of HTTP endpoints that return exactly what the PouchDB replicator expects.

- Another possibility (which may or may not work with your use case, depending on how your data is structured):
  - You can move some of your data (just what needs to sync to the browser) to CouchDB, but give Postgres access to it through the Foreign Data Wrappers feature in Postgres, so that you don't need to convert your entire app to putting everything in CouchDB, and you don't lose the benefits of a relational database.

- ## [Make `_rev` generation deterministic (similar to CouchDB)_201512](https://github.com/pouchdb/pouchdb/issues/4642)
  - PouchDB currently generates _rev values using a uuid. This presents problems when, for instance, an application has conflict resolution logic which might run on different devices concurrently (because they would both resolve the conflict but, in doing so, generate a new one).
  - CouchDB has an optimisation here where the _rev is deterministic, based on the contents of the document, attachments, deleted flag and rev history
  - It would be useful for PouchDB to have a similarly deterministic rev generation, though it's not really necessary to match the CouchDB one.

- ## in the pouch/couch model this will create a conflict that apps need to resolve, because they can’t know if the server or the client has the “correct” lastest change.
- https://twitter.com/CouchDB/status/1313857978181844992
- see [Use JSON Patch to Resolve Conflicts for CouchDB](https://neighbourhood.ie/blog/2020/09/15/use-json-patch-to-resolve-conflicts/) for automating some of that conflict resolution.

- ## Has anyone here ever used PouchDB, or some other IndexedDB adapter to create a distributed sort of "peer-to-peer" database? 
- https://twitter.com/BenLesh/status/1316085574697136128
- gundb should help you with p2p stuff
- CRDT 
- https://github.com/natevw/PeerPouch /js/inactive
  - A plugin for PouchDB which allows a remote PouchDB instance to be used locally. 
  - It transfers data over WebRTC, for simple lower-latency remote access and even particularly peer-to-peer replication!

- ## Anyone have experience using automerge CRDT in their apps for offline mode and cross-device sync? Would you recommend it over something like PouchDB/CouchDB? _202011
- https://twitter.com/andrey_butov/status/1333419124878417920
  - The one-db-per-user with proxy-auth approach is a bit hard to swallow.
- I don't use automerge, I use my own crdt implementation. I'm happy with it, but I'd only recommend it if local apps give you a real advantage. It is difficult to make schema changes some features are hard without a centralized point
  - but the payoff is very good, so it's worth it if you can take on the challenges. For auth, I just use my centralized server for that.

- ## [LevelUP Proposal_201401](https://github.com/pouchdb/pouchdb/issues/1250)
- theres work to experiment using a level based backend 

- ## [Sync Issue](https://github.com/pouchdb/pouchdb/issues/5291)
  - would like to know if theres a way to sync between local and remote db's only some specific documents, and only some specific attributes in each document, instead of the default behavior that syncs every document and attribute ?

- Sounds like you want to do a filtered replication
- In CouchDB (and PouchDB) there is a concept of a design document, this can give you a partial representation of your database (like a view).

- ## [how to to do partial (descending)l sync? F.e. chat messages](https://github.com/pouchdb/pouchdb/issues/8221)
  - Imagine I have chat app, and chat may have potentially million of messages in a room. What is a best practice to sync such a database to web browser? Is it possible to sync f.e. last 1000 messages, then if user scrolls, resync last 2000 messages?
  - As I understand I can achieve this passing query_selector to replicate method, but the question is, will it resync items with sequence_number lower then last sync? I mean will it sync oldest messages after newer message was synced?

- You can use filtered replication

- ## [Automatic Conflict Resolution_202008](https://github.com/pouchdb/pouchdb/issues/8163)
- There is a plugin for pouchdb that helps with conflict resolution
  - https://github.com/pouchdb/upsert
  - There is also a guide in the pouchdb docs about using upserts to help manage conflicts. 
- There's a big difference: 
  - 👉🏻 C/PouchDB's Conflict resultion suggestion is to **use an arbitrary version of two conflicting items** (I think on default it is to just ignore conflicts). 
  - Ex: JSON Item A and JSON Item B have both the same rev number when they want to be added to the main database. 
  - Since both have different changes, only one item can be used (like the last submitted). In contrast, automerge would look for the differences in the actual JSON objects, and automatically merge both, so that the latest changes of each version is added to the database.

- 👉🏻 This looks to me like what https://github.com/redgeoff/delta-pouch does. 
  - It saves the changes in order and syncs the changes. 
  - The data is a result of all changes applied in order. 
  - It is mentioned in PouchDB Conflicts guide.

- ## 🤔 [I think CouchDB/PouchDB do this similarly, the winner is deterministic though? | Hacker News](https://news.ycombinator.com/item?id=30414871)
- CouchDB and PouchDB have no idea how to merge a conflict, if two copies are edited prior to syncing, one version it marked as the 'winner' and the other as a conflict version. As the developer you can then either chose to dispose of conflicts or have your own way of merging them.
- This is actually a perfect use case for CRDTs such as Automerge and Yjs, I actually built a proof of concept combining Yjs with PouchDB to handle the conflicting edits

- ## 💡 [Distributed offline editing with couch/pouchdb - Yjs Community_202101](https://discuss.yjs.dev/t/distributed-offline-editing-with-couch-pouchdb/340)
  - Has anyone experimented with using Yjs with pouchdb as both the datastore and communication channel?

- I’m starting to try to build a PouchDB provider and plug-in for Yjs. My plan is that a Y.doc will manage the whole Pouch document and be included in it as a binary attachment. Then have a top level Y. Map that is also exported to json at save time to build the pouch document, this can then be queried and indexed by the standard pouchdb api. So the user doesn’t ever change the pouch document directly, only the Y.doc, and with that we can get conflict free merges in PouchDB.
  - When fetching a document from pouch we will also fetch all conflicting versions and will merge the Y.docs. Then we watch the pouchdb change feed and continue to merge in changes as they arrive.
  - This method obviously only merges whole document versions, great for offline editing but not real-time where vectors are better. 
  - It seems a combination of this with the websocket or webrtc provider for real-time collaboration would work well. 
  - PouchDB revision keys are deterministic hashes of the document and so if you combine a PouchDB provider with a websocket provider to merge in update vectors, the resulting document will have the same revision number, fully sidestepping(回避问题) the PouchDB/Couchdb sync (also important for the normal pouchdb sync). 
  - We would probably want to ‘pause’ or slow down the save to PouchDB while using a realtime collaborative provider to stop too many full document syncs in the background.
  - I’m also considering having an option for a pre-save extractor function, this would allow you to extract additional data (say from the y-prosemirror doc Y. XmlFragment) and add it to the main pouch json doc for indexing and searching.
- This plan should work well when you have a document open but the area where I have a question is when documents are not open. PouchDB will continue to sync in the background (when the app is open), and we can easily watch the change feed for new version conflicts of unopened documents. When using this with Prosemirror do we need to have the document open in Prosemirror (and have access to a browser DOM) when doing a merge or can we just naively merge the Y.docs? Would this cause a problem with the Prosemirror schema?

- Regarding schema conflicts: When you load an invalid document with y-prosemirror, (e.g. it has two headlines instead of one that is specified in the schema), then y-prosemirror will automatically correct the Yjs document. This will happen automatically (usually by removing the invalid node).

- I’m making good progress, I have a simple version running (using TipTap v2 so I need to check if I can show it yet) that works with open “foreground” documents with both realtime and offline (conflicting) edits. The next job is to have a background conflict manager to handle merging conflicting edits without them being actively open at the time (for example when you go back online after editing multiple documents).
  - As I said before, this works well, but when you have multiple people actively working on a document at once people should probably use the Websocket or WebRTC provider as it will be more efficient and has awareness support (which I don’t think should be built into a PouchDB provider).

- I recommend to mark transactions as remote when the update was created remotely. This is useful meta-information.

- ## 💡 @pouchdb wont lose data, the conflict is stored and reported, both(all) documents available to choose/create winner, 
- https://twitter.com/daleharvey/status/1043057187113848832
  - we do have encryption plugins (https://github.com/calvinmetcalf/crypto-pouch), no server copy however we dont do
- Yeah I know :) but since the version is only stored per-document, not per-field, you will end up losing data. You could try to auto-resolve by ways merging conflicts... but in which order? You can’t be sure and have to ask the user or something
  - By losing data, I mean from the UX perspective. User syncs, from their view the data is gone. Sure it’s internally there, but they’d have to manually bring it back. This is fully conflict free
- 👉🏻 The app decides which conflict resolution to take of which Last Write Wins, Merge strategies, CRDT or Users Choice are various options, tradeoffs involved in giving that choice to the app developer but prefer to not hear people advertising @pouchdb loses data since it doesnt :)
- Fair enough, good to clarify. Still a big problem that versions are document-level and not field-level though, hard to use CRDTs accurately with that
  - 👉🏻 You could have versions be change level if you wanted (https://github.com/redgeoff/delta-pouch), having fields merge and report only on same field changes is a pretty easy thing to write but I would like to see @pouchdb one day expose these choices as far simpler options
- Nice. With last-write-win though, you don't even need to store the entire history of changes, just the latest one. Anyway, all tradeoffs. I was able to still leverage sqlite with very efficient storage of this info. Pouch has different tradeoffs, still good!
