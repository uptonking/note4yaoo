---
title: lib-db-pouch-couch-community
tags: [community, couchdb, pouchdb]
created: 2023-10-29T02:23:22.305Z
modified: 2024-01-04T06:55:12.542Z
---

# lib-db-pouch-couch-community

# guide


# discuss-couch-internals
- ## 

- ## 

- ## [Why does CouchDB use an append-only B+ tree and not a HAMT - Stack Overflow](https://stackoverflow.com/questions/20816698/why-does-couchdb-use-an-append-only-b-tree-and-not-a-hamt)
- B-trees are used because they are a well-understood algorithm that achieves "ideal" sorted-order read-cost. Because keys are sorted, moving to the next or previous key is very cheap.
- HAMTs or other hash storage, stores keys in random order. Keys are retrieved by their exact value, and there is no efficient way to find to the next or previous key.
- Log Structured Merge (LSM) is a different approach to sorted order storage which achieves more optimal write-efficiency, by trading off some read efficiency.
  - However, LSM is more of a "family" of algorithms than a specific algorithm like a B-tree. Their usage is growing in popularity, but it is hindered by the lack of a de-facto optimal LSM design. 
  - LevelDB/RocksDB is one of the more practical LSM implementations, but it is far from optimal.

- ## 🧮🌲📕 [How the append-only btree works (2010) | Hacker News_202312](https://news.ycombinator.com/item?id=38805383)
- The immutable b+tree is a great idea, except it generates a tremendous amount of garbage pages. Every update of a record generates several new pages along the path of the tree.
  - There are two additional techniques to make immutable b+tree practical. 
  - One is to reclaim(恢复或收回) stale unreachable pages after the transactions using them have closed. 
  - Two is to use a pair of oscillating(波动，动摇，犹豫) fixed location meta pages.
  - A page is active if it’s in the latest snapshot or it is in use by an open transition; otherwise, it’s unreadable and can be reclaimed. When a transaction closes, it hands its list of in-use pages to the reclaimer. The reclaimer tracks these pages. When no other open transactions hold on to a page, it can be reclaimed.
  - The most frequently updated page in the tree is the meta page. Every write transaction updates it. This creates a lot of garbage pages. The second technique addresses this problem.

- The Hitchhiker Tree addresses the write amplification at the cost of making lookups and scans slightly more expensive, by keeping a small array of "pending writes" in every non-leaf node. The entire thing is still immutable, but instead of writing a new leaf node + path from root to that leaf, in the majority of cases we only write a new root. When there is no space left in the array, all the pending values get pushed one level down at the same time, so the write amplification is amortized.
  - This idea dates to at least 1996
- I believe the Bw-tree does the same thing, caching new updates in the intermediate branch nodes and only pushing the updates in batch down to the lower layers when running out of room at the branch node. These are the newer wave of algorithms to address the write amplification.

- Yes, CoW trees have tremendous write magnification. This is well-known. The fix is to amortize(分期偿还) this cost by writing transactions as a log and then doing a b-tree update operation for numerous accumulated transactions. Think of ZFS and it's ZIL (ZFS Intent Log). That's exactly what the ZIL is: a CoW tree write magnification amortization mechanism.
- > Does ZFS support transactional reading and writing?
  - I don't know that I understand your question. ZFS supports POSIX transactional semantics, which is not ACID, though ZFS's design could support ACID.
- > Is that just the traditional transaction log + btree update approach most databases used?
  - Basically, yes. The idea is to write a sequential log of a) data blocks, b) metadata operations (e.g., renames) to support fast crash recovery. During normal operation ZFS keeps in-memory data structures up to date but delays writing new tree transactions so as to amortize write magnification. 
- Thanks for the explanation. Basically ZFS maintains a ZIL based in-memory tree for the recent updates and a on-disk btree for the complete updates, minus the recent updates in ZIL. That's consistent with most database transaction log implementation. Some newer approach adds a Bloom filter to do fast decision between looking in the in-memory tree or in the on-disk btree.

- This description reminds me of a document I read about how ZFS is implemented. In particular, how snapshots work in ZFS, and what happens when you delete a snapshot.
  - It's a very similar idea. Traditional Unix-ish filesystems, with inodes and indirect nodes are a lot like b-trees, but ones where the indices are block numbers and where you can only append indices, trim, or replace indices. The ZIL (ZFS intent log) is a mechanism for amortizing the write magnification of copy on write trees. 

- I am immediately nerd-sniped by this. Is there any code out there you know of I can see? The dual meta-data pages sounds precisely like double-buffering (from graphics; my domain of expertise). I am also drawn to append-only-like and persistent data-structures.
  - LMDB works like this. The MDB_env struct keeps pointers to both meta pages
  - LMDB is the poster child of COW btree implementation. That paper is a good find. Thanks.

- IIRC, this is how 🛋️ CouchDB was implemented. The benefit is that it was resilient to crash without needing a write-ahead log. The downside was that it required running background compaction of the B+tree regularly.
  - LMDB works the same way. But it also stores a second data structure on disk listing all free blocks. Writes preferentially(优先的；给予优先的) take free blocks when they’re available. The result is it doesn’t need any special compaction step. It sort of automatically compacts constantly.

- 🌲🌲 Naively thinking here, how about a 2 immutable b+tree setup:
  - The "hot" tree is the WAL: All the data is there and copies are generated.
  - The "cold" tree is behind: In the background move from WAL and at the same time compact it.
- That's how the traditional transaction log + btree approach work. The append-only btree removes the need for a separate transaction log.
  - I think you could view the append-only B-tree as a deamortized version of the traditional update-in-place B-tree + WAL. 
  - It's true that it eliminates the problem of maintaining a separate WAL, but only by trading it for an arguably harder problem: compacting the B-tree. It's easy and cheap to truncate the WAL; it's difficult and expensive to compact the B-tree. 
  - I guess LMDB solves this problem by only updating at page-level granularity so it can reuse entire pages without compaction, although I haven't studied its design in much detail.

- 📕 LMDB was derived from this project, as mentioned in its copyright notice section.
  - Importantly, the LMDB API allows append mode, and it is very fast.

- The difference is that persistent data structures allow you to traverse the history of the data structure to find past versions. By contrast I only allowed you to see the current version, returning a new version of the root any time you made a modification. As a result, the memory associated with the old version could be freed once nothing would want to access it again. And any version that you had could still be manipulated.

- Append-only structures are not efficient enough for general use. You're paying a steep price for creating a snapshot of the data for every single operation.
  - I saw this when I was playing with Scala's immutable and mutable data structures - written by the same team - ages ago. The immutable structures were much slower for common operations.
  - The fastest databases tend to use undo logs to re-construct snapshots when they are needed
- You can build real useful systems on them. For example, Gmail used to be implemented on top of GFS as two append-only files per user: the zlog and the index. 
  - Gmail's now built on top of Spanner so uses a log-structured merge tree. Still append-only files but a bit different. Files aren't per user but per some arbitrary key range boundary; no more btree; multiple layers with the top ones getting compacted more frequently; etc.
- It's worth noting that 🌰 Google's internal scale-out filesystem is append-only (for various distributed systems and operational reasons), so you end up with append-only data structures proliferating in that ecosystem. That does not necessarily mean that the append-only data structures were chosen for any technical merit other than ability to be implemented on the append-only filesystem.
- Good point. It's also worth noting that raw flash also is generally treated as roughly append-only for wear leveling. "General-purpose" may be in the eye of the beholder, but I'd say these append-only data structures are useful in at least two significant environments.
- What you described is called event sourcing

- The biggest cost to copy-on-write data structures is write magnification. Adding a log to amortize that cost helps a lot. That's what the ZFS intent log does. Any CoW b-tree scheme can benefit from that approach.
- The benefits of CoW data structures are tremendous:
  - easy to reason about
  - easy to multi-thread for reading
  - O(1) snashopts (and clones)
- The downsides of CoW data structures are mainly:
  - the need to amortize write magnification
  - difficulty in multi-threading writes

- 🤼🏻 A mutable approach requires a write ahead log meaning you have to copy the data twice on every write which seems worse.
  - It is: two writes for write ahead log vs. log-n (tree-height) writes for CoW

- One thing that's not explicitly mentioned: append-only trees necessarily lack parent pointers.
  - This means that your "iterator" can't be a lightweight type, it has to contain an array of parent nodes to visit (again) later.
# discuss-couchdb-mvcc
- ## 

- ## 

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
# discuss-couchdb-git-revision
- ## 

- ## 

- ## [Is there a git implementation that runs on top of couchdb? - Stack Overflow](https://stackoverflow.com/questions/6115519/is-there-a-git-implementation-that-runs-on-top-of-couchdb)
- If you mean an implementation where the data of a Git repository is stored in a database rather than in filesystem, then there is some work done by Shawn Pearce in JGit to achieve this

- ## 🆚️🌵🛋️ [Is Git more than a version control system? Reimplementing CouchDB with Git+Bash... | Hacker News_200904](https://news.ycombinator.com/item?id=573699)
- I've been waiting for this. Ever since:
1. I learned from Linus that git is a decentralized "content" database that gives identity to different versions of the same content and allows them to be compared and merged. (as opposed to a traditional VCS which is more of a "delta" database)
2. I learned from Damien that CouchDB is a decentralized "document" database that gives identity to different versions of the same document and allows them to be compared and merged.
- I've been wondering just what the difference really is.
- 👉🏻 Git retains its change history, and if I remember correctly, uses the sha hash to verify that no one changed the history. Couchdb retains the change history until someone compresses the db (garbage collect). Its revision history is only used as a means of merging out of sync documents.
  - In addition, Git makes individual merges in a document, and when there's a conflict, it resorts to human intervention. Couchdb does not make merges inside a document, and will not do conflict resolution. Instead, using a brief set of rules, it picks one version of the document over another.
- Is there a way to make Git choose one over the other rather than merging? --mine or --yours or something?
  - There's a git merge strategy called "ours" which - as you might guess - does a quasimerge(类似-merge) which always results in whatever you have in your HEAD.

- Not really a new idea to use a VCS as a document database, other folks have back-ended Wikis and document management systems with SVN, for example. 
  - It's not the same thing. Using SVN as a document database is equivalent to using the filesystem as a document database. The only thing extra you get with SVN is a revision history.
  - Git actually is a content database. Its version control capabilities are built on top of that.

- Git and Darcs have very different underlying models. Most importantly, Git is content-centric (diffs are generated only as byproducts) while Darcs is patch-centric (any given "version" is just a sum of all the patches that produce it). Linus, for one, feels strongly that this is an important distinction.

- 🤔 Can Git be made to handle binary files as nicely as Dropbox does? Dropbox is also smart with how it tracks changes to files. Every time you make a change, Dropbox only transfers the piece of the file that changed (also known as block-level or delta sync), making it easy to work with big files like Photoshop or Powerpoint documents.
  - First off, the "block-level" sync is exactly what rsync is for. You'll probably have better results using that. You could track a list of local file paths in git, but sync the binaries themselves with rsync. (They complement each other well.)
  - Tracking changes in binary files (which cannot be merged in any reasonably generic fashion) is a fundamentally different issue than tracking changes in text, particularly source code. Git is designed to do the latter. While you can use it to track changes in binaries, merging doesn't make sense anymore, and hashing/scanning big binary files for changes is significantly slower. (A bunch of images generally won't matter, but I wouldn't use it to track, say, video, or large database dumps.)
# discuss-couch
- ## 

- ## 

- ## 

- ## [PostgREST: Providing HTML Content Using Htmx | Hacker News_202312](https://news.ycombinator.com/item?id=38687997)
- While cool as a proof of concept and kudos for execution, this looks like a nightmare to maintain for any non-trivial webapp.

- Is this kind of functionality / coding pattern used in new or modern applications?
  - Couchdb, a (json) document database, whose api is http-based, had built-in list and detail methods that allowed you to respond with any type of format you could generate within their javascript interpreter. In other words, no need for a server as the client can directly hit the database and get html and/or json back.
  - 🚨 After v1 they stopped working on that front as it makes for nightmare maintenance work.
  - I think many here remember the good old days of php or asp files having sql statemts mixed with html all in a single file. This doesn't look very different.
- It’s far from modern, Oracle had this over 25 years ago.

- ## [Backend Storage Engine, Storage formats used in Couchbase Server 6.x _202011](https://www.couchbase.com/forums/t/backend-storage-engine-storage-formats-used-in-couchbase-server-6-x/28290)
- What is the current back end storage engine used in Couchbase Server 6.x enterprise edition? Is it CouchDB based CouchStore or Magma?
  - Current back end storage engine in Couchbase Server 6.x is CouchStore.
- What is the current file storage format used by the storage engine?
  - Storage format is B+ Tree.
- What is the compaction strategy used to compact the Couchbase buckets?
  - Compaction strategy is %fragmentation based (hence depends on the write activity of your workload).
- What is the index storage format for Global Secondary Indexes in memory and on disk? I understand its Nitro based skip list in memory. What does it look like on disk for data greater than memory scenarios?
  - Index storage engine is Plasma which is based on skip list in memory. Recommendation is to have at least 20% of your index size available as memory.

- ## [CouchDB in multi-tenant environment_201006](https://user.couchdb.apache.narkive.com/Ht2wAdNw/couchdb-in-multi-tenant-environment)
  - I am evaluating CouchDB to be used in multi-tenant environment and would like to know if there are ways to have design documents from one database to be used by a another database.

- Currently this is not supported. CouchDB strives hard to avoid dependencies between databases. I think you'll have a more robust system in the long run if you keep a copy of the application in each client's database.

- ## [Show HN: Open-source obsidian.md sync server | Hacker News_202308](https://news.ycombinator.com/item?id=37247767)
- MongoDB was gaining a lot of traction, and I think because of that many people overlooked CouchDB.
  - I have been obsessed by it(couchdb) the past months. Coming from MongoDB the querying is a bit more limited, but I'd use it over MongoDB in a heartbeat. Very simple to host and even to set up multiple instances. 
  - Also CouchDB was embracing serverless before it was cool with their HTTP API.

- ## after CouchDB is configured as cluster, can I make it a single node again? In a case of docker swarm setup
- https://couchdb.slack.com/archives/C49LEE7NW/p1699208662136709
- Set up a single new node and replicate all databases to it. Way way way easier. But you don’t learn as much about CouchDB internals
- OR
  - Make sure all your databases have shards on at least one node (this is the default in a three node cluster)
  - Turn all nodes off except one.
  - Remove the other nodes from that node’s _nodes database
  - Update each db’s _dbs doc to only reference the one node.

- Updating each db's doc to reference one node might be an overkill of you have TBs of data. What do you think?
  - You are only updating one doc per database.
  - TBs of data will take a while to replicate, so using the originally outline procedure will be a lot faster.
  - If more complicated. Read up on the details in the “moving a shard” section of the doc. Just do the reverse

- ## [Couchdb有在实际生产环境中使用的例子吗？ - 知乎](https://www.zhihu.com/question/20112928/answers/updated)

- [CouchDB in the wild_201812](https://cwiki.apache.org/confluence/display/COUCHDB/CouchDB+in+the+wild)
  - Software & Websites

- ## 🤔 [Ask HN: To everybody who uses MapReduce: what problems do you solve? | Hacker News_201311](https://news.ycombinator.com/item?id=6706545)
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

- ## 🎯 [CouchDB 4.0 + FoundationDB · pouchdb/pouchdb_202010](https://github.com/pouchdb/pouchdb/issues/8195)
- Most of the changes in 4.x are around the implementation - the CouchDB API is mostly the same but with stronger consistency guarantees. For example, the _changes feed in CouchDB 4.x adheres to the old CouchDB 1.x semantics in that it is ordered and clients will not suffer rewinds if the server configuration changes.
  - Bearing in mind 4.x is still a work in progress, it's probably too early to say whether there would be any breaking changes in the API other than what has already been flagged for deprecation in 3.xx, 
  - but I wouldn't expect any changes to be required in PouchDB to stay compatible with replication and the core API.

- Thanks for the reply, having a hard limit for attachments of 8 MB is really a hard sell and I really hope they don't do this. If this is truly the case couchDB 4.0 would not be a viable option for us.
  - Just for clarification document size and attachment size are differentiated, so it appears like the hard limit of 8 MB does not apply to attachments, a lest for couchDB 3.0

- why not use the filesystem instead of attachments? Storing binaries in databases has always been a bad idea.

- I think for us the end to end solution and the same attachment API's that work both within PouchDB and CouchDB was pretty nice. 

- My thoughts would be to get out of attachments as soon as possible. It's not a CouchDB problem. It's a binary-on-database problem. In any database you might attempt this, it's a bad idea. 
  - Attachments would only lead to memory leaks, deep performance problem regarding indexes (binaries can't be indexed), overload, oversize, ... 
  - Using the operating-filesystem it's always best, because a database would not be able to outperform the FileSystem API in terms of performance and speed.

- That can be done as a plugin.. Store all images/so on/.. on local, and when doing replicating.to, write a plugin to handle all those uploads and get URL. That would be real hacky though, and can be easily be avoided by just using Cloudinary directly, and store the URL path on your doc.

- let's try to remove this stale label. also my 5 cents: while CouchDB/PouchDB obviously isn't a CDN, I found attachments to be still definitely useful in cases like user avatars or previews of large media files stored elsewhere. And CouchApps are built from attachments after all

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
  - I had PouchDB on top of IndexedDB handling hundreds of photos without breaking a sweat and those size limits all have nice opt-ins permission dialogs for IndexedDB if you exceed them. Where I found all of the pain in working with photos was server side. 🧐📎 CouchDB supports binary attachments, but the Replication Protocol is really dumb at handling them. Binary attachments would balloon CouchDB's own B-Tree files badly and its homegrown database engine is not great with that
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

- ## 🏘️ [What the HTTP is CouchApp | Hacker News_201008](https://news.ycombinator.com/item?id=1569664)
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
