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
  - ？基于history

- [An introduction to state-based CRDTs_201712](https://bartoszsypytkowski.com/the-state-of-a-state-based-crdts/)

- [Pure operation-based CRDTs_202104](https://bartoszsypytkowski.com/pure-operation-based-crdts/)
- [Operation-based CRDTs: JSON document_202103](https://bartoszsypytkowski.com/operation-based-crdts-json-document/)
# [聊聊CRDT](https://cloud.tencent.com/developer/article/1422458)
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

- https://github.com/netopyr/wurmloch-crdt
  - Experimental implementations of conflict-free replicated data types (CRDTs) for the JVM
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
