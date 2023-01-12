---
title: lib-collab-crdt-community
tags: [collaboration, community, crdt]
created: 2022-04-05T13:25:19.939Z
modified: 2022-04-05T13:25:40.892Z
---

# lib-collab-crdt-community

# discuss

- ## 

- ## Most CRDTs are optimized for text editing which isn't really our primary usecase.
- https://twitter.com/zack_overflow/status/1603402929586769925
  - Also most let you express dynamic JSON structures, but when you have a fixed type/structure there's a missed optimization opportunity
  - This journey was inspired by these awesome responses from josephg and @nathansobo when I asked about CRDTs on HN. They basically said CRDTs were simple/elegant, but the hard part was optimizing them.
- The crdts are written in Rust & compiled to Wasm, which is ok but im still evaluating the approach

- Ah yeah, I’ve been building out fixed-type json crdts. :) There’s some nice optimisations in the space!
  - https://github.com/siliconjungle/simple-fixed-json-crdt
  - Using fixed-type json-crdts on the server is incredibly performant if you flatten the hierarchy.
  - You don't actually need a JSON representation of the data, you just need to know which value is at each index.

- ## Or simply “conflict resolution algorithm”? Maybe a data structure API is just one (kinda object-oriented) way of thinking about conflict resolution, and we could also envisage other APIs that allow replicas to converge?
- https://twitter.com/martinkl/status/1504888983851053058
- The object-oriented concept is exactly what I would like to describe because I feel the term CRDT is misused (or at least very Confusing).

- ## An example of how to build a todo list app using state-based CRDTs.
- https://twitter.com/JungleSilicon/status/1576015894618451968
- A CRDT is just a data structure that is replicable across many different devices, regardless of the order in which operations arrive. (Doesn't rely on a centralised server for ordering). In this you can infer what has been deleted too.
  - In this implementation, to infer what has been deleted you need to store a latest seq per agent who has modified the document.
- Ah so your implementation is kind of history-based? You can delete the document but you still need to store the delete operation right?
  - Yes, but the history gets dropped over time. So say you delete something, everybody agrees, and the delete op stays the last one. The cached version is already deleted. Someday you'll drop the delete op too, and all trace of the doc is gone.
- If one of the people who've made an edit never comes back online, does that op stay forever? Or is it time / operation based where after a certain amount of time / operations has passed old changes are no longer valid?
  - Eventually the server decides to forget clients if they don't connect and forces them to drop local changes and reset on reconnect.
- I wonder why you store last timestamp for each replicaId. If you don't care about p2p, shouldn't storing: 
  - last timestamp on server by userid, and 
  - last timestamp on client 
  - On client is enough?

- ## A thread on practical local-first + multiplayer app development. 
- https://twitter.com/AdventureBeard/status/1510668678538309634
  - A challenging part of CRDT-powered apps is backward compat when updating. 
  - Your app needs to safely migrate outdated clients with stale data when the schema changes.
  - But it's not that easy. You have to consider what happens when multiple clients try to migrate the same data at the same time, or at different times, or when an old client encounters the new data. True offline + multiplayer is amazing UX, but it has tradeoffs.
- An error in your migration code can use your multiplayer features against you--virally propagating corrupted data to other clients. Without tests, data validation, and recovery (that's also offline-tolerant and subject to the above caveats), things can get nasty!
- Defensive tests, idempotent operations, and aggressive data validation are key. If you're using something like Yjs by @kevin_jahns , building a domain-aware wrapper around your Yjs code is important to standardize your operations and avoid mistakes.
- Mobile devs are probably familiar with some of this--mobile apps can have sqlite databases that need to be jostled around during app updates. That said, the Android/iOS/sqlite ecosystems have tools for making this easier.
- It's early for CRDT libraries and Yjs in particular, but helpful tools are already appearing. I don't think anyone's tackled complex data migration yet, but there are some great wrapper libraries:  SyncedStore by @yousefED , and immer-yjs by sep2 on Github seem really useful.
