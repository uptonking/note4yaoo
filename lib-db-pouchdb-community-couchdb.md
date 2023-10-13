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

- ## 🚀 [PouchDB, the JavaScript Database That Syncs | Hacker News_201612](https://news.ycombinator.com/item?id=13101870)

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
- You can then create another database that replicates from all the user databases in order to perform your aggregate queries on the back end. That sounds horribly space inefficient.
  - Yep. Everything in software is a trade-off. This trades space efficiency for multi master replication with first class offline app experiences. For many cases, that's a fine trade. Disks are cheap. If that isn't a fine trade for a particularly large dataset, use a different technology that's better at space efficiency and worse at other stuff.

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

- ## 🆚️ [What is the difference between CouchDB and Couchbase? - Stack Overflow](https://stackoverflow.com/questions/5578608/what-is-the-difference-between-couchdb-and-couchbase)
- [Couchbase vs CouchDB NoSQL Systems: Difference Between Them](https://www.couchbase.com/comparing-couchbase-vs-couchdb/)
- I think CouchBase seem to be perceived as CouchDB's 'enterprise' alternative. Which in a way seem to be true. Apart from lack of ability to attach files to records ( documents) and 'out-of-box' REST endpoints compared to CouchDB, CouchBase has sql like language i.e. N1QL (sometimes pronounced a Nickel, UPDATE renamed to SQL++ in Couchbase 7.0). This is one of the reason why I don't really like / recommend using the term 'NoSQL'. I personally like term 'Non-relational'.

- ## 🆚️ [CouchDB vs. MongoDB | Hacker News_201706](https://news.ycombinator.com/item?id=14564248)
- The article is strangely outdated on the CouchDB side
  - It fails to mention that CouchDB now has Mango, which is a MongoDB-compatible query language.
  - Since 2.0, CouchDB also has Dynamo-like clustering thanks to Cloudant's open sourcing of the BigCouch code.

- Mobile support: CouchDB stands out, in that it can run on an Android or iOS mobile device. In addition to being mobile, the database can also synchronize with a remote master database, allowing the data to be shared easily between mobile devices and servers.
  - Meteor actually provides exactly this for MongoDB; it has a "minimongo" package in the browser that supports Mongo's query language, running it synchronously against an in-memory copy of the collection. And with Meteor, you can specify "subscriptions" declaratively that enable bidirectional synchronization while their owner components are in scope.

- CouchDB replication has got to be among the easiest and nicest in the industry. Setting up master/master is a breeze.

- Snapshots: Any changes to a document occur as a revision and appends the information to the file. This means you can grab a “snapshot” of the file and copy it to another location even while the database is running without having issues with corruption.
  - This is the main feature I sell when pushing CouchDB. 
  - Use it to project events and you'll see what I mean.

- ## 🔖 [CouchDB 3.0 | Hacker News_202002](https://news.ycombinator.com/item?id=22425834)
- CouchDB is awesome, full stop. While it's missing some popularity from MongoDB and having wide adoption of things like mongoose in lots of open source CMS-type projects, it wins for the (i believe) unique take on map / reduce and writing custom javascript view functions that run on every document, letting you really customize the way you can query slice and access parts of your data...

- It works very poorly as a relational DB.

- The problem I had with CouchDB is integrating it into a framework like Rails. CouchDB on its own does so much cool stuff. The "free" HTTP API and client replication via PouchDB are the two huge ones. But it just wasn't smooth enough to get the data out, use it where I wanted, and then save it back.

- Cloudant on IBM Cloud is CouchDB API/replication compatible and offers support for Apache CouchDB
- I'm really can't wait for the per-doc permissions 
- Yeah, I'm still disappointed that the MongoDB API outpaced(超过，胜过) the CouchDB Replication Protocol in general adoption. 

- That's where I fell into love with the CouchDB world. Building offline-first databases in PouchDB, and letting that sync to any HTTP address that speaks the replication protocol is sometimes a dream.
- My biggest current concern is client side search and size. 
- I've not tried quick search. For the most part in the applications I've worked on I've just relied on the main primary key index (the _id field) for most lookups.
  - The approach I've been slowly moving towards is using _local documents (which don't replicate) with attached photos in PouchDB, metadata documents that do replicate with name, date, captions, ULID, resource paths/bucket IDs 

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

- Custom backend means no synchronisation and no advantages over postgres.

- 👉🏻 You can replicate all per-user DBs into a central database today.
  - We are working on per-document-access-control at the moment, to support this use-case out of the box

- there are no changes to the replication protocol in Couch 3.0, so PouchDB already works.

- The newest version of CouchBase mobile no longer supports CouchDB as a replication target. It can still be accomplish with the CouchBase Sync Gateway, but get complicated quickly.
# discuss-sync/collab
- ## 

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

- ## [Time your tech stack disappointed you? - devRant](https://devrant.com/rants/1579992/pouchdb-it-promised-full-blown-crdt-functionality-so-i-decided-to-adopt-it-disap)
- PouchDB
  1. CouchDB only, so your data model is under strict regulations
  2. No server-side logic.pagination is utter mess. Server-side timestamps are utter mess. ANY server-side logic is utter mess.messed up hack required to restrict users from accessing other users’ data, otherwise you have to store all the user data in single collection. Not the most performant solution.
  3. Authorization is a mess. auth somehow works but it doesn’t set cookie. I don’t know how to get access
  4. Error logs are mess too: 
  6. No hosting solutions. No backup solutions, no infrastructure around that at all. You are tied to bare metal VPS and Ansible.
  7. Huge pile of bullshit at frontend. Doesn’t work at Incognito mode, doesn’t work at Firefox

- ## [Are partial indexes supported when passing a selector to replication?](https://github.com/pouchdb/pouchdb/issues/7342)
- No it isn’t supported. Partial indexes are only supported for querying for CouchDB not for replication.
  - It would need to be implemented in CouchDB first

- ## 🚀 [Replicache: Easy Offline-First for Existing Applications | Hacker News_202001](https://news.ycombinator.com/item?id=22173500)

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
- PouchDB author here, your project looks great good job.
  - I certainly agree that switching backends to CouchDB has made it hard for people to adopt Pouch/Couch. I have often considered how I could make Pouch work with arbitrary data sources, but as you well know its a tricky problem.
- The technical difference is that when you do conflict resolution with Replicache you have more information, specifically the intent of the mutations.
-  The ergonomic difference is that conflict resolution in Replicache isn't something separate that is done after-the-fact. Replicache applies mutations to the server by calling normal HTTP APIs, just with potentially old arguments. This forces developers to consider conflict resolution at the point they are writing APIs, and keeps conflict resolution code colocated with the corresponding services.

- ## [Paperwork: An open source Evernote alternative | Hacker News_201501](https://news.ycombinator.com/item?id=8942823)
- You can use PouchDB for the browser side, CouchDB for the server, and Couchbase Mobile for the eventual mobile apps. 
  - Pros: offline and online; natural fit for document management; git-like revision and conflict management; simple to set up replication for backup. 
  - Cons: it's fallen out of favor; nobody seems to like writing the mapreduce code for searching and views.
- PouchDB dev here. The map/reduce API is definitely a bit cumbersome, which is why we're replacing it with pouchdb-find
