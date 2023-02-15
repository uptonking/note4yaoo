---
title: lib-collab-ot-community-stars
tags: [collaboration, community, ot]
created: 2022-10-02T20:53:52.128Z
modified: 2022-10-02T20:54:07.621Z
---

# lib-collab-ot-community-stars

# guide

# discuss-stars
- ## [json0 supporting of rfc6902 specification for JSON type?_201410](https://github.com/ottypes/json0/issues/4)
- The json0 type doesn't support moving objects between paths, so its not compatible with json patch.
- The new OT type won't use json-patch operations internally, but the new json type's operations will be almost isomorphic. When its done, it might be worth writing couple of functions to convert operations back and forth for interoperability.

- JSON1 OT Spec, Advantages compared to JSON0
  - The new type should support conversion between JSON operations and JSON Patch (RFC 6902). 
  - I want those conversions to be bidirectional if possible, although converting embedded custom OT types to JSON Patch won't work.

- ## Why OT cannot be applied on P2P networks? Does Google Docs use a transformation-based server mean that all OT need a central server?_201810
- https://news.ycombinator.com/item?id=18192147

- 👉🏻 josephg: Simple OT algorithms do work a lot better with a centralized server.
  - With a centralized server, you can consider every resolution as happening between 2 nodes (server and client). 
  - This means transform/catchup is as simple as a for loop.
- In contrast, in decentralized context OT code needs to support Transform Property 2 in order to converge correctly in all cases. 
  - TP2 dramatically complicates the OT implementation, and you need a much more complicated resolution algorithm to merge arbitrary changes between nodes.
- For text, this means you need:
  - Tombstones (or something like it) - eg https://github.com/josephg/TP2/blob/master/src/text.coffee
  - Either an operation prune function (anti-transform) or full history, forever.
  - A resolution algorithm that can flatten DAGs of operations into a transformed list. This stuff gets really hairy, and hard to implement efficiently. This is my attempt from a few years ago. Its correct, but super slow: https://github.com/josephg/tp2stuff/blob/master/node3.coffee
- Implementing high performance OT with centralized servers is easy. Implementing OT in a decentralized network is hard to do correctly, and much harder to implement in a highly performant way. For decentralized systems, CRDTs are a much better approach imo.

- There are a few things related to TP2, aka Convergence Property 2 (CP2), that needs to be unpacked here.
  - Do your system always need to preserve TP2/CP2 to converge correctly? Contrary to what many folks and papers will claim, answer is categorically no.
  - There are two general approaches to arrive this desired outcome: (1) avoiding it or (2) preserving it.

- You can implement correct and performant OT with both a centralized server or with a fully decentralized topology, using TP2/CP2-avoidance and/or with TP2/CP-preservation. I've built multiple production systems with all the varieties. I generally do prefer OT with TP2/CP2-avoidance on a server, but it's not because OT can't avoid TP2/CP2 without a server or preserve TP2/CP2, it is that there is not much real-world evidence showing clear benefits moving a collaborative editing system to decentralized topology, esp when most of the CRDT-based p2p proposals in papers that I've come across involves a server one way or another.

- TP2/CP2 in OT is often stood up as a straw-man(被用作挡箭牌的人; 起吓唬作用的稻草人) so folks can throw stones against its correctness, it is really a solved problem. The unfortunately outcome is that you see a ton of papers adopting this strategy to get published and overtime the conversation becomes really convoluted(错综复杂的；晦涩难懂的).

- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## You seem to be implying that OT requires a central server. OT was designed for peer-to-peer, at least as far as I know.
- https://news.ycombinator.com/item?id=23806564
- My understanding is that most specifications for OT have obscure failure cases if a central server is not used. Some papers have fixed these issues to enable fully P2P OT, but IIRC the resulting ops require similar amounts of metadata per-change as sequence CRDTs.

- Interesting. I thought that OT implementations require peers to have at least one authoritative view of the transformations somewhere, and then distribute different operation sequences (after transformed) to different node. That, in simplest way, would imply a central server (otherwise you will have an alternative method to communicate the authoritative view between peers, which sort of defeat the purpose).

- 👉🏻 Yes. There do exist peer-to-peer OT algorithms, however they have not become popular in any production websites.
  - The popular production systems (such as Google Wave and Docs) are based on the Jupiter style of operational transform, which features a single central server, with a single line of time. 
  - The clients try to send their edits to the server as the most-recent edit. 
  - If they fail, for instance because another client has made an edit, then they rebase their edit on the new most-recent version, and then try to submit it again.
- Keep in mind that OT and CRDT aren't actually algorithms -- they are perspectives from which a programmer might try to think of an algorithm.
  - The Operational Transform perspective says "think about how you can transform your edits (aka operations) so that they work when applied in a different order, on a peer with a different history of time.
  - The CRDT perspective says "think about how you can formulate your data structures so that you can apply any edit in any order."

- In practice, programmers who took OT perspective were able to create mostly-working systems pretty easily. 
  - 👉🏻 But getting full consistency (aka correctness) was very difficult, because it was difficult to think of all the ways in which multiple operations could interleave(插入/夹进) and affect one another, especially without the constraint of a central. 
  - Thus, it took many, many academic papers before anyone succeeded in coming up with a fully P2P algorithm that resulted in consistent synchronization after arbitrary edits.

- The CRDT paradigm made it easy to get fully-consistent peer-to-peer systems. 
  - 👉🏻 However, it has remained elusive to make one that's performant enough to be used in practice. 
  - They tend to require holding onto the entire history of all operations that have ever occurred, and each operation itself tends to require 10x or 100x overhead. 
  - Thus, you can edit a small text document and quickly end up with megabytes of data for a small string of text.

- But there's a third paradigm here that isn't discussed as much -- Version Control. 
  - Think about git. It provides a DAG of versions over time, that branch and fork, and a way to consistently merge any two versions. 
  - From this perspective, it turns out that OT is the discovery of the rebase operation, and CRDT is the discovery of multi-way merge in a DVCS. 
  - OT people have been trying to simplify complicated merges by doing clever rebasing. 
  - This is much easier with a central server, and it happens to allow you to clean up old history more easily, which saves a lot of memory, making it useful in production systems.

- In practice, I think that these three perspectives are all going in the same direction. 
  - If you build an OT system, and then try to make it fully consistent and peer-to-peer, you end up with CRDT algorithms. 
  - If you build a CRDT, and want more flexibility in memory requirements, a great approach is to throw a server into the mix and rebase (aka transform some operations). 
  - And git already has "operational transform" and "CRDT" algorithms in it.

- My personal interest is in unifying these algorithms in the https://braid.news project. 
  - We have a unified protocol that allows OT and CRDT systems to communicate with one another, and we've got some great new algorithms for pruning old history in a fully-p2p network that I expect to release this summer.
