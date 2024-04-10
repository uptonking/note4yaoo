---
title: lib-collab-yjs-blog-internals
tags: [blog, codebase, internals, yjs]
created: 2024-04-10T01:50:25.875Z
modified: 2024-04-10T01:50:45.337Z
---

# lib-collab-yjs-blog-internals

# guide

# blogs

## [Yjs代码简析 - SegmentFault 思否 _202306](https://segmentfault.com/a/1190000043871178)

- 在Yjs实现里面每个字符都是有一个唯一的id（clientId, clock），而里面的clock就是Lamport Clock。
  - 因为在分布式里面，所有的节点的时钟是很难保持精确统一的，想通过赋予一个时间戳给事件，然后对比事件的时间戳还原出各个节点的事件顺序几乎无法实现，所以Lamport Timestamp就被提出来，它通过节点之间交换信息，并使用logic clock而不是true lock来解决事件顺序问题。
- Lamport Clock存在一定的局限性，并不能完全从clock的大小就能推出所有事件间的顺序，只能获得部分有序的事件序列。
- Vector Clock是在Lamport Clock基础上扩展而来。Vector Clock要求每个一个节点都有自己独立的clock，当有本地事件发生时候只更新自己节点的clock+1；而在广播消息时要把节点整个Vector Clock传出去，当接收到消息时需要遍历接收的Vector Clock上所有节点，并使用max(节点的clock，接收的节点clock)来更新。

- Yjs提供丰富的数据结构YArray, YMap, YText等，而且数据结构间还可以组合一起，这样可以利用这些组成更加复杂的数据结构非常方便容易融入不同应用场景中。

- `Item`作为Yjs最核心的结构，支撑其他所有结构的实现
- `id`由[clientId, clock]组成，CRDT算法要求每个字符都分配一个id，而Yjs为了节省空间，会把相同clientId且连续的字符串合并成一个Item
  - 所以Item的id也就是第一个字符的id，而通过clock+字符串长度得到Item最后一个字符的id
- `origin和rightOrigin`指向的是Item插入时位置前后的字符的ID，主要是用在解决冲突的时候用来维持原始用户操作意图；
  - `left，right`是Item的经过解决冲突后实际前后节点，所以Item是双向链表的结构，而且left，right不会参与序列化传输的，只有origin，rightOrigin和content会被序列化传输过去；
- `parent`指向父节点(YText)，`parentSub`当父节点内容是YMap时，parentSub就是key；而父节点内容是其他的时候就是为null了。
- `content`就是Item实际承载的内容可以是ContentString，ContentJSON，ContentDoc，ContentType等等。

- `integrate`方法是Item的核心方法，主要是通过待插入Item的origin和rightOrigin，然后在Item链表里面寻找适合的位置进行插入。
  - 因为left，right属性是不跟在一起传输的；所以接收到外部操作的时就是使用getMissing方法，在本地Item链表上去寻找origin 和 rightOrigin，作为初始的left和right，
  - 如果找不到origin或rightOrigin的Item意味着仍然有其他用户依赖的操作还没有接收，放到等待队列里面，等接收到必须的操作才进入解决冲突。
- integrate方法，这个时候我们需要解决origin和rightOrigin之间存在的节点冲突。
- Yjs使用的是自己一套解决冲突的方法，核心规则就是：
  - origin之间的连线不能相交；
  - 满足规则1后，clientId小的节点排在左边；
- 红色连线都是节点的origin指向，当两根红线交叉的时候其实已经说明用户意图已经被破坏了；
  - 多人协作中解决冲突只能尽可能达到最优，很多时候没有完美的解法。

- Yjs的删除操作采用的是很多CRDT算法所采用的墓碑方式：即不做任何实际删除操作，只是仅仅做一个标记，
  - 这也是很多人对CRDT担忧的意味着随着操作增加空间占用也会越来越大，性能也会越来越低。
  - 删除的Item最终会转变成DeleteItem加入到transaction的deleteSet中，然后会跟着序列化传输到其他用户上。
  - 同样当接收到反序列化后的deleteSet，发现如果有其他操作还没接收到就会放到store的pendingDs等待后面接收到新的操作再进行处理。

- 所有delete的节点只会标记一下，并不会真实的处理，但是Yjs也提供了一个GC的方法来回收内存。
  - gc的方法就会把内容替换成ContentDelete，Yjs在每次transaction结束时都会触发一次tryGcDeleteSet
  - 默认的gcFilter都是返回true，所以默认情况下删除的Item都会被gc掉。

- `YText`是需要重点探索的一个数据结构，Yjs对于文本操作只提供插入，删除和格式化三个操作。
- insertText
  - Yjs的所有操作都是在一个transaction里面进行的，在transaction里面先通过findPosition找到文本开始插入的Item位置，如果插入的位置在Item的中间就需要splitItem分裂成两个Item。
  - 这个遍历是从Item列表一开始查找遍历的所以是一个O(n)的操作，但是Yjs会通过保存最近操作的位置来加快搜索速度，而且在搜索的过程中也要计算文本的格式属性，文本的每一个属性也会生成一个Item，它的content会是ContentFormat(主要是一个key value的键值对)。
  - 这种方式对操作格式化其实挺复杂的；
  - 无论增加还是删除文本的时候要清除它的格式都会异常麻烦。

- 简略说明一下整个transaction过程：
  transaction初始化时先计算beforeState (StateVector)
  业务操作
  清理阶段
  1）计算afterState（StateVector）用于跟beforeState对比，找出前后的差异
  2）尝试合并deleteSet（让传输信息体积更小）
  3）触发YText，YArray等结构上的事件监听器；类似在YText上会遍历整个Item链表找出有哪些节点是改动或者增加的，聚合到事件上
  4）尝试回收被标记删除的Item节点
  5）尝试合并已经标记删除的Item节点（让Item链表节点更少，占用内存更少）
  6）尝试合并新添加的Item节点
  7) 把新增加的Item节点和deleteSet写入UpdateMessage，然后触发文档上的update事件
  然后就可以把UpdateMessage发送给其他用户节点了

- deleteText
  - 只需要找到对应文本的Item节点然后调用它的delete方法即可，但是还要清理文本的格式就很麻烦了，需要小心处理不能清除会影响后续文本格式的属性

- 如果要格式化一段文本，同样需要以下步骤：
  找出需要格式化的文本的开始节点位置
  计算前面继承来的格式集合与即将插入的格式集合的差集合，根据计算的集合分别插入对应的ContentFormat节点
  然后遍历要格式化文本里面的所有节点，把不一样的ContentFormat节点删除，同时收集会影响后面文本的格式集合
  把收集的受影响格式重新插入到被删文本的节点后面

- `YArray`属于简化版本的YText，略过。

- `YMap`每个Key都指向一个Item双向链表，跟YText不一样的是，Key永远指向这个链表的最后一个节点，而其他节点都会标记为删除。
  - get/delete都直接读取/删除最后一个节点即可

- Yjs主要通过两个协议来完成各个节点间的同步交互：
- AwarenessProtocol
  - 用于节点发现，更新和离线事件感知
  - 通过解包所有来往AwarenessMessage并记录每个Client的状态，如果发现没有记录的Client就加入到Client Add List里面
  - 对于用户离线的判断，AwarenessProtocol主要靠两种方式：接收到节点发送state为null的信息; 超过30s没有接收到用户的信息
- SyncProtocol
  - 用于节点与节点间状态同步，文档描述整个过程实际只有两步，但是还是根据y-websocket把整个过程呈现出来比较直观
- LocalState本质上是各个节点对文档的操作序列，AwarenessState则是自定义一些状态。
- UpdateMessage本质就是一个包含各个client操作序列的Map，对于每个操作我们所需要考虑的只有三点：
  - 我们本身的LocalState是否有满足操作依赖的origin和rightOrigin
  - 要是LocalState不能满足，是否能在接收的UpdateMessage找到依赖
  - 要是都找不到，意味着仍然需要等待之后的UpdateMessage；这些没办法应用的操作就得放到pendingStructs结构中
- 如果最终都能满足操作的依赖那就可以执行Item的integrate方法

- Yjs的undo/redo有两种可选方案：
- 基于编辑器的undo/redo
  - 这种方案主要针对富文本编辑器这里自带操作历史记录管理，只要undo/redo时候Yjs跟着应用对应操作即可，Yjs本身无需做额外处理。
- 基于Yjs自身的UndoManager
  - UndoManager可以针对更加复杂的应用场景，本身Yjs提供的数据可以自由组合完全可以脱离富文本这种场景使用，而且UndoManager可以只针对组合结构里面任一子结构进行管理，灵活性大很多。
- 但是总结两种方案对于undo/redo都会影响全局的其他用户，也就是意味不能单独只undo/redo自身操作（一般这种更符合使用体验），如果需要这种效果需要做更进一步的处理。

## 💡 [探秘前端 CRDT 实时协作库 Yjs 工程实现 - 知乎 _202201](https://zhuanlan.zhihu.com/p/452980520)

- 本文会从 Yjs 的工程实现出发，介绍一个典型的工业级 CRDT 库是如何实现以下能力的

### 建模数据结构

- 在 Yjs 中，不论是 YText、YArray 还是 YMap，这些 YModel 实例中的数据都存储在一条双向链表里。
  - 粗略地说，这条链表中的每一项（或者说每个 item）都唯一地记录了某次用户操作所修改的数据
  - 对 YModel 的操作，最后都会转为对这条链表的 append、insert、split、merge 等结构变换。
  - 链表中每个 item 会被序列化编码后分发，而基于 CRDT 算法的保证，只要每个客户端最终都能接收到全部的 item，那么不论客户端以何种顺序接收到这些 item，它们都能重建出完全一致的文档状态。
- 基于上述手段实现的 CRDT 结构是 CRDT 流派中的一种，可以将其称为 operation-based CRDT、list CRDT 或 sequence CRDT。
- 显然， 在多人实时协作这种无法保证 item 接收时序的场景下，每个 item 都需要携带某种标识，供系统唯一确定其在逻辑时间轴上的位置。
- Yjs 会为每个 item 分配一个唯一 ID，其结构为 `ID(clientID, clock)`.
  - 这里的 clientID 和 clock 都是整数，前者用于唯一标识某个 YDoc 对应的客户端，而后者则属于一种名为 Lamport timestamp 的逻辑时间戳，可以认为这就是个从零开始递增的计数器
- 可以借助文本编辑的例子来理解这种 list CRDT 的工作方式。在未经任何优化的朴素情况下，这种结构要求我们把每个字符插入操作都建模为一个 item，也就是每个字符都携带了一个逻辑时间戳 ID
  - 这几个字符每个都对应一个 item（或者说一次字符插入的 operation）。它们通过 left 和 right 字段连接在一起。在插入新字符 T 的时候，Yjs 就会根据 item 的 ID 在链表中查找合适的插入位置，将新字符对应的 item 接入链表中。另外同个用户持续追加的文字也会被合并成 length 很长的单个 item，避免大量碎片化对象的性能问题。
- 在文档的高频增删过程中，并不是所有 item 都会持续存在于链表中。但由于 CRDT 的冲突解决需要依赖历史 item 的元数据，我们并不能直接将历史上的 item 硬删除，至多只能移除掉该 item 对应的 YModel 内容（为此 Yjs 特别设计了 GC 对象来将废弃的 YModel 替换为空结构，相当于一种墓碑机制）
- 该使用怎样的数据结构来存储文档内所有的 item 呢？
  - 由于任意 item 均可用 ID 来排序，因此一种选择是使用 B 树这样具备对数级优良插入和删除时间复杂度的数据结构，将所有的 item 维护在一棵平衡二叉树中。
  - 但实践中 Yjs 选择了一种更简单直接的方案，即为每个 client 分配一个扁平的 item 数组，相应的结构被称为 StructStore
- 每个 item 数组都是按 clock 字段的值来排序的。这样只需要做一次二分查找，就能快速找到某个 ID 对应的 item。
  - 在接收到远程 item 时，Yjs 除了将 item 插入链表，也会将它插入 StructStore 中的相应位置。
- 因此我们可以认为，Yjs 中存在两种索引数据的方式：
  - 依据文档结构顺序（即 document order）建模的双向链表。
  - 依据逻辑时序（即 insertion order）建模的 StructStore。
- item 相当于一个携带 left / right / ID 等 CRDT 字段的容器，其中具体的 YModel（或者说 AbstractType）数据会存储在 item.content 字段中，另外还有 parent 和 parentSub 字段会用于辅助表达 YMap 等嵌套结构的父子关系。
  - 由于 item.content 也能携带任意的 YMap 等 AbstractType 数据，这样就自然地支持了数据的嵌套。
  - 基于这种链式结构，此时一份 YMap 就对应于一系列的 entry，其中每个 key 都使用逻辑时间轴上最新的数据为当前状态，而这个 key 下其他更早的状态所对应的 item 都会被标记为删除。
- 为了优化本地插入的速度，Yjs 还设计了额外的缓存机制。如果在文档中任意位置随机插入新字符，这时新字符对应的 item 理论上需要 O(N) 的时间复杂度才能插入链表中。
  - 但实际上，大多数插入操作都会跟随在用户最后编辑的光标位置。
  - 因此 Yjs 默认会缓存 10 个最近的插入位置供快速匹配，在内部实现中这被称为 skip list（作者认为这一缓存机制是受到了跳表的启发）或 fast search marker。

### 解决并发冲突

- Yjs 中的 item 会组成一条双向链表。但为了妥善地解决冲突，它的实现并不仅包含 left 和 right 字段，还有这两个字段：
  - origin 字段存储 item 在插入时的左侧节点。
  - rightOrigin 字段存储 item 在插入时的右侧节点。
- 每个 item 在插入文档时都需要执行其 `integrate` 方法，核心的冲突解决算法就在这里用到了上述这些字段，一共仅有约 20 行
- 根据 Yjs 所用 YATA 算法的论文，上述代码的核心思想是保证新潜在插入 item 的左右连线（即下图中的红线）不形成交叉
- 有趣的是，冲突在实际应用中其实很罕见。因此虽然上面这段代码属于 CRDT 库的算法核心，但一般却很少会执行，也可以理解为一种保证数据不会因并发更新而损坏的保障性机制。

### 回溯历史记录

- 实际上一份文档中所有的 item 结构都可以被持续存储下来，这显然对历史记录有很大的价值。为此 Yjs 也自带了 UndoManager 来提供开箱即用的历史记录管理功能。
- 在讨论 UndoManager 的实现方式前，我们需要了解 Yjs 对删除操作所做的特殊处理。在 Yjs 中，每个 item 均可以被标记为删除（可以通过 item.deleted 的 getter 来检查），但 item 中并没有记录关于删除操作的更多信息
  - 在 item 中不会记录它时何时被删除，或是被哪个用户删除了。
  - 在 StructStore 中也不会记录删除操作。
  - 在删除发生后，本地的 clock 不会递增。
- 删除操作的信息是在哪里建模的呢？Yjs 引入了 DeleteSet 的概念，可以记录逻辑时间轴上某段时间内（或者说某次 transaction 中）所有被删除的 item，这份数据也会独立于 item 分发。
  - 换句话说，Yjs 中的删除操作被设计成了独立于双向链表的结构。
  - 在处理删除操作时，Yjs 的设计则相当于一种更简单的 state-based CRDT。
- 每次更新对应的 transaction 都包括两份数据：
  - 这次更新所插入的 item。
  - 这次更新所删除 item 的 DeleteSet。
- 在网络上实际分发的二进制增量更新数据，就是序列化编码后的 transaction。
  - 可以认为 transaction 既会用于编码更新，也是撤销重做操作对应的粒度。
- 基于上述数据结构，可以发现只要做两件事就可以撤销掉一次 transaction
  - 将这次 transaction 所插入的 item 标记为删除。
  - 重新插入这次更新所删除的 item（对 item 的删除是不可撤销的）。
- 由于 DeleteSet 的结构非常轻（例如在记录了真实用户 LaTeX 论文编辑过程的 B4 benchmark 数据集中，18.2 万次插入和 7.7 万次删除后仅生成了 4.5KB 的 DeleteSet），这种设计就进一步贴近了「零开销抽象」，因为删除时并没有创造出任何未知的新数据。

- 不过，个人认为这种设计虽然能起到更极致的优化效果，但也让维护变得更加困难了。如 UndoManager 之前一个难以修复的问题就是「连续撤销 3 次内可重做返回原始状态，4 次以上则可能丢失字段」。这一问题的根源在于当时的实现对 item 复原的逻辑有问题

- 如果有同学希望实现自己的试验性 CRDT 库，基于 DeleteSet 的优化应当并不属于第一个原型中就需要实现的能力。

### 同步网络状态

- 虽然 CRDT 库本身与具体的网络协议无关，但作为一整套渐进的解决方案，Yjs 也设计了配套的网络协议。
  - 整份 Yjs 文档可以被编码为 Uint8Array 形式的 update 数据，Yjs 也可以从二进制数据中反序列化出 YDoc 的对象结构。每次文档更新的 transaction 也会计算出增量的更新以供同步，其中包含 item 和 DeleteSet，如前所述。
  - Yjs 通过 state vector 的概念来定位逻辑时间轴，这种数据结构实际上就是一组记录了某时刻全部客户端 (client, clock) 的 tuple。

- 在同步文档状态时，Yjs 划分了两个阶段：
  - 阶段一：某个客户端可以发送自己本地的 state vector，向远程客户端获取缺失的文档 update 数据。
  - 阶段二：远程客户端可以使用各自的本地 clock 计算出该客户端所需的 item 对象，并进一步编码生成包含了所有未同步状态的最小 update 数据。

### 总结

- 到此为止，我们已经介绍了 Yjs 主要的内部特点：
  - 基于双向链表和 StructStore 的基础数据结构
  - 基于 YATA 算法的并发冲突解决机制
  - 基于 DeleteSet 和 Transaction 机制的撤销重做
  - 基于两阶段划分的同步机制

- 由于 Yjs 背后 CRDT 极佳的去中心化性质，它在 Web 3.0 时代或许有机会成为某种形式的前端基础设施。从它的案例中我们可以感受到，学术研究成果的实用化并非一蹴而就，更有赖于大量具体的工程细节处理与针对性优化，这背后仍然绕不开基础的数据结构和算法等计算机基础知识。

- discussion

- Yjs的算法先进，但在实际应用中确存在下面的问题：
  1. fast search marker 不支持在 YXmlText 中使用
  2. 不支持移动操作，移动后的合并位置不符合预期 (v14已实现)
  3. ContentFormat 不支持同类型样式的嵌套或交错（不能还原 ProseMirror Mark 的特性）
  4. ProseMirror 的 Step 和 Yjs 的 insert/delete API 不匹配，y-prosemirror 采用了一套 diff 算法，导致用户意图丢失。也许与 Quilljs 结合没有这样的问题。

- 墓碑也是 item，连续输入的 item 本身就可以被合并。然后如果你希望文档始终可以合入潜在的离线编辑，那确实就得维护所有历史 item。不过据我所知很多 OT 方案也是把所有 operation 的 JSON 全扔 DB 里……如果是协作 VSCode 之类产品，最后一个人关闭页面（房间）时就可以把 YDoc 干掉了。

- 每次update 是否都需要向其他客户端都发送一份完整的数据
  - 不用 首次启动state vector来首次同步，后续就只发送update数据了

## [浅谈 CRDT 与 Yjs - 知乎](https://zhuanlan.zhihu.com/p/634631128)

- shared types 是 Yjs 对外暴露的基础类型。实际上，Yjs 底层的数据结构 Item 和 shared types 是一一映射的关系。
  - `Item` 的 `content` 字段指向 share types 实例，而 share types 实例对象的 `_item` 字段指向Item。
  - 因此，当调用 share types 的 insert 时，实际上是插入 Item。
- Item的核心数据结构
  - ID。Item 的唯一标识符（ID），由客户端唯一 ID（clientId）和 Lamport 时间戳（clock）组成，确保每个客户端生成的 ID 是唯一的；
  - content。content 指 Item 所存储的数据（比如对应插入的字符串）。正如前面提到，content这里是直接指向了 share types 实例，存储了当前 Item 对应的基础类型或者复合类型；
  - position。postion 包括：left，right（Yjs 的 CRDT 数据结构基于双向链表，依赖于此）；origin，originRight，这两项属性是为了解决冲突；parent，parentSub，这两项是为了支持 Yjs 的灵活的嵌套数据结构；

- 不同 Doc 实例之间是通过 update 来进行数据的同步。update 主要是由 structs（所有 Item）和 ds（基于 state-base crdt 的 DeleteSet）组成

- 副本间的数据同步
  - 本地 Doc 副本发生的 insert 和 delete，通过转发给 transaction（src/utils/Transaction.js）统一处理；
  - transaction 收集完 update 便会将其广播给各个监听的 Doc 副本；
  - 其他 Doc 副本收到 update 之后，会进行计算和处理，存入本地的 struct store, struct store 在基于 state vector 的数据同步里，发挥了重要作用，被同步方可以使用二分法可以快速查到缺少的 structs 给同步方

- 相对位置保证了多个操作（update）能够以相同的因果顺序在不同副本中被 apply，即使并发，文档状态也能收敛至相同的状态，从而保证操作的因果一致性。
- 在线协同编辑领域，冲突解决需要保留意图。
  - Yjs 的实现是基于 YATA 算法
- YATA 算法有如下几个规则：
  - 禁止发生冲突的的插入的 origin 连线 之间发生交叉。
  - 规则 2 是指定了解决冲突函数的传递性
  - 当两个冲突的插入具有相同的 origin 时，创建者 id 较小的插入位于左侧。创建者 id 对应的就是 Yjs 的客户端唯一 ID（clientId）；

- Yjs 的优化
- Yjs 会根据用户的操作和兼容性，进行 Item 的合并。比如：当用户按顺序键入字符“ABC”，实际上B Item，C Item 会和A Item 合并为一个 Item。该优化降低了 Yjs 的存储开销，降低本地副本的计算复杂度，同时也降低了副本间同步的延迟；
- 优化 Item 部分字符删除的操作。
  - 比如：当用户在 content 为"ABC"的 Item 中的字符"A"时，会将 "ABC" Item 拆分成：标记位为 deleted 的 A Item，BC Item。
  - 该优化和前一优化的作用相似，同时这个优化也对undo/redo 有作用：使本地副本的操作历史更贴近用户实际的编辑情况，方便理解文档的修改历史；

- 为了优化本地插入的速度，Yjs 还设计了额外的缓存机制。
  - 如果在文档中任意位置随机插入新字符，这时新字符对应的 Item 理论上需要 O(N) 的时间复杂度才能插入链表中。但实际上，大多数插入操作都会跟随在用户最后编辑的光标位置。
  - 因此 Yjs 默认会缓存 10 个最近的插入位置供快速匹配，在内部实现中这被称为 skip list（作者认为这一缓存机制是受到了跳表的启发）或 fast search marker。

- 在副本间进行同步的时候，有时候需要交换差异。
  - 比如两个副本间使用 websocket 进行广播的时候，初始连接的时候，需要交换副本间的信息。
  - 为了低通信成本地交换差异，Yjs设计了如下的数据结构： `Map<clienId, clock>`，称之为 state vector（状态向量）。
  - 副本间通过交换 state vector，可以得知新连接的副本缺少的 update 并只将缺少的 update 发送给新连接的副本。
  - state vector 本身的数据结构体积很小，同时 state vector 使得副本间的同步无需传递整个副本，降低了同步时的数据传输消耗。

- Yjs大量使用了二进制存储和传输：
  - 使用类似 protcol buffer 的协议，将 json 格式的数据转换成如 uint8array 的二进制格式。比如：通过优化，在 json 中形如 {testA:'6', testB:'125'} 的数据结构，通过二进制转换，请求参数就不需要再包含字段 (testA，testB) 名称，只需发送类似 [6, 125] 的数据，降低网络请求的传输成本。
  - 优化数字的存储空间。比如"125"作为字符串在浏览器请求的中是9个字节（utf8编码格式），而作为二进制数，比如 uint8array 中传输只需要占用一个字节的空间。
# blogs-crdt-algorithms

## [Near Real-Time Peer-to-Peer Shared Editing on Extensible Data Types](https://www.researchgate.net/publication/310212186_Near_Real-Time_Peer-to-Peer_Shared_Editing_on_Extensible_Data_Types)

## 🧮📕 [【译】Near Real-Time Peer-to-Peer Shared Editing on Extensible Data Types - 掘金](https://juejin.cn/post/7027487213525041166)

- 在此之前，我们证明了 发生冲突的插入操作 存在全序关系。
- 在本节中，我们将给出一个算法，当我们已经有一个有序的插入列表时，计算新的插入的位置。
- 该算法利用不存在的交叉的 origin 链接作为中断条件。因此，当连接之间会交叉时，停止计算。

## [YATA线性数据插入算法](https://juejin.cn/post/7030327499829542942)

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

## [YATA：一种针对文本编辑优化的 CRDT 算法](https://hyrious.me/p/yata.html)

- YATA 算法的核心是：如果我们把参考节点一起发出去，新节点和参考节点之间连线，那么所有的这种连线都不能交叉。

- 如果有两个新元素的参考元素是同一个，这意味着发生了冲突，此时 YATA 算法引入了一个新的属性：right，表示参考元素右侧的元素。当发生冲突时，我们先切换到比较右侧元素上来，当右侧元素也一样时，再通过 id 排序决定。
# blogs-yrs

## [Delta-state CRDTs: indexed sequences with YATA _202108](https://www.bartoszsypytkowski.com/yata/)

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

## [Deep dive into Yrs architecture _202110](https://www.bartoszsypytkowski.com/yrs-architecture/)

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
# more
