---
title: lib-collab-community-sync
tags: [collaboration, community, synchronization]
created: 2022-11-29T20:41:00.894Z
modified: 2022-11-29T20:41:25.566Z
---

# lib-collab-community-sync

# guide

# discuss
- ## 

- ## 

- ## [TinyBase v2.0: reactive data store for local-first apps | Hacker News_202209](https://news.ycombinator.com/item?id=32871392)
- RxDB with PouchDB has support for typescript, json schema, and binary attachments. Moving the attachments to the file system will be up to you.

- I’m my limited experience, a reliable CRDT implementation necessitates a CDRT-first design baked into the core of any data / transaction model. Like I’ve heard some game developers say- multiplayer needs to come first because tacking it onto a single player game is a nightmare.

- ### [CRDTs for tinybase_202209](https://github.com/tinyplex/tinybase/discussions/31)
- I've had to do a bunch of background reading. Still not sure of quite the right strategy yet... 
  - but in our favor we have the fact that TinyBase can listen and update on a cellular granularity, reducing the likely conflicts per row or table.
- The current checkpoints module is an example of keeping a sequence of cell-level changes like that (and it handles deletes a charm). But I need to think about what a flexible API to get or replay such a log in a CRDT context would look like.
- I've started a dedicated disposable repo for these half-baked ideas. 
  - https://github.com/tinyplex/tinysync

- ## [Couchdb有在实际生产环境中使用的例子吗？ - 知乎](https://www.zhihu.com/question/20112928/answers/updated)
- CouchDB是HTTP Restful API来操作数据库的，其它数据库系统使用TCP，在传输大量数据的情况下，HTTP协议在TCP协议之上，可能HTTP协议会比数据库自身实现的数据交互协议payload要大，造成网络性能略差

- ## [Ask HN: The state of Firebase alternatives in 2020? | Hacker News](https://news.ycombinator.com/item?id=24843664)
- There really isn’t a competitor. 
- Supabase is trying to combine OSS tooling into a somewhat similar offering but it’s not nearly as feature rich as Firebase. 
  - That having been said, most people use Firebase for real time DB and auth, and Supabase supports that now. 
  - It doesn’t, however, support offline use cases, or any of the advanced functionality of firebase.
- Pouch and couch solve the offline data scenario and live replication, but no auth story and the mapping of users to data is problematic (unless you build a proxy layer, there’s not an easy way to have some data be public, some private, and some shared).
- Realm is paid these days, I believe, and it solves the data replication, but again, no auth.

- ## [meteor: Improve offline support_202110](https://github.com/meteor/meteor/discussions/11656)
  - With Minimongo there is a touch of offline support. This could be taken further and improved. First step most likely being the ability to not loose offline only changes when the app is closed and then improved syncing once connection is restored. The final step possibly being that you could create offline-first Meteor app.
  - There is also Hoodie which uses PouchDB and CouchDB as a pair to achieve this

- ## [Nano-SQL: Offline use with Sync to Server_201801](https://github.com/only-cliches/Nano-SQL/issues/18)
- Hey gents, I'm getting close to implementing this as a core feature.
- [Here's what I'm thinking:](https://github.com/only-cliches/Nano-SQL/issues/18#issuecomment-392220931)
  - 1. Implement a conflict resolution feature nearly identical to CouchDB that works on the client and the server. 
  - 2. Use websockets with ajax polling fallback to allow syncing between client side databases and servers alike. 
  - 3. Include a simple JSON Web Tokens feature in the client/server model with security baked in. 
  - 4. Make three way data binding super simple using the new observer feature
- I don't think we actually include any conflict resolution code, I really like CouchDBs approach 
  - here where if a record is conflicting at all, everything gets saved as revisions of that row and a winner is selected in a deterministic way. 
  - This lets the application developers handle conflict resolution in a way that suits their use case, prevents the build from bloating into hundreds of kilobytes and prevents loss of data.

- One of the "big deal" features for me that I haven't really seen in CouchDB, Gun and many others is a flexible security model, they seem to almost exclusively be all or nothing. 
  - Let me give you a very simple example: a system with blog posts like Wordpress. Everyone should have read capability, but only specific users should have write capability
  - These are the kinds of problems I'd like to solve with nanoSQL's offline/syncing system, and honestly where I've seen many of the existing solutions fall short.
- This is definitely an issue that Gun does not resolve. 
  - CouchDB does this though. 
  - Using a revision history for a document. 
  - In projects I have worked on revisions are kept for historical purposes. And could be used for manually merging or choosing revisions. 
  - So in any storage engine that Nano-SQL uses a revisions table for all changes(or one for each table's changes) could be managed to provide a history. 
  - However conflict determination would need to take place so that we can let the User know if a conflict occurred and let them take action if they are allowed to.

- Unfortunately implementing offline db use and eventual consistency is a fairly complex beast. 
  - Multiple users can have updated the server while you are offline, so the server needs to keep track of this. 
  - The clients need a way of finding out what has changed since they were last online and if there updates are newer, push them to the server. 
  - Deletes also need to be handled. 
  - Couch uses sequence numbers for part of this.
- Some articles etc. which will help here are:
http://docs.couchdb.org/en/2.1.1/replication/protocol.html
couchbase/couchbase-lite-ios/wiki/Replication-Algorithm (maybe out of date)
http://offlinefirst.org/sync
npmjs.com/package/dexie-syncable (possibly what I'll end up using)
share/sharedb
paldepind/synceddb
kinto.readthedocs.io/en/stable
forbesmyester/SyncIt
- Browser/Server communication should be abstracted so either http or websockets can be used. In Clibu I use Websockets.

- yjs. There is a good CRDT imlemenation that allows 100% synchronisation. 
  - Its used in production and very easy to use.
  - I really think you should look at this, because its a leap frog technology. The way CouchDB and others work is to use the `Last Write Wins` which does not guarantee that all changes on a type ( or datbase row as it were) that are from many offline users does resolve without anyones data being overwritten.
  - 👉🏻 The interesting thing about y.js is that all the reconciliation happens clientside.
  - This means that server side you can either hold the "last know version of a type" or hold all versions known to be out there. You can do either depending on the use case.

- yjs is interesting and works well, however I have several concerns. 
  - The changes stored in IndexedDb etc. appear to grow forever. I posted on Gitter back on Mar 13 and have not had a response. This level of support which just seems to be a single developer is another concern.
- Automerge is impressive but really only suitable for in memory objects. 
  - So for example if you want to merge database doc's for offline use it isn't suitable. 
  - Also I think it's memory use keeps growing with every change. ie. No garbage collection as @gedw99 mentioned.
- hypercore which is part of DAT seems only suitable for synchronizing files, not JS Objects or Database documents.
- Orbit.js
  - I can't see any way to specify/use database indexes. I've written a Gitter post on this. 21 Feb 18
  - It looks like all data is kept in memory which can be backed up to various stores, such as IndexedDB. However I can't see that it is possible to lose the in-memory store/cache and just use IndexedDB?
  - I can't find any documentation on how synchronization works. Latest wins, CRDT ...?  Docs say it can be used to sync editor content?
- I have real trouble thinking of GunDB as a "real" database.
  - To me it is more of a distributed in-memory cache. 
  - It has no query language, no indexes and the entire "DB" is in memory. 
  - Further it is unreliable - see this long outstanding issue
- Another new entrant is TurtleDB, which has very good docs and this article however as it is unusable for my specific use case. It is also an all-in-one library vs. separate independent modules as per your comment.

- There's also an actor based model of sync and state.
  - I can't really write much more about it right now (gotta run) but hopefully I'll remember to later.
  - Here's a project that implements this system http://ceptr.org/projects/holochain#local-source-chain
  - https://github.com/holochain/holochain-proto

- If remote sync is implemented I think it could make Nano-SQL an excellent choice for progressive web apps (PWAs).
- These are some of the alternatives I have evaluated and in my opinion their pros and cons:

- https://github.com/amark/gun
  - An open source cybersecurity protocol for syncing decentralized graph data.
  - GUN is an ecosystem of tools that let you build community run and encrypted applications - like an Open Source Firebase or a Decentralized Dropbox.
  - No support for relationships, join queries nor aggregate queries
- https://github.com/dfahlander/Dexie.js
  - Limited support for relationships and no support of join nor agregate queries
- https://github.com/google/lovefield
  - No remote sync, can use either a local or a remote adapter

- `Dexie.Syncable` the Sync Server just uses Nedb as a quick way to get a sample running. You would replace that with MongoDB or whatever backend DB you wanted so you con isn't relevant here.
- Automerge is indeed impressive however last I looked (and asked) it only works with in-memory objects and isn't durable as @gedw99 mentioned.
- Like y-js I'm also concerned about lack of garbage collection with automerge which could end up consuming a lot of memory if the objects are a reasonable size and change frequently. For example a 5KB Markdown document which was edited 20 times (in a day) would use 100KB + metadata.
- Logux is another library I've been evaluating and not had time to mention before (been travelling) but shows promise. 
  - What I like about Logux, is it is completely independent of the front/backend database. Which `Dexie.Syncable` is largely.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
