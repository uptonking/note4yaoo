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

- ## 

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

- ## yjs vs peritext
- https://news.ycombinator.com/item?id=29328431
- They way I see it there are two (or maybe more of a spectrum of) types of CRDT, from generic and to domain specific. 
  - Yjs actually has multiple different types, very generic types (Array and Map), slightly more specific types (XMLFragment and XMLElement), and then there is the Text type that covers both a generic plain text type but also has provision for rich formatting if needed. 
  - Peritext is basically a different method of implementing the Text type which aims to maintain a little more editor intent than Yjs currently does.
- For a full document, you need to represent both text elements with rich text formatting marks, but also block elements. With Yjs you would do this with the XMLElement type which as you would expect has attributes and can nest further XMLElements or Text within it. 
  - Peritext does not yet have support for block types.
- So, although the most common use of Yjs is for collaborative rich text editing, it can be used for many other things such as 2D/3D drawing or even gaming.

- ## Main takeaways from toying with both Yjs and Automerge_202112
- https://news.ycombinator.com/item?id=29507948

1. Extremely difficult to build backend in other programming languages than Nodejs
  - You will cry looking at source code C-binding, FFI, etc, https://github.com/yjs/y-crdt/blob/main/yffi/src/lib.rs
  - you weren't kidding - the rust port is total trash.
  - The internals are still very hot and in a state of flux, as we 1st decided to go with porting the Yjs, then leave cleaning and optimizations for 2nd step after we have something, that's compatible with existing Yjs behavior.
1. Both communities are great.
2. Watch out implementations of underline libraries. Trace lib0 libraries usage and internals in Yjs for example;JavaScript engines use UTF-16 encoding. Golang (my main backend language) is using UTF-8 ... reimplementing Yjs code in Golang with algorithms and optimization and futher scaling might become impossible for small startups.
3. Rich editing similar to Google Doc is very very complicated subject with lot of landmines
4. There's ProseMirror editor for collaborative editing. However you might not like its internals compare to Slatejs 
# automerge
- ## Automerge: A JSON-like data structure (a CRDT) that can be modified concurrently_202202
- https://news.ycombinator.com/item?id=30412550

- ## Automerge: JSON-like data structure for building collaborative apps_201802
- https://news.ycombinator.com/item?id=16309533
