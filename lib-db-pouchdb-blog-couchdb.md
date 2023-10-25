---
title: lib-db-pouchdb-blog-couchdb
tags: [blog, couchdb, pouchdb]
created: 2023-10-07T17:29:51.571Z
modified: 2023-10-07T17:30:26.998Z
---

# lib-db-pouchdb-blog-couchdb

# guide

# blogs
- [A Veteran's Guide to PouchDB](https://garbados.github.io/my-blog/veteran-pouchdb.html)

- [Part 1 — The Database. How to build a real time data sync, multi platform app with CouchDB and PouchDB_202012](https://blog.adaptabi.com/part-1-the-database-b7c575864407)

## [Local-first database: RxDB + PouchDB_202005](https://jaredforsyth.com/posts/local-first-database-rxdb-pouchdb/)

- I’ve thought about using a state-based json-crdt for each document, which would allow a client implementation to automatically resolve conflicts in a way that better preserves intent, but I haven’t attempted this. 
  - One option that’s mentioned in the docs is delta-pouch, which “stores every change as its own document”, and then reads out those changes to construct the “current” state of a document.
  - I’m a little wary about the “production-readiness” of this plugin, though, as shoehorning(强挤硬塞) a delta-based system onto pouchdb seems like it would introduce some pretty significant performance penalties(处罚；不利；损失).
# blogs-sync/collab
- [Use JSON Patch to Resolve Conflicts for CouchDB_202009](https://neighbourhood.ie/blog/2020/09/15/use-json-patch-to-resolve-conflicts/)

## [LiveGraph: real-time data fetching at Figma | Figma Blog_202110](https://www.figma.com/blog/livegraph-real-time-data-fetching-at-figma/)

- how do we empower our product engineers to build these real-time views easily, while abstracting away the complexity of pushing data back and forth?
  - 👉🏻 To provide a general solution to this fundamental business need, we developed LiveGraph, **a data fetching layer on top of Postgres that allows our frontend code to request real-time data subscriptions expressed with GraphQL**. 
  - It issues queries directly to the database and provides live updates in the order of(~of/in the order of sth, 大约、数量级) milliseconds by reading the database replication stream.

- We realized that we needed a more general framework that would allow product developers to declaratively define data subscriptions. 
  - A natural choice for this interface was to use GraphQL, which would allow the system to automatically fetch and keep the data live-updated. We decided to build it in-house and call it LiveGraph.
# blogs-couchdb

# more
- [Couchbase vs CouchDB NoSQL Systems: Difference Between Them](https://www.couchbase.com/comparing-couchbase-vs-couchdb/)
