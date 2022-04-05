---
title: lib-collab-crdt-community
tags: [collaboration, community, crdt]
created: '2022-04-05T13:25:19.939Z'
modified: '2022-04-05T13:25:40.892Z'
---

# lib-collab-crdt-community

# discuss

- ## 

- ## 

- ## 

- ## 

- ## A thread on practical local-first + multiplayer app development. 
- https://twitter.com/AdventureBeard/status/1510668678538309634
  - A challenging part of CRDT-powered apps is backward compat when updating. 
  - Your app needs to safely migrate outdated clients with stale data when the schema changes.
  - But it's not that easy. You have to consider what happens when multiple clients try to migrate the same data at the same time, or at different times, or when an old client encounters the new data. True offline + multiplayer is amazing UX, but it has tradeoffs.
- An error in your migration code can use your multiplayer features against you--virally propagating corrupted data to other clients. Without tests, data validation, and recovery (that's also offline-tolerant and subject to the above caveats), things can get nasty!
- Defensive tests, idempotent operations, and aggressive data validation are key. If you're using something like Yjs by @kevin_jahns , building a domain-aware wrapper around your Yjs code is important to standardize your operations and avoid mistakes.
- Mobile devs are probably familiar with some of this--mobile apps can have sqlite databases that need to be jostled around during app updates. That said, the Android/iOS/sqlite ecosystems have tools for making this easier.
- It's early for CRDT libraries and Yjs in particular, but helpful tools are already appearing. I don't think anyone's tackled complex data migration yet, but there are some great wrapper libraries:  SyncedStore by @yousefED , and immer-yjs by sep2 on Github seem really useful.
