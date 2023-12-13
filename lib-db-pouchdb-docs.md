---
title: lib-db-pouchdb-docs
tags: [docs, pouchdb]
created: 2023-10-10T21:37:10.415Z
modified: 2023-10-10T21:37:19.382Z
---

# lib-db-pouchdb-docs

# guide

- resources-pouch
  - [pouchdb FAQ](https://pouchdb.com/faq.html)

- resources-couch
  - [CouchDB Frequently Asked Questions](https://cwiki.apache.org/confluence/display/COUCHDB/Frequently+Asked+Questions)
  - [CouchDB Wiki - Confluence](https://cwiki.apache.org/confluence/display/COUCHDB/)
# faq

## Can PouchDB sync with MongoDB/MySQL/my current non-CouchDB database?

- No, your backend needs to speak the CouchDB replication protocol. 
  - The magic of PouchDB <–> CouchDB sync comes from this design, which in particular requires all documents to be versioned with the `_rev` marker. 
  - This allows PouchDB and CouchDB to elegantly handle conflicts

## How is PouchDB different from CouchDB?

- PouchDB is also a CouchDB client, and you should be able to switch between a local database or an online CouchDB instance without changing any of your application's code.

- View Collation
  - CouchDB uses ICU to order keys in a view query; 
  - in PouchDB they are ASCII ordered.
- View Offset
  - CouchDB returns an `offset` property in the view results. 
  - In PouchDB,  `offset` just mirrors the `skip` parameter rather than returning a true offset.

## What data types does PouchDB support?

- PouchDB has two types of data: documents and attachments.

- As in CouchDB, the documents you store must be serializable as JSON. Modifying the Object prototype or storing classes is not supported.
  - IndexedDB will actually support non-JSON data (e.g. `Date`s aren't stringified), but you should not rely on this, because CouchDB, LevelDB, and Web SQL do not behave the same.

- PouchDB also supports attachments, which are the most efficient way to store binary data. Attachments may either be supplied as base64-encoded strings or as Blob objects.
- PouchDB's strategies are:
  - Blob: data is stored in a true binary format. The most efficient method.
  - UTF-16 Blob: blobs are coerced to UTF-16, so they takes up 2x the normal space.
  - Base-64: data is stored as a base-64-encoded string. The least efficient method.
- Attachments are deduplicated based on their MD5 sum, so duplicate attachments won't take up extra space.
- To truly remove an attachment from the data store, you will need to use compaction to remove document revisions that reference that attachment.

- Different backends have different strategies for storing binary data, which may affect the overall database size. Attachment stubs have a length property that describes the number of bytes in the Blob object, but under the hood, it may actually take up more space than that.
# docs
- features-pouchdb
  - Cross Browser
  - Lightweight
  - Easy to Learn

## overview

- PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
- PouchDB is a JavaScript implementation of CouchDB.
- PouchDB and  CouchDB were designed for one main purpose: sync.
- PouchDB is an in-browser database that allows applications to save data locally, so that users can enjoy all the features of an app even when they're offline.
- PouchDB also runs in Node.js and can be used as a direct interface to CouchDB-compatible servers. 
  - In Node.js, PouchDB uses LevelDB under the hood, and also supports many other backends via the LevelUP ecosystem

- PouchDB is not a self-contained database; it is a CouchDB-style abstraction layer over other databases. 
  - By default, PouchDB ships with the IndexedDB adapter for the browser, and a LevelDB adapter in Node.js. 
- PouchDB attempts to provide a consistent API that "just works" across every browser and JavaScript environment, and in most cases, you can just use the defaults.
  - if you want the best performance, then you will sometimes want to tinker with the adapter settings.

- why we chose to implement CouchDB
  - No special protocol, no special drivers: just REST and HTTP. You can communicate with CouchDB entirely through your browser, curl, or a REST client
  - easy synchronization between different databases

- One of the main benefits of learning PouchDB is that it's exactly the same as CouchDB.
  - all of the API methods are the same, with only slight modifications to make it more JavaScript-y

## pouch-dev

- PouchDB provides a fully asynchronous API. 
  - This ensures that when you talk to PouchDB, the UI doesn't stutter, because the DOM is not being blocked by database operations.
- API is provided in both callback format and promise format.
  - if you include a callback as the last argument in a function, then PouchDB assumes you want the callback style. Otherwise it assumes you want the promise style.

- Implement basic two way sync
  - db.replicate() tells PouchDB to transfer all the documents to or from the remoteCouch.
  - `live` flag is used to tell PouchDB to carry on doing this indefinitely. The callback will be called whenever this finishes. For live replication, this will mean an error has occurred, like losing your connection or you canceled the replication.

```JS
function sync() {
  syncDom.setAttribute('data-sync-state', 'syncing');
  var opts = { live: true };
  db.replicate.to(remoteCouch, opts, syncError);
  db.replicate.from(remoteCouch, opts, syncError);
}
```

- 
- 

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

- PouchDB attachments allow you to use web storage to full advantage to store images, MP3s, zip files, or whatever you want.
- attachments are attached to documents. You can work with attachments either in base64-encoded format, or as a Blob.
- document has a special `_attachments` field that holds the attachments. Documents can have as many attachments as you want.
- When you create an attachment, you need to specify its `content_type`, otherwise known as the MIME type. Common MIME types include 'text/plain' for plain text, 'image/png' for PNG images
- By default, PouchDB will only give you an attachment `stub`, which contains a `digest`, i.e. the md5sum of the binary attachment.
  - To get the full attachments when using `get()` or `allDocs()`, you need to specify `{attachments: true}`.
- We are using the getAttachment() API, which returns a Blob rather than a base64-encoded string. To be clear: we can always convert between base64 and Blobs, but in this case, getAttachment() is just more convenient.

- we can also create the Blobs ourselves and store those directly in PouchDB.
  - In Node.js, PouchDB uses Buffers instead of Blobs. Otherwise, the same rules apply.
  - Blobs can be tricky to work with, especially when it comes to cross-browser support.

- 🆚️ Base64 vs Blobs/Buffers
  - Whether you supply attachments as base64-encoded strings or as Blobs/Buffers, PouchDB will try to store them in the most efficient way.
  - When you fetch attachments, however, getAttachment() will always return Blobs/Buffers.
- If you can insert and retrieve your attachments using only Blobs/Buffers, then you will typically get better performance, especially when it comes to memory usage. The base64 string format is mostly provided for developer convenience and debugging.

## [Replication](https://pouchdb.com/guides/replication.html)

- Unlike most databases, CouchDB requires you to manage revisions (`_rev`), which can be tedious.
  - managing your document revisions pays off in the future, when you eventually need to start dealing with conflicts.

- CouchDB supports a multi-master architecture. 
- When you use PouchDB, CouchDB, and other members of the Couch family, you don't have to worry which database is the "single source of truth." They all are.
- Typical relational databases such as MySQL are CP, which means they are consistent and tolerant to node partitions, at the expense of availability. 
  - CouchDB is an AP database, meaning that it's Partition-Tolerant, every node is Available at all times, but it's only eventually Consistent.
- In cases of conflict, CouchDB will choose an arbitrary winner that every node can agree upon deterministically. However, conflicts are still stored in the revision tree (similar to a Git history tree)

- The simplest case is unidirectional replication, meaning you just want one database to mirror its changes to a second one. 
  - Writes to the second database, however, will not propagate back to the master database.

- Live replication (or "continuous" replication) is a separate mode where changes are propagated between the two databases as the changes occur. 
  - In other words, normal replication happens once, whereas live replication happens in real time.
- However, there is one gotcha with live replication: what if the user goes offline? In those cases, an error will be thrown and replication will stop.
  - You can allow PouchDB to automatically handle this error, and retry until the connection is re-established, by using the retry option

- The replicate API supports canceling

- One thing to note about replication is that it tracks the data within a database, not the database itself. If you destroy() a database that is being replicated to, the next time the replication starts it will transfer all of the data again

- Any PouchDB object can replicate to any other PouchDB object. So for instance, you can replicate two remote databases, or two local databases. You can also replicate from multiple databases into a single one, or from a single database into many others.
  - You have an in-memory PouchDB that replicates with a local PouchDB, acting as a cache.
  - You have many remote CouchDB databases that the user may access, and they are all replicated to the same local PouchDB.
  - You have many local PouchDB databases, which are mirrored to a single remote CouchDB as a backup store.

- When you replicate between two remote databases, the changes flow through PouchDB. If this is not what you want, then you should POST directly to the CouchDB _replicate endpoint

## [Conflicts](https://pouchdb.com/guides/conflicts.html)

> PouchDB exactly implements CouchDB's replication algorithm, so conflict resolution works the same in both. 
> For the purposes of this article, "CouchDB" and "PouchDB" may be used interchangeably.

- CouchDB and PouchDB differ from many other sync solutions, because they bring the issue of conflicts front-and-center. With PouchDB, conflict resolution is entirely under your control.

- In CouchDB, conflicts can occur in two places: immediately, when you try to commit a new revision, or later, when two peers have committed changes to the same document. 
  - Let's call these immediate conflicts and eventual conflicts.

- Immediate conflicts can occur with any API that takes a rev or a document with _rev as input 
  - In your code, you should always be handling conflicts. No matter how unlikely it may seem, 409s can and do occur.
  - For instance, if you are doing live replication, a document may be modified by somebody else while the user is working on it. If the remote changes are replicated to the local database before the user tries to commit their changes, then they will receive the above 409 error.
- In many cases, the most practical solution to the 409 problem is to retry the put() until it succeeds.

- Eventual conflicts
  - Imagine two PouchDB databases have both gone offline. The two separate users each make modifications to the same document, and then they come back online at a later time.
  - Both users committed changes to the same version of the document, and their local databases did not throw 409 errors. What happens then?
  - 💡 By default, CouchDB will choose an arbitrary winner based on a deterministic algorithm, which means both users will see the same winner once they're back online. However, since the replication history is stored, you can always go back in time to resolve the conflict.
- Revision hashes start with 1-, 2-, 3-, etc., which indicates their distance from the first, "root" revision. The root always starts with 1-
- In fact, all databases in the network will see the exact same revision history – much like Git.
  - To fetch the losing revision, you simply get() it using the rev option
  - you can present both versions to the user, or resolve the conflict automatically using your preferred conflict resolution strategy: last write wins, first write wins, RCS, etc.
- To mark a conflict as resolved, all you need to do is remove() the unwanted revisions. 
  - If you want to resolve the conflict by creating a new revision, you simply put() a new document on top of the current winner, and make sure that the losing revision is deleted.

- Another conflict resolution strategy is to design your database so that conflicts are impossible. 
  - In practice, this means that you never update or remove existing documents – you only create new documents.
  - This strategy has been called the "every doc is a delta" strategy. 
  - There is also a PouchDB plugin that implements this strategy: delta-pouch.

## [Changes feed](https://pouchdb.com/guides/changes.html)

- One thing you will notice about the changes feed is that it actually omits non-leaf revisions to documents.
  - This is by design – the changes feed only tells us about leaf revisions. 
  - However, the order of those leaf revisions is determined by the order they were put in the database.
- If you expect this to be a very large number of changes, you can also use the limit option to do pagination
- The changes feed lists each change with a corresponding seq integer. seq always starts with 0, and beyond that it increases monotonically. (In Cloudant, these are strings rather than integers.)
- seq can be thought of as a version number for the entire database.
  - This sets it apart from the revision hash _rev, which marks the changes made to a single document.
- However, the seq between two databases is not guaranteed to be kept in sync. CouchDB and PouchDB have slightly different ways of increasing their seq values, so really seq is only meaningful within a single database.

- There are two types of changes: Added or modified documents; Deleted documents

- How can I distinguish between added and modified documents? 
  - Checking if the revision starts with '1-' is a pretty good trick. 
  - However, this will not work for databases that are replication targets, because replication only sends the latest versions of documents. This means that the '1-' revision may get skipped entirely, and the local database will only receive the 2nd, 3rd or 4th (etc.) revision. Conflicting revisions will also appear in the changes feed.
  - So the short answer is that you cannot. If you are trying to mirror changes in a non-Pouch structure (e.g. a list of DOM elements), then the best solution is to search all the DOM elements to see if the document already exists, or to re-run allDocs() for every change.

## [Mango queries](https://pouchdb.com/guides/mango-queries.html)

- Mango queries, also known as `pouchdb-find` or the `find()` API, are a structured query API that allows you to build secondary indexes beyond the built-in `allDocs()` and `changes()` indexes.
- The Mango query language is a DSL inspired by MongoDB, which allows you to define an index that is then used for querying. 

- At a basic level, there are two steps to running a query: `createIndex()` (to define which fields to index) and `find()` (to query the index).
- The important thing to understand is that, for a typical database, createIndex() is the expensive operation, because it is looping through all documents in the database and building a B-tree based on the name value.
  - Once the B-tree is built up, though, the find() is relatively cheap. (If this were not the case, then we would be better off just using allDocs() to iterate through the database ourselves!)
- we can continue paginating by using the last value as our next starting point. At any given point in time, there are only 10 documents stored in memory at once, which is great for performance.
- you can index on more than one field
  - One thing to note is that the order of these fields matters when creating your index. 
  - it's important to carefully design an index before creating a query to use that index. Otherwise, the query planner may fall back to in-memory querying, which can be expensive.

- you may create an index with createIndex(), but then write a find() query that doesn't actually use that index
- In general, the query planner tries to find the most appropriate index, but it may fall back to in-memory querying.
  - if you query using the _id field, then the query planner will automatically map that directly to an allDocs() query. 
  - However, if you query for a field that isn't yet indexed, then it will simply use allDocs() to read in all documents from the database (!) and then filter in-memory. This can lead to poor performance, especially if your database is large.
- If you're ever wondering how the query planner is interpreting your query, you can use the explain endpoint
  - the query planner will show a detailed explanation of how it has interpreted the query, whether it uses any indexes, and whether any parts of the query need to be executed in-memory.
- When creating a query, by settings the use_index field, it is possible to tell pouchdb-find which index to use. 

- The most complete documentation for selector options can be found in the CouchDB _find documentation.
  - PouchDB uses CouchDB as the reference implementation; they ought to be functionally identical.

## [Map/reduce queries](https://pouchdb.com/guides/queries.html)

- Map/reduce queries, also known as the `query()` API, are one of the most powerful features in PouchDB.
  - The PouchDB `query()` API (which corresponds to the `_view` API in CouchDB) has two modes: temporary queries and persistent queries.

- The first thing to understand is that you don't need map/reduce queries if you merely want to look up documents by _id or sort them by _id. The allDocs() API already does this, using an efficient built-in index.
- The second thing to know is that map/reduce is also unnecessary if you want to sort documents by their update time – this is exactly what the changes feed does! Again, this is a built-in index that you get for free.
- Finally, it's important to understand that Mango queries are much easier to use than map/reduce queries, and they can usually satisfy 99% of use cases. 
  - The point of map/reduce is to provide an extremely advanced API for building secondary indexes, suitable for those with specific querying needs.

- Temporary queries are very slow, and we only recommend them for quick debugging during development. 
  - To use a temporary query, you simply pass in a map function
  - The emit pattern is part of the standard CouchDB map/reduce API. What the function basically says is, "for each document, emit doc.name as a key."

- Persistent queries are much faster, and are the intended way to use the query() API in your production apps. 
  - First, you create a design document, which describes the map function you would like to use
  - Then you actually query it, by using the name you gave the design document when you saved it
  - Note that, the first time you query, it will be quite slow because the index isn't built until you query it. To get around this, you can do an empty query to kick off a new build

- CouchDB builds indexes in exactly the same way as PouchDB. So you may want to familiarize yourself with the "stale" option in order to get the best possible performance for your app.

- Indexes in SQL databases
  - in relational databases like MySQL and PostgreSQL, you can usually query whatever field you want
  - if you don't want your performance to be terrible, you first add an index
  - The job of the index is to ensure the field is stored in a B-tree within the database, so your queries run in O(log(n)) time instead of O(n) time.

- Indexes in NoSQL databases
  - All of the above is also true in document stores like CouchDB and MongoDB, but conceptually it's a little different. 
  - By default, documents are assumed to be schemaless blobs with one primary key (called _id in both Mongo and Couch), and any other keys need to be specified separately. 
  - The concepts are largely the same; it's mostly just the vocabulary that's different.
- In CouchDB, queries are called map/reduce functions. 
  - This is because, like most NoSQL databases, CouchDB is designed to scale well across multiple computers, and to perform efficient query operations in parallel. 
  - Basically, the idea is that you divide your query into a map function and a reduce function, each of which may be executed in parallel in a multi-node cluster.

- Map functions
  - in the simplest (and most common) case, you only need the map function. 
- Reduce functions
  - there are a few handy built-ins that do aggregate operations ('_sum', '_count', and '_stats'), and you can typically steer clear of(绕开, 避开) trying to write your own

- The map/reduce API is complex, and it can be computationally expensive because it requires building up an entirely new index. 
- Therefore, it's good to know some tricks for avoiding the map/reduce API when you don't need it:
  - If you can use allDocs() or changes() instead of the query() API, do it!
  - If your query is simple enough that you can use find(), use that instead.
  - Read the 12 tips for better code with PouchDB, especially the tip to "use and abuse your doc _ids."
  - If your data is highly relational, try the relational-pouch plugin, which follows this advice, and only uses _id and allDocs() under the hood.

## [Compacting and destroying](https://pouchdb.com/guides/compact-and-destroy.html)

- By default, PouchDB and CouchDB are designed to store all document revisions forever. This is very similar to how Git works, and it helps ensure that two databases can consistently replicate with each other.

- However, if you allow your database to grow without bounds, it can end up taking up much more space than you need. 
- To mitigate this problem, PouchDB offers two recourses: compaction and destruction.

- When you compact a database, you tell PouchDB to optimize its current storage usage. CouchDB will do the same thing
  - From the API perspective, nothing should be different about the database after compaction, except that non-leaf revisions will no longer be available.
- since leaf revisions are retained, this means that you can still do conflict resolution after compaction!

- If you really want to go all-in on compaction, then you can even put your database in `auto_compaction` mode. 
  - This means that it will automatically perform a compact() operation after every write.
- This feature is only available in local databases, not remote ones. On remote databases, the auto_compaction option will do nothing.

## [Local documents](https://pouchdb.com/guides/local-documents.html)

- Local docs have the following characteristics:
  - They don't replicate.
  - They can't contain attachments.
  - They don't appear in allDocs(), changes(), or query().
  - However, you can modify them with put()/remove()/bulkDocs(), and you can fetch them with get().

- local docs only exist for that database, and they don't mix with the "normal" documents.
- To create a local doc, you simply use `_local/` as the prefix of the `_id`. This is supported in both CouchDB and PouchDB

- Local docs are useful for small bits of configuration or metadata, which you don't necessarily want to replicate
- Many PouchDB plugins and core components use local docs. 
  - For instance, the replication algorithm uses them to store checkpoints, and map/reduce uses them to keep track of what's been emitted.
- Local docs also have some good performance characteristics compared to regular docs. 
  - They don't have a version history, so only the most recent revision is ever stored in the database.
  - This means that put()s and get()s are faster for local docs than for regular docs, and that local docs tend to take up less space on disk. 
  - In a sense, they are auto-compacted, although they take up even less space on disk than documents in a compacted database.

- Regardless, you need to provide the current _rev when you update local docs, just like with regular docs.
# more
