---
title: pm-pattern-local-first-drawbacks
tags: [drawbacks, local-first]
created: 2022-11-25T10:56:31.116Z
modified: 2022-11-25T10:58:09.770Z
---

# pm-pattern-local-first-drawbacks

# guide

# [rxdb: Downsides of Offline First](https://rxdb.info/downsides-of-offline-first.html)
- [Downsides of Offline First](https://github.com/pubkey/rxdb/blob/master/docs-src/downsides-of-offline-first.md)

## It only works with small datasets

## Browser storage is not really persistent

## There can be conflicts

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
# hackernews: Downsides of Offline First__202110
- https://news.ycombinator.com/item?id=28717848
  - https://news.ycombinator.com/from?site=rxdb.info
  - [rxdb: Downsides of Offline First](https://rxdb.info/downsides-of-offline-first.html)
- I’m a “true believer” in CRDTs, which I have some experience in. 
  - You can implement a useful CRDT for simple applications in under 100 lines if all you care about are standard database objects - like maps, sets and values. 
  - List CRDTs are where they get complicated, but most applications aren’t collaborative text editors.
  - The promise of CRDTs is that unlike most conflict resolution systems, you can layer over a crdt library and basically ignore all the implantation details. 
  - Applications should (can) mostly ignore how a CRDT works when building up the stack.
- The biggest roadblock to their use is that they’re poorly understood. Well, that and implementation maturity. 
  - Automerge-rs merged a PR the other day which brought a 5 minute benchmark run down to 2 seconds. But by bit we’re getting there.

- My biggest open question is how to design my centralized server side storage system for CRDT data. 
  - To service writes from old clients I need to retain a total history of a document, but I don’t want to force new clients to download the entire history nor do I want these big histories in my cache, so I end up wanting a hot/cold system; 
  - and building that kind of thing and dealing with the edge cases seems like more than 100 lines of code.
- It seems like the Yjs authors also recognize that CRDT storage on the server is an area to address, there was some work on a custom database in 2018, although my thinking is more about how to retrofit(改进，翻新) text CRDTs into my existing very conservative production cloud software stack than about writing to block storage.

- For prose text, what do you think about combining a document-scale CRDT, with fine-grained locking — e.g. splitting the document into a "list of lines/sentences", where lines have identity, and then only allowing one person to be modifying a given line at a time?
  - I almost thought Notion would be a good example of this, but apparently not — they actually do allow multiple users to be editing the same leaf-node content block at the same time, and so have taken on the full scope of the CRDT problem.
