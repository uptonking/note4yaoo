---
title: lib-db-rxdb-dev
tags: [database, rxdb]
created: 2022-12-02T11:15:20.076Z
modified: 2022-12-02T11:16:05.028Z
---

# lib-db-rxdb-dev

# guide

# discuss
- ## 

- ## 

- ## 

- ## [rxdb: Offline First_202109](https://news.ycombinator.com/item?id=28690427)
- what's a good solution for syncing with the main database after the device goes back online?
- 👉🏻 CouchDB/PouchDB(the JS compatible cousin) make use of a global sequence counter to track which documents have changed between sync.
- Each database uses an arbitrary byte string to mark a position in a sequence of updates to the database. 
  - Each document has the sequence counter of when it was created/updated/deleted. 
  - This sequence counter only matters to that particular database (it does not need to be mirrored, it's just a local ref. of WHEN the doc was modified in that particular database).
- Syncing is then a process of looking up the last read sequence counter from a checkpoint document (i.e. what was the last modification) and passing that sequence counter to the `changes` endpoint to get a list of all documents with a sequence counter AFTER that, and then pulling/pushing those documents to the local/remote database, and saving the new latest sequence counter.
- The official docs give some more info. One key point is if I modify a document several times between syncs, it will only show once in the changes feed with the latest sequence counter for that document. Couch's conflict resolution strategy is a topic for another time, but an interesting one.

- It’s an open question and ultimately depends on your app. 
  - For our mobile app we try to merge simple changes automatically and for trickier ones we allow the user to merge or select changes with a UI, a bit like git. 
  - We try to keep our objects small and granular enough that this very rarely occurs. 
  - For a lot of apps last write wins (e.g compare and always take the lastest timestamp) is enough and probably the most common solution you’ll see but you have to be OK with a certain amount of data loss. 
  - Newer, fancier CRDT based merging solutions are on the horizon, like Automerge for example but I feel they’re a little way off mainstream adoption.

- Earlier this year I experimented [1][2] with combining CRDTs using the incredible yJS[3] with PouchDB. It worked really well, completely magic syncing with full automatic handling of sync conflicts! 
  - [(Alpha) PouchDB integration for Yjs](https://gist.github.com/samwillis/1465da23194d1ad480a5548458864077)

- I think my main problem with PouchDB and by extension CouchDB was that it seemed hard to add validation in the backend (including authentication/authorization). I remember having to build some kind of proxy that hooks into the CouchDB protocol to deny certain requests. I am pretty sure that's solved by now
  - That was a problem I always had with replicating directly to CouchDB. They have added more authentication methods now, like proxy auth and JWT, so authorizing on a per-database basis isn't too bad.
  - However, I gave up on CouchDB after my server kept getting hacked by crypto miners. I'm sure whatever exploit they were using has been patched, but I'm hesitant now to use a DB that's open to the world.

- I still haven't found the "holy grail architecture" for offline-first with backend sync where the backend isn't just a simple data store but also has business logic and interacts with external systems.
  - Doing offline-first well implies that the app has a (sqlite or similar) local database, does work on that database and periodically syncs the changes to the backend. 
  - This means you have N+1 databases to keep in sync (with N=number of clients).
  - When the backend isn't very smart it's not too hard, you can just encapsulate any state-changing action into an event, when offline process the events locally + cache the chain of events, when online send the chain to the backend and have the backend apply the events one by one. Periodically sync new events from the backend and apply them locally to stay in sync. This is what classic Todo apps like OmniFocus do.
  - The problems start when the backend is smarter and also applies business logic that generates new events (for example enriching new entities with data from external systems, or adding new tasks to a timeline etc). 
  - When trying to make the offline experience as feature-rich as possible I always end up duplicating almost all of the backend logic into the clients as well. And in that case, what is even the point of having a smart backend.
- Check out WatermelonDB 
- pouchdb is mostly unmaintained and issues are just closed by the state bot instead of being fixed.
  - So in the last major RxDB release, I abstracted the underlaying pouchdb in a way that it can be swapped out for a different storage engine. 
  - This means you could in theory use RxDB directly on SQLite or indexeddb. 
  - In practice of course someone has to first create a working implementation of the RxStorage interface.
- Meteor uses `minimongo` on the client which sync's with the server; effectively doing the same thing. It's actually amazing how much better the UX is when you have spotty coverage.
- I think Oracle APEX works on the same premise? Store locally in indexedDB and sync up when the connection is back on-line. No need for difficult programming, APEX does this out of the box .
  - Anyhow, a way to force this behaviour in APEX is to make every user interaction a write action on the DB. This way you either save locally or to the backend (but you don't have to worry about the sync between the two).
