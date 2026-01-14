---
title: lib-collab-electric-sql-community
tags: [collaboration, community, electric-sql]
created: 2024-02-12T03:21:26.680Z
modified: 2024-02-12T03:22:23.769Z
---

# lib-collab-electric-sql-community

# guide

# dev

# docs
- [Event sourcing - ElectricSQL](https://electric-sql.com/docs/integrations/event-sourcing)
  - One of the key aspects of local-first software development is using event sourcing to trigger server-side / background processing.
  - ElectricSQL doesn't provide yet-another event sourcing solution. Instead it defers to existing change data capture systems that work with Postgres.
  - This section provides a summary of some of your options, including triggers, logical replication and streaming database integrations.
# discuss-stars
- ## 

- ## 

- ## 
# discuss-vendor-convex
- ## 

- ## 

- ## [Building Replicate _202601](https://robelest.com/journal/replicate-local-first)
- https://x.com/mikeysee/status/2007981002094997958
  - this is EXACTLY why its taken so long for @convex to tackle local-first!
- i'm building an AI first Notion like app, local first is not in my mind yet but I created a yjs impl for the editor that is very similar to @robelestifanos_ solution 
  - yjs deltas + sequence + periodic compaction with snapshots

# discuss-durable-stream/state
- ## 

- ## 

- ## 

- ## 

- ## ⛓️ Introducing Durable Sessions — the key pattern for collaborative AI.
- https://x.com/thruflo/status/2010826574002536905
  - this post shows how you can build Durable Sessions into your existing stack, schema and AI SDK using Durable Streams from @ElectricSQL and @TanStack DB.
  - The result is native multi-tab, multi-device, multi-user and multi-agent sessions. Built on an open protocol.
  - https://github.com/electric-sql/transport
  - You provide a single Standard Schema defining your token streaming and session state. The Durable Streams state layer takes care of the rest

- https://x.com/thruflo/status/2010830304148087121
  - If you're building AI apps on a request <> response model, you're doing it wrong. Here's looking at you: `useChat`

- ## ⚖️ Introducing the State Protocol—the first higher-level protocol built on Durable Streams. _202512
- https://x.com/ElectricSQL/status/2003606111811977492
  - Durable Streams = ordered, resumable byte delivery
  - State Protocol = insert, update, delete operations on typed entities
  - Database-style sync semantics over any durable stream.
  - The separation is intentional:
  - AI token streaming? Use Durable Streams directly—no CRUD needed
  - Real-time database sync? Add State Protocol for typed collections
  - Both in the same app? Different streams, different protocols
  - Adopt what you need.
  - State Protocol + @TanStack DB = reactive queries with incremental updates. 
  - Differential dataflow under the hood. Dramatically faster than filtering in JS.

- don't suppose there's any plans on a cloudflare / workers implementation?
  - we're only going to be maintaining the reference implementations in the repo + clients. There's a lot of potential server implementations and it'd be too much burden to maintain versions we're not using ourselves.
# discuss
- ## 

- ## 

- ## 

- ## I'm trying to figure out if Electric SQL will be able to meet my needs. _20240115
- https://discord.com/channels/933657521581858818/959469025728024586/1196476028713967626
  - Basically, I need to be able to handle "side effects" in a graceful way. For example, let's say that a user performs an action on client A which gives them 10XP, and another action on client B which gives them 20XP. I believe that syncing the state of the actions is likely trivial, but how can I make sure that the user ends up with 30XP in total, rather than 10 or 20 (which would be the case with last-write-wins). There are also other considerations, e.g. undo functionality and not awarding duplicate XP for a single action performed in multiple clients.
  - I originally planned to do this with event sourcing (without CRDTs), but now I'm wondering if CRDTs are the way to go. I'm very new to this stuff, but I haven't been able to find a concrete answer to my question anywhere online. Does anyone have insight here?

- as you're pointing out, a CRDT providing LWW semantics will end up with either 10 or 20 XP but not 30 XP (in case those 2 actions gaining 10 and 20 XP were concurrent). 
  - In order to end up with 30 XP you would need a specialised counter CRDT. 
  - 🐛 However, ElectricSQL does not have counter CRDTs, instead each value of a row is stored inside a LWW Register CRDT. 
  - To make your example work with Electric, you could store each action that leads to an increment/decrement of XP and aggregate those to get a user's total XP. e.g. have a separate "actions" table with a row per action that increments/decrement XP and then take the sum of all actions of a certain user if that makes sense?
- Indeed, that does make sense! I briefly considered it, but I'm just not sure about how scalable it would be. I don't think I'd want to sync all those actions across all clients and issue an aggregate query on each page load, so I'd probably need to cache the value on the users table anyway. Then there's some added complexity when it comes to users increasing in level as well... Perhaps that's the best solution, though it scares me a bit, hah.
- We are considering adding support for additional CRDTs. However, the road we're currently envisioning is to add support for Yjs. So, you could implement your application state as a Yjs document that is stored in Electric.
- Yjs is great for both (rich)text editing, but also any sort of JSON like data strutures. It has Map and Array CRDTs as well and XML like types for rich text. It doesn't have a counter type though. Essentially if you are considering a JSON column for storing a data structure, a Yjs document can be merged in an eventually consistent way. (JSON columns in Electric are LWR on the whole column) 
  - @thruflo suggestion of having a "compact" job is perfect, and what we are actually doing in our Yjs integration. Essentially, on a (random) interval a client merges all "update" rows into a new "update" row, and deletes those that where included in the merged row, inside a single transaction.

- ## 🤼🏻 I'm working on a system where multiple users can do increment and decrement numbers, even while offline. _20231216
- https://discord.com/channels/933657521581858818/1185429153512697876/1185429164287856640
- if you want to have a counter that supports increments and decrements even when offline and syncs when back online, have a look at how Positive Negative Counter CRDT works. In essence, you need to keep track of the number of increments and decrements per user. The actual counter value is the sum of all user’s increments minus the sum of all users decrements. 
  - Even though Electric does not have a built-in PN Counter CRDT you could manually implement something alike. e.g. Keep 2 rows per user in the DB one that counts their increments and one that counts decrements, on increment you increment the user’s row for the positive count, on decrement you increment that user’s row for the negative count.
  - The PN counter solution requires to track 2 integers per user that has interacted with the counter. Which could be represented as a row per user with a P and a N column. If you don’t do that, you will most probably encounter consistency issues as you won’t be able to reliably track all users increments/decrements and sync correctly 
  - by design the PN counter keeps 2 vectors: a P vector and an N vector whose length is the number of participants (i.e. the number of users that increment/decrement the counter).

- 🤼🏻 Adding counters to electricSQL is a question we debate internally from time to time. In SQL there is no really an increment operation. i.e. if you see x+1 is a statement you don't really know if it's an assignment or an increment.
  - So far, we've been deferring adding CRDT data types as first-class types, we're looking into integrating CRDT libraries instead.
  - You can check the checkout example, where we use event sourcing for processing orders in a store (re-stocks could be handled similarly).

- ## How do you handle absence of commands? _20231028
- https://discord.com/channels/933657521581858818/933657523049885698/1167732243855331338
  - I've been digging triggers/CDC stuff, and can't figure out how to make domain events, in an elegant way.
  - Either it's shit load of logic on CDC or unsafe events from frontend.
  - Unsafe because anyone can write some events, they will be replicated and processed, and I don't see way to secure this 

- Event sourcing in combination with the (in development) DDLX permissions system will enable secure triggering of server side functions. This is a design pattern we are going to document.
  - We are also considering various other hooks we could provide to simplify this process, but are only at the discussion stage on this.
  - Our suggested event sourcing and execution is documented here: https://electric-sql.com/docs/integrations/event-sourcing
