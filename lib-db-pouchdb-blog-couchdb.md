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

## 📝 [A Veteran's(老兵) Guide to PouchDB](https://garbados.github.io/my-blog/veteran-pouchdb.html)

## [Local-first database: RxDB + PouchDB_202005](https://jaredforsyth.com/posts/local-first-database-rxdb-pouchdb/)

- I’ve thought about using a state-based json-crdt for each document, which would allow a client implementation to automatically resolve conflicts in a way that better preserves intent, but I haven’t attempted this. 
  - One option that’s mentioned in the docs is delta-pouch, which “stores every change as its own document”, and then reads out those changes to construct the “current” state of a document.
  - I’m a little wary about the “production-readiness” of this plugin, though, as shoehorning(强挤硬塞) a delta-based system onto pouchdb seems like it would introduce some pretty significant performance penalties(处罚；不利；损失).

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

## [LiveGraph: real-time data fetching at Figma | Figma Blog_202110](https://www.figma.com/blog/livegraph-real-time-data-fetching-at-figma/)

- how do we empower our product engineers to build these real-time views easily, while abstracting away the complexity of pushing data back and forth?
  - 👉🏻 To provide a general solution to this fundamental business need, we developed LiveGraph, **a data fetching layer on top of Postgres that allows our frontend code to request real-time data subscriptions expressed with GraphQL**. 
  - It issues queries directly to the database and provides live updates in the order of(~of/in the order of sth, 大约、数量级) milliseconds by reading the database replication stream.

- We realized that we needed a more general framework that would allow product developers to declaratively define data subscriptions. 
  - A natural choice for this interface was to use GraphQL, which would allow the system to automatically fetch and keep the data live-updated. We decided to build it in-house and call it LiveGraph.
# blogs-couchdb

## [Upscaling LinkedIn's Profile Datastore While Reducing Costs | LinkedIn Engineering_202305](https://engineering.linkedin.com/blog/2023/upscaling-profile-datastore-while-reducing-costs)

- Instead, we chose to introduce Couchbase as a centralized storage tier cache for read scaling. 
  - This solution achieved a cache hit rate of over 99%, reduced tail latencies by more than 60%, and trimmed the cost to serve by 10% annually. 
- 
- 
- 

### [How LinkedIn Serves 5 Million User Profiles per Second](https://blog.quastor.org/p/linkedin-serves-5-million-user-profiles-per-second)

- Couchbase is a combination of ideas from Membase and CouchDB, where you have the highly scalable caching layer of Membase and the flexible data model of CouchDB.
  - It’s both a key/value store and a document store, so you can perform Create/Read/Update/Delete (CRUD) operations using the simple API of a key/value store (add, set, get, etc.) but the value can be represented as a JSON document.
  - With this, you can access your data with the primary key (like you would with a key/value store), or you can use N1QL (pronounced nickel). This is an SQL-like query language for Couchbase that allows you to retrieve your data arbitrarily and also do joins and aggregation.

- 
- 
- 

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

## [Magma Storage Engine: Couchstore and Magma Comparison_202210](https://www.couchbase.com/blog/magma-next-gen-document-storage-engine/)

- The Couchbase database platform supports two storage mechanisms: Couchstore, the default, and Magma, the recently released engine.

- Couchstore is a mature storage engine that is optimized for high performance with large datasets, particularly ones that can fit in memory. 
  - The minimum bucket size for Couchstore is 100MB. 
  - It’s ideal for caching use cases and situations where data compression is not a primary deciding factor. 
- Magma is a new storage engine that is designed to be highly performant even with very large datasets that do not fit in memory.
  - Magma is optimized to run on very low amounts of memory even with very large datasets

- The performance evaluation results showed that Magma outperformed both Couchstore and RocksDB engines in write-heavy YCSB workloads with datasets that were too large for memory.

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
# more
- [Building Multi-platform apps with React, Cordova, CouchDB/PouchDB, . NET, Kubernetes and Azure_202012](https://blog.adaptabi.com/building-multi-platform-apps-with-react-cordova-couchdb-pouchdb-net-kubernetes-and-azure-9c1a946ccc36)
  - [Part 1 — The Database. How to build a real time data sync, multi platform app with CouchDB and PouchDB_202012](https://blog.adaptabi.com/part-1-the-database-b7c575864407)
