---
title: lib-db-app-community-local-first-offlineable
tags: [community, database, local-first, offlineable]
created: 2023-09-22T19:27:50.280Z
modified: 2023-09-22T20:15:10.616Z
---

# lib-db-app-community-local-first-offlineable

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Re-wrote DB logic. Order of magnitude faster, order of magnitude less chatty, order of magnitude smaller payloads. 
- https://twitter.com/LewisCTech/status/1712674992100642976
  - Source of truth is now 1 dynamic array vs 3 binary search trees. 
  - Logical clock entries half the size. 
  - Still converges per CvRDT laws.
  - TL; DR thinking more, coding less works!
- Employing tiger style - design is cheap

- ## 💡💡 "The log is the DB, everything else is just a cache" lives rent-free(不收租金) in my head.
- https://twitter.com/LewisCTech/status/1712207592963854453
  - So for multi-master systems, we takes the log/DB, cache it as a set, (causal history?) , and if the causal histories (caches) are equal, it's converged.
  - If I'm wrong or unclear in my thinking or you have a paper I need to read/re-read - bring it.

- If your log is a sequence CRDT, then it'll eventually converge across multiple master. The caches are then just a pure function/reduction of the log. If the logs converge then the cache converges as well
- the append log of a db replica would have to record events in the exact (transactional) order that particular replica received them in. So I don't think they could ever converge on that level, the order would always be different. Or am I missing something?
  - Yeah I'm assuming you reorder when syncing. So each event would have a causal parent so it basically becomes eventually consistent linked list. It creates a total order but obviously won't be able to guarantee that events are ordered chronologically across replicas
  - The caches would have to be able to replay events but if it's designed to be a side-effect-free reducer then you can just use snapshots of previous states that can act like checkpoints so you don't have to regenerate from the very beginning
- Hmm. whenever people say 'log' in the context of databases, I assume append only, so no re-ordering. Should check out some WAL implementations though. Food for thought!
- Yeah conceptually it's still append-only. You can even model it so that each master maintains it's own isolated log for each other master that are literally only appended to but then it's the job of the "cache" to monitor the ends of each and rebase/replay some events when necessary
  - 👉🏻 This is the most simple implementation: @evoluhq
  - This is 100% the model I am trying to implement! appending to the end of a block of memory is snappier(snappier) than inserting it into a B-Tree.
- When you have a distributed multi-master append only log, and it can have branches, you can sync them by picking the longest branch. There, you get a blockchain

- Crdts, imo, work best when they’re based on event logs. Each node has its own append only log. All nodes agree on the same state by agreeing on how to traverse the tree of logs.

- understanding undo/redo/undo-redo logs will give you an epiphany
- Chapter 17 seems very relevant, appreciate the link had no idea this existed.
  - Happy that you find it useful! DBs are the most noble art in system programming… one you enter this rabbit hole everything is a DB
- It all started out because I wanted web apps to work offline... wtf happened to me!
- I should probably just write my own transactional append only log, right? How hard can it be..
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Show HN: Anki alternative with integrated notes and import/export | Hacker News_202106](https://news.ycombinator.com/item?id=27662266)
- can anyone tell me why anki is implemented so poorly in its core functionality? it works, but its slow, clunky, and error prone. that's the drawback for me and reason i am even willing to check out competition in this tech.
- I'm building an open source Anki clone, and lemme tell you shit's surprisingly hard. Getting syncing working without resorting to uploading entire SQLite databases is nontrivial. You're basically doing multi-master database replication... but you gotta build it yourself (there's no easy way to sync sqlite with some serverside database (ignoring firebase/couchdb/pouchdb for various technical reasons))
- I've built my own flashcard app and I ended up just syncing a journal of all your actions on a device (creating/edit cardings, evaluating them) and having all your other devices play those back to get to the "shared state". I store data using SQLite as well. It works pretty well for me.
  - you're describing "event sourcing" and it's the technique I'm using
- Yup, I'm doing event sourcing.
  - For my approach, I really just have each device append to its own journal file. I use iCloud's file storage, so I don't even have a service that I run. **Each peer device just uploads the latest version of its journal to a shared folder and downloads its peers' journals and plays back the delta as needed**.
  - I intentionally chose this architecture since I didn't want to run my own sync service. It keeps the sync system free, but iCloud can be slow. Unfortunately for me, if iCloud is slow, the app gets blamed for it.
- I am using event sourcing, and git is basically event sourcing for code

- ## 🆚️💡 [Offline-First Database Comparison | Hacker News_202110](https://news.ycombinator.com/item?id=28995268)

- So glad to see PouchDB included. We use it and have generally had a great experience! We use it with CouchDB on the backend, and Couch seems like a fantastic way to go for use cases involving syncing data between devices with an offline mode and syncing between clients. It was built from the ground up with replication in mind.
  - The nature of pouchdb/couchdb and the design philosophy behind it makes it relatively easy to scale to additional servers. Couchdb is master-master, which is a good eventually consistent model that should help in any horizontal scaling. The base process is erlang/elixir which should scale vertically well.
- I use the PouchDB/CouchDB combo for exactly the use case your describing. The query language for CouchDB leaves a little to be desired, but ultimately it has worked well for me. I'm self hosting on a digital ocean droplet.
- I use CouchDB. I love its multi-master replication capability, HTTP API and its ability to monitor for changes easily.

- 🌰 I had a really great experience building an EAV store with Datalog as the query interface on top of SQLite for embedding in native mobile apps.
  - Pros: querying complex data hierarchies was easy, and was able to skip the pain typically associated with managing a SQL schema.
- What’s the application for this? **EAV is often an anti-pattern when a schema could be defined**, but I’m actually using it as well. Our application is an end-user-defined database for mobile data collection. The EAV model in SQLite is a bit of a cognitive burden but makes offline sync and conflict resolution pretty straight forward. It’s almost a crude(简陋的；粗糙的) CRDT implementation.
- I wasn't aware that EAV is an anti-pattern in that case. Is it an efficiency thing?
  - For clarity, my design wasn't schemaless, values (can) have defined datatypes and relationships are first-class. I meant that I found adding to or modifying the schema was less cumbersome and error prone than traditional SQL schema additions or changes. I feel like SQL schema management is more suited to server-based dbs where you have tight control over the db lifecycle, which you don't when it lives on a bunch of mobile devices.
  - Totally agree with the ease of sync and conflict resolution, another strong pro.

- 🤔 Are you able to elaborate on **why you chose EAV over using something like the json1 extension of SQLite**?
- It was built on a single table that held the entity-attribute-value tuple along with some additional metadata like type information, whether or not the attribute was a pointer to another entity, and the cardinality of that relationship (one or many).
  - **Relationships were walked via self joins and the eav columns were all indexed**.
- This sounds very similar to what we’re doing and we are in the process of migrating most of the EAV models (other than the relationships) to a json1 column (Which I’d argue is still EAV just in document format). Keeping the relationship foreign keys outside of the json allows the database itself to enforce referential integrity.
  - The **difficulty with having all attributes be EAV** becomes apparent when having to do multiple joins to fetch a single record type (what would be a “table” traditionally). 
  - Although this is manageable, the **bigger difficulty** I’ve found is synchronizing deletions of records, especially if deletions/insertions are done in bulk. 
  - Rather than just 1 transaction you have to do multiple delete/insert queries to also delete/insert the attributes and the values and they should be done in a way that doesn’t break key constraints.

- You might be interested in the now defunct Mentat project from Mozilla. They made an EAV store with syncing on top of sqlite. **It ran datalog queries by translating them into sql**.

- Do you use «one database per user» model or «all users data in one db» model?
  - One database per user. And even disregarding(不顾; 忽视) the obvious inability to natively join information across tables, it still was a mess to subscribe to changes across all of them and all the other things you take for granted with a relational database. And to me, it looks like couchdb is on life support as a technology. It's a great idea and revolutionary in it's time, putting everything as documents with views, etc. But, too many gaps and unclear direction.
- Jan has actually been working on per-document access control and according to the discussion it is expected to land in CouchDB 4 
- IMHO, user databases (both CouchDB and PouchDB) are just front cache. User can mess with his data in CouchDB/PouchDB using API, so it's important to keep data in an inner database, inaccessible to user, and copy data between databases. Inner database can be a SQL database, e.g. PG with jsonb.
  - Really depends on your use case. If that's the user's data anyway, no need to put it in an inner database.
- I've actually been using Couch DB with Pouch directly to authenticate users on a small app, with a DB per user. Tbf, my app isn't all that large or complex at this stage, so I don't know if there's any overlap in what we're doing. But from your post, relational joins aside, I can't understand what's breaking for you specifically. You're offering nebulous gripes tbf, not discrete problems.

- 👉🏻 I use couch and pouch frequently. For replication mostly. I’ve copied airtable data to it in the past. 
  - Recently I implemented an event store CQRS system designed to be usable offline. I considered syncing events to the client via sockets but I needed to implement diffs. So I use couch and pouch as read only side of CQRS with an append only event CouchDB. The actual data is in Postgres. 
  - Authorization is tricky. I do not recommend trying to do document level access control. I simply added an express endpoint that allows only reads and checks the session user for which table they can access. Then pass the request to couch. 
  - Overall works really well. I recently turned off live sync for web and react native and loop over all of my databases on a set timeout interval. I had trouble with many connections at once.
- When i used it for web I hit a max of 6 simultaneous connections in chrome. I seem to recall that it was an (intended) browser limitation - but it doesn't throw any errors, so it's not very obvious. I forked the socket-pouch library and changed it a bit to sync unlimited db's over a single websocket connection. It worked like a charm (despite my messy code).

- Biggest bummer(令人不开心的事；令人失望的事) of CouchDB? If you’re not hosting it yourself, there’s only one major player in the market that I know of: IBM Cloudant.
  - That's the biggest problem my projects using Pouch/Couch are facing. 

- You can use CouchDB installed on a desktop PC and tell PouchDB to use that instead of the web browser's IndexedDB for offline-first apps. This approach gets you pretty close to native app speed.

- Last write wins is not a strategy for conflict resolution, it's a surrender. So I'm glad to hear something else apart from Pouch actually handles it. Anyone familiar with rxdb and can chime in on how they do it?
- It sounds like rxdb is built on top of pouch, so probably the same set of options with the possibility of some opinionated design or sensible defaults though I can't find anything. obvious.
  - Yes **RxDB conflict resolution is equal to PouchDBs**. At least for now, there are plans to improve from there where you have a global resoluting function instead of listening for conflicts in the changestream.

- What kind of consistency models do Offline-first databases like RxDB and PouchDB have?
  - [2.1. Introduction to Replication — Apache CouchDB® 3.3 Documentation](https://docs.couchdb.org/en/stable/replication/intro.html)

- Apparently, both android and ios tend to wipe browser/web-view local storage at random/when space is needed(?).
  - Lesson of the story, even if it isn't dependent on indexeddb, if you're looking for a local storage option for a mobile app and happen to be using a js framework with capacitor or anything that utilizes a web-view, stay away from anything that uses indexeddb. If a wipe like this were to happen post release, the chance that your app succeeds afterwards would be near 0%
- I am using RxDB with Capacitor (iOS and Android app). You can use the SQLite based pouchdb adapter with capacitor. It keeps your data and is (sometimes) faster.
- A **benefit to PouchDB over raw IndexedDB** is the great replication support and replicating everything back down in the case of one of those worst case wipes is an alright solution in some cases (but that does require managing remote data storage solutions, unfortunately).
- My biggest gripe with offline-first capability of PWAs is speed. a network roundtrip is generally faster then fetching the same information from indexeddb, and you still have to sync first because indexeddb tends to get wiped at inopportune times.
- I've used indexedDB on a couple of projects at work, while there are definitely downsides with its indexing design, limited querying options and the menagerie of fuckups by Team Fruit(TM), it works well as a local cache when our clients are out on site with their customers and all they've got is a crappy intermittent 3/4g signal.

- In my tests I actually went with plain indexed db at the end, because I wanted to make sure it's as fast as it could go. It's true that the indexeddb access is faster then a 3g signal with timeout, but that wasn't happening often enough to warrant slowing down all other requests measuribly just to speed up the rare case when this occurs. Loading from indexeddb generally took about 100-200ms, loading data over WLAN/4g from a remote server (~500km real life distance) over socket took < 50ms overall for multiple json payloads with about 200 serialized entities altogether. And doing both at the same to serve whatever finished first wasn't worth the trade for me either, as the indexeddb access isn't cheap from a energy drain perspective either. Other people might come to different conclusions depending on their challenges.

- Really? I've never used index db but to confirm your saying to fetch data from local memory is slower than network round trip?
  - The complaint was about IndexedDB access, not local memory. Folk mentioning this are usually referring to the disastrous implementation in Chrome

- IMO the principal consideration here is that these are offline/local databases for browsers and (probably?) Electron, so they are not intended to be scalable at all. If you have a progressive web app (PWA) and you need a queryable database for some reason, then you would use these. Otherwise, stick your queries behind API endpoints.
  - CouchDB is a lot more scalable than SQL databases because it has a distributed scaling model built in (just add nodes), no need to mess with read-replicate and finicky hot-failover, it all just works out of the box (Dynamo style).
- It’s more scalable in theory, and I talked its praises in a different comment, but our team has hit scaling issues with our one-user-per-database approach. It was a mess to sort out, but Cloudant support was very helpful.
  - Our major issue: we write many small documents, and we write them over every user’s database fairly frequently. And Cloudant’s default settings don’t like that with a one-user-per-database approach. In fact, they discourage anyone from the one-db-per-user approach these days
  - That blog post calls it an anti-pattern, but I would respectfully disagree. It is an absolutely great pattern to keep a native app and a web app in sync across multiple devices with intelligent conflict resolution.

- I considered to add Supabase, RethinkDB and meteor. But they are not really client side databases. They realtime stream query results from the server to the client.

- how do you manage the fact that Supabase is based on a relational db? Do you just put all fields (except the primary key) in a JSON column?
  - Personably I kinda like the fact that it’s a relational DB. The stuff you gain by having users only allowed to do certain things based on certain fields using Policies makes life a lot easier and more relaxing.

- For offline-first use PouchDB can connect directly to a CouchDB installed on your desktop PC as opposed to storing user data in your browser's built-in IndexedDB and syncing that with a Cloud based CouchDB.
  - Syncing that local CouchDB to your web based CouchDB is very fast and it's done in the background so it doesn't affect the performance of actually using the app. 
- 👉🏻 This is not true.**When you compare the CouchDB replication with other replication protocols, it is slow**. **The reason is that CouchDB supports replication with many instances at the same time**. This creates big overhead in handling revision trees. Many requests have to be made all the time. You can observe that by starting the PouchDB subproject in the comparison repo. Watch the network tab in dev tools. Another problem is that CouchDB does not support Websocket replication, everything is long polling and plain http requests.
  - Other replications that only support many-clients-to-one-server are way faster. Both, on the initial load and on ongoing changes. This was the main reason why I build GraphQL replication for RxDB.
- while I've not done benchmark studies with CouchDB I have monitored the logs to watch those syncs and we're not talking painfully "slow" in real world use. It is reliable though. 

- I've used CouchDB and PouchDB on a previous project, and it was a blast. The built-in features like replication and HTTP API are great. My only regret is the **limited support (at the time) for full text search and complex queries**.
  - Yeah although the docs claim to support things like regex-based searches, it's so horrendously slow it shouldn't even be listed as a feature.

- 🤔 What is the advantages of using one of these client side databases vs using indexeddb directly?
  - Replication, Encryption, Conflict Handling, Multi-Tab-Support, Compression, Observability and many more..
  - IndexedDB is a joke of a database. Yes, it can store data, and you can create a very simple index, so it's _technically_ a database… 
  - But its ability to express queries is borderline(几乎；差不多) useless for all but simplest use cases, it's slow, and it's very inconvenient to use. So solutions exist that range from giving IDB a simpler, more modern API, all the way to using IDB as a dumb storage medium to a fast in-memory database.

- 
- 
- 
- 
- 
