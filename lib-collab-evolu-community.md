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

- ## Today, I'm going to improve Evolu's useQuery to add some missing features from SWR.
- https://twitter.com/evoluhq/status/1635681745935773700
  - But it will be simpler because useQuery can't fail and because "Many Small Queries Are Efficient In SQLite".
