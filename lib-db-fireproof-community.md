---
title: lib-db-fireproof-community
tags: [collaboration, community, crdt, fireproof]
created: 2023-12-24T10:48:12.614Z
modified: 2023-12-24T10:49:01.941Z
---

# lib-db-fireproof-community

# guide

# blogs
- [Why Verifiable CRDTs Are the Future of Web Data_201309](https://fireproof.storage/posts/why-verifiable-crdts-are-the-future-of-web-data/)
# discuss-stars
- ## 

- ## 

- ## [new test harness for the executable feature spec](https://github.com/fireproof-storage/fireproof/issues/55)
  - 

- ## 💡🤔 The meaning of the term "CRDT" is really starting to drift.
- https://twitter.com/LewisCTech/status/1719807159217844603
  - Libraries like automerge and yjs are just *implementations* that happen to be a CRDT. 
  - But the idea of a CRDT itself is much older. I've seen "proto-CRDTs" described as far back as 4 decades.
- CRDTs are just abstract data types with operations that follow some algebraic laws, that guarantee they will converge in a sensible way. That's really it. They don't need to be complicated. They don't even need to be single record - a whole DB could itself constitute a CRDT.
  - Agree. 🛋️ @CouchDB is a CRDT at the database level and at the document level. @FireproofStorge is one at the database level. Also, all Merkle-diffs are CRDTs.

- ## 💡 One of the biggest challenges in creating @FireproofStorge is that I refused to take on infrastructure operations. 
- https://twitter.com/jchris/status/1717195946822660289
  - This means the entire database has to be built to run anywhere. (It eats trash, so you don’t have to.)
  - Fireproof is like SQLite, it runs embedded in your application. This means it’s my job to make it so nobody has to worry about compiling dependencies, or making a misconfiguration that loses data.
  - I could have created a minimal backend that runs in a container or some other abstraction layer. But that is not the path of simplicity, and simplicity is one of the competitive advantages someone like me can offer.
  - Instead, the focus is on making it work with any backend from S3 to the file system to @IPFS and @partykit_io — this requires a level of focus on the storage engine that I haven’t seen in other browser databases.
  - Because we use content addressed data, our files are self-verifying. But that is only half the battle, because a database that stores files anywhere could be putting your data everywhere. I couldn’t in good conscience be writing app data to random public buckets, in the clear for anyone to read.
  - Fireproof is end-to-end encrypted by default. This means if you manage your keys correctly, it can be as secure as you want. And if you don’t know what you are doing, at least you’re not spraying clear data all over the place.
  - The result is a database that any front-end developer will feel at home with, but also lets them get work done without asking for anything from the backend team.

- 🤔 why do u choose ipfs instead of hypercore ?
  - If hypercore can shuffle binary blobs, then they work the same for Fireproof.  I started with IPFS because of the IPLD data structures, which are the center of interesting research for immutability. But that stuff is independent of the actual transport.
  - The content addressable trees and CRDTs that come from @mikeal , @_alanshaw and friends are at the forefront of the industry. I saw my opportunity to package that fundamental advancement for the masses.
# discuss
- ## 

- ## 

- ## 🛋️ As someone coming from databases like HCL Notes/Domino or CouchDB, Fireproof looks pretty familiar and powerful. _202312
- https://discord.com/channels/1142273421674303619/1142286889588629604/1191037240873320568
  - All three have concepts of changes feeds that can be leveraged to incrementally update external indexes. 
  - What I don't find in the Fireproof docs is how deletions get reported in the changes callback. We need those to remove entries from the external index.
  - And I am curious what indexers you have in mind for persistent views of data, e.g. to keep b-trees with selected doc data persistent on disk and to have flexible queries for fast index-optimized filtering/sorting. 
  - We could mirror Fireproof doc data in Sqlite for that and use SQL for queries, but maybe you found another package/approach, something with a query planner that picks indexes if needed/available. 
  - The database.query method seems to run the JS function on each DB document, which probably is too slow for large amounts of docs (e.g. when syncing a whole CRM system to the client).
- there is a config flag to persist the indexes so they are incremental on page reload, I haven't been documenting the fine-grained config b/c I hope to normalize it before we move out of beta. You can try the `persistIndexes` option, which should add incrementalism 
  - currently we tombstone for deletes, and there are a couple of loose ends as the underlying CRDT is adding more advanced delete support, which we'll be able to use in our index manager
  - Your idea of using SQLite as a specialized index is a great one for folks who are happy to take on that dependency. 
  - My goal with Fireproof will be to hone(使更锋利) the implementation to a simple as possible, so the incremental indexes won't be going away, but for something with a query planner you will likely want an add-on

- Oh, didn't know that the indexes have a persistIndex option. That's already a good start to have fast data lookups in an app. I thought the current implementation was rebuilding the index on every app load. Is there also a method to delete a stored index afterwards? Then I could create them on demand (e.g. when a user resorts a grid), track when they are last used and do an auto-cleanup for indexes not used for some time.
  - Regarding deletion handling, Notes/Domino keeps so called deletion stubs in the database for some time (e.g. 3 months) so that replicating clients know that something got deleted and needs to be deleted on client side as well. A deletion stub just contains the document id and a date. After that period, deletion stubs get purged and docs coming in from clients would actually reappear on the server side during replication, but IBM (or HCL who bought the product years ago) added a DB option to prevent replicating too old data.
  - Would be great if there was a compact option for Fireproof so that deleting content eventually removes it from the database or at least just keeps a tombstone without more data in the DB (for privacy reason and to reduce the DB size). But I know nothing (yet) about the CRDT you are using.  So not sure this is possible.

- Stoked to have Lotus folks in the room! Currently compaction preserves all data, but we aren’t religious(宗教的，虔诚的) about that

- CouchDB should have focussed on the embedded use case, instead of warping the project into a clustered solution. SQLite is great as a foundation for clustered solutions, and CouchDB was also. What we did at Couchbase to scale it makes sense but the core project should have stayed with its roots, IMHO.
  - 🏘️ I think of Fireproof databases as a "unit of collaboration" so maybe you'd have one database for each collaborative doc, whiteboard, chat room, chess game, etc. And then another per-user database to track the collaborative groups of interest for that user. That's how the more complex apps I've built with it are arranged.
  - As far as filtered replication, you could have a cloud function subscribe to server database A and write a subset of records to server database B. The leaf nodes holding the document bodies get their own CIDs, so "all it would take" is implementing a unified storage mode, and you'd get deduplication across server database records despite different filters. In this case, server database B would contain pointers to a subset of records from server database A, and the user would replicate server database B. (The default encryption mode breaks the deduplication, but running it in clear mode is a step in that direction for now.)
  - My stress testing has been in the multi-writer scenario, to ensure blocks are never communicated that aren't yet available. The slow path is finding lowest common ancestor in the CRDT, so workloads that involve multi-writer concurrency are most challenging. For single writer workloads, or workloads that are paused when the merge backlog grows, the big-O is comparable to other databases.
- pouchdb style filtered replication would totally work as described above. You would need to prepare a replica to sync from, instead of filtering on the sync stream. this is because replication points to database snapshot CIDs, so you need to compute the snapshot before you can sync it
  - as far as sparse downloading, the _files feature automatically uploads files, but only downloads them on demand
  - for a gaming application, I would have multiple databases, each for its own sync channel. eg a database that is the list of available levels or worlds. Then for each world, a database that syncs on demand with the world assets. 

- Ok, but that means that for each user/data selection we need to prepare the same data on server side, duplicating the data. How do we handle incoming edits this way? Collect edits on server side from those small databases into the main one?
  - for each collaborative context, you'd have a database that's shared with those users. So in the game model above, if you had 5 players in a world together, that's one database
  - there are some intriguing possibilities that come from running a global indexer across all databases in the cloud, but those require disabling end-to-end encryption
  - or at least sharing the key with the indexer

- Our use case is a CRM database with 250.000 documents (Domino database). Years of emails from different customers, project plans, activities, appointments etc., some with file attachments. Not each user needs to have everything available locally of course.
  - that makes sense, if the data starts out in a big shared repository then you'd want to think about it like that
  - you might have to shard it by customer and then maybe also year, depending on what is a good way to precompute a syncable set. are your selection formulas materializable as a finite set of tags or are they completely dynamic?
- They are dynamic, e.g. created after 2023-01-01 or modified since 2023-01-06 
- the fireproof core database goal is to be leaner and cleaner over time, so subset sync probably turns into a cloud add-on. in your case are the selection formulas also implementing security policy, or just optimizing based on interest?
  - Only on interest. Every user could change them on their own, working like filtered replication in CouchDB. 
  - So the solution for CouchDB and probably for Fireproof is one database per user or role on the server side with preselected data.
- in Couchbase Mobile we did a cloud filter index thing called channels. this also has a degree of access control, not just interest filtering. I'm not sure I want to go this far for Fireproof, but its an interesting model
  - that channels thing could implement what you describe, by using a sync function that understands your access control schema
  - if we did a channels filter thing, technically it would look like a wrapper around the fireproof you see today. so the end user would see the filtered remote as a normal database, and the predicates would be applied in the cloud for hydrating it. In the long run those cloud copies can be more like indexes instead of replicas, which will cut down on the storage duplication

- ## 🚀 fireproof.storage Light up your data!_202303
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
