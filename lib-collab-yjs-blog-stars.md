---
title: lib-collab-yjs-blog-stars
tags: [blog, collaboration, yjs]
created: 2022-10-22T18:45:04.054Z
modified: 2022-10-22T18:45:23.619Z
---

# lib-collab-yjs-blog-stars

# guide

# [探秘前端 CRDT 实时协作库 Yjs 工程实现 - 知乎](https://zhuanlan.zhihu.com/p/452980520)
- 本文会从 Yjs 的工程实现出发，介绍一个典型的工业级 CRDT 库是如何实现以下能力的：
- 建模数据结构
- 解决并发冲突
- 回溯历史记录
- 同步网络状态

- Yjs 的算法先进，但在实际应用中确存在下面的问题：
  1. fast search marker 不支持在 YXmlText 中使用
  2. 不支持移动操作，移动后的合并位置不符合预期
  3. ContentFormat 不支持同类型样式的嵌套或交错（不能还原 ProseMirror Mark 的特性）
  4. ProseMirror 的 Step 和 Yjs 的 insert/delete API 不匹配，y-prosemirror 采用了一套 diff 算法，导致用户意图丢失。也许与 Quilljs 结合没有这样的问题。
# [Near Real-Time Peer-to-Peer Shared Editing on Extensible Data Types](https://www.researchgate.net/publication/310212186_Near_Real-Time_Peer-to-Peer_Shared_Editing_on_Extensible_Data_Types)

# [【译】Near Real-Time Peer-to-Peer Shared Editing on Extensible Data Types - 掘金](https://juejin.cn/post/7027487213525041166)
- 在此之前，我们证明了 发生冲突的插入操作 存在全序关系。
- 在本节中，我们将给出一个算法，当我们已经有一个有序的插入列表时，计算新的插入的位置。
- 该算法利用不存在的交叉的 origin 链接作为中断条件。因此，当连接之间会交叉时，停止计算。
# [YATA线性数据插入算法](https://juejin.cn/post/7030327499829542942)
- 一个插入操作 Item 包含了唯一的操作标识符 ID、插入操作的内容和插入的意图 originLeft 和 originRight。
  - 这里需要注意的是，YATA 中的插入意图只有 originLeft，Yjs 为了解决一种特殊情况，添加了 originRight，下文会讲述。
- 操作的唯一标识符 ID 是由 Client 和 Clock 组成的元组，其中 Client 是副本的唯一标识符，Clock 是一个副本产生操作的累加计数器，每产生一个操作，计数器加 1。
  - 在 Yjs 中，如果连续的插入操作的内容都是同类型的文本，为了降低空间复杂度，会将这些连续的文本操作合并成一个操作。
  - 👉🏻 考虑到以后有把这些操作拆分的需求，所以在 Yjs 中，Clock每次加的是**内容的长度**。
- 考虑一个纯文本文档，对于文档的编辑只包含插入和删除两种操作。
  - 在 YATA 中，删除采用了墓碑法，对于文档的操作只有插入文本一个操作。
  - 所以，文档可以看成是插入操作的集合。
  - 为了保证各个副本之间的收敛，需要插入操作的集合满足全序关序，即每两个插入操作都有一个前后关系。
  - YATA 插入算法正是在这样一个前提下，提出了三条规则，最后根据这三条规则，提出了线形数据的插入算法。
- Yjs 对于文档内容Doc.content的定义采用的是操作的链表结构，这里为了更方便的解释算法，在不考虑时间复杂度的情况下，采用了数组结构 Item[]

- 插入算法的核心在于插入操作的集合满足全序关序，每两个插入都有一个前后关系。
  - 现在要将副本 1 产生的 o1o_1o1​与副本 2 产生的 o2o_2o2​ 集合在一起，为了保证副本 1 和副本 2 有相同的前后顺序，就需要计算出 o1o_1o1​ 和 o2o_2o2​ 的前后关系。
# [YATA：一种针对文本编辑优化的 CRDT 算法](https://hyrious.me/p/yata.html)
- YATA 算法的核心是：如果我们把参考节点一起发出去，新节点和参考节点之间连线，那么所有的这种连线都不能交叉。

- 如果有两个新元素的参考元素是同一个，这意味着发生了冲突，此时 YATA 算法引入了一个新的属性：right，表示参考元素右侧的元素。当发生冲突时，我们先切换到比较右侧元素上来，当右侧元素也一样时，再通过 id 排序决定。
# [Delta-state CRDTs: indexed sequences with YATA](https://www.bartoszsypytkowski.com/yata/)
- This time we'll cover YATA (Yet Another Transformation Approach): a delta-state based variant, introduced and popularized by Yjs framework

- A core concept behind all indexed CRDTs is notion of unique identifier assigned to the inserted element

- A popular approach is to define that unique identifier as a composite of two values:

- Unique identifier of a given replica/peer. Since we cannot guarantee uniqueness of sequence numbers generated concurrently by different peers, we can use them together with peer's own ID to make it so.
- Sequence number used for comparison. 
- It varies depending on the algorithm:
  - LSeq uses a variable-length byte sequence which is a function id(left_neighbor, righ_neighbor) that's expected to produce a sequence which is lexically greater than id of an item at previous index, but lower than id of an item at the next index (lseq[n-1].id < lseq[n].id < lseq[n+1].id).
  - ❓ RGA maintains a single globally incremented counter (which can be ordinary integer value), that's updated anytime we detect that remote insert has an id with sequence number higher that local counter. Therefore every time, we produce a new insert operation, we give it a highest counter value known at the time.
  - YATA also uses a single integer value, however unlike in case of RGA we don't use a single counter shared with other replicas, but rather let each peer keep its own, which is incremented monotonically only by that peer. Since increments are monotonic, we can also use them to detect missing operations eg. updates marked as A:1 and A:3 imply, that there must be another (potentially missing) update A:2.

- YATA is similar to RGA in regard to keeping expected predecessor id as part of the operation. 
  - Additionally we also attach a successor id. In YATA naming convention, we call them left/right origins. 
  - Therefore insert operation can be defined as `ins(left, right, id, char)`. 
- Why do we need two origins instead of one like in case of RGA? 
  - YATA is delta-state CRDT with a fairly low number of restrictions regarding its replication protocol - at least when we compare it to a reliable causal broadcast requirements of their operation-based counterparts. 
  - In order to correctly place inserts send out of order, sometimes we may need two pointers instead of just one.

- In order to safely resolve any potential conflicts, that may have appeared in result of concurrent block insertion, we use left and right origins as a reference points. That mean, they must have been there first.

- there's a 1-1 relation between YATA block IDs and vector clocks. 
  - Given such vector clock, we can also easily generate the deltas themselves. 
  - All we need to do is to take blocks which sequence numbers are higher that sequence numbers of corresponding vector clock entries. 
  - After this we're almost done: we also need to remember that there might be blocks known to remote peer, that have been deleted in the meantime. 
  - For this reason we take IDs of tombstoned blocks and pass them over as well.
# [Deep dive into Yrs architecture](https://www.bartoszsypytkowski.com/yrs-architecture/)
- Document is the most top-level organization unit in Yjs. 
  - It basically represents an independent key-value store, where keys are names defined by programmers, and values are so called root types: a Conflict-free Replicated Data Types (CRDTs) that serve particular purposes. 
- In Yjs every operation happens in a scope of its document: all information is stored in documents, all causality (represented by the vector clocks) is tracked on per document basis. 
  - If you want to compute or apply a delta update to synchronize two peers, this also must happen on an entire document.

- Documents are using delta-state variant of CRDTs and offer a very simple 2-step protocol, which is similar to an optimization technique we discussed in the past
  - Document A sends its vector version (in Yrs it's called StateVector) to Document B.
  - Based on A's state vector, B can calculate missing delta which contains only the necessary data and then send it back to A.
- This way we make deltas efficient and very lightweight. 
  - Even more, Yrs encodes deltas using customized binary format, optimized specifically to make payloads small and efficient.

- Under the hood, document represents all user data together with an information used for tracking causality within a dedicated collection called the block store.

- A concept correlated to documents is one of a transaction
  - that name was inherited from Yjs and may be deceptive(误导的), as they don't have anything in common with ACID transactions known from standard databases. 
  - They are more like batches of updates reinforced with some optimization logic - like checking if updates that happen within a scope of transaction can be squashed(压碎、压扁或挤烂) into previously existing block store structure or triggering update events, programmers can subscribe to.

- All updates in Yrs are represented as blocks (a.k.a. structs in Yjs). 
  - Whenever you're inserting or removing a piece of data into your Y-data structure - be it a YText, YArray, YMap or XML types - you're producing a block. 
  - This block contains all metadata necessary to correctly resolve potential concurrency conflicts with blocks inserted concurrently by other users
- These blocks are organized in a block store on per client (peer) basis - all blocks produced by the same client are laid out next to each other in memory
- This layout is optimal to perform several operations like using state vectors and deltas, block squashing, efficient encoding format etc

- Yjs/Yrs use YATA algorithm as an universal conflict resolution strategy for all data types

- You may think, this is a lot of metadata to hold for every single character inserted by the user. That would be right, however Yjs implements an optimization technique that allows us to squash blocks inserted or deleted one after another, effectively reducing their count while keeping all guarantees in check.

- Block split
- We already discussed in detail how to implement a block-wise variant or RGA CRDT on this blog post, and it's YATA equivalent is not that much different. 
- The tl; dr explanation is: whenever we want to make a new insert in between elements grouped under the same block, we split that block in two parts and rewire their left and right neighbour pointers to a newly inserted block.
- All of this is possible because consecutive(连续不断的) block ID (client_id-clock pairs) are not assigned using clock numbers increased by one per block, but by one per a block element 

- Block squashing
- it's a reverse of splitting, executed upon transaction commit. 
- It's very useful in scenarios when the same peer inserts multiple elements one after another as a separate operations. 
- The most obvious case of this is simply writing sentences character by character in your text editor.
- Thanks to block squashing, we can represent separate consecutive blocks of data (eg. A:1=[a] followed by A:2=[b]) using a single block instead (A:1=[a, b]).
- The major advantage is reduction of memory footprint 
- Keep in mind that squashing has some limits to it: squashed blocks must be next to each other both in terms of A) being each others neighbours B) emitted by the same client and C) their IDs must follow one another with no "holes between"

- Yrs uses delta-state approach to CRDTs with an extremely small and robust replication protocol
- These types can be nested in each other according to their limitations
- Underneath all CRDT collections are represented by the same kind of block content known as a Branch. 
- Branch node is capable of storing two specific types of collections at once: both key-value entries and index-ordered double-linked list containing batches of items.

- Yrs Text and Array types make use of the same indexed sequence component and their in-memory representation is basically a double linked list of continuous elements (such as individual string characters or ranges of JSON values).
- Thanks to the use of YATA conflict resolution algorithm, these types are free from interleaving issues boggling other CRDT algorithms like LSeq. 
- And since we're using split-block approach, it lets our insert operations computational complexity to become independent of the number of elements inserted (in most cases). 

- a dynamic nested XML tree of nodes, which can contain attributes, text or other nodes. 
  - The way it works is actually pretty simple: a branch node uses its list head to point to a first XML child node block and map field to point to blocks used as attributes.

- v1 encoding relies heavily on variable integer encoding and block store layout to omit fields which can be inferred using blocks mutual relationships.
- v2 encoding was influenced by research made by Martin Kleppmann when he worked on automerge library, and adapted to Yjs. 
  - It extends the formatting to make use of run-length encoding, which can bring further savings, especially for deltas having many block updates.
# [Syncing text files between browser and disk using Yjs and the File System Access API_202205](https://motif.land/blog/syncing-text-files-using-yjs-and-the-file-system-access-api)
- Wrote this blog post on how to sync files between browser and disk using Yjs and the File System Access API. It works really well! 
- https://twitter.com/michaelfester/status/1523698983117684736

- https://news.ycombinator.com/item?id=31315717
