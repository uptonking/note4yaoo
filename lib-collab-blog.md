---
title: lib-collab-blog
tags: [blog, collaboration]
created: 2021-10-14T11:16:52.887Z
modified: 2022-04-05T10:10:27.212Z
---

# lib-collab-blog

# guide

- [数据冲突解决方案 - 最终一致性实现](https://juejin.cn/post/6983237844579909668)
# [协同文档：OT与CRDT实现协同编辑笔记](https://www.zhoulujun.cn/html/webfront/engineer/Architecture/8564.html)
- 实时协同编辑，是指多人同时编辑一个文档，你可以实时看到别人做出的修改，不用手动刷新页面，最典型的例子是 Google Docs。
- 要实现实时编辑，我们需要解决两个技术点：实时通信问题、编辑冲突问题，其中实时通信问题比较好解决，可以使用 long pull 或 WebSocket

## OT与CRDT的区别

- OT主要用于文本，CRDT更通用
  - CRDT不仅仅应用在协同编辑，还有分布式系统的最终一致性上也有应用。

- OT操作必须通过服务器的转换才可以合并，
  - CRDT由于其数据结构特性，不通过服务器也可以合并。

- CRDT实现协同编辑的原理不同
  - OT通过改变操作来实现。操作是通过连线发送的，而并发操作在接收到它们后会进行转换。
  - CRDT通过改变状态来实现。对本地crdt进行操作。它的状态通过连线发送，并与副本的状态合并。合并的次数和顺序无关紧要—所有副本都会聚合。

- 因为OT中的 transformation 流程太复杂，OT概念不是很清楚，
  - 而CRDT很好理解，实现起来也不难。

## OT

- 实时协同编辑，通俗来讲，是指多人同时在线编辑一个文档，且当一个参与者编辑文档的某处时，这个修改会立即同步到其他参与者的计算机上。归纳起来，需要下面几个步骤：
  - 计算出当前参与者对文档做出的修改，并发送到服务器
  - **在服务器端，对所有参与者的修改进行合并以及冲突处理**
  - 将合并之后的结果返回到所有参与者的计算机上
  - 将光标移动到正确的位置
- 由于没有锁的机制，当多个参与者在编辑同一处内容时，便可能出现冲突，这个时候就需要通过一定的算法来自动地解决这些冲突。
  - 最后，当所有改变都同步后，每个参与者计算机上所看到的文档内容应该是完全一致的。

- How does Operational Transformation work?
  - Every change to a shared document is represented as an operation. 
  - In a text editor, this operation could be the insertion of the character ‘A’ at position 12. 
  - An operation can be applied to the current document resulting in a new document state.
  - To handle concurrent operations, there is a function (usually called transform) that takes two operations that have been applied to the same document state (but on different clients) 
    - and computes a new operation that can be applied after the second operation and that preserves the first operation’s intended change. 
  - This function can be used to build a client-server protocol that handles collaboration between any number of clients. 

- 一个文档可以被抽象为一系列操作的集合，这个集合便是 changeset。
  - changeset 是对文档一系列操作的集合
  - 这些操作必须是指定的一些操作其中的一种或多种
  - changeset 只有它基于某个特定的版本的文档时才是有意义的
  - 一个文档可以表示为一系列的 changeset 依次应用于 空文档 之后得到的
  - 义运算 $AB$，意为将 changeset $B$ 应用到 $A$ 上
  - 定义 $C = AB$，意为 changeset $C$  产生的效果等等价于依次应用 $A$, $B$ 产生的效果
  - changeset 一般表示为 $C_v$， 意为一个基于版本号 $v$ 的 changeset
- changeset 中 action 的顺序必须保留，因为 index 的位置可能会被改变。
  - 一般每 500ms 收集一次 action （变更动作），并生成一个 changeset

## CRDT

- CRDT有两种形式：
- 基于状态
  - 即将各个节点之间的CRDT数据直接进行合并，所有节点都能最终合并到同一个状态，数据合并的顺序不会影响到最终的结果。
- 基于操作
  - 将每一次对数据的操作通知给其他节点。只要节点知道了对数据的所有操作（收到操作的顺序可以是任意的），就能合并到同一个状态。

- CRDT必须符合可交换性，结合性，还有幂等性，所以 CRDT 数据类型合并最终会收敛到相同状态。
- 为什么要符合可交换性，结合性，还有幂等性三个特性呢？因为可以解决分布式达到最终一致会遇到的问题：
  - 网络问题导致发送接收顺序不一致（幂等性）
  - 以及多次发送（可交换性）

- 在因果关系的事件需要知道事件的先后顺序，并且能够按照正确的顺序处理这些事件，所以需要 Lamport timeStamp 来确定事件发生的顺序，Lamport timeStamp 只需要保证两个规则就好了。
  - newTimeStamp[local] = Max(timeStamp[local], timeStamp[receive])
  - newTimeStamp[local] = timeStamp[local] + 1

- 每个客户端都有一个唯一UUID，再加上 Lamport timeStamp 就可以为每个操作添加唯一可排序的 ID。
- 每个操作都有唯一的ID，接下来就是定义操作的数据结构，并且符合 CRDT 的特性，ID的唯一性可以保证操作的幂等性，操作可以排序保证了交换性，接下来只要保证每个操作都可以被合并就可以了。
# experiments

## [Braid: Synchronization for HTTP](https://braid.org/)

- https://github.com/toomim
  - https://github.com/braid-org/braidjs
  - https://invisible.college/@toomim

- The Braid Protocol is an extension to HTTP that generalizes it from a state transfer to a state synchronization protocol.
- Braid adds these features to HTTP:
  - Versioning to HTTP resources
  - Subscriptions to GET requests
  - Patches to Range Requests
  - Merge-Types to specify OT or CRDT behavior
# ref
- [How Figma’s multiplayer technology works__201910](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/)
