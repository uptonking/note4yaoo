---
title: lib-collab-crdt-blog-stars
tags: [blog, crdt]
created: 2023-03-11T15:37:35.868Z
modified: 2023-03-11T15:37:59.134Z
---

# lib-collab-crdt-blog-stars

# guide

# blogs

## [You might not need a CRDT | Drifting in Space](https://driftingin.space/posts/you-might-not-need-a-crdt)

- CRDTs differ from simple leader/follower replication in that they do not designate an authoritative source-of-truth that all writes must pass through.
  - Instead, all replicas are treated as equal peers. 
  - Each replica may be modified locally, and changes to any replica are propagated to the others.

- when we started talking to dozens of companies building ambitious browser-based apps, we found it rare for apps to use true CRDTs to power multiplayer collaboration.

- The core problem that multiplayer apps need to solve is maintaining shared state. 
  - this means that there is some data structure (say, a tree or list) representing the document which exists in multiple locations: one for each user with the document open. 
  - Changes made on one copy need to be reflected by the others, as quickly as possible.
- One way to accomplish this is to serialize each change and broadcast it over the network.
- 💡 The problem comes down to the interplay of two facts:
  - Operations on our data structure are not commutative: the result of applying them depends on the order in which they are applied.
  - Our operations are unordered. Each replica might receive and apply the changes in a different order.
- If we can design a system in which either one of these statements is no longer true, we can ensure that our data structure is eventually-consistent. 
- Path #1 represents CRDTs. Broadly, you can think of CRDTs (specifically, operation-based CRDTs) as a family of useful data structures (lists, sets, maps, counters) carefully designed such that all operations are commutative.
- Path #2 in its pure form represents state machine replication. We ensure that each replica receives changes in the same “global” order, and apply change on each replica in that same global order. This ensures that each replica stays in sync, even if change operations are not commutative.

- most of the systems we’ve looked at could be described as hybrid approaches that borrow ideas from both paths. 
  - They represent operations as commutative where possible so that they can apply them immediately on the local replica without worrying about where they appear in the global order, but they ultimately depend on a global order for convergence.
- Both paths will allow us to ensure that each replica converges on the same state, but that alone does not guarantee that this state is the “correct” state from the point of view of user intent.
- State machine replication is not a silver bullet; we still need to be thoughtful about how change operations apply when the underlying data has changed. 
  - Our Aper Rust library is an experiment in seeing how much of this can be generalized into a data structures library.

- CRDTs are complex, in both the runtime overhead and cognitive load senses, but in a peer-to-peer environment, this is a necessary cost.
- In contrast, browsers are inherently not peer-to-peer. To run an application from the web, you connect to a server. 
  - Since the server is centralized anyway, we can have it enforce a global ordering over the events. 

- Figma isn't using true CRDTs […]. 
  - CRDTs are designed for decentralized systems where there is no single central authority to decide what the final state should be. 
  - There is some unavoidable performance and memory overhead with doing this. 
  - Since Figma is centralized (our server is the central authority), we can simplify our system by removing this extra overhead and benefit from a faster and leaner implementation.
- With a global order, we don’t need to bend over backwards to ensure that data mutations are commutative, we can use the global order to apply them in the same order on every replica.
- A modern web application is likely deployed to multiple servers, not one, which complicates using “the server” as a source of truth. 
- Figma solves this by routing messages to a dedicated process for each live document. 
- Plane and Jamsocket generalize that approach

- when applications have presence features that provide hints， users tend not to conflict with each other
- A general theme of successful multiplayer approaches we’ve seen is not overcomplicating things.

- Although CRDTs aren’t always the best solution for always-online collaborative apps, it’s still fascinating tech that has real use cases.
  - Apps that need to run offline in general are good candidates for CRDTs.

## [Designing Data Structures for Collaborative Apps - Matthew Weidner](https://mattweidner.com/2022/02/10/collaborative-data-design.html)

- A good starting point is to design an ordinary (non-CRDT) data model, using ordinary objects, collections, etc., then convert it to a CRDT version. 
  - So variables become Registers, objects become CRDT Objects, lists become List CRDTs, sets become Unique Sets or Add-Wins Sets, etc

## [A comprehensive study of Convergent and Commutative CRDT_201101](https://www.researchgate.net/publication/50949847_A_comprehensive_study_of_Convergent_and_Commutative_Replicated_Data_Types)

- Sets constitute one of the most basic data structures. 
  - Containers, Maps, and Graphs are all based on Sets.
- We consider mutating operations add (takes its union with an element) and remove (performs a set-minus). 
  - Unfortunately, these operations do not commute. 
  - 👉🏻 Therefore, a Set cannot both be a CRDT and conform to the sequential specification of a set.
- Thus, a CRDT can only approximate the sequential set. 
- The CALM Theorem states that anything that is logically monotonic (read: append-only) can be made into a CRDT. Non-monotonic things may ‘retract’(收回；否认) previous statements.

- Two-Phase Set (2P-Set)
  - It combines a G-Set for adding with another for removing; the latter is colloquially known as the tombstone set. 
  - To avoid anomalies, removing an element is allowed only if the source observes that the element is in the set.
