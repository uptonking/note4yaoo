---
title: lib-collab-blog
tags: [blog, collaboration]
created: 2021-10-14T11:16:52.887Z
modified: 2022-04-05T10:10:27.212Z
---

# lib-collab-blog

# guide

- [数据冲突解决方案 - 最终一致性实现](https://juejin.cn/post/6983237844579909668)
# [Top 5 Ways to Implement Real-Time Rich Text Editor (ranked by complexity)_202101](https://exaspark.medium.com/top-5-ways-to-implement-real-time-rich-text-editor-ranked-by-complexity-3bc26e3c777f)

> Real-time experience becomes the new norm in building modern online tools.

- building a rich doc editor that allows typing with other users in real-time, keeping docs’ history, forking docs, submitting changes, etc. 
- I try to classify real-time problems into the following two categories:
- Real-time without conflicts (easy)
  - can be solved by using some generic BaaS tools such as Pusher, Firebase, PubNub or open-source tools such as Phoenix Channels, Rails ActionCable, Node.js Socket.io that allow pushing updates to clients on certain changes.
- Real-time with conflicts (hard)
  - harder to implement since multiple users can change the same data object, which may lead to race-conditions, conflicts, and data inconsistency.

## Global Lock

- For example, if Alice changed “Foo” to “FooBar”, she first acquires a lock. Bob after that won’t be able to edit the doc.
  - It’s also possible to make the lock more granular. For example, implement a lock per element instead of the global doc lock.

- pros
- The easiest to implement compared to other approaches. 但不太符合实时协作

- cons
- Doesn’t actually enable real-time text editing, it prevents it
- Hard to deal with properly acquiring and releasing locks.
- May cause deadlocks similarly to a Mutex, for example.

## Last Write Wins

- If multiple users change the same doc at the same, the last user who made changes (e.g., the last changes received by the server) overrides all other users’ changes.
  - One strategy to reduce the number of conflicts could be to split the doc into many smaller fragments. 
  - Then use the “last write wins” approach only on each fragment instead of the whole doc.
- Notion implements the “last write wins” approach that works fine enough in most cases.

- pros
- The easiest to implement approach that enables real-time.

- cons
- Overrides the user’s changes if multiple users edit the same element.
- Bad UX, as it may look that somebody deleted the user’s recent changes.
- Hard to maintain users’ local text cursor/selection positions.

## Diff and Merge

- The idea with this approach is to find the difference between the users’ changes and then try to merge them to avoid any data loss.
- The initial Google Docs version used the “diff and merge” approach until it was rewritten by using operational transformation (OT).
- One disadvantage is that it’s sometimes impossible to properly merge conflicting changes. 
  - For example, Alice added a character “i” to have “Foio” and Bob made the whole word bold “Foo”. Here it’s hard to tell exactly what’s going to happen, whether we should make the added character bold “Foio” or keep it not bold “Foio” or merge everything “FoioFoo”.
  - That’s why Git, for example, delegates resolving some conflicts to developers, as there is not enough context for it to know what the expected outcome is.

- pros
- Great for merging changes made offline or asynchronously (like Git).

- cons
- It’s not always possible to diff and merge changes correctly. Requires users’ input that might be frustrating if that happens very often.
- Hard to maintain users’ local text cursor/selection positions.

## Conflict-free Replicated Data Type (CRDT)

- CRDT is used for building various types of distributed systems.
  - For example, databases such as Redis Enterprise or Riak, cross node syncing in Elixir Phoenix, building privacy-centric alternatives to Zoom or YouTube with GUN.
- Apple Notes app uses CRDT for syncing offline edits between devices.

- The basic idea behind CRDT is to use some data types that make resolving conflicts extremely simple. 
- To achieve this, operations on these data types should satisfy the following mathematical properties:
  - Commutativeness, changing the order shouldn’t change the result. I.e. the order doesn’t matter.
  - Idempotence, applying the same change multiple times produces the same result as it was applied only once.
- When building a text editor, it is possible to split the content into separate characters and make sure that each of them has a unique ID. With these IDs, we can now correctly identify characters’ positions in the text.
- when both Alice and Bob deleted “o”, it works the same way as only one of them did that (idempotence).

- pros
- Great for peer-to-peer communication in distributed systems, doesn’t require a central server.
- Relatively simple to reason about and easy to implement.
- Text cursor/selection positions are simpler to implement by using unique IDs. But it has to be implemented on a separate layer.
- There are a few useful open-source tools such as Yjs, Automerge, GUN.
- Can work offline.

- cons
- Requires using specific data structures. 
  - If you already have a rich text editor with docs in the DB, it may mean a complete rewrite.
- Doesn’t play well if you want to have your server to be a single source of truth. 
  - Usually, your server becomes just one of the P2P nodes and may not have the latest data.
- Since it’s a relatively new approach, it’s not used very often for building real-time text editors, especially rich text editors beyond plain text. 
  - You’d need to read some research papers. For example, CRDT with JSON, CRDT with extensible data types, etc.
- CRDT simplifies conflict resolution, but it sacrifices intention-preservation. 
  - For example, Alice wanted to replace “F” in “Foo” with “W” to have “Woo”. 
  - Bob wanted to replace “Foo” with “Bar”. CRDT will split these replace operations into simple `delete + add`. 
  - Alice and Bob wanted to change “Foo” to have another word, but they’ll end up with something like “WBar” instead.

## Pseudo Operational Transformation (OT)

- There is no single conventional way to implement both CRDT and OT.

- Figma, for example, implements real-time design collaboration by using Pseudo CRDT. 
- In the same way, ProseMirror, a very popular framework for building rich text editors, implements Pseudo OT (I call it that way).
  - The New York Times uses ProseMirror with Pseudo OT for collaborative editing.

- Alice makes an operation (step in ProseMirror) that says Insert “A” at position #2. Sends a request with V1 to the central server. Bumps her version of the doc to V2.
- Bob makes another operation that says Insert “B” at position #3. Sends a request with V1 to the central server. Bumps his version of the doc to V2.
- The server receives Alice’s operation with V1 first and persists it. then broadcast Alice's op.
- 👀 The server receives Bob’s operation with V1. Since the server already saw an operation with V1, it ignores it, assuming that Bob will resend this operation again.
- Alice receives her operation as an acknowledgment.
- Bob receives and applies Alice’s operation. 
  - Then Bob performs OT (`rebasing` in ProseMirror) on his operation Insert “B” at position #3 that becomes Insert “B” at position #4 
  - After that, he tries to resend his operation again, now with V2. Bumps his version of the doc to V3.
- The server receives Bob’s operation Insert “B” at position #4
- Bob receives his recent operation as an acknowledgment.
- Alice receives Bob’s operation and applies it. After that, she bumps her version of their docs to V3.  

- pros
- If you already use a text editor like ProseMirror, this approach feels very natural, 
  - and it comes with tools that already work with the existing data structures (steps) and implement OT (rebasing).
- It works great in the client/server architecture with a central DB. 
  - Clients can continue changing the doc with an optimistic UI and a local buffer with unconfirmed operations.
- 👉🏻 The server doesn’t have to know anything about OT. 
  - It just stores operations (event sourcing), broadcasts or rejects some of them if there is a conflicting version.
- Unlike CRDT, it preserves users’ intentions. 
  - E.g. “replace a character” instead of “delete + add a character” or “make a character bold” instead of “delete and add a bold character”.
- It automatically keeps track of text cursor/selection positions.
 
- cons
- It’s not conventional OT. 协同编辑的实现和prosemirror耦合了
  - It increases coupling to ProseMirror and its internal implementation (along with its limitations).
- Since OT happens only on the client-side, it may cause a network messages overhead when trying to transform and resubmit changes from the clients. 
  - The more clients are editing the same doc, the more conflicting changes and more messages are being sent back and forth. 
  - This may lead to broadcasting delays.
- Rebasing changes (aka local changes transformation only, not remote) may sometimes fail and lead to dropping some changes. 
  - For example, Alice deleted the word “Foo”. When Bob tries to append “Bar” to “Foo”, his operation may fail as it’s not rebasable against Alice’s deletion. I.e. “Bob” may lose his “Bar” change.
- This approach is not suitable for long offline sessions.

## Operational Transformation (OT)

- This is a conventional approach used by most popular real-time text editors such as Google Docs, Dropbox Paper, Etherpad and many others.
- It took 2 years to write Google Wave’s whitepaper that later allowed Google to build Google Docs with the client/server communication architecture.
- It’s similar to the Pseudo OT approach. 
- The major difference though is that the server can also apply transformations, so there is no need to force clients to resolve conflicts by applying transformations and resubmitting the changes.

- Alice makes an operation that says Insert “A” at position #2. Sends a request with V1 to the central server. Bumps her version of the doc to V2.
- Bob makes another operation that says Insert “B” at position #3. Sends a request with V1 to the central server. Bumps his version of the doc to V2.
- The server receives Alice’s operation with V1 first and persists it. then broadcast Alice's op.
- 👀 The server receives Bob’s operation with V1. Since the server already saw an operation with V1, it transforms Bob’s operation to Insert “B” at position #4 and save it. After that, it’ll broadcast this operation to all other clients.
- Alice receives her operation as an acknowledgment.
- Bob receives and applies Alice’s operation that inserts 1 character. Then Bob locally also performs OT to Insert “B” at position #4. Bumps his version of the doc to V3.
- Alice receives Bob’s operation and applies it. After that, she bumps her version of their docs to V3.
- Bob receives his operation acknowledgment.

- 👉🏻 It means that clients send their changes only once and wait for acknowledgment from the server. 
  - The server performs transformations when there are conflicts and always accepts any new operations.
- It’s all possible only with transformations that can be applied by both the client and the server to get to the same convergent state, no matter when they received the other operations. These states are called state spaces because they contain different paths of operational transformation.

- pros
- The battle-tested and historically one of the most popular approaches for building real-time rich text editors.
- It works great in the client/server architecture with a central DB. 
  - The server uses only a single state space as the source of truth. 
  - Clients wait for acknowledgment to make sure that they stay on the same server’s OT path.
- Unlike the Pseudo OT, there are no extra back-and-forth messages sent between the clients and the server.
- Unlike CRDT, OT can ensure that the effect of executing an operation on any document state is the same as the intention of the operation (intention preservation).
- There are a few helpful open-source tools such as quill-delta, ottypes, sharedb, etc.
- It allows keeping track of text cursor/selection positions.
- Can work offline.

- cons
- The server should also know how to perform operational transformation. 服务端和客户端的transform算法要一致
- Depending on your editor, it might require adding an extra layer on top. 
  - For example, to map data structures from ProseMirror to OT.
- Relatively hard to implement. 
  - Doesn’t provide 100% correctness. 
  - Similarly to CRDT, requires deep understanding of the theory behind it.

## Conclusion

- To build a real-time rich text editor, it’s also necessary to solve a lot of extra problems and find answers to questions about real-time communication and infrastructure, implementing shared or local undo/redo, keeping track of local or remote text cursors/selections, versioning, etc.

- As a general rule of thumb:
  - If you need to build a basic real-time text editor, you might be fine with implementing a “lock” or the “last write wins” strategy.
  - For large text changes made asynchronously or offline, the best solution could be to implement the “diff and merge” strategy.
  - If you build a text editor that is meant to be used P2P, then you probably want to choose CRDT.
  - If you use ProseMirror, then you might consider using its prosemirror-collab plugin.
  - If you know that real-time rich text editing will be your primary feature, then you’d probably want to double down and use OT.
# [协同文档：OT与CRDT实现协同编辑笔记，偏理论](https://www.zhoulujun.cn/html/webfront/engineer/Architecture/8564.html)
- 实时协同编辑，是指多人同时编辑一个文档，你可以实时看到别人做出的修改，不用手动刷新页面，最典型的例子是 Google Docs。
- 要实现实时编辑，我们需要解决两个技术点：实时通信问题、编辑冲突问题，其中实时通信问题比较好解决，可以使用 long pull 或 WebSocket
- 一个文档可以被抽象为一系列操作的集合，这个集合便是 changeset。
  - changeset 是对文档一系列操作的集合
  - 一个文档可以表示为一系列的 changeset 依次应用于 空文档 之后得到的
  - 定义运算 $AB$，意为将 changeset $B$ 应用到 $A$ 上
  - 定义 $C = AB$，意为 changeset $C$  产生的效果等等价于依次应用 $A$, $B$ 产生的效果

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
