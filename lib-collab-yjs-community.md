---
title: lib-collab-yjs-community
tags: [collaboration, community, yjs]
created: 2022-04-05T10:11:24.612Z
modified: 2022-04-05T10:11:40.379Z
---

# lib-collab-yjs-community

# guide

# discuss
- ## 

- ## 

- ##  I had no idea how popular yjs was compared to other folks in this space
- https://twitter.com/steveruizok/status/1673442035611717632
- Yeah yjs was miles ahead in terms of performance until the recent wave of optimisations hit. Now I think some of the other libraries are doing comparatively / outperforming in different ways but the community support still makes it the defacto for a lot of people.

- for a long time it was the only game in town that was a) fast, and b) actively maintained

- ## [Show HN: SyncedStore CRDT – build multiplayer collaborative apps for React / Vue | Hacker News_202112](https://news.ycombinator.com/item?id=29483913)
  - It's designed specifically for React, Vue, Svelte but also works with plain JS. 
  - By using Javascript Proxies, the data store looks like plain javascript objects, except that they'll now sync automatically across devices / users!
  - The API is inspired mostly by Reactive Programming libraries such as MobX (from the same author as Immer).

- ## [Modeling slate split node behavior in YJS - Yjs Community](https://discuss.yjs.dev/t/modeling-slate-split-node-behavior-in-yjs/283)
- Is there a way to perform a slate like split node operation in YJs?
  - Currently I’m modeling a split node operation by removing the 2nd part of the split text from the “origin” node and creating a new text with the removed part, but this leads to issues
- There are two answers to this:
- Answer 1: Use Y. Text
- Answer 2: There is no right solution for splitting nodes
  - Sync conflicts are resolved almost immediately. So in the unlikely case that two users really split the same node concurrently, the users will easily manage to undo one of the splits and continue working together. Shared editing cannot be implemented perfectly and it is impossible to model every intention. Most users will avoid working on the same paragraph anyway when they see the cursor location of another user. So implementing shared cursors already solves this issue.

- ## Published a small react library to make adding presence (live cursors/avatars) to multiplayer applications easy using Yjs. 
- https://twitter.com/nayajunimesh/status/1482192104503713792
  - https://codesandbox.io/s/y-presence-demo-live-avatars-65xpc

- ## Main takeaways from toying with both Yjs and Automerge_202112
- https://news.ycombinator.com/item?id=29507948

1. Extremely difficult to build backend in other programming languages than Nodejs
  - You will cry looking at source code C-binding, FFI, etc, https://github.com/yjs/y-crdt/blob/main/yffi/src/lib.rs
  - you weren't kidding - the rust port is total trash.
  - The internals are still very hot and in a state of flux, as we 1st decided to go with porting the Yjs, then leave cleaning and optimizations for 2nd step after we have something, that's compatible with existing Yjs behavior.
2. Both communities are great.
3. Watch out implementations of underline libraries. Trace lib0 libraries usage and internals in Yjs for example;JavaScript engines use UTF-16 encoding. Golang (my main backend language) is using UTF-8 ... reimplementing Yjs code in Golang with algorithms and optimization and futher scaling might become impossible for small startups.
4. Rich editing similar to Google Doc is very very complicated subject with lot of landmines
5. There's ProseMirror editor for collaborative editing. However you might not like its internals compare to Slatejs 
