---
title: lib-collab-ot-blog
tags: [blog, collaboration, ot]
created: 2022-10-13T07:59:24.658Z
modified: 2022-10-13T07:59:45.878Z
---

# lib-collab-ot-blog

# guide
- [协同文档方案调研资源汇总](https://github.com/GarinZ/Blog/issues/2)
# [如何实现协同编辑 - 理解Operational Transformation](https://garinzhang.com/coding/how-to-implemente-collaborative-editing-understanding-operational-transformation.html)
- 整体来看，OT解决并发编辑冲突问题的思路有以下几步
- 定义原子操作类型
  - 将用户在UI上触发的基于Event的操作抽象成由可枚举的N个原子操作类型组成的操作序列，这样一来复杂的UI界面操作的冲突就转换成了原子操作之间的冲突，同时也为多端数据同步定义了基本数据结构。
- 设计冲突解决算法
  - 通过算法能将冲突的2个操作序列转换成2个可以和原来冲突的操作序列串行执行的新操作序列。
  - 可串行的两组操作序列作用在文本后，产生的影响相同。
  - 串行后的操作需要保持原有语义
- 多端冲突解决
  - 通过向各端同步新的可串行操作序列完成冲突解决

- 在图中所有调用transform方法的地方都是冲突发生的地方。
  - 也就是说在实际的协同编辑应用中，冲突会在两种场景下发生：
  - 1）Server接收到Client上传的操作。
  - 2）Client接收到Server广播的操作。

- 在Client/Server协作时，还有几个事实我们需要意识到：
  - Client和Server都需要进行冲突解决，那么两端需要配置同构的transform算法
  - 由于冲突解决算法的串行化逻辑一定是有倾向的：在上文的实现对同一位置的相同操作，operationA要优先于operationB）。那么为了最终一致性，Client和Server端都必须偏向Server端。所以Client同步下来的操作必须放在operationA的位置，Server获取到的新操作必须放在operationB的位置

- 整体来看，OT是一种基于阻塞同步的多版本并发控制方案。
  - 阻塞同步：每次冲突解决时，只同步处理两个operation
  多版本：Client/Server端同时存在从同一个版本衍生出的的修改，最终通过某种方式再次合并成一致的版本。

# [OT算法](https://juejin.cn/post/7022681910337863687)
- 分析了ot.js的客户端、服务端实现
# [协同编辑中使用的 OT 算法是什么？](https://zhuanlan.zhihu.com/p/559699843)
- OT 算法可以解决一致性问题
- 这里的核心在于这个 transfrom 方法，它能够对操作进行修正。transform 没有固定实现，要根据实际需求自行实现。
- transform 操作既发生在服务端，将基于某个版本的并发操作对象转换成串行操作。也发生在客户端，本地的修改还没来得及提交，就收到了服务端推送。
- https://codesandbox.io/s/b8ds8h
# [实时协同编辑的实现 diff-patch/OT__201404](https://fex.baidu.com/blog/2014/04/realtime-collaboration/)
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
# more-blogs
- [An Intro to Operational Transformation](https://davidwalsh.name/collaborative-editing-javascript-intro-operational-transformation)

- [Operational Transformation, the real-time collaborative editing algorithm](https://srijancse.medium.com/operational-transformation-the-real-time-collaborative-editing-algorithm-bf8756683f66)
  - In this post, I would be digging deep into the transformation function, how clients wait for acknowledgement from the server before sending more operations and the compound operational transformation.

- [Operational Transformations as an algorithm for automatic conflict resolution](https://medium.com/coinmonks/operational-transformations-as-an-algorithm-for-automatic-conflict-resolution-3bf8920ea447)
  - 示例流程图较多
