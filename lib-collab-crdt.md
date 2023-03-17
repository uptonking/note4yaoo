---
title: lib-collab-crdt
tags: [collaboration, crdt, pattern]
created: 2021-07-23T15:50:09.211Z
modified: 2022-04-05T10:10:08.537Z
---

# lib-collab-crdt

# guide

- 协作方案参考
  - Liveblocks, synced-store, FluidFramework, gundb, pouchdb
  - automerge (2017), yjs (2015), sharedb (2013)

- state-based和operation-based没必要二选一，两者可转换
  - 两者的主要区别
    - 基于op的数据更新操作逻辑和数据结构设计起来可能较复杂
    - 基于op的节点间交换的数据量一般较少
    - 基于op依赖可靠的传输来保证操作的因果性 Reliable Causal Broadcast(RCB)，不可丢失或重复
  - 对于业界成熟的实现如yjs，是结合两种方式来优化性能的

- crdt的结构实现
  - id设计: counter, timestamp, array
  - op-insert: sort+insert
  - gc: tombstone
  - interleaving

- crdt的常见数据结构
  - base-data-structures
    - Counter
    - Last Write Wins Register
    - Multi Value Register
    - Growing-only Set
  - 基于state
    - Growing-only Counter
    - PNCounter
    - 2-Phase Set
    - Observed Remove Set
    - Delta-state growing-only counter
    - (replica-id, sequence-nr), aka. dot
    - Delta-aware Add-Wins Observed Remove Set
  - 基于operation
    - Lseq
    - RGA
    - Block-wise Replicated Growable Arrays
  - 基于sequence
    - woot
    - logoot/lseq
    - treedoc
    - conclave
    - yata/yjs
    - chronofold

- 实现协作要考虑到切换冲突处理算法，如slate-yjs/automerge/sharedb

- [Bartosz Sypytkowski crdt series](https://www.bartoszsypytkowski.com/the-state-of-a-state-based-crdts/)
# [cs-repeat: CRDTs for Mortals_James Long__201912](https://www.youtube.com/watch?v=DEcwa68f-jY)
- Why haven’t “offline-first” apps taken off?
  - syncing is hard
  - local apps are a distributed system
- why local-first
  - offlineable
  - fast
  - privacy
  - ad-hoc queries

- 👉🏻 hard parts 1: unreliable ordering
- 传统数据库是strong consistency
- 最近流行 eventual consistency，允许操作order不同
  - 每个客户端接收的changes顺序不同，最终达到最终一致
- 为了解决顺序判断，用timestamp时间戳的思路
  - 全局的id，跨客户端的clock
  - vector clock
  - HLC/hybrid logical clock
- hlc会生成时间戳
  - assign clock to a change, 以便于可以比较change
  - hlc比较大小
 
- 👉🏻 hard parts 2: conflicts
- 根据时间戳保证交换律(乱序)、幂等
- 基础数据结构：lww-map(处理changes) + g-set(处理数据状态)
  - 使用grow-only set因为可能后面changes会有相关操作
- How to take basic relational data and turn it into CRDTs?
  - SQLite table  =>  G-Set of LWW-Maps
  - msg-table, 若id不存在，就插入新row
- 读取查询很快
- 更新数据时，update-self，push changes to others
- 删除时，添加tombstone字段，并未物理删除

```JS
update("transactions", {
  id: "30127b2e-f74c-4a19-af65-debfb7a6a55b",
  name: "Kroger",
  amount: 450
})

// becomes

[{
  dataset: "transactions",
  row: "30127b2e-f74c-4a19-af65-debfb7a6a55b",
  column: "name",
  value: "Kroger",
  timestamp: "2019-11-02T15:35:32.743Z-0000-85b8c0d2bbb57d99"
}, {
  dataset: "transactions",
  row: "30127b2e-f74c-4a19-af65-debfb7a6a55b",
  column: "amount",
  value: 450,
  timestamp: "2019-11-02T15:35:32.743Z-0001-85b8c0d2bbb57d99"
}]
```

- Other features
  - Ensuring consistency with a merkle tree 
  - End-to-end encryption

- 👉🏻 Conclusion
  - Local apps have superior UX. They are super fast, no latency, and work offline
  - We’ve got to start simplifying our solutions
  - Clocks (particularly HLCs) and CRDTs are an elegant solution to distributed apps

- [crdt-example-app with notes that help describe how things work](https://github.com/clintharris/crdt-example-app_annotated/blob/master/NOTES.md)
# [聊聊CRDT](https://segmentfault.com/a/1190000019109149)
- CRDT是Conflict-free Replicated Data Type的简称，也称为a passive synchronisation，即免冲突的可复制的数据类型，这种数据类型可以用于数据跨网络复制并且可以自动解决冲突达到一致，非常适合使用AP架构的系统在各个partition之间复制数据时使用；
  - 具体实现上可以分为State-based的CvRDT、Operation-based的CmRDT、Delta-based、Pure operation-based等

- State-based(CvRDT)
  - CvRDT即Convergent Replicated Data Type的简称，也称为an active synchronisation，通常在诸如NFS, AFS, Coda的文件系统以及诸如Riak, Dynamo的KV存储中使用
  - 这种方式是通过传递整个object的states来完成，需要定义一个`merge`函数来合并输入的object states
  - 该merge函数需要满足commutative及idempotent，即monotonically increasing，以做到可以重试及与order无关

- Operation-based(CmRDT)
  - CmRDT即Commutative Replicated Data Type的简称，通常在诸如Bayou, Rover, IceCube, Telex的cooperative systems中使用
  - 这种方式是通过传递operations来完成，需要`prepare`方法生成operations，以及effect方法将输入的operations表示的变更作用在local state中
  - 这里要求传输协议是可靠的，如果可能重复传输则要求effect是幂等的，而且对order有一定要求，如果不能保证order则需要effect叠加在一起是or的效果

- Delta-based
  - Delta-based可以理解为是结合State-based及Operation-based的一种改进，它通过delta-mutators来进行replicate

- Pure operation-based
  - 通常Operation-based的方式需要prepare方法生成operations，这里可能存在延时，
  - Pure operation-based是指prepare的实现不是通过对比state生成operations，而是仅仅返回现成的operations，这就需要记录每一步对object state操作的operations

- [Conflict-free replicated data type - Wikipedia](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type)
  - Operation-based CRDTs are also called commutative replicated data types, or CmRDTs. 
    - CmRDT replicas propagate state by transmitting only the update operation. 
    - For example, a CmRDT of a single integer might broadcast the operations (+10) or (−20). 
    - Replicas receive the updates and apply them locally. 
    - The operations are commutative. 
    - 👉🏻 However, they are not necessarily idempotent. 
    - 👉🏻 The communications infrastructure must therefore ensure that all operations on a replica are delivered to the other replicas, without duplication, but in any order.
  - Pure operation-based CRDTs are a variant of operation-based CRDTs that reduces the metadata size.
  - State-based CRDTs are called convergent replicated data types, or CvRDTs. 
    - In contrast to CmRDTs, CvRDTs send their full local state to other replicas, where the states are merged by a function which must be commutative, associative, and idempotent. 
    - The merge function provides a join for any pair of replica states, so the set of all states forms a semilattice. 
    - The update function must monotonically increase the internal state, according to the same partial order rules as the semilattice.
  - Delta state CRDTs (or simply Delta CRDTs) are optimized state-based CRDTs where only recently applied changes to a state are disseminated(散布，传播) instead of the entire state.

- Convergent Operations
  - 对于CRDT来说，为了实现Conflict-free Replicated对数据结构的一些操作需要满足如下条件：
  - Associative
    - (a+(b+c)=(a+b)+c)，即grouping没有影响
  - Commutative
    - (a+b=b+a)，即order没有影响
  - Idempotent
    - (a+a=a)，即duplication没有影响(幂等)

- CRDT的基本数据类型有Counters、Registers、Sets

- Counters
- Grow-only counter(G-Counter)
  - 使用max函数来进行merge
- Positive-negative counter(PN-Counter)
  - 使用两个G-Counter来实现，一个用于递增，一个用于递减，最后取值进行sum

- Registers，有assign()及value()两种操作
- Last Write Wins -register(LWW-Register)
  - 给每个assign操作添加unique ids，比如timestamps或者vector clock，使用max函数进行merge
- Multi-valued -register(MV-Register)
  - 类似G-Counter，每次assign都会新增一个版本，使用max函数进行merge

- Sets
- Grow-only set(G-Set)
  - 使用union操作进行merge
- Two-phase set(2P-Set)
  - 使用两个G-Set来实现，一个addSet用于添加，一个removeSet用于移除
  - the latter is colloquially known as the tombstone set.
- Last write wins set(LWW-element Set)
  - 类似2P-Set，有一个addSet，一个removeSet，不过对于元素增加了timestamp信息，且timestamp较高的add及remove优先
- Observed-remove set(OR-Set)
  - 类似2P-Set，有一个addSet，一个removeSet，不过对于元素增加了tag信息，对于同一个tag的操作add优先于remove

- A sequence, list, or ordered set CRDT can be used to build a Collaborative real-time editor, as an alternative to Operational transformation (OT).
  - Some known Sequence CRDTs are Treedoc, RGA, Woot, Logoot, and LSEQ
- Industrial sequence CRDTs are known to out-perform academic implementations due to optimizations and a more realistic testing methodology.
  - The main popular example is Yjs CRDT, a pioneer in using a plain list instead of a tree (ala Kleppmann's automerge).
  - Deletions in Yjs are treated very differently from insertions. 
  - 👉🏻 Insertions are implemented as a sequential operation based CRDT, but deletions are treated as a simpler state based CRDT.
# [A comprehensive study of Convergent and Commutative Replicated Data Types_201101](https://www.researchgate.net/publication/50949847)
- CvRDT/state-based
  - State-based mechanisms (CvRDTs) are simple to reason about, since all necessary information is captured by the state. 
  - They require weak channel assumptions, allowing for unknown numbers of replicas. 
  - However, sending state may be inefficient for large objects; this can be tackled by shipping deltas, but this requires mechanisms similar to the op-based approach. 
  - Historically, the state-based approach is used in ﬁle systems such as NFS, AFS, Coda, and in key-value stores such as Dynamo and Riak.

- CmRDT/op-based
  - Specifying operation-based objects (CmRDTs) can be more complex since it requires reasoning about history, but conversely they have greater expressive power. 
  - The payload can be simpler since some state is effectively offloaded to the channel. 
  - Op-based replication is more demanding of the channel, since it requires reliable broadcast, which in general requires tracking group membership. 
  - Historically, op-based approaches have been used in cooperative systems such as Bayou, Rover, IceCube, Telex.

- https://github.com/gbogard/crdts-introduction
  - https://crdt.guillaumebogard.dev/
  - A gentle introduction to Conflict-free replicated data types, including visual demos
  - A state-based CRDT is a data structure, together with a binary operation that can produce a single state out of two possibly different states. More formally, a state-based CRDT is a tuple (S, s0, q, u, m)
  - operation-based CRDT is a data-structure whose updates are encoded by operations, and operations are sent over the network. 
    - A new state can be produced given the current state and an operation. 
    - When the structure is modified, the replica responsible for the update generates one or many operations, applies them locally, and then propagates them across the network. 
  - Operation-based CRDTs guarantee that, when operations are successfully propagated, all replicas converge to the same state.
    - Like merging state-based CRDTs, applying operations is associative and commutative, i.e. operations can be applied in any order, however, unlike it isn't necessarily idempotent. It is the responsibility of the transport layer to make sure operations are properly delivered, and not applied more than once.

- [An introduction to Conflict-Free Replicated Data Types](https://lars.hupel.info/topics/crdt/08-outlook/)
  - 一系列的教程
  - [CRDT简介 - 知乎](https://zhuanlan.zhihu.com/p/500375820)
  - state-based CRDTs, or CvRDTs
    - They are simple and elegant because you can merge any two values (of the same data type, of course) and obtain a well-defined result. 
    - Their requirements to the communication channel are simple: to achieve convergence, you need messages to be delivered every once in a while. Because of their properties, it also doesn’t matter if messages get duplicated.
    - a big disadvantage: You need to send the entire value over the wire. This could become prohibitively expensive once the data structures grow larger.
  - operation-based CRDTs, or CmRDTs
    - While their design goals are the same as state-based CRDTs (convergence), they achieve this in a completely different way. 
    - They work by transmitting only the operations that have been applied since the last sync.
    - State-based CRDTs achieve convergence by the lattice properties. 
    - But in operation-based CRDTs, replicas never actually see each other’s entire state. Instead, we must make sure that operations commute. This means that no matter in what order the operations from one replica are applied to another replica, they end up reconstructing the same state.
    - The convergence theorem for them requires reliable broadcast channels.
    - Specifying operation-based objects can be more complex since it requires reasoning about history, but conversely, they have greater expressive power. The payload can be simpler since some state is effectively offloaded to the channel. Op-based replication is more demanding of the channel, since it requires reliable broadcast, which in general requires tracking group membership.
  - There’s no clear winner here
    - You need to decide which one to use based on your concrete use case and channel assumptions. 
    - But one more thing: A Git-like approach where before syncing, both replicas negotiate the precise subset of objects that they need to exchange, may give you the benefits of small message sizes while keeping the conceptual simplicity of state-based CRDTs, at the cost of introducing a more complex protocol.

- https://github.com/pfrazee/crdt_notes
- Operation Based vs. State Based replication
  - There are two fundamental methods to propagate updates among replicas. 
  - In State based replication, updates contain the full object state (or in optimized versions, a delta of the state). 
  - In operation based, the updates contain the operations that modify the object and must be executed in all replicas. 
  - The size of an object is typically larger than the size of an operation. Transmitting the whole state of an object can introduce a large overhead in message size. 
  - On the other hand, if the number of operations is high it can be better to transmit the whole state instead of all operations. 
  - Also, it can be simpler to update the state of an object than applying the operations on it, as discussed in 2.1.5.

- [Data Laced with History: Causal Trees & Operational CRDTs](http://archagon.net/blog/2018/03/24/data-laced-with-history/)
- CmRDTs, or operation-based CRDTs, only require peers to exchange mutation events, but place some constraints on the transport layer. 
  - (For instance, exactly-once and/or causal delivery, depending on the CmRDT in question.) 
- With CvRDTs, or state-based CRDTs, peers must exchange their full data structures and then merge them locally, placing no constraints on the transport layer but taking up far more bandwidth and possibly CPU time. 
- Both types of CRDT are equivalent and can be converted to either form.

- https://github.com/mpareja/node-uncorded
  - A state-based CRDT was chosen over an operation-based CRDT so we could forgo(放弃) the requirement of a reliable network ensuring idempotent message delivery. 
  - The downside of a state-based CRDT is that we always replicate a node's entire state. 
  - Uncorded's small and short-lived state is a great fit here so long as we don't hold remove-set values indefinitely.
  - Nodes publish changes to listeners via newline delimited JSON representations of their state. Listeners apply the state changes according to the 2P-set merge algorithm.
# yjs vs automerge

## [yjs Compared to Automerge](https://github.com/yjs/yjs/issues/145)

- You are welcome to ask about the differences. 
- I don't have much experience with automerge. 
  - If I understand correctly, automerge was primarily build for sharing application state. 
  - They decided to make application state immutable, and therefore it nicely integrates into react applications.
- Yjs was primarily build for shared editing on text and rich-text. 
  - Yjs exposes state as mutable data types. 
  - State is mutable by design, because some computations can be done more efficiently on mutable objects.
- I would argue that Yjs is the better choice if you plan to share huge (text / rich-text) documents, 
  - because 1. its algorithm is specifically designed for shared editing and 
  - 2. it encodes its structure very efficiently in a binary format. 
  - Automerge on the other hand might be easier to handle because state changes are just operations on the shared document.
- If you are not working on a shared editing application and you are not hitting any performance problems, then you are probably fine with automerge. 
  - Otherwise you should definitely consider Yjs.
- I created a set of benchmarks to compare Yjs with Automerge
  - https://github.com/dmonad/crdt-benchmarks
# ref
- [KeyValueCRDT](https://bdewey.com/til/2021/08/21/)
  - https://github.com/bdewey/KeyValueCRDT /swift
  - My goal with KeyValueCRDT is to provide a CRDT implementation that can work as a file format for a wide range of applications.
  - KeyValueCRDT uses SQLite for its storage

- [Peritext: A CRDT for Rich-Text Collaboration](https://www.inkandswitch.com/peritext/)
  - supports overlapping inline formatting, and shown how to implement it efficiently.
  - it simply allows two versions of a rich-text document to be merged automatically.
