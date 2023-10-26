---
title: lib-db-pouchdb-community-couchdb
tags: [community, couchdb, pouchdb]
created: 2023-10-07T17:28:56.496Z
modified: 2023-10-07T17:29:16.871Z
---

# lib-db-pouchdb-community-couchdb

# guide

# discuss-stars
- ## 

- ## 

- ## 🚀 fireproof.storage Light up your data!
- https://twitter.com/jchris/status/1633113469179314179
  - check out my new project, a real-time database that runs in any page, with indexes, event feeds, automatic replication, and cryptographic verifiability. 
- It either took me two weeks to write this JSON database, or 14 years.
  - Part of what makes it so easy to use is that it’s an embedded database with network support, like PouchDB or Couchbase Lite. So developers don’t have to worry about setting it up, nor do they have to worry about where the data is stored.
  - The current version just keeps data in browser local storage, but it manages transactions and blocks using the immutable IPFS protocol. This means you can save and load data from almost anywhere.
  - The combination of lightweight runtime, and the ability to reach across the network for blocks, makes me tell my kids I’m making an “infinite database.”
- Limitations: currently encryption is living on a branch that I will merge as soon as I figure out the last webpack issues
- Some of the prime use cases for this sort of technology:
  - adding dynamic features to static pages 
  - saving/memoizing pure functional transforms in a verifiable way (cough: prompt, model, params) 
  - serving as a content-addressed oracle for smart-contract execution 
  - games!

- Are the indexes local-only or also synced? For integration in non-JS codebases, is there a spec to interoperate?
  - The indexes use the same block store as the database, so when you activate replication, they also sync to @Web3Storage , but I think this will be optional, as you’d rather rebuild than copy when you’re on a slow connection.
  - Another option I’ll be adding soon is the ability to serialize the current state as a single car file so that you can embed it in your app for instant preload
  - As far as a spec, not yet. I plan to swap out some of the core data structures with more nuanced implementations, at which point that will be front of mind.

- How does it differ from Pouch?
  - One of the stand-out use cases for this is adding features to Web3 style link in profile pages. Because if you’re deploying HTML that has its content hash in a block chain somewhere, and the html contains the root hash of your database. Merkle!

- ## [What Is JSON Patch? | Hacker News_202205](https://news.ycombinator.com/item?id=31301627)
- Last year I experimented with an app architecture that used CouchDB/PouchDB for for synchronising data for a single user, multi device app. Then using Yjs to merge the conflicting edits - it worked incredible well. If I had the time I would love to build a Yjs/CRDT native CouchDB like database that could use the Yjs state vectors as a wire protocol for syncing…
  - This is the very rough code behind the PouchDB/Yjs datastore. Effectively each Pouch/Couch document is actually "managed" by Yjs, all changes/operations via it. It then saves the binary Yjs blob as an attachment on the Pouch document with the current Yjs state exported as JSON for the main Pouch document. This gives you all the indexing/search you get with Pouch/Couch but with automatic merging of conflicting edits.
  - **Ultimately though I don't think PouchDB is a good platform for this**, building something that is native Yjs would be much better. If anyone is interested I would love to hear from them though!
- Something that stands out immediately to me is that reliance on binary attachments. 
  - 👉🏻 In my own CouchDB ecosystem work binary attachments have turned out to be just about the worst part of the ecosystem. 
  - PouchDB stores them pretty reliably, but every other CouchDB ecosystem database (Couchbase, Cloudant) including different versions of CouchDB itself (1.x is different from 2.x is different from 3.x in all sorts of ways) all have very different behavior when synchronizing attachments, the allowed size of attachments, the allowed types of attachments, the allowed characters in attachment names, and in general the sync protocol itself is prone to failures/timeouts with large attachments that are tough to work around because the break in the middle of replications. 
  - The number of times I've had to delete an attachment that PouchDB stored just fine to get a sync operation to complete with another server has been way too many already.
  - I've had to build bespoke attachment sync tools because I haven't been able to rely on attachments working in the CouchDB ecosystem.
  - I've been thinking that I need to replace the CouchDB ecosystem as a whole. PouchDB is great, but the flux I've seen in the Apache CouchDB project and the issues I've had with the managed service providers especially Cloudant after IBM makes it really hard to recommend the ecosystem. Overall it seems unhealthy/in-decline, which is sad when the core sync infrastructure seems so nice to work with when it works

- ## 🤔 [I created PouchDB. After a year... | Hacker News](https://news.ycombinator.com/item?id=24355263)
- I created PouchDB. After a year or so I handed that project off to some great maintainers that made it much better as I had grown a little skeptical of the replication model and wanted to pursue some alternatives.
- It’s been about 10 years, much longer than I thought it would take, but I have a young project that finally realizes the ideas I had back then.
- 👉🏻 **Sometime after PouchDB was created I realized that it just wasn’t going to work to replicate a whole database to every client**. 
  - In fact, even a view of the database wasn’t going to work, because the developer isn’t in a position to really understand the replication profile of every user on all of their devices, you need a model that has partial, or more accurately “selective” replication based on what the application accesses in real time.
- I became convinced that the right primitives were already present in git: merkle trees. Unfortunately, git did a very poor job of surfacing those primitives for general use and I wasn’t having much luck finding the right approach myself.
- Shortly after joining Protocol Labs I realized they had already figured this out in a project called IPLD. Not long after that, I started leading the IPLD project/team and then putting together my ideal database whenever I found a free moment.
- It’s very young, lots of missing features, still working on some better data-structures for indexing, but **it is very much a database that replicates the way git does and approaches indexing over a primary store the way CouchDB does, but there’s a lot more too**.
- With these primitives we can easily **nest databases inside of other databases** (and create unified indexes over them) and we can easily extend the data types in the database to user provided types. Using some of these features it already supports streams of binary data, databases in databases, and linking between pieces of data.

- dagdb /133Star/MIT/202010/js/leveldb/git/inactive
  - https://github.com/mikeal/dagdb
  - DagDB is a portable and syncable database for the Web.
  - It can run as a distributed database in Node.js, including using AWS services as a backend.

- ## [Show HN: ElectricSQL, Postgres to SQLite active-active sync for local-first apps | Hacker News](https://news.ycombinator.com/item?id=37584049)
- Hey, I work at Electric, The CouchDB/PouchDB pattern is how I originally got interested in local first, they are such a good tool, but having the full power of Postgres and then SQLite on the client, I believe, is a real game change.

- ## 🚀 [Realm Mobile Platform – Realtime Sync Plus Fully Open Source Database | Hacker News_201609](https://news.ycombinator.com/item?id=12589426)
- So this is like alternative to Firebase? How different is their offering?
  - Realm is self-hosted compared to Firebase which is an MBass.
  - Native objects all the way down vs. a JSON structure

- Hi, former Apache CouchDB guy, former Cloudant employee, and former Realm employee here… I (still) love CouchDB but at the end of the day I think its sync is a better fit for server-to-server or web client-to-server use-cases, not mobile-to-server.
  - There’s tons of stuff CouchDB sync doesn’t support that end up being a huge problem with mobile apps
  - Here are the top 3 things Realm adds in my opinion: great client-side performance, native models that are extremely easy to use, and conflict-free sync (not conflict resolution!). 
  - With my own eyes I’ve seen a generation of developers try CouchDB for mobile apps and then abandon it because of the limitation of its approach. I think this is the first general-case true sync (à la Google Docs) for mobile, and I hope it will continue to spur more iterations & innovation in other open-source projects as well.
- As I understand PouchDB is performant, uses JSON (pretty much the definition of "Native Models"), and allows server-arbitrated conflict resolution with stored revisions, making the simplest conflict resolution "last-in-wins" with user UI for "undo" (or any JS-object merge library).
  - I think you're misunderstanding what "Native Models" means in the context of iOS work. Saying that a database uses JSON immediately, to many ios devs, recalls years of writing very fragile json serialization code. Looking through CouchDB's iOS example apps confirms that yes, basically everything that isn't a string or int has to be serialized into JSON. That's a pretty enormous annoyance, and incorporates a lot of additional cognitive overhead when dealing with data that Realm simply handles properly for iOS from the beginning.

- ## 🆚️ [Comparison: PouchDB vs. NeDB_201507](https://github.com/pouchdb/pouchdb/issues/4031)
- I dont have experience with NeDB so only making a comparison by reading the README, but from a brief look it looks like the main differences are PouchDB does synchronisation between the server and the browser, and that PouchDB was designed with the browser in mind. 

- **PouchDB will definitely have overhead compared to the other databases, because it stores everything in a "revision" model where the history of every document is preserved**. (Think of it as git vs just overwriting files.) Hence it tends to have overhead, even for gets/puts.

- Personally, NeDB has become my go-to for most projects. The sole exception I've, thus far, had was an app that had 2.4 million rows of data. NeDB worked, but it created significant lag so I switched to SQLite and made calls to a backend handler for DB interaction.
  - I considered PouchDB, and it definitely looks like a better alternative for very large datasets ... but I think I'd still go with SQLite in those cases. For most things, according to the benchmarks posted by @user8614, NeDB appears to perform as well or better.
- I work on PouchDB, in terms of those points:
  - "great client-side performance": PouchDB is more than fast enough for most use cases, its just a wrapper over indexedDB. (there are areas we can improve, particularly performance of map reduce / mango queries).
  - "native models that are extremely easy to use": Not sure what that means, PouchDB and CouchDB use json, its native and easy to use in JavaScript
  - "conflict-free sync (not conflict resolution!)": Certainly going to have to take a look at this, any conflict free sync protocol I have seen put a lot of limitations on how data within your application is structured but conflict resolution certainly is something that can be improved within Pouch / Couch.
  - I do think there is a bunch we can (and are) improving in PouchDB and its great to see alternatives, will be looking into this further now. But I certainly do not agree that (C|P)ouchDB are not suited for mobile <-> web sync, thats the primary use case I work on Pouch for.
- In general, I tend to be skeptical of systems that hinge(依赖；装上铰链) on last-write-wins, but LWW is definitely a model that works in a lot of cases where you're not too concerned about the possibility of losing data, and it's also a simpler mental model for the app developer.
- 👉🏻 Realms approach to conflict resolution is very different from what you see in products like Couch.
  - Realm is an _object_ database, so in contrast to document databases where conflict resolution happens very coarse grained at the document level, in Realm it happens at the object level (and actually all the way down into individual properties).
  - This essentially means that the entire object graph is treated as one big CRDT, transparently handling conflict across individual objects, properties and relations.
  - When talking about ordering by time, both in the context of LWW and insertions in lists, we are talking about **vector clock time**, not necessarily device time (or though that is taken into account as well).
- LWW is a tradeoff. You'll be better off selling it as an automated-resolution option on top of manual resolution, instead of an innovation over manual resolution. (MV registers are a CRDT as well!)
- Adam from Realm. Our approach differs in building off our object database. We couple this with low-latency sync that only transmits changes and deterministic conflict resolution, making collaborative experiences really easy to build

- ## 🚀🔥 [PouchDB, the JavaScript Database That Syncs | Hacker News_201612](https://news.ycombinator.com/item?id=13101870)

- Do you mind me asking why you choose to use PouchDB in this way instead of Realm for React Native?
  - 1) Realm works only in React Native and not in React web. This has paid off in the prototype mode because it allowed us to build some simple reports in our web product.
  - 2) Realm was very new and I felt we were already using too many new frameworks. 
  - 3) On the server side, CouchDB has Futon to simplify our learning curve and give us a basic GUI to have a sanity check when our code wasn't functioning as expected. Not sure what Realm's server side looks like.

- 👉🏻 We've been running PouchDB in production for ~15 months now. We chose it because it was a greenfield project and it gave us 2 things: Easy offline support and real-time syncing that makes it easy to create collaboration a-la Google Docs.
  - In terms of architecture we have about 250 tenants with separate Couch databases per each. We're still running Couch 1.6. We have yet to evaluate Couch 2.0.
- we had to tackle few interesting problems that came along
  1. Load times. Once you get over certain db size the initial load time from clean slate takes ages due to PouchDB being super chatty. I'm talking about 15-30 mins to do initial sync of 20-30mb database. We had to resort to pouch-dump to produce dump files periodically. That helped a lot. I think this issue has been rectified with Couch 2.0 and sync protocol update.
  2. Browser limits. Once we hit the inherent capacity of some browsers (namely Safari on iOS, 50mb) we had to get creative. Now we're running 2 CouchDB databases for each tenant where 1 has full data and the other only contains last 7-8 days. Pouch syncs to the latter one. We run filtered replications between the full db and the reduced db and do periodic purging. On the client side if a customer tries to go back more than 7 days we just use the Pouch in online only mode where it acts as a client library to remote couch and doesn't sync locally.
  3. Dealing with conflicts. This might matter or it might not depending on the domain but you have to be aware of data conflicts. Because CouchDB/PouchDb is eventually consistent multi-master setup and you will get data conflicts where people update the same entity based on the same source revision. PouchDB has nice hooks to let you deal with this but you have to architect for it.
  4. Custom back-end logic. Because Pouch talks directly to Couch you can't exactly execute custom back-end logic when needed. We had to introduce a REST back-channel to make sure our back-end runs extra logic when needed.
  5. We had some nasty one-off surprises. Last one was with an object that had 1700 or so revisions in couch and once it synced to PouchDB it would crash the Chrome tab in a matter of seconds. Due to the way PouchDB stores revision tree (lot's of nested arrays) Chrome would choke during `JSON.parse()` call and eat up memory until crash. We resolved this one by reducing the revision history limit that is kept.
- That chattiness is what has driven me away from Pouch, sadly. It's a flaw in the Couch replication protocol design that won't be fixed until the spec is changed.
  - The chattiness is mostly addressed with _bulk_get in CouchDB 2.0 - Pouch will automatically use it if the server supports it. Another option is to stick a HTTP/2 proxy in front of your CouchDB instance - the chatter to the db is ultimately still there but it significantly reduces the latency cost to the PouchDB client. There are plans to add first class HTTP/2 support to Couch but for remote client architectures just adding a proxy should be a significant improvement.
- nested recision tree: I think Nolan ended up writing a non recursive JSON parser to deal with this and there was some debate about whether it made sense to be used as it was significantly slower (though could handle deeply nested structures)
  - Yup, exactly. We use JSON.parse inside of a try/catch and then fall back to vuvuzela which is a non-recursive JSON parser in cases of stack overflows
  - Unfortunately the only way to resolve this without vuvuzela would have been to change the structure of the stored documents which would have required a large migration, so I'm glad to hear that the vuvuzela solution was the right way to go.

- 🤔 on the server side, is one database per user feasible? IIRC Couch can only handle 100 or so different databases on one instance. And you can't do views across them.
- PouchDB contributor here.
  - There are actually several layers of "cache" inside of a browser, including the traditional HTTP cache (which is global) as well as the site storage, which includes stuff like IndexedDB, WebSQL, LocalStorage, AppCache, and window.caches (all of which is per origin)
  - This site storage _can_ be cleared by the browser (it's "temporary" per the spec), but in practice it isn't very frequently cleared unless the machine is running low on space. E.g. Chrome only does it if a site exceeds 20% of total per-origin browser storage
  - In any case, when the browser does clear this storage, it clears everything at once for that origin, so the user essentially has the experience of visiting the site for the first time. 
  - This is why it's a good practice to periodically sync your PouchDB data to CouchDB because it can be lost in rare cases.
- Client side pouch happily syncs directly with server side couch
- Right, but how do you scale that out on the server-side while protecting data on a per-user basis? Sorry if I'm missing something obvious.
  - Usually you create a separate database for every user. This sounds _nuts_ from a traditional database mindset, but works great in Couch. You can then create another database that replicates from all the user databases in order to perform your aggregate queries on the back end.
- Seconded. This is the standard CouchDB approach: one database per user.
  - Sounds weird coming from my Postgres and MySQL background, but works great in practice, depending on your use case and if you clear out old revisions and unused docs, which for our use case can number into the thousands fairly rapidly.
- You can then create another database that replicates from all the user databases in order to perform your aggregate queries on the back end. **That sounds horribly space inefficient**.
  - Yep. Everything in software is a trade-off. This trades space efficiency for multi master replication with first class offline app experiences. For many cases, that's a fine trade. Disks are cheap. If that isn't a fine trade for a particularly large dataset, use a different technology that's better at space efficiency and worse at other stuff.

- Any guidance on moving from Cloudant to CouchDB? Are you hosting it yourself? If so, has the amount of maintenance been more than you expected, or was it mostly setup time and then forget about it?
  - Yup, hosting it ourselves. Its a peach. There are few things that it doesnt come with out of the box - clustering, Full text search, geoindexing, chained map reduce, auto compaction, index auto-updation. Once thats done, if anything it was more forget about it than Cloudant, which bills on requests / thoroughput. This can catch you out because continuous replications between databases on the same cloudant account are also counted as requests and billed as such. 

- I let the user decide to logout and destroy or just logout if it's a trusted device but obviously the local db could be accessed. Most users don't logout and I set a long cookie expiration. You could also encrypt data.

- Is the project sponsored by Couchbase? If not, have you thought about publishing a storage API that the replication protocol calls so that it could be adapted to work with any backend db? What about P2P sync - (eg. serverless) has anyone thought of making PouchDB do that?
  - For pluggable storage engines our node.js adapter uses leveldown, so any *down backend can be plugged in.
  - For p2p yup its been something quite a few people have been using pouchdb for, one of the more notable examples has been http://thaliproject.org/, the core storage format is entirely compatible with p2p (inherited from couchdb)
- The idea of making pouch sync with other databases is covered in their faq
  - Basically, your other data base probably handles conflicts in a different way to Couch that would make syncing this way nonsensical.
- Couchbase is more or less a merge of Membase and Couchdb. With Couchdb it only shares its lineage and its creator; apart from that they are entirely different beasts

- I'm interested in PouchDB to make my JavaScript app easily sync to the server, but I don't want to switch my server's database from Postgres to CouchDB. Surely I'm not the only one in this situation?
  - A lot of people would like their current data to just be able to sync, but it almost always needs changes in the way data is stored and complementary changes to the application code

- 🤔 what's the benefit of using PouchDB as opposed to vanilla localStorage functionality?
  - the main use case of PouchDB over plain browser storage is its ability to sync data.
  - It can sync data between CouchDB servers (e.g. IBM Cloudant) and the browser.
- The sync happens in an unmanaged fashion, without the user or the application programmer having to care about the state of the connection.
  - Your PouchDB application works locally on your device, whether the connection is up and down, and the data is synched with the remote database whenever there is connection.
- The alternatives to this PouchDB to CouchDB synching mechanism would have to be either:
  - the user checks whether the connection is up, and manually manages the sync, or
  - the application programmer saves the user the trouble by adding code that checks whether the connection is up, and automatically manages the sync
- Using a synced data model provides a few features for users, data access is efficient and far far faster (disk/memory is faster than network) and it allows offline usage (+ failure tolerance, the server goes down the client still works). It can also enable p2p use cases and a bunch of other things, the above 2 are the main drivers though
- localStorage quota is 5MB (per domain IIRC), PouchDB uses IndexedDB or WebSQL internally, which gives you a lot more quota
  - localStorage is not indexed, you have to implement some sort of lookup yourself. If you go that way, a tip is to store values as objects with ids as keys, that way you get a sort of hash map as index thing going which alleviates things a bit. PouchDB is indexed and provides a way to query your documents.
- Computed views.

- Datomic-ClojureScript in the browser backed by PouchDB would be killer.
  - Datomic already has a CouchDB-compatible datastore via its support for Couchbase. That would mean Datomic-ClojureScript on PouchDB could run in the browser and sync with Datomic-Clojure backed by CouchDB/Couchbase on the the server -- that would be killer and give Datomic massive reach.

- 🤔 PouchDB's replication capability is interesting, but is there a way to make it **lazy load to the local DB instead of doing everything up front**? I hesitate to use it for a web project with 10+ MB of docs where it would otherwise be ideal.
  - You can provide a **server-side filter function** to replication and progressively filter partial replications until eventually everything gets replicated. At that point it becomes a question of architecture of your documents: how much is needed to replicate before a user may be productive?
  - You can also explore **pouchdb-replication-stream** to build bundles that PouchDB can bootstrap from a little bit faster than a chatty replication.
  - That said, I've found initial replications of large databases (one I've worked with this week is a 25+ MB CouchDB database full of photos) is **quick enough** (and mostly bandwidth constrained) that I haven't had much in the way of concern over it.
# discuss-couchdb/couchbase
- ## 

- ## 

- ## [Ask HN: To everybody who uses MapReduce: what problems do you solve? | Hacker News_201311](https://news.ycombinator.com/item?id=6706545)
- 👉🏻 It's worth noting that CouchDB is using map-reduce to define materialized views. Whereas normally MR parallelization is used to scale out, in this case it's used instead to allow incremental updates for the materialized views, which is to say incremental updates for arbitrarily defined indexes! 
  - By contrast SQL databases allow incremental updates only for indexes whose definition is well understood by the database engine. I found this to be pretty clever.
- I've been using CouchDB (and now BigCouch) for about four years and it's both clever and useful. We're storing engineering documents (as attachments) and using map/reduce (CouchDB views) to segment the documents by the metadata stored in the fields. The only downside is that adding a view with trillions of rows can take quite a while.

- ## [MiniCouchDB in Rust | Hacker News_202006](https://news.ycombinator.com/item?id=23446852)

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

- ## [We have a problem with promises | Hacker News_201505](https://news.ycombinator.com/item?id=9564076)
- as I mention in the article, ES7 async/await should help fix that

- ## [Datomic Update: Client API, Unlimited Peers, Enterprise Edition, and More | Hacker News_201611](https://news.ycombinator.com/item?id=13055961)
- SQL views don't compose at the same level that Datalog expressions do, but that's because they aren't typically expressed as raw graph data (i.e. lists of strings where each list item is a node in the graph). If you could just name arbitrary chunks of SQL AST and mash them together, it would be just as composable (though perhaps more cumbersome due to boilerplate).
- you might give CouchDB a look. It's a document datastore that offers map/reduce views written in Javascript (use as much or as little composition/abstraction as you want). The distributed features are pretty cool (bidirectional sync, versioned documents) and writing apps with it is awesome

- ## [Cloudant/IBM back off from FoundationDB based CouchDB rewrite | Hacker News_202203](https://news.ycombinator.com/item?id=30652281)
- [Important update on couchdb's foundationdb work-Apache Mail Archives](https://lists.apache.org/thread/9gby4nr209qc4dzf2hh6xqb0cn1439b7)
  - CouchDB embarked(开始；从事) on an attempt to build a next-generation version of CouchDB using the FoundationDB database engine as its new base.
  - The principal sponsors of this work, the Cloudant team at IBM, have informed us that, unfortunately, they will not be continuing to fund the development of this version and are refocusing their efforts on CouchDB 3.x.

- The FoundationDB rewrite would introduce a size limit on document attachments, there currently isn’t one. Arguably the attachments are a rarely used feature but I found a useful use case for them.
  - I combined the CRDT Yjs toolkit with CouchDB (PouchDB on the client) to automatically handle sync conflicts. Each couch document was an export of the current state of the Yjs Doc (for indexing and search), all changes done via Yjs. The Yjs doc was then attached to the Couch document as an attachment. When there was a sync conflict the Yjs documents would be merged and re-exported to create a new version. 
  - The issue being that the FoundationDB rewrite would limit the size and that makes this architecture more difficult. It’s partly why I ultimately put the project on hold.
  - (Slight aside, a CouchDB like DB with native support for a CRDT toolkit such as Yjs or Automerge would be awesome, when syncing mirrors you would be able to just exchange the document state vectors - the changes to it - rather than the whole document)
- As others have noted, the solution to storing attachments in FDB, where keys and values have an enforced maximum length, is to split the attachments over multiple key/values, which is exactly what the CouchDB-FDB code currently does.
  - The other limit in FDB is the five second transaction duration, which is a more fundamental constraint on how large attachments can be, as we are keen to complete a document update in a single transaction. The S3 approach of uploading multiple parts of a file and then joining them together in another request would also work for CouchDB-FDB. While it _could_ be done, there's no interest in the CouchDB project to support it.
- Exactly, almost all the time you would be better to save the attachment to an object store. However I think I found that small edge case where the attachment system was perfect. It was essential to save the binary Yjs doc with the couch document, it needed to be synced to clients with the main document. Saving it to an object store is not viable due to the overhead during syncing.
  - yup. the purpose of couchdb's original attachment support was for "couchapps". The notion that you'd serve your entire application from couchdb. Attachments were therefore for html, javascript, image, font assets, which are all relatively small. The attachment support in CouchDB <= 3.x is a bit more capable than that due to its implementation, but storing large binaries was not strictly a goal of the project.

- SyncedStore is a brilliant Yjs reactive store for SPAs, it’s not a database. It like an automatically distributed real-time reactive redux/vuex for collaborative apps.
  - The y-IndexedDB you linked to is actually part of the Yjs toolkit, it is a way of persisting a Yjs document in the browser for offline editing in a PWA. It doesn’t provide a way to sync a whole (or subset of a) database like Couch/PouchDB does. It’s a very important part of the Yjs toolkit but doesn’t do what I’m describing (it’s just a key value store).

- I don't see why there would be a fundamental reason why there would be an attachment size limit. I guess it would just need to be implemented by breaking the attachment into multiple keys? There may be some overhead but it seems that this is valuable because it allows large attachments to be split across servers as required.
  - FoundationDB has size limitations on the k/v pairs it can accept and splitting documents and writing those chunks in small transactional batches is the recommended workaround (along with some other 'switch over' transactional write which makes the complete document visible all at once.)
  - If I remember the fdb docs, there's also a time limit on transactions that further limits the feasible max size.

- So what's the deal with the unpopularity of CouchDB?
  - Querying in a more ad-hoc way (vs. building indexes ahead of time and querying by key, etc) is a bit janky / not 1st class (I think mango addresses this but not entirely sure).
  - The runtime being erlang? It certainly seemed to be the cause of some issues when I tried to run it in WSL, or atleast my lack of knowledge with erlang made diagnosing it more trouble.
  - The JS query server engine is/was fairly old (I think it might have jumped to a more recent version of Spidermonkey at some point), and hooked up in a way that, while more modular, limits the performance (documents have to be serialized to/from the engine in another process, rather than just natively passed in)
  - The authorization model is... unique. You can limit down to a doc/field level who can submit changes 
  - the admin interface "fauxton" never really felt finished and debugging views is not welcoming for new users.
  - It's been a while, but seems like many people wanted something simpler like MongoDB for a NoSQL document database. CouchDBs map/reduce queries were hard to get people's heads around, many people didn't need attachments, etc.

- The FoundationDB Document Layer is compatibile with MongoDb 3.x API. https://github.com/FoundationDB/fdb-document-layer .and you get the transaction Al integrity. I stopped using MongoDB and switched to this.
  
- ## [Kinto by Mozilla – An open-source Parse alternative | Hacker News_201601](https://news.ycombinator.com/item?id=10994736)
- CouchDB is so underrated in this space.
  - I get it: CouchDB was a very early (the first real?) document-based database, and it got some things wrong, or at least weird early on (e.g. map/reduce queries, a reduce step to the map/reduce query that is actually one-to-many (on purpose! there are concrete reasons in real life you want this!), etc.).
  - But they also got so much right:
  - The database is all HTTP, all the time.
  - Offline replication and database streaming, standardized at the protocol level
  - You can store your HTTP assets right alongside the DB for Firebase-like asset hosting.
  - You can store full-blown files, which is great for lots of practical app these days.
  - Trivial replication. The scaling of CouchDB itself is honestly a bit crappy, but Couchbase has great scaling
- 
- 
- 
- 
- 

- ## 💡 [Ask HN: Pros and Cons of Using CouchDB? | Hacker News_202205](https://news.ycombinator.com/item?id=31423986)

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
  - corporate supported development is dwindeling (I believe, not entirely up to date on this)
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

- 
- 

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

- I have never heard of anyone saying erlang is bad because of couchdb. I've heard criticisms of couchdb itself, sure. But they've been more along the lines of "MVCC multi-master document stores are not a good solution for this problem" more than "CouchDB is a bad MVCC multi-master document store".
- It doesn't use real node-local/shard-local MVCC AFAICT. It's O_APPEND on flat files.
  - It _is_ append only. But doesn’t use flat files. The main storage files have 2 different immutable btrees to find documents (by id and by sequence num). And it does have mvcc for both storage and secondary indexes. Internally it has transactions but they aren’t exposed to the user, as multi document transactions don’t make sense for the replicated document model.
- Can I ask how the MVCC is implemented (e.g. WAL, MVTO, MVRC, etc.), or if there's documentation around that might give some additional insight?
  - Here’s a link that describes the Couchstore file format. It’s the storage engine for Couchbase and is essentially the same design as CouchDB. https://github.com/couchbaselabs/couchstore/wiki/Format

- The main point is to sync server side data to a client side database, smoothly, so that the application can continue to function offline and then resync once the connection is re-established.
  - The main point is to sync server side data to a client side database, smoothly, so that the application can continue to function offline and then resync once the connection is re-established.**Couch has always been good at this use case** where systems on both ends may have changed in the disconnect time.
  - Realm looks like a much more modern solution to that problem.
- Not entirely sure what you misunderstand, PouchDB stores multiple revisions because thats how CouchDB's sync protocol works, the point of PouchDB was to match CouchDB semantics. PouchDB (as CouchDB) provides options to control how much you track (revs_limit, auto_compaction) and there are improvements we could do to handle tracking less information better. We use transactions under the hood actually writing data to indexeddb
  - I mean I both get it, and don't get it. CouchDB is all about master-master, and pouchdb just brings that to the browser. But at the same time I don't understand why you'd want a 'master' at the edge of the network, or the overhead of multiple revisions when a users browser isn't going to have tones of concurrent connections.
- I had to make that distinction fairly early on wether PouchDB would be an edge client or a full node and I decided full node, tradeoffs either way but pros of being a full node:
  - Additional (p2p) use cases, honestly I dont use CouchDB much these days, I use express-pouchdb-server so I can embed pouchdb into my server easier than any other database, there is also pouchdb-server and p2p projects like Thali
  - CouchDB existed, sync is super hard, writing an edge client would have meant designing it myself, writing a couchdb clone meant I needed to make a lot less decisions about how it worked while being very confident it would work, The test suite runs the same tests against pouchdb/couchdb to ensure compatibility (and replication via each configuration)

- ## 🆚️ [What is the difference between CouchDB and Couchbase? - Stack Overflow](https://stackoverflow.com/questions/5578608/what-is-the-difference-between-couchdb-and-couchbase)
- [Couchbase vs CouchDB NoSQL Systems: Difference Between Them](https://www.couchbase.com/comparing-couchbase-vs-couchdb/)
- I think CouchBase seem to be perceived as CouchDB's 'enterprise' alternative. Which in a way seem to be true. Apart from lack of ability to attach files to records ( documents) and 'out-of-box' REST endpoints compared to CouchDB, CouchBase has sql like language i.e. N1QL (sometimes pronounced a Nickel, UPDATE renamed to SQL++ in Couchbase 7.0). This is one of the reason why I don't really like / recommend using the term 'NoSQL'. I personally like term 'Non-relational'.

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

- Reducing max document size from 4GB down to 8MB seems hyper-restrictive.
  - 8MB is just the default, you can switch it back to 4GB if you want, but you won't have an easy time switching to 4.0 due to the 8MB limit imposed by FoundationDB.
- **If you're trying to store single GB documents in couch, you're doing it wrong... Unless those are binaries you can usually fragment data logically across many documents, then write custom views to aggregate however you need to.**
  - Updates on huge docs would be painful!

- Couch/Pouch combination is really slow when document +attachment are too large. Based on my experience, Practical limit was more like 20-30Mb, and I'd suggest not even getting close to that. 8Mb simply recognizes reality.
  - That’s another great point, an exactly why we are doing this. It is a best practice already.

- why would you use CouchDB over something like MongoDB?
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

- Custom backend means no synchronisation and no advantages over postgres. Is there any secure open source code with pouchdb/couchdb integrations?
- Your backend can be a reverse proxy that authenticates requests then passes them off to CouchDB (or PouchDB, since that also runs on the server). I have an example up @ https://github.com/daleharvey/noted. The server is 200 lines and does signup / email authentication etc.
  - This server can't prevent authenticated user from uploading huge document of running expensive query.
- Any reverse proxy can limit the the size of a document upload. Even just plain NGINX can do that. Just set the client max body size.
  - As for queries, it kind of depends on your model. Mango queries are pretty limited (no joins, no arbitrary filters), so it's not necessarily as easy as you think to write one that hosed performance. A client could of course write one that doesn't use an index, which may or may not be a concern.
  - An easy option if it is though is just don't expose the _find endpoint, which effectively limits your users to the map/reduce queries you've written (unless you give them admin they don't have the ability to create their own).
- A popular model is for the clients to run the queries locally, the server doesnt need to expose any query endpoints, only the ones necessary for replication.
- I feel like your thinking about Couch as exposing your entire PostgreSQL DB to the internet, whereas with couch, a common model is to have a single database per user. In the Postgres model, providing the end user with any direct access is a nightmare, because every other users data is in there and I have to keep other users from viewing/modifying it. In Couch, you give them access to their database and only their database, that's how you isolate users.
- If I use backend I can create all validation logic in application server. But in this case no automatic synchronisation. One of the major selling point of couchdb is replication protocol for client-server data syncing. When you design product with posgress you don't allow to execute raw sql queries from clients without any application server. But looks like it is recommended way to update data in couchdb world if you want to have synchronisation. I can't understand how can this architecture be secure?
  - Couchdb has options for controlling which documents are replicated. This may help depending on your use case.

- 👉🏻 You can replicate all per-user DBs into a central database today.
  - We are working on per-document-access-control at the moment, to support this use-case out of the box

- there are no changes to the replication protocol in Couch 3.0, so PouchDB already works.

- The newest version of CouchBase mobile no longer supports CouchDB as a replication target. It can still be accomplish with the CouchBase Sync Gateway, but get complicated quickly.

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
# discuss-sync/collab
- ## 

- ## in the pouch/couch model this will create a conflict that apps need to resolve, because they can’t know if the server or the client has the “correct” lastest change.
- https://twitter.com/CouchDB/status/1313857978181844992
- see [Use JSON Patch to Resolve Conflicts for CouchDB](https://neighbourhood.ie/blog/2020/09/15/use-json-patch-to-resolve-conflicts/) for automating some of that conflict resolution.

- ## Has anyone here ever used PouchDB, or some other IndexedDB adapter to create a distributed sort of "peer-to-peer" database? 
- https://twitter.com/BenLesh/status/1316085574697136128
- gundb should help you with p2p stuff
- CRDT 
- https://github.com/natevw/PeerPouch /js/inactive
  - A plugin for PouchDB which allows a remote PouchDB instance to be used locally. 
  - It transfers data over WebRTC, for simple lower-latency remote access and even particularly peer-to-peer replication!

- ## Anyone have experience using automerge CRDT in their apps for offline mode and cross-device sync? Would you recommend it over something like PouchDB/CouchDB? _202011
- https://twitter.com/andrey_butov/status/1333419124878417920
  - The one-db-per-user with proxy-auth approach is a bit hard to swallow.
- I don't use automerge, I use my own crdt implementation. I'm happy with it, but I'd only recommend it if local apps give you a real advantage. It is difficult to make schema changes some features are hard without a centralized point
  - but the payoff is very good, so it's worth it if you can take on the challenges. For auth, I just use my centralized server for that.

- ## [LevelUP Proposal_201401](https://github.com/pouchdb/pouchdb/issues/1250)
- theres work to experiment using a level based backend 

- ## [Sync Issue](https://github.com/pouchdb/pouchdb/issues/5291)
  - would like to know if theres a way to sync between local and remote db's only some specific documents, and only some specific attributes in each document, instead of the default behavior that syncs every document and attribute ?

- Sounds like you want to do a filtered replication
- In CouchDB (and PouchDB) there is a concept of a design document, this can give you a partial representation of your database (like a view).

- ## [how to to do partial (descending)l sync? F.e. chat messages](https://github.com/pouchdb/pouchdb/issues/8221)
  - Imagine I have chat app, and chat may have potentially million of messages in a room. What is a best practice to sync such a database to web browser? Is it possible to sync f.e. last 1000 messages, then if user scrolls, resync last 2000 messages?
  - As I understand I can achieve this passing query_selector to replicate method, but the question is, will it resync items with sequence_number lower then last sync? I mean will it sync oldest messages after newer message was synced?

- You can use filtered replication

- ## [Automatic Conflict Resolution_202008](https://github.com/pouchdb/pouchdb/issues/8163)
- There is a plugin for pouchdb that helps with conflict resolution
  - https://github.com/pouchdb/upsert
  - There is also a guide in the pouchdb docs about using upserts to help manage conflicts. 
- There's a big difference: 
  - 👉🏻 C/PouchDB's Conflict resultion suggestion is to **use an arbitrary version of two conflicting items** (I think on default it is to just ignore conflicts). 
  - Ex: JSON Item A and JSON Item B have both the same rev number when they want to be added to the main database. 
  - Since both have different changes, only one item can be used (like the last submitted). In contrast, automerge would look for the differences in the actual JSON objects, and automatically merge both, so that the latest changes of each version is added to the database.

- 👉🏻 This looks to me like what https://github.com/redgeoff/delta-pouch does. 
  - It saves the changes in order and syncs the changes. 
  - The data is a result of all changes applied in order. 
  - It is mentioned in PouchDB Conflicts guide.

- ## 🤔 [I think CouchDB/PouchDB do this similarly, the winner is deterministic though? | Hacker News](https://news.ycombinator.com/item?id=30414871)
- CouchDB and PouchDB have no idea how to merge a conflict, if two copies are edited prior to syncing, one version it marked as the 'winner' and the other as a conflict version. As the developer you can then either chose to dispose of conflicts or have your own way of merging them.
- This is actually a perfect use case for CRDTs such as Automerge and Yjs, I actually built a proof of concept combining Yjs with PouchDB to handle the conflicting edits

- ## [Distributed offline editing with couch/pouchdb - Yjs Community](https://discuss.yjs.dev/t/distributed-offline-editing-with-couch-pouchdb/340)
  - Has anyone experimented with using Yjs with pouchdb as both the datastore and communication channel?

- I recommend to mark transactions as remote when the update was created remotely. This is useful meta-information.

- ## 💡 @pouchdb wont lose data, the conflict is stored and reported, both(all) documents available to choose/create winner, 
- https://twitter.com/daleharvey/status/1043057187113848832
  - we do have encryption plugins (https://github.com/calvinmetcalf/crypto-pouch), no server copy however we dont do
- Yeah I know :) but since the version is only stored per-document, not per-field, you will end up losing data. You could try to auto-resolve by ways merging conflicts... but in which order? You can’t be sure and have to ask the user or something
  - By losing data, I mean from the UX perspective. User syncs, from their view the data is gone. Sure it’s internally there, but they’d have to manually bring it back. This is fully conflict free
- 👉🏻 The app decides which conflict resolution to take of which Last Write Wins, Merge strategies, CRDT or Users Choice are various options, tradeoffs involved in giving that choice to the app developer but prefer to not hear people advertising @pouchdb loses data since it doesnt :)
- Fair enough, good to clarify. Still a big problem that versions are document-level and not field-level though, hard to use CRDTs accurately with that
  - 👉🏻 You could have versions be change level if you wanted (https://github.com/redgeoff/delta-pouch), having fields merge and report only on same field changes is a pretty easy thing to write but I would like to see @pouchdb one day expose these choices as far simpler options
- Nice. With last-write-win though, you don't even need to store the entire history of changes, just the latest one. Anyway, all tradeoffs. I was able to still leverage sqlite with very efficient storage of this info. Pouch has different tradeoffs, still good!

# discuss
- ## 

- ## 

- ## 

- ## I am actually using @pouchdb instead of the native @CouchDB . Which they are similar in many, there are differences that can throw one off. In my case, PouchDB's _sum can't do js object.
- https://twitter.com/yuankuan_/status/1316634065747943424
- The proposal is to disable them by default, not to remove the functionality.

- ## [Django, HTMX and Alpine.js: Modern websites, JavaScript optional | Hacker News](https://news.ycombinator.com/item?id=29319034)
- we use pouch+couch to one way sync from our server to thousands device. And from our sales force device to our server while we still save the data in pouch, we choose to use pwa's service worker to send directly to postgresql instead of pouchdb-couchdb sync.
  - Thanks for the reply. And I guess you do the service worker -> postgresql thing to avoid the database-per-user setup with pouch-couch 2-way sync?

- ## [Local-first software: you own your data, in spite of the cloud | Hacker News_201911](https://news.ycombinator.com/item?id=21581444)
- I may be biased as the maintainer of PouchDB but you can do all this today (and for the last 5+ years) with PouchDB.
  - The comment about CouchDB and the "difficulty of getting application-level conflict resolution right" I am not really certain how it applies, 
  - You dont have to handle conflicts in Pouch/CouchDB if you dont want to, there is a default model of last write (actually most edits) wins but you can handle them if needed
- I'm one of the local-first paper coauthors. I'm a fan of PouchDB (thanks for that) and the whole CouchDB lineage(直系/血统)
  - I've been down the CouchDB/PouchDB path several times with several different engineering teams. Every time we were hopeful and every time we just couldn't get it to work.

- ## [Offline-First Apps: Why Should Apps Be Made to Work in an Offline State? | Hacker News_202208](https://news.ycombinator.com/item?id=32544837)
- I’ve tried PouchDB before but only on “toy” projects not deployed production. What challenges have there been with PouchDB or other offline-first techniques?
  - I like offline first app design, and have built several. However, I don't do it anymore unless there is a very clear use case and direct customer benefit. Some apps just don't work offline at all.
  - 👉🏻 One of the decision trees is **you often have some API needs and can't just live within the pouch db database. Particularly account creation and such.** It may need to plug into other services and initiate them, you could use a database as a message queue, but it's awkward compared to an API.
  - The couch/pouch models gets somewhat more complex when you leave the one db per user model. If there are shared data buckets, the database access patterns require a good deal of thought and experience with the couch db auth model. Particularly it's limitations.
  - Offline access also requires thought around sensitive data. If a user has had their access revoked, an offline first app may preserve it which can rub against security requirements.
  - Initial sync can be very slow if you're dealing with a lot of data. This can be a poor experience if you make a new user wait minutes to get started. Or you can also build a backend so they can start immediately and then switch to the local copy after replication. I've build this kind of system before.
  - There are advantages to the route. Minimal data transfer from the server can represent lower load for your services. You can also do an offline only model for data, potentially lowering cloud costs for the number of users you serve - a definite boon(恩惠, 好处) for free tiers.

- The only thing approaching an off the shelf solution to this is the CouchDB replication protocol. While technically good, it suffers from a number of issues if you want to use it in practice:
  - dearth of cloud providers for CouchDB
  - There's pouchDB for the browser but there's nothing for native mobile clients
  - While PouchDB is great, it has to run on-top of browsers IndexedDB implementation, all of which suffer from reliability and capacity issues

- When building an iOS/Android hybrid app with web technology, SQLite can be used as storage engine for PouchDB.

- ## 💡 [RxDB – a real-time database on top of PouchDB | Hacker News_202009](https://news.ycombinator.com/item?id=24340802)
- I built the first version of NoteBrook on top of couch/pouch, and the biggest pain points were:
1. Pouchdb was before async/await and typescript. The typings can be inconsistent, and it’s very difficult to properly manage the lifetimes of local databases because of the promise chaining.
2. A database technology for Real time replication Needs ACLs on a per-document basis. I built provisioning scripts to manage separate databases per user, as suggested, and it’s very cumbersome. It prevents me from lots of data sharing models like promoting one record to public view, or sharing a record with another user in a different tenant.
3. Personally I feel that the naming / marketing of the product is poor. It does not feel professional ( couch, futon, fauxton, pouch, couchbase) do not feel like professional grade products I can depend on to run a business.

- I don't see any authentification related suff like pouchDB have, like create an user with password hash, auto handle cookie in the browser, restrict document to user or group.

- ## [Downsides of Offline First | Hacker News__202110](https://news.ycombinator.com/item?id=28717848)

- PouchDB works well as the primary client store and can sync to CouchDB in the cloud. IMHO this is one of the more mature combinations that gives you a ready client side document database that takes care of data replication for you.
  - Unfortunately, I think PouchDB <=> CouchDB replication has past the "mature" point to the "decrepit" and "falling apart" stage, maybe to the point of "evolutionary dead end" if I'm feeling strongly pessimistic enough, and I've been for years trying to figure what to replace it with.
  - I too have to noticed that CouchDB may not have the best/compatible future. I have an existing product that depends on PouchDB in the client and the replication. I'm not really into the managed db service offerings. My tentative solution for the application is to go with PouchDB on node.js on the backend too

- I've been working on offline-first apps (CouchDB/PouchDB + Cordova/Capacitor and published via App/Play Store) in the last years and can definitely relate. But some points to add:
  - The 7 days IDB limitation does not apply for apps that are published through the stores
  - Conflicts can happen, but depending on your design they might not matter in practise. „Implement a proper conflict resulution strategy“ has been on my „todo: maybe“ list for over 3 years now but was never important enough.
  - Data migration is not needed as long as schema changes are additive (new doc fields, new doc types). Design carefully early on, keep track of „abandoned“ properties and you'll rarely need a difficult migration.
  - Depending on the performance of your customers' phones and the amount of data your app is processing, it (JS -> ... -> IDB and back) might not be fast enough. I had to add caching layers for some use cases. But at some point, you probably want a proper state management library anyways which should include caching nearly for free.
  - You can (and should!) still consider most of your data relational. There is even a relational-pouch plugin. But I'm strongly missing foreign key constraints and better DB-level data validation than CouchDB's design docs provide.

- ## [Offline-First Database Comparison | Hacker News_202110](https://news.ycombinator.com/item?id=28995268)
- The "DO offering" is a basic VPS and you host/manage the couchdb process yourself. DO does not offer a managed couchdb service. I've found couchdb to be reasonably stable and worry free.
  - The nature of pouchdb/couchdb and the design philosophy behind it makes it relatively easy to scale to additional servers. Couchdb is master-master, which is a good eventually consistent model that should help in any horizontal scaling. The base process is erlang/elixir which should scale vertically well.

- I tried to use couchdb with pouchdb. It was a mess to add the proper authentication layer over it and the fact that even the couchdb team has changed their opinions on the right way to do it was not impressive.

- I use couch and pouch frequently. For replication mostly.
I’ve copied airtable data to it in the past.
  - Recently I implemented an event store CQRS system designed to be usable offline. I considered syncing events to the client via sockets but I needed to implement diffs. So I use couch and pouch as read only side of CQRS with an append only event CouchDB. The actual data is in Postgres.
  - Authorization is tricky. I do not recommend trying to do document level access control. I simply added an express endpoint that allows only reads and checks the session user for which table they can access. Then pass the request to couch.
  - Overall works really well. I recently turned off live sync for web and react native and loop over all of my databases on a set timeout interval. I had trouble with many connections at once.
- Authorization is tricky. 
  - If you're trying to do that, true. But if you simply let the user sync his data as he pleases, auth is quite easy with the library I maintain (link in my profile).

- You can use CouchDB installed on a desktop PC and tell PouchDB to use that instead of the web browser's IndexedDB for offline-first apps.

- For offline-first use PouchDB can connect directly to a CouchDB installed on your desktop PC as opposed to storing user data in your browser's built-in IndexedDB and syncing that with a Cloud based CouchDB.
- When you compare the CouchDB replication with other replication protocols, it is slow. The reason is that CouchDB supports replication with many instances at the same time. This creates big overhead in handling revision trees. Many requests have to be made all the time. You can observe that by starting the PouchDB subproject in the comparison repo. Watch the network tab in dev tools. 
  - Another problem is that CouchDB does not support Websocket replication, everything is long polling and plain http requests.
  - Other replications that only support many-clients-to-one-server are way faster. Both, on the initial load and on ongoing changes. This was the main reason why I build GraphQL replication for RxDB.

- I've used CouchDB and PouchDB on a previous project, and it was a blast. The built-in features like replication and HTTP API are great. My only regret is the limited support (at the time) for full text search and complex queries. I suppose I like joins a bit too much.. 

- ## 💡 [Offline First | Hacker News_202109](https://news.ycombinator.com/item?id=28690427)
- in the last major RxDB release I abstracted the underlaying pouchdb in a way that it can be swapped out for a different storage engine. 

- 👉🏻 Offline first is a dream to me, I build a big note-taking app (midinote.me) which is 100% offline, but now the biggest pain point is the full text search, yes, we can use DB like this and PouchDB to store data, 
  - but currently, there isn't a good solution for full text search in javascript, 
  - I tried lunr.js the performance is poor, and researched FTS by sqlite, it don't support Chinese, I ever considered pack the lucene (on JVM) with Electron.js( the desktop wrap on JS) on desktop, 
  - I'm not sure it is a good idea, now I am going to re-think all these things, and considering give up offline and switch to server side full text search, it will save huge effort comparing to client-side search!
- Just spitballing(不假思索地发言) here: maybe there’s a way to use Redis (and RediSearch) compiled to WebAssembly and then use it on client side?

- You can do offline first by installing CouchDB on the client side and using that to store user data. This only works on a desktop PC right now but for some apps that's a much better approach.
  - Using CouchDB with PouchDB.js provides a "Live Sync" option that syncs data both ways and that feature works very well with the apps I've made which do not have 1000s of users accessing the same DB. In my case there are probably not more than a dozen users accessing the same DB. And in my case there is not much chance more than one user is modifying a document at any given time.

- I only have two pain points with a CouchDB/PouchDB setup:
  1. Technically, a user could post some garbage into his database after obtaining a session token. Design docs can help, but still cause overhead.
  2. Only the "one database per user" approach properly ensures that each user can only access his private stuff. But then, querying information across users always requires to write some script that fetches the info from each database and aggregates them - instead of making one simple query.

- CouchDB / PouchDB(the JS compatible cousin) make use of a global sequence counter to track which documents have changed between sync.
  - Syncing is then a process of looking up the last read sequence counter from a checkpoint document (i.e. what was the last modification) and passing that sequence counter to the changes endpoint to get a list of all documents with a sequence counter AFTER that, and then pulling/pushing those documents to the local/remote database, and saving the new latest sequence counter.

- I think my main problem with PouchDB and by extension CouchDB was that it seemed hard to add validation in the backend (including authentication/authorization). I remember having to build some kind of proxy that hooks into the CouchDB protocol to deny certain requests. I am pretty sure that's solved by now (or I was just asking the wrong questions back then).
  - It's possible to use the same design docs both for client- and serverside validation. They don't look pretty, but maintaining them in readable JS and deploying them via CI works fine.

- ## 👉🏻 [Local-First Web Development | Hacker News_202302](https://news.ycombinator.com/item?id=34857435)
- PouchDB does have rather expensive adapters that use memory or LocalStorage. Almost twice the size as the base package (minified).
- I really liked it, but the typical pattern of one-db-per-user with internal replication on the server was a bit difficult plan/orchestrate for shared data. I'm patiently waiting for the couchdb PR for document level access control.
  - These days I use supabase with row level security and a Vue-wrapper that can cache queries locally and update the result as the network request finishes. Works as good as pouch + couch (but naturally comes up short for queries that rely on Date.now())

- I also love CouchDB/PouchDB, but it’s quite **clunky(笨重的) to configure the security settings on a per user basis**, and many times I want to additionally transform the data before bringing it to the client. I also don’t like to be locked into directly blasting(批评，痛斥) a database with requests (sometimes it’s better to use caching). So for those reasons I keep it behind an API layer.

- ## [Time your tech stack disappointed you? - devRant](https://devrant.com/rants/1579992/pouchdb-it-promised-full-blown-crdt-functionality-so-i-decided-to-adopt-it-disap)
- PouchDB
  1. CouchDB only, so your data model is under strict regulations
  2. No server-side logic.pagination is utter mess. Server-side timestamps are utter mess. ANY server-side logic is utter mess.messed up hack required to restrict users from accessing other users’ data, otherwise you have to store all the user data in single collection. Not the most performant solution.
  3. Authorization is a mess. auth somehow works but it doesn’t set cookie. I don’t know how to get access
  4. Error logs are mess too: 
  5. No hosting solutions. No backup solutions, no infrastructure around that at all. You are tied to bare metal VPS and Ansible.
  6. Huge pile of bullshit at frontend. Doesn’t work at Incognito mode, doesn’t work at Firefox

- ## [Are partial indexes supported when passing a selector to replication?](https://github.com/pouchdb/pouchdb/issues/7342)
- No it isn’t supported. Partial indexes are only supported for querying for CouchDB not for replication.
  - It would need to be implemented in CouchDB first

- ## 🚀 [Replicache: Easy Offline-First for Existing Applications | Hacker News_202001](https://news.ycombinator.com/item?id=22173500)

- How does it compare to CouchDB/RxDb, or Gun?
- RxDB:
  - Doesn't guarantee convergence. It's up to the developer to provide a feed of deltas to the client and ensure they have the correct effect when applied to the client. This is the one of the hardest parts!
  - Provides no help with conflict resolution. Push replication just pushes the new version of each document. The server must figure out how the document differs from the stored version and what that must mean in terms of logical operations.
  - Implemented in JavaScript. Difficult to use in native apps.
- RxDB maker here. You can do conflict-resolution by subscribing to the changeFeed and when multiple versions with the same revision-height exist, you create a new version with a 'merged' document. Depending on your dataset this can be tricky and painful.

- I have been digging deep into sync for the past few months and am very interested in how this works. I am currently trying to understand automerge and delta patching trying to implement from scratch. I have looked at Gun and couch db + pouch db but both did not feel like the right answer.
- 👉🏻 Be aware that CRDTs like automerge are solving a different (and harder) problem than Replicache. **They are trying to implement convergence in an asynchronous system where there is no central authority**. 
  - Most classic web services don't have this requirement because they do in fact have a central authority -- the service itself.
  - Moreover, for web services, it is crucial that the central authority actually be authoritative. You don't want client and server state kind of gets smooshed together arbitrarily, but for the client's view of the state to be a mere suggestion - one which the server always overrides.
  - Replicache actually started out as a true CRDT and moved to its current design after extensive iteration with customers

- Using couch as your backend db ends up being a nonstarter for most applications. A distributed multitenant database is a big big thing and a hugely important technical decision. Most orgs are not going to go with couch just to get sync. 
  - The couchdb replication protocol offers no help with conflict resolution. It just tells you there was a conflict and gives you two conflicting documents. This isn't practical for most applications.
- 👉🏻 PouchDB author here, your project looks great good job.
  - I certainly agree that switching backends to CouchDB has made it hard for people to adopt Pouch/Couch. I have often considered how I could make Pouch work with arbitrary data sources, but as you well know its a tricky problem.
- The technical difference is that when you do conflict resolution with Replicache you have more information, specifically the intent of the mutations.
-  The ergonomic difference is that conflict resolution in Replicache isn't something separate that is done after-the-fact. Replicache applies mutations to the server by calling normal HTTP APIs, just with potentially old arguments. This forces developers to consider conflict resolution at the point they are writing APIs, and keeps conflict resolution code colocated with the corresponding services.

- ## [Paperwork: An open source Evernote alternative | Hacker News_201501](https://news.ycombinator.com/item?id=8942823)
- You can use PouchDB for the browser side, CouchDB for the server, and Couchbase Mobile for the eventual mobile apps. 
- Pros: 
  - offline and online; 
  - natural fit for document management; 
  - git-like revision and conflict management; 
  - simple to set up replication for backup. 
- Cons: 
  - it's fallen out of favor; 
  - nobody seems to like writing the mapreduce code for searching and views.
- PouchDB dev here. The map/reduce API is definitely a bit cumbersome, which is why we're replacing it with pouchdb-find
