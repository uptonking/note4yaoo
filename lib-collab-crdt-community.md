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


- ## [Hypercore protocol: a distributed (P2P) append-only log | Hacker News](https://news.ycombinator.com/item?id=25407193)
- This is coming up twice today, but I’m interested in using a P2P append only log as a total order broadcast for use with (my day job) Fluid Framework.
- Decentralizing the broadcast would make Fluid more aligned with the Ink and Switch essays about offline first.


- ## [Supabase – Realtime: Multiplayer Edition | Hacker News](https://news.ycombinator.com/item?id=32510405)
- after thinking it through, I'm not clear on what Supabase is calling multiplayer.




- ## [Lessons learned from creating a real-time collaborative rich-text editor | Hacker News](https://news.ycombinator.com/item?id=18220020)

- ## [Lessons learned from creating a rich-text editor with real-time collab (2018) | Hacker News](https://news.ycombinator.com/item?id=25394609)
- Disclosure: I work on a related project (Fluid Framework) that makes application agnostic CRDTs easily available.
  - The CKEditor folks did a great job building an OSS text editor and they did an especially strong work building a text editor that works well with collaboration. 
  - I've made a few OSS rich text editors work (mostly) with Fluid [0, 1] and the design of the text editor really changes how easily collaboration can be added. Luckily the text editor accepts remote changes, integrating an OT or CRDT solution is approximately the same.
  - They also did a great job explaining the problem. 
- My experience has been that people don't intuitively understand why real time collaboration is a tricky problem. I didn't. 
  - First of all, for a bunch of use cases websockets + redis + a last write wins conflict resolution (or some similar solution) is totally enough. 
  - Second, it's not immediately obvious why rich text editing requires more complex conflict resolution. 
  - Third, it's not obvious why solving the RTE problem doesn't immediately lend itself to other problems 

- ## [Microsoft Loop brings back Google Wave? | Hacker News](https://news.ycombinator.com/item?id=29082706)
- Has anyone tried to develop anything with MSFT's Fluid Framework [1], which is used to build Loop? 
- 👉🏻 I haven't used it, only read through documentation, but IMO Fluid's problem is not so much lock-in as an embrace of old-school columnar storage and handle-based object manipulation. 
  - An experienced Windows developer or game dev might feel entirely at home with the tradeoffs/footguns implied by https://fluidframework.com/docs/build/dds/#picking-the-right... ... 
  - but show that to a junior React developer and they're likely to be fundamentally confused, or worse assume that the only code example shown is a valid code example. 


- Contributor Martin Kleppman (of Designing Data-Intensive Applications fame) has great overview slides here: https://martin.kleppmann.com/2021/06/04/craft-conf.html . 
  - If anything, Automerge suffers from a "there's multiple ways to have a server backend, including P2P and centralized, and no one right way" anti-lockin problem, which is refreshing and also frustrating for people who just want to try something out. This is a solvable problem though!


- I think you have to consider your use case. If you want to build pure online collaboration tool it is fine. But if you want to build something that supports offline collaboration it seems not to be ready yet:
  - > Clients do have to be connected to the Fluid service. Fluid can tolerate brief network outages and continue operating but eventually the promise of being able to merge local changes weakens. We are investigating ways to improve this using other merging techniques designed to reason over large deltas but no final solution is in place today.



- ## [Fluid framework, for building distributed, real-time collaborative web apps_202009](https://news.ycombinator.com/item?id=24417482)
- Does Fluid use operational transforms?
  - Fluid does not use Operational Transforms, but we learned a tremendous amount from the literature on OT. 
  - While OT uses operations that can be applied out of order by transforming operations to account for recent changes, Fluid relies on a Total Order Broadcast to guarantee that all operations are applied in a specific order.

- Does Fluid use CRDT?
  - Fluid does not use Conflict-Free Replicated Data Types (CRDTs), but our model is more similar to CRDT than OT. 
  - The Fluid Framework relies on update-based operations that are ordered using our Total Order Broadcast to prevent conflicts. 
  - This allows us to have non-commutative operations because their is an explicit ordering.
- Their model sounds a lot like how Croquet (https://en.wikipedia.org/wiki/Croquet_Project) used to work, where every operation is given a globally-ordered timestamp as it passes through a shared message router.

- Looks like a CRDT/Operational Transform server/pubsub as a service. 

- Adding more context: Fluid uses a mix of CRDT + OT to maintain state across multiple clients. I wrote a quick high level explanation of how Fluid uses eventual consistency and why it matters for real time collaboration
  - [Solving real time collaboration using Eventual Consistency](https://matt.aimonetti.net/posts/2020-09-solving-real-time-collaboration-using-eventual-consistency/)

- ## [Faster CRDTs: An Adventure in Optimization | Hacker News](https://news.ycombinator.com/item?id=28017204)
- By the way, Microsoft has a new set of libraries for concurrent editing called Fluid Framework[2]. 
  - I'm told it's a "generalized data structure" that was inspired by Causal Trees but with a unique and intention-preserving editing scheme. 
  - I found out about it after they decided to use my fast-cloning-copy-on-write B+Tree for TypeScript[3]... 
  - they sent me a pull request for diffing versions of B+ trees, but I haven't yet looked into the architecture of their concurrent data type.

- ## [The interface looks much more similar to Notion than Google Wave; I don't see th... | Hacker News](https://news.ycombinator.com/item?id=29085200)
- Do you know if the Fluid Framework is built on top of CRDTs?

- From what I recall of a BUILD talk once on the deep dive fundamentals, Fluid is based on CRDTs under the hood (or possibly the CRDT predecessor OT like Wave was), but Fluid believes writing CRDTs is hard (it is), especially writing them that obey the math laws CRDTs are supposed to, and then getting that to perform well (including and especially things like catch-up/replay) is also hard, so yes the actual programming interface Fluid presents is high level "distributed data structures" though the wire format is closer to CRDTs with some cheats from assumed knowledge of the data structures (things like sending the latest contents of a list for catch-up rather than replaying the entire CRDT chain for that list).

- ## Full disclosure I work at MSFT and on the fluid framework.
- https://news.ycombinator.com/item?id=29654955
- We use websockets and solve a lot of the state management problem called out here by keeping very little state on the server itself. The primary thing on server is a monotonically increasing integer we use to stamp messages, this gives us total order broadcast which we then build upon
- The map package is a decent place to look for how we leverage total order broadcast to keep clients in sync in our distributed data structures
- The deltamanger in the container-loader package is where we manage the websocket. It also hits storage to give the rest of the system a continuous, ordered stream of events

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

- how does this compare to something like https://replicache.dev/
- From what I understand from Replicache, it focuses only on conflicts resolution with CRDTs, and it does not come with a web socket infrastructure nor a hosted backend. You need to have your own servers or use external services to have live cursors. (https://doc.replicache.dev/guide/poke)
- At Liveblocks, we want to bundle all that together because we believe that being tightly integrated is necessary to provide a great experience.

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
