---
title: lib-collab-crdt-blog
tags: [blog, collaboration, crdt]
created: 2022-10-13T07:59:52.953Z
modified: 2022-10-13T08:00:21.260Z
---

# lib-collab-crdt-blog

# guide

- resources
  - [CRDT Tutorial for Beginners](https://github.com/ljwagerfield/crdt)
  - [arXiv: collaborative editing](https://arxiv.org/search/?query=collaborative+editing&searchtype=all&source=header)
# [CRDT Survey, Part 1: Introduction - Matthew Weidner](https://mattweidner.com/2023/09/26/crdt-survey-1.html)
- the beginning of a survey of CRDT techniques and how to apply them to collaborative apps.
  - This post gives a gentle definition of op-based and state-based CRDTs and outlines my goals for the survey.
  - Part 2 of my CRDT survey blog series is out! This post covers "semantic techniques": deciding what a collaborative should do for users, independent of implementation details like op-based vs state-based.
# [Making CRDTs 98% More Efficient | jakelazaroff.com_202310](https://jakelazaroff.com/words/making-crdts-98-percent-more-efficient/)
- ## JSON structures are not good when you have a lot of events. Binary structures are better for CRDT log.
- https://twitter.com/sitnikcode/status/1775917335863271616
  - It uses a graphical editor as an example, but the same approach is used for text.
# 👨🏻‍🏫 [CRDTs Turned Inside Out _202312](https://interjectedfuture.com/crdts-turned-inside-out/)
- There is another class of CRDTs: Merkle CRDTs.
- Merkle-DAG CRDTs
- Merkle Search Tree CRDTs

- [Trade-offs between Different CRDTs | Hacker News](https://news.ycombinator.com/item?id=38916647)
# 👥 [CRDTs Turned Inside Out | Hacker News _202401](https://news.ycombinator.com/item?id=39130945)

# 👨🏻‍🏫 [Understanding CRDTs: A Gentle Introduction (Chapter 1) _202401](https://federicoterzi.com/blog/understanding-crdts-a-gentle-introduction-chapter-1/)

- https://github.com/federico-terzi/crdt-experiments /MIT/202402/rust
  - An experimental, high-performance CRDT JSON data structure in Rust

- 👥 [Understanding CRDTs: A Gentle Introduction | Hacker News](https://news.ycombinator.com/item?id=39092787)
# 👨🏻‍🏫 [A Gentle Introduction to CRDTs – vlcn.io](https://vlcn.io/blog/intro-to-crdts)
- Last Write - What Can Go Wrong?
  - Error 1: Forgetting to Update the Loser's Timestamp
  - Error 2: Forgetting & Inconsistent Tie Breaking
  - Error 3: Clock Pushing when Proxying Changes, A向中间代理B请求12点后的changes，B向C请求11点后的
  - Error 4: Trusting System Time

- The simplest logical clock implementation is simply to keep an integer in your process that you increment for every event. 
  - Each event gets timestamped with this counter.
  - To totally order events within your process, order by that timestamp. 
  - To scale this up to many cores, use an atomic integer that you can compare-and-swap.
# 👨🏻‍🏫 [An Interactive Intro to CRDTs | jakelazaroff.com_202310](https://jakelazaroff.com/words/an-interactive-intro-to-crdts/)
- A register is a CRDT that holds a single value. 
    - There are a couple kinds of registers, but the simplest is the Last Write Wins Register (or LWW Register).
- LWW Registers simply overwrite their current value with the last value written. 
  - They determine which write occurred last using timestamps, represented here by integers that increment whenever the value is updated.

- You might ask: why not use the actual time? 
  - Unfortunately, accurately syncing clocks between two computers is an extremely hard problem. 
  - Using incrementing integers like this is **one simple version of a logical clock**, which captures the order of events relative to each other rather than to the “wall clock”.
# 👥 [An interactive intro to CRDTs | Hacker News_202310](https://news.ycombinator.com/item?id=37764581)
- In practice, most apps will only need Last-Writer-Wins registers and not the more complicated sequence CRDT's that you find in Y.js and Automerge.
  - We've built a auto-syncing database that uses CRDTs under the hood but never exposes them through the API. So if you want all of the benefits of CRDTs e.g. offline-first user experience, checkout our project, Triplit!
- why didn't/don't you build Triplit on cr-sqlite?
  - We're aware of cr-sqlite and I've talked to the author, Matt, a few times. 
  - Short answer: SQLite has serious shortcomings when it comes to reactivity and we think we can be as fast as SQLite for the application-type queries we aim to support. 
  - The long answer would be about supporting all of features we don't need in SQLite and all of the quirks that come with it like having `null` as a primary key
  - We also recently came up with a relational-style querying system without joins
# 📝 [Building a Collaborative Pixel Art Editor with CRDTs | jakelazaroff.com](https://jakelazaroff.com/words/building-a-collaborative-pixel-art-editor-with-crdts/)
- In An Interactive Intro to CRDTs, we learned what CRDTs are, and implemented two: a **Last Write Wins Register** and a **Last Write Wins Map**. 
  - We now have everything we need to build a collaborative pixel art editor
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
# more-crdt
- [CRDTs and Realtime Collaboration](https://nyxtom.dev/2020/09/01/intro-to-crdts)

- [Collaborative Web Apps_202108](https://zjy.cloud/posts/collaborative-web-apps)
  - At the time of the writing, one shortcoming of Replicache is that its local transactions are not fast enough to enable heavy interactions such as drag and drop. 
  - To prevent lagging, we turned on the useMemstore: true option to disable offline support. 

- [CRDTs: Part 7 Registers and Deletion](https://lars.hupel.info/topics/crdt/07-deletion/)

- [CRDT Implementations](https://jzhao.xyz/thoughts/CRDT-Implementations/)

- [CRDT: 分数排序 Fractional Indexing](https://hyrious.me/p/crdt-fractional-indexing)
