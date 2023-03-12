---
title: lib-collab-crdt-algorithms
tags: [algorithms, collaboration, crdt]
created: 2023-03-07T04:43:40.023Z
modified: 2023-03-07T04:43:58.713Z
---

# lib-collab-crdt-algorithms

# guide

- tips
  - 更建议使用成熟的算法
  - 算法需要生态，如undo/redo、offline、versions、presence、server、room、轻量级实现、社区轮子
  - 学术界的代码大多都是玩具，经过业务产品验证过的更可靠
  - crdt算法修改版不会直接成为亮点，在业务有影响力后的亮点更大
  - https://github.com/pfrazee/crdt_notes
  - [A comprehensive study of Convergent and Commutative Replicated Data Types_201101](https://www.researchgate.net/publication/50949847)
  - [Building a BFT JSON CRDT](https://jzhao.xyz/posts/bft-json-crdt/)
  - [Visualization of different CRDT algorithms (including Yjs/YATA and Automerge/RGA)](https://text-crdt-compare.surge.sh/)

- 数据结构分析
  - 基础数据结构: map, array, text, set
  - id的结构，创建方式
  - insert op
  - delete op

- Oster
  - [Publications – Gérald OSTER](https://members.loria.fr/goster/publications/)
  - 2005年发布WOOT
  - 2017年发布Mute, 基于logoot变体

- gritzko
  - https://github.com/gritzko
  - citrea-model, 2012
  - swarm, 2013
  - chronofold, 2020
# crdt-algorithms

## RGA(Replicated Growable Array) / Causal Tree

- pros
  - less interleaving

- cons
  - tombstone

- who is using #crdt-rga
  - automerge
  - peritext
  - [Under the Hood of Spark Email Real-Time Collaboration](https://readdle.com/blog/under-the-hood-of-spark-email-real-time-collaboration)

- ?
  - timestamp如何计算的，插入时如何确定位置

- tips
  - insert依赖preceding元素的id/counter/timestamp，这可以有效避免interleaving
  - 

- https://github.com/pfrazee/crdt_notes
  - The Replicated Growing Array (RGA) implements a sequence as a linked list (a linear graph). 
  - It supports operations `addRight(v,a)`, to add an element containing atom a immediately after element v. 
  - 👉🏻 An element’s identifier is a timestamp, assumed unique and ordered consistently with causality, i.e., if two calls to now return t and t', then if the former happened-before the latter, then t < t'. 
  - If a client inserts twice at the same position, as in addRight(v, a); addRight(v, b), the latter insert occurs to the left of the former, and has a higher timestamp. 
  - Accordingly, two downstream inserts at the same position are ordered in opposite order of their timestamps. 
  - As in Add-Remove Partial Order, removing a vertex leaves a tombstone, in order to accommodate a concurrent add operation.
  - They illustrate an example in which timestamps are represented as a pair (local-clock.client-UID).

- RGA
  - Widely considered to be one of the fastest CRDT implementations. 
  - Utilizes a timestamped insertion tree and references hash table lookups for character lookups. 
  - Causal trees are a similar approach (named CT but in RGA it's called a timestamped insertion tree). 
  - In any case, CT/RGA algorithms have been proven to use the same algorithm

### [Operation-based CRDTs: arrays (part 1)](https://www.bartoszsypytkowski.com/operation-based-crdts-arrays-1/)

- A key observation of most (if not all) CRDT approaches to ordered sequences is simple: we need to be able to track the individual elements as other elements in collection come and go. 
  - For this reason we mark them with **unique identifiers**, which - unlike traditional array index, which can refer to different elements over time - will always stick to the same element.
  - While in literature they don't have a single name, here I'll call them **virtual pointers**.

- where LSeq virtual pointers use byte sequences, in RGA it's just a combination of a single monotonically increasing number and replica identifier
- In case of LSeq, virtual pointers where generated to reflect a global lexical order that matches the insertion order. 
  - They were not related ot each other in any other way. 
- 👉🏻 In case of RGA, pointers are smaller and of fixed size, but they're not enough to describe insertion order alone. 
  - Instead insert event refers to a preceding virtual pointer. 
  - For this reason we cannot simply remove them, since we don't known if another user is using them as reference point for their own inserts at the moment. 
  - Instead of deleting permanently, RGA puts tombstones in place of removed elements.
- because RGA insert relates to previous element - the sequences of our own inserts will be linked together, preventing from interleaving with someone else's inserts.
  - When initiating an empty RGA, we can put an invisible header at its head as a starting point
- PS: in this implementation, we're using an ordinary array of vertices, but in practice it's possible to split metadata and contents into two different structures and/or use specialized tree-based data structures (like ropes) to make insert/remove operations more efficient.

- how the insertion itself should look like? 
  - First we need to find an actual index, where a predecessor of inserted element can be found. 
  - Then just insert our element under next index. 

- 👉🏻 what if two actors will concurrently insert different elements after the same predecessor?
  - Again we'll use our virtual pointers, and extend them with one important property - we'll make them ordered (first by sequence number, then replica ID), just like in the case of LSeq. 
- Now the rule is: recursively, we shift our insertion index by one to the right every time when virtual pointer of the element living under that index already had a higher value than virtual pointer of inserted element.
  - 插入位置的id要比现有节点id大
- since our RGA is operation-based, we can count on the events being applied in partial order. 
  - B pointer's sequence number is equal or greater than Cs - that means that B has been inserted concurrently on another replica. 
  - In this case we also compare replica ID to ensure that virtual pointers can be either lesser or greater to each other (but never equal). 
  - This way even when having partially ordered log of events we can still guarantee, that elements inside of RGA itself will maintain a total order - the same order of elements on every replica.

### [Operation-based CRDTs: arrays (part 2) Block-wise Replicated Growable Array](https://www.bartoszsypytkowski.com/operation-based-crdts-arrays-2/)

- fit better into scenarios, where we insert and delete entire ranges of elements

### [Thinking about efficient backing stores for CRDTs](https://slightknack.dev/blog/backing-crdt-store/)

- Today, we’re going to focus on creating out an efficient backing store for a particular family of algorithms known as Replicated Growth Arrays (RGA).
- Under RGA, we represent documents as trees of strings. 
  - If this sounds familiar, that because it’s a bit like a Rope. 
  - To ensure that these trees always merge, we provide an algorithm for merging two trees together in a deterministic manner.
- The merging algorithm behind RGA is pretty elegant. 
  - Each character in the tree points to the one before it. 
  - If two characters have the same parent, we order them from back to front, the latest character going first (sorting by user in case of a tie).

- 💡 Note that although conceptually RGA operates on trees, **implementation-wise, (tree)it’s not a requirement**. 
  - Trees are an inefficient substrate(底层；基底) for RGA for a number of reasons, the largest being wasted space and the fact that they don’t play well with the L1 cache.
  - If we flatten the tree out into a list (still inefficient for other reasons), the RGA insertion algorithm discussed above looks something like this
- In the above example, we’re using a Rust Vec, which is a dynamically growable array. 
  - Vectors are really efficient in cache, but as mentioned, horrifically slow for insertion (which requires reallocation) or indexing by key (an O(n) linear search).
- 👉🏻 In light of this, a few people have come up with better backing data structures that exist to fill the gap. 
  - Most of these are build around Ropes or Range Trees.
  - These work great in practice, but still have some overhead when looking up entries by key or storing many small edits.

- I’ve been thinking about this issue for the past few days, and I think I have an interesting possible solution. 
  - I’m no expert, but I do have some experience with OT and optimization, so we’ll see how it goes. 
  - I’m calling this solution a Backed Tree Log, and it functions as an append-only log + a backing key-value tree for efficient key lookup.

### [Causal Trees and "ORDTs" · ipfs/notes](https://github.com/ipfs/notes/issues/405)

- a CT ORDT(op-based) and an RGA CRDT work pretty much the same. 
  - The mechanics map nearly 1 to 1.
  - The main difference is that RGA doesn't explicitly treat operations as fundamental units of data, nor the data structure as an event log. Everything is muddled together. 
  - RGA defines operations very similarly to a CT, as units of atomic data with timestamp+UUID metadata; 
  - but as soon as operations are received, their causality metadata is stripped and they're inserted into their final spot in the array. 
  - Similarly, delete operations immediately turn their targets into tombstones, which are later "purged" once all sites have received the deletion. 
- RGA is a very effective algorithm, but it doesn't make the logical leap of treating its data structure as an event log, even though that's what it is in practice. Traditionally, one would say that an RGA insert is applied and turned into data; but another way to look at it is that the insert operation is placed in the position of its intended output, then stripped of its metadata. ORDTs make this explicit.

### implementation

- https://github.com/maca/ace-crdt /js/rga
  - Collaborative text editor proof of concept using CRDT
- https://github.com/jorendorff/peeredit /201611/js/rga
  - This is example code for a talk on CRDTs.
  - 示例使用ace.v1编辑器

- https://github.com/josephg/simple-crdt-text /ts
  - This implements automerge's underlying algorithm (RGA)
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.

- https://github.com/gritzko/citrea-model
  - A CRDT-based collaborative editor engine of letters.yandex.ru (2012, historical)

- https://github.com/crdteam/causal-tree-ts
  - causal tree replicated data type (RDT) in Typescript.

- more-rga
  - https://github.com/ipfs-shipyard/peer-crdt/blob/master/src/types/rga.js
  - https://github.com/peer-base/js-delta-crdts/blob/master/src/rga.js

### more-rga

- [Replicated Growable Array / Causal Tree](https://replicated.cc/rdts/rga/)
  - Overall, RON 2.1 RGA/CT follows the classic RGA/CT data structure

- [Which algorithm y-array is using? · y-js/y-array](https://github.com/y-js/y-array/issues/9)
  - Yjs does not share any concepts with the RGA algorithm. 
  - If you want to compare it conceptually, Yjs is actually more similar to WOOT. 

- [CRDT: Tree-Based Indexing - Made by Evan](https://madebyevan.com/algos/crdt-tree-based-indexing/)
  - Compared to fractional indexing, tree-based indexing is more complicated but prevents interleaving of concurrently-inserted runs, which makes it appropriate for textual data. 
  - The algorithm presented here is similar to a well-known one called "RGA" but with reordering layered on top.

## json-crdt

### tips

- 考虑到数据源和持久化，通常会将json扁平化，normalize
  - 还要考虑编码解码
  - 扁平化后方便使用 lww + map

### [Shelf: a remarkably small, remarkably useful CRDT](https://braid.org/algorithms/shelf)
- A shelf is efficient, and guarantees consistency, with multiple writers in a P2P network. 
- A shelf supports most of JSON, however, it does not:
  - Support CRDT insertions or deletions in sequences (arrays/strings)
  - Distinguish null from undefined
- But many use-cases don't need those features. 

- Here is a shelf: `[VALUE, VERSION_NUMBER]`.
  - A shelf is an array with two elements: (1) `X`, and (2) some version number.
  - `X` can be a number or string or bool.. or.. a map (but not an array.. and if it's a string, we don't recurse into the string with our crdt, a string is atomic

- Shelves can be merged by VERSION_NUMBER, the bigger version wins
  - If the versions match, then it sorts the value, lower value wins

### [When using fixed data types for JSON CRDTs you can really reduce the amount of metadata needed.](https://twitter.com/JungleSilicon/status/1587070718688514048)

- Rather than storing path info, you can just store an index. You can also only store versions for the whole blob of the change.
- this is essentially just encoding a JSON CRDT as a list CRDT isn't it?? haha very smart
- I think of it as being similar to c structs and how they get flattened in memory.
  - I maintain the parent / child relationship so that child fields can be over written when a parent is changed too.
- It uses a flyweight pattern so that all of the documents can use the same type metadata as a lookup so you can avoid storing paths, parent data, etc.

- Adding type metadata to fixed-type crdts so it's easy to validate the changes that peers are making.
- https://twitter.com/JungleSilicon/status/1588313885458976768
  - This will include different crdt types so that more complex crdts are composable. (e.g. counters, lists, etc).
  - The idea is that all "documents" are JSON CRDTs and then each field can have more specialised CRDTs associated with them. When you override the field it will create a new CRDT in that slot.

- Ok so I've had a bit of an insight with fixed-type JSON-CRDTs.
- https://twitter.com/JungleSilicon/status/1594290808857202688
  - Since the type doesn't change, you don't need to store version information for containers (arrays & objects).
  - It's only the fields that need version information.
  - This means that you no longer need to send a parent version along with a field as the hierarchy has been flattened.
  - Since the fields have been turned into a set, you can run-length encode the fields.
- If you set the fieldIndices in a breadth-first way, then siblings will group together (e.g. position.x, position.y and position.z) when run-length encoded.
  - This also means that multiple changes to the same set of fields will be fast as you can set the version for a group.

- Using fixed-type json-crdts on the server is incredibly performant if you flatten the hierarchy.
- https://twitter.com/JungleSilicon/status/1594303337369079809
  - You don't actually need a JSON representation of the data, you just need to know which value is at each index.
- I was just thinking about this more and it feels super exciting. I imagined a semi-fixed type system where object type definitions get stored in CRDT and can change, changes happen on flattened objects but the type definitions can change over time

### [I feel somewhat limited by JSON working on CRDTs.](https://twitter.com/JungleSilicon/status/1580699240833372162) 

- I wish there was an easy way to associate metadata with an object or array without needing to wrap them in another object or array.
  - So currently this is annoying cos the version is an array and you also need to wrap objects in arrays to associate a version.

- We should chat, that’s exactly how we handle it in the @kosmik_app database
- Assuming you're in JS, doesn't Proxy solve this? Immer uses this extensively. Then you can build whatever metadata you want either by wrapping or some sidecar data structure and hide that from the user.
  - Eh, not really. They’re slow and don’t feel very good / consistent. Also it’s not about hiding the interface, it’s about the core data structure.

- Here’s a super simple example of versioning in a ‘shelf’ like syntax.
  - 经典json结构，value类型为数组 [val, clock]
- why not use flat map with path as key?
  - That's pretty gross. Not only do you get the slow down of needing to split / combine strings, you also need to store the full path of each field, you also lose hierarchical information so if you replace the object at "position", then finding the children to remove is harder.
- YMMV, working with normalized data is easier because everything can be thrown into a KV store. This does mean you will need an ORM to normalize and denormalize data; however, it also offers a cleaner abstraction as sync is now separate from managing app-level data-dependencies.

### [intro to json-crdt](https://twitter.com/JungleSilicon/status/1577523277207326720)

- `[seq, agentId]`: lamport clock with agentId as a tie-breaker
- each key stores a last-write-win register as value

- [A breakdown of many different techniques for constructing state-based JSON CRDTs.](https://twitter.com/JungleSilicon/status/1577123150696833025)

- a shared version per field
- flattened crdt with parent
- infer version by parent
- fixed type using index instead of path
- fixed type with versions

### impl

- https://github.com/siliconjungle/simple-fixed-json-crdt
  - https://github.com/siliconjungle/fixed-json-crdt
  - A json-crdt for fixed types of data. Very minimal data required.

- https://github.com/dglittle/shelf /发布在202110
  - a shelf: [VALUE, VERSION_NUMBER]
  - https://braid.org/meeting-8 (the shelf part with Greg starts at about 43 minutes in to the recording.)

- https://github.com/siliconjungle/cabinet
  - A key value store & subscriptions wrapping a json blob crdt (shelf).

- more-impl
  - https://github.com/automerge/automerge-classic
  - https://github.com/samuel-christian/json-crdts

### more-json-crdt

- [Shelf: easy way for recursive CRDT documents](https://www.bartoszsypytkowski.com/shelf-crdt/)

- [JSON-CRDT](https://github.com/ipfs/notes/blob/master/CRDT/json-crdt.md)

## Logoot/LogootSplit

- pros
  - no tombstone

- cons
  - interleaving

### tips

- who is using #logoot
  - mute
  - [DTNDocs: A delay tolerant peer-to-peer collaborative editing system_201801](https://ieeexplore.ieee.org/document/8343092)
    - DTNDocs Android application uses IBR-DTN to communicate over a delay tolerant network and a modified LogootSplit algorithm for ensuring consistency in shared contents.

- https://news.ycombinator.com/item?id=18193094
  - My hunch(预感；直觉) is that because CRDTs are so much easier to grok(通过感觉意会) than OT, engineers are empowered to make use case-specific improvements that aren't reflected in academic literature.
  - For example, the Logoot/LSEQ CRDTs have issues with concurrent insert interleaving; however, this can be solved by dedicating a bit-space in each ID solely for followup inserts.
  - The "Inconsistent-Position-Integer-Ordering" problem is solved by comparing ids level-by-level instead of in one shot.
- Additionally, the best CRDTs (like Logoot/LSEQ) don't require tombstones, garbage collection, or "quiescence." The complexity burden is far lower.
- To top it off, CRDTs are offline-capable by default.

### [LSEQ: an Adaptive Structure for Sequences in Distributed Collaborative Editing](https://hal.science/hal-00921633/en)

- In order to preserve the total order on the elements of the sequence, a unique and immutable identifier is associated with each basic element of the structure (character, line or paragraph according to the chosen granularity). 
- This allows distinguishing two classes of sequence CRDTs: 
- (i) Fixed size identifier (also called the tombstones class). 
  - This class includes WOOT [11], WOOTO [20], WOOTH [1], CT [7], RGA [13], [23]. 
  - In this class, a tombstone replaces each suppressed element. 
  - Although it enjoys a fixed length for identifiers and it has a space complexity which depends on the number of operations. 
  - For example, a document with an history of a million operations and ﬁnally containing a single line can have as much as 499999 tombstones. 
  - Garbaging tombstones requires costly protocols in decentralized distributed systems. 
- (ii) Variable-size identifiers. 
  - This class includes for example Logoot [21]. It does not require tombstones, but its identifiers can grow unbounded. Consequently, although it does not require garbage protocols, its space complexity remains till now linear with the number of insert operations. Thus, it is possible to have only a single element in the sequence having an identifier of length 499999. 
  - Treedoc [12] uses both tombstones and variable size identifiers but relies on a complex garbage protocol when identifiers grow too much.
- In this paper, we propose a new approach, called LSEQ, that belongs to the variable-size identifiers class of sequence CRDTs.
  - LSEQ is an adaptive allocation strategy with a sub-linear upper-bound in its spatial complexity. 
- We choose Logoot (for comparison) as it delivers overall best performances for variable-size sequence CRDTs

- The Logoot paper [21] already highlighted the importance of allocation strategies (alloc). 
- Indeed, experiments concerned two strategies. 
  - (1) Random: randomly choosing between the identifiers of the two neighbours. It delivers poor performance because the identifiers quickly saturate the space, resulting in the creation of new levels. As consequence, the size of identifiers grows quickly. 
  - (2) Boundary: randomly choosing between the identifiers of the two neighbours bounded by a boundary maximum value. The strategy allocates the new identifiers closer to their preceding identifier. Of course, it works well when the editions are performed right-to-left.
- LSEQ applies a very simple strategy: each time it creates a new level in the tree between two identifiers p and q, it doubles the base of this depth and it randomly chooses a strategy among boundary+ and boundary–.
  - boundary+ allocates from p plus a fixed boundary, boundary– allocates from q minus a fixed boundary. 
  - The boundary never changes whatever the depth of the tree.

- Logoot’s [21] underlying allocation strategy always uses the same base to allocate its identifiers. 
  - With regard to the tree representation, it means that the arity is set to base.
- A high base value is not profitable if the number of insert operations in this part of the sequence is low.
  - On the contrary, keeping a constant base value when the number of insert operations starts to be very high does not allow to fully benefit of the boundary strategy.
- the objective is to adapt the base according to the number of insertions in order to make a better reflection of the actual size of the document. 
  - Since it is impossible to know a priori the size of the document, the idea is to start with a small base due to the empty sequence, and then to double it when and where necessary, i.e. when the depth of identifiers increases.
- Doubling the base at each depth implies an exponential growth of the number of available identifiers. 
  - Thus, the model corresponds to the exponential trees and consequently it benefits of their complexities. 

- The variable-size identifiers class of CRDT includes Logoot [21] and Treedoc [12]. 
- These CRDTs use growing identifiers to encode the total order among elements of the sequence. 
  - In the worst case, the size of identifiers is linear in the total number of insert operations done on the document [1]. 
- Logoot and Treedoc [12] have different allocation strategies. 
- Treedoc has two allocation strategies: 
  - (i) the first strategy allocates an identifier by directly appending a bit on one of its neighbour identifier. 
  - (ii) The second strategy increases the depth of this new identifier by ⌈log2(h)⌉+1 (where h is the highest depth of the identifiers already allocated) and allocates the lowest value possible with this growth, in prevision of future insertions. 
- Logoot’s boundary strategy and Treedoc’s second strategy are very similar, both in their goals and their weaknesses. 
  - They assume an editing behaviour in the end, and therefore they become application dependent. 
- Compared to Logoot and Treedoc, LSEQ is adaptive and significantly enlarges the applicability of sequence CRDTs.

- In this paper, we presented an original allocation strategy for sequence CRDTs called LSEQ. 
  - Compared to state of art, LSEQ is adaptive, i.e., it handles unpredictable different editing behaviour and achieves sub-linear space complexity. 
  - Consequently LSEQ does not require a costly protocol to garbage or re-balance identifiers, and is suitable for building better distributed collaborative editors based on sequence CRDTs.
- Three components compose LSEQ: 
  - (1) a base doubling, 
  - (2) two allocation strategies boundary+ and boundary–, 
  - (3) a random strategy choice.
  - Although each component cannot achieve sub-linear complexity, the conjunction of three components provides the expected behaviour.

### TreeDoc: A Commutative Replicated Data Type for Cooperative Editing

- Logoot uses a sparse n-ary tree rather than Treedoc's dense binary tree. 
  - A position identifier is a list of (long) unique identifiers, and Logoot does not flatten.

- A Logoot position identifier is a sequence of fixed-sized unique identifiers.
- Position identifiers are ordered in lexicographical order of their components. 
- Logoot allocates position identifiers sparsely in order to facilitate insertions. 
- To insert, Logoot allocates a free unique identifier ordered between the left and right position identifiers, if one exists; otherwise it extends the identifier of the left position with an additional layer. 
- A deleted atom can be removed immediately, but Logoot does not flatten the tree.

### [Collaborative text editing with Logoot_201712](https://medium.com/@ravernkoh/collaborative-text-editing-with-logoot-a632735f731f)

- To collaborate in a document, the naive approach would be to send over each operation a user performs to all other users editing the document. 
  - when network latency becomes significant, it is incredibly easy to achieve race conditions like this one.
- When using CRDTs instead of OT, we are trading time complexity for space complexity. 
  - This means that while OT will take more time to process than CRDTs, CRDTs will usually end up using significantly more memory than OT.

- it assigns unique identifiers to each character/group of characters in the document, and performs the insertions and deletions based on the position of these identifiers.
- In Logoot, the document is split up into groups of text. 
- A group of text is called an **atom**. 
- Each atom is given a unique identifier, or a uid
- Each uid is comparable to other uids. 
- The document is then stored as an array of (uid, atom) pairs, sorted by the uids within the pairs in ascending order. 
- There will also be two special, blank lines that exist in every document. 
  - One at the very start which will have the MIN_uid, and at the very bottom, which will have the MAX_uid.

- the most important part
  - 👉🏻 For any two different uids, you should always be able to find a uid in between them. 
- using integers as uids does not adhere to the property 
  - what about floats? 
  - However, in the context of a computer, this isn’t possible. 
  - Floating point numbers are simply approximations of real numbers, which means that it’s not always possible to find a floating point number between any two floating point numbers.
  - Simply put, you cannot represent an infinite number of floating point numbers in just 32/64-bits.
- So how are these uids represented? 
  - The answer is lists. 
  - A uid is represented by a list of integers. 
  - Let’s say we have the uids [4] and [5] 
  -  In order to find a uid in between [4] and [5], we can simply make a longer list, that starts with a 4 (e.g. [4, 8])
  - in Logoot, uids are represented by lists of integers.

- In Logoot, a document is made up of an array of pairs. 
  - Each pair containing a uid, and an atom. 
  - An atom is simply a string, containing some of the content in the document. 
  - The pairs in the document are always sorted by their uids. 
  - To get the content of the entire document, simply concatenate all the atoms in order. 
- To perform an insertion, you simply need to have the pair to insert. 
  - To generate the uid for the pair, you simply have to take two existing uids and generate a random uid in between them.
- To perform a deletion, you only need to know the uid to delete.
- to insert in a blank document, the start and end lines are two lines that always exist in a Logoot document. 
  - They contain an empty atom and their uids are 0 and MAX respectively, where MAX is the maximum size of an integer.

### implementation

- https://github.com/mkdynamic/logoot
  - Collaborative text editor using Logoot CRDT algorithm. 
  - Adds an informal versioning scheme based on state vectors to ensure casual ordering of operations is maintained.

- https://github.com/t-mullen/logoot-crdt
  - Implemented as a tree for fast character position lookups.

- https://github.com/nybblr/logoot /js
  - Test-driven implementation of the Logoot CRDT, with LSEQ strategy and a healthy distaste for mutation.

- impl
  - https://github.com/usecanvas/logoot-js /js
  - https://github.com/bnoguchi/logoot /js
  - https://github.com/ravern/logoot /go

### more-logoot

- [Conflict-Free Replicated Data Types (CRDT) for Distributed JavaScript Apps. - YouTube](https://www.youtube.com/watch?v=M8-WFTjZoA0)
  - lsql, logoot

- [Introduction to CRDTs for Realtime Collaboration - DEV Community](https://dev.to/nyxtom/introduction-to-crdts-for-realtime-collaboration-2eb1)
  - Logoot/LSEQ/TreeDoc does not store tombstone deletions and instead takes an approach with fractional/unbounded divisible indexing. 
  - This, as discussed earlier, can cause issues with interleaving edits so it becomes impractical to guarantee proper sane convergence with concurrent operations.

- [An Elixir implementation of the Logoot CRDT](https://hexdocs.pm/logoot/readme.html)
  - Because of how these atom identifiers are structured, they are totally ordered, as opposed to causally ordered. 
  - No identifier cares about the identifier before it once it’s been created, and so tombstones are not necessary.

- [A simple approach to building a real-time collaborative text editor_201710](https://digitalfreepen.com/2017/10/06/simple-real-time-collaborative-text-editor.html)
  - I adapted Logoot

- [Interleaving anomalies in collaborative text editors](https://martin.kleppmann.com/2019/03/25/papoc-interleaving-anomalies.html)

## WOOT

- pros
  - simple

- cons
  - tombstone
  - ? interleaving

- 业务产品并不多，参考fro scala.js

### all-phedkvist-crdt

#### [Collaborative Editing Using CRDTs WOOT](http://www.pierrehedkvist.com/posts/collaborative-editing-using-crdts)

- A collaborative editor consists of several components, a text editor, a model which can solve any conflicting updates, and a communication layer that can send updates to and from users.

- If you think of text being edited, it's easy to think in terms of indexes.
  -  A problem appears because they apply the operations in different orders, which makes their copy of the document diverge into different states.
- WOOT will instead describe a character by the identifier of its neighbors. 

- The document itself is stored in a sequence of W-characters. 
  - In my implementation I used an array for this.

- A W-character c is a five-tuple
  - id is the identifier of the character (site id, unique natural number).
  - value is the alphabetical value of the character.
  - visible indicates if the character is visible/deleted.
  - idcp is the identifier of the previous W-character of c.
  - idcn is the identifier of the next W-character of c.
- So the position of the character is determined by its neighboring characters, and not any numerical index. 
- the visible boolean, which says whether or not a character has been deleted, as deleted characters are kept in the state, as tombstones. 
  - This is one downside of some CRDTs, as deleted characters needs to stay in the sequence.
- The id of a character consists of the site id (id of the site that produced the character), and a natural number, which increments after every update.
  - The natural number is just a local clock that increments on every change, the site id stays the same. 
  - This will later be used to know at what point in time the edit was being made. 
  - It can also be used to identify which character a certain user might be missing from the others users.

- To locally insert a character, all that is needed is to create W-character and add the neighboring visible characters id to `idcp` and `idcn`. 
  - Then broadcasting this operation to other sites. 

- Generating a delete operation is easy, just find the character among the visible ones, and mark it as deleted and broadcast to other sites.

- The tricker operation is integrating inserts from other sites. 
  - The algorithm has to find the right position between the previous and next character. 
  - There could potentially be characters that have already been added in between these two characters, or either one of them could have been removed already. 
  - The algorithm will take a subsequence of the characters between idcp and idcn, if its empty it can be inserted here. 
  - Otherwise it will sort all characters and find a smaller subsequence where the character belongs, and make a recursive call until its found its place in the sequence.

- interleaving
  - Another interesting property that comes up when dealing with collaborative editing algorithms is something called interleaving. 
  - It can happen when multiple users are editing characters that are in close proximity to each other, where the text is intertwined when its synchronized. 
  - In such a scenario, the document look something like this.
- This is of course not the intent of either user, since the sentence looks really strange. 
  - But technically the document has the same state. 

- Communication layer
- In order to keep all sites in sync with each other, they need to communicate and let each other know their current state. 
  - This can easily be solved by using version vectors. 
- The version vector can be stored at each site, it will contain how many updates it has received from other sites. 
  - Bob will have his own version vector, which says how many number of updates he has received from Alice and vice versa. 
  - They can then simply just send these to each other and sync changes that way. 
  - Or a central server can keep all users up to date.

- Mathematics behind CRDTs
- CRDTs follow certain mathematical properties that ensures any potential conflicts will be resolved. 
- If you have heard of CRDTs before, you probably have come across join semi-lattices. 
  - Which might sound intimidating, but this concept originates from order theory, which is based on simple mathematics. 
  - An order is a binary relation, for example 1 is less than 2. 
  - You can also think of it in terms of son <= father. Combine this with the commutative and idempotent properties, you will get a semi-lattice.
- Lattice（格）
  - ​ 如果一个偏序集中任意两个元素都有最大下界和最小上界的话，我们就可以将这个偏序集称之为一个格，
  - 可见格的概念是包含在偏序集中，也可以说一部分特殊的偏序集也就是格。
- Semilattice（半格）
  - 给定一个偏序集，对于任意的a和b，如果只有最大下界存在，那么可以称为`meet-semilattice`，如果只有最小上界存在，那么可以称为`join-semilattice`，就是只满足格的一半性质的偏序集。
  - the join semi-lattice is following the commutative and idempotent properties.
- Complete Lattice（全格） 
  - 全格的所有的子格都有最小上界和最大下界，有穷格是全格，无穷（没有边界）一般都不是全格。
  - 全格一定有穷吗？ 不一定，如实数界[0, 1] 
  - 每个全格都有Top和Bottom。
- A good structure for explaining a join semi-lattice is by using a vector clock.
  - Its a vector containing timestamps, each element is a number.
  - look this (1, 4, 2)
  - If Alice, Bob and Charlie were to write a collaborative editor, each item in the vector clock could represent the number of operations that particular user has contributed to the system. 
  - each user has their own version vector, which keeps track of the changes it has.
  - This vector clock can then be used to figure out which operations are missing in any of the users system.
- This means that the vector clocks, can be different to one another, but when receiving the missing updates, the vector clocks should eventually have the same value, and the state will converge.
- A join semi-lattice follows the following properties.
  - Commutative: (a ∪ b)= (b ∪ a)
  - Associative: (a ∪ b) ∪ c) = (a ∪ (b ∪ c))
  - Idempotent: (a ∪ a) = a
- Here, ∪ is the union operation, but it can be replaced by other binary operations, such as max, min. 
- The version vectors above takes the maximum value of every element in the vector, in order to arrive at the desired state.

#### [Creating a Collaborative Editor using Sequence](http://www.pierrehedkvist.com/posts/1-creating-a-collaborative-editor)

- A CRDT Sequence can be represented as a sequence of characters in a list, where each character has a unique global index. 
  - Meaning the index will be the same for all users. 
  - We have a list, and it will be the same for all users, 
  - even if two users make an insert at the same index, a “conflict” occurs, 👉🏻 the tiebreaker is solved by figuring out which user has the **lowest** user id. 
  - So each user is given a unique user id (UUID), that solves any conflict.
  - 可以约定，userId小的插在前面，userId大的插在后面

- The deletion of characters in a CRDT Sequence is very simple. 
  - By marking a character as removed, using a tombstone, the character can simply not be rendered in the editor. 
  - But the character is still present in the CRDT Sequence. 
  - It can not yet be removed since the CRDT is bound by mathematical properties that must be followed.
- The obvious downside of this is that our document might potentially be filled with a bunch of characters that are removed, but not seen in the editor, causing unbounded memory growth.

- While these operations are occurring we have to keep in mind that users might be disconnected from the server. 
  - Therefore it's necessary to be able to bring the user back to a consistent state when they connect again. 
  - 👉🏻 Version Vectors can be used to solve this problem. 
  - Its a vector that counts how many changes are made by each user. 
  - Each user stores their own local version vector. 
  - This vector can be compared with other vectors to see which changes are missing and needs to be sent to some user.

- Implementation
- onChange (Intercept text changes): In order to capture changes made in the text editor, which is translated into CRDT Characters that can be sent to other users.
- Changes made to the text editor needs to be translated into its equivalence in the CRDT model. 
- Once a user receives a change, it will first apply the change to its own CRDT Sequence. Then the CRDT Sequence can tell the rich text editor to apply the change to the editor.
- Whenever a user removes a character, in the editor, the index will be translated into the equivalent index in the CRDT Sequence and set the tombstone to true.

- https://github.com/PHedkvist/crdt-sequence
  - 自己实现了 history、activeUsers
  - quill的功能使用得很少
  - dev-to
    - 多人光标待改进
  - https://github.com/PHedkvist/crdt-server

### implementation

- https://github.com/d6y/wootjs /scala.js
  - WOOT is a collaborative text editing algorithm, 
  - allowing multiple users (`sites`) to insert or delete characters (`WChar`) from a shared document (`WString`).
  - The algorithm preserves the intention of users, and ensures that the text converges to the same state for all users.
  - Its key properties are simplicity, and avoiding the need for a reliable network or vector clocks (it can be peer-to-peer).

- https://github.com/ryankaplan/woot-collaborative-editor
  - When a textarea-change is detected, diff the textarea content against the last known content. 
  - With the help of WootTypes. WString, turn that diff into `WStringOperations` and broadcast those operations to the server.
  - When we receive operations from the server, apply those operations to our WString instance and apply them to the text in #collab-doc.

### more-woot

- [WOOT: an Algorithm for Concurrent and Collaborative Authoring (2013) [video] | Hacker News](https://news.ycombinator.com/item?id=10677667)

## LSEQ

- cons
  - interleaving

- In case of LSeq these identifiers are represented as sequences of bytes, which can be ordered in lexical order

```JS
// example of lexically ordered sequence
a => v1
ab => v2
abc => v3
b => v4
ba => v5
```

- Since no generator will ever guarantee that byte sequences produced on disconnected machines are unique 100% of the time, the good idea is to make virtual pointer a composite key of byte sequence together with unique replica identifier (using replica ID to guarantee uniqueness is quite common approach). 
- In order to insert an element at given index, in LSeq we first need to find virtual pointers of elements in adjacent indexes, then generate new pointer, which is lexically higher than its predecessor and lower than its successor
  - There are many possible ways to implement such generator - the trivial one we're going to use is to simply compare both bounds byte by byte and insert the byte that's 1 higher than a corresponding byte of the lower bound, BUT only if it's smaller than corresponding byte of the higher bound
- One issue of LSeq data type is how it deals with concurrent updates interleaving.
  - This problem can be solved (or at least amortized) in theory: we just need to generate byte sequences in a "smart way", so that elements pushed by the same actor one after another will land next to each other after sync. Problem? So far no one presented such "smart" algorithm.

## TreeDoc

- pros
  - no interleaving

- cons
  - unbalanced tree is bad for query

- uses a binary tree to represent the document

- https://github.com/mweidner037/uniquely-dense-total-order
  - [Plain Tree: A Basic List CRDT](https://mattweidner.com/2022/10/21/basic-list-crdt.html)
    - The rest of this post introduces a basic UniquelyDenseTotalOrder that I especially like. 
    - I have not seen it in the existing literature, although it is similar enough to Logoot, Treedoc, and others that I wouldn’t be surprised if it’s already known. For now, I call it Plain Tree.

- Logoot and TreeDoc used variable-length identifiers.

- [CRDT: Tree-Based Indexing - Made by Evan](https://madebyevan.com/algos/crdt-tree-based-indexing/)
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [CRDT: Fractional Indexing_202211](https://news.ycombinator.com/item?id=33764449)
- I’m not the GP, but OT is pretty annoying to implement. There are so many cases that it’s quite difficult to formally prove an OT correct. On the other hand, a large subset of CRDTs can be implemented in Datalog and if you do that you can’t possibly end up with an invalid CRDT.
- This is basically the idea behind Logoot [Weis_2009] that was improved by LSeq [Nédelec_2013] and later extended to the first block-wise sequence CRDT: LogootSplit [André_2013]. LogootSplit was recently improved as Dotted LogootSplit [1] [Elvinger_2021].
