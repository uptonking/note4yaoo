---
title: lib-db-pouchdb-docs
tags: [docs, pouchdb]
created: 2023-10-10T21:37:10.415Z
modified: 2023-10-10T21:37:19.382Z
---

# lib-db-pouchdb-docs

# guide

- [Apache CouchDB Wiki - Confluence](https://cwiki.apache.org/confluence/display/COUCHDB/)
  - [Frequently Asked Questions - Apache CouchDB](https://cwiki.apache.org/confluence/display/COUCHDB/Frequently+Asked+Questions)
# docs
- features-pouchdb
  - Cross Browser
  - Lightweight
  - Easy to Learn

## overview

- PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
- PouchDB is a JavaScript implementation of CouchDB.

- why we chose to implement CouchDB
  - No special protocol, no special drivers: just REST and HTTP. You can communicate with CouchDB entirely through your browser, curl, or a REST client
  - easy synchronization between different databases

- One of the main benefits of learning PouchDB is that it's exactly the same as CouchDB.
  - all of the API methods are the same, with only slight modifications to make it more JavaScript-y

## [pouch databases](https://pouchdb.com/guides/databases.html)

- PouchDB databases come in two flavors: local and remote.
- The remote database will not be created until you do an API call, e.g.: `db.info()`. 
  - The reason behind that is that the PouchDB constructor is completely synchronous, for ease of error handling (i.e. no asynchronous errors).
- `doc_count`: the number of undeleted documents in the database

- Differences between the local and remote databases
  - The goal of PouchDB is to allow you to seamlessly communicate with one or the other. You should not notice many differences between the two, except that of course the local one is much faster!

## [pouch documents](https://pouchdb.com/guides/documents.html)

- PouchDB is a NoSQL database, meaning that you store unstructured documents rather than explicitly specifying a schema with rows, tables
- Whenever you `put()` a document, it must have an `_id` field so that you can retrieve it later.
- The new field,  `_rev` is the revision marker. It is a randomly-generated ID that changes whenever a document is created or updated.

- 👉🏻 Unlike most other databases, whenever you update a document in PouchDB or CouchDB, you must present the entire document along with its current revision marker.
  - So to update Mittens' age, we will first need to fetch Mittens from the database, to ensure that we have the correct _rev before we put them back. 
  - We don't need to manually assign the _rev value here (like we did above), as it is already in the doc we're fetching.

## pouch-dev

- PouchDB provides a fully asynchronous API. 
  - This ensures that when you talk to PouchDB, the UI doesn't stutter, because the DOM is not being blocked by database operations.
- API is provided in both callback format and promise format.
  - if you include a callback as the last argument in a function, then PouchDB assumes you want the callback style. Otherwise it assumes you want the promise style.

- 
- 
- 
- 
- 
- 

## [Updating and deleting documents](https://pouchdb.com/guides/updating-deleting.html)

- why do we have to deal with _rev at all?
  - because _revs are what makes sync work so well. PouchDB asks for a little upfront(预付的，预交的) effort with managing document revisions, so that later on, sync is a breeze.
- PouchDB and CouchDB's document revision structure is very similar to Git's. 
  - In fact, each document's revision history is stored as a tree (exactly like Git), which allows you to handle conflicts when any two databases get out of sync.
- When you remove() a document, it's not really deleted; it just gets a _deleted attribute added to it.
  - That is, the database saves a tombstone at the end of the revision tree.

## [Bulk operations](https://pouchdb.com/guides/bulk-operations.html)

- PouchDB provides two methods for bulk operations
  - `allDocs()` for bulk reads
  - `bulkDocs()` for bulk writes

- Bulk operations tend to be faster than individual operations, because they can be combined into a single transaction (in a local IndexedDB/WebSQL) or a single HTTP request (in a remote CouchDB).
  - Neither bulkDocs() nor allDocs() constitutes a transaction in the traditional sense. That means that, if a single put() fails, you should not assume that the others will fail.

> By design, CouchDB and PouchDB do not support transactions. A document is the smallest unit of operations.

- when you read from allDocs(), the documents are returned sorted by order of `_id`. 
  - This makes the `_id` a very powerful field that you can use for more than just uniquely identifying your documents.
- Another common way to take advantage of this is to use new Date().toJSON() as your document _ids. In this way, all your documents will be sorted by date.

- It not only returns documents in order – it also allows you to reverse the order, filter by _id, slice and dice using "greater than" and "less than" operations on the _id, and much more.
- Far too many developers overlook this valuable API, because they misunderstand it. 
  - When a developer says "my PouchDB app is slow!", it is usually because they are using the slow query() API when they should be using the fast allDocs() API.
- For 99% of your applications, you should be able to use allDocs() for all the pagination/sorting/searching functionality that you need.

## [Working with attachments](https://pouchdb.com/guides/attachments.html)

- 
- 
- 

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
