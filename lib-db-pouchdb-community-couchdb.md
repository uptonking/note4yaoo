---
title: lib-db-pouchdb-community-couchdb
tags: [community, couchdb, pouchdb]
created: 2023-10-29T02:23:22.305Z
modified: 2023-10-29T02:23:35.064Z
---

# lib-db-pouchdb-community-couchdb

# guide

# changelog-couchdb
- v4.0_202x
- v3.0_202002
  - User-defined partitioned databases for faster querying
  - Live Shard Splitting for incremental scale-out
  - Automatic view index warmer
- v2.0_201609
  - Clustering
  - New Query Language: mango
  - 2.0 is the unification of BigCouch(Cloudant's work) with the old single node CouchDB
  - New Admin Interface (written in React): fauxton
- v1.0_201007
# discuss-stars
- ## 

- ## 🤔 [Does multiple versions of couchDB keeps redundant data? - Stack Overflow](https://stackoverflow.com/questions/41510495/does-multiple-versions-of-couchdb-keeps-redundant-data)
- CouchDB holds multiple complete revisions of documents, it does not store incremental changes. 
  - The internals of CouchDB use an append-only data structure, so each new revision is added to the database file.
  - In addition, CouchDB uses MVCC (multi-version concurrency control) which prevents the need for locks while allowing concurrent writers. 
- 👉🏻 In short, you will have duplicates in your database each time you modify a document. 
  - Thus, modifying the same document many times can lead to an inflated(膨胀的) database file. 
  - In addition, very large documents with fewer modifications also have this same effect. For each document, only the latest version is considered "active" by the database, but old revisions may still be around. 
- This might sound inefficient and wasteful, but CouchDB has you covered with a feature called compaction. 
  - This process removes all revisions (except for the most recent) from the database file altogether. 
  - Prior to CouchDB 2.0, this was generally invoked manually by an admin, but now it is much more automated.
- One common misconception about CouchDB is that the multiple versions can be used like a version-control system (eg: git, svn), so you can always keep some sort of historical record of your database. 
  - However, this is completely false, as MVCC is purely for concurrency control. 
  - As stated before, compaction removes the old revisions, so you should only depend on the most recent revision existing in your database at any time.

- ## [Can I do transactions and locks in CouchDB? - Stack Overflow](https://stackoverflow.com/questions/299723/can-i-do-transactions-and-locks-in-couchdb)
- The answer is valid for CouchDB v1 only. CouchDB v2 is ignoring the "all_or_nothing" property.

- No. CouchDB uses an "optimistic concurrency" model. In the simplest terms, this just means that you send a document version along with your update, and CouchDB rejects the change if the current document version doesn't match what you've sent.

- Couch is probably not the best choice here. Using views is a great way to keep track of inventory
  - A view is a good way to handle things like balances / inventories in CouchDB.
  - With this model, you're never updating any data, only appending. This means there's no opportunity for update conflicts. All the transactional issues of updating data go away

- ## 🛢️ [Cloudant/IBM back off from FoundationDB based CouchDB rewrite | Hacker News_202203](https://news.ycombinator.com/item?id=30652281)
- [Important update on couchdb's foundationdb work-Apache Mail Archives](https://lists.apache.org/thread/9gby4nr209qc4dzf2hh6xqb0cn1439b7)
  - CouchDB embarked(开始；从事) on an attempt to build a next-generation version of CouchDB using the FoundationDB database engine as its new base.
  - The principal sponsors of this work, the Cloudant team at IBM, have informed us that, unfortunately, they will not be continuing to fund the development of this version and are refocusing their efforts on CouchDB 3.x.

- 📎 The FoundationDB rewrite would introduce a size limit on document attachments, there currently isn’t one. Arguably the attachments are a rarely used feature but I found a useful use case for them.
  - I combined the CRDT Yjs toolkit with CouchDB (PouchDB on the client) to automatically handle sync conflicts. Each couch document was an export of the current state of the Yjs Doc (for indexing and search), all changes done via Yjs. The Yjs doc was then attached to the Couch document as an attachment. When there was a sync conflict the Yjs documents would be merged and re-exported to create a new version. 
  - The issue being that the FoundationDB rewrite would limit the size and that makes this architecture more difficult. It’s partly why I ultimately put the project on hold.
  - (Slight aside, a CouchDB like DB with native support for a CRDT toolkit such as Yjs or Automerge would be awesome, when syncing mirrors you would be able to just exchange the document state vectors - the changes to it - rather than the whole document)
- As others have noted, the solution to storing attachments in FDB, where keys and values have an enforced maximum length, is to split the attachments over multiple key/values, which is exactly what the CouchDB-FDB code currently does.
  - The other limit in FDB is the five second transaction duration, which is a more fundamental constraint on how large attachments can be, as we are keen to complete a document update in a single transaction. 
  - The S3 approach of uploading multiple parts of a file and then joining them together in another request would also work for CouchDB-FDB. 
  - 🤷🏻 While it _could_ be done, there's no interest in the CouchDB project to support it.
- Exactly, almost all the time you would be better to save the attachment to an object store. However I think I found that small edge case where the attachment system was perfect. It was essential to save the binary Yjs doc with the couch document, it needed to be synced to clients with the main document. Saving it to an object store is not viable due to the overhead during syncing.
  - yup. the purpose of couchdb's original attachment support was for "couchapps". The notion that you'd serve your entire application from couchdb. Attachments were therefore for html, javascript, image, font assets, which are all relatively small. The attachment support in CouchDB <= 3.x is a bit more capable than that due to its implementation, but storing large binaries was not strictly a goal of the project.

- SyncedStore is a brilliant Yjs reactive store for SPAs, it’s not a database. It like an automatically distributed real-time reactive redux/vuex for collaborative apps.
  - The y-IndexedDB you linked to is actually part of the Yjs toolkit, it is a way of persisting a Yjs document in the browser for offline editing in a PWA. It doesn’t provide a way to sync a whole (or subset of a) database like Couch/PouchDB does. It’s a very important part of the Yjs toolkit but doesn’t do what I’m describing (it’s just a key value store).

- I don't see why there would be a fundamental reason why there would be an attachment size limit. I guess it would just need to be implemented by breaking the attachment into multiple keys? There may be some overhead but it seems that this is valuable because it allows large attachments to be split across servers as required.
  - 💡 FoundationDB has size limitations on the k/v pairs it can accept and splitting documents and writing those chunks in small transactional batches is the recommended workaround (along with some other 'switch over' transactional write which makes the complete document visible all at once.)
  - If I remember the fdb docs, there's also a time limit on transactions that further limits the feasible max size.

- 🤔 So what's the deal with the unpopularity of CouchDB?
  - Querying in a more ad-hoc way (vs. building indexes ahead of time and querying by key, etc) is a bit janky / not 1st class (I think mango addresses this but not entirely sure).
  - The runtime being erlang? It certainly seemed to be the cause of some issues when I tried to run it in WSL, or atleast my lack of knowledge with erlang made diagnosing it more trouble.
  - The JS query server engine is/was fairly old (I think it might have jumped to a more recent version of Spidermonkey at some point), and hooked up in a way that, while more modular, limits the performance (documents have to be serialized to/from the engine in another process, rather than just natively passed in)
  - The authorization model is... unique. You can limit down to a doc/field level who can submit changes 
  - the admin interface "fauxton" never really felt finished and debugging views is not welcoming for new users.
  - It's been a while, but seems like many people wanted something simpler like MongoDB for a NoSQL document database. CouchDBs map/reduce queries were hard to get people's heads around, many people didn't need attachments, etc.

- The FoundationDB Document Layer is compatibile with MongoDb 3.x API. https://github.com/FoundationDB/fdb-document-layer . and you get the transaction Al integrity. I stopped using MongoDB and switched to this.

- ## 🦀 [MiniCouchDB in Rust | Hacker News_202006](https://news.ycombinator.com/item?id=23446852)

- One of the things that really turned me off from firebase is the rules system where you have to build an ACL there. I really disliked trying to essentially build my authorization system into a backend which I couldn't run locally and was primarily edited in their web console.
  - For me, writing a proxy that sits in front of couchdb is very simple. I use JWT tokens that get passed between components in the system. I keep my authorization logic out of couch. I can write normal unit tests on my proxy. And my pouchdb client code mirrors the structure of my backend structure, which is a mental model I really prefer.
  - I guess I'm saying I think having a separate database for each user makes more sense to me, not less.
  - The only thing I'm struggling with is running code when a document is updated. I have a polling client that watches for the _global_changes updates, but it seems really hacky. I wish there was a better way to get access to all database changes that looked like firestore functions.
- _changes should be available in an event stream format for continuous consumption, and you can apply filter functions to the feed?
  - It is, but I am using the global changes feed (so I don't need to create a process for each database which doesn't scale for me). And you have to manually create that database to have it work. And I have to filter based on my own code, I just wish there was a way to subscribe to high level events. In general it works fine but I keep thinking there could be a better way.

- 👉🏻 In general, we are trying to move away from running your whole application in CouchDB. We would prefer that you **have an application layer in front of your CouchDB** instance. We recommend that you put up a proxy if you want to expose your replication to PouchDB. That way you can add security around that endpoint.
- If you look back on the history of couchdb on HN for example, the lack of document based ACLs continues to come up as a serious limitation of couchdb. Because it speaks http(s) natively, it is a perfect db that can be used directly in place of a lot of the rest of your stack if your use case is a MBaaS.

- This is an architecture I use a lot. The reverse proxy is there to implement the replication, having your application understand the replication protocol is a big ask. Instead, your app takes http requests, handles the ones it is supposed to, and forwards database requests directly to (c|p)ouchdb (after checking auth)

- You're probably write about writing your own authentication layer but it still shouldn't be part of CouchDB or PouchDB. A better solution is for some OSS project to build a standard proxy that applies the document level authorization that everyone is asking for. No reason for it to be built-in.

- ## 🧐💡 [Ask HN: Pros and Cons of Using CouchDB? | Hacker News_202205](https://news.ycombinator.com/item?id=31423986)

- Pros:
  - Sync is best in class for NoSQL databases
  - PouchDB is still one of the best JS libraries for NoSQL local storage
- Cons:
  - Confusing subtle incompatibilities between versions (CouchDB 1.x, 2.x, and 3.x break compatibility on various things, naturally, but also things like Couchbase is CouchDB compatible until it is not)
  - Attachments don't sync well for a high level feature
  - Managed/auto-scaling providers are slim-pickings and growing worse: Cloudant is IBM Cloud only now
  - Supabase: are you listening?

- Pros:
  - It does what it says, a document database with multi-primary/master nodes, which is good and rare.
  - It has been relatively reliable over the years for my previous company. CouchDB has been the most reliable component of the stack, together with RabbitMQ (both are using Erlang).
  - The community is not huge but friendly and helpful. 
  - It improves slowly but surely over the years. The background indexing has been a huge improvement for example.
- Cons:
  - It's not very fast, especially on VMs with network volumes.
  - Indexing takes a while, so migrations can take a very long time when you transfer the data.
  - The indexes uses a lot of ram, by design.
  - The community is small, so sometimes you have to send a pull-request or two.
  - Complex queries is not its strong side. The query optimiser will default to a large scan in most cases if you are not careful to use your indexes correctly.
  - When you have an issue or a question, not many people got it before you.

- PROs:
  - Your documents are kept with revisions instead of overwriting then.
  - REST API already built in
  - Authentication (also usable in your app) already built in
  - map/reduce
  - CouchApps
- CONs:
  - corporate supported development is dwindeling
  - only REST API, no wire protocol
  - CouchApps

- Being a document database it's not a good candidate for your typical CRUD Web app that has relations and foreign keys and joins and all that.
  - I wouldn't store my main app database in there, I would use postgres (with django most probably) for that.
  - I would use it to store meta data, that makes more sense in json format and that has fairly simple querying needs (no complex or flexible joins, sums, etc).

- Excellent read performance if you don’t want real time data. I had millions of documents and search/read was super fast, just that we were okay with 1 minute late data for our use case.
  - We had terrible experience with mongodb (very early version) even with 100k docs.
  - Cons: - Large disk space required for indexes - Indexing is somewhat slow
- 👉🏻 Go with “smaller” document ids, you can thank me later.
  - The thing is, document ids are used for indexing. So taking a simple eCommerce store as an example (assuming you have 100s of thousands of products) Product.id will be used extensively in indexes, you would want products to be displayed in a particular order, categorize them, sort/filter by price/listing date etc and so on. Which means lots of map-reduce views (which create these indexes). So you would want product ids to be as small as possible.
  - Seller.id, Review.id won't be used as extensively, you can then go for UUIDs.
  - But Ids can be used creatively for filtering or sorting prod-{yyyy-mm-dd}-iphone13, if that's your use case, you should forget about the id length. Id length matters mostly for disk usage in indexes.

- ## 🆚️ [CouchDB vs. MongoDB | Hacker News_201706](https://news.ycombinator.com/item?id=14564248)
- The article is strangely outdated on the CouchDB side
  - It fails to mention that CouchDB now has Mango, which is a MongoDB-compatible query language.
  - Since 2.0, CouchDB also has Dynamo-like clustering thanks to Cloudant's open sourcing of the BigCouch code.

- Mobile support: CouchDB stands out, in that it can run on an Android or iOS mobile device. In addition to being mobile, the database can also synchronize with a remote master database, allowing the data to be shared easily between mobile devices and servers.
  - Meteor actually provides exactly this for MongoDB; it has a "minimongo" package in the browser that supports Mongo's query language, running it synchronously against an in-memory copy of the collection. And with Meteor, you can specify "subscriptions" declaratively that enable bidirectional synchronization while their owner components are in scope.
- The CouchDB one is actually a fully persisted database, not just an in-memory cache. Both are useful, but it's not quite the same thing.

- CouchDB replication has got to be among the easiest and nicest in the industry. Setting up master/master is a breeze.
  - Snapshots: Any changes to a document occur as a revision and appends the information to the file. This means you can grab a “snapshot” of the file and copy it to another location even while the database is running without having issues with corruption.
  - This is the main feature I sell when pushing CouchDB. 
  - Use it to project events and you'll see what I mean.

- 🤔 We've found the Postgres json store works just fine for our purposes
- The reason I rejected PG's JSON store, was it's inability to update fields inside of a JSON doc, without replacing the whole document. In your case, does this constraint push you to use more types of smaller documents, or do you just read the whole doc, update it in the application, and then write it back to the DB?
  - JSONB data-type allows for specific field modifications in the JSON object. Operators look ugly in hand-crafted SQL but, works a treat.
- Does PG's Jason support multi-master sync? Native db level support for that feature simplifies a lot of my use cases. It'd be interesting to see a SQLite/WebSQL <-> Postgres multi-master syncing system. It'd be the equivalent of CouchDB <-> PouchDB. Maybe even using the same CouchDB protocol
  - CouchDB and Couchbase both support only whole document updates. So you get document conflicts in those document stores as well, meaning your app needs to understand and handle 409's. But those conflicts are relatively easy to handle in most cases, at the cost of a new round trip. Mostly it's a matter of downloading the new document state and merging your change to it and re-post. If you're using Redux/Vuex/Event Sourcing this becomes trivial to support. Another way to handle it is to split a single large document into smaller pieces and write a map/reduce view that returns a composite document. That should be possible in Postgres as well with a prepared statement.
- Mongo really isn't about storing JSON. At least that shouldn't be it's selling point. The selling point that is since it's basically just a glorified key value store it's very replicable and distributable. Postgres is very much not either of those things. The JSON is nice for a few things and I use it sometimes but Postgres is and will always be extremely difficult to cluster and replicate.
  - Postgres 10 added support logical replication. It makes horizontal scaling fairly painless.
  - Until you need to reseed the original master, want to do quick rolling restarts or want any automation in automatic failover. PG has a long way to go.
- Logical replication by default doesn't even handle DDL statements so something as simple as adding a new column requires extra process. Postgres is probably the weakest of all relational databases when it comes to scalability, both vertical and horizontal.

- I use couch, pouch, elasticsearch and sql dbs. I never really got the "schemaless" selling point of nosql though. I do see the point of storing documents rather than rows for some use cases, or dbs extra strong on searches, etc. But what is the problem with an "add column" or "change datatype" operation is sql..?
  - Partly because MySQL requires a full table lock and full table copy to implement those operations. Much of the nosql movement originated from implementing schema changes on production MySQL databases. In many if not most cases, NoSQL is really NoMySQL.
  - Many other engines, PostgreSQL for example, can add a new column without constraints as a nearly instant metadata change only. Data type changes that do not require validation (expanding a VARCHAR vs CHAR to INT) are also rapid.
- In my experience, "schemaless" just means that I'll have to manage the schema manually through some "updater" scripts. Any data without schema is just noise, so if you have any data, it means that you have schema for it somewhere.

- ## 🆚️ [What is the difference between CouchDB and Couchbase? - Stack Overflow](https://stackoverflow.com/questions/5578608/what-is-the-difference-between-couchdb-and-couchbase)
- [Couchbase vs CouchDB NoSQL Systems: Difference Between Them](https://www.couchbase.com/comparing-couchbase-vs-couchdb/)
- I think CouchBase seem to be perceived as CouchDB's 'enterprise' alternative. Which in a way seem to be true. Apart from lack of ability to attach files to records ( documents) and 'out-of-box' REST endpoints compared to CouchDB, CouchBase has sql like language i.e. N1QL (sometimes pronounced a Nickel, UPDATE renamed to SQL++ in Couchbase 7.0). This is one of the reason why I don't really like / recommend using the term 'NoSQL'. I personally like term 'Non-relational'.

# discuss-couchdb
- ## 

- ## 

- ## 

- ## 

- ## [Couchdb有在实际生产环境中使用的例子吗？ - 知乎](https://www.zhihu.com/question/20112928/answers/updated)

- [CouchDB in the wild_201812](https://cwiki.apache.org/confluence/display/COUCHDB/CouchDB+in+the+wild)
  - Software & Websites

- ## [Ask HN: To everybody who uses MapReduce: what problems do you solve? | Hacker News_201311](https://news.ycombinator.com/item?id=6706545)
- 👉🏻 It's worth noting that CouchDB is using map-reduce to define materialized views. Whereas normally MR parallelization is used to scale out, in this case it's used instead to allow incremental updates for the materialized views, which is to say incremental updates for arbitrarily defined indexes! 
  - By contrast SQL databases allow incremental updates only for indexes whose definition is well understood by the database engine. I found this to be pretty clever.
- I've been using CouchDB (and now BigCouch) for about four years and it's both clever and useful. We're storing engineering documents (as attachments) and using map/reduce (CouchDB views) to segment the documents by the metadata stored in the fields. The only downside is that adding a view with trillions of rows can take quite a while.

- ## [We have a problem with promises | Hacker News_201505](https://news.ycombinator.com/item?id=9564076)
- as I mention in the article, ES7 async/await should help fix that

- ## [Datomic Update: Client API, Unlimited Peers, Enterprise Edition, and More | Hacker News_201611](https://news.ycombinator.com/item?id=13055961)
- SQL views don't compose at the same level that Datalog expressions do, but that's because they aren't typically expressed as raw graph data (i.e. lists of strings where each list item is a node in the graph). If you could just name arbitrary chunks of SQL AST and mash them together, it would be just as composable (though perhaps more cumbersome due to boilerplate).
- you might give CouchDB a look. It's a document datastore that offers map/reduce views written in Javascript (use as much or as little composition/abstraction as you want). The distributed features are pretty cool (bidirectional sync, versioned documents) and writing apps with it is awesome

- ## [Kinto by Mozilla – An open-source Parse alternative | Hacker News_201601](https://news.ycombinator.com/item?id=10994736)
- CouchDB is so underrated in this space.
  - I get it: CouchDB was a very early (the first real?) document-based database, and it got some things wrong, or at least weird early on (e.g. map/reduce queries, a reduce step to the map/reduce query that is actually one-to-many (on purpose! there are concrete reasons in real life you want this!), etc.).
  - But they also got so much right:
  - The database is all HTTP, all the time.
  - Offline replication and database streaming, standardized at the protocol level
  - You can store your HTTP assets right alongside the DB for Firebase-like asset hosting.
  - You can store full-blown files, which is great for lots of practical app these days.
  - Trivial replication. The scaling of CouchDB itself is honestly a bit crappy, but Couchbase has great scaling

- ## [What Sucks About Erlang (2008) | Hacker News_201805](https://news.ycombinator.com/item?id=17114810)
- I had been contemplating(考虑; 沉思; 凝视) CouchDB for a new application at work, maybe you have a link I could read about it? I thought that the incrementally updating mapreduce style views looked really powerful, especially when combined with the changes subscriptions/long polling features.
- 🤔 for couchdb, Any complaints in particular?
  - 👉🏻 **Map/reduce views ("secondary indexes")** are currently built by serializing JSON down a pipe to an external process called couchjs that links against a seven year old version of Mozilla Spidermonkey(v1.8.5_201103). Multiple CVEs have been reported for v1.8.5
  - This external process then pipes the map results back, again as JSON. Forget zerocopy; we're serializing and deserializing twice per document. Almost all of this "external view server" (the only kind AFAICT) is actually written in Javascript on that seven year old engine. 
  - Nothing is streaming; your map function is sandbox-evaled in that process, the results of a single call are stuffed into a Javascript array via .push, then stringified and printed on standard output as a single line. The entire internal "view server" protocol is based on a pipe of single-line JSON commands and data payloads. Performance (and likely security, due to age of the engine) in this subsystem is extremely poor IME. I'm talking about the internals of couchjs. 
  - You can write map/reduce views in Erlang itself as an alternative, but that engine is disabled by default due to security concerns – it's "not sandboxed". Performance in this area also appeared to be proportional to the code size of the map function, which sounded a lot like it was being serialized down a pipe with no caching.
  - If you make a change to a single view in a design document, the database system will rebuild all indexes in that design document unconditionally, even if the other view code hasn't changed. The only way to prevent this is to store a single view per design document, and manage those documents yourself.
  - Once you've endured your multi-day index rebuild on a couple million documents, you'll also have to issue an extra "cleanup" command to delete the old (now essentially useless) indexes. It's a full rebuild, so you need 2x the space at a minimum to pull it off.
  - The data itself is stored in a single file per shard, opened in O_APPEND mode, effectively serializing all writes on the shard. You also will not see kswapd active, ever, because the OS VMM is not being used effectively – no shared memory for IPC, and no use of mmap AFAICT.
  - Server-side changes feed filters appear to be extremely slow when compared to just filtering the results in the client.
  - Authorization: limiting read access will be difficult at best. 
  - Transactional behavior: no, aside from a single bulk write feature (make sure to use "all or nothing" mode though).
  - Logging: signal to noise ratio is poor. Giant stack traces for minor events. You may even see strings emitted as UTF-32 arrays of integers in base 10. Hope you brought an ASCII table at least
  - But worst of all: every time it starts up, it tells me "it's time to relax". Nothing about this is relaxing.
- > Nothing is streaming
  - Except CouchDB entire REST API, where nearly every endpoint streams result row by row, which is great.
  - `_list` functions stream, and was specifically designed to be able to stream. However, streaming does not help much in this case, moreover too small chunks dramatically reduce already awful _list perf. Taking this in account I see no value for views to stream. Sending all emitted KVs for the doc to Erlang bits in one turn seems both much more predictable and safe.
- > Performance (and likely security, due to age of the engine) in this subsystem is extremely poor
  - for query server: indexing is slow for the reasons you pointed out. Requesting persisted index is ok. Taking in account CouchDB persists everything, it‘s not in-memory DB (which is again great), I‘d say it‘s even fast.
- > Performance in this (Erlang) area also appeared to be proportional to the code size of the map function
  - Performance in this area depends much more on how branchy is the json doc being processed. It‘s not about CouchDB itself, it‘s about json parser used. There might be a situation when you have better perf using JS views.
  - we discovered the effect during internal tests. Reason is simple: accessing values in deep branchy JSONs is generally faster in JS, because it‘s native format. JSON in Erlang is a monster like {[{<<"abc">>, 1}]} for {abc:1}, which, when has a lot of levels and nodes at each level, performs bad for selecting random node.
- > Nothing about this is relaxing.
  - Indeed. But then it just works, for years, with zero maintenance even for replications – the result I‘ve never even nearly achieved with any other DB I used.
- We sometimes measure number of docs with M postfix
  - Yeah, we did this in 2003 on commodity hardware, and even it built indexes faster than CouchDB builds map/reduce indexes. Fix the external view server protocol or be honest with people and kill it off – the status quo is unacceptable.
- 👉🏻 For balance: there is a newer query/index system called **Mango** in Apache CouchDB 2.0+, that IIRC is internal and doesn't rely on any external view server. It wasn't in 1.7.1, though, so if you're coming from there, it's very much a "switch query APIs to get tolerable performance" situation.

- 🔀 I have never heard of anyone saying erlang is bad because of couchdb. I've heard criticisms of couchdb itself, sure. But they've been more along the lines of "MVCC multi-master document stores are not a good solution for this problem" more than "CouchDB is a bad MVCC multi-master document store".
- It doesn't use real node-local/shard-local MVCC AFAICT. It's O_APPEND on flat files.
  - It _is_ append only. But doesn’t use flat files. The main storage files have 2 different immutable btrees to find documents (by id and by sequence num). And it does have mvcc for both storage and secondary indexes. Internally it has transactions but they aren’t exposed to the user, as multi document transactions don’t make sense for the replicated document model.
- Can I ask how the MVCC is implemented (e.g. WAL, MVTO, MVRC, etc.), or if there's documentation around that might give some additional insight?
  - Here’s a link that describes the Couchstore file format. It’s the storage engine for Couchbase and is essentially the same design as CouchDB. 
  - [The CouchBase Database File Format](https://github.com/couchbaselabs/couchstore/wiki/Format)
- Sorry, wasn't clear if you were talking about MVCC in a replication context or in a node-local context. It does the former, it definitely does not do the latter.
  - From the point of view of a single cluster or node (ignoring replication for a moment), it just doesn't have any strong notion of transactions. There's no write-ahead log, no rollback, and no situation where you'd be able to operate in a mode equivalent to something like SERIALIZABLE on a relational database.
- Are their good master-master systems out there with local transactions?
  - The claim from daimenkatz was that transactions and MVCC are supported internally, but not externally. It's unclear to me if any of this is accurate. 

- The main point is to sync server side data to a client side database, smoothly, so that the application can continue to function offline and then resync once the connection is re-established.
  - The main point is to sync server side data to a client side database, smoothly, so that the application can continue to function offline and then resync once the connection is re-established.**Couch has always been good at this use case** where systems on both ends may have changed in the disconnect time.
  - Realm looks like a much more modern solution to that problem.
- Not entirely sure what you misunderstand, PouchDB stores multiple revisions because thats how CouchDB's sync protocol works, the point of PouchDB was to match CouchDB semantics. PouchDB (as CouchDB) provides options to control how much you track (revs_limit, auto_compaction) and there are improvements we could do to handle tracking less information better. We use transactions under the hood actually writing data to indexeddb
  - I mean I both get it, and don't get it. CouchDB is all about master-master, and pouchdb just brings that to the browser. But at the same time I don't understand why you'd want a 'master' at the edge of the network, or the overhead of multiple revisions when a users browser isn't going to have tones of concurrent connections.
- I had to make that distinction fairly early on wether PouchDB would be an edge client or a full node and I decided full node, tradeoffs either way but pros of being a full node:
  - Additional (p2p) use cases, honestly I dont use CouchDB much these days, I use express-pouchdb-server so I can embed pouchdb into my server easier than any other database, there is also pouchdb-server and p2p projects like Thali
  - CouchDB existed, sync is super hard, writing an edge client would have meant designing it myself, writing a couchdb clone meant I needed to make a lot less decisions about how it worked while being very confident it would work, The test suite runs the same tests against pouchdb/couchdb to ensure compatibility (and replication via each configuration)

- ## 🎯 [CouchDB 3.0 | Hacker News_202002](https://news.ycombinator.com/item?id=22425834)
- CouchDB is awesome, full stop. While it's missing some popularity from MongoDB and having wide adoption of things like mongoose in lots of open source CMS-type projects, it wins for the (i believe) unique take on map/reduce and writing custom javascript view functions that run on every document, letting you really customize the way you can query slice and access parts of your data...

- It works very poorly as a relational DB.

- The problem I had with CouchDB is integrating it into a framework like Rails. CouchDB on its own does so much cool stuff. The "free" HTTP API and client replication via PouchDB are the two huge ones. But it just wasn't smooth enough to get the data out, use it where I wanted, and then save it back.

- Cloudant on IBM Cloud is CouchDB API/replication compatible and offers support for Apache CouchDB
- I'm really can't wait for the per-doc permissions 
- Yeah, I'm still disappointed that the MongoDB API outpaced(超过，胜过) the CouchDB Replication Protocol in general adoption. 

- That's where I fell into love with the CouchDB world. Building offline-first databases in PouchDB, and letting that sync to any HTTP address that speaks the replication protocol is sometimes a dream.
- My biggest current concern is client side search and size. 
- I've not tried quick search. For the most part in the applications I've worked on I've just relied on the main primary key index (the _id field) for most lookups.
  - I had PouchDB on top of IndexedDB handling hundreds of photos without breaking a sweat and those size limits all have nice opt-ins permission dialogs for IndexedDB if you exceed them. Where I found all of the pain in working with photos was server side. CouchDB supports binary attachments, but the Replication Protocol is really dumb at handling them. Binary attachments would balloon CouchDB's own B-Tree files badly and its homegrown database engine is not great with that
  - The approach I've been slowly moving towards is using _local documents (which don't replicate) with attached photos in PouchDB, metadata documents that do replicate with name, date, captions, ULID, resource paths/bucket IDs and a Blurhash so there's at least a placeholder to show when photos haven't replicated, and side-banding photo replication to some other Blob storage option (S3 or Azure Storage). 
  - It's somewhat disappointing to need two entirely different replication paths (and have to secure both) and multiple storage systems in play, but I haven't found a better approach.
- You’ve convinced me I should store photos separately; will probably do something similar to what it sounds like you did and have pouch just store a pointer either to S3 or some other backend for file storage. I don’t anticipate photos being that important a feature for me, so having them be disabled when offline might be acceptable, otherwise I’ll probably opt for storing them locally and only syncing metadata/pulling stuff from s3 when metadata changes indicate a change to the file like you’re doing.

- 😩 Reducing max document size from 4GB down to 8MB seems hyper-restrictive.
  - 8MB is just the default, you can switch it back to 4GB if you want, but you won't have an easy time switching to 4.0 due to the 8MB limit imposed by FoundationDB.
- In CouchDB 4.0 the backend of CouchDB will be switching to FoundationDB, which will have a 8MB limit, so they're preemptively making the change. You can remove the limit now if you'd like.
  - FoundationDB needs is a consistent (as per CAP) database, to make that work in a distributed fashion, there are limits on distributed transactions in size and time. CouchDB needs to adopt those in order to move to FoundationDB.
  - In CouchDB terms, you’d store data like this in attachments, not as raw JSON.
- 👉🏻 **If you're trying to store single GB documents in couch, you're doing it wrong... Unless those are binaries you can usually fragment data logically across many documents, then write custom views to aggregate however you need to.** Updates on huge docs would be painful!
- Couch/Pouch combination is really slow when document +attachment are too large. Based on my experience, Practical limit was more like 20-30Mb, and I'd suggest not even getting close to that. 8Mb simply recognizes reality.
  - That’s another great point, an exactly why we are doing this. It is a best practice already.
- At least since 2.0, the docs have always recommended to only use small documents in a CouchDB and to use an external storage for large files. The IBM Cloudant free tier only allows Docs up to 1 MB.

- 🆚️ why would you use CouchDB over something like MongoDB?
  - CouchDB is licensed under Apache License 2.0, while MongoDB uses SSPL
  - The main reason most people use CouchDB is because of the HTTP API and offline support with Couchbase Mobile and PouchDB. Doesn't CouchDB have most of those things already from 2.3? 
- MongoDB recently bought Realm which is an amazing mobile database with first class replication
  - last time I looked, realm did “last write wins” “conflict resolution”, which is just marketing speech for “randomly losing customer data”, which is something CouchDB decidedly works very hard to never ever do
- CouchDB has another pattern, each master is really a master and you can have live replication but also offline replication. You can connect two clusters every new moon and they will synchronize. For sure the clients may have to deal with potential conflicts but in practice it's very neat and that's what makes couchdb worth it if you need this feature.
  - MongoDB does replica sets and sharding. As far as I know it doesn't support multi-master architectures or data syncing. Even the Atlas-style global data distribution is sharding, right?

- 🤔 CouchDB/PouchDB looks very promising for offline first apps, but I can’t understand how to restrict bad clients. Client potentially could insert document of huge size or execute expensive query and degrade experience of other clients on the same server. Is it any way to prevent this?
- A couple ways:
  - One you implement validation functions on user databases to control what kind of data can be inserted into couch. 
  - you can also implement a proxy. This doesn't have to interfere with sync functionality, you just have to make sure you proxy all the endpoints in the replication protocol. Envoy is one such proxy that essentially applies document level permissions to a CouchDB database without interfering with sync.
  - If the goal is just to limit document size, or throttle clients trying to hammer the API, this doesn't even have to be a custom proxy, and reverse proxy with the needed control knobs (such as NGINX) will do. 
  - At scale there's a decent chance you want a proxy in front of your Couch instance anyway, since Couch is truly multi-master, meaning you probably want to balance your clients across all your nodes anyway.

- 🤔 Custom backend means no synchronisation and no advantages over postgres. Is there any secure open source code with pouchdb/couchdb integrations?
- Your backend can be a reverse proxy that authenticates requests then passes them off to CouchDB (or PouchDB, since that also runs on the server). I have an example up @ https://github.com/daleharvey/noted. The server is 200 lines and does signup / email authentication etc.
  - This server can't prevent authenticated user from uploading huge document of running expensive query.
- Any reverse proxy can limit the the size of a document upload. Even just plain NGINX can do that. Just set the client max body size.
  - As for queries, it kind of depends on your model. Mango queries are pretty limited (no joins, no arbitrary filters), so it's not necessarily as easy as you think to write one that hosed performance. A client could of course write one that doesn't use an index, which may or may not be a concern.
  - An easy option if it is though is just don't expose the _find endpoint, which effectively limits your users to the map/reduce queries you've written (unless you give them admin they don't have the ability to create their own).
- 👉🏻 A popular model is for the clients to run the queries locally, the server doesnt need to expose any query endpoints, only the ones necessary for replication.
- Is it any documents that describes secure couchdb architecture? 
  - I feel like your thinking about Couch as exposing your entire PostgreSQL DB to the internet, whereas with couch, a common model is to have a single database per user. In the Postgres model, providing the end user with any direct access is a nightmare, because every other users data is in there and I have to keep other users from viewing/modifying it. In Couch, you give them access to their database and only their database, that's how you isolate users.
- There are plenty of proxies that do that with some config like nginx. Even if you were using a relational database with a backend you’d still have to solve the same problem.

- If I use backend I can create all validation logic in application server. But in this case no automatic synchronisation. One of the major selling point of couchdb is replication protocol for client-server data syncing. When you design product with posgress you don't allow to execute raw sql queries from clients without any application server. But looks like it is recommended way to update data in couchdb world if you want to have synchronisation. I can't understand how can this architecture be secure?
  - Couchdb has options for controlling which documents are replicated. This may help depending on your use case.
  - nginx couldn't solve the "execute expensive query" though right, only limit max size. I guess you could do a request timeout + blacklist, but that would also be hard to do right, since at heavy load some proper clients might get blacklisted.

- 🤔 I once read that the right way to use CouchDB is for every user to have its own database. However, how does this work with BI? Or with public data that should be known by all users? 
  - 👉🏻 You can replicate all per-user DBs into a central database today.
  - We are working on `per-document-access-control` at the moment, to support this use-case out of the box
- For public data, you can try to partition it in such a way that writes can be merged without any potential conflicts. E.g. a user's posts are in a separate partition. I have never done this with CouchDB, but the technique is described in Martin Kleppman's __Designing Data Intensive Applications__.

- there are no changes to the replication protocol in Couch 3.0, so PouchDB already works.

- The newest version of CouchBase mobile no longer supports CouchDB as a replication target. It can still be accomplish with the CouchBase Sync Gateway, but get complicated quickly.

- ## 🎯 [CouchDB 2.0 | Hacker News_201609](https://news.ycombinator.com/item?id=12543342)
- TL; DR
  - Clustering
  - New Query Language: mango
  - New Admin Interface (written in React): fauxton
  - Also, 2.0 is the unification of BigCouch (Cloudant's work) with the old single node CouchDB.
- CouchDB 2.0 is a direct descendant of CouchDB 1.x. The API is 99% compatible, same community working on it, you can replicate between them and so on.

- If you want filtered replication, we designed Couchbase Sync Gateway because we thought db-per-user was to heavy. What's fun is to think about the options for mix-and-match across the stack.

- I'm sad that the Couchapp thing never took off or is getting de-emphasized. That was one of the really brain-bendy ideas about Couch that I loved, that these DB-side applications could also replicate to other people.

- Who is the audience for 2.0? Who does IBM hope to reach with Cloudant?
  - There are a lot of use cases, particularly around multi-region/DC master-master replication, where CouchDB/Cloudant is a great fit. IBM also offers MongoDB, RethinkDB, Postgres as managed services and the MVCC/conflict model in Couch is still a standout feature. 
  - The other use case I see a lot of is offline-capable apps backed by Couch replication-compatible datastores (PouchDB, Cloudant Sync, Couchbase Lite).

- I think there's a lot for you to like in 2.0.
- > The replication protocol, which supports multi-master, has changed little
  - 2.0 adds an additional endpoint, _bulk_get which can significantly reduce the number of requests when CouchDB is paired with an on-device database such as PouchDB, Cloudant Sync
  - Also, CouchDB 2.0 introduces internal cluster replication using distributed Erlang. 
- > In other words: everybody seem to be looking at CouchDB as just a very poor and limited MongoDB.
  - it provides a query syntax that should be familiar to MongoDB users and more query flexibility than views allow. I think Query still has a fair way to go - this is the first release
- > Filtered replication was implemented, but it is slow to the point that no one recommends that you use them.
  - The new _selector filter [[2] in CouchDB 2.0 offers a significant performance improvement for filtered _changes. It should be a small change for replicators such as PouchDB can take advantage of this.
- > About Couchapps, the special database features that powered them in the first place were left aside
  - it seems there has been much debate about this in the CouchDB community and the conclusion was that there are better solutions to most Couchapp-shaped problems than running application logic in the database

- CouchDB is eventually consistent and does not guarantee consistency. Would a Jepsen test make sense?
  - Yes. Eventual consistent doesn't mean inconsistent, but eventually it will be. That means under a network partition (P of th CAP Theorem) things should converge after the network converges. 
  - This is precisely the type of semantic that Aphyr wrote Jepsen for. See his testing of Cassandra (eventually consistent) or the CockroachDB team (eventually consistent) or Riak (eventually consistent) running Jespsen to prove things work as expected.

- MongoDB makes a lot of sense to folks already familiar with relational databases. Collections are like tables, documents are like rows, and it's easy to use document IDs to establish relations and perform queries like you would in a relational database. There are a lot of problems with using it like a RDBMS, but still a developer with zero knowledge of MongoDB can become productive with it very quickly.
  - When learning CouchDB, the first WTF moment is when you realize there are no tables and that all the documents regardless of the type of data they contain go in the same place. Eventually you learn that you can add a type field to the documents to distinguish between them, which does feel hackish. The next WTF moment is when you want to query the data and realize you have to use map-reduce to do what would seem trivial in any other database.

- ## 🎯 [CouchDB 1.0 | Hacker News_201007](https://news.ycombinator.com/item?id=1514797)
- couch hits a number of sweet spots. Documents can have attachments so you can build a complete application out of html, css, and javascript and have the entire app reside in a couch database. Coupled with P2P replication this make for some interesting possibilities.
  - couch also inherits a lot from it's choice of implementation language, Erlang, and it's append-only storage design. A high level functional language such as Erlang makes for a small manageable code base.

- ## [Why Replication is Awesome | Hacker News_201311](https://news.ycombinator.com/item?id=6690607)
- my own opinion that Couchdb is highly overrated. Not because it is not a good implementation of a document style database, but because the document store itself is not a good match for most use cases.
  - If the only requirement is a replicated JSON document store, it may work OK for you. But so would Riak, Postgres and some others.
  - If you need to update the data in those documents or ever need to query the data in ways you did not initially envision, you will quickly find yourself missing features which even traditional SQL databases are very good at. Development is slower.
  - Writing map/reduce for queries seems particularly cumbersome, particularly if you prefer not to use Javascript. And you have to plug them into a textarea in a webpage interface, or manually put them into Couchdb over http using curl or some library that abstracts this away. Either way it is a degree of separation that makes the data feel more out of reach than through a console interface like psql or mysql.
  - Consider the scenario where you want to update the value in an attribute on several thousand, or even just several documents that match some criteria. In SQL, you would simply jump in the console and `update table set col=val where criteria` . There is no such feature in Couchdb. You will need to write code to filter and fetch each matching document, manipulate it as needed, then write the entire thing back. 
- I agree with some but not all of what you write.
  - 0) CouchDB will never lose your data. Period. Not many other stores are 'append only, copy on write'. 
  - 1) I think document DB's are as good or better than a key value store like riak. It's great to have the choice, at a later point in time, to reach inside your documents, build indexes, etc.
  - 2) The biggest wart(缺点；错误) with couchdb from a scaling point is the single server, master-slave, and master-master. There is no dynamo style clustering, ala cassandra, risk, etc. 
  - 3) Finally, the biggest wart from a usability standpoint is the need to build materialized views. Ad hoc queries are painful. In Apache CouchDB most folks use Elastic Search in conjunction. 

- When criticising CouchDB, don't forget about its killer features:
  - Replication: slave, master, multi-master, pull, push, single, continuous over http(s), you name it.
  - Update handlers: You don't have to fetch, modify and save in every case.
  - MVCC semantics: Lock-free write access. Never, ever database dead-locks.

- ## [The Future of CouchDB | Hacker News_201201](https://news.ycombinator.com/item?id=3427491)
- This feels like bad news for CouchDB users, since they will need to re-write code and re-learn a new system if they choose to migrate to Couchbase Server.

- ## [Goodbye, CouchDB | Hacker News_201205](https://news.ycombinator.com/item?id=3954596)
- So, the TL; DR version of this is: we stopped using CouchDB because it sucked, but we took all the things that made it great, and shoe-horned them in to MySQL, while negating using anything that an RDBMS is designed for, like joins...

- I've been using CouchDB for the past six months for the internal product-CMS for my business. Its got a great feature set for what I am using it for. MVCC architecture, master-master replication and stored views make it a natural fit as a backend for internal tools. The benefits actually grow as you get more desginers/artists etc working together; each on their own DB.
  - It seems like all the problems he has are with scaling. I can't comment on that, but I would whole-heartedly recommend it for internal tooling.

- CouchDB has some features that other databases don't have: a continuous changes feed, REST interface, master-to-master replication, a web interface to the data and management (Futon).

- The unique feature of CouchDB is the way it does views, but that doesn't mean you can't' do views (in fact, in my opinion, better) in other databases.

- One of the nice features of CouchDB is that the views are incrementally updated, ideal if you have a large dataset that changes frequently with little changes and you want frequently get the most up to date transformed data.
  - In Riak you would aim to update those views at write time, to minimize the number of reads required.

- ## [Cassandra vs MongoDB vs CouchDB vs Redis vs Riak comparison | Hacker News_201012](https://news.ycombinator.com/item?id=2052852)

- My understanding is that in CouchDB you can't guarantee that older versions of documents will still exists (they might be there, but they could have been removed by compaction or not replicated). However, there is a fairly nice way of storing older versions of documents - hold older versions as file attachments on the document.
  - This is probably the biggest misunderstanding of couchdb, imo. The versioning system in couchdb is only there to make the seamless replication possible. There's no guarantee that previous versions will exist at a future time, like in git.

- Trying to use CouchDB's versioning system seems like depending on a very leaky abstraction. That you can see it's versioning is a side-effect of how it behaves; not a feature it is providing. If you need versioned records, you are likely better off identifying your versioning requirements and building to those than trying to piggyback off of something else poorly suited.

- ## [What the HTTP is CouchApp | Hacker News_201008](https://news.ycombinator.com/item?id=1569664)
- CouchDB is really fun. There is a native Javascript driver and the protocol is RESTful (HTTP GET, PUT, DELETE).
  - Compare the the closest NoSQL alternative, MongoDB. I say close because they are both document stores (fancy key/value) with indexing and map/reduce.
- MongoDB is very lean and blazing fast. But there isn't anything close to an HTTP layer in Mongo. It speaks in a binary JSON protocol. The format, commands, and driver, while well done, are a whole new set of rules to learn. Plus a Ruby middleware to talk HTTP.

- Read access is on a per-database basis. So if you have a work group only Joe, Anne, and Robert should access, you can give them a database, with their own copy of the app running in it. We don't do per-document read-control because it becomes to complex to manage in real world situations.

- 👉🏻 However, you can put the database behind a proxy and use lists and shows (that get passed the user info) to restrict the read access.

- If you want to allow the users to take the db offline, you will still be happiest giving each user or group their own database. Databases are just a file on the server, and CouchDB has been deployed with millions of databases on a single server. So the one database per user model is totally viable.

- 🤔 If an app can be replicated to a user's machine, can the user then also manipulate the couchapp's view and design documents using futon or otherwise, even though validation functions are in place? ie, would a user be able to alter the application themselves, and not just their data?
  - Yes, depending on how the access and security is setup. If the user has access to the database, they can just open the _design document and edit the html template, JavaScript code, the view, list and show functions.
  - couchapp takes advantage of the fact that couchdb is accessed via a RESTful interface. It renders html page templates saved as document attachments, and fills those in with data from some view (read: query), and then returns HTML.
  - It basically cuts out the traditional middle layer by performing that work inside the database.
- Actually, whatever is on the user's machine (or in a Couch in the cloud controlled by the user) is 100% under the control of the user. They are free to alter the application, validations, etc, as they see fit.
  - However, when the user attempts to replicate changes to another server (maybe the original source server, maybe another server not under their control) it is the validation functions on the target server that control which writes are allowed to proceed.

- ## [What the HTTP is CouchApp? | Hacker News_201011](https://news.ycombinator.com/item?id=1944055)
- Riak and other HTTP based databases do not have the peer-based replication which sets CouchDB apart. Being able to share an application and its data with a simple HTTP call, and synchronize it across all your phones and laptops -- that is not something other databases can do.
- I wish the couch guys would just focus on integrating the _changes feed into different languages. What I find appealing is their attempt to solve the distributed sync problem. That's useful, but adopting couchdb on all the clients doesn't make much sense. Microsoft's sync framework is moving to allowing full cross language / platform sync. It already allows two-way syncing odata feeds to the iPhone, android, windows phone, and pure javascipt. I don't see why I need build all my clients on couchdb directly to get this functionality. It seems like a nonstarter for 95 percent of use cases.

- 🤔 Where normally does a couchapp put its application/business logic? At client side javascript?
  - There is a server-side JavaScript validation function which can reject updates for being malformed or if the user isn't allowed to proceed

- It looks interesting but I see any moderately complex web app, i.e. more than CRUD, hitting a wall of complexity when using CouchApp as a base. You eliminate so called "fragile custom code" up until the point where the framework doesn't support something and you need the custom code anyway, except now there is the overhead of getting custom code working together with everything else. 

- Not sure how I feel about exposing my database directly to a client. This means all security regarding reading and writing any data must be handled in CouchDB. Not knowing about CouchDB, the existence of CouchApp leads me to believe there must be some way to do this, but I can't see how this would be possible with MySQL or Postgres.
  - CouchDB's security is per-database (since you assume you will be replicating a complete database to the end-user, the concept of cell-level security doesn't make sense).
- Cell-level security would never make sense, which is why you need an application layer to perform queries and return and modify only data that a client has permission for. Am I right that the database would be shared by all clients and that the application layer is essentially moved into the client? If so, this seems like a pretty silly architecture.
- yes the application runs entirely on the client, but validation functions are run on replication, so I can change my copy of your blog post, but you won't let me change it via replication. That would be silly.
