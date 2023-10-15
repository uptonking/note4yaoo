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
# discuss-stars
- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

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

- ## [RxDB – a real-time database on top of PouchDB | Hacker News_202009](https://news.ycombinator.com/item?id=24340802)
- I always loved how Rx composes with IO on the client side, this looks like the missing half. I hope it survives.
  - Subscribe-on-update databases are, almost by definition, problematic to use at scale as a generic storage solution. The fundamental problem is that they do not solve many real world problems efficiently enough to warrant the significantly higher running cost. Of course there are exceptions but it'll be hard to launch a MongoDB type of product that uses a subscription only model 

- ## [RxDB – Local JavaScript-Database | Hacker News_201701](https://news.ycombinator.com/item?id=13507367)
- Before I started creating RxDB, I used pouchdb, minimongo, gunJS and lokiDB and had just too many things to handle by myself. RxDB is an approach to create a database which is easier to use and does not create discussing-point when using it in a big team.

- Possible replacement for Meteor's minimongo?
  - It depends. RxDB can be used completely serverless, while minimongo always needs a stream to the server. But minimongo is better integrated into your meteor-server-side. The approach of RxDB is to fullfill the principles of offline-first
