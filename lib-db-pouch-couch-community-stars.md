---
title: lib-db-pouch-couch-community-stars
tags: [community, couchbase, couchdb]
created: 2024-01-04T06:35:05.415Z
modified: 2024-01-04T06:55:00.085Z
---

# lib-db-pouch-couch-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-sync
- ## 

- ## 

- ## is offline sync still working with a clustered setup? 
- https://couchdb.slack.com/archives/C49LEE7NW/p1704937572870599
  - Or is offline sync and http replication separate things?

- When you setup a cluster, data will be synced across clustered node automatically, based on the replicas and shards configured for the databases.
  - And, you may use replication to manually sync your data with other couchdb cluster (or single node setup). 
  - Replication protocol is being used by other databases like [PouchDB] to sync CouchDB database on your Browser's IndexedDB (internally used by PouchDB).  
  - Using replication you can also sync only limited (selected through query) documents, instead of full database.

- 🔁 Replication and sync are the same thing. CouchDB doesn’t care if it is server to server, server to client, or cluster node to cluster node. It is all internally compatible.
- 
- 
- 
- 
- 
- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 🛋️ [Damn Cool Algorithms: Log structured storage (2009) | Hacker News_201705](https://news.ycombinator.com/item?id=14447727)
- 🤔 Are there any open source implementations of a database that uses event sourcing?
- I built https://github.com/amark/gun after I was using MongoDB to event source data. The key piece for me was wanting to have Firebase-like realtime sync for my event sourcing.
- I've become a bit of a CouchDB zealot(狂热者) of late for this exact reason... Native support for incrementally updating map-reduce combined with change-feeds makes implementing event sourcing straightforward. 
  - If you wanted to reimplement event sourcing in couch, it can be implemented as a versioned merge in a map-reduce view that takes a sequential ordered events (e.g. ui-event:0000025) and maps those changes into a "versioned" JSON. This versioned JSON changes leaf values into versioned objects like "fieldValue": { "_val": 34.00, "_ver": 25 } which I call property fields. 
  - This is necessary because CouchDB is a B+Tree implementation and reduce operations are sequential but not contiguous(相邻的). 
  - The reduce phase merges all events sequentially by choosing property fields with the latest event – making it a CRDT type – and resulting in a single JSON document with the latest fields with "_ver" info for each. 
  - This scheme has a drawback that each event needs to have a unique serially ordered ID to work. Not sure how time stamps would work. I chose the ID based scheme to allow the UI be able to know when a user interaction conflicts (a vector clock between) and let it display the conflict to the user or decide how to merge the knew state.

- ## 🤔💡 [Best practice for a multiuser CouchDB-based app? - Stack Overflow](https://stackoverflow.com/questions/16141158/best-practice-for-a-multiuser-couchdb-based-app)
- The critical question is whether you want to expose CouchDB to the public or not.
  - If you want to build your CMS as a classical 3-tier architecture where CouchDB is exclusively accessed from a privileged scripting layer, e.g. PHP, then I would recommend you to roll your own authorization system. This will give you better control over the authorization logic. Particularly, you can realize document based read access control (not available in the CouchDB security system).
  - If instead you want to expose CouchDB to the public, things are different. You cannot actually write server side logic, so you will have to use CouchDB's built in authentication/authorization system. That limits you to read access controlled on a database level (not document level!). 
  - CouchDB admins should not be equivalent to application admins as a CouchDB admin is rather comparable to a server admin in a traditional setting.

- ## CouchDB is great but it is NOT made for the web. _202206
- https://twitter.com/rxdbjs/status/1542161610940243968
  - The replication protocol is way to slow to be used in anything more then a prototype. It is made for server-server sync, not server-client.
  - this is the first thing clients tell me when they try out the CouchDB replication in their production app. I use CouchDB myself on the backend and it is great especially when you work with microservices and you need to share data between them

- What I meant is that its REST api makes it a natural fit for web applications, not to mention that it allows for the creation of couchapps by virtue of it acting like a web server. The client-server sync perf issue is another matter.

- ## 🚀🔍 released our first (in a series) of #CouchDB-adjacent products: Structured Query Server __202306
- https://twitter.com/janl/status/1674328745140690944
  - It brings #SQL-querying (as in data retrieval, not manipulation) to almost all CouchDB users and extends CouchDB’s native querying ability significantly
  - Here is a short behind-the-scenes thread about the motivations for making this. 

- why doesn’t CouchDB do this?
- One of the promises of CouchDB is seamless scalability. If you build an app that runs on a single-node CouchDB instance it works the same on a 3-node, 16-node or 48-node cluster. That’s a pretty bold claim, how does it do that?
  - 👉🏻 The trade-off CouchDB makes here is that it does not have any features that support this scaling at the expense of just not having that many features.
  - 👉🏻 You may have heard that large MySQL installations “do not use JOINs”. That happens for the same reason, SQL JOINs inherently are hard to scale. CouchDB as such just does not have a JOIN feature on its own.
- We spent a good amount of time making it fast and proving it is fast so it is comparable with indexing speed, query speed and concurrency with CouchDB’s other querying facilities. 
- Finally: this is a commercial product. We love Open Source and we contribute to CouchDB et. al. any chance we get, but we’d like to do even more, and products like Structured Query Server allow us to make #CouchDB better for everyone.
- In our estimation, 95% of #CouchDB users run a deployment with 1–6 cluster nodes. Structured Query Server is for those 95% that can reach decent scale, but that have no need for CouchDB’s more extreme scaling options.

- Finally a bit of a blast from the past. Used to be a few options for SQL in Couch but they where just a translation to Mango. I had success with joins in views, then abused the lists functions to get a nested JSON response.

- ## [Structured Query Server: SQL Queries for Apache CouchDB | Hacker News_202307](https://news.ycombinator.com/item?id=36679556)
  - paid

- ## [What if OpenDocument used SQLite? (2014) | Hacker News_202309](https://news.ycombinator.com/item?id=37553574)
- > I like taking the approach of CouchDB where the only correct way to close the system is to crash it.
  - The term you're looking for is (aptly named) crash-only software.
  - [Crash-only software - Wikipedia](https://en.wikipedia.org/wiki/Crash-only_software)

- Why do you use a secondary, volatile database ? Performance-wise you won't gain a lot more (we're talking about a user editing a file, so not even 1 write per second).
- A proposal: write directly, and automatically in the database. No more Save button. There are multiple advantages:
  - the system is crash-resistant. I like taking the approach of CouchDB where the only correct way to close the system is to crash it. That way a crash is an expected situation that you actually account for, not a special case that you might forget
  - there is only one database. Less code, fewer bugs.
  - it is safe. A write to SQLite works or doesn't work, there is no in-between. 
  - it is how SQLite was intended to work. 

- ## 🎯 [Cloudant/IBM back off from FoundationDB based CouchDB rewrite | Hacker News_202203](https://news.ycombinator.com/item?id=30652281)
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

- con: Please correct me if i'm wrong, but i think the syncing feature makes it impossible to validate and/or process data from clients on the server side.

- ## 🛋️ [The database I wish I had | Lobsters_202008](https://lobste.rs/s/m9vkg4/database_i_wish_i_had)
- Well, I took the author at their word: “Being immutable means that only new information is added, no in-place update ever happens, and nothing is ever deleted.”
  - What you’re describing is what I’d call append-only or log-based. That’s how CouchDB’s and Couchbase Server’s databases work. It has the downside of lots of write amplification, since all the live data gets rewritten every time you compact.
  - On devices with limited storage, append-only has the worse problem that you can’t free up any storage unless you have enough free space to copy all the live data first. Which basically means it’s dangerous to fill up more than half of your storage, unless you carefully keep track of how much live data you have. 
- In fact, git itself implements this internally with “packfiles”, which is an internal binary format to represent diffs efficiently regarding storage. However every bit of data is still there, the “compaction” is transparent to the user.
  - Having snapshots is an possibility, but this would be better if left to the application to do, if the database could expose the snapshot and build more data on top of it, and let the application delete old data when convenient.

- The sync protocol, and conflict handling, are IMHO a lot more interesting problems than the implementation of the local DB. 
  - Take a look at Dat and Scuttlebutt … neither is perfect, but they have interesting designs. (And they make good use of append-only data structures at the sharing/protocol level.)
  - For a lower level approach to syncing, the CouchDB replication protocol, at a very high level, is a decent design. We still use the same architecture in Couchbase Lite, although the details of the protocol are completely different because sending zillions of HTTP requests is too expensive.

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
- Does PG's Json support multi-master sync? Native db level support for that feature simplifies a lot of my use cases. It'd be interesting to see a SQLite/WebSQL <-> Postgres multi-master syncing system. It'd be the equivalent of CouchDB <-> PouchDB. Maybe even using the same CouchDB protocol
  - 👉🏻 CouchDB and Couchbase both support only whole document updates. So you get document conflicts in those document stores as well, meaning your app needs to understand and handle 409's. But those conflicts are relatively easy to handle in most cases, at the cost of a new round trip. 💡 Mostly it's a matter of downloading the new document state and merging your change to it and re-post. 🧐 If you're using Redux/Vuex/Event Sourcing this becomes trivial to support. 💡 Another way to handle it is to split a single large document into smaller pieces and write a map/reduce view that returns a composite document. That should be possible in Postgres as well with a prepared statement.
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
