---
title: lib-db-pouchdb-blog-couchdb
tags: [blog, couchdb, pouchdb]
created: 2023-10-07T17:29:51.571Z
modified: 2023-10-07T17:30:26.998Z
---

# lib-db-pouchdb-blog-couchdb

# guide

- resources
  - [pouchdb blog](https://pouchdb.com/blog/)
  - [couchdb blog](https://blog.couchdb.org/)
# blogs

## [Understanding CouchDB Conflicts_201312](https://writing.jan.io/2013/12/19/understanding-couchdb-conflicts.html)

## 📎 [Binary Data Attachments & Blobs: Handle w/ Couchbase Mobile_202006](https://www.couchbase.com/blog/store-sync-binary-data-attachments-blobs-couchbase-mobile/)

- In addition to supporting the standard JSON data types, Couchbase Mobile also supports binary data that include images, audio, video, PDF files, etc. 
  - A JSON document can be associated with one or more elements of binary data referred to as “attachments” or “blobs”. 
  - The binary data can be synced between Couchbase Lite clients and the server via the Sync Gateway. 
- In this post, we discuss how to create binary data attachments, how to retrieve and update them
  - Everything in this post applies to a Couchbase Mobile 2.x based deployment.

- Support for associating binary data with JSON documents within Couchbase Mobile has evolved over the years. 
- In Couchbase Mobile 1.x, binary data was stored in the form of “attachments” within a top-level `_attachments` attribute. 
- Couchbase Mobile introduced the `blob` data type for storing binary data. 
- In most cases, the discrepancy(差异；不一致) between the representations across versions is seamlessly handled by Couchbase Mobile so end users don’t have to do anything special within their apps to deal with it. 
- However, there are certain cases wherein app developers would have to take extra measures to deal with the discrepancy.

- Workflow #1: Handling attachments created on Couchbase Lite
  - A document can be associated with one or more attachments or blobs
  - Sync Gateway is backward compatible with Couchbase Mobile 1.x. This implies that the Sync Gateway needs to be capable of processing binary data using the 1.x _ attachments style representation as well as the 2.x blob type
  - The reason for this discrepancy is because the Sync Gateway only deals with 1.x style attachments.

- Workflow #2: Handling of attachments created on Sync Gateway
  - The attachment data that is created through the Sync Gateway REST endpoint is persisted in the Couchbase Server bucket and synced over to Couchbase Lite clients subject to the access control policies configured on the Sync Gateway.

- 🤔 Where are attachments stored?
  - On Couchbase Lite, attachments are stored in the Couchbase Lite database instance that contains the corresponding document. 
    - It is stored separately from the document which contains the associated metadata that holds the reference to the attachment. 
    - If the same attachment is shared by multiple documents, only a single instance of the attachment is stored in the database.
  - On Couchbase Server, attachments are stored in the same Couchbase Server bucket as the corresponding document. 
    - It is stored separately from the document which contains the associated metadata that holds the reference to the attachment. 
    - If the same attachment is shared by multiple documents, only a single instance of the attachment is stored in the bucket.

- What is the maximum size of an attachment?
  - The maximum size of each attachment is 20MB. This follows from the limits on document sizes on Couchbase Server. 
  - While Couchbase Lite itself allows attachments of size greater than 20MB and this is fine as long as the attachment is local-only and is guaranteed to never be synced to the server. 
  - However, developers are cautioned from creating such large attachments as they will be rejected by the Sync Gateway.

- Do attachments sync every time the associated JSON document changes?
  - The replication protocol is optimized to only sync attachments when there are updates to them. 
  - This implies that they are not pushed or pulled by Couchbase Lite clients even if there are updates to other data in the associated JSON documents.

## 🌰 [CouchDB, The Open-Source Cloud Firestore Alternative? - DEV Community_201909](https://dev.to/juliendemangeon/couchdb-the-open-source-cloud-firestore-alternative-2gc0)

- There is no per-document rights, only per-DB.
  - A common recommendation around this is to use many (think thousands) of DBs, i.e. DB-per-user, and set up filtered replications to maintain each user's access. Unfortunately this has very poor performance - I found that for a small project (~150 users with a few admin roles) the CPU usage for replication became unwieldy.
- Couchbase, does a much better job of security and rights, though has its own quirks. 
  - It requires a secondary layer (called Sync Gateway) to give it a Couch-like API which can connect to PouchDB. 
  - This also provides a very useful "sync function" that allows very smooth per-document rights. I'm mostly happy with it. 

## 📝 [A Veteran's(老兵) Guide to PouchDB](https://garbados.github.io/my-blog/veteran-pouchdb.html)

## [Local-first database: RxDB + PouchDB_202005](https://jaredforsyth.com/posts/local-first-database-rxdb-pouchdb/)

- I’ve thought about using a state-based json-crdt for each document, which would allow a client implementation to automatically resolve conflicts in a way that better preserves intent, but I haven’t attempted this. 
  - One option that’s mentioned in the docs is delta-pouch, which “stores every change as its own document”, and then reads out those changes to construct the “current” state of a document.
  - I’m a little wary about the “production-readiness” of this plugin, though, as shoehorning(强挤硬塞) a delta-based system onto pouchdb seems like it would introduce some pretty significant performance penalties(处罚；不利；损失).

## [Filtered replication: from Couch to Pouch and back_201504](https://pouchdb.com/2015/04/05/filtered-replication.html)

- Filtered replication can become a vital feature for many applications, when you realize you don't need the whole dataset to be replicated to each client. 
- At the same time, filtered replication can be the wrong solution to your problem if:
  - You're trying to address security concerns. Replicating only the user's documents via filtering might seem simplest, but filtering isn't a substitute for proper authentication.
  - you'd like to provide a better per-user or per-role experience

- Filters in PouchDB
- Client-side filtering takes nothing more than a JS function. 
  - This will prevent useless documents from being stored locally, 
  - but it means the documents will still go over the wire, and the client will waste CPU cycles to handle them properly.
- Server-side filtering, again, takes nothing more than a JS function, 
  - but it's executed by CouchDB. 
  - This will prevent documents from going over the wire in the first place! So obviously we prefer this one.

- you might be wondering about the difference between a view and a filter. 
- My reason for using filters is easy: I want to emit the whole document, and I want to emit documents according to a parameter provided by the client. 
  - While you could create a view that emits the whole document, taking parameters becomes a bit too complicated for my taste.

- When using filtered replication, you should not use the DELETE method to remove documents, but instead use PUT and add a _deleted:true field to the document, preserving the fields required for the filter. Your Document Update Handler should make sure these fields are always present. 
  - This will ensure that the filter will propagate deletions properly.

- To make two-way filtered replication work, the design document needs to be in both the remote database and the local database. 
  - To do this, we might decide to simply replicate the design document alongside the other documents.
- It is enough to have it stored locally; Pouch will handle the rest. The downside is that now we need to remember to handle the design document, by not letting it mingle with the documents needed in the UI.
- If you feel you'd rather keep the filter function clean and not worry about filtering the design document itself, then you could also have two different design documents by the same id, one in Couch and one in Pouch, not replicating.

## [How we test PouchDB](https://pouchdb.com/2014/11/27/testing-pouchdb.html)

- Test library
  - Mocha
- Test platform
  - Travis CI
- Test runner
  - Selenium
- Performance tests
  - choose which version of PouchDB to test

## [Secondary indexes have landed in PouchDB_201405](https://pouchdb.com/2014/05/01/secondary-indexes-have-landed-in-pouchdb.html)

- With the release of PouchDB 2.2.0, we're happy to introduce a feature that's been cooking on the slow simmer for some time: secondary indexes, a.k.a. persistent map/reduce.
  - it allows you to index anything in your JSON documents – not just the doc IDs.
  - the new API is modeled after CouchDB's

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

- PouchDB has actually had map/reduce queries since way before version 2.2.0, via the query() API. 😩 It had a big flaw, though: all queries were performed in-memory, reading in every document in the entire database just to perform a single operation.
- The new persistent query() method is much more memory-efficient, and it won't read in the entire database unless you tell it to. 
- It has two modes:
  - Temporary views (like the old system)
  - Persistent views (new system)

- CouchDB calls indexes views, and these views are stored in a special document called a design document. 
  - Basically, a design document describes a view, and a view describes a map/reduce query, which tells the database that you plan to use that query later, so it better start indexing it now. 
- In other words, creating a view is the same as saying `CREATE INDEX` in a SQL database.
- Temporary views are exactly that – temporary. Instead of using a design document, you just call pouch.query(), so the view is created, written to disk, queried, and then poof, it's deleted. That's why, in older version of PouchDB, we could get away with doing it all in-memory.
  - temporary views have to do a full scan of all documents every time you execute them, along with all the reading and writing to disk that that entails, only to throw it away at the end.
- Persistent views need to be saved in a design document (hence "persistent"), so that the emitted fields are already indexed by the time you look them up. 
  - Subsequent lookups don't need to do any additional writes to disk, unless documents have been added or modified, in which case only the updated documents need to be processed.
- Design documents are special meta-documents that CouchDB uses for things like indexes, security, and schema validation (think: "designing" your database). 
  - They are stored, updated, and deleted exactly like normal documents, but their `_ids` are prefixed with the reserved string `_design/`. They also show up in allDocs() queries, but you can filter them out by using `{startkey: '_design0'}`.
- Technically, a design doc can contain multiple views, but there's really no advantage to this. Plus, it can even cause performance problems in CouchDB, since all the indexes are written to a single file. 
  - 💡 So we recommend that you create one view per design doc, and use the same name for both, in order to make things simpler.

- Just like regular documents, design docs can always be deleted or changed later. The index will be updated automatically the next time you query() it.
  - Technically, the view will not be built up on disk until the first time you query() it. 
  - So a good trick is to always call query(viewName, {stale: 'update_after'}) after creating a view, to ensure that it starts building in the background. 
  - You can also use {stale: 'ok'} to avoid waiting for the most up-to-date results.

- allDocs() API will read all documents into memory, just like before
  - But in general, we strongly recommend upgrading your apps to the new map/reduce API instead.

- When not to use map/reduce
- views can take awhile to build up, both in CouchDB and PouchDB. 
  - Each document has to be fetched from the database, passed through the map function, and indexed, which is a costly procedure for large databases. 
  - And if your database is constantly changing, you will also incur the penalty at query() time of running the map function over the changed documents.
  - Luckily, it turns out that the primary index, _id, is often good enough for a variety of querying and sorting operations. So if you're clever about how you name your document _ids, you can avoid using map/reduce altogether.

- if you're just using the randomly-generated doc IDs, then you're not only missing out on an opportunity to get a free index – you're also incurring the overhead of building an index you're never going to use. So use and abuse your doc IDs!

- Tips for writing views
- Don't index it if you don't need it
  - If the null field is meaningful for some reason, though, you can emit it and look it up later using query(viewName, {key: null}). Any undefined fields are treated as null.
- Move logic to the query params
- Use high characters for prefix search
  - Or you can set inclusive_end to false
- Use {} for complex key ranges
  - In CouchDB collation ordering, {} is higher than everything except other objects.

- 🧐💡 For the database geeks: implementation details
- One of the neat things about how we implemented map/reduce is that we managed to do it entirely within PouchDB itself. 
- your map/reduce view is just a regular old PouchDB database, and map/reduce itself is a plugin with no special privileges, creating databases in exactly the same way a regular user would. Since the implementation sits on top of the PouchDB API, it's exactly the same for all three backends: LevelDB, IndexedDB, and WebSQL.
- In fact, as we were debating how to implement this feature, we originally ran on the assumption that we'd need to build additional functionality on top of PouchDB. It was only after a few months of discussions and experiments that we realized the whole thing could be done in PouchDB proper.
  - In the end, the only additional functionality we had to add to the main PouchDB code was a hook to tell PouchDB to destroy the map/reduce database when its parent database was destroyed. That's it.
- This technique also has a nice parallel in CouchDB: it turns out that they, too, reused the core _view code in order to write _all_docs. In CouchDB, _all_Docs is just a special kind of _view, whereas in PouchDB, we built map/reduce views on top of allDocs(). We did it backwards, but the spirit of the idea was the same.
- As for the index itself, what it basically boils down to is clever serialization of arbitrary JSON values into CouchDB collation ordering – i.e. nulls before booleans, booleans before numbers, numbers before strings, strings before arrays, arrays before objects, and so on recursively. 
  - Every JSON object maps to an indexable string that guarantees the same ordering in every database backend, and we only deviate from CouchDB by using ASCII string ordering instead of ICU ordering (since that's what our backends use).
  - Then, we take this value and concatenate it with whatever else needs to be indexed (usually just the doc _id), meaning the entire lookup key is a single string. 
- We decided on this implementation because:
  - LevelDB does not support complex indexes.
  - IndexedDB does support complex indexes, but not in IE.
  - WebSQL supports multi-field indexes, but it's also a dead spec, so we're not going to prioritize it above the others.
- The next part of the design was to divide the data we needed to store into two kinds of documents: 
  - 1) emitted key/values with doc IDs, which are used for querying and pagination, and 
  - 2) mappings from doc IDs to those key/values, so that we can delete or update them when their parent documents are deleted or updated. 
- Since by design, PouchDB databases do not have multi-document transaction semantics, we implemented a task queue on top of the database to serialize writes.
- Aside from that, the only other neat trick was a liberal(不严格的；自由的) use of `_local` documents, which are a special class of documents that aren't counted in the `total_rows` count, don't show up in `allDocs`, but can still be accessed using the normal put() and get() methods. This is all it takes to fully reimplement CouchDB map/reduce in a tiny JavaScript database

## [Pagination strategies with PouchDB_201404](https://pouchdb.com/2014/04/14/pagination-strategies-with-pouchdb.html)

- allDocs(), doesn't do any pagination by default.
  - allDocs() doesn't return the full document data by default, unless you pass in the option `{include_docs : true}`.
  - It only returns the document `id` and revision hash `rev`.
- Since PouchDB is modeled after CouchDB, we can learn about these parameters by directly consulting the Couch docs
  - both `startkey` and `endkey` are inclusive — i.e., the matching value itself is included in the results.
  - `skip` tells PouchDB how many documents to skip from its normal starting point.
  - limit: maximum number of docs to return
- you might recognize `skip` and `limit` as our old friends from SQL: `OFFSET` and `LIMIT`. 
  - You might also imagine that these parameters are the only ones you need for proper pagination. But this is a trap!
  - once `skip` grows to a large number, your performance will start to degrade pretty drastically. 
  - That's because those documents must literally be skipped over with each query, and the database will still read into memory every document that it's skipping. 
- Smart method: leveraging `startkey`, instead of relying on the performance-killer `skip`.
- To be fair, WebSQL and CouchDB (since version 1.1.1) do not suffer from this problem, due to their ability to efficiently count SQLite rows/B-tree offsets. 
  - However, since IndexedDB and LevelDB (and other backends modeled on LevelDOWN) are traditional key-value stores, they don't have a good way to count offsets. 
  - Also, some experimental data suggests that CouchDB 1.5 is still faster with the `startkey` pattern. So you're better off just using `startkey` everywhere.

- PouchDB uses standard JavaScript string ordering. 
  - if you provide your own IDs, you can make sorting incredibly easy for a variety of applications.

- total_rows, you can think of this as your COUNT(*).

## 📝 [12 pro tips for better code with PouchDB_201406](https://pouchdb.com/2014/06/17/12-pro-tips-for-better-code-with-pouchdb.html)

01. Use put(), not post(). put() requires you to supply your own doc ID, whereas post() generates a random one for you
02. Don't `emit(doc.foo, doc)`; use `emit(doc.foo)`;
- you never need to emit() the full document in your map/reduce functions. You can always just use {include_docs: true} when you query
- if you emit the full doc, then it will actually serialize and write out that entire document to disk. 
  - This is true in both PouchDB and CouchDB, and it's pure waste.
03. Don't emit(doc.foo, 1) and then _sum; don't use `_sum` when a simple `_count` will do.
04. Attachments are overrated
- Replicating large attachments is still not recommended, but attachments can be handy if used correctly. blob-util can help.
- NPM has moved away from storing attachments in CouchDB
  - Nowadays they use a CDN for the binaries, and CouchDB just stores the metadata
- In PouchDB, attachments have been one of the biggest sources of bugs, since every browser seems to handle them differently. 
- In general, both CouchDB and PouchDB are just poor fits for storing binary data. (Databases rarely are.) 
- Instead of attachments, try using a CDN or a simple fileserver, and store the URLs or checksums in the database if you need to.
- you should never put your binaries in the database. It's a terrible idea. It always goes wrong. I have never met a database in 15 years of which it is not true, and it's definitely not true of CouchDB.
05. Use plugins, or write your own
06. Don't just update docs for the hell of it
- Every time you modify a document, another revision is added to its revision history – think Git. 
- Except unlike Git, these revisions contain the full document data (not just the diffs), which can take up a lot of space on disk. 
- So if nothing changed in a document, don't bother put()ing it again.
07. Use and abuse your doc IDs
- if you don't want bad performance from your secondary indexes, the best strategy is to avoid secondary indexes altogether. The primary index should be sufficient for sorting and searching in nearly all of your applications, or at least for the hot-path code.
- if you really want to get fancy with your doc IDs, you can use PouchDB Collate to serialize arbitrary data into strings that are sorted according to CouchDB collation ordering. This allows you to index on arrays, objects, numbers
- This is actually what persistent map/reduce uses under the hood!
- for cases where you only need to build complex IDs out of strings, there is also the fantastic DocURI project, which can build a more human-readable ID like this: `movie/gallery-image/12/medium`.
- Choose whichever one fits your app better, or just concatenate the strings yourself.
08. Use Web SQL for better performance.
- since this post was written, IndexedDB performance has improved, and is often better than WebSQL in Chrome. 
09.  Move logic from the map function to query()
- every `map` function you write has to be executed for every single document in your database. No exceptions.
- the query() options like startkey, endkey, key, and keys have been optimized to hell, and they leverage the native indexes in the database to deliver the maximum possible performance.
- Each of those db.query() calls represents a separate temporary index. I.e., all your docs are read in, run through the map function, spit out to an index, queried, and then the whole thing is thrown away. For every query! 
- No need to completely rebuild the index when your query changes; just switch around `startkey/endkey/descending` and friends at query time to get the data you want.
10. You probably don't need reduce
- unless you're running your queries against the server, they don't buy you any performance benefits.
- PouchDB runs in Node or the browser, meaning it's a single-threaded, single-process environment. 
- There's no massive parallelization of the map/reduce functions like you could get with CouchDB
- PouchDB takes a shortcut and just runs every reduce function in memory (there's no point in writing it to disk), meaning it's not doing anything you couldn't just do yourself.
- So if you find yourself writing three different design documents that all emit the same thing but have different reduce functions: don't bother. You can get better performance and smaller code by just writing a single design document with no reduce, and then doing the reduce yourself.
11. Debug with the CouchDB UI. http://localhost:5984/_utils
12. Contribute!
- database isn't really that hard. Keys map to values, stuff's written to disk: it's a cinch(容易做的事情) once you learn the basics.

## 📝 [10 things I learned from reading (and writing) the PouchDB source_201410](https://pouchdb.com/2014/10/26/10-things-i-learned-from-reading-and-writing-the-pouchdb-source.html)

- I first joined the project around December of last year, at which point PouchDB was already fairly mature. (The first commit from Mikeal Rodgers is already 4 years old!)
- The main goals I had with PouchDB were to increase its performance and browser compatibility

01. Nobody can agree on what the Web SQL "estimated size" means
- User agent sniffing! 
- W3C has done everyone a disservice by using 5*1024*1024 in their sample code
02. IE has race conditions in IndexedDB
- we ensure all "open" and "destroy" operations on the databases are done sequentially
03. Binary data in Web SQL is a mess
- At the time the Web SQL spec was hammered out, nothing like Blobs or ArrayBuffers had been standardized
- As of PouchDB 3.1.0, we will also avoid hexing entirely for large binary attachments, because it causes performance problems. 
04. Binary data in IndexedDB is a mess too
- Blobs were not supported in Chrome until v37
  - PouchDB falls back to storing Blobs as base64-encoded strings. 
05. IE doesn't support complex keys
- CouchDB is one of the grandaddies(祖师爷) of NoSQL databases, so unsurprisingly it influenced IndexedDB's design. 
- we're basically trying to rewrite CouchDB on top of IndexedDB.
- it's intentional: we concatenate the strings together, because IE does not support complex keys.
- This also heavily influenced our design for persistent map/reduce, because instead of assuming the underlying database can sort by more than one value, we invented a toIndexableString() function that converts any JSON object into a big CouchDB-collation-ordered string. Yeah, we went there.
06. IndexedDB throws an error if you try to iterate backwards with start/end keys
- You can actually swap the start and end in the `IDBKeyRange`, and that allows you to iterate backwards in all browsers
07. IndexedDB and Web SQL are jealous of other callbacks
- In both IndexedDB and Web SQL, you can forget about using Promises or even invoking another callback within a transaction. Whenever control is returned to the event loop, the transaction auto-closes.
- under the hood, PouchDB's own code is pure callback hell.
08. Recursion is a double-edged sword
- The gist is that any native JavaScript function that takes an object as input, such as `JSON.stringify()` or IndexedDB's `put()`, has a maximum limit on the depth of the object you can pass in. 
- The limit itself will vary based on the available memory, but in any case, if you hit that limit, you get a "too much recursion" or "maximum call stack" error.
- The limit itself will vary based on the available memory, but in any case, if you hit that limit, you get a "too much recursion" or "maximum call stack" error.
09. In IndexedDB, unique indexes throw constraint errors, but keyPaths don't
- This is one of those counter-intuitive things that probably made sense to IndexedDB creator Nikunj Mehta, but surprised the hell out of me.
- In IndexedDB, however, object stores with primary keys will not throw an error upon insertion, but instead silently overwrite the existing object. In other words, the put() is an upsert. 
  - Unique indexes, however, behave totally differently and will indeed throw.
- you can use add() instead of put() to get a constraint error with keyPaths. 
10. CouchDB influenced IndexedDB influenced LevelDB influenced...
- Databases are not designed in a vacuum, and the more I learn about this stuff, the more I find that everything is related somehow.
- Web SQL was originally inspired by Google Gears
  - Web SQL also lives on indirectly in IndexedDB, given that both Mozilla's and Apple's implementations are independently (!) implemented on top of SQLite.
- you can even find the influence of CouchDB in early discussions of IndexedDB
- Google went on to create LevelDB as their implementation of the IndexedDB spec
- PouchDB itself has hopped on the LevelUP bandwagon, and today we have PouchDB Server, which is a nearly-complete implementation of CouchDB's HTTP API, but based on Node.js and LevelDB.

## 👥 [Things I learned from reading and writing the PouchDB source | Hacker News_201411](https://news.ycombinator.com/item?id=8589376)

- I wouldnt write couchbase-lite off entirely, sync is extremely hard and with Pouch we are still struggling with slow replications and bugs with binary objects. 
  - The couchbase-lite devs have been contributing to PouchDB and couchbase-lite, PouchDB and CouchDB should all interoperatate in a p2p environment, if they dont then its a bug
# blogs-sync/collab
- [Use JSON Patch to Resolve Conflicts for CouchDB_202009](https://neighbourhood.ie/blog/2020/09/15/use-json-patch-to-resolve-conflicts/)

## [figma: LiveGraph: real-time data fetching at Figma | Figma Blog_202110](https://www.figma.com/blog/livegraph-real-time-data-fetching-at-figma/)

- how do we empower our product engineers to build these real-time views easily, while abstracting away the complexity of pushing data back and forth?
  - 👉🏻 To provide a general solution to this fundamental business need, we developed LiveGraph, **a data fetching layer on top of Postgres that allows our frontend code to request real-time data subscriptions expressed with GraphQL**. 
  - It issues queries directly to the database and provides live updates in the order of(~of/in the order of sth, 大约、数量级) milliseconds by reading the database replication stream.

- We realized that we needed a more general framework that would allow product developers to declaratively define data subscriptions. 
  - A natural choice for this interface was to use GraphQL, which would allow the system to automatically fetch and keep the data live-updated. We decided to build it in-house and call it LiveGraph.
# blogs-couchdb-user

## [Creating a Multiple User App with PouchDB & CouchDB_201801](https://www.joshmorony.com/creating-a-multiple-user-app-with-pouchdb-couchdb/)

01. Create your own API
02. Use a single database
03. Create a database for each user

## [Solving "one database per user" in CouchDB/IrisCouch/Cloudant_201704](https://gist.github.com/nolanlawson/9676093)

- the CouchDB docker image now has a built-in `couch-per-user` support, making this much easier to implement
# blogs-couchdb

## [10 Common Misconceptions about Apache CouchDB - Speaker Deck_201311](https://speakerdeck.com/wohali/10-common-misconceptions-about-apache-couchdb)

### [Another 10 Common Misconceptions about Apache CouchDB - Speaker Deck_201809](https://speakerdeck.com/wohali/another-10-common-misconceptions-about-apache-couchdb)

## [Upscaling LinkedIn's Profile Datastore While Reducing Costs | LinkedIn Engineering_202305](https://engineering.linkedin.com/blog/2023/upscaling-profile-datastore-while-reducing-costs)

- Instead, we chose to introduce Couchbase as a centralized storage tier cache for read scaling. 
  - This solution achieved a cache hit rate of over 99%, reduced tail latencies by more than 60%, and trimmed the cost to serve by 10% annually. 

### [How LinkedIn Serves 5 Million User Profiles per Second](https://blog.quastor.org/p/linkedin-serves-5-million-user-profiles-per-second)

- Couchbase is a combination of ideas from Membase and CouchDB, where you have the highly scalable caching layer of Membase and the flexible data model of CouchDB.
  - It’s both a key/value store and a document store, so you can perform Create/Read/Update/Delete (CRUD) operations using the simple API of a key/value store (add, set, get, etc.) but the value can be represented as a JSON document.
  - With this, you can access your data with the primary key (like you would with a key/value store), or you can use N1QL (pronounced nickel). This is an SQL-like query language for Couchbase that allows you to retrieve your data arbitrarily and also do joins and aggregation.

## 🆚️ [Couchbase vs. MongoDB: NoSQL Misconceptions Part 1 - What about SQL?_202206](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-1/)

- [Couchbase vs. MongoDB: Part 2 - Is Couchbase just a Key-Value Store? _202206](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-2/)
- [Is NoSQL Database Secure? Couchbase vs. MongoDB (Part 3)_202207](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-3/)
- [Are NoSQL Databases Scalable? Couchbase vs. MongoDB (Part 4)_202207](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-4/)
- [Memory Usage in Databases: Buffering & Caching (Part 5)_202207](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-5/)

- [NoSQL Document Database Replication - MongoDB vs. Couchbase_202003](https://www.couchbase.com/blog/replication-in-nosql-document-databases-mongo-db-vs-couchbase/)

## 🆚️ [CouchDB and MongoDB Compared](https://www.mongodb.com/compare/couchdb-vs-mongodb)

- Although MongoDB and CouchDB share a similar concept of a document-oriented database, there are some key advantages to MongoDB over CouchDB technology as well as some key differences we should address.

- MongoDB is a document database built for general-purpose usage. 
  - It stores data in an optimized JSON format called BSON (Binary JSON). 
    - This allows the MongoDB document model to benefit from the flexibility of JSON documents stored in logical groups called collections. 
    - The document model supports many different data types, including strings, dates, numbers, arrays, decimals, nested objects, geo data, and binary data.
  - MongoDB uses replication and data partitioning called sharding to distribute data for high availability and scalability purposes
  - Additionally, MongoDB Enterprise and MongoDB Atlas offer enterprise-grade security features like authentication, authorization, and LDAP support as well as end-to-end encryption.

- CouchDB is a NoSQL document-oriented database implemented in Erlang. 
  - CouchDB documents are JSON-based and stored in databases. 
  - The database software can be installed as a single instance or a cluster of instances for durability and high availability. 
    - CouchDB’s overall design favors availability over consistency, and is considered eventually consistent in many read scenarios.
  - CouchDB is designed on the concept of “optimistic concurrency, ” which places an added burden on the application for handling data consistency. 
  - The query system does not lock database objects on writes, meaning any conflict resolution or locking mechanisms for consistency need to be implemented by the application developer.
  - CouchDB uses an HTTP Rest API to perform database access and document manipulation, rather than native drivers using a unified query language like many other modern databases. It supports basic types of authentication like session cookies/users and TLS/SSL for the Rest API traffic.

- comparison table
- Data Model
  - couchdb data formats are limited to: strings, numbers, arrays, objects, boolean.
  - mongodb: strings, numbers, geo data, dates, arrays, decimal, nested objects, binary data.
- Indexing
  - couchdb: Indexing of documents is limited. For some workloads, indexing requires a special “Design Document” definition.
  - mongodb: Secondary indexes on any field are available and supported in different types: Compound, Text, Geo, TTL
- Query Language
  - couchdb: If you require more complex queries, you will need to use views and map-reduce aggregations to filter and query your documents.
- Transactions
  - 😩 CouchDB does not support transactions.
- Concurrency
  - CouchDB is eventually consistent and uses optimistic locking as part of its database operations. Write operations do not lock database objects and conflict errors need to be resolved by the application developer.
  - MongoDB uses document level locking so writes to a single document occur either in full or not at all, and clients always see consistent data.
  - MongoDB supports different read and write concerns for distributed clusters and retryable reads and writes.
- High Availability and Scalability
  - CouchDB supports a concept of a replication factor as well as a sharding setting on a global or per database basis.
  - MongoDB was built from the ground up to support distribution of data using replication and sharding mechanisms. Replica sets host an identical copy of the data and elect a primary which receives all the writes, while other nodes are secondaries replicating all the data. Sharding allows you to easily scale your collections across multiple replica sets.
- Security
  - CouchDB security is built for simple website backend requirements
  - mongodb: Authentication and authorization using built-in SCRAM or certificates
- Mobile Support
  - PouchDB: Conflict resolution needs to be solved by the developer.
  - Realm is a lightweight reactive object-store designed to work seamlessly with mobile frameworks.

## 🆚️ [Couchbase vs CouchDB NoSQL Systems: Difference Between Them](https://www.couchbase.com/comparing-couchbase-vs-couchdb/)

## 📕 [Couchbase Under the Hood](https://info.couchbase.com/rs/302-GJY-034/images/Couchbase_Under_The_Hood_WP.pdf)

- The original multi-model NoSQL database Couchbase was originally founded through the merger of two open source database companies, CouchOne and Membase.
  - CouchOne employed developers of Apache CouchDB, an original, highly-reliable, document database, while Membase employed developers of memcached, a high- performance, memory-first, key-value database. 
  - The merger of these teams led to the design of Couchbase, a reliable, scalable, fast in-memory, key-value database with document-based access and storage. 
  - In this model, document identification “keys” store “value” data as a JSON document. 
- Couchbase was the first of its kind, dual model access database, setting the standard for advancing consolidation(联合或合并) of single-access NoSQL datastores. 
  - Couchbase further distanced itself from its origin sources by adding support for SQL++ (aka N1QL) as its primary query language.

- Couchbase is a pioneer in offering multiple data access methods to gain, read, and update access to its foundational JSON and Key/Value storage structures. 
  - This type of NoSQL database is referred to as “multimodel” because many NoSQL systems have only one access method which is bound to their physical storage design structures on disk to minimize access latency.
- While many developers may confuse the two, Couchbase and CouchDB are not the same

- Couchbase has also introduced a new storage engine format which is defined as buckets are created
- Magma combines the performance of a log-structured merge trees (LSM) with the compaction, reorganizability, and immutability of sorted string tables (SSTables) to provide a high performance in a well organized, low latency engine that suits write-heavy, low latency point lookup workloads. 
  - This design minimizes disk space increases, called “storage amplifications, ” and the accompanying complexity which occurs when documents are heavily mutated without being reorganized.

### [Magma Storage Engine: Couchstore and Magma Comparison_202210](https://www.couchbase.com/blog/magma-next-gen-document-storage-engine/)

- The Couchbase database platform supports two storage mechanisms: Couchstore, the default, and Magma, the recently released engine.

- Couchstore is a mature storage engine that is optimized for high performance with large datasets, particularly ones that can fit in memory. 
  - The minimum bucket size for Couchstore is 100MB. 
  - It’s ideal for caching use cases and situations where data compression is not a primary deciding factor. 
- Magma is a new storage engine that is designed to be highly performant even with very large datasets that do not fit in memory.
  - Magma is optimized to run on very low amounts of memory even with very large datasets

- The performance evaluation results showed that Magma outperformed both Couchstore and RocksDB engines in write-heavy YCSB workloads with datasets that were too large for memory.
# more
- [Database Deep Dives: CouchDB - IBM Blog_201907](https://www.ibm.com/blog/database-deep-dives-couchdb/)

- [Building Multi-platform apps with React, Cordova, CouchDB/PouchDB, . NET, Kubernetes and Azure_202012](https://blog.adaptabi.com/building-multi-platform-apps-with-react-cordova-couchdb-pouchdb-net-kubernetes-and-azure-9c1a946ccc36)
  - [Part 1 — The Database. How to build a real time data sync, multi platform app with CouchDB and PouchDB_202012](https://blog.adaptabi.com/part-1-the-database-b7c575864407)
