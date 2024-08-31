---
title: lib-collab-crdt-blog-stars
tags: [blog, crdt]
created: 2023-03-11T15:37:35.868Z
modified: 2023-03-11T15:37:59.134Z
---

# lib-collab-crdt-blog-stars

# guide

# blogs-fractional-index

## 🧮 [CRDT: Fractional Indexing - Made by Evan _202211](https://madebyevan.com/algos/crdt-fractional-indexing/)

- [Realtime Editing of Ordered Sequences - Made by Evan _201703](https://madebyevan.com/figma/realtime-editing-of-ordered-sequences/)

- Collaborative peer-to-peer applications sometimes need to operate on sequences of objects with a consistent order across all peers. 
  - Unlike my original article about this technique, the algorithm presented here uses random offsets to avoid requiring a central server, and works in true peer-to-peer scenarios.
- Compared to tree-based indexing, fractional indexing is simpler but doesn't prevent interleaving of concurrently-inserted runs, which makes it inappropriate for textual data.

### [CRDT: Tree-Based Indexing - Made by Evan _202211](https://madebyevan.com/algos/crdt-tree-based-indexing/)

- Compared to fractional indexing, tree-based indexing is more complicated but prevents interleaving of concurrently-inserted runs, which makes it appropriate for textual data. 
- The algorithm presented here is similar to a well-known one called "RGA" but with reordering layered on top.

## 👥🧮 [CRDT: Fractional Indexing _202211](https://news.ycombinator.com/item?id=33764449)

- 👷🏻jitl: To me the other algorithms described in the list are more novel and interesting:
  - crdt-tree-based-indexing/ - for when precise order is critical, like paragraphs in a document. This algorithm is almost like storing adjacency information like a linked list, but is more convergent. 
  - crdt-mutable-tree-hierarchy/ - for tree-shaped data, like blocks in a Notion page that should have exactly one parent, but allow concurrent re-parenting operations
  - log-spaced-snapshots/ - log space snapshots, for choosing what fidelity of historical information to store. For context, many CRDTs for rich text or sequences store unbounded history so that any edit made at any time can be merged into the sequence. For long-lived documents, this could be impractical to sync to all clients or keep in "hot" memory. Instead, we can decide to compact historical data and move it to cold storage, imposing a time boundary on what writes the system can accept on the hot path. The log-spaced snapshots algorithm here could be used to decide what should be kept "hot", and how to tune the cold storage.
- do you have thoughts on the CRDT vs OT debate? 
- I’m not the GP, but OT is pretty annoying to implement. There are so many cases that it’s quite difficult to formally prove an OT correct. 
  - On the other hand, a large subset of CRDTs can be implemented in Datalog and if you do that you can’t possibly end up with an invalid CRDT.

- CRDTs are often talked about in the same breath as collaborative editing software, but they're useful for much more than that. They really are a theoretical model of how distributed, convergent, multi-master systems have to work. 
  - IE the DT in CRDT could be a whole datastore, not as just an individual document.

- 🧮 This is basically the idea behind Logoot [Weis_2009] that was improved by LSeq [Nédelec_2013] and later extended to the first block-wise sequence CRDT: LogootSplit [André_2013]. LogootSplit was recently improved as Dotted LogootSplit(MPLv2/201907) [Elvinger_2021].
- Is this the same as LSeq except rather than using bytes one is basically using digits in a floating point representation (given this is JS where most things are floats)?

- This is kind of interesting but "fractional indexing" doesn't seem to be a computer science topic, and I think it might be clearer to treat these indexes as lists of numbers (or ordinals in ω^ω, if you prefer) rather than fractions. 
  - Those are simpler to generate and compare than arbitrary-precision fractions. Or as jitl's post suggests, using trees as indexes (I haven't yet looked at jitl's linked articles). Those would presumably have order type. 
  - It's not clear to me why you'd want that, but it seems doable. In all these schemes you might occasionally want a "stop the world garbage collection" where you reset all the indices to be ordinary integers or maybe pairs of integers. I guess that is also doable without having to pause all the updates, at least if you use pairs.

- Reminds me a little of "Lexorank" used in Jira, except by using decimals instead of base-36 strings, which I guess could be more efficient? The "rebalancing" aspect is interesting because on a long enough timescale for a document you will definitely want to do it. Would love to read up more on any algorithms for doing this in a p2p manner - with a central server it's probably quite easy using some tombstoning or something.

- reminds me a lot of Ford Circle / Farey Diagram / Stern Brocot tree Basically a tree of fractions where you take two rational points on a number line, a/b and c/d, then the next point in the tree is (a+b) / (c+d). Turns out that every single point you create this way has a unique position and never duplicate each other, and it forms a tree like structure.

- The algorithm exposed in the article would be better served by a Stern-Brocot than average + jitter.

- Doesn't this end up being effectively a binary heap, with a maximum tree depth of 23 (floating point mantissa precision)? I imagine there must be a rebalancing operation required every so often, possibly more frequently for pathological insertion orders.
  - > Fractional positions should be represented using arbitrary-precision decimals so that they don't run out of precision. Floating-point numbers are insufficient.

## [Reordering Part 2: Tables and Fractional Indexing - Steve Ruiz _202202](https://www.steveruiz.me/posts/reordering-fractional-indices)

- In a previous blog post, we looked at implementing four common reordering commands in a zoom UI or canvas app. Those commands are:
  - Send to Back
  - Send Backward
  - Bring Forward
  - Bring to Front
- While the last post showed how we might implement these commands when our items were stored in an array, this post will focus on the more complex implementation for cases where items are stored in hash tables.

- Let's say we have an application where we're storing items in a hash table—in JavaScript, a regular object. 
  - Because tables (unlike arrays) have no "position" or index for items in the table, we'll need to keep track of that information ourselves.
  - each item's `index` is stored as a property using number.
- 🤔 How should we implement changes to our `index` properties? 
  - A simple approach could reproduce the same index logic as in an array, re-assigning each item's index whenever a reorder occurs.
  - The problem with this approach is that making a change to one item's order might mean making a change to all items in the stack. 
  - This strategy could lead to excessive writes to a database, or larger packets being sent to ensure consistency between users in a multiplayer session, and even unnecessary renders depending on how changes are observed.
  - What we really want is a method that ensures that only the moving items will require new index values.
- The strategy we'll be using is called "fractional indexing", common in databases but introduced to me by Figma's article on the topic.
  - In this strategy, an `index` only needs to ensure that, when our items are sorted by their index, the items end up in the right order. 
  - The index values themselves do not have to be integers or evenly distributed—all that matters is that they let us produce the correct sort.
- Fractional indexing makes reordering operations much cheaper in terms of writes to the document or database, as we only need to mutate the items that have actually moved.
  - There is one issue, however, and you may have spotted it already: how many times can you divide a number before the difference is less than your program's floating point precision? With the implementation shown here, that number is 52.
- Better Indexing! The solution to this is to use a more accurate index.
  - At the moment we're sorting based on the greater of two numbers; however, we can also sort alphabetically.

## 🧮 [Fractional Indexing – vlcn.io](https://vlcn.io/blog/fractional-indexing)

- To enable user provided ordering of rows, most people reach for a fractional index. 
  - They're great given they let you change the position of one row without modifying any other rows. 
- Fractional indices have a number of gotchas, however.
- 🐛 Precision
  - You might think 52 bits of precision (for JS floats) would be plenty to continuously insert between two items. Since inserts divide the space by 2, you will actually run out of precision after 53 insertions in the wrong spot.
- 🐛 Collisions
  - In a distributed setting, fractional indices have problems when it comes to nodes assigning items the same orders.
- 🐛 Interleaving
  - Since each node is assigning orders to items independently, this can cause unwanted interleaving of data. 

- Fixing the Gotchas
- 💡 Precision & Exponential Index
  - To prevent exponential growth of your fractional index, insertions at the end should be whole increments and insertions at the beginning should be whole decrements.
  - You can also use a variable length encoding for your fractional index to compress away repeating numbers
- 💡 Collisions
  - A proposed workaround for collisions is to add random jitter to your index. 
  - Jitter(晃动, 抖动; 偏移), unfortunately, can still lead to a collision and will increase the space of your index.
  - The other workaround is to allow collisions
  - This is implemented in cr-sqlite here.
- 💡 Interleaving
  - To fix interleaving we will part ways with fractional indexing and instead sort based on recursive relationships between rows. You can read about this in recursive ordering.
  - there are other approaches to fix interleaving

## [Building Conclave: a decentralized, real time, collaborative text editor _201801](https://medium.com/hackernoon/building-conclave-a-decentralized-real-time-collaborative-text-editor-a6ab438fe79f)

- Conclave is a decentralized, real time, collaborative editor for the browser. 
- Relative positions are the key concept that differentiates a CRDT from OT. The positions of characters in a CRDT never change even if the characters around them are removed. Furthermore, the relative position can always be used to determine the location of the character in the document.
  - Fractional positions as arrays of integers.

- Version Vector is simply a strategy that tracks which operations we have received from each user.
  - Whenever an operation is sent out, in addition to the character object and the type of operation (insert/delete), we include the character’s Site ID and Site Counter value. The Site ID indicates who originally sent the operation and the Counter indicates which operation number it is from that particular user.

- https://github.com/conclave-team/conclave /MIT/202106/js/lseq/inactive
  - https://conclave-team.github.io/conclave-site/
  - CRDT and WebRTC based real-time, peer-to-peer, collaborative text editor
  - 示例使用simplemde、rxjs、peerjs
  - Intrigued by collaboration tools like Google Docs, we set out to build one from scratch. 
  - Conclave uses (CRDT) to make sure all users stay in-sync and WebRTC to allow users to send messages directly to one another.
  - We implemented an “adaptive allocation strategy for sequence CRDT” called LSEQ(exponential tree).
  - Similar non-academic implementation with optimizations and tweaks - based on Logoot/LSEQ.

- [Building Conclave: a decentralized, real time, collaborative text editor | HackerNoon _201712](https://hackernoon.com/building-conclave-a-decentralized-real-time-collaborative-text-editor-a6ab438fe79f)

## 🧮 ["Position Strings" for Collaborative Lists and Text _202304](https://mattweidner.com/2023/04/13/position-strings.html)

- it provides “position strings” for use in collaborative lists or text strings. 
  - Each position string points to a specific list element (or text character), and the list order is given by the lexicographic order on position strings.
- position-strings is supposed to make it easy to add list/text CRDT functionality to an existing data model, such as a database table. 
- Unlike most CRDT implementations, position-strings doesn’t “own” the list state or store extra metadata; 
  - instead, you are free to store the positions and chars (or list values) wherever you like.
  - For example, you could store each { position, char } as a row in a cloud-synced database like Firebase Realtime DB - I provide an example app that implements collaborative text editing this way.
- You can also think of position-strings like fractional indexing, but with a few extra features: global uniqueness, non-interleaving, and slower (logarithmic) length growth in sequences.

- The catch is that a list/text CRDT using `position-strings` will have more storage and network overhead than a dedicated data structure like `Y.Array`
- Under the hood, position-strings uses an optimized version of `Fugue`’s string implementation. 

## [Fugue(Plain Tree): A Basic List CRDT _202210](https://mattweidner.com/2022/10/21/basic-list-crdt.html)

- This post was previously titled “Plain Tree: A Basic List CRDT”. 
  - Since posting, I and Martin Kleppmann wrote a paper about this list CRDT and renamed it Fugue.

- In this post, I describe Fugue, a basic List CRDT that I find fairly easy to understand, plus some simple implementations. My goal is that you will also understand it, filling in a gap from my previous post. 
  - Despite its simplicity, the CRDT described here is my preferred List CRDT. 
  - In particular,  `Collabs` uses it for all list implementations.

- 
- 
- 

# blogs-comparison

## [A comparison of JS CRDTs - (not my) ideas _202403](https://blog.notmyidea.org/a-comparison-of-javascript-crdts.html)

- The goal here is not to tell which one of these libraries is the best one. They’re all great and have their strenghs. None of them implement the high-level API I was expecting, where the clients talk with each other and the server just relays messages, but maybe it’s because it’s better in general to have the server have the representation of the data, saving a roundtrip for the clients.

- 
- 
- 

## 🆚️🔀 [Trade-offs between Different CRDTs | Hacker News](https://news.ycombinator.com/item?id=38916647)

- This is a clear and crisp way of differentiating delta based vs state based CRDTs.
  - But I don't think it's accurate enough. For example, the article claims delta based CRDTs don't use vector clocks. But even to decide if a set of events are concurrent it's necessary to attach vector stamps to every event. Maybe the author meant something else when he says vector clocks are not needed for op based CRDTs.
  - Also as mentioned in article it's true evergrowing event log is not such a bad idea with compression techniques and cheaper disks. But the problem with evergrowing datastructures is not just disk space. This data has to be loaded onto main memory to do anything useful with it. This data has to be transmitted across network to power SaaS apps. So stating that disks are cheaper hence evergrowing datastructures are fine - is an oversimplification.

- I don't recall if it was git itself or github that bragged about inverting the storage structure so that it was simplest to read the current state, and HEAD~3 was determined by substracting the last 3 patches rather than fast forwarding from root to length - 3.
  - There absolutely is. I’m writing a paper at the moment about how we’ve done this in diamond types. The core idea is to store the original operations and the versions. And then reconstruct the crdt state on each peer as needed. Because most editing histories are mostly linear, it usually ends up faster than CRDTs in practice anyway. But you can then just send the latest document state and send historical operations on demand for merging and to access old document states.
# blogs

## [Store the history and the state of CRDTs in a KV store _202403](https://twitter.com/zxch3n/status/1772864473348653162)

- Git is built on top of its own KV store to store the history of edits. 
  - We can probably do similar things for CRDTs libs like @loro_dev and Automerge, where we can extract the history(all the operations) of CRDTs into a separate KV store and load them lazily. 
  - 🆚️ The differences are Git uses the hash as keys, CRDTs should use the id of the ops as keys, and they tend to have significantly more entries than Git because they treat every keystroke as a separate version.
- Document states can also be persisted in the KV store, enabling scenarios like spreadsheets with millions of cells or storing the entire Git repo inside a single "CRDTs document." 
  - This would make these CRDTs libs more like embedded databases. There are many exploratory works to be done, but I'm excited about its potential.

- This would make these CRDTs libs more like embedded databases. There are many exploratory works to be done, but I'm excited about its potential.

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

## 👥 [You might not need a CRDT | Hacker News _202212](https://news.ycombinator.com/item?id=33865672)

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

- ⚡️💥 We have used Automerge a bunch, but found that there is a threshold where beyond a given document size, performance gets exponentially worse, until even trivial updates take many seconds' worth of CPU. 
  - That is often how it works when the document end state is exclusively the sum of all the edits that have ever happened.
  - Our answer was to reimplement the Automerge API with different mechanics underneath that allows for a "snapshots + recent changes" paradigm, instead of "the doc is the sum of all changes". That way performance doesn't have to degrade over time as changes accumulate.
  - Project is here: https://github.com/frameable/pigeon
- This is an implementation problem with automerge. I wrote a blog post last year about CRDT performance. I re-ran the benchmarks a couple months ago. Automerge has improved a lot since then. I've had a chat with some of the automerge people about it. They're working on it, and I've shared the techniques I'm using in diamond types (and all the code). Its just an implementation bottleneck.

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
