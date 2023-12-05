---
title: lib-db-triplitdb-community
tags: [community, triplitdb]
created: 2023-10-11T21:37:14.549Z
modified: 2023-10-11T21:37:25.329Z
---

# lib-db-triplitdb-community

# guide

# discuss-author
- ## 

- ## 

- ## 

- ## We’ve been spending a lot of time thinking about the best way to expose and implement relational querying in Triplit.
- https://twitter.com/triplit_dev/status/1707509447789043760
  - We’ve decided not to introduce any new concepts like “joins”, “links”, or “references”. What we settled on is devilishly simple yet powerful
  - Soon in any query, you'll be able to drop a *subquery* right in where clause next to your other filters
  - You can also arbitrarily nest subqueries to simulate traversing a graph of relations!
- I think this [nesting] is the right way. You can more easily de-compose sub-selects into their own reactive queries than if you were to introduce joins.
  - That's been a big motivation. We feel like this is the best format for both the query compiler and for users/devs

- We're working on predefining relations as subqueries in our schemas then you can just use dot notation to access them in filters
- https://twitter.com/ccorcos/status/1707809858077209070
  - This cool. In my experience, I’ve found it frustrating when APIs return denormalized formats. You end up having to renormalize things yourself and merge with all the data you already have in some kind of client side database. That’s something I never understood about graphql
- Totally agree. We're actually going to limit sub-queries to filtering/where clauses to start and only add them into selects when we have a compelling use case

- ## TriplitDB support for javascript Dates, nullable attributes and default values _202309
- https://twitter.com/triplit_dev/status/1704300302373957767
  - Triplit Client support for fetch policies
  - Triplit now supports using Javascript Dates directly in updates and inserts!

- ## one cool thing we did with Tuple DB is we made a wrapper to allow querying across multiple storage backends and dynamically scoping reads and writes to subsets of those storage layers_202308
- https://discord.com/channels/1138467878623006720/1138870969688150016/1139382908151418990
  - it can let you do cool things like database "forking"
- Interesting. You kind of lose transactional guarantees that way though. What’s your use case?
  - Yeah we tend to only write to single store at once so it's not much of a concern. But we use it to essentially create two layers where one layer is the cache of committed entities and the other layer (called "outbox") is local mutations that need to be synced. That way a rollback can just be clearing outbox storage but from a querying perspective it seems like one unified layer 

- ## Last week we open sourced our database, TriplitDB._202308
- https://twitter.com/triplit_dev/status/1689051390880989185
- Always glad to see a new triplestore on the block!

- ## Big improvements to our update API - much easier to use and less code! Under the hood we use a ES6 proxy, similar to how Immer.js works. _202308
- https://twitter.com/triplit_dev/status/1688638103164981248

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 👨🏻‍🏫 [An interactive intro to CRDTs | Hacker News_202310](https://news.ycombinator.com/item?id=37764581)
- In practice, most apps will only need Last-Writer-Wins registers and not the more complicated sequence CRDT's that you find in Y.js and Automerge.
  - We've built a auto-syncing database that uses CRDTs under the hood but never exposes them through the API. So if you want all of the benefits of CRDTs e.g. offline-first user experience, checkout our project, Triplit!
- 🤔 why didn't/don't you build Triplit on cr-sqlite?
  - We're aware of cr-sqlite and I've talked to the author, Matt, a few times. 
  - Short answer: SQLite has serious shortcomings when it comes to reactivity and we think we can be as fast as SQLite for the application-type queries we aim to support. 
  - The long answer would be about supporting all of features we don't need in SQLite and all of the quirks that come with it like having `null` as a primary key
  - We also recently came up with a relational-style querying system without joins

# discuss
- ## 

- ## 

- ## Ever wonder what it would take to make your app feel faster? Let’s speed-run optimizing a typical web app so we can see how challenging it actually is. 
- https://twitter.com/matthew_linkous/status/1724501205701783899
- You have your local database setup and you've re-implemented every endpoint on your backend server as a client-side query. You app is running seamlessly even when disconnected from the network but you still need to figure out how to sync data between the frontend and backend
- On first blush, you think all you need to do is insert data from your backend when your app starts and then read from the SQLite database exclusively, but soon you realize it's much more complicated than you thought...
- For starters, how do you even subscribe to changes on your remote database? As you unravel(解开，拆开) the challenge ahead of you you're left with more questions than answers:
  - How do you keep a schema in sync between your local and remote database? 
  - How do you rollback changes on the client when they're rejected by the server? 
  - How do you handle conflicting changes from different users?
  - Are you polling the remote database too often?

- ## 🌰 [Some notes on local-first development | Hacker News_202309](https://news.ycombinator.com/item?id=37488034)
- One common misconception with local-first, is that it's essentially local-only. 
  - But I believe the best experience is where the server and client are equally capable and only a partial set of data is stored on the client. The server still maintains authority but the client is always snappy(迅速的) when updated data or changing queries/views. 
  - We basically call this a full-stack database and we're building that at Triplit.

- 1. What to do with stale user data? What happens if a user doesn't open the app for a year? How do you handle migrations?
  - Just don't delete the old cases. Refuse to run sync if device is not on the latest schema version.
  - I can take a DB dump from 2018, migrate it, and have the app run against master, without any manual fixes.
- 2. What about data corruption? What happens if the user has a network interruption during a sync? How do you handle partial states?
  - Run the sync in a transaction.
- 3. What happens when you have merge conflicts during a sync? CRDT structures are not even close to enough for this.
  - CRDTs are probably the best we have so far, but what you should do depends on the application. You may have to ask the user to pick one of the possible resolutions. "Keep version A, version B, or both?"
- 4. What happens when the user has millions of items? How do you handle sync and storage for that?
  - Every system has practical limits. Set a soft limit to warn people about pushing the app too far. Find out who your user with a million items is. Talk to them about their use cases. Figure out if you can improve the product, maybe offer a pro/higher-priced tier.
- Mobiles are really bad with memory. iOS and Android have insane level of restrictions on how much memory an app can consume, and for good reason because most consumer mobile phones have 4-6 gbs of RAM.
  - You don't load up your entire DB into memory on the backend either. 
- You're asking very broad questions, and I know these are very simplistic answers - every product will be slightly different and face unique trade-offs.

- Query-based sync to partially replicate is an absolute must. This was a key feature with Ditto: https://www.ditto.live
- Query-based replication works when you know what the user probably wants to have in advance (e.g. a device in a warehouse needs records for that stock in that warehouse, not others). But that's still push.
  - You still need pull on demand access when a user opens any random item where we don't know in advance what they probably want (e.g. a discussion board scenario).

- Partial replication is a problem I haven't seen many people solving but it is definitely the next frontier in this space.

- 🗣️ I am the developer of RxDB, a local-first javascript database, and I made multiple apps with it and worked with many people creating local first apps. The problems you describe are basically solved.
- > What to do with stale user data?
  - Version/Schema migration in RxDB (same for IndexedDB and watermelonDB) can be done in simple javascript functions.
- > What about data corruption?
  - Offline first apps are built on the premise that internet connections drop or do not exist at all. The replication protocols are build with exact that purpose so they do not have any problems with that
- > What happens when you have merge conflicts during a sync?
  - You are right, CRDTs are not the answer for most use cases. Therefore RxDB has custom conflict handlers, which are plain javascript functions. 
- > What happens when the user has millions of items?
  - There is a limit on how much you can store on a client device. If you need to store gigabytes of data, it will just not work. You are right at that point.
- > How do you handle backups? How do you handle exports?
  - live backups; json export/import  
