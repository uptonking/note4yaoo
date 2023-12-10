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

- ## 

- ## [Selective sync · janl/couchdb-next_201702](https://github.com/janl/couchdb-next/issues/14)
- I wonder if replication via view vs _changes might something to consider here. I know we have some view based replication stuff on 1.6 but AFAIK that was basically just to only replicate things in a view. I'm thinking more along the lines of that we just follow the key order in a view and then clients can specify a view and any complex logic they want. Last 90 days for instance could be something like emit(doc.date, null) and then replicate using a start_seq of now() - 90 days

- Anything that requires create view is fairly prohibitive imo, both in terms of performance of view generation and for the amount of work developers need to go through to get it working, there are quite a lot of replication improvements we can do via clever filtering already and they arent done because setting up a filter (and understanding the replication protocol enough to know what to do) is hard enough.
  - We are moving away from views / map reduce in pouchdb in general so I would like to avoid them being further depended on in core functionality

- That's fair. And in hindsight a view doesn't really give us a whole lot over a filter anyway. I'd agree with you that looking at improving filters would likely be the better approach.
# discuss
- ## 

- ## 

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

- ## [Distributed offline editing with couch/pouchdb - Yjs Community](https://discuss.yjs.dev/t/distributed-offline-editing-with-couch-pouchdb/340)
  - Has anyone experimented with using Yjs with pouchdb as both the datastore and communication channel?

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
