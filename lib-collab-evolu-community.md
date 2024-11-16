---
title: lib-collab-evolu-community
tags: [collaboration, community, evolu, sqlite]
created: 2023-05-14T04:32:13.354Z
modified: 2023-05-14T04:32:30.696Z
---

# lib-collab-evolu-community

# guide

# discuss-authors
- ## 

- ## That's one of the reasons I'm removing Effect from Evolu right now (sorry, the new sync, you have to wait a little). _202411
- https://x.com/evoluhq/status/1856327710349369667
  - This is nothing against Effect; design patterns are proper, and the implementation, when used properly, as well). I would still recommend it for enterprise apps.
  - The low-level library is the other case. We need maximum performance. We need maximum simplicity for contributors. We need 'readable stack traces'. Last but not least, we must limit vendor locks as much as possible.
  - Personally, I would love to see Effect AOT compiled—no runtime, just code. But it's hard, of course; good things are. It took React 10 years to have its compiler. I believe the Effect will be faster.

- Low level library code that sits on the sync rendering path is one of the use cases where effect doesn't fit (even promises here would hurt). High level app code have different requirements so the tradeoffs are much better.

- Effect Compiler wouldn't really have a clear scope, stack traces are one of the things you lose using lazy code (even if using () => Promise) we recover debuggability via telemetry but the creation of runtime is an awkward spot especially in a recursive case like yours

- ## 🆚️ SQLite WASM is much slower than the in-memory better-sqlite3, but still, the new Evolu CRDT algorithm can handle approximately 1666 mutations per second
- https://x.com/evoluhq/status/1836518784539980248
  - I developed and tuned it with the in-memory better-sqlite3, where you can get around 25k mutations per second
  - Note: Don't expect that one mutation will be exactly 1 / 1666; that's not how Just in Time (JIT) compilation works. 
  - The start is always slower before it picks up speed 

- ## I completely refactored Evolu and am finally satisfied with the code structure. Why? Because of @EffectTS_ Layer._202308
- https://twitter.com/evoluhq/status/1692221690388885886
  - The Effect Layer is just a functional constructor. 
  - Now all platform dependencies are injected and hence switchable.
  - React Native full support soon

- ## ✨ introducing Evolu - React Hooks library for local-first software with end-to-end encrypted backup and sync using SQLite and CRDT._20220929
- https://twitter.com/evoluhq/status/1575478499648774145
- AbsurdSQL is dead and buggy. I had to rewrite it to wa-sqlite.

- In a few weeks, Evolu will replace wa-sqlite with the official SQLite WASM implementation and GPL-3.0 license with a much better MIT license. The API will stay the same, so you can safely develop with Evolu today._202211

- ## ✨ I've spent the last couple months quietly building a mobile app for @actualbudget , _201809
- https://twitter.com/jlongster/status/1042799826310770688
  - and more importantly, rebuilt the database layer to be syncable.
- I love the web. But I don't think a lot of people realize just how hard offline first is. There's no stop-gap, no half way solution. It either syncs up correctly or you're screwed. If you're using service workers, you better be using something like CRDTs
- To reiterate: I'm still using normal sqlite with normal tables. But I added an additional layer of CRDTs to track the order of changes which makes it easily syncable. Understand something so you can implement it yourself (don't grab a lib)! It unlocks all kinds of possibilities
- A bit different: CRDTs mean the order doesn't matter, as long as you have all of the messages. For some CRDTs, all you need is the *most recent* message per field, doesn't have to be since beginning of time. That's the case here.
- sqlite! Using CRDTs and hybrid logical clocks to generate a list of ordered changes

- 💡 why not pouchdb/couchdb? They are made for that very case. Do you use db per user?
  - db per budget, user can have multiple budgets. pouch/couch is cool but a few problems: I want centralized server so clients don't have to be online at same time. that would require centralized server having a copy of db, no go for me. my db only keeps partial changes
  - also I plan on doing end-to-end encryption, no idea of pouch/couch supports that. Most problematic though is they aren't conflict free, and conflicts happen at document level, not field level

- just using a last write wins based on whoever is more recent, "recent" being defined by a hybrid logical clock
  - That's actually not too far from what this is, but with LWW you just don't need to keep the full log. Someone else pointed out a library Logux which you should check out as well, it uses a CRDT of logs.

- ### Have you considered something like logux? How are you resolving conflicts?
- https://twitter.com/okonetchnikov/status/1042812504206991360
  - Never heard of it, at a glance tho, I don't think it's the right approach. It should only sit at the lowest-level db layer via insert/update/delete commands per item. Looks like they try to do LWW, but how does it generate `time`? I don't see anything about hybrid logical clocks
- It(logux) is something like Redux + CRDT
- Very nice! Do you implement the hybrid logical clock algorithm specifically? Looks very close. A lot of good stuff in there.
  - Yeap, own clock. I am not sure how clock will fit DBs needs, but I try to create a easy to understand clock for application level. Maybe you know sooner list of distribution time implementations? To compare different clicks and choose for your task?
- Yeap, good (hlc)clock for DB.
  - Seems like there is no idea case for every case 
  - I tried to solve, when you do not have a connection between nodes for a while and also one of client could have wrong time. (I think it is very popular case when you are making JS framework like @logux_io )
- it's all tradeoffs, but HLC with some additional checks would still work well for that. You only allow the clock to drift a certain amount (say 60 seconds) and reject messages outside of that range. client would have to start over and lose local changes, but it's their fault
  - You don't want to actually use `Date.now()`, lots of little edge cases with that. Also, CRDTs are conflict free. There are no conflicts.
# discuss
- ## 

- ## Effect reminds me of Rx. I used Rx a lot but I will not use Effect.
- https://twitter.com/gregberge_/status/1787693851320496596
  - Coupling your code to libraries like that is actually not a good idea. Universal JavaScript is better in the long term.
- Agree. I'm not writing software that requires fear of uncaught errors, and Effect.ts doesn't seem to allow me to write TS with the usual syntax, so I'll use Rust instead, which has a built in Pattern Match.
- i forget who made the take, but they said treat Effect as a different language. i agree with that take

- ## evolu Switch to the official sqlite3 WASM client with a friendly MIT license
- https://twitter.com/evoluhq/status/1622708143670042625
  - Evolu no longer uses IndexedDB for persisting sqlite3 files. Instead, it uses modern Origin-Private FileSystem (OPFS) in Chrome and good old LocalStorage in other browsers.
- The LocalStorage implementation leverages VFS, so it doesn't load and save whole files. In other words, it's fast enough. The only limit is LocalStorage max size (5MB), which is sufficient unless a lot of data are stored.
- The Origin-Private FileSystem (OPFS) is currently supported only in Chrome, but both Safari and Firefox are finishing their support. Meanwhile, Evolu is using LocalStorage.

- ## Experimental new feature: Local only tables
- https://twitter.com/evoluhq/status/1716515808182992963
  - A local-only table is a table prefixed with "_" that will never be synced—a small but handy addition. 
  - Imagine editing huge JSON. Should we store it on any change or allow the user to "commit" data later? In an ideal world, we would have CRDT abstraction for any data, and we will have, but for now, we can postpone or even cancel sync with local-only tables. 
  - Another use-case is device-only data, for example, some settings that should not be shared with other devices. 
  - Local-only tables also allow real deletion. Use the isDeleted common column and the row will be deleted instead of marked as deleted.

- ## I'm keen on adding a few things that Evolu doesn't have atm
- https://twitter.com/kndwindev/status/1663431276119085057
- Poke protocol simliar to Replicache
  - [Poke | Replicache Docs](https://doc.replicache.dev/byob/poke)
  -  WebSocket-based services are more complex to scale because they have to keep state in memory for each connected client.
  - Replicache instead uses WebSockets only to hint the client that it should pull again. No data is sent over the socket. 
  - This enables developers to build their realtime web applications in the standard stateless request/response style.
  - We refer to this WebSocket hint as a poke, to go along with push and pull. You can use any hosted WebSocket service to send pokes, such as socket.io or Pusher
- Drizzle ORM's relational queries
- Maybe even Prisma's schema generation

- ## Today, I'm going to improve Evolu's useQuery to add some missing features from SWR.
- https://twitter.com/evoluhq/status/1635681745935773700
  - But it will be simpler because useQuery can't fail and because "Many Small Queries Are Efficient In SQLite".
