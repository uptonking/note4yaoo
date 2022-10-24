---
title: lib-collab-crdt
tags: [collaboration, crdt, pattern]
created: 2021-07-23T15:50:09.211Z
modified: 2022-04-05T10:10:08.537Z
---

# lib-collab-crdt

# guide

- crdt的实现思路
  - 基于state
    - yjs
  - 基于operation
    - cabinet

- [An introduction to state-based CRDTs_201712](https://bartoszsypytkowski.com/the-state-of-a-state-based-crdts/)

- [Operation-based CRDTs: JSON document_202103](https://bartoszsypytkowski.com/operation-based-crdts-json-document/)
# [CRDTs for Mortals_James Long_201912](https://www.youtube.com/watch?v=DEcwa68f-jY)
- Why haven’t “offline-first” apps taken off?
  - syncing is hard
-  local apps are a distributed system
- why local-first
  - offlineable
  - fast
  - privacy
  - ad-hoc queries

- hard parts 1: unreliable ordering
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
 
- hard parts 2: conflicts
- 根据时间戳保证交换律(乱序)、幂等
- 基础数据结构：lww-map(处理changes) + g-set(处理数据状态)
  - 使用grow-only set因为可能后面会有相关操作
- How to take basic relational data and turn it into CRDTs?
  - SQLite table  =>  G-Set of LWW-Maps
  - msg-table, 若id不存在，就插入新row
- 读取查询很快
- 更新数据时，update-self，push changes to others
- 删除时，添加tombstone字段，并未物理删除

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

- A sequence, list, or ordered set CRDT can be used to build a Collaborative real-time editor, as an alternative to Operational transformation (OT).
  - Some known Sequence CRDTs are Treedoc, RGA, Woot, Logoot, and LSEQ
- Industrial sequence CRDTs are known to out-perform academic implementations due to optimizations and a more realistic testing methodology.
  - The main popular example is Yjs CRDT, a pioneer in using a plain list instead of a tree (ala Kleppmann's automerge).
  - Deletions in Yjs are treated very differently from insertions. 
  - 👉🏻 Insertions are implemented as a sequential operation based CRDT, but deletions are treated as a simpler state based CRDT.

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
- Last write wins set(LWW-element Set)
  - 类似2P-Set，有一个addSet，一个removeSet，不过对于元素增加了timestamp信息，且timestamp较高的add及remove优先
- Observed-remove set(OR-Set)
  - 类似2P-Set，有一个addSet，一个removeSet，不过对于元素增加了tag信息，对于同一个tag的操作add优先于remove

- https://github.com/gbogard/crdts-introduction
  - https://crdt.guillaumebogard.dev/
  - A gentle introduction to Conflict-free replicated data types, including visual demos
  - A state-based CRDT is a data structure, together with a binary operation that can produce a single state out of two possibly different states. More formally, a state-based CRDT is a tuple (S, s0, q, u, m)
  - operation-based CRDT is a data-structure whose updates are encoded by operations, and operations are sent over the network. 
    - A new state can be produced given the current state and an operation. 
    - When the structure is modified, the replica responsible for the update generates one or many operations, applies them locally, and then propagates them across the network. 
    - Operation-based CRDTs guarantee that, when operations are successfully propagated, all replicas converge to the same state.
    - Like merging state-based CRDTs, applying operations is associative and commutative, i.e. operations can be applied in any order, however, unlike it isn't necessarily idempotent. It is the responsibility of the transport layer to make sure operations are properly delivered, and not applied more than once.

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
  - A state-based CRDT was chosen over an operation-based CRDT so we could forego the requirement of a reliable network ensuring idempotent message delivery. 
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
