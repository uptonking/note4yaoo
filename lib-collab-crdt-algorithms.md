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

- crdt-text
  - 能不能将协作的粒度从字符提升为句子
  - 或者crdt-text-by-lines, still sequence crdt，参考typewriter-quill
# crdt-experts
- Kevin Jahns, yjs
  - https://github.com/dmonad
  - https://github.com/yjs/yjs
  - port到各种语言

- Martin Kleppmann, automerge
  - https://github.com/ept
  - [blog posts](https://martin.kleppmann.com/archive.html)
  - [crdt.tech](https://crdt.tech/)

- Oster, woot/logoot
  - [Publications – Gérald OSTER](https://members.loria.fr/goster/publications/)
  - 2005年发布WOOT
  - 2017年发布Mute, 基于logoot变体

- gritzko, swarm/chronofold
  - https://github.com/gritzko
  - citrea-model, 2012
  - swarm, 2013
  - chronofold, 20 20

- Seph Gentle, sharedb/diamond-types
  - https://github.com/josephg
  - https://github.com/josephg/diamond-types
# crdt-algorithms
- rga: linked-list or tree
- fractional-index
- logoot
  - sparse n-ary tree
- treedoc/2009
  - binary tree
- lseq/2013
  - exponential tree

## RGA(Replicated Growable Array) / Causal Tree

- pros
  - less interleaving

- cons
  - tombstone

- who is using #crdt-rga
  - automerge
  - peritext
  - [Under the Hood of Spark Email Real-Time Collaboration](https://readdle.com/blog/under-the-hood-of-spark-email-real-time-collaboration)

- not-yet
  - timestamp如何计算的，插入时如何确定位置

- tips
  - insert依赖preceding元素的id/counter/timestamp，这可以有效避免interleaving

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

- 🤔 what if two actors will concurrently insert different elements after the same predecessor?
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
  - RGA defines operations very similarly to a CT, as units of atomic data with `timestamp+UUID` metadata; 
  - but as soon as operations are received, their causality metadata is stripped and they're inserted into their final spot in the array. 
  - Similarly, delete operations immediately turn their targets into tombstones, which are later "purged" once all sites have received the deletion. 
- RGA is a very effective algorithm, but it doesn't make the logical leap of treating its data structure as an event log, even though that's what it is in practice. Traditionally, one would say that an RGA insert is applied and turned into data; but another way to look at it is that the insert operation is placed in the position of its intended output, then stripped of its metadata. ORDTs make this explicit.

### 🧮 [Causal Trees | Hacker News_202312](https://news.ycombinator.com/item?id=38661580)

- [Causal Trees](https://www.farley.ai/posts/causal)

- https://github.com/sno6/causal /202312/go/ts
  - https://causal-sno6.vercel.app/
  - a CRDT implementation playground.

- Another name for Causal Trees is "RGA" (Replicated Growable Array). They are ~identical algorithms that were published concurrently. E.g., Automerge uses RGA
  - That is true, but I think the CT paper frames the algorithm in a much clearer way than the RGA paper does. It’s a pleasure to read.

- How does the performance of Causal Trees compare to other CRDT implementations, especially in scenarios with a high frequency of concurrent updates? 
  - In my experience, this depends a lot more on the implementation than the CRDT algorithm. If you implement Causal Trees directly (as a tree with one node per char), it will be tolerably fast but use a lot of memory + storage. If you instead group chars into "runs" of sequentially-inserted chars and only store one Causal Tree node per run, it should be quite efficient.
  - For a different tree-based CRDT, I did a head-to-head comparison of implementations that use a node-per-char (Fugue Simple) vs runs (Fugue), with results in Section 5 of this paper
- I don't have any experience with this, but the use of flat arrays (rather than unbalanced trees) in Yjs sped things up considerably according to this long and interesting blog post below.
  - We can use a flat array to store everything, rather than an unbalanced tree. This makes everything smaller and faster for the computer to process
- Thanks for linking my post. I really need to write a followup at some point - we’ve gotten another 2-10x speed up from when I ran those benchmarks, depending on how you measure it.
  - I still stand by what I wrote in that blog post. Using lists rather than trees is still a good approach. And it’s super simple to implement too. You can have a working crdt in a few dozen lines of code.
- > One problem seems to be one that Kleppmann points out in [2, end of section 4], when you press enter in the middle of a line, so that a line is split into two lines, you have to deal with that in a special way. Similarly with splitting/joining blocks.
  - I was about to mention this problem. We ran into this with Google wave. The initial document model (based on an xml tree) used `<line>` tags for lines. We hit exactly this problem - if you press enter in the middle of a line while someone is concurrently editing that line, how does it handle those changes? The initial code had special split and join operations but nobody could figure out how to make split and join work correctly in an OT system.
  - Wave was over a decade ago now. I don’t know if anyone has solved this problem - all the working systems that I know of bailed on(使…失望) this approach. It’s much easier if you just make newline characters be an item that can be inserted or deleted like any other character. And then make lines be a higher order concept.
  - If you get this working (working = passing fuzz test suite), I’d love to hear about it. But the well trodden path of those who come before is to use newline characters instead.
- Definitely interested in how you achieved another 2-10x over the btree approach
- The btree works great, and has barely changed. I made it faster with two tricks:
  - I made my own rope library (jumprope) using skip lists. Jumprope is about 2x faster than ropey on its own. And I have a wrapper around the skip list (called “JumpropeBuf” in code) which buffers a single incoming write before touching the skip list. This improves raw replay performance over ropey by 10-20x iirc.
  - Text (“sequence”) CRDTs replicate a list / tree of fancy “crdt items” (items with origin left / origin right / etc). This special data structure needs to be available both to parse incoming edits and generate local edits. 👉🏻 Turns out that’s not the only way you can build systems like this. Diamond types now just stores the list of original edits. [(Edit X: insert “X” position 12, parent versions Y, Z), …]. Then we recompute just enough of the crdt structure on the fly when merging changes.
  - This has a bunch of benefits - it makes it possible to prune old changes, it lowers memory usage (you can just stream writes to disk). The network and disk formats aren’t dependant on some weird crdt structure that might change next week. (Yjs? RGA? Fugue?). File size is also smaller.
  - And the best bit: linear traces don’t need the btree step at all. Linear traces go as fast as the rope. Which - as I said above, is really really fast. Even when there are some concurrent edits and the btree is created, any time the document state converges on all peers we can discard all the crdt items we generated so far and start again. Btrees are O(log n). This change essentially keeps resetting n, which gives a constant size performance improvement.
  - The downside is that the code to merge changes is more complex now. And it’s slower for super complex traces (think dozens of concurrent branches in git).

- Why bother with CRDTs if you’re doing server-side synchronization? MMORPGs can handle synchronizing thousands of users without problem.
  - CRDTs solve the problem of concurrent updates bij users. And offline edits from concurrent users

- The one “downside” compared to regular databases is that CRDTs use optimistic concurrency. If you want transaction support, or want multiple writers to block each other, CRDTs are a bad fit. They move conflict resolution to the point when reads happen rather than make writers fetch and retry. Still fine for a lot of use cases though.

- What does SoundCloud need CRDTs for?
  - tl; Dr: time-series event storage via a LWW-element-set

### impl

- https://github.com/inkandswitch/peritext /MIT/ts
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - Peritext builds upon RGA, which is similar to Causal Trees, although our algorithm could use any of these plain text CRDTs with minor adaptations. 
  - [Peritext algorithm may attach deleted mark to new inserted text](https://github.com/inkandswitch/peritext/issues/32)
  - [What could be the direction for making Peritext support block elements](https://github.com/inkandswitch/peritext/issues/27)

- https://github.com/maca/ace-crdt /js/rga
  - Collaborative text editor proof of concept using CRDT
- https://github.com/jorendorff/peeredit /201611/js/rga
  - This is example code for a talk on CRDTs.
  - 示例使用ace.v1编辑器

- https://github.com/josephg/simple-crdt-text /ts
  - This implements automerge's underlying algorithm (RGA)
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.

- https://github.com/jaredly/local-first/tree/master/packages/text-crdt
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.
  - Your approach seems to resemble RGASplit which I believe is bases for

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

- [💡 Which algorithm y-array is using? · y-js/y-array](https://github.com/y-js/y-array/issues/9)
  - Yjs does not share any concepts with the RGA algorithm. 
  - If you want to compare it conceptually, Yjs is actually more similar to WOOT.

- [CRDT: Tree-Based Indexing](https://madebyevan.com/algos/crdt-tree-based-indexing/)
  - Compared to fractional indexing, tree-based indexing is more complicated but prevents interleaving of concurrently-inserted runs, which makes it appropriate for textual data. 
  - The algorithm presented here is similar to a well-known one called "RGA" but with reordering layered on top.

## json-crdt

### tips

- 考虑到数据源和持久化，通常会将json扁平化，normalize
  - 还要考虑编码解码
  - 扁平化后方便持久化 lww + map
  - 合理设计数据结构，避免json

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
  - [Shelf: easy way for recursive CRDT documents](https://www.bartoszsypytkowski.com/shelf-crdt/)

- https://github.com/siliconjungle/cabinet
  - A key value store & subscriptions wrapping a json blob crdt (shelf).

- more-impl
  - https://github.com/automerge/automerge-classic
  - https://github.com/samuel-christian/json-crdts

### more-json-crdt

- [JSON-CRDT](https://github.com/ipfs/notes/blob/master/CRDT/json-crdt.md)

## WOOT

- pros
  - simple

- cons
  - tombstone
  - ? interleaving

- who is using #crdt-woot
  - 业务产品并不多，参考fro scala.js
  - atom-teletype

### [Atom-teletype代码协同编辑原理详解_202011](https://mp.weixin.qq.com/s?src=11&timestamp=1686732708&ver=4589&signature=8ifZN03y4mobAX0Mn0CnG1Pv3oT5RHfMds3ZQX4IbFMeBLv6di-WBPRSMDXf-4Y6DW5u6nzCQGw3KZuKTap-bdOPzO9bZQpRKQWI6uo9RAdEmPiihZ2be3lwelV-LT4V&new=1)

- 本文主要介绍 TELETYPE-CRDT中如何设计WOOT算法来保证文本类型数据的最终一致性，并使用复合的数据结构（称之为 IDTree）来优化代码的运行效率。

- Vectorclock：向量时钟。简单来说，在这个分布式系统中，是对每个进程维护的计数器。在向其它进程发送信息时，通过携带自己当前的计数，其它进程处理问题时可以保证操作的因果关系。
- Splay Tree：伸展树。是一种特殊的二叉搜索树，每次查找后对树进行重构，把被查找的节点搬到离树根更近的地方。

- 先考虑的是最简单的情况：一个字符为一个节点，且它们通过线性的结构组织。后续会将其拓展为一个字符串对应一个节点，并使用一种复合数据结构将这些节点组织在一起，提升查询和插入的性能。
- 在 WOOT 算法中，程序内部使用了 ID的大小来定义两个字符的大小关系比较。在两个字符存在大小关系的情况下，同时插入两个字符时，通过比较 ID大小来对字符进行排序，这样就避免了产生冲突。
- WOOT 算法通过定义 ID来避免冲突，处理结果取决于 ID大小比较的定义方式。
- 本地会一直存在一个循环，不断地将操作池中的操作尝试集成到本地。
  - 在建立了 TCP 连接的情况下，对于其它单个客户端来说，操作顺序是能保证的。
  - 假设一个客户端协同过来一个操作 op1（op1 依赖另一个仍未协同到我这边的操作 op2），那么在 op2 协同过来我这边之前，op1 必不可能被集成到我的客户端内。

- 作为 CRDT 的一种实现，WOOT 算法确实是一种理论可行的办法。但从实际来说，WOOT 算法仍需要进行优化才能落地。
- 时间复杂度
  - 从伪代码中可以直观看出，无论是查找字符串中是否有墓碑，还是从 S'生成 L字符串的过程，WOOT 算法都充满了 O(n)时间复杂度的字符串遍历操作
  - 上面提到我们使用到了线性结构。如果使用链表进行查找，每次 O(n)的查询效率是完全不可接受的，而使用数组，则每次 O(n)的插入效率同样是不可接受的。
  - 因此我们更倾向于考虑使用树形结构进行组织，这样就能把查询和插入操作复杂度降低到对数级别甚至以下。
- 空间复杂度
  - 另外，上述的这种状态是**对每个字符都生成对应的节点数据结构**，从而进行后续的比较。这在代码编辑器这种字符数量如此之大的场景下会产生巨大的内存占用，这是完全不可用的。
  - 另外，在文本编辑的过程中，我们常常会在一段时间内输入一大段的文字，而非一个个字符地进行输入。因此在同步操作时，也应该批量地同步文字。
  - 也就是说，我们应该把**数据结构上的一个节点对应成一段文字而不是一个字符**，这样能少创建非常多的节点，从而减少非常多的内存消耗。

- 为了保证查询和插入效率，teletype 引入了一种数据结构，称之为 IDTree。
  - 所谓的 IDTree实际上是一种自定义的数据结构。它在原来链表节点的基础上新增了指针，使这个链表复合了一棵二叉搜索树，并新增了一个变量保存该节点的子树大小用以简化查找。

- ID的大小比较影响了字符并发插入时的排序
  - 为了保证后续能支持撤销重做的操作， ID必须首先能区分客户端。因此它上面必须保存客户端的标识符，称之为 `siteID`。
  - 其次，由于操作间可能存在因果关系，比如“删除字符”的操作会依赖“该字符串被插入”。因此 ID必须能识别操作的因果关系。因此它上面还需要保存向量时钟的值，称之为 `seq`。

- 考虑刚才线性表的 case，由于数组是连续不断的内存空间，插入的性能似乎是无法优化的；而链表的查询性能却能通过将其整合成一棵树来提升（树的查找效率仅跟高度有关）
- 查询操作从原先的遍历链表变成了根据权重执行二分查找
- 新的插入操作逻辑变复杂了，但由于本质上还是指针的操作，复杂度并没有明显提升
- 由于原来的线性表关系没有被断开，删除一个节点只需要将其从查找树上去除，并将其表示墓碑的标志字段置为 true 即可

- Teletype-crdt 如何继续优化 ID Tree
  - 普通的二叉搜索树执行相对有序的插入，会使树的结构趋向于链表，降低查询效率。因此替换为可调整的二叉搜索树树是一个不错的选择。
  - 树上只有可视的节点，它们的节点的位置和内容通过一个 hashMap 映射到 UI 的显示状态。那么这棵树无论如何调整节点位置，只要它节点对应的文本内容和文本位置不变，就不会引起 UI 的更新。

- teletype-crdt使用了伸展树来优化 IDTree。
- 伸展树（Splay Tree）是一种在一般情况下，统计学上效率更高的二叉搜索树，每当伸展树的节点被修改时，伸展树会通过 AVL 旋转把最近修改的节点旋至根节点，而不改变 BST 的性质。伸展树尤其擅长处理重复的查询和修改操作。
- 代码编辑恰好是符合这种场景的，一段被修改的代码大概率是会被重复修改的，因此伸展树的平均效率更高。

- 将节点从“点”变成“块”
  - 在一个节点上仅保存一个字符，会导致编辑时产生大量的节点对象，产生大量的内存占用。因此，一个节点上必须要保存一块字符串。
  - 当节点保存一块字符串时，编辑该节点的字符串中间的字符时需要有合理的方式拆分该节点。因此，节点上还需要保存额外的一些信息。
  - 扩充后，必须保留原有数据结构的性质，节点拆分后仍然能进行二分查找，保持高性能；且不能改变原有的链表结构，否则就会出现冲突。

- 另外， teletype内部维护了一个 hash map，可以使用 ID快速查找到对应的节点。

- 对于效率的实际提升请参考：《High Responsiveness for Group Editing CRDTs》的第五节。

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

### impl

- https://github.com/ryankaplan/woot-collaborative-editor /201601/ts
  - When a textarea-change is detected, diff the textarea content against the last known content. 
  - 编辑器使用textarea，依赖diff-match-patch
  - With the help of WootTypes. WString, turn that diff into `WStringOperations` and broadcast those operations to the server.
  - When we receive operations from the server, apply those operations to our WString instance and apply them to the text in #collab-doc.
  - WOOT, as an approach, gets really slow unless you implement tombstone garbage collection (aka getting rid of text that users have deleted) which can only happen when everyone has disconnected from a document.

- https://github.com/atom/teletype-crdt /js
  - [Can teletype-crdt work with other wysiwyg editor ?](https://github.com/atom/teletype-crdt/issues/6)
    - Probably not. This CRDT is for text. A wysiwyg editor’s underlying model isn’t text, it’s a tree (with nodes and properties to represent rich text).
    - teletype-crdt is a CRDT that exposes APIs that work only with plain text and markers. A WYSIWYG editor has a more complex structure than just text, so you will need to enhance it in such a way that can support your use case.
  - [协同编辑冲突处理算法综述](https://mp.weixin.qq.com/s?__biz=MjM5MTY2NTIyMA==&mid=2649000528&idx=1&sn=98521c16c3f24809f426fe39ae48e203&chksm=bea2377b89d5be6df3656e8b8c76d022ab1fe6deece6b3f16e88ab07b5cba227542240f7d5d7)
    - atom 编辑器的协同插件 teletype 即是基于 WOOT 实现

- https://github.com/d6y/wootjs /scala.js
  - WOOT is a collaborative text editing algorithm, 
  - allowing multiple users (`sites`) to insert or delete characters (`WChar`) from a shared document (`WString`).
  - The algorithm preserves the intention of users, and ensures that the text converges to the same state for all users.
  - Its key properties are simplicity, and avoiding the need for a reliable network or vector clocks (it can be peer-to-peer).

### more-woot

- [WOOT: an Algorithm for Concurrent and Collaborative Authoring (2013) [video] | Hacker News](https://news.ycombinator.com/item?id=10677667)

## Logoot/LogootSplit

- pros
  - no tombstone

- cons
  - interleaving

### tips

- who is using #crdt-logoot
  - mute
  - Conclave(lseq)
  - [DTNDocs: A delay tolerant peer-to-peer collaborative editing system_201801](https://ieeexplore.ieee.org/document/8343092)
    - DTNDocs Android application uses IBR-DTN to communicate over a delay tolerant network and a modified LogootSplit algorithm for ensuring consistency in shared contents.

- [Faster CRDTs: An Adventure in Optimization | Hacker News_202108](https://news.ycombinator.com/item?id=28017204)
  - This is still hard for me to determine when position-based list CRDT (Logoot, LogootSPlit, ...) are better than tombstone-based list CRDT (RGA, RgaSplit, Yata, ...). It could be worth to assess that.
  - 3 year ago I started an update of LogootSplit. The new CRDT is named Dotted LogootSplit and enables delta-synchronizations. The work is not finished: I had other priorities such as writing my thesis
  - I have to perform some benchmark. However I'm more interested in the hypothetical advantages of Dotted LogootSplit regarding synchronization over unreliable networks. From an engineering point-of-view, I'm using a partially-persistent-capable AVL tree. Eventually I would like to switch to a partially-persistent-capable b-tree. Unfortunately writing a paper is very time consuming, and time is missing.

- https://news.ycombinator.com/item?id=18193094
  - My hunch(预感；直觉) is that because CRDTs are so much easier to grok(通过感觉意会) than OT, engineers are empowered to make use case-specific improvements that aren't reflected in academic literature.
  - For example, the Logoot/LSEQ CRDTs have issues with concurrent insert interleaving; however, this can be solved by dedicating a bit-space in each ID solely for followup inserts.
  - The "Inconsistent-Position-Integer-Ordering" problem is solved by comparing ids level-by-level instead of in one shot.
  - Additionally, the best CRDTs (like Logoot/LSEQ) don't require tombstones, garbage collection, or "quiescence." The complexity burden is far lower.
  - To top it off, CRDTs are offline-capable by default.

### 📕 [LSEQ: an Adaptive Structure for Sequences in Distributed Collaborative Editing_201309](https://www.researchgate.net/publication/262162421_LSEQ_an_Adaptive_Structure_for_Sequences_in_Distributed_Collaborative_Editing)

- In order to preserve the total order on the elements of the sequence, a unique and immutable identifier is associated with each basic element of the structure (character, line or paragraph according to the chosen granularity). 
- This allows distinguishing two classes of sequence CRDTs: 
- (i) Fixed size identifier (also called the tombstones class). 
  - This class includes WOOT [11], WOOTO [20], WOOTH [1], CT [7], RGA [13], [23]. 
  - In this class, a tombstone replaces each suppressed element. 
  - Although it enjoys a fixed length for identifiers and it has a space complexity which depends on the number of operations. 
  - For example, a document with an history of a million operations and finally containing a single line can have as much as 499999 tombstones. 
  - Garbaging tombstones requires costly protocols in decentralized distributed systems. 
- (ii) Variable-size identifiers. 
  - This class includes for example Logoot. It does not require tombstones, but its identifiers can grow unbounded. Consequently, although it does not require garbage protocols, its space complexity remains till now linear with the number of insert operations. Thus, it is possible to have only a single element in the sequence having an identifier of length 499999. 
  - Treedoc uses both tombstones and variable size identifiers but relies on a complex garbage protocol when identifiers grow too much.
- 💡 In this paper, we propose a new approach, called LSEQ, that belongs to the variable-size identifiers class of sequence CRDTs.
  - LSEQ is an adaptive allocation strategy with a sub-linear upper-bound in its spatial complexity. 
- We choose Logoot (for comparison) as it delivers overall best performances for variable-size sequence CRDTs

- The Logoot paper already highlighted the importance of allocation strategies (alloc). 
- Indeed, experiments concerned two strategies. 
  - (1) Random: randomly choosing between the identifiers of the two neighbours. It delivers poor performance because the identifiers quickly saturate the space, resulting in the creation of new levels. As consequence, the size of identifiers grows quickly. 
  - (2) Boundary: randomly choosing between the identifiers of the two neighbours bounded by a boundary maximum value. The strategy allocates the new identifiers closer to their preceding identifier. Of course, it works well when the editions are performed right-to-left.
- LSEQ applies a very simple strategy: each time it creates a new level in the tree between two identifiers p and q, it doubles the base of this depth and it randomly chooses a strategy among boundary+ and boundary–.
  - boundary+ allocates from p plus a fixed boundary, boundary– allocates from q minus a fixed boundary. 
  - The boundary never changes whatever the depth of the tree.

- Logoot’s underlying allocation strategy always uses the same base to allocate its identifiers. 
  - With regard to the tree representation, it means that the arity is set to base.
- A high base value is not profitable if the number of insert operations in this part of the sequence is low.
  - On the contrary, keeping a constant base value when the number of insert operations starts to be very high does not allow to fully benefit of the boundary strategy.
- the objective is to adapt the base according to the number of insertions in order to make a better reflection of the actual size of the document. 
  - Since it is impossible to know a priori the size of the document, the idea is to start with a small base due to the empty sequence, and then to double it when and where necessary, i.e. when the depth of identifiers increases.
- Doubling the base at each depth implies an exponential growth of the number of available identifiers. 
  - Thus, the model corresponds to the exponential trees and consequently it benefits of their complexities. 

- The variable-size identifiers class of CRDT includes Logoot and Treedoc. 
- These CRDTs use growing identifiers to encode the total order among elements of the sequence. 
  - In the worst case, the size of identifiers is linear in the total number of insert operations done on the document. 
- 🆚️ Logoot and Treedoc have different allocation strategies. 
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

### 📕 [TreeDoc: A Commutative Replicated Data Type for Cooperative Editing_200906](https://www.researchgate.net/publication/221460068_A_Commutative_Replicated_Data_Type_for_Cooperative_Editing)

- 🌲 Logoot uses a sparse n-ary tree rather than Treedoc's dense binary tree. 
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

### impl

- https://github.com/mkdynamic/logoot
  - Collaborative text editor using Logoot CRDT algorithm. 
  - Adds an informal versioning scheme based on state vectors to ensure casual ordering of operations is maintained.

- https://github.com/t-mullen/logoot-crdt
  - Implemented as a tree for fast character position lookups.

- https://github.com/nybblr/logoot /201911/js
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

## LSEQ

- cons
  - interleaving

- who is using #crdt-lseq
  - conclave

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

- [LSEQ and causal tree · conclave-team/conclave](https://github.com/conclave-team/conclave/issues/14)
  - LSEQ isn't so much a data type as it is a data allocation strategy. 
  - It keeps track of all of the characters that have already been inserted into the document and is used to determine the position of a new character when it is inserted.
  - When a new character is inserted, it will look at the position of the character before it and after it on the tree and generate a position between them.
  - It follows a tree structure, but LSEQ trees are dynamic and grow according to how large the document is. 
  - That also means that nodes in an LSEQ tree are removed when the corresponding characters are removed. 
  - Also, the behavior of an LSEQ tree depends on what level of the tree you're on and which allocation strategy you chose to use.

### impl

- https://github.com/Chat-Wane/LSEQTree /js
  - an implementation of a CRDT-based array with an underlying exponential tree and the allocation strategy LSeq

## TreeDoc

- pros
  - no interleaving

- cons
  - unbalanced tree is bad for query

- 🌲 uses a binary tree to represent the document

- https://github.com/mweidner037/uniquely-dense-total-order
  - [Fugue(Plain Tree): A Basic List CRDT _202210](https://mattweidner.com/2022/10/21/basic-list-crdt.html)
    - The rest of this post introduces a basic UniquelyDenseTotalOrder that I especially like. 
    - I have not seen it in the existing literature, although it is similar enough to Logoot, Treedoc, and others that I wouldn’t be surprised if it’s already known. For now, I call it Plain Tree.

- Logoot and TreeDoc used variable-length identifiers.

- [CRDT: Tree-Based Indexing - Made by Evan](https://madebyevan.com/algos/crdt-tree-based-indexing/)
  - Compared to fractional indexing, tree-based indexing is more complicated but prevents interleaving of concurrently-inserted runs, which makes it appropriate for textual data. 
  - The algorithm presented here is similar to a well-known one called "RGA" but with reordering layered on top.

### impl

- https://github.com/matanbroner/Text-Editor-CRDT /js
  - Basic text editor CRDT based on the the TreeDoc data structure
# discuss
- ## 

- ## 

- ## 

- ## 🆚️ Here's a visual comparison of the data structures underlying three different "collaborative text editing" algorithms.
- https://twitter.com/jaredforsyth/status/1232532781936173056
  - [yjs vs automerge vs rga](https://text-crdt-compare.surge.sh/)
  - yjs uses a doubly-linked list of nodes
  - mine(local-first-rga) uses a tree
  - automerge uses a transaction log (and has in-memory caches for perf)
- Your approach seems to resemble RGASplit which I believe is bases for
