---
title: lib-db-pouchdb-community-stars
tags: [community, pouchdb]
created: 2023-12-06T15:58:40.413Z
modified: 2023-12-06T15:59:01.332Z
---

# lib-db-pouchdb-community-stars

# guide

# discuss-stars
- ## 

- ## 🔁 how would you implement "undo" using RxDB? 
- https://discord.com/channels/969553741705539624/1148193932744867890
  - E.g. a user performs an action which triggers query/queries. Then they click an "undo" button, which should revert the changes from those queries
- I do not think this is rxdb specific. The thing is that between the original action and the undo, another user might have updated the documents.
  - ou could somehow remember all changes and their post-write _revision value. Then on undo you can check all documents and then undo them if the revision is still the same (=not changed by another user)
  - Just for info, Cross-document transactions are not possible in rxdb, that is intentional.

- 🧐 Changes themself are not stored in rxdb. This was the case with pouchdb/couchdb but it is too much of a performance burden for a client side database. Only the latest state of a document is stored.
  - You can access the revision value from the metadata of a RxDocument like doc.toJSON(true)._rev
  - Did you have a look at the CRDT plugin? This stores all operations of a document in a crdt-list. You could modify that to flag each crdt-operation and "revert" it by removing the operation from each document. 

- ## I want pouchdb to replicate ‘as-needed’, AKA to use pouchdb as a ‘read-through cache’. _20231024
- https://couchdb.slack.com/archives/C016TJAE7A4/p1698079241868579?thread_ts=1698040668.376679&cid=C016TJAE7A4
  - Although full replication works like a charm, it’s a heavy requirement for mobile network users.
  - My initial thought was that I would observe what documents I query, then create a replication per query. This would ensure I always query my local DB, and I can use the changes API as a hook to re-query the local DB. This keeps source of truth nice-and-easy and I let pouchDB handle all the work. 
  - As a slight alternative, I could maintain a single replication per app, and cancel/restart it given each query, and that single replication contains all the documents of-interest to the current app state
  - I currently have full replication to the app’s local DB. I am trying to cut down on network bandwidth for mobile users. The database is large (for indexeddb).

- could you use the http adapter while the initial replication runs so your app talks to your server CouchDB and then swap to the indexeddb adapter when the replication is done?
  - that is some clever secret sauce, let me toy with that. It still doesn’t cut down on “I am replicating stuff this user may not yet need”

- If you can somehow determine the update seq of your server db after which you want all docs on the client, you can initiate the initial replication since that update seq.
  - If the changes are not contiguous, you could also create a view on the server side that returns a list of doc ids for the client to use as a doc_ids filter for the initial replication.
  - Finally you could use a filter function on the server, but that comes with a bunch of caveats, so avoid for now 
- it would be really, really cool if filtered replication (not with the functions) would accept a range of keys instead of a list of document ids like `{ startKey: 'foo_', endKey: 'bar_123'}`.
  - you could do that with a mango filter. that is not as bad as a JS filter, but also not as good as the query-a-view option
  - it’s not a mango query. just a filter function that is expressed as a mango selector

- ## what type of system architecture does PouchDB use (Embedded, Shared-Disk, Shared-Everything, Shared-Memory, or Shared-Nothing)? _201912
- https://groups.google.com/g/pouchdb/c/rj-9MX9mlGY
- If you think only of the local database and the standalone application, it is an embedded database. 
  - When you're doing replication, it's a shared-nothing, or multi-master architecture.

- ## 🆚️ pouchdb vs triplitdb _20231202
- https://discord.com/channels/1138467878623006720/1138467879113728033/1180309062169149461
  - I've been looking into offline-first in-browser DBs and PouchDB seems like the most solid option. Any opinions on it and how it compares to Triplit?

- PouchDB is pretty cool but fairly outdated at this point. There are also quite a few differences. 
- I'll just share a few things that Triplit has that Pouch doesn't 
  - 1. Schemas
  - 2. Relational Queries
  - 3. Conflict-free syncing
  - 4. First party Typescript support
- I would say 3. is there if you use the event sourcing data model, 1. is kind of a feature, 4. has gotten better, but 2. is definitely not there.
  - PouchDB is more of a lower level DB solution, however it's been there for a while, it's stable, maintained and not going anywhere, which is the most attractive point for me, the days of experimenting with alpha/beta libraries for products are behind me

- Triplit also has an schemaless mode. But yes that is true that it's had plenty of time to mature (their last blog post is from 2014) and I've enjoyed using it in the past until I ran into document conflicts

- It seems like this space is very fragmented

- ## 🆚️ [PouchDB vs. NeDB _201507](https://github.com/pouchdb/pouchdb/issues/4031)
- I dont have experience with NeDB so only making a comparison by reading the README, but from a brief look it looks like the main differences are PouchDB does synchronisation between the server and the browser, and that PouchDB was designed with the browser in mind. NeDB looks like it has a slightly more featureful querying than pouchdb-find

- 🐛 **PouchDB will definitely have overhead compared to the other databases, because it stores everything in a "revision" model where the history of every document is preserved**. (Think of it as git vs just overwriting files.) Hence it tends to have overhead, even for gets/puts.

- Personally, NeDB has become my go-to for most projects. The sole exception I've, thus far, had was an app that had 2.4 million rows of data. NeDB worked, but it created significant lag so I switched to SQLite and made calls to a backend handler for DB interaction.
  - I considered PouchDB, and it definitely looks like a better alternative for very large datasets ... but I think I'd still go with SQLite in those cases. For most things, according to the benchmarks posted by @user8614, NeDB appears to perform as well or better.

- ## 🆚️ [pouchdb vs realm _201609](https://news.ycombinator.com/item?id=12589426)
- Here are the top 3 things Realm adds in my opinion: great client-side performance, native models that are extremely easy to use, and conflict-free sync (not conflict resolution!).

- I work on PouchDB, in terms of those points:
  - "great client-side performance": PouchDB is more than fast enough for most use cases, its just a wrapper over indexedDB. (there are areas we can improve, particularly performance of map reduce / mango queries).
  - "native models that are extremely easy to use": Not sure what that means, PouchDB and CouchDB use json, its native and easy to use in JavaScript
  - "conflict-free sync (not conflict resolution!)": Certainly going to have to take a look at this, any conflict free sync protocol I have seen put a lot of limitations on how data within your application is structured but conflict resolution certainly is something that can be improved within Pouch/Couch.
  - I do think there is a bunch we can (and are) improving in PouchDB and its great to see alternatives, will be looking into this further now. But I certainly do not agree that (C|P)ouchDB are not suited for mobile <-> web sync, thats the primary use case I work on Pouch for.
- For "conflict-free sync, " according to the docs, realm appears to be last-write-wins along with a special case for deletes.(Incidentally Couch/Pouch also has a special case for deletes, but it does the opposite behavior by default – deletions lose to updates.)
  - In general, I tend to be skeptical of systems that hinge(依赖；装上铰链) on last-write-wins, but LWW is definitely a model that works in a lot of cases where you're not too concerned about the possibility of losing data, and it's also a simpler mental model for the app developer.
- 🔀 Realms approach to conflict resolution is very different from what you see in products like Couch.
  - Realm is an _object_ database, so in contrast to document databases where conflict resolution happens very coarse grained at the document level, in Realm it happens at the object level (and actually all the way down into individual properties).
  - This essentially means that the entire object graph is treated as one big CRDT, transparently handling conflict across individual objects, properties and relations.
  - When talking about ordering by time, both in the context of LWW and insertions in lists, we are talking about **vector clock time**, not necessarily device time (or though that is taken into account as well).
- LWW is a tradeoff. You'll be better off selling it as an automated-resolution option on top of manual resolution, instead of an innovation over manual resolution. (MV registers are a CRDT as well!)
- Adam from Realm. Our approach differs in building off our object database. We couple this with low-latency sync that only transmits changes and deterministic conflict resolution, making collaborative experiences really easy to build
# discuss-perf/large-data 💥
- ## 

- ## 

- ## My `db.get` is slow occasionally (3-4 seconds to return the doc). How can I optimize this?
- https://couchdb.slack.com/archives/C016TJAE7A4/p1751622772088449
  - My database contains 1307 docs , total size 1.3 MB
  - I'm using PouchDB (9.0) on my Angular app. There's a live sync with CouchDB 3.3.3.
  - db il my local database let db = new PouchDB(environment.pouchDbName + this.clientId); 

- How's your document's revision counter (number before dash in _rev) growing between requests? 
  - I'm currently able to reproduce the problem on a document that hasn't changed.

- I tried creating an empty application, or a page that only performs the get() function. In both cases, the get() function is always fast. On my pages where the application is slow, when the get() function is slow, I see an `allDocs()` request in the PouchDB debug. Is this the PouchDB <> CouchDB synchronization?
  - Please investigate where the allDocs call is coming from: that's likely the source of your slowdown. In synchronization (technically correct: two-way replication), you should see (in your network tab of dev tools) two calls to `https://dbServer/` , requests to `/${pouchDbName}${clientId}` and then just requests to `_changes` endpoint on your db.

- ## [Most performant way of range querying large PouchDB datasets - Stack Overflow](https://stackoverflow.com/questions/35023293/most-performant-way-of-range-querying-large-pouchdb-datasets)
- Which is the most performant on the two, or is there a smarter way of creating the indices? Or is there a different approach without using PouchDB at all?
  - Approach 1 - Multiple databases, one index
  - Approach 2 - One database, multiple indices

- Answering my own question as I found a solution, not using PouchDB but using YDN-DB. 
  - Using Approach 1 above with multiple databases and one indexed column (of type integer timestamp), I've reached very good performance.
  - Both writing and reading ~5000 rows takes about 300 ms. My tests showed that this approach is about 3x faster than using a compound index (Approach 2).

- nlawson(201601): As the primary author of PouchDB secondary indexes (and of pouchdb-find), I can concur(同意) that the implementation is much slower than YDN-DB/Dexie/etc. For query-heavy applications, I wouldn't recommend PouchDB secondary queries at all (at least until we make it faster
# discuss
- ## 

- ## [Idea: in-memory cache of doc ids for better performance_201405](https://github.com/pouchdb/pouchdb/issues/2227)
- Cookies don't work how you think they do.
  - More generally while I think a cache layer could be a very good idea see lru-cache for a good example of something we could use, I'd be hesitant to optimize for low document counts, a persistent database will ALWAYS be slower then an in memory one, that is the price you pay for being able to pull the plug after doing something and knowing that it's saved.
  - Back to using a cache layer, that might be doable for leveldb but with http and to a lesser extent idb and websql you're going to start having to worry about the datastore changing out from under the cache

- I think the conclusion is that this is a bad idea. For localstorage-down I'd like to move to a more robust copy-on-write btree, and for everything else users can try the memory adapter as a replicating cache, which was at least reported by one user to give small performance gains.

- ## do local docs have revision trees?
- https://couchdb.slack.com/archives/C016TJAE7A4/p1697613422859539
  - i can't see why they would need them
  - couch docs show all local docs with rev 0-1
  - pouch code shows local revs being incremented in idb and leveldown adapters from idb
- They don’t have rev trees, but IIRC we increment their _rev so we know what’s older and what’s newer

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

- 🆚️ How does it differ from Pouch?
  - One of the stand-out use cases for this is adding features to Web3 style link in profile pages. Because if you’re deploying HTML that has its content hash in a block chain somewhere, and the html contains the root hash of your database. Merkle!

- ## [What Is JSON Patch? | Hacker News_202205](https://news.ycombinator.com/item?id=31301627)
- 🌰 Last year I experimented with an app architecture that used CouchDB/PouchDB for for synchronising data for a single user, multi device app. Then using Yjs to merge the conflicting edits - it worked incredible well. If I had the time, I would love to build a Yjs/CRDT native CouchDB like database that could use the Yjs state vectors as a wire protocol for syncing…
  - This is the very rough code behind the PouchDB/Yjs datastore. Effectively each Pouch/Couch document is actually "managed" by Yjs, all changes/operations via it. It then saves the binary Yjs blob as an attachment on the Pouch document with the current Yjs state exported as JSON for the main Pouch document. This gives you all the indexing/search you get with Pouch/Couch but with automatic merging of conflicting edits.
  - 🧐 **Ultimately though I don't think PouchDB is a good platform for this**, building something that is native Yjs would be much better. If anyone is interested I would love to hear from them though!
- I'm also interested in following updates to your approach here. Something that stands out immediately to me is that reliance on binary attachments. 
  - 👉🏻 In my own CouchDB ecosystem work binary attachments have turned out to be just about the worst part of the ecosystem. 
  - PouchDB stores them pretty reliably, but every other CouchDB ecosystem database (Couchbase, Cloudant) including different versions of CouchDB itself (1.x is different from 2.x is different from 3.x in all sorts of ways) all have very different behavior when synchronizing attachments, the allowed size of attachments, the allowed types of attachments, the allowed characters in attachment names, and 😩 in general the sync protocol itself is prone(易于做某事；有做某事的倾向) to failures/timeouts with large attachments that are tough to work around because the break in the middle of replications. 
  - The number of times I've had to delete an attachment that PouchDB stored just fine to get a sync operation to complete with another server has been way too many already.
  - I've had to build bespoke(定制的) attachment sync tools because I haven't been able to rely on attachments working in the CouchDB ecosystem.
  - I've been thinking that I need to replace the CouchDB ecosystem as a whole. PouchDB is great, but the flux(一系列的变化；持续的变化) I've seen in the Apache CouchDB project and the issues I've had with the managed service providers especially Cloudant after IBM makes it really hard to recommend the ecosystem. Overall it seems unhealthy/in-decline, which is sad when the core sync infrastructure seems so nice to work with when it works

- ## 🤔🛢️ [I created PouchDB. After a year... | Hacker News](https://news.ycombinator.com/item?id=24355263)
- I created PouchDB. After a year or so I handed that project off to some great maintainers that made it much better as I had grown a little skeptical of the replication model and wanted to pursue some alternatives.
- It’s been about 10 years, much longer than I thought it would take, but I have a young project that finally realizes the ideas I had back then.
- 🧐 **Sometime after PouchDB was created I realized that it just wasn’t going to work to replicate a whole database to every client**. 
  - In fact, even a view of the database wasn’t going to work, because the developer isn’t in a position to really understand the replication profile of every user on all of their devices, you need a model that has partial, or more accurately “selective” replication based on what the application accesses in real time.
- I became convinced that the right primitives were already present in git: merkle trees. Unfortunately, git did a very poor job of surfacing those primitives for general use and I wasn’t having much luck finding the right approach myself.
- Shortly after joining Protocol Labs I realized they had already figured this out in a project called IPLD. Not long after that, I started leading the IPLD project/team and then putting together my ideal database whenever I found a free moment.
  - 🛢️ It’s very young, lots of missing features, still working on some better data-structures for indexing, but **it is very much a database that replicates the way git does and approaches indexing over a primary store the way CouchDB does, but there’s a lot more too**.
  - With these primitives we can easily **nest databases inside of other databases** (and create unified indexes over them) and we can easily extend the data types in the database to user provided types. Using some of these features it already supports streams of binary data, databases in databases, and linking between pieces of data.

- dagdb /133Star/MIT/202010/js/leveldb/git/inactive
  - https://github.com/mikeal/dagdb
  - DagDB is a portable and syncable database for the Web.
  - It can run as a distributed database in Node.js, including using AWS services as a backend.

- ## [Show HN: ElectricSQL, Postgres to SQLite active-active sync for local-first apps | Hacker News_202309](https://news.ycombinator.com/item?id=37584049)
- Conceptually sounds like this is what Firebase, Couchbase Lite, and Mongo Reach do in the NoSQL world.

- I'm looking forward to trying this out. Currently I get this functionality by using PouchDB on the client with a CouchDB sever. Then on my API server I have some janky code in a cron job to sync changes from CouchDB to PostgreSQL.
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

- 🔁 PouchDB's replication capability is interesting, but is there a way to make it **lazy load to the local DB instead of doing everything up front**? I hesitate to use it for a web project with 10+ MB of docs where it would otherwise be ideal.
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
