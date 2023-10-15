---
title: pattern-local-first-drawbacks
tags: [drawbacks, local-first]
created: 2022-11-25T10:56:31.116Z
modified: 2023-09-13T20:24:49.401Z
---

# pattern-local-first-drawbacks

# guide

# 📝 [rxdb: Downsides of Offline First](https://rxdb.info/downsides-of-offline-first.html)
- [Downsides of Offline First](https://github.com/pubkey/rxdb/blob/master/docs-src/downsides-of-offline-first.md)

## It only works with small datasets

## Browser storage is not really persistent

## There can be conflicts

- The default in many offline first databases is a deterministic(不可抗拒的；不可逆转的) conflict resolution strategy. 
  - Both conflicting versions of the document are kept in the storage and when you query for the document, a winner is determined by comparing the hashes of the document and only the winning document is returned. 
  - Because the comparison is deterministic, all clients and servers will always pick the same winner. 
  - This kind of resolution only works when it is not that important that one of the document changes gets dropped. 
  - Because conflicts are rare, this might be a viable solution for some use cases.
- A better resolution can be applied by listening to the changestream of the database. 
  - The changestream emits an event each time a write happens to the database. 
  - The event contains information about the written document and also a flag if there is a conflicting version. 
  - For each event with a conflict, you fetch all versions for that document and create a new document that contains the winning state. 
  - With that you can implement pretty complex conflict resolution strategies, but you have to manually code it for each collection of documents.
- Instead of the solving conflict once at every client, it can be made a bit easier by solely relying on the backend. 
  - This can be done when all of your clients replicate with the same single backend server. 
  - With RxDB's Graphql Replication each client side change is sent to the server where conflicts can be resolved and the winning document can be sent back to the clients.
- Sometimes there is no way to solve a conflict with code. 
  - If your users edit text based documents or images, often only the users themselves can decide how the winning revision has to look. 
  - For these cases, you have to implement complex UI parts where the users can inspect the conflict and manage its resolution.
- You do not have to handle conflicts if they cannot happen in the first place. 
  - You can achieve that by designing a write only database where existing documents cannot be touched. 
  - Instead of storing the current state in a single document, you store all the events that lead to the current state. 
  - Sometimes called the "everything is a delta" strategy, others would call it **Event Sourcing**. 
  - Like an accountant that does not need an eraser, you append all changes and afterwards aggregate the current state at the client.
- There is this thing called conflict-free replicated data type, short CRDT. 
  - Using a CRDT library like automerge will magically solve all of your conflict problems. 
  - Until you use it in production where you observe that implementing CRDTs has basically the same complexity as implementing conflict resolution strategies.

## Realtime is a lie

- this "realtime" is not the same as in realtime computing
- Even when you run a query against the local database, there is no "real" realtime. 
  - Client side databases run on JavaScript and JavaScript runs on a single CPU that might be partially blocked because the user is running some background processes. 
  - So you can never guarantee a response deadline which violates the time constraint of realtime computing.

## Eventual consistency

## Permissions and authentication

## You have to migrate the client database

## Performance is not native

- When you create a web based offline first app, you cannot store data directly on the users filesystem. 
  - In fact there are many layers between your JavaScript code and the filesystem of the operation system.
- Let's say you insert a document in RxDB:
  - You call the RxDB API to validate and store the data
  - RxDB calls the underlying RxStorage, for example PouchDB.
  - Pouchdb calls its underlying storage adapter
  - The storage adapter calls IndexedDB
  - The browser runs its internal handling of the IndexedDB API
  - In most browsers IndexedDB is implemented on [top of SQLite](https://hackaday.com/2021/08/24/sqlite-on-the-web-absurd-sql/)
  - SQLite calls the OS to store the data in the filesystem

## Nothing is predictable

- You cannot know because people have different devices, and even equal devices have different things running in the background that slow the CPUs.
- So if your app does heavy data analytics, you might better run everything on the backend and just send the results to the client.

## There is no relational data

- I started creating RxDB many years ago and while still maintaining it, I often worked with all these other offline first databases out there. 
  - RxDB and all of these other ones, are based on some kind of document databases similar to NoSQL. 
- So why are there no real relations in offline first databases? 
  - I could answer with these arguments like how JavaScript works better with document based data, how performance is better when having no joins or even how NoSQL queries are more composable. 
- 👉🏻 But the truth is, everything is NoSQL because it makes replication easy. 
  - An SQL query that mutates data in different tables based on some selects and joins, cannot be partially replicated without breaking the client. 
  - You have foreign keys that point to other rows and if these rows are not replicated yet, you have a problem. 
  - To implement a robust replication protocol for relational data, you need some stuff like a reliable atomic clock and you have to block queries over multiple tables while a transaction replicated.
- So creating replication for an SQL offline first database is way more work than just adding some network protocols on top of PostgreSQL. 
  - It might not even be possible for clients that have no reliable clock.
# 👥 [Downsides of Offline First | Hacker News__202110](https://news.ycombinator.com/item?id=28717848)
- I’m a “true believer” in CRDTs, which I have some experience in. 
  - You can implement a useful CRDT for simple applications in under 100 lines if all you care about are standard database objects - like maps, sets and values. **List CRDTs are where they get complicated, but most applications aren’t collaborative text editors**.
  - The promise of CRDTs is that unlike most conflict resolution systems, you can layer over a crdt library and basically ignore all the implantation details. 
  - Applications should (can) mostly ignore how a CRDT works when building up the stack.
  - 👉🏻 The biggest roadblock to their use is that they’re poorly understood. Well, that and implementation maturity. 
  - Automerge-rs merged a PR the other day which brought a 5 minute benchmark run down to 2 seconds. But by bit we’re getting there.
- I agree with your assessments here - CRDT is the way forward for most applications; no user wants to fiddle with a merge UI or picking versions like with iCloud. I think RxDB’s position here is from their CouchDB lineage.
  - My biggest open question is how to design my centralized server side storage system for CRDT data. To service writes from old clients I need to retain a total history of a document, but I don’t want to force new clients to download the entire history nor do I want these big histories in my cache, so I end up wanting a hot/cold system; and building that kind of thing and dealing with the edge cases seems like more than 100 lines of code.
  - It seems like the Yjs authors also recognize that CRDT storage on the server is an area to address, there was some work on a custom database in 2018, although my thinking is more about how to retrofit(改装，对…翻新改进) text CRDTs into my existing very conservative(保守的) production cloud software stack than about writing to block storage.
- For prose text, what do you think about combining a document-scale CRDT, with fine-grained locking — e.g. splitting the document into a "list of lines/sentences", where lines have identity, and then only allowing one person to be modifying a given line at a time?
  - I almost thought Notion would be a good example of this, but apparently not — they actually do allow multiple users to be editing the same leaf-node content block at the same time, and so have taken on the full scope of the CRDT problem.

- I was also a "true believer" in CRDTs for a long time, implementing my first ones in Erlang about 9 years ago, but my opinion of where they fit has changed significantly.
  - The one issue with CRDT that I find is rarely mentioned and often ignored is the case where you've deployed these data structures that include merge logic to a set of participating nodes that you can't necessarily update at will. Think phones that people don't update
  - When you include merge logic – really any code or rules that dictate what happens when the the data of 2 or more CRDTs are merged – and you have bugs in this code running on devices you can never update, this can be a huge mess

- In an true offline-first approach with CouchDB/PouchDB, the client-side database can be considered to be main data store and the Server-Side DB could just be a backup. Or it might not be needed at all/ might only be used to migrate from one device to another.

- In practice I believe last write wins or compare last two writes is sufficient. Any thoughts on this in practice?
  - Last write wins is a simple CRDT merge type. It’s just that their are others depending on the data type. LWW might be good for an avatar photo, but not great for a counter.
