---
title: lib-collab-crdt-blog
tags: [blog, collaboration, crdt]
created: 2022-10-13T07:59:52.953Z
modified: 2022-10-13T08:00:21.260Z
---

# lib-collab-crdt-blog

# guide

- ref
  - [CRDT Tutorial for Beginners](https://github.com/ljwagerfield/crdt)
  - [arXiv: collaborative editing](https://arxiv.org/search/?query=collaborative+editing&searchtype=all&source=header)
# 🪟 [Conflict-free Replicated Spread Sheets](https://www.bartoszsypytkowski.com/crdt-tables/)

# 📝 [An Interactive Intro to CRDTs | jakelazaroff.com_202310](https://jakelazaroff.com/words/an-interactive-intro-to-crdts/)

- A register is a CRDT that holds a single value. 
    - There are a couple kinds of registers, but the simplest is the Last Write Wins Register (or LWW Register).
- LWW Registers simply overwrite their current value with the last value written. 
  - They determine which write occurred last using timestamps, represented here by integers that increment whenever the value is updated.

- You might ask: why not use the actual time? 
  - Unfortunately, accurately syncing clocks between two computers is an extremely hard problem. 
  - Using incrementing integers like this is **one simple version of a logical clock**, which captures the order of events relative to each other rather than to the “wall clock”.
# 👥 [An interactive intro to CRDTs | Hacker News_202310](https://news.ycombinator.com/item?id=37764581)

# 📝 [Building a Collaborative Pixel Art Editor with CRDTs | jakelazaroff.com](https://jakelazaroff.com/words/building-a-collaborative-pixel-art-editor-with-crdts/)
- In An Interactive Intro to CRDTs, we learned what CRDTs are, and implemented two: a **Last Write Wins Register** and a **Last Write Wins Map**. 
  - We now have everything we need to build a collaborative pixel art editor
# 📝 [Building a BFT JSON CRDT](https://jzhao.xyz/posts/bft-json-crdt/)
- CRDTs are a family of data structures that are designed to be replicated across multiple computers without needing to worry about conflicts when people write data to the same place. 
- Traditional databases focus on a property called linearizability, which guarantees that all operations behave as if executed on a single copy of the data. 
  - Linearizability is a strong correctness condition, which constrains what outputs are possible when an object is accessed by multiple processes concurrently. It is a safety property which ensures that operations do not complete in an unexpected or unpredictable manner.
  - We call this canonical view the primary site.
  - Every read in a linearizable system, no matter what database node you read from, gives you an up to date value.
- Achieving this property adds a lot of overhead because both writes and reads need to coordinate across all database nodes to ensure consistency. 
  - This creates an availability problem: if you can’t reach a majority of your nodes, you can’t process any operations.
- using CRDT, we trade linearizability for a property called strong eventual consistency:
  - All updates will eventually reach every node
  - Every node that has received the same updates will have the same state

- CRDTs are a family of data structures.
  - A fundamental limitation here is that there are certain types of data structures (like sets) that cannot be made into CRDTs

- we can use Lamport timestamps. 
  - These track logical time rather than actual wall time, meaning we count number of events that have occurred rather than seconds elapsed.
  - This timestamp is just a simple counter. 
- For the rest of the blog post, we refer to this counter as the sequence number `seq`.
  - All nodes start their counter at 0
  - Everytime we perform an operation locally, we increment our counter by one
  - Everytime we broadcast a message to our peers, we attach this counter
  - Everytime we receive a message, we set our timer to `max(self.seq, incoming.seq) + 1`

- Lamport timestamps only give us a partial ordering, which means two identical sequence numbers might not correspond to the same unique event. 
  - we can actually create a total ordering of events in a distributed system by using some arbitrary (but deterministic) mechanism to break ties. 
  - For CRDTs, if we give each node a unique ID, we can actually tie-break on this ID to provide a deterministic way to order concurrent events.

- But we can’t figure out this causality information from just sequence numbers alone.
  - It turns out the fix for this is actually quite easy.
  - As we have a unique way of identifying each operation, we can just send along a list of operations it causally depends on. 
  - That way, if we receive a message and we know we’ve received all of its causal dependencies, it should be safe to deliver.
  - If we receive a message where we haven’t received all of its causal dependencies, then we can add it to a queue so that when the message does get delivered, we can apply it afterwards. 
  - This means that as long as we declare the right causal dependencies, we can make certain things that don’t seem commutative (like list operations) actually commute.

- make a distinction between the data in the CRDT itself and the view of that data.
  - The data itself are the operations that are coming in
  - The view is the data structure we compute from it (and what applications end up seeing)

- we never4 delete any operations from the internal data representation. 
  - The best we can do is mark them as deleted using a tombstone. 
  - Because a peer could technically reference any past operation as a causal dependency, we need to keep that metadata around.

## List CRDTs (RGA Explained)

- When you think of the API for a list, most operations are normally done by indexing.
- The key insight here is that instead of using relative addressing (e.g. positional indexing), we can use absolute addressing (e.g. using IDs).
  - Every time we insert an element into the list, we need to know the ID of the character we are inserting after. 
  - Then, we just place it somewhere between that element and the element following it.
  - So instead of saying “insert ‘A’ after the character at position 4” we say “insert ‘A’, with ID 5, and insert it after the character with ID 4”.
- Conveniently, we can encode this causality by making the causal parent of each item the character it was inserted after. 
  - This forms a sort of causal tree and this is effectively how RGA, a list CRDT, structures its data internally.
- When inserting a character we
  - Find the origin (causal dependency). If it doesn’t exist, we queue it up for later.
  - Starting at this node, all of its siblings were inserted concurrently. We look through the list of siblings until we reach a node that we are greater determined by the happens-before comparison we defined

- To get the actual list this CRDT represents, we perform an in-order traversal over the tree and only keep nodes that are not marked as deleted.

## Adding Byzantine Fault Tolerance for free (almost)

- Up to this point, the CRDTs we’ve covered all work in trusted scenarios. 
  - These are scenarios in which you know all of the people participating and you trust them to not screw up the system for everyone else.
- However, most of the interactions we have online are not in trusted scenarios. 
  - Luckily, we have servers to help mediate(调停；调解) these interactions, dictate what is and what isn’t possible. 
- The CRDTs we have been exploring so far do not work in these untrusted scenarios. 
  - That is, any one node can do something bad and cause state to diverge permanently. Not good.
- To be more concrete, here are some examples of what a malicious actor can do:
  - Send malformed updates
  - Not forward information from honest nodes (an eclipse attack)
  - Send invalid updates
    - Messages that have duplicate IDs
    - Send incorrect sequence numbers (an equivocation attack)
    - Claim to be another user
- To borrow a term from distributed systems, we want to make our CRDTs Byzantine fault-tolerant
  - The ‘Byzantine’ part of the name comes from the Byzantine Generals Problem, a situation where, in order to avoid catastrophic failure of the system, the system’s actors must agree on a concerted strategy, but some of these actors are unreliable and potentially malicious.
- Notation wise, we denote the total number of nodes in the system `n`. 
  - We denote the number of faulty/Byzantine nodes `f`. 
  - Most consensus algorithms claim a tolerance of up to `f < n/3`, which means they can tolerate up to 33% Impossibility Result
- However, CRDTs require an even weaker bound. Remember that we are not trying to achieve consensus! 
  - All we really need to do is make sure that Byzantine actors can’t interrupt honest nodes from functioning properly.

- In fact, we can reduce this to a problem called Byzantine Broadcast
  - Dolev-Strong, back in 1983, showed that it was possible to tolerate up to $f < n$ faulty nodes! 
  - This means that, as long as there are honest nodes and they are connected to each other, they can still function properly
- Kleppmann detailed an approach in his paper Making CRDTs Byzantine Fault Tolerant that works without changing the internals of most CRDTs; it can be fully retrofit on top of it. 
  - We can create a ‘BFT adapter’ layer between the transport and application layer that is responsible for filtering out any Byzantine operations.

## A JSON CRDT

- Ok, we’ve seen now how we can create a Byzantine Fault Tolerant list CRDT. How can we make a JSON CRDT out of this?
- Normally with JSON CRDTs, we just have a bunch of nested CRDTs.
  - Values are LWW registers
  - Lists are RGA lists
  - Maps are lists of key-value pairs
- Each nested CRDT also keeps track of its path (e.g. inventory[0].properties.damage) so that when CRDTs produce an event, this information is also included. 
- However, we have to be careful about how we store this path. We can’t naively just use the index into the list as we saw earlier how this is unstable. A small workaround here is having the `OpID` be the index.

- There is one last challenge to account for: JSON has no schema; data types can change!
  - The way Automerge and Yjs resolve this is by essentially using a multi-value register: they keep both values and punts the responsibility to the application choose the right answer.
- With most applications, allowing users to set arbitrary JSON is not actually desirable. We can somewhat mitigate these problems by allowing the application developers to define a fixed schema ahead of time and validating all operations through this
# [Bartosz Sypytkowski crdt series](https://www.bartoszsypytkowski.com/the-state-of-a-state-based-crdts/)

## [CRDT optimizations](https://www.bartoszsypytkowski.com/crdt-optimizations/)

- If you take a closer look at the implementation details of block-wise RGA algorithms, you may notice that CRDT specifics usually depend on the metadata alone - we are usually only interested in the length of the content rather than content itself. 
  - In reality we could abstract it into a separate structure optimized for text manipulations (like `Rope` or string buffers of specific editors), while RGA-specific metadata only holds ranges that given block is responsible for.

- 
- 
- 

## [Operation-based CRDTs: registers and sets](https://www.bartoszsypytkowski.com/operation-based-crdts-registers-and-sets/)

- You can think of registers as value cells, that are able to provide CRDT semantic over any defined type. 
  - Remember, that we're still constrained by commutativity/associativity/idempotency rules. 
  - For this reason we must apply additional metadata, which will allow us to provide arbitrary conflict resolution in case of conflict detection.

- Registers are one the most wide spread ways of working with CRDTs. 
  - The reason is simple: they allow us to wrap any sort of ordinary data types in order to give them CRDT-compliant semantics.
  - However, this comes at the price - we cannot simply change any non-CRDT value into CRDT without some compromises: if that would be possible, we wouldn't need CRDTs in the first place. 
  - For these, two popular approaches are known as last-write-wins and multi-value registers.

- 👉🏻 Last write wins is a popular way of dealing with conflicts being the result of concurrent updates in many systems (Cassandra is good example of a database that's quite known from this approach).

- The algorithm is simple: on each register value update, we timestamp it. 
  - If our current timestamp is higher than the most recent one remembered by the register itself, we change the value, otherwise leave existing one (more recent) untouched.
- One of the issues of last-write-wins approach is its inherent risk of data loss - we took an easy to use API at price of automatically throwing out potentially useful data.

- 👉🏻 Another approach is to build a register that doesn't drop any data, instead it keeps track of all causal (happened-before) relationships between updates and in case of conflicts returns all conflicting cases. 
  - It's known as Multi Value Register.
- We track causality of register updates, and in case of conflicts - as when two independent updates are happening concurrently - we'll provide all conflicting values. 
  - Programmer is then free to choose any value and override concurrent conflicts with more recent update.

### [Registers and Deletion](https://lars.hupel.info/topics/crdt/07-deletion/)

- A register may contain arbitrary data with some additional metadata on top. 
  - Precisely what kind of metadata varies across different register implementations.
- Assignments may be done concurrently by different threads and merging may:
  - discard all concurrent assignments but one, 
  - keep all concurrent assignments.

- A Last-Writer-Wins Register (LWW-Register) creates a total order of assignments by associating a timestamp with each update.
  - I understand that the explanation of LWW-Registers may be a little anticlimactic. They literally only store a single piece of metadata that is used to impose a total ordering. 
- But again, their power lies within their composition
  - values are now LWW-Registers that I express as a pair of (value, time). 
  - map + lww

- The Multi-Value Register (MV-Register) does not assume the presence of an ordered clock across all nodes. 
  - Instead, it relies on a vector clock
- The basic principle of a vector clock is the same as for a Lamport clock. 
  - The clock does not measure real time; rather, it increments whenever an event occurs. 
  - Each node keeps its own clock. 
  - The difference now is that each node keeps each other node’s clock, too (i.e., a “vector” of clocks). 
  - When a message is sent, the sending node increases only its own clock, but includes a copy of the entire vector in the message. 
  - On the other side when a message is received, the receiving node again increments its own clock, and for everyone else’s clock, it takes the maximum of the own vector and the received vector.
- Using a vector clock, this situation can be detected easily. 
  - Whenever someone writes a value into the register, they also record the current state of their vector clock.
- Now let’s say Alice and Bob want to merge their MV-Registers. 
  - They first have to compare the timestamp, just like for a LWW-Register. 
  - But whereas in a LWW-Register, they just compare two numbers, here they have to compare an entire vector.
  - If the two vector clocks are incomparable, then we have a concurrent write. It occurs when there is a connection loss right after the start. It means that both writes happened concurrently and we don’t really know which one is “better” than the other.
  - So what do we do? The name “Multi-Value Register” already gives it away. We keep both writes.
  - Neither value’s vector clock is ≥ any other value’s vector clock. Consequently, the MV-Register now simultaneously contains {0, 2, 3, 4}. 
- You might be wondering how such a mess could ever be cleaned up? Well, future writes might do that.

### more-register

- [CRDT: Conflict-free Replicated Data Types](https://medium.com/@amberovsky/crdt-conflict-free-replicated-data-types-b4bfc8459d26)

- register: A memory cell with two operations — assign() and value(). 
  - The issue is with the assign() operations — they do not commute.
  - There are two approaches to solve this issue: lww / mv

- lww
  - Columns in cassandra
  - NFS — a whole file or a part of it

- mv
  - Amazon shopping basket. It has a well-known bug when an item re-appears in the basket after deletion. The reason is that MV-Register doesn’t behave like a set even though it stores a set of values (see below). Amazon indeed doesn’t treat that as a bug — it actually increases sales.
# 📝 [supabase: `pg_crdt` - an experimental CRDT extension for Postgres_202212](https://supabase.com/blog/postgres-crdt)
- https://github.com/supabase/pg_crdt
  - pg_crdt is an experimental extension adding support for conflict-free replicated data types (CRDTs) in Postgres.
  - It supports Yjs/Yrs and Automerge.
  - Our goal was to evaluate if we could leverage a Postgres-backed CRDT and Supabase's existing Realtime API for change-data-capture to enable development of collaborative apps on the Supabase platform.
  - pg_crdt extension is a proof-of-concept that wraps rust's yrs and automerge libraries using the pgx framework to add a Postgres native CRDT, crdt.ydoc.

- CRDTs are a special type of data structure designed to solve a specific problem: they can merge changes in a way that the final state of the data will be the same, no matter the order in which the updates were applied.
  - In simple terms, a CRDT allows multiple users to make changes to the same data without the need for a central authority to coordinate their actions.
- I personally believe CRDTs are the future. For some things. If databases were invented today, I'm certain most of the effort would be spent developing CRDT databases or something with “offline algorithms” built-in.
- It's possible that developers will need to be selective about their “level” of offline support, at least if they plan to use an “incumbent” databases. 
  - For the cases, a simple “last write wins” strategy is probably acceptable (see the excellent Replicache and Watermelon libraries), but there will be important pieces of their application where it is not.
- pg_crdt is an extension which adds CRDT support to Postgres as a data type.
  - The `content` column is now a Yjs Doc. 
  - Updates to this column are commutative and idempotent. 
  - This means that they can be applied in any order and multiple times, and the result will always be the same.
- both Yjs and Automerge have JavaScript and Rust implementations, which means they work natively in both a browser and a Postgres environment. 

- ❓ Why not build this into Realtime?
- An alternative approach for CRDT support in Supabase is to build support directly into Realtime and use it as an Authoritative server.
  - In this scenario, Realtime would serialize the CRDT and save it to Postgres (probably as a bytea data type). 
  - Yjs has the concept of Providers which would facilitate this. 
- realtime as an authority
  - Realtime acts as the “middleman” for saving the CRDT in the database
- postgres as an authority
  - CRDT is pushed directly to the database, and Realtime receives updates from Postgres. (Note also that clients can send peer-to-peer updates.)
- If we make Realtime the authority, it strongly couples developers to the Supabase infrastructure. 
  - By placing the CRDT into the database, it simplifies the architecture, enables other tools (like Debezium), and provides the possibility to update the database directly (for semi-realtime events like counters or page-views).

- These are a few of the known limitations:
  - Realtime broadcasts database changes from the Postgres write ahead log (WAL). The WAL includes a complete copy of the the underlying data so small updates cause the entire document to broadcast to all collaborators
  - Frequently updated CRDTs produce a lot of WAL and dead tuples
  - Large CRDT types in Postgres generate significant serialization/deserialization overhead on-update.
# 👥 [Show HN: Pg_CRDT – an experimental CRDT extension for Postgres | Hacker News_202212](https://news.ycombinator.com/item?id=33931971)

- 
- 

- Just store all updates - as if you do event sourcing - ordered by a timestamp. 
  - The list of updates will eventually converge as will any function of that list, including any function that merges all the updates into a current state. 
  - You might have to [partially] reevaluate the function in case a delayed update shows up and has to be inserted into the middle of the list of updates. 
  - So I guess there are additional requirements in order to qualify as a CRDT, bounded additional space or bounded amount of computation on updates. But I don't know as it turned out my understanding of what qualifies as a good CRDT was too narrow.
- Yeah **event sourcing and what you described is what these libraries are calling delta CRDTs**. The appeal is they’re hiding away the actual event log, metadata and rebasing/merging parts and exposing data types that look something like what you’d normally use.
  - And if you tie the conflict resolution logic to the individual delta operations, you get Operational Transforms.

- 
- 

- [pg_crdt - a CRDT extension for #postgresql](https://twitter.com/kiwicopple/status/1601553881246609409) 

- The heavy-lifting is done by the teams at Yjs[0] and Automerge[1], who have re-implemented their JS libs in Rust. This made it possible for us to wrap them into a Postgres extension using pgx[2] (which is fast becoming a de-facto tool at supabase)

- Support for CRDT columns within a db to enable JSON like indexing/querying capabilities is fundamental to then building some exciting further developments. Supporting both Yjs and Automerge is exactly the right route forward.
- did you investigate querying/indexing within the documents?
  - Without the ability to index properties, or do ad-hock queries, on the documents there is little reason to to the merging in-DB. It then makes more sense to merge outside the DB and save both the raw CRDT object and a serialised JSON next to it for querying. I assume that if you had found it's performance better, indexing+querying would have been the next step?
  - Personally I find the offline + eventual consistency the most interesting use case. The ability to sync a users document set to a local db (SQLite or a future mini-pg/supabase) with local querying and then merge them back later. This could be as basic as a three column table (guid, doc, clock), the clock being a global Lamport like clock to enable syncing only changed documents.

> This could be as basic as a three column table (guid, doc, clock), the clock being a global Lamport

This would be achievable, but also perhaps quite strict - we're dictating a table structure rather than working with existing CRDT libs. That said, we could probably do this today, without any mods/extensions

> querying/indexing

Yeah, there is nothing in this implementation for that

> Without the ability to index properties, or do ad-hock queries, on the documents there is little reason to to the merging in-DB

One benefit is the ability to send "directly" to the database, but I agree that lack of additional features in the current form outweighs this benefit

> a serialised JSON

This is how we might do it with with "Realtime as an authority" approach (and is the most likely approach tbh).

- Last Writer Wins is not the most compelling use case for CRDT because if those fruits were denormalized into Postgres rows, you'd already have the behavior described. 
- In general, Sequence CRDTs seem to be the most difficult and most interesting area of continuous research. In my own work, I've implemented a sequence CRDT to create a distributed log of events across users that then (because the order is guaranteed to eventually be the same for each device) can just be reduced to whatever data structure you need. It means, we end up with one CRDT to rule them all and then can just write the "conflict resolution" in simple term with the business logic.
# [去中心化在线协作：Feakin 的图形协作是如何设计的？_202209](https://www.phodal.com/blog/collaboration-with-crdt/)
- 通讯协议：WebSocket vs HTTP
- 数据格式：JSON vs Binary
- 协作算法：中心化还是去中心化？ OT 算法 vs CRDT

- 服务端：Actix + Diamond Types + CRDT
- 客户端：编辑生成 patches
- 客户端：编辑器应用 patches
# [CRDT 解决最终一致问题的利器_201809](https://juejin.cn/post/6844903672032264199)
- 先简单统一一下概念
  - object: 可以理解为“副本”
  - operation: 操作接口，由客户端调用，分为两种，读操作query和写操作update
  - query: 查询操作，仅查询本地副本
  - update: 👉🏻 更新操作，先尝试进行本地副本更新，若更新成功则将本地更新同步至远端副本
  - merge: update在远端副本的合并操作

- 一个数据结构符合CRDT的条件是update操作和merge操作需满足交换律、结合律和幂等律
- 如果update操作本身满足以上三律，merge操作仅需要对update操作进行回放即可，这种形式称为op-based CRDT，最简单的例子是集合求并集。
- 如果update操作无法满足条件，则可以考虑同步副本数据，同时附带额外元信息，通过元信息让update和merge操作具备以上三律，这种形式称为state-based CRDT。
- 让元信息满足条件的方式是让其更新保持__单调__，这个关系一般被称为__偏序关系__。
  - 举一个简单例子，每次update操作都带上时间戳，在merge时对本地副本时间戳及同步副本时间戳进行比对，取更新的结果，这样总能保证结果最新并且最终一致，这种方式称为Last Write Wins
- update操作无法满足三律，如果能将元信息附加在操作或者增量上，会是一个相对state-based方案更优化的选择
- 如果同步过程能确保exactly once的语义，幂等律条件是可以被放宽掉，比如说加法本身满足交换律结合律但不幂等，如果能保证加法操作只回放一次，其结果还是最终一致的。
# [如何设计 CRDT 算法](https://www.zxch3n.com/crdt-intro/design-crdt/)
- 以 Op-based CRDT 的思路设计 Last-write-wins Set(LWWSet)
# [数据库系统小报：CRDT初探](https://zhuanlan.zhihu.com/p/510797688)

# 📝 [5000x faster CRDTs: An Adventure in Optimization__202107](https://josephg.com/blog/crdts-go-brrr/)
- Automerge (and Yjs and other CRDTs) think of a shared document as a list of characters. 
  - Each character in the document gets a unique ID, and whenever you insert into the document, you name what you're inserting after.

- Automerge is based on an algorithm called RGA
  - Automerge (RGA) solves this with a neat hack. It adds an extra integer to each item called a sequence number. 
  - Whenever you insert something, you set the new item's sequence number to be 1 bigger than the biggest sequence number you've ever seen
  - The rule is that children are sorted first based on their sequence numbers (bigger sequence number first). 
- Why is automerge slow though?
  - Automerge's core tree based data structure gets big and slow as the document grows.
  - Automerge makes heavy use of Immutablejs
  - Automerge treats each inserted character as a separate item.

- Yjs - which we'll see more of later - implements a CRDT called YATA. 
- YATA is identical to RGA, except that it solves this problem with a slightly different hack. 
- Instead of implementing the CRDT as a tree like automerge does
  - Yjs just puts all the items in a single flat list

- how do you insert a new item into a list? 
- With automerge(tree) it's easy:
  - Find the parent item
  - Insert the new item into the right location in the parents' list of children
- But with this list approach it's more complicated:
  - Find the parent item
  - Starting right after the parent item, iterate through the list until we find the location where the new item should be inserted (?)
  - Insert it there, splicing into the array

- I implemented both Yjs's CRDT (YATA) and Automerge using this approach in my experimental reference-crdts codebase
  - It's hard to understand, but once you understand it, you can implement the whole insert function in about 20 lines of code

- The important point is this approach is better:
  - We can use a flat array to store everything, rather than an unbalanced tree. This makes everything smaller and faster for the computer to process.
  - The code is really simple. Being faster and simpler moves the Pareto efficiency frontier. Ideas which do this are rare and truly golden.
  - You can implement lots of CRDTs like this. Yjs, Automerge, Sync9 and others work. You can implement many list CRDTs in the same codebase. In my reference-crdts codebase I have an implementation of both RGA (automerge) and YATA (Yjs). They share most of their code (everything except this one function) and their performance in this test is identical.
# 📝 [I was wrong. CRDTs are the future__202009](https://josephg.com/blog/crdts-are-the-future/)
- I saw Martin Kleppmann’s talk a few weeks ago about his approach to realtime editing with CRDTs, and I felt a deep sense of despair(绝望). 
  - Maybe all the work I’ve been doing for the past decade won’t be part of the future after all, because Martin’s work will supersede it. Its really good.
- Around 2010 I worked on Google Wave. 
  - Wave was an attempt to make collaboratively editable spaces to replace email, google docs, web forums, instant messaging and a hundred other small single purpose applications. 
- Internally, Wave’s collaborative editing was built on top of Operational Transform (OT). 
  - OT has been around for awhile - the algorithm we used was based on the original Jupiter paper from 1995. 
  - It works by storing a chronological(按时序排列的) list for each document of every change.
- Most of the time, users are editing the latest version of the document and the operation log is just a list of all the changes. 
  - But if users are collaboratively editing, we get concurrent edits. 
  - When this happens, the first edit to arrive at the server gets recorded as usual. 
  - If the second edit is out of date, we use the log of operations as a reference to figure out what the user really intended. (Usually this just means updating character positions). 
  - Then we pretend as if thats what the user meant all along and append the new (edited) operation. 
  - Its like realtime git-rebase.
- Once Wave died, I reimplemented the OT model in ShareJS.
  - https://github.com/josephg/sharejs
  - It only took about 1000 lines of code to get a simple collaborative editor working
  - At its heart, OT is a glorified(吹捧的；吹嘘的；美化的) `for()` loop with some helper functions to update character offsets. 
  - In practice, this works great. OT is simple and understandable. 
  - Implementations are fast. (10k-100k operations per second in unoptimized javascript. 1-20M ops/sec in optimized C.). 
  - The only storage overhead is the operation log, and you can trim that down if you want to. (Though you can’t merge super old edits if you do). 
  - You **need a centralized server to globally order operations**, but most systems have a centralized server/database anyway, right?

- The **big problem with OT is that dependency on a centralized server**.
  - The reason (I think) is that when you open a google doc, one server is picked as the computer all the edits run through. When the mob descends, google needs to pull out a bunch of tricks so that computer doesn’t becomes overwhelmed.
- There’s some workarounds they could use to fix this. 
  - Aside from sharding by document (like google docs), you could edit via a retry loop around a database transaction. 
  - This pushes the serialization problem to your database. (Firepad and ShareDB work this way).
  - Its not perfect though. 
  - We ended up with a scheme where every wave would arrange a tree of wave servers and operations were passed up and down the tree. But it never really worked. 
  - I don’t think they were ever fixed in the opensource version. Its all just too complicated.

- researchers have been busy trying to make OT work better. 
  - The most promising work uses CRDTs (Conflict-Free Replicated data types). 
  - CRDTs approach the problem slightly differently to allow realtime editing without needing a central source of truth.
- People have been asking me what I think of them(CRDT)
  - They’re slow. Like, really slow. Eg Delta-CRDTs takes nearly 6 hours to process a real world editing session with a single user typing a 100KB academic paper.
  - Because of how CRDTs work, documents grow without bound. The current automerge master takes 83MB to represent that 100KB document on disk. It needs to be loaded into memory to handle edits.
  - CRDTs are missing features that OT has had for years. For example, nobody has yet made a CRDT that supports /object move/ (move something from one part of a JSON tree to another). 
  - CRDTs are complicated and hard to reason about.
  - You probably have a centralized server/database anyway.
- I made all those criticisms and dismissed CRDTs. But in doing so I stopped keeping track of the literature. 

- CRDTs went and quietly got better.
  - Speed: Using modern CRDTs (Automerge/RGA or y.js/YATA), applying operations should be possible with just an log(n) lookup. 
  - Size: Martin’s columnar encoding can store a text document with only about a 1.5x-2x size overhead compared to the contents themselves. 
  - Features: There’s at least a theoretical way to add all the features using rewinding and replaying, though nobody’s implemented this stuff yet.
  - Complexity: I think a decent CRDT will be bigger than the equivalent OT implementation, but not by much. 
- Martin managed to make a tiny, slow implementation of automerge in only about [100 lines of code](https://github.com/automerge/automerge/blob/main/test/fuzz_test.js).
  - https://github.com/automerge/automerge
  - A JSON-like data structure (a CRDT) that can be modified concurrently by different users, and merged again automatically.
  - Automerge is a library of data structures for building collaborative applications in JavaScript.
- I still wasn’t completely convinced by the speed argument, so I made a simple proof of concept CRDT implementation in Rust using a B-tree using ideas from automerge and benchmarked it.
  - So that means we’ve made CRDTs good enough that the difference in speed between CRDTs and OT is smaller than the speed difference between Rust and Javascript.
- automerge isn’t the only decent CRDT out there. 
  - Y.js works well and kicks the pants off automerge’s current implementation in the Y.js benchmarks. 
  - Its missing some features I want, but its generally easier to fix an implementation than invent a new algorithm.

- I care a lot about inventing the future.
  - But I’m no longer convinced OT - and all the work I’ve done on it
  - I feel really sad about that.
- JSON and REST are used everywhere these days. Lets say in 15 years realtime collaborative editing is everywhere. Whats the JSON equivalent for realtime editing that anyone can just drop in to their project? 
  - In the glorious future we’ll need high quality CRDT implementations, because OT just won’t work for some applications. 
  - You couldn’t make a realtime version of Git, or a simple remake of Google Wave with OT. 
- But if we have good CRDTs, do we need good OT implementations too? I’m not convinced we do. 
  - Every feature OT has can be put in to a CRDT. (Including trimming operations, by the way). But the reverse is not true.
  - Smart people disagree with me, but if we had a good, fast CRDT available from every language, with integration on the web, I don’t think we need OT at all.
- OT’s one advantage is that it fits well in centralized software - which is most software today. 
  - But distributed algorithms work great in centralized software too. (Eg look at Github). 
  - And I think a really high quality CRDT running in wasm would be faster than an OT implementation in JS. 
  - And even if you only care about centralized systems, remember - Google runs into scaling problems with Google Docs because of OT’s limitations.
- So I think its about time we made a lean and fast CRDT. The academic work has been mostly done. We need more kick-ass implementations.
- I increasingly don’t care for the world of centralized software.
  - Philosophically, if I modify a google doc my computer is asking Google for permission to edit the file. 
  - (You can tell because if google’s servers say no, I lose my changes.
- In comparison, if I git push to github, I’m only notifying github about the change to my code. My repository is mine.
  - I own all the bits, and all the hardware that houses them. 
  - This is how I want all my software to work.
- Thanks to people like Martin, we now know how to make good CRDTs. 
  - But there’s still a lot of code to write before local first software can become the default.
  - I mourn all the work I’ve done on OT over the years. 
  - But OT is no longer fits into the vision I have for the future. 
  - CRDTs would let us remake Wave, but simpler and better. 
  - And they would let us write software that treats users as digital citizens, not a digital serfs(农奴).
# 👥 [CRDTs are the future | Hacker News_202204](https://news.ycombinator.com/item?id=31049883)
- I don't really understand why every single article on CRDTs is about collaborative text editing. Is no one else bothering to build systems with CRDTs outside of this space?
- Why have I been focussing on collaborative text editing? Because I think performance has been the #1 blocker stopping us from using CRDTs in most software. And text CRDTs are a canary in the coal mine for performance. Uh, thats a tortured metaphor. I mean, If we can make text CRDTs fast, we can make everything fast.
  - And JSON editing (what everyone actually wants) needs to embed text editing anyway. So we've sort of gotta do that first anyway.
  - Smart people have also been working on the JSON editing problem. 
  - Shelf algorithm for last-writer-wins JSON editing is simple enough you can implement it in less than 100 lines of code. But shelf doesn't support collaborative list or text editing (text is a list of characters).
  - thats something Yjs and automerge both already do, and do quite well.

- 👉🏻 Probably because outside collaborative text editing, it's called more generally, like CQRS or event sourcing

- More generally, CRDTs are useful when syncing any kind of change-events between peers (with no central ability to pre-linearize those events), where the ordering of change-events doesn't matter — i.e. where the operations described by the events are "commutative", such that you'll get the same results out if you apply events {1, 2, 3} or {3, 2, 1} or any other order. 
  - As long as all peers see all events, all peers arrive at the same eventually-consistent position in the "lattice" of possible states. 
  - In other words, CRDTs + gossip protocols = the ability for peers to just process events as they hear about them, without a worry about receiving events from peers "out of order"; rather than needing to wait around for a some elected peer to forcibly linearize the events (i.e. without the need to introduce a serial write bottleneck.)
- A good example of the distributed-systems-backend kind of use of CRDTs, is in the Elixir web framework Phoenix, which does a sort of mesh delivery of web-socket messages between a cluster of backends. CRDTs are used to sync presence information (= which clients are connected to which backend) between the backends.
- On the other hand: A lot of practical applications are fine with last write
- I’m more excited about the use of CRDTs outside of text editing, there are so many use cases. However there are still some problems to solve with the existing general purpose toolkits such as Yjs and Automerge. 
  - Take Yjs and it’s ProseMirror bindings, Yjs can represent any internal state of a ProseMirror document and merge them. However it does not have an understanding of the specific ProseMirror schema being used, this could limit the valid states possible (a max length on a heading for example). When Yjs merges multiple edits you could end up with an invalid document for your schema, Yjs loads this into ProseMirror which then throws away the invalid data (with the heading example it just deletes the excess text, it may be better to dump it into the next line but should be configurable).
  - Ultimately the general purpose CRDT toolkits need to have more internal types with a wider ability to capture intent. I also think they need to have the ability to understand the schema of the data structure they are tracking and how to handle more complex merges.
  - The alternative to doing that with a general purpose toolkit is to build your own CRDTs from scratch for your data model. I don’t think many people would go that route though.
- Not all CRDT libraries focus on text editing. For example, I'm working on a Byzantine fault tolerant general-purpose data sync library loosely based on CRDTs: https://www.hyperhyperspace.org

- We at www.ditto.live will likely get to a SQL like implementation with Delta state CRDTs this year.
# 👥 [CRDTs are the future | Hacker News_202009](https://news.ycombinator.com/item?id=24617542)
- I'm part of the team that makes Zoho Writer (a Google Docs alternative)
  - We went with OT for our real-time syncing of edits in 2010 and a decade later, we are still sticking with OT
  - However, in the spirit of "There are no solutions, only trade-offs" CRDTs are absolutely necessary for certain type of syncing - like syncing a set of database nodes.
  - But for systems which already mandate a central server (SaaS/Cloud) and especially for a complex problem like rich-text editing (i.e semantic trees) I still think OT provides better trade-offs than CRDT.
- We went with OT five years ago in CKEditor 5 and we have the same experience. While it would be tempting to try CRDT, it seems to come with too significant tradeoffs in our scenario.

- Right now if you want you can use yjs or sharedb. But the APIs aren't spectacular. Eventually I want these things integrated into svelte / react / swiftui and postgres / sqlite / whatever so it just sort of all works together and we get nice tutorials taking you through what you need to know.
  - We aren't there yet. Automerge is slow (but this is being worked on). Yjs is hard to use well with databases, and its missing some features. We'll get there. The point of all the mathematical formalisms is that if we do it right, it should just work and you shouldn't have to understand the internals to use it.
- It's worth noting that many of the CRDT discussions focus on collaborative text editing. That's a really hard problem. CRDTs are (and have been for some time) a useful primitive for building distributed systems.

- 
- 
- 

# 📝 [Are CRDTs suitable for shared editing?__202008](https://blog.kevinjahns.de/are-crdts-suitable-for-shared-editing/)
- CRDT don't require a central authority to resolve sync conflicts
  - They open up new possibilities to scale the backend infrastructure and are also well-suited as a data-model for distributed apps that don't require a server at all.
- However, several text editor developers report not to use them because they impose a too significant overhead.
- Marijn Haverbeke wrote about his considerations against using CRDTs as a data model for CodeMirror 6
  - the cost of such a representation is significant, and in the end, I judged the requirement for converging positions to be too obscure to justify that level of extra complexity and memory use
- The Xi Editor used a CRDT as its data model to allow different processes (syntax highlighter, type checker, ..) to concurrently access the editor state without blocking the process. They reverted to a synchronous model because
- [CRDT is not pulling its (considerable) weight.__201905](https://github.com/xi-editor/xi-editor/issues/1187#issuecomment-491473599)
  - By now we have lots of examples where trying to design features around the structure imposed by CRDT turned out to be a lot more complicated than it would be in a more synchronous world - we saw the auto-indent stuff above, difficulty getting the selection right in transpose
  - CRDT is a tradeoff
# 👥 [Are CRDTs suitable for shared editing?_202008](https://news.ycombinator.com/item?id=24176455)
- I’m part of the team that makes Zoho Writer (Google Docs alternative)
  - Back in 2009, we wrote our real time collaboration component using Operational Transformations (OT). 
- But when CRDTs started to gain the spotlight, these are the reasons why it didn’t warrant a rewrite to our stack:
  1. Memory issues with tombstones(墓碑). Marking as deletion has a cost of maintaining them throughout the session.
  2. CRDTs were perfect for plain strings and arbitrary key/value pairs. But when it comes to schematic JSON that has semantic value, CRDT was an added overhead. For example, try making a collaborative HTML editor with support for table operations. It is very likely you will end up with a table structure that is invalid to render. In OT analysing, modifying or cancelling ops were much easier.
  3. Since the software is primarily a cloud document editor, a central server is necessary even otherwise. So why not use the server for efficient version management and operation sequencing as well? Why prefer CRDTs whose bulk of complexity comes from eliminating the need of a central system?
- Such practical reasons have kept us from venturing into CRDTs. 
  - As of now, common editing platforms like Google Docs, Zoho Writer, CKEditor, ProseMirror, Quill, CodeMirror - all of these work with OTs instead of CRDT for collaborative editing.
- I think the main impetus for this post is to assert that #1 and #2 aren't much of a problem for Yjs, as they are for the arguably more well-known CRDT lib for JS, Automerge.
  - With respect to #3, one reason to prefer CRDTs over OT (even if a central server is required for other stuff) is that making the collaboration infra P2P can save a lot of resources if most of your collab is happening between a few individuals at a time. 
  - Not very necessary at a small scale, but if you have 10, 000 small teams collab'ing, the cost savings you get from off-loading RTC to the end users can definitely add up.

- OT doesn’t require a central server, just a tie breaker. You could just do leader election over webRTC using raft and offload OT to the client side as well and have that node push updates to the server for durable saving every x seconds and shift RTC off your infra.
  - Right, the idea that OT requires a "central server" is a bit of an oversimplification. It requires an authority that can serialize concurrent revisions into a globally consistent sequence. By far the easiest way to achieve that is an actual central server, but distributed algorithms have also been published for a long time, for example SOCT2 which uses a state vector.
  - **The downside is the complexity**. Now there are more things that can go wrong: the OT algorithm can fail (either due to bugs or because of corrupted data), and now also the distributed consensus algorithm can fail as well. 
  - When you have this level of complexity, going to CRDT is pretty appealing as an alternative.

- I've implemented operational transform based systems several times, and every time I check out CRDTs I end up staying with OT.
  - I find the complexity arguments against OTs to be far, far overblown and mostly academic, and that OT is, for me, much easier to understand.
  - The **two big critiques against OT are transform explosion**: you could have N^2 transforms. Except that not every operation pair interacts. I usually see just a couple of categories of operations: text, key/value, tree, and list, and they all only need transforms within a category.
  - The **second critique is around sequencing in a distributed system**, but I've also never seen a production system that doesn't have a central coordinating service. With a star topology OT sequencing because simple. You don't even need a lamport clock, you can get away with a simple counter. Buffering at the clients simplifies even more.
  - There's a great series of posts on collaborative editing by Marijn Haverbeke, the author of CodeMirror and ProseMirror, that are designed with OT in mind

- It seems like CRDTs would be useful for contact tracing in that distributed contact tracers collect data on cases and potential cases. They operate independently for hours through the day with occasional network access or at least end of day.
  - Since there is no concurrency in contact tracing (only you will manipulate your own data), a CRDT might be an unnecessary overhead. 
  - There is concurrency in contact tracing. In developing nations it’s like a map reduce problem. You send out the contact tracers in the morning, they gather results and sync up at the end of the day.
# crdt: state-based/CvRDTs vs operation-based/
- [Two kinds of CRDTs · CRDTs: Part 8](https://lars.hupel.info/topics/crdt/08-outlook/)

- you might think that operation-based CRDTs are superior to their value-based friends. 
  - The messages are smaller and they allow you to do more things since they are not constrained by monotonicity. 
  - But there’s a catch (of course there is): The convergence theorem for them requires reliable broadcast channels. 
  - That is: if a message with an operation gets lost, suddenly your replicas won’t agree on the correct value anymore. 
  - It’s not impossible to set up a reliable channel

- [A service framework for operation-based CRDTs - Martin Krasser's Blog](http://krasserm.github.io/2016/10/19/operation-based-crdt-framework/)

- State-based CRDTs are designed to disseminate state among replicas whereas operation-based CRDTs are designed to disseminate operations.
- CmRDT/op replicas are guaranteed to converge if operations are disseminated through a **reliable causal broadcast (RCB)** middleware and if they are designed to be commutative for concurrent operations.
- CvRDTs/state don’t require special guarantees from the underlying messaging middleware but require increasing network bandwidth for state dissemination with increasing state size. 
  - They converge if their state merge function is defined as a join: a least upper bound on a join-semilattice. CvRDTs are not further discussed in this article.

- The execution of a CmRDT operation is done in two phases,  `prepare` and `effect` (also called `atSource` and `downstream` ): 
  - prepare is executed on the local replica. It looks at the operation and (optionally) the current state and produces a message, representing the operation, that is then disseminated to all replicas. 
  - effect applies the disseminated operation at all replicas.
# [CRDT: Conflict-free Replicated Data Types](https://medium.com/@amberovsky/crdt-conflict-free-replicated-data-types-b4bfc8459d26)
- State-based/CvRDT
  - replicas propagated changes by sending a full state of the objects.
  - A merge() function must be defined to merge incoming changes with the current state.
  - Used in such file systems as NFS, AFS, Coda and in such KV-storages like Riak, Dynamo.

- Operation-based/CmRDT
  - replica propagates changes by sending the operation to all replicas.
  - Used in such cooperative systems, like Bayou, Rover, IceCube, Telex.

- Delta-based
  - combines both State/op approaches and propagates so-called delta-mutators which update the state accordingly to the last synchronisation date. 
  - You need to send a full state in case of the first ever synchronisation, however, some realisations actually consider the state of the remote replicas to lower the amount of needed data.

- Pure operation-based
  - There is a delay in the op-based synchronization to create an effector(). 
  - In some systems such delays are unacceptable. 
  - In this case an update must be propagated immediately at the cost of more complex organization protocol and more space requirements for metadata.

- op-based synchronization requires effector() to be delivered only once to each replica. 
  - 👉🏻 This requirement can be loosened by requiring effector() to be idempotent. 
  - In practice, it is much easier to implement the former than the latter.

- Op-based and State-based synchronizations can be emulated(仿真，模拟) by each other with keeping CRDT requirements. 
# 📝 [Introduction to CRDTs for Realtime Collaboration](https://dev.to/nyxtom/introduction-to-crdts-for-realtime-collaboration-2eb1)
- 对各种数据类型进行了简介

- Data consistency is hard.
  - Approaches to this usually take the form of ACID guarantees, BASE (basically available, eventually consistent) and in the case of CRDT strong eventual consistency. 

- How do we get events to be in the right order?
  - We can use the server's timestamp in a typical architecture to serve as the authoritative clock but this isn't available in distributed systems.
  - Logical Timestamps. Doing this kind of ordering helps us get closer to total ordering.
  - Event Logs. this is typically called event sourcing, where every operation is stored as data and playback is used when you need to construct the model. To give a log total ordering we need to sort operations by time and then by unique origin.

- Consider how Figma makes these tradeoffs by combining multiple CRDT-inspired techniques (associativity, commutativity, idempotent) with a last-write-wins (LWW) approach and a central server to coordinate some aspects of conflicts and updates.
  - Other things like tree re-ordering in the document, undo/redo behaviors, are resolved with domain specific desired implementations. 
  - Additionally, Figma side-steps the entire realtime text interleaving/merging issue due to the fact that the text content of a text element is just another property on an object.
  - As such, changes in this system still follow the LWW model they have gone with.
- Additionally, they go over the Fractional Indexing approach that looks very much like the approach seen in Logoot/LSEQ.

- Given that you have no record of tombstones (like in the case of Logoot/LSEQ) then you run into the problem of interleaving edits on merge. 
  - However, Figma can make this trade-off due to the fact that it is a design tool not necessarily centered around realtime text editing.

- OR-Set (Observed-Remove Set) 
  - Similar to LWW-Element-Set except uses tags instead of timestamps. 
  - For each element in the set, a list of add-tags and a list of remove-tags are maintained. 
  - Insertions are done by generating a unique tag and added to the add-tag list for the element. Elements are removed by having all the tags in the element's add-tag list added to the element's remove tag set (tombstone list). 
  - Merging is done by the union of the add-tag list for each element, and the union of remove-tag lists for each element. 
  - An element is a member if the element's add tag list - remove tag list is nonempty.

- Logoot/LSEQ/TreeDoc does not store tombstone deletions and instead takes an approach with fractional/unbounded divisible indexing. 
  - This, as discussed earlier, can cause issues with interleaving edits so it becomes impractical to guarantee proper sane convergence with concurrent operations.

- RGA
  - Widely considered to be one of the fastest CRDT implementations. 
  - Utilizes a timestamped insertion tree and references hash table lookups for character lookups. 
  - Causal trees are a similar approach (named CT but in RGA it's called a timestamped insertion tree). 
  - In any case, CT/RGA algorithms have been proven to use the same algorithm
# 📝 [CRDTs The Hard Parts 笔记_202010](https://zhuanlan.zhihu.com/p/265074361)
- 包括 Google Docs、Figma、Trello 在内的协同编辑软件，需要依赖收敛算法（convergence algorithms）使得不同节点上发生的修改可以确定地（deterministically）合并到一致的状态。
  - 最常见的收敛算法有两类：OT（Operational Transformation）和 CRDT（Conflict-free replicated data type）。

- 首先以 Google Docs 为例介绍 OT。
  - server 会接收不同节点的写，按照规则调整插入的 offset
  - OT 的关键在于使用 server 统筹不同节点的写。
  - OT 保证了只要两个节点接收到同一列操作，即便两列操作的顺序不同，节点上的状态也肯定收敛至相同状态。
- 收敛是很好的性质，但收敛到的状态是否合意（desirable），还需要人为的判断，这一点对于 CRDTs 同样适用。
  - 相比 OT，CRDT 的合并是去中心化的，无需通过 server，但同样需要保证合并是合意的。

## CRDTs: Interleaving anomalies(异常事物)

- 方案一：给新插入的字母分配一个位于[0, 1]的数字。
  - 这种方法确实能保证收敛，但下面这种情况明显不是合意的收敛
  - 这种 interleaving 发生在很多 CRDTs（包括 Logoot、LSEQ、Astrong）实现中，而且没办法修复，因为问题根植在算法本身。

- 方案二：RGA。一种叫做 RGA 的 CRDT 算法存在不那么严重的 interleaving 问题。
  - 用户 2 输入的 Alice 可能被插入到用户 1 输入的 dear 和 reader 之间，原因在于 RGA 使用了一种基于时间戳的列表数据结构。
  - 根据 RGA 算法，用户的节点上会形成一个如下的树状链表，每个节点都指向输入时该位置所位于的节点

## CRDTs: Moving list items

- 许多 CRDTs 都实现了 List 数据结构，但不支持 move 操作。
  - 用户可以把 move 拆解为 delete-then-insert。
  - 但是会发生下面的 anomaly。
  - 需要找到一个合适的数据结构来表达 pos，让 pos 具有 last writes win 的性质
  - 每个 list item 都要有一个 LWWRegister，并把它们放在一个 Add-Wins Set (AWSet) 中

## CRDTs: Moving subtrees of a tree

- 在一棵树内移动子树也是个很 tricky 的问题，但是这样的场景比较常见，例如文件系统就是一棵树。
- 一个可行的解决办法是引入操作的时间戳。

## CRDTs: Reducing metadata overhead

- 为了完成 undo 和 redo，CRDT 需要存储很大的 metadata
- Martin 开始介绍 automerge 项目，他的 proposal 和 PR#253 使用 columnar encoding 的思路，使得 CRDT 的 overhead 变得很小。
# more-crdt
- [CRDTs and Realtime Collaboration](https://nyxtom.dev/2020/09/01/intro-to-crdts)

- [Collaborative Web Apps_202108](https://zjy.cloud/posts/collaborative-web-apps)
  - At the time of the writing, one shortcoming of Replicache is that its local transactions are not fast enough to enable heavy interactions such as drag and drop. 
  - To prevent lagging, we turned on the useMemstore: true option to disable offline support. 

- [CRDTs: Part 7 Registers and Deletion](https://lars.hupel.info/topics/crdt/07-deletion/)

- [CRDT Implementations](https://jzhao.xyz/thoughts/CRDT-Implementations/)

- [CRDT: 分数排序 Fractional Indexing](https://hyrious.me/p/crdt-fractional-indexing)
