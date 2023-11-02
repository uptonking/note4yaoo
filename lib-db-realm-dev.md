---
title: lib-db-realm-dev
tags: [database, realm]
created: 2022-12-02T11:36:15.787Z
modified: 2022-12-02T11:36:42.735Z
---

# lib-db-realm-dev

# guide

- [Atlas Device Sync | MongoDB](https://www.mongodb.com/atlas/app-services/device-sync)
  - [Get Started with Atlas Device Sync — Atlas App Services](https://www.mongodb.com/docs/atlas/app-services/sync/get-started/)
# [MongoDB Realm: Device Sync Protocol](https://www.mongodb.com/docs/atlas/app-services/sync/details/protocol/)
- Atlas Device Sync uses a protocol to correctly and efficiently sync data changes in real time across multiple clients that each maintain their own local Realm files. 
  - The protocol defines a set of pre-defined request types as well as a process by which a client, like a Realm SDK, can connect to an Atlas App Services application server and sync data.
  - The Realm SDKs internally implement and manage the sync protocol, so for most applications you don't need to understand the sync protocol to use Device Sync
- A changeset is a list of instructions that describe granular modifications made to a known object state or version by one or more write operations. 
  - Changesets are the base unit of the sync protocol. 
  - Synced realm clients send changesets to the Device Sync server whenever they perform a write operation. 
  - The server sends each connected client the changesets for write operations executed by other clients.
- 👉🏻 The Device Sync server accepts changesets from any connected sync client (including changes in a synced MongoDB cluster) at any time and uses an **operational transformation** algorithm to serialize changes into a linear order and resolve conflicting changesets before sending them to connected clients.
  - When you make a change to a synced object, App Services does not re-upload the entire object. 
  - Instead, App Services sends only the difference ("delta") between before and after. 
  - The service compresses the deltas with zlib compression.
- Device Sync uses operational transformation to resolve conflicts between changesets from different sync clients that apply to the same base state.
- Realm is an offline-first local database even when sync is enabled, which means that any device may perform offline writes and upload the corresponding changesets later when network connectivity is re-established. 
  - The operational transformation algorithm is designed to gracefully handle changesets that arrive "out of order" with respect to the logical server clock such that every synced Realm file converges to the same version of each changed object.
  - An operational transformation on Realm changesets is analogous to a rebase operation in Git.
# [Conflict Resolution — Atlas App Services](https://www.mongodb.com/docs/atlas/app-services/sync/details/conflict-resolution/)
- Device Sync handles conflict resolution using 
operational transformation
, a set of rules that guarantee strong eventual consistency, meaning all clients' versions will eventually converge to identical states. 
  - This will be true even if changes were made in a different order.

- Rules of Conflict Resolution
- Deletes always win.
  - If one side deletes an object it will always stay deleted, even if the other side has made changes to it later on.
- Last update wins.
  - If two sides update the same property, Device Sync will keep the value from the most recent update.
- Inserts in lists are ordered by time.
  - If two items are inserted at the same position, the item that was inserted first will end up before the other item. This means that if both sides append items to the end of a list, will include both items in order of insertion time.
- Primary keys designate object identity.
  - If two sides both create objects of the same class with identical primary keys, they will be treated as instances of the same object.

- Counters and strings are special cases to be aware of in your client code.
- Using integers for counting is a special case. 
  - we offer a way to express whether you are incrementing (or decrementing) the value, giving enough hints so the merge can reach the correct result. 
- 👉🏻 Device Sync interprets the value of a string as a whole and does not merge conflicts on a per-character basis. 
  - For example, this means that if a character or substring is inserted or deleted within a string, Device Sync will treat this as a replacement of the entire value of the string.

## Custom Conflict Resolution

- Generally speaking, the conflict resolution of Device Sync should work for most purposes, and you should not need to customize it. 
- That said, the typical way to do custom conflict resolution is to change a property type from string to list. 
  - Each side can then add its updates to the list and apply any conflict resolution rules it wants directly in the data model. 
  - You can use this technique to implement max, min, first write wins, last write wins, or any other kind of resolution you can think of.
# discuss
- ## 

- ## 

- ## So far my biggest discovery is Realm and how it is in many ways similar to Minimongo in @meteorjs
- https://twitter.com/StorytellerCZ/status/1534212664976547840

- ## [Where does MongoDB realm store the data?_202210](https://www.reddit.com/r/mongodb/comments/xtrinj/where_does_mongodb_realm_store_the_data/)
- MongoDB Inc bought Realm, and screwed up by rebranding MongoDB Stitch to MongoDB Realm, and calling the local-remote sync for MongoDB Device Sync.

- ## [mongodb - How to achieve synchronization and backup using Realm Sync? - Stack Overflow](https://stackoverflow.com/questions/72323467/how-to-achieve-synchronization-and-backup-using-realm-sync)
- Realm Sync is cloud based - meaning there's a cloud based server that stores the app data remotely
- The data is stored locally first and then automatically sync'd to the cloud at a later time (usually within seconds or faster). 
  - That's why Realm is considered an "offline first" database; data is stored locally (offline) and then copied/stored online.
- Realm can either be a purely local only database with no cloud sync or can be a synchronized online as a "real-time" cloud database. (or both!)
- When sync is used, the database that backs Realm is called MongoDB, and is a NoSQL database.

- ## [The First Object Database for Node: Introducing Realm Node.js | Hacker News_201611](https://news.ycombinator.com/item?id=12968948)
- This is still using Realm Core(cpp), but exposed via JavaScript API
- realm is "object" database. PouchDB is a NoSQL document database. It certainly predates Realm.
- GunDB also runs in Node by the way, AND the browser

- ## [Realm is a mobile database: an alternative to SQLite and key-value stores | Hacker News_201702](https://news.ycombinator.com/item?id=13583107)
- Is this just a perception thing because everybody started uploading his weekend hack toy database to GitHub and blogs about it?
- There are two products - Realm Mobile Database[0] and Realm Mobile Platform[1].
