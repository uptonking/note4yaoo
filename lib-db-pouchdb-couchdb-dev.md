---
title: lib-db-pouchdb-couchdb-dev
tags: [couchdb, database, pouchdb]
created: 2022-12-02T11:12:38.058Z
modified: 2022-12-02T11:15:15.257Z
---

# lib-db-pouchdb-couchdb-dev

# guide

# docs

## [Conflicts](https://pouchdb.com/guides/conflicts.html)

- PouchDB exactly implements CouchDB's replication algorithm, so conflict resolution works the same in both. 
  - For the purposes of this article, "CouchDB" and "PouchDB" may be used interchangeably.

- CouchDB and PouchDB differ from many other sync solutions, because they bring the issue of conflicts front-and-center. 
  - With PouchDB, conflict resolution is entirely under your control.

- In CouchDB, conflicts can occur in two places: immediately, when you try to commit a new revision, or later, when two peers have committed changes to the same document. 
  - Let's call these immediate conflicts and eventual conflicts.

- you can present both versions to the user, or resolve the conflict automatically using your preferred conflict resolution strategy: last write wins, first write wins, RCS, etc.
- Another conflict resolution strategy is to design your database so that conflicts are impossible. 
  - In practice, this means that you never update or remove existing documents – you only create new documents.
  - This strategy has been called the "every doc is a delta" strategy. 
  - There is also a PouchDB plugin that implements this strategy: delta-pouch.
# discuss
- ## 

- ## 

- ## 

- ## @pouchdb wont lose data, the conflict is stored and reported, both(all) documents available to choose/create winner, 
- https://twitter.com/daleharvey/status/1043057187113848832
  - we do have encryption plugins (https://github.com/calvinmetcalf/crypto-pouch), no server copy however we dont do
- Yeah I know :) but since the version is only stored per-document, not per-field, you will end up losing data. You could try to auto-resolve by ways merging conflicts... but in which order? You can’t be sure and have to ask the user or something
  - By losing data, I mean from the UX perspective. User syncs, from their view the data is gone. Sure it’s internally there, but they’d have to manually bring it back. This is fully conflict free
- 👉🏻 The app decides which conflict resolution to take of which Last Write Wins, Merge strategies, CRDT or Users Choice are various options, tradeoffs involved in giving that choice to the app developer but prefer to not hear people advertising @pouchdb loses data since it doesnt :)
- Fair enough, good to clarify. Still a big problem that versions are document-level and not field-level though, hard to use CRDTs accurately with that
  - 👉🏻 You could have versions be change level if you wanted (https://github.com/redgeoff/delta-pouch), having fields merge and report only on same field changes is a pretty easy thing to write but I would like to see @pouchdb one day expose these choices as far simpler options
- Nice :) With last-write-win though, you don't even need to store the entire history of changes, just the latest one. Anyway, all tradeoffs. I was able to still leverage sqlite with very efficient storage of this info. Pouch has different tradeoffs, still good!

- ## Using couch as your backend db ends up being a nonstarter for most applications. 
- https://news.ycombinator.com/item?id=22175530
  - A distributed multitenant database is a big big thing and a hugely important technical decision. 
  - Most orgs are not going to go with couch just to get sync.
  - The couchdb replication protocol offers no help with conflict resolution. 
  - It just tells you there was a conflict and gives you two conflicting documents. This isn't practical for most applications.

- I think it's fair to offer a look at what CouchDB says about conflict resolution and what's provided to help manage it.
  - [2.3. Replication and conflict model — Apache CouchDB® 3.3 Documentation](https://docs.couchdb.org/en/stable/replication/conflicts.html)

- PouchDB author here
  - I certainly agree that switching backends to CouchDB has made it hard for people to adopt Pouch/Couch. I have often considered how I could make Pouch work with arbitrary data sources, but as you well know its a tricky problem.
- Thank you for the comment. I think there is a technical difference and an ergonomic difference:
1. The technical difference is that when you do conflict resolution with Replicache you have more information, specifically the intent of the mutations. Consider something very simple like a positive-only counter. The parent is `1` and the forks are `2` and `0`. Is the correct resolution `2`? Is it `0`? Or is it `1`? There's no way to know because we don't know what the intent of those changes was. Was fork 1 incrementing? Was it multiplying? Was fork 2 decrementing? By how much? Now multiply this simple example by real applications with many developers, many features, and many client versions in the wild. Having the intent of each change travel with the change is crucial.
2. The ergonomic difference is that conflict resolution in Replicache isn't something separate that is done after-the-fact. Replicache applies mutations to the server by calling normal HTTP APIs, just with potentially old arguments. This forces developers to consider conflict resolution at the point they are writing APIs, and keeps conflict resolution code colocated with the corresponding services.

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
