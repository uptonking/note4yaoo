---
title: lib-editor-collab-blog
tags: [blog, collaboration, editor, lib]
created: '2021-10-14T11:16:52.887Z'
modified: '2021-10-14T11:18:03.650Z'
---

# lib-editor-collab-blog

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
# [实时协同编辑的实现__201404](https://fex.baidu.com/blog/2014/04/realtime-collaboration/)
- 这里所说的实时协同编辑，是指多人同时编辑一个文档，你可以实时看到别人做出的修改，不用手动刷新页面。
- 在最近某个项目中打算使用协同编辑来解决冲突问题，因此抽空调研了现有的实现方案
- 要实现实时编辑，我们需要解决两个技术点：实时通信问题、编辑冲突问题，
  - 其中实时通信问题比较好解决，可以使用 long pull 或 WebSocket，所以这里就不过多讨论了，重点将放在如何解决编辑冲突问题上。
- 按从易至难的顺序来介绍几种可行的方案，分别是：「编辑锁」、「GNU diff-patch」、「Myer’s diff-patch」、「Operational Transformation」和「分布式 Operational Transformation」。

## 编辑锁

- 编辑锁这是实现协同编辑最简单的方法，
  - 简单来说就是当有人在编辑某个文档时，系统会将这个文档锁定，避免其他人同时编辑，
  - 因为实现简单，所以这个方案是应用最广的，比如公司内部常用的 TWiki 系统，
  - 采用这种方式虽然可以在一定程度上避免覆盖问题，但它的使用体验不好，也做不到「实时」，所以这里就不讨论了。

## GNU diff-patch

- Git 等版本管理软件其实也是一种协同编辑工具，因为每个人都可以并行编辑，遇到编辑同一个文件时可以自动合并，因此我们也能使用类似的原理来实现协同编辑，具体可以有两种方法：diff-patch 和 merge。

- 先说 diff-patch，这里的 diff 和 patch 是指两个 unix 下的命令，diff 能输出两个文本的不同之处，然后用 patch 来更新其它文件，
- 我们只要在 JS 中实现这两个算法，就能通过如下流程来实现协同编辑：
  - 每个用户进来时都建立长连接，保存好当前文档副本
  - 有人编辑时，如果停顿 5 秒（具体要根据产品策略），就将现有文档和之前的副本进行 diff，将结果传给服务端，更新副本
  - 服务端更新文档，然后通过长连接将这个 diff 结果发给同时在编辑的其它用户，这些用户使用 patch 方法来更新 ta 们文档

- 但 GNU diff 有个问题，因为基于行匹配的，所以很容易冲突
- 使用 patch 命令部下，它在冲突后会生成一个新文件 my-new.txt.rej 来描述失败原因，这种展现方式不直观，需要打开两个文件比对，
  - 我们使用另一种方式来更好地展现，那就是接下来介绍的merge命令
  - merge命令和Git等工具中的合并算法是一样的
- 通过使用我们可以发现 merge 命令有个缺点，那就是需要使用 3 份完整的文本来进行比较，为了避免每次传递所有文本内容，我们可以结合使用 diff 来减小传输体积，在后端 patch 成新的文本。
- 无论是 diff 还是 merge，由于它们的算法都是基于行进行比较，导致对同一行的编辑必然冲突，为了解决这个问题，我们可以尝试基于字符粒度的 diff 算法，那就是接下来将介绍的 Myer’s diff-patch。

## Myer’s diff-patch

- 它的 diff 策略是基于字符匹配的
- 整体来看 Myer 算法可以低成本地解决大部分问题，所以有些在线编辑器选择它来实现协同编辑功能，比如 codebox
- 不过 Myer 在某些情况下会丢字符，是否还有更好的方法？答案是有，那就是接下来介绍的 Operational Transformation 技术。

## Operational Transformation

- OT技术正是 Google Docs 中所采用的方案
- 看了之后才后发现它的原理并不复杂
- 首先，我们可以将文本内容修改转成以下 3 种类型的操作(Operational)：
  - `retain(n)`：保持 n 个字符，也就是说这 n 个字符不变
  - `insert(str)`：插入字符 str
  - `delete(str)`：删除字符 str
- 提取这些操作可以通过 Levenshtein distance（编辑距离）算法来实现。
  - 我们需要转换 B 的操作来适应新的字符串
- 这个转换算法就是OT的核心，实际上 OT 指的是一类技术，而不是具体的算法，
  - 这个思路就是首先将编辑转成操作(Operational)，如果多人操作同时进行，需要对这些操作进行转换(Transformation)，这就是为什么叫 Operational Transformation，
  - 而具体应该拆分成哪些操作以及转换算法都是可以自定义的，因此 OT 可以灵活地支持各种协同编辑应用，比如非文本类的编辑。

## 分布式 Operational Transformation

- 顺序问题
  - 首先第一个问题是顺序问题，因为 OT 等算法都是依赖顺序的，不同顺序会导致结果不同，
  - 这个问题的解决方法很简单，我们可以在客户端和服务器端都加上队列来保证请求顺序，等前一个请求结束后再发下一个请求。

- 存储的原子操作
  - 如果有多台服务器，或者有多个线程/进程在同时处理请求时就会遇到覆盖问题，因为读写数据库并不是原子操作
- 好在这种问题还算比较常见，解决办法可以有 3 种：
  - 保证操作只在一个线程中执行，比如某个文档的更新只在某个固定的机器，使用 Node 这样的单线程模型提供服务，这样就不可能并行修改了
  - 如果数据库支持事务(transaction)，可以通过事务来解决
  - 如果数据库不支持事务，就只能用分布式锁了，如 ZooKeeper
  - 从实现角度来看，第一和第二种方法都比较简单，而第三种方法会带来很多问题，比如可能导致文档被锁死，假如上锁后由于种种原因没有执行解锁操作，这个文档就会永远被锁住，所以还得加上超时限制等策略。

- 版本管理问题
  - 要解决这个问题，就必须引入版本，每次修改后都需要存储下新版本，
  - 有了版本我们就能使用 diff 功能来计算不同版本的差异，得到其它人修改的内容，然后通过 OT 合并算法合并两个操作
  - 如果保存所有版本会导致数据量大大增加，所以还需要再优化，比如每个服务器保存一个数据副本，但这里就不再展开了，可以看要支持分布式 还是挺麻烦的

## 初步结论

- 如果你只是一个内部小项目，实时性要求不高，但对准确性要求比较高
  - 推荐用 merge 或 diff3 工具，出现同一行冲突时由用户来解决，这样能避免自动合并有可能出错的问题

- 如果想具备一定的实时性，流量不大，不想实现太复杂，且对少量的冲突可以忍受
  - 推荐用 Myer’s diff，后端只开一个 Node 进程

- 如果想具备实时性，且有多台后端服务同时处理
  - 可以用 Operational Transformation 或 Myer’s diff，但需要注意分布式带来的问题

- 如果需要很精细的控制，如支持富文本编辑等非单纯文本格式
  - 只能使用 Operational Transformation，但要自己实现操作合并算法，比如 XML

- 除了文本合并，真正要做在线编辑还有很多细节处理
  - 支持选区，看到其他人选择的文本段，当然，这也有合并问题
  - 指针要更随文本变化移动到正确的位置
  - 支持undo
# ref
- [How Figma’s multiplayer technology works__201910](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/)
