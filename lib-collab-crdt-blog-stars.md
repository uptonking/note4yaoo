---
title: lib-collab-crdt-blog-stars
tags: [blog, crdt]
created: 2023-03-11T15:37:35.868Z
modified: 2023-03-11T15:37:59.134Z
---

# lib-collab-crdt-blog-stars

# guide

# blogs

## [CRDTs _202209](https://www.gatlin.io/content/crdts)

- Regarding internal state management, you can think of operation-based CRDTs as analogous to event sourcing. It is an implementation detail, but presumably a "pure" operation-based CRDT will store "just" the events, and compute the state from that (which it may or may not store, internally). 
  - State-based CRDTs will store the state internally (and may or may not store message events depending on how broadcasting is implemented).

- An ORSet, or "Observed-Remove Set", is the same as an AWSet, or "Add-Wins Set". 
  - It is a way of defining the tie-breaking semantics of conflicting, concurrent updates. 
  - If concurrent operations call for a remove and an add, the add wins.

## 📝 [You might not need a CRDT, but server reconciliation _Replicache](https://pitch.com/public/a49fccb0-da65-4d64-966e-e519674d951f)

- replicache doesn't use crdt
  - it uses server reconciliation, technology from the late 2000s
  - popularized by video game industry, but has a lot of advantages for web apps too
- some products also dont use crdt
  - figma
  - notion
  - linear
  - google docs

- yjs is sequence crdt
  - designed for long list/text/sorted-map
- counter is not sequence or map, so yjs doesnot fit
  - yjs `map.set` may cause `increment` op lost

- how replicache works
  - mutations continuously added at each device independently, without waiting for server
  - mutations continuously pushed to server
  - server linearizes mutations arbitrarily, iie in order of arrival
  - server applies mutations to create new authoritative state
- mutations are often added while awaiting confirmation of earlier ones
- pending/unacked mutations are rebased atop latest server state by again running their code

- when crdts work well, it's by capturing and preserving user intent
- server reconciliation generalizes this idea. apps define their own intents using mutators
- instead of each intent having to define a custom merge function, history linearization serves as a general-purpose merge.

- crdts cannot easily implement data validation
- with server reconciliation, only intents are sent upstream and server computes effect for itself
  - this means u get validation for free
  - if server ignores or alters a mutation, clients will all do the same

- because server is authoritative, mutations do not have to be deterministic

### [Slides for yesterday's talk on Replicache and Reflect](https://twitter.com/aboodman/status/1664008955214061569)

- Are you considering evolving towards full OT by allowing mutators to transform pending mutations?
  - Well *now* I am. 
- I've built this system. The linearization is the part that makes the rest simple, add a simple logical clock   
- It's a cool idea but I'm curious about concrete benefits that it would provide over the current simple model.
  - The classic example is text editing. You receive two text insert operations that are individually valid and causally concurrent, but after you apply one, the other is incorrect unless its offsets are transformed by the length of the first.
- I wish I had more time to think about this problem in particular.
  - I keep thinking that there is probably something interesting and useful we can do for text editing in particular that takes advantage of the server. I'd love to have time to do a survey of the state of collaborative text editing and how they map to replicache.
  - Like it's a pretty powerful thing that the mutators are *code* that can run and change its own result. Given the right state the second "insert" mutator ought to be able to implement the offsetting logic itself.
- 💡 Yeah, so you could implement OT in mutators: keep a sequence number on the doc as a logical clock, **send sequence number with operation**, store the operations in a log along with their sequence number...
  - then implement computeOffset by looking at all operations in the log with a sequence number greater than what was sent with the mutation.

- The slides are good - some of the things that you’ve said are difficult with CRDTs is more a limitation of the libraries. E.g transactions, counters, server authority. 
  - CRDT’s are network agnostic and can work well in centralised environments. Also Figma uses some CRDTs.
- Can you expand? "Transaction" is a bit of a squishy word, but isolated transactions are only possible in a CRDT if you sacrifice durability. I believe durable transactions are possible but AFAIK it has never been demonstrated and would be research-level work.
  - It is certainly possible to have a server be one of the nodes in a CRDT, but it is not easy to have the server actually be authoritative. You can filter operations before applying to server but (a) this is difficult to do well because you end up having to reverse engineer intent, and (b) you have to do something about the client that has now diverged.

## 📝 [You might not need a CRDT | Drifting in Space_202212](https://driftingin.space/posts/you-might-not-need-a-crdt)

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

## 👥 [You might not need a CRDT | Hacker News_202212](https://news.ycombinator.com/item?id=33865672)

- This is the most underrated problem with CRDTs:
  - > Both paths will allow us to ensure that each replica converges on the same state, but that alone does not guarantee that this state is the “correct” state from the point of view of user intent.
  - In context of richtext editors, it's easy to converge a rich-text JSON into a single state for all collaborators. 
  - What's difficult is to ensure that the converged state is renderable as richtext. For example, is there a table cell that was inserted where a column was deleted?
  - I wrote a summary of this issue with CRDTs here
  - [Where is the CRDT for syntax trees](https://writer.zohopublic.com/writer/published/grcwy5c699d67b9c444219b60cdb90ccbabc7)
  - PS: We currently use OT for collaboration in Zoho Writer_202212

- They/crdts are "conflict free" in as much as they are able to merge and resolve in the basic sense. That does not mean that the resulting state is valid or meets your internal schema.
  - A good example of this is using Yjs with ProseMirror, it's possible for two concurrent edits to resolve to a structure that doesn't meet your ProseMirror schema.
  - It's possible for two users to add that caption to the figure concurrently, Yjs will happily merge its XMLFragment structures and place two captions in the figure. However when this is loaded into ProseMirror it will see that the document does not match its schema and dump the second caption. 
  - This is all ok if you are doing the merging on the front end, but if you try to merge the documents on the server, not involving ProseMirror, the structure you save, and potentially index or save as html, will be incorrect.
  - Point is, it's still essential with CRDTs to have a schema and a validation/resolution process. That or you use completely custom CRDTs that encodes into their resolution process the validation of the schema.
- I'm surprised that MS's concurrent revisions haven't taken off because this is what they do by default: you specify a custom merge function for any versioned data type so you can resolve conflicts using any computable strategy.

- There's actually an approach that sits in between this and formal CRDTs.
  - I had the same insight that **having a total ordered log of changes solves a lot of the issues with concurrent updates**. 
  - We solved this by creating one sequence CRDT that ensures all events from clients eventually end up in the same order and then our data structures are just reductions over those events. 
  - It's a little bit like a distributed, synchronized Redux store. 
  - This let us avoid having to think in terms of CRDT types (LWW registers, Grow-only sets, sequences, etc) and just think in terms of the domain-specific business logic (e.g. "what should happen when someone marks a todo as done, after it's deleted?").
- 🤔 Have you considered backing your application's state-synchronization with a centralized CQRS/ES event store? You get the same semantics, without paying the overhead of building them on top of a CRDT abstraction; and the event store itself also "knows" (in the sense that it supplies the framework and you supply the logic) how to reduce over states in order to build snapshot states ("aggregates") for clients to download for fast initial synchronization.
  - We basically have that as well! We use CRDTs on the client to allow for optimistic updates and fast replication of events directly to other clients but we also do exactly what you describe on the server so that a user loading the data for the first time just gets the "snapshot" and then plays events on top of it.
- Isn't that essentially doing a CRDT, but the replica is the whole datastore? Ties in nicely with event sourcing - the ordered sequence of events is the CRDT, and sending events between nodes are the delta states.
- How do you solve the ordering? Timestamps can be wildly out of whack? Be interested to hear more
  - We use logical timestamps instead of datetime.

- CRDTs have been on HN a lot recently. I'm working on a database that deals in events rather than raw data. Application developers specify event handlers in JavaScript. The database layer then takes the event handlers and distributes them to the clients. Clients receive the raw stream of events and reconcile the final data state independently. The key aspect is all the event handlers are reversible. This allows clients to insert locally generated events immediately. If any remote events are received out-of-order, the client can undo events, insert the new events, and reapply everything on top of the new state.

- 
- 
- 

- ### You may not need crdt
- https://twitter.com/aboodman/status/1663523389133434880
  - [LFW.dev/4 Meetup - YouTube](https://www.youtube.com/watch?v=7Bb0KRLL8FI&t=1892s)
  - Replicache and Reflect don't use CRDTs. 
  - Replicache is instead built on an older technique from multiplayer games. 
  - Turns out there's still a lot to love in that smooth old-school sync.

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

## 📝 [Some notes on Local-First Development_202309](https://bricolage.io/some-notes-on-local-first-development/)

- I see “local-first” as shifting reads and writes to an embedded database in each client via“sync engines” that facilitate data exchange between clients and servers. 
  - Applications like Figma and Linear pioneered this approach, but it’s becoming increasingly easy to do. 

- The benefits are multiple:
  - Simplified state management for developers
  - Built-in support for real-time sync, offline usage, and multiplayer collaborative features
  - Faster (60 FPS) CRUD
  - More robust applications for end-users

- What Approaches are People Exploring Now?
  1. Replicated Data Structures
  2. Replicated Database Tables
  3. Replication as a Protocol
# more
