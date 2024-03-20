---
title: lib-collab-crdt-blog-vendors
tags: [blog, collaboration, crdt, vendors]
created: 2023-05-30T15:50:07.368Z
modified: 2023-10-26T18:14:17.038Z
---

# lib-collab-crdt-blog-vendors

# guide

# blogs

## [Ditto Delta State CRDT](https://docs.ditto.live/javascript/common/how-it-works/crdt)

- [Extend Hybrid Logical Clock documentation](https://github.com/getditto/docs/issues/413)

- The Ditto document is a JSON like document made from a CRDT Map that represents the JSON Object. 
  - The JSON properties are map keys, and the values are any of the Counter/Register/Map types
  - One way to think about the types that make up a Ditto document is like a tree, where there are collections (Array and Map) and leaf values that are registers or counters.
  - Register: A single primitive value (Number, String, Boolean, Binary File)
  - Counter: A special number capable of preserving incrementing and decrementing semantics
  - Map: A dictionary of name->value mappings

- The foundation of determining how data should be merged is using a Ditto document's **version vector**.
  - Every time a change is made to a document, the version of that document is incremented by one. 
  - When a peer incorporates changes from other peers, the local peer can use the incoming remote peer's version vectors to determine whether the changes are new or old. 

- Each document in each peer contains a hidden metadata map of a `Site_ID` and a `HLC`. 
  - The HLC stands for a hybrid logical clock. This HLC is used to determine whether a change has "happened before".
  - Ditto uses a `UInt128` to represent the `Site_ID` and `64bit` timestamp for the `HLC`. But for educational purposes, this documentation will often use strings and numbers for readability.
- In Ditto's distributed system, the HLC is a `64-bit` timestamp comprised of `48 bits` of a physical timestamp and `16 bits` of a monotonically increasing logical clock.

## [Using Ditto as a Local Database](https://ditto.live/blog/local-database)

- you can use Ditto in your apps as a regular document database

## 🪧 [EmacsWiki: Collaborative Editing](https://www.emacswiki.org/emacs/CollaborativeEditing)

## 🪧 [jupyterlab-rtc: We can class the RTC Algorithms into 3 main categories crdt/ot/diff](https://jupyterlab-rtc.readthedocs.io/en/latest/about-rtc/algorithms.html)

- We can class the RTC Algorithms into 3 main categories:
  - CRDT category doesn’t need a central server and is used by Riak, TomTom GPS, Teletype for Atom…
  - OT category needs a central server and is used by Google Docs, Office365…
  - Diffs category used by Cocalc

## [zed: How CRDTs make multiplayer text editing part of Zed's DNA_2022212](https://zed.dev/blog/crdts)

## 📝 [supabase: `pg_crdt` - an experimental CRDT extension for Postgres_202212](https://supabase.com/blog/postgres-crdt)

- https://github.com/supabase/pg_crdt
  - pg_crdt is an experimental extension adding support for conflict-free replicated data types (CRDTs) in Postgres.
  - It supports Yjs/Yrs and Automerge.
  - **Our goal was to evaluate if we could leverage a Postgres-backed CRDT and Supabase's existing Realtime API for change-data-capture to enable development of collaborative apps on the Supabase platform**.
  - pg_crdt extension is a proof-of-concept that wraps rust's yrs and automerge libraries using the 66 framework to add a Postgres native CRDT, crdt.ydoc.

- CRDTs are a special type of data structure designed to solve a specific problem: they can merge changes in a way that the final state of the data will be the same, no matter the order in which the updates were applied.
  - In simple terms, a CRDT allows multiple users to make changes to the same data without the need for a central authority to coordinate their actions.
- I personally believe CRDTs are the future. For some things. If databases were invented today, I'm certain most of the effort would be spent developing CRDT databases or something with “offline algorithms” built-in.
- It's possible that developers will need to be selective about their “level” of offline support, at least if they plan to use an “incumbent” databases. 
  - For the cases, a simple “last write wins” strategy is probably acceptable (see the excellent Replicache and Watermelon libraries), but there will be important pieces of their application where it is not.
- pg_crdt is an extension which adds CRDT support to Postgres as a data type.
  - The `content` column is now a Yjs Doc. 
  - Updates to this column are commutative and idempotent. 
  - This means that they can be applied in any order and multiple times, and the result will always be the same.
- both Yjs and Automerge have JavaScript and Rust implementations, which means they work natively in both a browser and a Postgres environment. 

- ❓ Why not build this into Realtime?
- An alternative approach for CRDT support in Supabase is to build support directly into Realtime and use it as an Authoritative server.
  - In this scenario, Realtime would serialize the CRDT and save it to Postgres (probably as a bytea data type). 
  - Yjs has the concept of Providers which would facilitate this. 
- realtime as an authority
  - Realtime acts as the “middleman” for saving the CRDT in the database
- postgres as an authority
  - CRDT is pushed directly to the database, and Realtime receives updates from Postgres. (Note also that clients can send peer-to-peer updates.)
- If we make Realtime the authority, it strongly couples developers to the Supabase infrastructure. 
  - By placing the CRDT into the database, it simplifies the architecture, enables other tools (like Debezium), and provides the possibility to update the database directly (for semi-realtime events like counters or page-views).

- These are a few of the known limitations:
  - Realtime broadcasts database changes from the Postgres write ahead log (WAL). The WAL includes a complete copy of the the underlying data so small updates cause the entire document to broadcast to all collaborators
  - Frequently updated CRDTs produce a lot of WAL and dead tuples
  - Large CRDT types in Postgres generate significant serialization/deserialization overhead on-update.

## 👥 [Show HN: Pg_CRDT – an experimental CRDT extension for Postgres | Hacker News_202212](https://news.ycombinator.com/item?id=33931971)

- 
- 

- Just store all updates - as if you do event sourcing - ordered by a timestamp. 
  - The list of updates will eventually converge as will any function of that list, including any function that merges all the updates into a current state. 
  - You might have to [partially] reevaluate the function in case a delayed update shows up and has to be inserted into the middle of the list of updates. 
  - So I guess there are additional requirements in order to qualify as a CRDT, bounded additional space or bounded amount of computation on updates. But I don't know as it turned out my understanding of what qualifies as a good CRDT was too narrow.
- Yeah **event sourcing and what you described is what these libraries are calling delta CRDTs**. The appeal is they’re hiding away the actual event log, metadata and rebasing/merging parts and exposing data types that look something like what you’d normally use.
  - And if you tie the conflict resolution logic to the individual delta operations, you get Operational Transforms.

- 
- 

- [pg_crdt - a CRDT extension for #postgresql](https://twitter.com/kiwicopple/status/1601553881246609409) 

- The heavy-lifting is done by the teams at Yjs[0] and Automerge[1], who have re-implemented their JS libs in Rust. This made it possible for us to wrap them into a Postgres extension using pgx[2] (which is fast becoming a de-facto tool at supabase)

- Support for CRDT columns within a db to enable JSON like indexing/querying capabilities is fundamental to then building some exciting further developments. Supporting both Yjs and Automerge is exactly the right route forward.
- did you investigate querying/indexing within the documents?
  - Without the ability to index properties, or do ad-hock queries, on the documents there is little reason to to the merging in-DB. It then makes more sense to merge outside the DB and save both the raw CRDT object and a serialised JSON next to it for querying. I assume that if you had found it's performance better, indexing+querying would have been the next step?
  - Personally I find the offline + eventual consistency the most interesting use case. The ability to sync a users document set to a local db (SQLite or a future mini-pg/supabase) with local querying and then merge them back later. This could be as basic as a three column table (guid, doc, clock), the clock being a global Lamport like clock to enable syncing only changed documents.

> This could be as basic as a three column table (guid, doc, clock), the clock being a global Lamport

This would be achievable, but also perhaps quite strict - we're dictating a table structure rather than working with existing CRDT libs. That said, we could probably do this today, without any mods/extensions

> querying/indexing

Yeah, there is nothing in this implementation for that

> Without the ability to index properties, or do ad-hock queries, on the documents there is little reason to to the merging in-DB

One benefit is the ability to send "directly" to the database, but I agree that lack of additional features in the current form outweighs this benefit

> a serialised JSON

This is how we might do it with with "Realtime as an authority" approach (and is the most likely approach tbh).

- Last Writer Wins is not the most compelling use case for CRDT because if those fruits were denormalized into Postgres rows, you'd already have the behavior described. 
- In general, Sequence CRDTs seem to be the most difficult and most interesting area of continuous research. In my own work, I've implemented a sequence CRDT to create a distributed log of events across users that then (because the order is guaranteed to eventually be the same for each device) can just be reduced to whatever data structure you need. It means, we end up with one CRDT to rule them all and then can just write the "conflict resolution" in simple term with the business logic.
# more
- [Many Worlds: A Philosophy of Data Collaboration _202111](https://terminusdb.com/blog/many-worlds-a-philosophy-of-data-collaboration/)
