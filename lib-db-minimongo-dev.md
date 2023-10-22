---
title: lib-db-minimongo-dev
tags: [database, minimongo, mongodb]
created: 2022-12-02T11:12:05.223Z
modified: 2022-12-02T11:12:29.905Z
---

# lib-db-minimongo-dev

# guide
- minimongo的示例对应idb中的单张表+多行数据

- minimongo/meteor 的replication协议参考 [Distributed Data Protocol (DDP)](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)
# discuss
- ## 

- ## [10 Years of Meteor | Hacker News_202206](https://news.ycombinator.com/item?id=31915573)
- 100% agree with this post. I also co-authored a book about Meteor.
  - Having methods that can run on either the front end or the back end with basically zero boilerplate was an incredible idea which unfortunately never really got traction. 
  - I don't think that "Database Everywhere" deserves a thumbs down. It's an insanely useful prototyping tool, genuinely useful when trying to replicate reactivity, not to mention extremely performant for all that work it actually did (it sort of "hacked" this by hooking into Mongo's oplog). Meteor's mistake was, imo, mainly deciding to do this with MongoDB instead of a SQL variant.

- Meteor came out before async-await was a thing for Node. Meteor solved the callback hell with fibers. However fibers introduced concurrency bugs. A fiber has pre-emption points when doing IO. If some other code then changes some state then it can be dangerous because of data races.

- Aggregate database queries using Meteor (at least as of 1.0) would create an immense amount of backend overhead if you queried through minimongo. And the overhead was incurred as long as a user was on that page because of how the reactivity worked. I tried making a PR to optimize this but apparently it wasn't comprehensive enough. I kept checking for years but no one attempted to fix this. Before you get nostalgic for Meteor, issues like that were awful. Meteor (and RethinkDB) were just* pub/sub you had almost no control over. Was fun playing around with, though!
  - That's not a Meteor issue. Running aggregations on fact tables at runtime is slow. On top of that, being a document store, mongo is not the best at aggregations. Then instead of using mongo you use minimogo (DB implemented in JS). Then you rerun that query all the time. Of course it'll be slow/expensive.

- ## [If Not SPAs, What? | Hacker News_202010](https://news.ycombinator.com/item?id=24920702)
- Is this the same model meteor.js uses? I seem to recall their system maintains a mini-database on the client side and syncs it with the main server through a pub-sub model.
  - Yes. At least it can use service workers. Meteor uses MongoDB on the backend, and minimongo client side. Those two are synced over their DDP protocol IIRC.
  - Not quite. It's just a client-side cache of query results matching a MongoDB query on the server (pub/sub).

- ## [Ask HN: Is Meteor.js still a thing? | Hacker News_201711](https://news.ycombinator.com/item?id=15624623)
- 🤔 Lot's of people mentioning "reactivity as being expensive/non-scalable". is there a good read up on what reactivity in the context of meteor.js is and why it is expensive ?
- TLDR is:
  - Meteor uses MongoDB as a data store
  - You write queries on the server called "publications", that make documents available to the client
  - The client implements "MiniMongo", which basically lets you query the documents that have been published via your publications using Mongo queries as if you were writing them straight from the server
  - The publications are (by default) reactive, so whenever any of the documents in your queries is added/removed/modified, the changes propagate instantly to your client.
  - The original view library (Blaze) would seamlessly update with these changes in your UI.
- 👉🏻 From memory, the performance bottlenecks here are:
  - It uses the Mongo OpLog to determine when changes have been made to the collections, which makes the queries themselves quite slow.
  - For every dataset published to the client, Mongo keeps a cache of that dataset on the server so it knows when it needs to send deltas over the wire.
  - So for both of these reasons, once your queries get big, they get SLOW.
  - The other thing that is costly (but not fundamentally a fault of Meteor itself), is that most people building web apps model their data in relational terms. If you try and apply that to Mongo, (ie, treating collections as tables and "joining" across them instead of nesting data hierarchically inside your documents), you'll end up writing slow queries.

- ## [Use IndexedDB as alternative storage for minimongo · meteor/meteor-feature-requests](https://github.com/meteor/meteor-feature-requests/issues/407)
- Using IndexedDB as a data-storage for minimongo would give us several advantages, I think, e.g. of automatically having indexes built in
- One major downside I see so far is that many of the calls are asynchronous (based on callbacks) and could therefore only be introduced on the client if we would switch to a promise-based interface for database-calls.
- One issue with IndexedDB is that data has a same origin policy, so if you have multiple tabs open all tabs can see data from all other tabs. This means you have to query Minimongo for exactly what you want instead of just assuming that what's there is only what you're subscribed to. (This is already good practice.)

- ## [Is GroundDB the best for offline storage? - help - Meteor forums_202109](https://forums.meteor.com/t/is-grounddb-the-best-for-offline-storage/56654)
- I found that the internal API in LocalCollection that ground:db uses switched from an object to a Map sometime around Meteor 2.4.
  - I did a from-the-ground-up (pun unintended) rewrite, which I’m calling GroundedCollection. 
  - I switched to Typescript, added the ability to specify compression/decompression functions for writes/reads to IndexedDB, and switched from localforage to Dexie, but otherwise tried to keep the API similar.
  - As a bonus, Dexie allowed me to use bulk reads/writes, which decreased load times by an enormous amount
  - https://gist.github.com/banjerluke/554cb2274c4f55c2254288aa243994ed

- ## 🤔 why Minimongo in Meteor don’t support indexeddb or websql like Minimongo official project?_202101
- https://forums.meteor.com/t/minimongo-and-store/54877
- What would you like to do offline?
  - Minimongo was designed for something different, it is a mirror of a batch of data from Mongo. Minimongo is almost Mongo.
  - Where the whole offline concept fails is when you want to offline-edit a note which is not on your phone. Or if you want to book a ticket offline, paginate some posts, etc. There are so many case that don’t work in any app not only Meteor.
  - Offline we can both generate documents like in a chat.
  - However, when we both have the same document and we both want to edit it offline… if online, there is conflict
  - What I am saying here with this story is that you can very well do a lot of offline, away from Minimongo, using Methods and writing to a local DB (I prefer RealmDB because it is … possibly the best mobile JS DB). It is not that you cannot and it is not that it can be built natively into Meteor (my opinion). This is subject to application design for each an every individual app.

- Is to difficult? is not right to do because is not suitable for Meteor ?
  - One major downside I see so far is that many of the calls are asynchronous (based on callbacks) and could therefore only be introduced on the client if we would switch to a promise-based interface for database-calls.
  - Such a change would force virtually everyone to make a lot of changes to their projects.
- I tested a few of these offline-minimongo packages in the past (at least 3 years back) and I think ground:db was the one that worked for us the most.
