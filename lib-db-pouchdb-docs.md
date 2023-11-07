---
title: lib-db-pouchdb-docs
tags: [docs, pouchdb]
created: 2023-10-10T21:37:10.415Z
modified: 2023-10-10T21:37:19.382Z
---

# lib-db-pouchdb-docs

# guide

# docs
- features-pouchdb
  - Cross Browser
  - Lightweight
  - Easy to Learn

## overview

- PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
- 
- 
- 
- 
- 
- 
- 
- 

## [Updating and deleting documents](https://pouchdb.com/guides/updating-deleting.html)

- PouchDB and CouchDB's document revision structure is very similar to Git's. 
  - In fact, each document's revision history is stored as a tree (exactly like Git), which allows you to handle conflicts when any two databases get out of sync.

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
# more
