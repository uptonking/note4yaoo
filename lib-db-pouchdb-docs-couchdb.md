---
title: lib-db-pouchdb-docs-couchdb
tags: [couchdb, docs, pouchdb]
created: 2023-11-07T10:22:22.504Z
modified: 2023-11-07T10:22:34.529Z
---

# lib-db-pouchdb-docs-couchdb

# guide

- resources
  - [Fauxton Visual Guide: 提供了admin界面使用说明、faq](https://couchdb.apache.org/fauxton-visual-guide/index.html#answers)
# [docs-couchdb](https://docs.couchdb.org/en/stable/)
- features-couchdb
  - Single Node Database: works just like any other database behind an application server of your choice
  - Cluster: improves on the single-node setup with higher capacity and high-availability without changing any APIs
  - HTTP/JSON: makes use of the ubiquitous HTTP protocol and JSON data format and is compatible with any software that supports them
  - Offline First Data Sync: CouchDB’s unique Replication Protocol is the foundation for offline first
  - Ecosystem: PouchDB is built for mobile & web-browsers, Fauxton
  - Reliability: Individual nodes use a crash-resistant append-only data structure. A multi-node CouchDB cluster saves all data redundantly

- CouchDB is a database that completely embraces the web
  - features, such as on-the-fly document transformation and real-time change notifications, make web development a breeze
  - multi-master syncing database with an intuitive HTTP/JSON API, designed for reliability
- We care a lot about distributed scaling. CouchDB is highly available and partition tolerant, but is also eventually consistent

## [4. Best Practices — Apache CouchDB® Documentation](https://docs.couchdb.org/en/stable/best-practices/index.html)

- 4.1. Document Design Considerations
- 4.1.1. Don’t rely on CouchDB’s auto-UUID generation
  - If for any reason you miss the 200 OK reply from CouchDB, and storing the document is attempted again, you would end up with the same document content stored under multiple _ids. 
  - This could easily happen with intermediary proxies and cache systems that may not inform developers that the failed transaction is being retried.
  - _ids are the only unique enforced value within CouchDB so you might as well make use of this. CouchDB stores its documents in a B+ tree. Each additional or updated document is stored as a leaf node, and may require re-writing intermediary and parent nodes. You may be able to take advantage of sequencing your own ids more effectively than the automatically generated ids if you can arrange them to be sequential yourself.
- 4.1.2. Alternatives to auto-incrementing sequences
  - Because of replication, as well as the distributed nature of CouchDB, it is not practical to use auto-incrementing sequences with CouchDB
- 4.1.3. Pre-aggregating your data
  - If your intent for CouchDB is as a collect-and-report model, not a real-time view, you may not need to store a single document for every event you’re recording. In this case, pre-aggregating your data may be a good idea. 
  - In this case, using an in-memory store to summarize your statistical information, then writing out to CouchDB every 10 seconds / 1 minute / whatever level of granularity you need would greatly reduce the number of documents you’ll put in your database
  - Later, you can then further decimate your data by walking the entire database and generating documents to be stored in a new database with a lower level of granularity (say, 1 document a day).
- 4.1.4. Designing an application to work with replication
  - CouchDB does not provide a mechanism for this itself. It stores arbitrary numbers of old _ids for one document (trunk now has a mechanism for pruning the _id history), for the purposes of replication. However it will not keep the documents themselves through a compaction cycle, except where there are conflicting versions of a document.
  - Do not rely on the CouchDB revision history mechanism to help you build an application-level version history. Its sole purpose is to ensure eventually consistent replication between databases.
  - Approach 1: Single JSON doc
  - Approach 2: Separate document per field. A better way is to keep a string representation of index, which can grow as the tree is subdivided.
  - Approach 3: Immutable history / event sourcing
  - Approach 4: Keep historic versions explicitly
- 4.1.5. Adding client-side security with a translucent(半透明的; 真实的；毫不虚假的) database
  - The simplest solutions use a one-way function like SHA-256 at the client to scramble the name and password before storing the information. This solution gives the client control of the data in the database without requiring a thick layer on the database to test each transaction.
  - There are many variations on this theme detailed in the book Translucent Databases

- 4.2. Document submission using HTML Forms
- 4.2.1. The HTML form
- 4.2.2. The update function
- 4.2.3. Example output
- As CouchDB no longer recommends the use of CouchDB-hosted web applications, you may want to use a reverse proxy to expose CouchDB as a subdirectory of your web application
- Another option is to alter CouchDB’s CORS settings and use a cross-domain POST. 

- 4.3. Using an ISO Formatted Date for Document IDs
  - The ISO 8601 date standard describes a useful scheme for representing a date string in a `Year-Month-DayTHour:Minute:Second.microsecond` format. 
  - For time-bound documents in a CouchDB database this can be a very handy way to create a unique identifier, since JavaScript can directly use it to create a `Date` object. 

- 4.4. JavaScript development tips
- Be sure to guard all document accesses to avoid exceptions when fields or subfields are missing: `if (doc && doc.myarray && doc.myarray.length)`.

- 4.5. View recommendations
- 4.5.1. Deploying a view change in a live environment
- It is possible to change the definition of a view, build the index, then make those changes go live without causing downtime for your application. 
  - The trick to making this work is that CouchDB’s JavaScript view index files are based on the contents of the design document - not its name, _id or revision. 
  - This means that two design documents with identical view code will share the same on-disk view index files.

- 4.6. Reverse Proxies
  - CouchDB recommends the use of HAProxy as a load balancer and reverse proxy.
  - Reverse proxying with HAProxy/nginx/Caddy/Apache HTTP Server

## [3.2.4. View Cookbook for SQL Jockeys](https://docs.couchdb.org/en/stable/ddocs/views/nosql.html)

- This is a collection of some common SQL queries and how to get the same result in CouchDB.
- 3.2.4.1. Using Views
- 3.2.4.2. Look Up by Key
- 3.2.4.3. Look Up by Prefix
- 3.2.4.4. Aggregate Functions
- 3.2.4.5. Get Unique Values
- 3.2.4.6. Enforcing Uniqueness

## [1.1. Technical Overview — Apache CouchDB® Documentation](https://docs.couchdb.org/en/stable/intro/overview.html)

- A CouchDB server hosts named databases, which store documents. 
  - Each document is uniquely named in the database, 
  - and CouchDB provides a RESTful HTTP API for reading and updating (add, edit, delete) database documents.
- Documents are the primary unit of data in CouchDB and consist of any number of fields and attachments. 
  - Documents also include metadata that’s maintained by the database system. 
  - Document fields are uniquely named and contain values of varying types (text, number, boolean, lists, etc), and there is no set limit to text size or element count.
- The CouchDB document update model is lockless and optimistic. 
  - Document edits are made by client applications loading documents, applying changes, and saving them back to the database. 
  - If another client editing the same document saves their changes first, the client gets an edit conflict error on save. 
  - To resolve the update conflict, the latest document version can be opened, the edits reapplied and the update tried again.
- Single document updates (add, edit, delete) are all or nothing, either succeeding entirely or failing completely. The database never contains partially saved or edited documents.

- The CouchDB file layout and commitment system features all Atomic Consistent Isolated Durable (ACID) properties. 
  - On-disk, CouchDB never overwrites committed data or associated structures, ensuring the database file is always in a consistent state. 
  - This is a “crash-only” design where the CouchDB server does not go through a shut down process, it’s simply terminated.
- Document updates (add, edit, delete) are serialized, except for binary blobs which are written concurrently. 
  - Database readers are never locked out and never have to wait on writers or other readers. 
  - Any number of clients can be reading documents without being locked out or interrupted by concurrent updates, even on the same document.
  - CouchDB read operations use a Multi-Version Concurrency Control (MVCC) model where each client sees a consistent snapshot of the database from the beginning to the end of the read operation. 
  - This means that CouchDB can guarantee transactional semantics on a per-document basis.
- Documents are indexed in B-trees by their name (DocID) and a Sequence ID. 
  - Each update to a database instance generates a new sequential number. Sequence IDs are used later for incrementally finding changes in a database. 
  - These B-tree indexes are updated simultaneously when documents are saved or deleted. 
  - The index updates always occur at the end of the file (append-only updates).
- Documents have the advantage of data being already conveniently packaged for storage rather than split out across numerous tables and rows in most database systems.
  - When documents are committed to disk, the document fields and metadata are packed into buffers, sequentially one document after another (helpful later for efficient building of views).
- When CouchDB documents are updated, all data and associated indexes are flushed to disk and the transactional commit always leaves the database in a completely consistent state. 
- 👉🏻 Commits occur in two steps:
  - All document data and associated index updates are synchronously flushed to disk.
  - The updated database header is written in two consecutive, identical chunks to make up the first 4k of the file, and then synchronously flushed to disk.

- Wasted space is recovered by occasional compaction. 
  - On schedule, or when the database file exceeds a certain amount of wasted space, 👉🏻 the compaction process clones all the active data to a new file and then discards the old file. 
  - The database remains completely online the entire time and all updates and reads are allowed to complete successfully. 
  - The old database file is deleted only when all the data has been copied and all users transitioned to the new file.

- Unlike SQL databases where data must be carefully decomposed into tables, data in CouchDB is stored in semi-structured documents. 
  - CouchDB documents are flexible and each has its own implicit structure, which alleviates the most difficult problems and pitfalls of bi-directionally replicating table schemas and their contained data.

- To address this problem of adding structure back to unstructured and semi-structured data, CouchDB integrates a view model. 
- 👁‍🗨 Views are the method of aggregating and reporting on the documents in a database, and are built on-demand to aggregate, join and report on database documents. 
  - Because views are built dynamically and don’t affect the underlying document, you can have as many different view representations of the same data as you like.
- View definitions are strictly virtual and only display the documents from the current database instance, making them separate from the data they display and compatible with replication. 
  - 👉🏻 CouchDB views are defined inside special design documents and can replicate across database instances like regular documents, so that not only data replicates in CouchDB, but entire application designs replicate too.
- Views are defined using JavaScript functions acting as the `map` part in a `map-reduce` system. 
  - A view function takes a CouchDB document as an argument and then does whatever computation it needs to do to determine the data that is to be made available through the view, if any. 
  - It can add multiple rows to the view based on a single document, or it can add no rows at all.
- Views are a dynamic representation of the actual document contents of a database
  - generating a view of a database with hundreds of thousands or millions of documents is time and resource consuming, it’s not something the system should do from scratch each time.
- To keep view querying fast, the view engine maintains indexes of its views, and incrementally updates them to reflect changes in the database. 
  - CouchDB’s core design is largely optimized around the need for efficient, incremental creation of views and their indexes.
- Views and their functions are defined inside special “design” documents, and a design document may contain any number of uniquely named view functions. 
- 👉🏻 When a user opens a view and its index is automatically updated, all the views in the same design document are indexed as a single group.
- The view builder uses the database sequence ID to determine if the view group is fully up-to-date with the database. 
  - If not, the view engine examines all database documents (in packed sequential order) changed since the last refresh. 
  - Documents are read in the order they occur in the disk file, reducing the frequency and cost of disk head seeks.
- The views can be read and queried simultaneously while also being refreshed. If a client is slowly streaming out the contents of a large view, the same view can be concurrently opened and refreshed for another client without blocking the first client. 
- As documents are processed by the view engine through your ‘map’ and ‘reduce’ functions, their previous row values are removed from the view indexes, if they exist. If the document is selected by a view function, the function results are inserted into the view as a new row.
- When view index changes are written to disk, the updates are always appended at the end of the file, serving to both reduce disk head seek times during disk commits and to ensure crashes and power failures can not cause corruption of indexes. 
  - If a crash occurs while updating a view index, the incomplete index updates are simply lost and rebuilt incrementally from its previously committed state.

- To protect who can read and update documents, CouchDB has a simple reader access and update validation model that can be extended to implement custom security models.
- CouchDB database instances have administrator accounts. 
  - Administrator accounts can create other administrator accounts and update design documents. 
  - Design documents are special documents containing view definitions and other special formulas, as well as regular fields and blobs.
- The update validations are enforced for both live usage and replicated updates, ensuring security and data validation in a shared, distributed system.

- CouchDB is a peer-based distributed database system. It allows users and servers to access and update the same shared data while disconnected. Those changes can then be replicated bi-directionally later.
- Both documents and designs can replicate, allowing full database applications (including application design, logic and data) to be replicated to laptops for offline use
- The replication process is incremental. At the database level, replication only examines documents updated since the last replication. If replication fails at any step, due to network problems or crash for example, the next replication restarts at the last checkpoint
- 👉🏻 Partial replicas can be created and maintained. 
  - Replication can be filtered by a JavaScript function, so that only particular documents or those meeting specific criteria are replicated. 
  - This can allow users to take subsets of a large shared database application offline for their own use, while maintaining normal interaction with the application and that subset of data.

- The CouchDB storage system treats edit conflicts as a common state, not an exceptional one. 
- The conflict handling model is simple and “non-destructive” while preserving single document semantics and allowing for decentralized conflict resolution.
- 👉🏻 CouchDB allows for any number of conflicting documents to exist simultaneously in the database, with each database instance deterministically deciding which document is the “winner” and which are conflicts. 
  - Only the winning document can appear in views, while “losing” conflicts are still accessible and remain in the database until deleted or purged during database compaction. 
  - Because conflict documents are still regular documents, they replicate just like regular documents and are subject to the same security and validation rules.
- When distributed edit conflicts occur, every database replica sees the same winning revision and each has the opportunity to resolve the conflict. 
  - Resolving conflicts can be done manually or, depending on the nature of the data and the conflict, by automated agents. 
  - The system makes decentralized conflict resolution possible while maintaining single document database semantics.
- Conflict management continues to work even if multiple disconnected users or agents attempt to resolve the same conflicts. 
  - If resolved conflicts result in more conflicts, the system accommodates them in the same manner, determining the same winner on each machine and maintaining single document semantics.

- Using just the basic replication model, many traditionally single server database applications can be made distributed with almost no extra work. CouchDB replication is designed to be immediately useful for basic database applications

- CouchDB is built on the Erlang OTP platform, a functional, concurrent programming language and development platform
  - Erlang uses lightweight “processes” and message passing for concurrency, it has no shared state threading and all data is immutable. 
  - The robust, concurrent nature of Erlang is ideal for a database server.
- For higher availability and more concurrent users, CouchDB is designed for “shared nothing” clustering. 
  - In a “shared nothing” cluster, each machine is independent and replicates data with its cluster mates, allowing individual server failures with zero downtime

## [1.2. Why CouchDB?](https://docs.couchdb.org/en/stable/intro/why.html)

- Relax
- Its internal architecture is fault-tolerant, and failures occur in a controlled environment and are dealt with gracefully. Single problems do not cascade through an entire server system but stay isolated in single requests.
- CouchDB is also designed to handle varying traffic gracefully. 

- A Different Way to Model Your Data
- CouchDB combines an intuitive document storage model with a powerful query engine

- A Better Fit for Common Applications
- CouchDB is a great fit for common applications because it embraces the natural idea of evolving, self-contained documents as the very core of its data model.
- An invoice contains all the pertinent information about a single transaction the seller, the buyer, the date, and a list of the items or services sold. 
  - there’s no abstract reference on this piece of paper that points to some other piece of paper with the seller’s name and address
  - Yet using references is exactly how we model our data in a relational database
  - We call this “self-contained” data, and it’s an important concept in understanding document databases like CouchDB.
- While a traditional relational database requires you to model your data up front, CouchDB’s schema-free design unburdens you with a powerful way to aggregate your data after the fact, just like we do with real-world documents

- Building Blocks for Larger Systems
- Whether you need a system that’s crazy fast but isn’t too concerned with reliability (think logging), or one that guarantees storage in two or more physically separated locations for reliability, but you’re willing to take a performance hit, CouchDB lets you build these systems.
- CouchDB is no silver bullet – but in the area of data storage, it can get you a long way.

- CouchDB Replication
- Its fundamental function is to synchronize two or more CouchDB databases. 
- This may sound simple, but the simplicity is key to allowing replication to solve a number of problems: 
  - reliably synchronize databases between multiple machines for redundant data storage; 
  - distribute data to a cluster of CouchDB instances that share a subset of the total number of requests that hit the cluster (load balancing); 
  - and distribute data between physically distant locations
- CouchDB replication uses the same REST API all clients use.
- Replication works incrementally; that is, if during replication anything goes wrong, like dropping your network connection, it will pick up where it left off the next time it runs. It also only transfers data that is needed to synchronize databases.
- CouchDB doesn’t try to hide the network; it just handles errors gracefully and lets you know when actions on your end are required.

- Local Data
- Mobile applications can then use the local CouchDB to fetch data, and since no remote networking is required for that, latency is low by default.

## [1.3. Eventual Consistency](https://docs.couchdb.org/en/stable/intro/consistency.html)

- Consistency: All database clients see the same data, even with concurrent updates.
- Availability: All database clients are able to access some version of the data.
- Partition tolerance: The database can be split over multiple servers.

- the traditional relational database approach to consistency makes it very easy for application programmers to rely on global state, global clocks, and other high availability no-nos, without even realizing that they’re doing so.
- The CAP theorem describes a few different strategies for distributing application logic across networks. 
  - CouchDB’s solution uses replication to propagate application changes across participating nodes. 
  - This is a fundamentally different approach from consensus algorithms and relational databases

- When a system grows large enough that a single database node is unable to handle the load placed on it, a sensible solution is to add more servers. 
  - When we add nodes, we have to start thinking about how to partition data between them
- Regardless of which approach we take, the one problem we’ll keep bumping into is that of keeping all these database servers in sync.
  - If you write some information to one node, how are you going to make sure that a read request to another database server reflects this newest information? 
  - These events might be milliseconds apart. Even with a modest collection of database servers, this problem can become extremely complex.
- If availability is a priority, we can let clients write data to one node of the database without waiting for other nodes to come into agreement. If the database knows how to take care of reconciling these operations between nodes, we achieve a sort of “eventual consistency” in exchange for high availability. This is a surprisingly applicable trade-off for many applications.
- Unlike traditional relational databases, where each action performed is necessarily subject to database-wide consistency checks, CouchDB makes it really simple to build applications that sacrifice immediate consistency for the huge performance improvements that come with simple distribution.

- At the heart of CouchDB is a powerful B-tree storage engine. 
  - A B-tree is a sorted data structure that allows for searches, insertions, and deletions in logarithmic time. 
  - CouchDB uses this B-tree storage engine for all internal data, documents, and views. 
- CouchDB uses MapReduce to compute the results of a view. 
  - MapReduce makes use of two functions, “map” and “reduce”, which are applied to each document in isolation. 
  - Being able to isolate these operations means that view computation lends itself to parallel and incremental computation. 
  - More important, because these functions produce key/value pairs, CouchDB is able to insert them into the B-tree storage engine, sorted by key. 
  - Lookups by key, or key range, are extremely efficient operations with a B-tree, described in big O notation as O(log N) and O(log N + K), respectively.
- In CouchDB, we access documents and view results by key or key range. 
  - This is a direct mapping to the underlying operations performed on CouchDB’s B-tree storage engine. 
  - Along with document inserts and updates, this direct mapping is the reason we describe CouchDB’s API as being a thin wrapper around the database core.
- 👉🏻 Being able to access results by key alone is a very important restriction because it allows us to make huge performance gains. 
  - As well as the massive speed improvements, we can partition our data over multiple nodes, without affecting our ability to query each node in isolation. 
  - BigTable, Hadoop, SimpleDB, and memcached restrict object lookups by key for exactly these reasons.

- No Locking
- A table in a relational database is a single data structure. 
  - If you want to modify a table – say, update a row – the database system must ensure that nobody else is trying to update that row and that nobody can read from that row while it is being updated. 
  - The common way to handle this uses what’s known as a lock. 
  - If multiple clients want to access a table, the first client gets the lock, making everybody else wait. 
  - This serial execution of requests, even when they arrived in parallel, wastes a significant amount of your server’s processing power.
- Modern relational databases avoid locks by implementing MVCC under the hood, but hide it from the end user, requiring them to coordinate concurrent changes of single rows or fields.
- Instead of locks, CouchDB uses Multi-Version Concurrency Control (MVCC) to manage concurrent access to the database.
  - Requests are run in parallel
- Documents in CouchDB are versioned, much like they would be in a regular version control system such as Subversion. 
  - If you want to change a value in a document, you create an entire new version of that document and save it over the old one. 
  - After doing this, you end up with two versions of the same document, one old and one new.
- A read request will always see the most recent snapshot of your database at the time of the beginning of the request.

- Validation
- CouchDB provides a powerful way to perform per-document validation from within the database.
- CouchDB can validate documents using JavaScript functions similar to those used for MapReduce. 
  - Each time you try to modify a document, CouchDB will pass the validation function a copy of the existing document, a copy of the new document, and a collection of additional information, such as user authentication details. 
  - The validation function now has the opportunity to approve or deny the update.

- maintain consistency between multiple database servers
  - You could use multi-master, single-master, partitioning, sharding, write-through caches, and all sorts of other complex techniques.

- Incremental Replication
- Incremental replication is a process where document changes are periodically copied between servers. 
- We are able to build what’s known as a shared nothing cluster of databases where each node is independent and self-sufficient, leaving no single point of contention across the system.
- Need to scale out your CouchDB database cluster? Just throw in another server.
- 👉🏻 CouchDB’s replication system comes with automatic conflict detection and resolution. 
  - When CouchDB detects that a document has been changed in both databases, it flags this document as being in conflict, much like they would be in a regular version control system.
  - When two versions of a document conflict during replication, **the winning version is saved as the most recent version in the document’s history**. 
  - Instead of throwing the losing version away, CouchDB saves this as a previous version in the document’s history, so that you can access it if you need to. 
  - This happens automatically and consistently, so both databases will make exactly the same choice.
- It is up to you to handle conflicts in a way that makes sense for your application. You can leave the chosen document versions in place, revert to the older version, or try to merge the two versions and save the result.

- CouchDB’s design borrows heavily from web architecture and the lessons learned deploying massively distributed systems on that architecture.

## [1.5. Security](https://docs.couchdb.org/en/stable/intro/security.html)

- CouchDB has the idea of an admin user (e.g. an administrator, a super user, or root) that is allowed to do anything to a CouchDB installation. 
  - By default, one admin user must be created for CouchDB to start up successfully.
  - CouchDB also defines a set of requests that only admin users are allowed to do. 
- CouchDB administrators are defined within the config file
- if regular users are also stored there?
  - No, they are not. CouchDB has a special authentication database, named `_users` by default, that stores all registered users as JSON documents.
  - This special database is a system database.

- Each database on a CouchDB server can contain its own set of authorization rules that specify which users are allowed to read and write documents, create design documents, and change certain database configuration parameters. 
  - The authorization rules are set up by a server admin and can be modified at any time.
- Database authorization rules assign a user into one of two classes:
  - members, who are allowed to read all documents and create and modify any document except for design documents.
  - admins, who can read and write all types of documents, modify which users are members or admins, and set certain per-database configuration options.
- Note that a database admin is not the same as a server admin – the actions of a database admin are restricted to a specific database.

## [1.7. The Core API](https://docs.couchdb.org/en/stable/intro/api.html)

- Documents are CouchDB’s central data structure. 
  - The idea behind a document is, unsurprisingly, that of a real-world document – a sheet of paper such as an invoice, a recipe, or a business card
- Each document in CouchDB has an ID. This ID is unique per database. 
  - You are free to choose any string to be the ID, but for best results we recommend a UUID 
  - you should notice that CouchDB added two fields to your JSON structure. The first is `_id`. The second field is `_rev`. It stands for revision.

- ✏️ If you want to change a document in CouchDB, you load the full document out of CouchDB, make your changes in the JSON structure (or object, when you are doing actual programming), and save the entire new revision (or version) of that document back into CouchDB. 
  - Each revision is identified by a new `_rev` value.
- If you want to update or delete a document, CouchDB expects you to include the `_rev` field of the revision you wish to change. 
  - When CouchDB accepts the change, it will generate a new revision number. 
  - This mechanism ensures that, in case somebody else made a change without you knowing before you got to request the document update, CouchDB will not accept your update because you are likely to overwrite data you didn’t know existed. 
  - 👉🏻 Or simplified: **whoever saves a change to a document first, wins**. 
- There are multiple reasons why CouchDB uses this revision system, which is also called Multi-Version Concurrency Control (MVCC). 

- One of the aspects of the HTTP protocol that CouchDB uses is that it is stateless
  - Making a request includes opening a network connection to CouchDB, exchanging bytes, and closing the connection. This is done every time you make a request. 
  - Holding a connection open for later use requires the server to do extra work. One common pattern is that for the lifetime of a connection, the client has a consistent and static view of the data on the server. 
  - Managing huge amounts of parallel connections is a significant amount of work. HTTP connections are usually short-lived, and making the same guarantees is a lot easier. As a result, CouchDB can handle many more concurrent connections.

- Another reason CouchDB uses MVCC is that this model is simpler conceptually and, as a consequence, easier to program. 
  - The revision system also has positive effects on replication and storage mechanisms

- Using new versions for document changes works a lot like version control, but there’s an important difference: CouchDB does not guarantee that older versions are kept around. Don’t use the ``_rev`` token in CouchDB as a revision control system for your documents.

- CouchDB’s schema-less documents can contain whatever you know. After all, you should relax and not worry about data.

- We’re getting back the 201 Created HTTP status code in the response headers, when we created a database. 
  - The Location header gives us a full URL to our newly created document.
  - An ETag in HTTP-speak identifies a specific version of a resource. it identifies a specific version (the first one) of our new document. Yes, conceptually, an ETag is the same as a CouchDB document revision number. ETags are useful for caching infrastructures.

- CouchDB documents can have attachments just like an email message can have attachments. 
  - An attachment is identified by a name and includes its MIME type (or `Content-Type`) and the number of bytes the attachment contains. 
  - Attachments can be any data. It is easiest to think about attachments as files attached to a document. These files can be text, images, Word documents, music, or movie files. 
- Attachments get their own URL where you can upload data. 
  - you need to provide the current revision number of the document you’re attaching the artwork to, just as if you would update the document. Because, after all, attaching some data is changing the document.
- `_attachments` is a list of keys and values where the values are JSON objects containing the attachment metadata. `stub=true` tells us that this entry is just the metadata. 

- In a simple `POST` request, you tell CouchDB the source and the target of a replication and CouchDB will figure out which documents and new document revisions are on source that are not yet on target, and will proceed to move the missing documents and revisions over.
- CouchDB maintains a session history of replications. 
  - The response for a replication request contains the history entry for this replication session. 
  - It is also worth noting that the request for replication will stay open until replication closes.
- It is important to note that replication replicates the database only as it was at the point in time when replication was started. 
  - So, any additions, modifications, or deletions subsequent to the start of replication will not be replicated.
- What you just did is called **local replication** in CouchDB terms. 
  - You created a local copy of a database. 
  - This is useful for backups or to keep snapshots of a specific state of your data around for later. 
- Using a local source and a remote target database is called **push replication**. 
  - We’re pushing changes to a remote server.
- You can also use a remote source and a local target to do a **pull replication**. 
  - This is great for getting the latest changes from a server 
- you can run **remote replication**, which is mostly useful for management operations

- While CouchDB’s core database, document, and attachment API are RESTful, not all of CouchDB’s API is. The replication API is one example. 
- Why are there RESTful and non-RESTful APIs mixed up here?
  - REST is an architectural style that lends itself to certain architectures (such as the CouchDB document API). But it is not a one-size-fits-all. 
  - Triggering an event like replication does not make a whole lot of sense in the REST world. It is more like a traditional remote procedure call.

## [2. Replication](https://docs.couchdb.org/en/stable/replication/index.html)

- Replication is an incremental one way process involving two databases (a source and a destination).
  - The aim of replication is that at the end of the process, all active documents in the source database are also in the destination database and all documents that were deleted in the source database are also deleted in the destination database (if they even existed).
- 👉🏻 The replication process only copies the last revision of a document, so all previous revisions that were only in the source database are not copied to the destination database.

- Replication involves a source and a destination database, which can be on the same or on different CouchDB instances.
- During replication, CouchDB will compare the source and the destination database to determine which documents differ between the source and the destination database. 
  - It does so by following the Changes Feeds on the source and comparing the documents to the destination. 
  - Changes are submitted to the destination in batches where they can introduce conflicts. 
  - Documents that already exist on the destination in the same revision are not transferred. 
  - As the deletion of documents is represented by a new revision, a document deleted on the source will also be deleted on the target.

- One replication task will only transfer changes in one direction. 
  - To achieve master-master replication, it is possible to set up two replication tasks in opposite direction. 
  - When a change is replicated from database A to B by the first task, the second task from B to A will discover that the new change on B already exists in A and will wait for further changes.

- 💡 There are three options for controlling which documents are replicated, and which are skipped:
- Defining documents as being local.
  - Local documents are never replicated
- Using Selector Objects.
  - Selector Objects can be included in a replication document
  - A selector object contains a query expression that is used to test whether a document should be replicated.
- Using Filter Functions.
  - The replication task evaluates the filter function for each document in the changes feed. 
  - The document is only replicated if the filter returns true.

- > Using a selector provides performance benefits when compared with using a Filter Functions. You should use Selector Objects where possible.

- When using replication filters that depend on the document’s content, deleted documents may pose a problem, since the document passed to the filter will not contain any of the document’s content. 
  - This can be resolved by adding a `_deleted:true` field to the document instead of using the `DELETE HTTP` method, paired with the use of a validate document update handler to ensure the fields required for replication filters are always present. 
  - Take note, though, that the deleted document will still contain all of its data (including attachments)!

- Replication can be especially useful for bringing data closer to clients. 
  - PouchDB implements the replication algorithm of CouchDB in JavaScript, making it possible to make data from a CouchDB database available in an offline browser application, and synchronize changes back to CouchDB.

- A persistent replication is controlled through a document in the `_replicator` database, where each document describes one replication process 
- A replication is triggered by sending a JSON object either to the `_replicate` endpoint or storing it as a document into the `_replicator` database
- The `_replicator` database works like any other in CouchDB, but documents added to it will trigger replications. 
  - Create (`PUT` or `POST`) a document to start replication. 
  - `DELETE` a replication document to cancel an ongoing replication.

## [2.3. Replication and conflict model](https://docs.couchdb.org/en/stable/replication/conflicts.html)

- Replication of databases takes place over HTTP, and can be either a “pull” or a “push”, but is unidirectional. 
  - So the easiest way to perform a full sync is to do a “push” followed by a “pull” (or vice versa).
- Because the changes are always replicated, the data is safe. Both machines have identical copies of both documents, so failure of a hard drive on either side won’t lose any of the changes.
- 👉🏻 By default, CouchDB picks one arbitrary revision as the “winner”, using a deterministic algorithm so that the same choice will be made on all peers. 
  - The same happens with views: the deterministically-chosen winner is the only revision fed into your map function.

- When working on a single node, CouchDB will avoid creating conflicting revisions by returning a 409 Conflict error. 
  - This is because, when you PUT a new version of a document, you must give the _rev of the previous version. 
  - If that _rev has already been superseded, the update is rejected with a 409 Conflict response.
  - So when working in this mode, your application still has to be able to handle these conflicts and have a suitable retry strategy, but these conflicts never end up inside the database itself.

- When you update a document in CouchDB, it keeps a list of the previous revisions. 
  - In the case where conflicting updates are introduced, this history branches into a tree, where the current conflicting revisions for this document form the tips (leaf nodes) of this tree
  - Each branch can then extend its history
- When you compact a database, the bodies of all the non-leaf documents are discarded. 
  - However, the list of historical _revs is retained, for the benefit of later conflict resolution in case you meet any old replicas of the database at some time in future. 
  - There is “revision pruning” to stop this getting arbitrarily large.

- The basic `GET /{db}/{docid}` operation will not show you any information about conflicts. You see only the deterministically-chosen winner, and get no indication as to whether other conflicting revisions exist or not
- If you do `GET /db/test?conflicts=true`, and the document is in a conflict state, then you will get the winner plus a _conflicts member containing an array of the revs of the other, conflicting revision(s).

- CouchDB’s Mango system allows easy querying of documents with conflicts, returning the full body of each document as well.

- Views only get the winning revision of a document. 
  - However they do also get a _conflicts member if there are any conflicting revisions. 
  - This means you can write a view whose job is specifically to locate documents with conflicts. 

- if you want to work with diffs, the recommended way is to store those diffs within the new revision itself. 
  - That is: when you replace v1 with v2a, include an extra field or attachment in v2a which says which fields were changed from v1 to v2a. This unfortunately does mean additional book-keeping for your application.

### 🆚️ couchdb vs git

- Git is a well-known distributed source control system. 
  - Like Unison, Git deals with files. 
  - However, Git considers the state of a whole set of files as a single object, the “tree”. 
  - 👉🏻 Whenever you save an update, you create a “commit” which points to both the updated tree and the previous commit(s), which in turn point to the previous tree(s). 
  - You therefore have a full history of all the states of the files. This history forms a branch, and a pointer is kept to the tip of the branch, from which you can work backwards to any previous state. The “pointer” is an SHA1 hash of the tip commit.
- If you are replicating with one or more peers, a separate branch is made for each of those peers.
  - In the regular workflow, replication is a “pull”, first “fetch” the state of the peer into the remote tracking branch for that peer; and then attempt to “merge” those changes into the local branch.
- 👉🏻 Note that while it is possible to build new merge algorithms into Git, the standard ones are focused on line-based changes to source code. They don’t work well for XML or JSON if it’s presented without any line breaks.
- The other interesting consideration is multiple peers. In this case you have multiple remote tracking branches. Note that each peer is explicitly tracked, and therefore has to be explicitly created. If a peer becomes stale or is no longer needed, it’s up to you to remove it from your configuration and delete the remote tracking branch. This is different from CouchDB, which doesn’t keep any peer state in the database.
- Another difference between CouchDB and Git is that it maintains all history back to time zero - Git compaction keeps diffs between all those versions in order to reduce size, but CouchDB discards them. 
  - If you are constantly updating a document, the size of a Git repo would grow forever. It is possible (with some effort) to use “history rewriting” to make Git forget commits earlier than a particular one.

- couchdb's data model, has these useful characteristics:
- Every record in CouchDB is completely independent of all others. That sucks if you want to do a JOIN or a transaction, but it’s awesome if you want to write a replicator. Just figure out how to replicate one record, and then repeat that for each record.
- Like Git, records have a linked-list revision history. A record’s revision ID is the checksum of its own data. Subsequent revision IDs are checksums of: the new data, plus the revision ID of the previous.
- In addition to application data ({"name": "Jason", "awesome": true}), every record stores the evolutionary time line of all previous revision IDs leading up to itself.
- Git isn’t really a linear list. It has forks, when one parent has multiple children. CouchDB has that too.
  - CouchDB “conflicts” do not correspond to Git “conflicts.” A Couch conflict is a divergent revision history, what Git calls a “fork.”
- Git also has merges, when one child has multiple parents. CouchDB sort of has that too.
  - In the data model, there is no merge. The client simply marks one time line as deleted and continues to work with the only extant time line.
  - In the application, it feels like a merge. Typically, the client merges the data from each time line in an application-specific way. Then it writes the new data to the time line.
  - ❓ These behaviors are different because, in Git, the time line itself is important; but in CouchDB, the data is important and the time line is incidental(次要的)—it’s just there to support replication. That is one reason why CouchDB’s built-in revisioning is inappropriate for storing revision data like a wiki page.

## [2.4. CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)

- The CouchDB Replication Protocol is a protocol for synchronising JSON documents between 2 peers over HTTP/1.1 by using the public CouchDB REST API and is based on the Apache CouchDB MVCC Data model.
- The reference implementation, written in Erlang, is provided by the `couch_replicator` module in Apache CouchDB.

- Verify Peers
- Get Peers Information
- Find Common Ancestry
- Locate Changed Documents
- Replicate Changes
- Continue Reading Changes

## [3. Design Documents](https://docs.couchdb.org/en/stable/ddocs/index.html)

- CouchDB supports special documents within databases known as “design documents”. 
  - These documents, mostly driven by JavaScript you write, are used to build indexes, validate document updates, format query results, and filter replications.
- Note: Previously, the functionality provided by CouchDB’s design documents, in combination with document attachments, was referred to as “CouchApps.” 
  - The general principle was that entire web applications could be hosted in CouchDB, without need for an additional application server.
- Use of CouchDB as a combined standalone database and application server is no longer recommended.
  - There are significant limitations to a pure CouchDB web server application stack, including but not limited to: fully-fledged fine-grained security, robust templating and scaffolding, complete developer tooling, and most importantly, a thriving ecosystem of developers, modules and frameworks to choose from.

- Design documents contain functions such as view and update functions. These functions are executed when requested.

- Views are the primary tool used for querying and reporting on CouchDB documents. 

- Views are useful for many purposes:
  - Filtering the documents in your database to find those relevant to a particular process.
  - Extracting data from your documents and presenting it in a specific order.
  - Building efficient indexes to find documents by any value or structure that resides in them.
  - Use these indexes to represent relationships among documents.
  - Finally, with views you can make all sorts of calculations on the data in your documents. 

- You provide CouchDB with view functions as strings stored inside the views field of a design document. 
  - You don’t run the JavaScript function yourself. Instead, when you query your view, CouchDB takes the source code and runs it for you on every document in the database your view was defined in.
- When you query your view, CouchDB takes the source code and runs it for you on every document in the database. 
  - If you have a lot of documents, that takes quite a bit of time and you might wonder if it is not horribly inefficient to do this. 
  - Yes, it would be, but CouchDB is designed to avoid any extra costs: it only runs through all documents once, when you first query your view. 
  - If a document is changed, the map function is only run once, to recompute the keys and values for that single document.
- The view result is stored in a B-tree, just like the structure that is responsible for holding your documents. 
  - View B-trees are stored in their own file, so that for high-performance CouchDB usage, you can keep views on their own disk. 
  - The B-tree provides very fast lookups of rows by key, as well as efficient streaming of rows in a key range.

- We explained that the B-tree that backs the key-sorted view result is built only once, when you first query a view, and all subsequent queries will just read the B-tree instead of executing the map function for all documents again
  - What happens, though, when you change a document, add a new one, or delete one? Easy: CouchDB is smart enough to find the rows in the view result that were created by a specific document. It marks them invalid so that they no longer show up in view results. 
  - If a document got updated, the new document is run through the map function and the resulting new lines are inserted into the B-tree at the correct spots. New documents are handled in the same way. 
  - The B-tree is a very efficient data structure for our needs, and the crash-only design of CouchDB databases is carried over to the view indexes as well.

- Map functions are side effect–free functions that take a document as argument and emit key/value pairs. 
  - CouchDB stores the emitted rows by constructing a sorted B-tree index, so row lookups by key, as well as streaming operations across a range of rows, can be accomplished in a small memory and processing footprint, while writes avoid seeks. 
  - Generating a view takes O(N), where N is the total number of rows in the view. 
  - However, querying a view is very quick, as the B-tree remains shallow even when it contains many, many keys.
- Reduce functions operate on the sorted rows emitted by map view functions. 
  - CouchDB’s reduce functionality takes advantage of one of the fundamental properties of B-tree indexes: for every leaf node (a sorted row), there is a chain of internal nodes reaching back to the root. 
  - Each leaf node in the B-tree carries a few rows (on the order of tens, depending on row size), and each internal node may link to a few leaf nodes or other internal nodes.

- A common mistake new CouchDB users make is attempting to construct complex aggregate values with a reduce function. Full reductions should result in a scalar value, like 5, and not, for instance, a JSON hash with a set of unique keys and the count of each. The problem with this approach is that you’ll end up with a very large final value. The number of unique keys can be nearly as large as the number of total keys, even for a large set. It is fine to combine a few scalar calculations into one reduce function; for instance, to find the total, average, and standard deviation of a set of numbers in a single function.

- View functions specify a key and a value to be returned for each row. 
  - CouchDB collates(检点并整理; 核对，校对) the view rows by this key. In the following example, the `LastName` property serves as the key, thus the result will be sorted by `LastName`.
  - CouchDB allows arbitrary JSON structures to be used as keys. You can use JSON arrays as keys for fine-grained control over sorting and grouping.

- how you’d go about modeling a simple blogging system with “post” and “comment” entities, where any blog post might have N comments. If you’d be using an SQL database, you’d obviously have two tables with foreign keys and you’d be using joins. But what would the “obvious” approach in CouchDB look like?
- Approach #1: Comments Inlined
- Approach #2: Comments Separate
- Optimization: Using the Power of View Collation
# docs-tips

## [3.13. Miscellaneous Parameters](https://docs.couchdb.org/en/stable/config/misc.html#uuids-configuration)

- CouchDB uses sequential UUID by default
  - the choice of UUID has a significant impact on the layout of the B-tree, prior to compaction.
  - For example, using a sequential UUID algorithm while uploading a large batch of documents will avoid the need to rewrite many intermediate B-tree nodes. A random UUID algorithm may require rewriting intermediate nodes on a regular basis, resulting in significantly decreased throughput and wasted disk space space due to the append-only B-tree design.
  - It is generally recommended to set your own UUIDs, or use the sequential algorithm unless you have a specific need and take into account the likely need for compaction to re-balance the B-tree and reclaim wasted space.
# docs-replication

## [Replication Algorithm · couchbase/couchbase-lite-ios](https://github.com/couchbase/couchbase-lite-ios/wiki/Replication-Algorithm)

- This is a historical document that applies to version 1 of Couchbase Lite. 
  - Version 2 uses a different protocol (based on WebSockets) that's a lot more efficient, but the high level algorithm is still the same.

- Couchbase Lite 1.x's replication protocol is compatible with Apache CouchDB. 
- 
- 

# ⚖️ [The CouchBase Database File Format_201805](https://github.com/couchbase/couchstore/wiki/Format)
- [The CouchBase Database File Format_201211](https://github.com/couchbaselabs/couchstore/wiki/Format)

- https://github.com/couchbase/couchstore/blob/master/file_format.md

- This is the current database file format used by Couchbase Server 2.0. 
  - It's similar, but not identical, to the format used by Apache CouchDB 1.2. 
  - It is implemented in a Couchbase 2.0 fork of CouchDB (in Erlang), and also by CouchStore in C.

- The most important thing to understand about a CouchDB file is that it is append-only. 
  - The only way the file is modified is to append new data at the end; bytes written are never overwritten. 
  - As a consequence, the critical file "header" data actually lives at the tail end of the file, since it has to be re-appended every time the file is changed.

- advantages
  - The data format is extremely robust, since the software can recover simply by scanning back from the end of the file to the last valid header.
  - Writers don't disturb readers at all, allowing concurrent access without read locks.
  - By default, earlier versions of a record remain in the file, making it easy to implement a version history and multi-version concurrency control (as exposed in the CouchDB API.)

- disadvantages
  - the file grows without bound as it's modified. To work around this, the file is periodically compacted by writing the live data to a new file, then replacing the old file with the new one. This can be done in the background without locking out either readers or writers.

- B-Tree Format
  - The B-trees used in CouchDB files are a bit different than in a typical implementation, because the file is append-only. 
    - A tree node is never updated in place; instead, a new copy of the updated node is written at the end of the file. 
    - Of course this means that the node's parent also has to be updated to point at the updated node, so the effect is that 👉🏻 every modification has to rewrite all the nodes from the affected leaf up to the root. 
    - In practice this isn't too expensive, especially if multiple writes are batched together into one update.
  - CouchDB's B-trees also have to forgo(弃绝；放弃) the sibling-node chaining that's typically used to speed up sequential access. 
    - The reason is that updating a node would invalidate the pointers to it in its siblings, forcing those nodes to be updated as well, resulting in a huge cascade of updates. 
    - Instead, the iteration algorithm remembers the path back to the root and periodically backtracks to find the next sibling node.
- Nodes On Disk
  - All B-tree nodes are compressed using the Snappy algorithm.

- Indexes
- A CouchDB database file contains three B-trees:
  - The by-ID index, which maps document IDs to values.
  - The by-sequence index, which maps sequence numbers (database change numbers, which increase monotonically with every change) to document IDs and values.
  - The local-documents index, which is conceptually the same as the by-ID index except that the documents in it do not appear in the by-sequence index, and by CouchDB convention the document IDs all begin with the ASCII sequence `_local/`.
- A CouchDB mapreduce view file contains two B-trees:
  - The by-ID index, which maps document IDs to values. This is also called the back-index.
  - The mapreduce-view index, which maps the the keys emitted by the view to its emitted values.

- The By-ID Index
  - This B-tree is an index of documents by their IDs. 
  - The keys are simply the document IDs, ordered lexicographically by raw bytes (as by the memcmp function.)
- The By-Sequence Index
  - The keys in this B-tree are 48-bit numbers representing the sequence number of a change to the database. 
  - This number is strictly increasing.
- The Local Documents Index
  - The reduce value in interior nodes of this B-tree is unused (empty).
- The Mapreduce-View Index
  - The keys in this B-tree consist of the emitted key and the document ID. 
  - For node pointer it is the emitted key and document ID of the rightmost child node.

- Numbers And Alignment
  - Numbers are in big-endian byte order (most significant byte first).
  - All values are tightly packed; there is no padding or multi-byte alignment.
  - Some values occupy partial bytes and have lengths that are not a multiple of 8 bits. These are stored in most-significant to least-significant bit order. 

- File Blocks
  - For purposes of locating the current file header (q.v.), the file is organized into 4096-byte blocks. 
  - The first byte of every block is reserved and identifies whether it's a data block (zero) or a header block (nonzero). 
  - Therefore only 4095 of the bytes are available for storing data.
  - Above the block level, these prefix bytes are invisible and simply skipped. So a data value that spans a block boundary will be written out with a zero byte inserted at the boundary, and this byte will be removed when reading the value.

- Data Chunks
  - The data in the file (above the block level) is grouped into variable-length chunks. 
  - All chunks are prefixed with their length as a 32-bit big endian integer, followed by the CRC32 checksum of the data. 

- File Header
  - A file header always appears on a 4096-byte block boundary, and the first byte of the block is nonzero to signal that it contains a header. 
  - A file will contain many headers as it grows, since a new updated one is appended whenever data is saved; 
  - So the algorithm to find the header when opening the file is to seek to the last block boundary, read one byte, and keep skipping back 4096 bytes until the byte read is nonzero.
# more
