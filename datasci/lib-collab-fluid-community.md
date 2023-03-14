---
title: lib-collab-fluid-community
tags: [community, fluid-framework]
created: 2023-02-11T11:07:19.102Z
modified: 2023-02-11T11:07:43.781Z
---

# lib-collab-fluid-community

# guide

# discuss
- ## 

- ## 

- ## [How can you ensure the database is the source of truth in the Fluid world?](https://github.com/microsoft/FluidFramework/discussions/9536)
- not yet

- ## [Building a BFT JSON CRDT | Hacker News](https://news.ycombinator.com/item?id=33694568)
- It's the Byzantine Fault Tolerant part of this that is particularly innovative and based on Kleppmanns most recent work. I believe it solves the issue of either malicious actors in the networks modifying others transactions, spoofing them, or the messages being modified by third parties ("outside" the network) who have MITM the connection. These are really great problems to solve.

- Interesting, yeah access-control is kinda open problem with Yjs. Regarding ProseMirror and rich-text documents, you can mess up documents in other ways as well. Eg deploy a faulty command with a transaction that inserts nodes with invalid children (can be prevented though by using createChecked). Or just changing your schema in an incompatible way with the previous version. So you kinda have to deal with possible malformed documents either way.
  - And about the schema layer on top of Yjs, you possibly could inspect every update and apply some validation rules. Arent all operations just inserts, updates or deletes of nodes? You can at least rollback to previous version as you flush the updates to the doc in the db. Not ideal though.

- When I was working on this problem with Fluid Framework, we did a few interesting experiments with "owned objects" and centralized ACL objects. I believe the team primarily implemented centralized ACL because that implementation works for many enterprise use cases.
  - With a centralized schema provider, you run a connected node on a trusted server and reject changes that are out of schema or should not be accessed by a user.
  - An owned object is an object where a user (or user group that votes via quorum) that owns the object can veto changes to the object. The changes are temporarily applied until accepted by the owners. I haven't dug deep enough into this BFT implementation to know how our model would map to this model.

- ## [Lessons learned from creating a rich-text editor with real-time collab (2018) | Hacker News](https://news.ycombinator.com/item?id=25394609)
- Disclosure: I work on a related project (Fluid Framework) that makes application agnostic CRDTs easily available.
  - The CKEditor folks did a great job building an OSS text editor and they did an especially strong work building a text editor that works well with collaboration. 
  - I've made a few OSS rich text editors work (mostly) with Fluid [0, 1] and the design of the text editor really changes how easily collaboration can be added. Luckily the text editor accepts remote changes, integrating an OT or CRDT solution is approximately the same.
  - They also did a great job explaining the problem. 
- My experience has been that people don't intuitively understand why real time collaboration is a tricky problem. I didn't. 
  - First of all, for a bunch of use cases websockets + redis + a last write wins conflict resolution (or some similar solution) is totally enough. 
  - Second, it's not immediately obvious why rich text editing requires more complex conflict resolution. 
  - Third, it's not obvious why solving the RTE problem doesn't immediately lend itself to other problems 

- ## [Hypercore protocol: a distributed (P2P) append-only log | Hacker News](https://news.ycombinator.com/item?id=25407193)
- This is coming up twice today, but I’m interested in using a P2P append only log as a total order broadcast for use with (my day job) Fluid Framework.
- Decentralizing the broadcast would make Fluid more aligned with the Ink and Switch essays about offline first.

- ## [Microsoft Loop brings back Google Wave? | Hacker News](https://news.ycombinator.com/item?id=29082706)
- Has anyone tried to develop anything with MSFT's Fluid Framework, which is used to build Loop? 
- 👉🏻 I haven't used it, only read through documentation, but IMO Fluid's problem is not so much lock-in as an embrace of old-school columnar storage and handle-based object manipulation. 
  - An experienced Windows developer or game dev might feel entirely at home with the tradeoffs/footguns implied by https://fluidframework.com/docs/build/dds/#picking-the-right... ... 
  - but show that to a junior React developer and they're likely to be fundamentally confused, or worse assume that the only code example shown is a valid code example. 

- Contributor Martin Kleppman (of Designing Data-Intensive Applications fame) has great overview slides here: https://martin.kleppmann.com/2021/06/04/craft-conf.html . 
  - If anything, Automerge suffers from a "there's multiple ways to have a server backend, including P2P and centralized, and no one right way" anti-lockin problem, which is refreshing and also frustrating for people who just want to try something out. This is a solvable problem though!

- 👉🏻 I think you have to consider your use case. If you want to build pure online collaboration tool it is fine. But if you want to build something that supports offline collaboration it seems not to be ready yet:
  - Clients do have to be connected to the Fluid service. Fluid can tolerate brief network outages and continue operating but eventually the promise of being able to merge local changes weakens. We are investigating ways to improve this using other merging techniques designed to reason over large deltas but no final solution is in place today.

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
- By the way, Microsoft has a new set of libraries for concurrent editing called Fluid Framework. 
  - I'm told it's a "generalized data structure" that was inspired by Causal Trees but with a unique and intention-preserving editing scheme. 
  - I found out about it after they decided to use my fast-cloning-copy-on-write B+Tree for TypeScript... 
  - they sent me a pull request for diffing versions of B+ trees, but I haven't yet looked into the architecture of their concurrent data type.

- ## [The interface looks much more similar to Notion than Google Wave; I don't see th... | Hacker News](https://news.ycombinator.com/item?id=29085200)
- Do you know if the Fluid Framework is built on top of CRDTs?

- From what I recall of a BUILD talk once on the deep dive fundamentals, Fluid is based on CRDTs under the hood (or possibly the CRDT predecessor OT like Wave was), but Fluid believes writing CRDTs is hard (it is), especially writing them that obey the math laws CRDTs are supposed to, and then getting that to perform well (including and especially things like catch-up/replay) is also hard, so yes the actual programming interface Fluid presents is high level "distributed data structures" though the wire format is closer to CRDTs with some cheats from assumed knowledge of the data structures (things like sending the latest contents of a list for catch-up rather than replaying the entire CRDT chain for that list).

- ## Full disclosure I work at MSFT and on the fluid framework.
- https://news.ycombinator.com/item?id=29654955
- We use websockets and solve a lot of the state management problem called out here by keeping very little state on the server itself. The primary thing on server is a monotonically increasing integer we use to stamp messages, this gives us total order broadcast which we then build upon
- The map package is a decent place to look for how we leverage total order broadcast to keep clients in sync in our distributed data structures
- The deltamanger in the container-loader package is where we manage the websocket. It also hits storage to give the rest of the system a continuous, ordered stream of events
