---
title: lib-collab-yjs-blog-stars
tags: [blog, collaboration, yjs]
created: 2022-10-22T18:45:04.054Z
modified: 2022-10-22T18:45:23.619Z
---

# lib-collab-yjs-blog-stars

# guide

# blogs

## [Yjs Fundamentals - Part 1: Theory | by Dovetail Engineering | Dovetail Engineering | Medium _202210](https://medium.com/dovetail-engineering/yjs-fundamentals-part-1-theory-232a450dad7b)

- 
- 
- 

### [Yjs Fundamentals — Part 2: Sync & Awareness _202212](https://medium.com/dovetail-engineering/yjs-fundamentals-part-2-sync-awareness-73b8fabc2233)

- 
- 
- 
- 

## [深度解析 Yjs 协同编辑原理【看这篇就够了】 - 掘金 _202312](https://juejin.cn/post/7316592817341399090)

- 将doc.gc=false设置为禁用垃圾收集并能够恢复旧内容
- 共享文档上的每一个更改都发生在一个事务中, 在每个事务之后都会调用Observer调用和update事件。您应该将更改捆绑到单个事务中，以减少事件调用。

- 在共享类型的作用域上创建新的Y. UndoManager。
  - 如果任何指定的类型或其任何子类型被修改，UndoManager会在其堆栈上添加一个反向操作。也可以指定trackedOrigins来筛选特定的更改。
  - 默认情况下，将跟踪所有本地更改, UndoManager合并在特定captureTimeout（默认为500ms）内创建的编辑, 将其设置为0可单独捕获每个更改。
- 调用stopCapturing（）以确保UndoManager上的下一个操作不会与上一个操作合并

## [CRDT与协同编辑 简介](https://www.herui.club/archives/1066)

- OT与CRDT
  1. OT (Operational Transformation) 操作转换
  2. CRDT (Conflict-free Replicated Data Type) 无冲突复制数据类型
- YATA算法思想
- 数据结构
  - YATA从一开始就为在文档中创建的每个字符构造一个特殊的数据结构Item，Item之间以双向链表的形式连接在一起；
  - Item之间可以根据ID来比较逻辑先后关系。由此，我们获得了数学上严格的偏序结构。
- 冲突处理
  - Item之间是通过ID排序的，因此这个序列如果满足以下三条规则，在数学上可以证明是严格全序的：
    - 规则一：禁止互相冲突的操作之间有交叉连接的原点。
    - 规则二：当指定`O1<O2`时，不会存在另外一个操作比O2大同时比O1小。
    - 规则三：当两个冲突的插入操作具有相同Origin时，用户ID小的操作在左侧。此规则参照了OT算法。
- 历史回溯
  - CRDT中使用了链表的数据结构，而不是根据坐标定位，所以可以理解为完全没有「脏路径」问题
  - 基于 CRDT 的方案中，实现 undos/redos 应该就比较简单了，只需要根据 CRDT 的数据结构的新增或者删除去实现 undos/redos 栈就可以有效解决问题。 假如进行了一个生成结构对象的操作，那么撤回的时候就把它标记删除即可。
- 网络同步
  - 设计了配套的网络协议y-protocols。核心是分发序列化的Item，因为Item携带了前驱后继等引用信息，所以不能简单地直接序列化为JSON格式
  - y-protocols使用了Uint8Array 形式的 update 数据编解码。YATA支持每个客户端离线编辑，并把操作记录在本地，客户端联网后，YATA会检查本地数据和共享数据的不同并完成数据同步。
  - 在同步文档状态时，Yjs 划分了两个阶段：
    - 阶段一：某个客户端可以发送自己本地的 state vector，向远程客户端获取缺失的文档 update 数据。
    - 阶段二：远程客户端可以使用各自的本地 clock 计算出该客户端所需的 item 对象，并进一步编码生成包含了所有未同步状态的最小 update 数据。

## [再遇协同编辑：Yjs + Quill，文档协同编辑竟如此简单 _202402](https://juejin.cn/post/7339341982836097075)

- Yjs 中 Documents/Shared Types 的所有更改都发生在事务中，每次发生事务后都会触发 observer 调用和 update 事件，触发监听和更新操作。

- 在不使用 y-quill 的情况下，使用 Yjs 自带的 API 实现了 Quill 的协同编辑。  
  - 首先监听 Quill 文本的变化； 接着将 Quill 的 Delta 数据结构转换为 yText 结构；
  - yText 改变时通过 y-websocket 发送到其他客户端；
  - 其他客户端监听 yText 的变化，解析出 Quill 的 Delta 数据，回填到编辑器中。

- Yjs 已经提供了常用的编辑器的数据绑定，像Prosemirror、Tiptap、Monaco、Quill 等等，我们可以看下y-quill和y-monaco的源码，Yjs 应用到不同的编辑器，基本都是这一套逻辑：
  - 首先监听编辑器的数据变化，当发生变化时，将编辑器数据转为 Yjs 的 Shared Types 数据结构，当本地 Yjs 数据发生变化时会通过 Network Provider 将数据结构同步给所有协同者，其他协同者再通过监听 Yjs 数据的变动，将 Yjs 数据转为编辑器数据，利用自身的 API 将变化填充到编辑器中，从而实现协同编辑。

- 每一个客户端都维护了一个 Yjs 数据结构的副本

## [基于CRDT的一种文档冲突算法 - 一行舟 _202202](https://juejin.cn/post/7064236095440961550)

- 本文我们主要介绍基于CRDT的一种文档合并算法-YATA, 开源实现Yjs
  - 全文偏理论

## [实时协作-yjs基本理解 | 一席之地 _201704](https://www.ximing.ren/post/2017/%E5%AE%9E%E6%97%B6%E5%8D%8F%E4%BD%9C-yjs%E5%9F%BA%E6%9C%AC%E7%90%86%E8%A7%A31-%E6%A6%82%E8%A7%88/)

- 
- 

### [实时协作-yjs基本理解2-向量时钟 | 一席之地](https://www.ximing.ren/post/2017/%E5%AE%9E%E6%97%B6%E5%8D%8F%E4%BD%9C-yjs%E5%9F%BA%E6%9C%AC%E7%90%86%E8%A7%A32-%E5%90%91%E9%87%8F%E6%97%B6%E9%92%9F/)

### [实时协作-yjs基本理解3-操作日志 | 一席之地](https://www.ximing.ren/post/2017/%E5%AE%9E%E6%97%B6%E5%8D%8F%E4%BD%9C-yjs%E5%9F%BA%E6%9C%AC%E7%90%86%E8%A7%A33-%E6%93%8D%E4%BD%9C%E6%97%A5%E5%BF%97/)

### [实时协作-yjs基本理解4-Ytext | 一席之地](https://www.ximing.ren/post/2017/%E5%AE%9E%E6%97%B6%E5%8D%8F%E4%BD%9C-yjs%E5%9F%BA%E6%9C%AC%E7%90%86%E8%A7%A34-Ytext/)

## [Yjs——一个基于CRDT的数据协同框架_腾讯alloy_202104](https://mp.weixin.qq.com/s?src=11×tamp=1686787686&ver=4591&signature=0vaM7PBUtg8XVbWmk8vJypnfhEzMZKA*n2ZLsyNLrvul6UKW2aw8*1teZ1rzopI6YHA*2wP1t9PSaUaQhpkV0XhyA6jRigandep79YE59mpO5*e*tJGuHIoORlbpDViE&new=1)

# blogs-comparison 🆚️

## [A comparison of JavaScript CRDTs - Alexis Métaireau _202403](https://blog.notmyidea.org/a-comparison-of-javascript-crdts.html)

- Conflict-free Resolution Data Types are a family of data types able to merge their states with other states without generating conflicts. 
- “Append-only sets” are probably one of the most common type of CRDT: you can add the same element again and again, it will only be present once in the set. It’s our old friend Set, as we can find in many programming languages.

- I found Y.js and Automerge quite similar for my use case, while JSON Joy was taking a different (less “all-included”) approach. 

- In order to observe the changes, we need to inspect the given patches and work on what we find.
- One thing to keep in mind is that these “patch” events happen only once per patch received. You can see it as a “diff” of the state between the current and the incoming states.
  - Y.js exposes a utility which is able to tell you what the action on the key is (“delete”, “update” and “add”)
  - Automerge and JSON Joy, on the other hand, don’t provide such utility functions, meaning you would need to find that out yourself.

- Conclusion
  - None of them implement the high-level API I was expecting, where the clients talk with each other and the server just relays messages, but maybe it’s because it’s better in general to have the server have the representation of the data, saving a roundtrip for the clients.

## [实时协作-yjs和ShareDB对比 | 一席之地 _201704](https://www.ximing.ren/post/2017/%E5%AE%9E%E6%97%B6%E5%8D%8F%E4%BD%9C-yjs%E5%92%8CShareDB%E5%AF%B9%E6%AF%94/)

- Yjs (基于 CRDT 算法) 的优点：
  - 离线支持和冲突解决： CRDT 算法在设计上就考虑到了离线工作和冲突解决，使得 Yjs 能够在无需中心化服务器参与的情况下解决冲突。用户可以在离线状态下进行编辑，然后在重新连接时将其更改与其他副本合并，而不会导致任何冲突。
  - 分布式和去中心化： CRDT 不需要中心服务器来解决冲突，这使得 Yjs 在设计上更加分布式和去中心化，可以在不同的网络环境中使用，包括 peer-to-peer 网络。
高性能和可伸缩性： Yjs 的实现对于大量用户协作编辑大型文档具有很好的性能和可伸缩性。

- Yjs (基于 CRDT 算法) 的不足：
  - 数据负载： 由于 CRDT 保持所有操作的历史记录以解决冲突，因此文档的大小可能会随着时间和操作的数量而增长，这可能会对网络传输和存储产生影响。
  - 复杂性： CRDT 的理论和实现比 OT 更复杂，这可能会增加学习和实施的难度。

- ShareDB (基于 OT 算法) 的优点：
  - 实时同步： ShareDB 通过使用 WebSocket 提供实时的数据同步，这使得它在低延迟的网络环境中表现良好。
  - 灵活性： ShareDB 支持任何 JSON 可序列化的数据类型，使其适用于更多种类的应用。

- ShareDB (基于 OT 算法) 的不足：
  - 需要中心服务器： OT 需要一个中心服务器来处理和转换操作，以解决冲突。这使得 ShareDB 更依赖于中心服务器和网络连接。
  - 离线支持和冲突解决： 尽管 ShareDB 提供了离线支持，但是在没有服务器参与的情况下解决冲突往往会更复杂，而且实践下来存在乱序&丢内容的情况。
  - 性能和可伸缩性： 与 CRDT 相比，OT 的性能和可伸缩性可能会受到更多的限制，特别是在大量用户协作编辑大型文档的情况下。
# more
