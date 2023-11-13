---
title: lib-collab-crdt-community
tags: [collaboration, community, crdt]
created: 2022-04-05T13:25:19.939Z
modified: 2022-04-05T13:25:40.892Z
---

# lib-collab-crdt-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🤔 The meaning of the term "CRDT" is really starting to drift.
- https://twitter.com/LewisCTech/status/1719807159217844603
  - Libraries like automerge and yjs are just *implementations* that happen to be a CRDT. 
  - But the idea of a CRDT itself is much older. I've seen "proto-CRDTs" described as far back as 4 decades.
- CRDTs are just abstract data types with operations that follow some algebraic laws, that guarantee they will converge in a sensible way. That's really it. They don't need to be complicated. They don't even need to be single record - a whole DB could itself constitute a CRDT.
  - Agree. 🛋️ @CouchDB is a CRDT at the database level and at the document level. @FireproofStorge is one at the database level. Also, all Merkle-diffs are CRDTs.
- I've been telling myself for months I was going to sit down and actually figure out if Couch was formally a CRDT - so I'll take your word for it!
  - I think part of the lesson here is that formality matters less than the behavioral characteristics. Never throw away data, allow conflicts to be surfaced to the user.
  - Damien’s og Couch has some additional behavioral characteristics, like fairness on the changes feed and group commit, that have mechanical sympathy with the append-only implementation and the Erlang scheduler. I haven’t seen anything else quite like it. 
  - Binary attachments can be streamed in and out of the same file in parallel with write workload. And the whole code was smaller than your average Rails app.

- Same with “event sourcing.” RTS games were doing “event sourcing” 35 years ago without knowing it.
  - This was well-known architecture by ~1990.

- ## 👥 The whole idea of "conflict-free data structures for offline-capable apps" is dubious(不大可靠的；有争议的).
- https://twitter.com/msimoni/status/1719778725514883255
  - It cannot work in the general case, so you have to resort to horrors like "last write wins" if you can't resolve a conflict.
  - Much better to bite the bullet and let the user resolve conflicts.
- I don't think this post is really understanding the benefits of crdts. It isn't that they are conflict free. Nothing really is. It's that you can make them behave anywhere from automatic resolution to full user resolution depending on context.
- Would you be comfortable in using a CRDT instead of Git for your source code?
  - Yes, if anything I would feel *more* confident. 
  - Git is a *lossy* format that only shows you the state at each commit. 
  - CRDTs and OT would allow you to have a full history of every change that has ever happened (as well as snapshots at particular points in time). You could make a CRDT have the *exact same* workflow as git. 
  - If you also add event sourcing data, not only do you know *what operations* caused the changes from the first snapshot to the next, but you'd also know *what actions* a user took to create those operations.
- I'm curious, assuming you're not comfortable using CRDTs for source code, why is that?
  - Because every CRDT I've looked at mentions last write wins semantics.
- That's an implementation detail rather than something that is inherent to CRDTs. If you use multi-value registers, you can just store a full causal graph and only resolve when either a) a user chooses to, or b) business logic decides on which wins.
- I agree that for async coding (as opposed to pair programming), I'd want most of concurrent changes to be merged manually. But CRDTs could still yield better merges than git

- What do you do when you can't resolve a conflict?
  - Intelligent application design is about setting document granularity so those instances are rare. Because CRDTs never throw away data, you can always bubble conflicts to the user if it matters. In practice, I almost never see that happen.

- The most general case for this stuff is not "last write wins", it's "multi-values". As in we have multiple values for this key, the nodes have to agree on which value it is.

- One compromise is to use a git-like arch (full history, merge reviews) but store CRDT updates instead of git's patches. The CRDT enables live collaboration, and first-pass merges for non-code data (e.g. spreadsheets).

- ## So many people in the crdt & data sync space now. Feels like it is time for me to move on to the next frontier of problems
- https://twitter.com/tantaman/status/1711538960277602496
  - To be clear, I'll still be supporting my existing projects but tipping the balance further towards new research.
  - Not going away! Still supporting cr-sqlite and all my new ideas still center around what applications need from an embedded database.
- I don't think it'll be "solved" so much as a good set of opinionated defaults that work for most cases are surfacing (replicache, cr-sqlite, electric, triplit) as well as primitives for power users to compose (cr-sqlite, replicache, collabs, ?) for custom solutions.
- Low level building blocks, sure, but I haven’t seen anyone get high level DX right yet
- It's very tilted towards B2C SAAS and collaborative apps. Industrial solutions (that don't run on a phone) are what still excite me. We're still so far away.

- ## [Request for Comments: CRDTish approach to Solid - Build a Solid App - Solid Community Forum_202104](https://forum.solidproject.org/t/request-for-comments-crdtish-approach-to-solid/4211)

- ## What properties would the design of a programming language need to have to be sync / collaboration friendly?
- https://twitter.com/JungleSilicon/status/1673146654818725889
  - Which programming concepts would be best represented by tree's, lists, ranges, etc? Is plain text a poor binding between what we write and the AST, would some kind of rich-text format for code be more effective?

- ## 💡 What is being measured here are *client* ops/sec. 
- https://twitter.com/Horusiath/status/1660705223818596358
  - These are strictly correlated with actions of individual users.
  - What gets replicated are deltas, which are not discussed in the post
- I just read the code. Its code doesn't support encoding/decoding yet for StringRga. But it seems like it might as well get pretty fast on those tasks.
- Thing is you don't need to optimize client ops beyond certain point. They are constrained to actions of a single client. What you may want to optimize are store/load updates, as they scale with number of connected clients and their actions.
- Now, when it comes to replication Yrs can serialize document state made of 259778 client operations (inserts and deletes) in 2-3ms (86.5mln client ops/sec) and sync it in 13ms (~20mln ops/sec) with a payload size of 160kB (less than 1B per op). On a single core.
  - Tbh. most of Yrs speed comes right off the bat and I barely did any optimisations there. 

- ## I’m surprised there is no popular framework to build Figma-like apps. (Correct me if I’m wrong.) 
- https://twitter.com/reneeshah123/status/1674130544207220736
- Things I’d want in a framework: 
  1. An easy way to build desktop-like experiences in the browser – especially for data intensive apps
  2. Multiplayer support
  3. Great devex
- @liveblocks , @replicache , and @FluidFramework all do multiplayer. @drifts_in_space does "session-lived backends" for these apps. All are compelling, and I'm sure I'm missing many.

- ## [Real Differences Between OT and CRDT for Co-Editors | Hacker News](https://news.ycombinator.com/item?id=18191867)
- On page 30 par 2 you conclude that OT has time complexity O(1) while CRDT is O(C) or so... I guess, you compare a rope-based OT implementation and a naive CRDT implementation (like, one doing a full rewrite on each key press). At least, that is my best guess.
  - Why don't you compare them the other way around? Rope-based CRDT and a naive OT? String splicing is O(N), you may put it on either side of the scales. Hashtable-hosted Causal Tree is O(1); hashtable-hosted RGA is basically the same.
  - I find the general discourse of the article not so useful. I may guess, you overreacted to certain marketing messages coming from the CRDT community.

- ## If you store a CRDT as a BLOB in a SQLite column, you can do efficient partial reads or incremental writes instead of reading/writing the whole thing via UPDATE 
- https://twitter.com/jitl/status/1530308079237070848
  - I'm not sure how transactional this interface is.

- ## Most CRDTs use immutable append-only logs but Is a waste of performance/efficiency.
- https://twitter.com/marknadal/status/1543666528746295297
  - Like git, it does not scale well for new/joining viewers.
  - Its better that the CRDT directly understands snapshotting. This is what GUN does, Snapshots at load. Diff/patches over the wire live.

- Pretty much all the other CRDT systems use append-only immutable logs:
- https://twitter.com/marknadal/status/1575739378684477440
  - Which causes scaling problems.
  - Compared to in-place mutable updates. (GUN can also do append-only/immutable, but that's not as fast)

- ## [Lessons learned from creating a real-time collaborative rich-text editor | Hacker News](https://news.ycombinator.com/item?id=18220020)

- ## [Liveblocks: Add real‑time collaboration to your product in minutes | Hacker News_202107](https://news.ycombinator.com/item?id=27994480)
- Liveblocks does not come with a specific UI. We're providing APIs to create rooms and share states between users. 
  - The state can be volatile (like cursors, focused input, selection) or persisted even when the session is over, like a figma file or a google document (this part is still in private beta). 
  - We're using custom CRDTs for the persisted state.

- This looks great, how do you stack up against something like YJS?
- Like Yjs, our Storage block is CRDTs based, but we're making different trade-offs. 
  - For example, our CRDTs are not "pure" so we solve some conflicts on the server. 
  - 🚨 Also, we don't support Text CRDTs yet.
- But Liveblocks is not just about conflicts resolution! 
  - Our vision is to shape our API and guides to help companies transform existing products into collaborative ones. 
  - For example, by simply adding live cursors and avatars and refreshing the data with existing REST endpoints, an existing app becomes more collaborative even if the conflict resolution is not perfect. 
  - At the same time, we provide analytics on how Liveblocks is used to help product teams prioritize their collaborative features and if they still want to integrate Liveblocks further.
- We're also hosting the WebSocket infrastructure and make it scale because we know how troublesome it can be to maintain.

- 🤔 how does this compare to something like https://replicache.dev/
- From what I understand from Replicache, it focuses only on conflicts resolution with CRDTs, and it does not come with a web socket infrastructure nor a hosted backend. You need to have your own servers or use external services to have live cursors. (https://doc.replicache.dev/guide/poke)
- **At Liveblocks, we want to bundle all that together** because we believe that being tightly integrated is necessary to provide a great experience.
- Some people might prefer managing their own backend infrastructure, but we want to provide it because we know how difficult it might be to scale and load balance web sockets rooms. We want to help companies focus on their core product and not spend too much time working on the multiplayer infrastructure and algorithms.

- I work in the "realtime" space too (founder of Fanout, low level push infra).
  - Liveblocks looks like it's somewhere between Firebase and Sendbird, providing live updates and state management, but for specific use-cases and stopping short of the UI. I haven't seen too many products operating at that level of abstraction, so maybe you're on to something. I also like how you solve for more use-cases than chat, the dominant "block" in the market.

- There are a lot of live sharing/working/... coming out these days.
- FYI: Your cursor examples uses x/y explicit coordinates where as people using different screen sizes and resolutions wouldn't see proper mouse cursor location. Rather it should be x/y relative coordinates.example x: 35%, y:12% (top left corner to bottom right corner)
- From our experience, live cursors positioning depends on the use case and the content behind them.
  - For a "canvas app" (like Figma), the positioning will be absolute with an offset depending on the panning.
  - Sometimes, cursors are not the best way to show what users are doing on a web page. For a form, displaying an indicator close to the focused input is more valuable.
  - Because there is no perfect solution, we're not shipping any UI with Liveblocks and only provide guides. In the future, if a common abstraction appears, we will create some package to make the integration easier.

- ## To summarize the differences between Ably/Pusher and Liveblocks, 
- https://news.ycombinator.com/item?id=31684467
  - Ably/Pusher use a centralized Redis to broadcast messages to channels. 
  - Liveblocks has tiny isolated servers on the edge for every room. 
- These two different architectures create the following trade-offs:
  - Ably/Pusher are lower level than Liveblocks. It doesn't have any storage associated to a channel and does not solve any conflicts.
  - Liveblocks provides API to migrate existing app into collaborative ones via integration with state management library like Redux/Zustand. I have a POC somewhere that try integrate with Vuex, would love to release that at some point!
  - Ably/Pusher charges per WebSocket message sent. Liveblocks charges per WebSocket connection. Because of that, building features like cursors can become quite expensive on Pusher.
  - Ably/Pusher lets you connect to multiple channels with a single WebSocket connection (because they're using a centralized Redis IIRC). Liveblocks requires a single WebSocket connection per room. Pusher is good for notifications systems, Liveblocks shines when you need to build an app like Figma or Google spreadsheet.

- ## Before anyone "well actually"'s me, @replicache is causal consistent. 
- https://twitter.com/aboodman/status/1623822005098401793
  - It doesn't rely on clocks for correctness. 
  - Walltime still comes in handy a surprising amount of cases.
- Lol. Reminded me of spanner and true time

- ## [Supabase – Realtime: Multiplayer Edition | Hacker News](https://news.ycombinator.com/item?id=32510405)
- after thinking it through, I'm not clear on what Supabase is calling multiplayer.

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
