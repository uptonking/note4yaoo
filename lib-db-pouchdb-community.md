---
title: lib-db-pouchdb-community
tags: [community, pouchdb]
created: 2023-10-07T17:28:56.496Z
modified: 2023-10-29T02:23:48.086Z
---

# lib-db-pouchdb-community

# guide

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

- ## 

- ## do local docs have revision trees?
- https://app.slack.com/client/T49P1AZRT/C016TJAE7A4
- They don’t have rev trees, but IIRC we increment their _rev so we know what’s older and what’s newer

- ## is it expected that .get() with open_revs would load every rev in a separate db transaction?  specifically looking at idb & indexeddb adapters...
- https://couchdb.slack.com/archives/C016TJAE7A4/p1697458610217519
- This might be a perf optimisation so this doesn’t  block other operations if you have a lot of open revs.
  - Happens during replication
  - Well, less perf, more not occupying transactions

- so probably deliberate?
  - Possibly, yeah. That said, I could see a more complex implementation that batches, say, up to 10 revs to get a best of both worlds
- i think indexeddb adapter stores all the revs directly in the doc. so could be big perf wins by just overriding api.get(). so N+1 db transactions would collapse to 1. sounds like if this was possible, i should see impact on replication.  perhaps in the replication perf tests
  - Totally worth a try!

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

- ## 🚀 [PouchDB, the In-Browser Database That Replicates | Hacker News_201310](https://news.ycombinator.com/item?id=6611745)
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
