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

- who is using #logoot
  - mute
  - [DTNDocs: A delay tolerant peer-to-peer collaborative editing system_201801](https://ieeexplore.ieee.org/document/8343092)
    - DTNDocs Android application uses IBR-DTN to communicate over a delay tolerant network and a modified LogootSplit algorithm for ensuring consistency in shared contents.

- Oster
  - [Publications – Gérald OSTER](https://members.loria.fr/goster/publications/)
  - 2005年发布WOOT
  - 2017年发布Mute, 基于logoot变体
# crdt-algorithms

## Logoot/LogootSplit

### tips

- pros
  - no tombstone

- cons
  - interleaving

- https://news.ycombinator.com/item?id=18193094
  - My hunch(预感；直觉) is that because CRDTs are so much easier to grok(通过感觉意会) than OT, engineers are empowered to make use case-specific improvements that aren't reflected in academic literature.
  - For example, the Logoot/LSEQ CRDTs have issues with concurrent insert interleaving; however, this can be solved by dedicating a bit-space in each ID solely for followup inserts.
  - The "Inconsistent-Position-Integer-Ordering" problem is solved by comparing ids level-by-level instead of in one shot.
- Additionally, the best CRDTs (like Logoot/LSEQ) don't require tombstones, garbage collection, or "quiescence." The complexity burden is far lower.
- To top it off, CRDTs are offline-capable by default.

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

- [Introduction to CRDTs for Realtime Collaboration - DEV Community](https://dev.to/nyxtom/introduction-to-crdts-for-realtime-collaboration-2eb1)
  - Logoot/LSEQ/TreeDoc does not store tombstone deletions and instead takes an approach with fractional/unbounded divisible indexing. 
  - This, as discussed earlier, can cause issues with interleaving edits so it becomes impractical to guarantee proper sane convergence with concurrent operations.

- [An Elixir implementation of the Logoot CRDT](https://hexdocs.pm/logoot/readme.html)
  - Because of how these atom identifiers are structured, they are totally ordered, as opposed to causally ordered. 
  - No identifier cares about the identifier before it once it’s been created, and so tombstones are not necessary.

- [A simple approach to building a real-time collaborative text editor_201710](https://digitalfreepen.com/2017/10/06/simple-real-time-collaborative-text-editor.html)
  - I adapted Logoot

## WOOT

- pros
  - simple

- cons
  - interleaving
  - tombstone

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
  - ​ 如果一个偏序集中任意两个元素都有最大下界和最小上界的话，我们就可以将这个偏序集称之为一个格，可见格的概念是包含在偏序集中，也可以说一部分特殊的偏序集也就是格。
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

- [WOOT](https://github.com/d6y/wootjs) is a collaborative text editing algorithm, 
  - allowing multiple users (`sites`) to insert or delete characters (`WChar`) from a shared document (`WString`). 
  - The algorithm preserves the intention of users, and ensures that the text converges to the same state for all users.
  - Its key properties are simplicity, and avoiding the need for a reliable network or vector clocks (it can be peer-to-peer).

- https://github.com/ryankaplan/woot-collaborative-editor
  - When a textarea-change is detected, diff the textarea content against the last known content. 
  - With the help of WootTypes. WString, turn that diff into `WStringOperations` and broadcast those operations to the server.
  - When we receive operations from the server, apply those operations to our WString instance and apply them to the text in #collab-doc.

### more-woot

- [WOOT: an Algorithm for Concurrent and Collaborative Authoring (2013) [video] | Hacker News](https://news.ycombinator.com/item?id=10677667)

## RGA(Replicated Growable Array)/

### [Operation-based CRDTs: arrays (part 1)](https://www.bartoszsypytkowski.com/operation-based-crdts-arrays-1/)

### [Operation-based CRDTs: arrays (part 2) Block-wise Replicated Growable Array](https://www.bartoszsypytkowski.com/operation-based-crdts-arrays-2/)

- fit better into scenarios, where we insert and delete entire ranges of elements

### implementation

- https://github.com/maca/ace-crdt /js/rga
  - Collaborative text editor proof of concept using CRDT

- https://github.com/gritzko/citrea-model
  - A CRDT-based collaborative editor engine of letters.yandex.ru (2012, historical)

- https://github.com/josephg/simple-crdt-text /ts
  - This implements automerge's underlying algorithm (RGA)
  - The goal is to have some simple code that I can use to clarify semantics and as a basis for fuzz testing correctness of a faster implementation.

### more-rga

- [Replicated Growable Array / Causal Tree](https://replicated.cc/rdts/rga/)
  - Overall, RON 2.1 RGA/CT follows the classic RGA/CT data structure

## TreeDoc

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
