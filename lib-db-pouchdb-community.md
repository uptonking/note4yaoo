---
title: lib-db-pouchdb-community
tags: [community, pouchdb]
created: 2023-10-07T17:28:56.496Z
modified: 2023-10-29T02:23:48.086Z
---

# lib-db-pouchdb-community

# guide

# discuss-stars
- ## 

- ## 

- ## [Store incremental data for views · pouchdb/pouchdb_201208](https://github.com/pouchdb/pouchdb/issues/99)

- [Persisted indexes for map/reduce_201403](https://github.com/pouchdb/pouchdb/issues/1658)
- 
- 

- [cache queries_201401](https://github.com/pouchdb/mapreduce/issues/12)
  - currently all non-http queries are done from scratch each time, we could save the result from the map query to a _local document and the sequence number, subsequent queries to avoid having to iterate through the whole database, we could even listen to the changes feed and update cache every time a document is created/updated.
  - After three months of debate and about a half-dozen false starts, we finally figured it out. 

- ## [Local-first software: You own your data, in spite of the cloud (2019) | Hacker News_202310](https://news.ycombinator.com/item?id=37743517)
- Couchdb/pouchdb remains one of the best: it's super easy to setup and is production-ready, but it's gonna be json docs with no transactions, so it can be limiting.
  - Y.js and automerge emerged as solutions combining CRDTs and content transfer, they look really promising. There is a Y.rs version if that's better for you.
  - I feel like you're not really interested in full p2p but want some centralization point to manage some auth stuff, so I'd investigate couchdb/pouchdb first.

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

- 🆚️ How does it differ from Pouch?
  - One of the stand-out use cases for this is adding features to Web3 style link in profile pages. Because if you’re deploying HTML that has its content hash in a block chain somewhere, and the html contains the root hash of your database. Merkle!

- ## [What Is JSON Patch? | Hacker News_202205](https://news.ycombinator.com/item?id=31301627)
- Last year I experimented with an app architecture that used CouchDB/PouchDB for for synchronising data for a single user, multi device app. Then using Yjs to merge the conflicting edits - it worked incredible well. If I had the time, I would love to build a Yjs/CRDT native CouchDB like database that could use the Yjs state vectors as a wire protocol for syncing…
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

- 🆚️ Do you mind me asking why you choose to use PouchDB in this way instead of Realm for React Native?
  - 1) Realm works only in React Native and not in React web. This has paid off in the prototype mode because it allowed us to build some simple reports in our web product.
  - 2) Realm was very new and I felt we were already using too many new frameworks. 
  - 3) On the server side, CouchDB has Futon to simplify our learning curve and give us a basic GUI to have a sanity check when our code wasn't functioning as expected. Not sure what Realm's server side looks like.
- Realm looks very promising, but the lack of a version that can run in the browser is also why I had to cross it off my list of potential DBs for the project I'm working on.
- We opted to use Realm instead because it offers encrypted storage exposed to React-Native. Would have loved to use *ouchDB but this was a missing critical piece.
- 1. Realm on the server/sync is closed beta at the moment. It's not ready. 
  - 2. Realms design does not gel well if you use Redux architecture.

- 🆚️ Did you also consider Couchbase Lite?
  - I've used pouch on a few projects and also attempted to use cb lite. I found pouch dramatically easier to get up and running with.
  - Cb lite was complicated since it needs a native plugin rather than being just js. That wasn't too bad.
  - The thing that put the nail in it for me was all the setup on the server side with sync gateways, multiple databases that then sync with one another, etc etc.
- I explored using Couchbase Lite in an app and realized that PouchDB was still the best client library for it, and at least in my testing of Couchbase Lite's Cordova plugin I saw a bunch of bugs 
  - and didn't see much in the way of a performance benefit on even iOS/Android over PouchDB's performance with IndexedDB and/or SQLite.

- 🌰 We've been running PouchDB in production for ~15 months now. We chose it because it was a greenfield project and it gave us 2 things: Easy offline support and real-time syncing that makes it easy to create collaboration a-la Google Docs.
  - In terms of architecture we have about 250 tenants with separate Couch databases per each. We're still running Couch 1.6. We have yet to evaluate Couch 2.0.
- we had to tackle few interesting problems that came along
  1. Load times. Once you get over certain db size the initial load time from clean slate takes ages due to PouchDB being super chatty. I'm talking about 15-30 mins to do initial sync of 20-30mb database. We had to resort to pouch-dump to produce dump files periodically. That helped a lot. I think this issue has been rectified with Couch 2.0 and sync protocol update.
  2. Browser limits. Once we hit the inherent capacity of some browsers (namely Safari on iOS, 50mb) we had to get creative. Now we're running 2 CouchDB databases for each tenant where 1 has full data and the other only contains last 7-8 days. Pouch syncs to the latter one. We run filtered replications between the full db and the reduced db and do periodic purging. On the client side if a customer tries to go back more than 7 days we just use the Pouch in online only mode where it acts as a client library to remote couch and doesn't sync locally.
  3. Dealing with conflicts. This might matter or it might not depending on the domain but you have to be aware of data conflicts. Because CouchDB/PouchDb is eventually consistent multi-master setup and you will get data conflicts where people update the same entity based on the same source revision. PouchDB has nice hooks to let you deal with this but you have to architect for it.
  4. Custom back-end logic. Because Pouch talks directly to Couch you can't exactly execute custom back-end logic when needed. We had to introduce a REST back-channel to make sure our back-end runs extra logic when needed.
  5. We had some nasty one-off surprises. Last one was with an object that had 1700 or so revisions in couch and once it synced to PouchDB it would crash the Chrome tab in a matter of seconds. Due to the way PouchDB stores revision tree (lot's of nested arrays), Chrome would choke during `JSON.parse()` call and eat up memory until crash. We resolved this one by reducing the revision history limit that is kept.
- That chattiness is what has driven me away from Pouch, sadly. It's a flaw in the Couch replication protocol design that won't be fixed until the spec is changed.
  - The chattiness is mostly addressed with _bulk_get in CouchDB 2.0 - Pouch will automatically use it if the server supports it. Another option is to stick a HTTP/2 proxy in front of your CouchDB instance - the chatter to the db is ultimately still there but it significantly reduces the latency cost to the PouchDB client. There are plans to add first class HTTP/2 support to Couch but for remote client architectures just adding a proxy should be a significant improvement.
- nested recision tree: I think Nolan ended up writing a non recursive JSON parser to deal with this and there was some debate about whether it made sense to be used as it was significantly slower (though could handle deeply nested structures)
  - Yup, exactly. We use `JSON.parse` inside of a try/catch and then fall back to `vuvuzela` which is a non-recursive JSON parser in cases of stack overflows
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

- 🆚️ what's the benefit of using PouchDB as opposed to vanilla localStorage functionality?
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
  - You can also explore `pouchdb-replication-stream` to build bundles that PouchDB can bootstrap from a little bit faster than a chatty replication.
  - That said, I've found initial replications of large databases (one I've worked with this week is a 25+ MB CouchDB database full of photos) is **quick enough** (and mostly bandwidth constrained) that I haven't had much in the way of concern over it.

- ## [Show HN: PouchDB - The JavaScript database that syncs | Hacker News_201307](https://news.ycombinator.com/item?id=6044892)
- 🤔 How does authentication with the Couch server work, though? 
  - CouchDB had some quirks related to user accounts as it has the added burden of trying to be an application server as well as a database server.
  - With PouchDB a lot of the application server logic doesnt apply and you can use CouchDB as a private data server that requires any connection to be authenticated, in the example we use basic auth but other methods are available and none of the security quirks with 'couchapps' apply.
- 🤔 How do I keep one user from accessing another user's data?
  - By giving each user their own database
  - You can configure databases to require the correct user to authenticate before touching it.
- Sadly it's not possible to have CouchDB make that happen for you! You can very easily allow unauthenticated requests to create users, but there's no way to create those per-user databases without writing some trusted code that runs separately from CouchDB.

- I especially like PouchDB-Server as a mini CouchDB replacement
- In the browser PouchDB will store its data in IndexedDB or WebSQL, in node its LevelDB, with the HTTP adapter you can use any product that implements the CouchDB HTTP Api protocol, currently this is CouchDB, Cloudant, PouchDB-Server and Couchbase Lite (previously TouchDB)
  - The important part is that it can only sync with a backend that implements the same replication protocol.

- 🤔 Can PouchDB sync with MySQL / my current non CouchDB database?
  - No, the data model of your application has a lot of impact on its ability to sync, relational data with the existence of transactions make this harder. It may be possible given some tradeoffs but right now we are focussing on making PouchDB <-> (PouchDB / CouchDB) sync as reliable and easy to use as possible.

- I'm not too familiar with Couch, but as I understand it caches views and updates them. Does Pouch do something similar, or does the query function filter all the documents in the database?
  - Currently PouchDB views do a full table scan, there is an open bug to do incremental views more inline with CouchDB

- Its not really like cassandra, which has functionality aimed towards managing and querying huge volumes of data. 
  - The main feature here is the syncing, which is reasonably unique to the CouchDB world

- PouchDB is the database, you never need to be online to use it and it isnt queuing writes, its doing them locally. 
  - The ability to sync is to let you use the same data across various devices.
# discuss-search
- ## 

- ## 

- ## 
# discuss-mvcc-concurrency
- ## 

- ## 

- ## [Possible to write local doc without knowing rev?_201803](https://github.com/pouchdb/pouchdb/issues/7139)
- local docs are a bit weird, we don't do all the MVCC stuff for them

- ## [use a bloomfilter for idb_201502](https://github.com/pouchdb/pouchdb/pull/3485)
- _local docs do not have MVCC and are not replicated around a
cluster. If you write two copies simultaneously then I think it will be
last write wins (which might not be the same as last request wins). This
actually might cause some strange behaviour in a cluster (a discussion for
#couchdb-dev) but my understanding is that's how it's worked in Cloudant
forever...

- ## [Read/Write Consistency_201401](https://github.com/pouchdb/pouchdb/issues/1249)
- My concurrency issue was that we read data and write it from/to leveljs. there is no transaction around that or mvcc mechanism so I dont know anyway in which it cant be broken, ie 2 writes, both read the same metadata, last write overwrites first's data
  - to be honest I am really surprised it hasnt come up, so its possible I am missing something, but I just assumed the way we write our tests didnt expose it. Our Indexeddb (or websql) implementation does not have this issue

- ## [Create conflicting documents?_201407](https://github.com/pouchdb/pouchdb/issues/2486)
- We do not support all_or_nothing, and it's definitely going away in Couch 2.0, so it's not what you want.
  - If you are making frequent changes to a document, you will want to upsert instead. I.e. you keep trying to PUT, catching 409s and repeating the GET/PUT as necessary.
  - Once thing you should know about this, though, is that if you are generating a new document for every keystroke, your history is going to grow very quickly unless you turn on auto-compaction. And auto-compaction will slow down your database, 💡 so as an alternative, you may just want to **use `setInterval` to occasionally update, rather than updating for every single keystroke**.

- ## 🔀 [Transaction control feature request_201311](https://github.com/pouchdb/pouchdb/issues/1013)
  - Since Pouch can use a single thread and the underlying database supports transaction control I think it might be feasible.

- Not all of our underlying storage protocols support transactions, we also lean towards not implementing things that CouchDB cant support so we get a symmetrical API
  - I would definitely love transaction support, but I feel like this may be a while away

- CouchDB's all_or_nothing, if its not already taken out, most definitely will be with the bigcouch merge

- This cant be implemented

- ## 🔀 [Transaction control_201310](https://github.com/pouchdb/pouchdb/issues/954)
- Couchdb doesn't support transactions and it's architecture prevents this. but I assume there's no reason pouchdb can't support them. Though there are workarounds it would be amazing if pouch could support them.
  - PouchDB is supposed to be backend independent, so the backend may be CouchDB (or indexedDB) and the users should not have to worry about the difference, introducing this would break that assumption.
  - I would like to see alternative apis that do support things like transactions, but it would be too big a change from what PouchDB already does

# discuss-auth
- ## 

- ## 

- ## 

- ## [Yet Another Database Design question (pouchdb and couchdb) : CouchDB](https://www.reddit.com/r/CouchDB/comments/119s2q8/yet_another_database_design_question_pouchdb_and/)
- So there’s some thing called design-docs & filters in couchdb.
  - So based on the role of user you can select which documents to sync…

# discuss
- ## 

- ## 

- ## [Level.js concerns](https://github.com/pouchdb/pouchdb/issues/1678)

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
  3. Personally I feel that the naming/marketing of the product is poor. It does not feel professional ( couch, futon, fauxton, pouch, couchbase) do not feel like professional grade products I can depend on to run a business.

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

- ## [PouchDB, the In-Browser Database That Replicates | Hacker News_201310](https://news.ycombinator.com/item?id=6611745)
- 🤔 How does this handle security? Sending data directly into a database from the browser with no application layer sounds a bit scary.
  - PouchDB is optimized for the use case of one database per user, a logged in user has full access to a specific database that only they have access to (for shared data access you can use replication on the server side)
- Think of it like this:
  1. Any application layer is in effect a transform, with security and sanity constraints, on user input.
  2. There is at least the degenerate case where user input does not need to be transformed, only constrained
  3. And about those constraints. CouchDB requires you write a validation function, and it lives inside the database, again obviating(消除) the need for that logic in the application layer.
  4. What was your anxiety again?
- It's supposed to be used with one db per user for a subset of data I think, in which case security would not matter much.
- If you look at their demo code it has a username and password right in the javascript source - as you would expect - which means keen users could do all kinds of things.
  - Aye, which is why putting your administrative credentials in client-side JavaScript is an unspeakably bad idea.
  - Instead, serve {client, user}-specific keys from the server on request, or let the user generate them through a signin process in the frontend, say by using the _users database that CouchDB and Cloudant allow.
- And this is why your database server needs row-level security
- it can work with cookie authentication with just a little more lines of code.

- Does it store data serialized or in object form? I am not sure how JS reacts to a few millions objects.
  - It stored plain objects, they are persisted to disk so memory shouldnt really be a concern, it uses idb in firefox / chrome, websql in others (or leveldb in node)

- ## [PouchDB (Portable CouchDB JavaScript implementation) | Hacker News_201108](https://news.ycombinator.com/item?id=2866447)
- to implement a couch you need a key/value store with transactions so you can atomically update the by-sequence index and the key/value storage simultaneously. 
  - pouch is neat because it does this in your browser (or on top of any leveldb) so that you can replicate and sync databases anywhere you can run pouch. 
  - i'd love to see more databases implement replication but sadly not many database developers think to store by-sequence indexes or expose their databases over http
- Yes and no. The most important part of replication is to have an algorithm that's capable of merging two document histories that are not identical. 
  - This core bit of CouchDB is quite important and often overlooked in terms of its replication scheme. 
  - Randal Leeds is currently hacking this into PouchDB and I'm quite excited to see the algorithm in a non-functional language so that more people can see its simplicity without worrying about learning a new programming paradigm.
  - On the other hand the atomic update of the two indexes is quite important for efficient replication. Without the atomic update of a by-update-sequence index it would require a full table scan for each replication. Its definitely a necessary optimization, but not a sufficient optimization. The per-doc revision history merging is the special sauce that makes things work.

- I would go so far as to "bypass" the spec of CouchDB -- at least for Pouch -- by doing a sort of auto-compaction, clearing out the database of the previous revision at storage time, and only storing the latest revision. 
  - This doesn't stop you from doing an effective merge, it simply stops the original notion of Couch having multiple branches of the same document. Again, in the browser, to sacrifice indexedDB space, I think that's an okay step to take.
  - The real win will be when a WebWorker is able to run through a view and automatically add the results of that to a separate dbspace. It looks like viewQuery is the beginnings of that.
