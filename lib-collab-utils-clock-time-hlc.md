---
title: lib-collab-utils-clock-time-hlc
tags: [collaboration, crdt, hybrid-logical-clock]
created: 2023-01-18T17:00:07.960Z
modified: 2023-03-20T10:28:16.979Z
---

# lib-collab-utils-clock-time-hlc

# guide

- search
  - https://github.com/search?type=code&q=HybridLogicalClock++language%3Ajavascript
  - https://github.com/search?type=issues&q=hybrid+logical+clock+language%3Ajavascript+language%3Atypescript&s=updated&o=desc
# hybrid logical clock
- who is using #hybrid-logical-clock
  - jaredly/local-first: hlc + rga
  - verdant/lo-fi: hlc + websocket, no-merkle
  - harika: hlc + sqlite + absurd-sql, no-merkle
  - evolu: hlc + sqlite + merkle-tree
  - CockroachDB
  - YugaByte DB
  - tinybase
  - crsqlite
  - Ditto: hlc
  - TiDB: Centralized clock

- hlc可以解决lamport逻辑时钟无限增长的问题

- hybrid-logical-clock roadmap 待改进的地方
  - 需要保存所有op，新客户端需要获取所有op从头开始计算
  - 每个单元格都有一个clock，其实可以每行保存一个clock+每列保存到该clock的偏移量
  - ref
    - [crsqlite](https://github.com/vlcn-io/cr-sqlite#3-crdts-for-mortals)

- tips
  - 不必执着于hlc的使用案例，可对成熟案例在业务逻辑不变的情况下将其他clock替换成hlc

## blogs

### [Ditto Delta State CRDT](https://docs.ditto.live/javascript/common/how-it-works/crdt)

- [Extend Hybrid Logical Clock documentation](https://github.com/getditto/docs/issues/413)

- The Ditto document is a JSON like document made from a CRDT Map that represents the JSON Object. 
  - The JSON properties are map keys, and the values are any of the Counter/Register/Map types
  - One way to think about the types that make up a Ditto document is like a tree, where there are collections (Array and Map) and leaf values that are registers or counters.
  - Register: A single primitive value (Number, String, Boolean, Binary File)
  - Counter: A special number capable of preserving incrementing and decrementing semantics
  - Map: A dictionary of name->value mappings

- The foundation of determining how data should be merged is using a Ditto document's **version vector**.
  - Every time a change is made to a document, the version of that document is incremented by one. 
  - When a peer incorporates changes from other peers, the local peer can use the incoming remote peer's version vectors to determine whether the changes are new or old. 

- Each document in each peer contains a hidden metadata map of a `Site_ID` and a `HLC`. 
  - The HLC stands for a hybrid logical clock. This HLC is used to determine whether a change has "happened before".
  - Ditto uses a `UInt128` to represent the `Site_ID` and `64bit` timestamp for the `HLC`. But for educational purposes, this documentation will often use strings and numbers for readability.
- In Ditto's distributed system, the HLC is a `64-bit` timestamp comprised of `48 bits` of a physical timestamp and `16 bits` of a monotonically increasing logical clock.

### [计算机的时钟（五）：混合逻辑时钟 Hybrid Logical Clocks](http://yang.observer/2020/12/16/hlc/)

- 前面的文章中我们介绍了计算机处理时钟的两种方式，
  - 一种是物理时钟，包括NTP协议和TrueTime都属于物理时钟，
  - 另一种是逻辑时钟，包括Lamport逻辑时钟和向量时钟。
- 物理时钟的优点在于直观，就是真实世界的时间，使用方便，缺点在于无法做到绝对精确，成本相对高一些。
- 逻辑时钟的优点在于可以做到精确的因果关系，**缺点**在于节点之间需要通信，而且使用上不如物理时钟直观。

- 混合逻辑时钟(HLC)将物理时钟和逻辑时钟结合起来
  - 2014年的论文《Logical Physical Clocks and Consistent Snapshots in Globally Distributed Databases》中提出。目的是为了填补理论（逻辑时钟）和实际（物理时钟）之间的差距，支持因果关系，同时又有物理时钟的直观特点。
- 给分布式系统中每个事件分配一个HLC，比如e事件的HLC记作 l.e，HLC保证能够满足以下四个性质：
  - 如果 e 事件发生在 f 事件之前（e happened before f），那么 l.e 一定小于 l.f，也就是满足因果关系。
  - l.e 可以存储在一个整数中，不会随着分布式系统中节点数的增加而增加。（这点和向量时钟不一样，向量时钟会随着节点数的增加而增加）
  - l.e 的值不会无限增长。（这点和Lamport逻辑时钟不一样，Lamport逻辑时钟会无限增长）
  - l.e 的值和 e 事件发生的物理时钟值接近，| l.e - pt.e |的值会小于一定的范围。

- 虽然在Lamport逻辑时钟的基础上引入了物理时钟，但是我们却不知道这个值究竟是物理时钟增长导致的还是逻辑时钟增长导致的。这样即使物理时钟的增长追赶上了逻辑时钟的增长，我们也没办法重置逻辑时钟部分的值。
  - 第一版算法凉凉。

- 为了解决这个问题，很自然地想到**把物理时钟和逻辑时钟分开来表示**。
- 我们把HLC分成两部分 l.j 和 c.j。
  - l.j 表示事件 j 发生时所感知到的最大物理时钟值，c.j 是事件 j 的逻辑时钟部分，
  - 当几个事件在同一个物理时钟值内发生时，c 用于记录事件之间的因果关系。
  - pt 依然表示本地NTP协议的物理时钟值。

- 第二版算法

```js
// 👉🏻 part1 初始化：
l.j = 0;
c.j = 0;

// 👉🏻 part2 发送消息事件或者本地事件：
if (pt.j <= l.j) {
  c.j = c.j + 1
} else {
  // 💡 若本地物理时钟大，则更新本地时间戳+重置counter
  l.j = pt.j;
  c.j = 0;
}

// 👉🏻 part3 接收m消息事件：
if (l.j == l.m == pt.j) {
  // 如果j事件,m消息和本地物理时钟的值相同，增加逻辑时钟部分
  c.j = max(c.j, c.m) + 1
} else if (pt.j <= l.j and l.m <= l.j) {
  // 如果本地物理时钟没赶上HLC的物理时钟，并且j事件的逻辑时钟更大，更新逻辑时钟的值
  c.j = c.j + 1
} else if (pt.j <= l.m and l.j <= l.m) {
  // 如果本地物理时钟没赶上HLC的物理时钟，并且m消息的逻辑时钟更大，更新HLC的逻辑时钟部分和物理时钟部分
  c.j = c.m + 1;
  l.j = l.m;
}
// 💡 若本地物理时钟大，则更新时间戳+重置counter
else {
  l.j = pt.j;
  c.j = 0;
}
```

- 新算法执行的过程中，本地时钟的值通过NTP协议更新，HLC的值并不会修改本地时钟的值。
  - 由于分离了物理时钟和逻辑时钟，新的事件发生时，如果物理时钟部分的值没增长，就只增加逻辑时钟部分的值。
  - 如果本地的物理时钟赶上了HLC的物理时钟部分的值 l.j，就可以重置逻辑时钟部分的值 `c.j = 0`，并把 l.j 更新为新的本地物理时钟。
  - 这样就可以解决第一版算法中HLC无限增长的问题，也满足了性质3和性质4的要求。
- 对于任何一个事件 j，pt.j <= l.j，也即HLC的物理时间戳部分的值一定大于等于本地NTP的时钟值。
  - 假设整个分布式系统中，NTP协议的时钟误差值为 ε。新算法中，对于任何一个事件 j，| l.j - pt.j | <= ε，也就是HLC物理部分的值和本地物理时钟值的差距不会超过 ε。
- 工程实现上，HLC可以设置成64比特的整数，高位48比特是以毫秒为单位的物理时间。低位16比特是一个单调增长的整数，最大65535。整体结构有点像雪花算法生成的唯一ID。

- 如果某个节点的NTP物理时钟值出现了异常，比如变成一个极大的值，其他节点收到这个故障节点的消息，会导致其他节点的HLC值出现问题。
  - 为了阻止故障的扩散，可以设置HLC物理部分偏差的上限，
  - **如果收到的消息物理部分值的偏差超过上限，忽略这条消息**，同时发送告警等待人工处理。

- HLC可以用于分布式数据库一致性快照读的处理中。很多系统中都使用了HLC，比如HBase和CockRoachDB。
  - CockRoachDB在分布式事务中使用了HLC。根据HLC的性质4，| l.e - pt.e |的值会小于一定的范围 MaxOffset，CockRoachDB默认这个值为500毫秒，pt.e + MaxOffset一定是系统中最大的物理时间。
  - 启动事务时会获取本地的HLC值 hlc.e，并且确定一个区间 [ hlc.e, hlc.e + MaxOffset ]，然后发往其他节点执行快照读

### [计算机的时钟（一）：NTP协议 - Yang Blog](http://yang.observer/2020/07/11/time-ntp/)

- 假如隔了好几天打开你的电脑，任务栏的时间依然是显示正确的，即使你的电脑没有联网，这是如何做到的？
  - 计算机的主板上有一个石英晶体振荡器和一个纽扣电池。石英晶体振荡器的频率是32768Hz每秒。在通电的时候，石英晶体每振动32768次，电路就会传出信息，表示1秒钟到了，通过这种方式来记录时间。
  - 但是石英晶体会有误差，正常情况下，每天的计时误差在正负1秒钟。而且在极端温度下，比如零下二十度，误差会变大。
- 正是因为石英晶体误差比较大，所以1985年特拉华大学的David L. Mills设计了网络时间协议NTP（Network Time Protocol）来同步不同计算机系统之间的时钟。
- NTP协议的目标是将所有计算机的时间同步到几毫秒误差内。
  - NTP协议是一种主从式架构协议，使用分层的时钟源系统，每一层称为Stratum
- NTP协议使用UDP协议来传输，端口为123
- NTP协议在广域网可以达到几十毫秒的误差，局域网误差可以在1毫米内。
  - 误差最大的一个原因是发送请求和接收响应这两个阶段的网络时间可能是不一样的。

### [计算机的时钟（二）：Lamport逻辑时钟](http://yang.observer/2020/07/26/time-lamport-logical-time/)

- 在分布式系统中，如何确定不同机器上的两个事件发生的先后顺序呢？
  - NTP协议存在误差，所以不能通过不同机器上的本地时间来确定顺序，Lamport逻辑时钟是解决这个问题的方法之一
- 为什么分布式系统需要知道两个事件的先后顺序
  - 举个例子：分布式数据库中不同事务并发执行的时候，需要做事务隔离。
  - 隔离的一种做法是使用MVCC(Multiple Version Concurrent Control)多版本并发控制，根据数据的版本号来控制该版本数据的可见性。
  - 这时候就需要知道数据修改事件发生的先后顺序才能正确的实现隔离性。
- 偏序的意思是说集合中的元素是部分有序的，而全序的意思是集合中任意一对元素都是可以相互比较的，可以完全排序。
  - 自然数的集合是全序。
  - 复数的集合是偏序，1和100i是无法比较的，没有意义。
- 对于分布式系统来说，我们想知道事件的先后顺序，实际上就是希望创建一种全序的关系来描述事件的顺序。

- 👉🏻 既然物理时钟不可靠，那就人为构造一个递增的序列来为事件排序，这就是Lamport逻辑时钟的基本思想。
- 首先需要定义先后关系(happened before)，我把事件 a 发生在 b 之前定义为 `a → b`。
  - 如果a和b没有先后关系，则称两个事件是并发的，记作 `a || b`。
- `a → b` 除了可以表示两个事件的先后关系，也**可以理解为两个事件的因果关系**，a事件导致了b事件的发生，或者说a事件影响了b事件，
  - 而 `a || b` 也可以理解成两个事件没有因果关系
- 我们引入逻辑时钟算法： 分布式系统中每个进程Pi保存一个本地逻辑时钟值Ci，Ci (a) 表示进程Pi发生事件a时的逻辑时钟值，Ci的更新算法
  - 进程Pi每发生一次事件，Ci加1。
  - 进程Pi给进程Pj发送消息，需要带上自己的本地逻辑时钟Ci。
  - **进程Pj接收消息，更新Cj**为 `max(Ci, Cj) + 1`。
- 从以上算法可以很容易地得出下面两个结论：
  - 同一个进程内的两个事件a和b，如果 a → b，那么 Ci (a) < Ci (b)。
  - a是Pi进程的消息发送事件，b是Pj进程该消息的接收事件，那么 Ci (a) < Cj (b)。
  - 总结，对于任意两个事件a和b，如果 `a → b`，那么 `C (a) < C (b)`。
- 如果 `C (a) < C (b)`，那么可以得出 `a → b` 吗？
  - 答案是不能，举个反例，图二中C (e) = 2，C (d) = 3，虽然 C (e) < C (d)，但并不能得出 e → d

- 上文介绍的逻辑时钟算法构造的整个事件集合 (happened before →) 是一种偏序关系，只有部分事件可以比较大小。
  - 我们加入另外一个条件也就是**判断两个进程号的大小**，可以使整个事件集合变成一种全序关系。
- 定义全序关系 ⇒ 如下：Pi进程的事件a和Pj进程的事件b如果满足下面两个关系中的任何一个，则称 a ⇒ b。
  - Ci (a) < Cj (b)
  - Ci (a) = Cj (b) 并且 Pi < Pj。
  - 全序关系 ⇒ 把偏序关系 → 变成了任何两个元素都可比较的全序关系，而且有 a → b，则 a ⇒ b。
  - 注意即使物理时间上e发生于d之后，但由于两个事件并没有因果关系，所以排序时没有按照物理时间顺序也不会有问题。
- 全序关系 ⇒ 有什么用呢？在论文中，Lamport老爷子举了一个分布式锁的例子来描述 ⇒ 的作用。

- 👉🏻 全序关系 ⇒ 可以为系统中所有事件排序，但是**系统外的事件却可能破坏这种关系**，导致异常行为。
- 外部事件，我们的分布式系统并不能感知到这个外部事件。
- 解决这个问题有两个方法：
  - 第一种方法是给外部事件也加上分布式系统的时钟，比如上面例子中，a事件的逻辑时钟是Ta，给上海朋友电话时，带上Ta，然后上海朋友提交b请求时带上晚于Ta的时钟。
  - 第二种方法是引入物理时钟，这种方法和Google Spanner的TrueTime很类似，后面介绍TrueTime的时候再介绍这种方法。

### [计算机的时钟（三）：向量时钟](https://yang.observer/2020/09/12/vector-clock/)

- 在《计算机的时钟（二）：Lamport逻辑时钟》中，我们介绍过对于任意两个事件a和b，如果 a → b，那么 C (a) < C (b)，但是反向并不成立，C(a) < C(b)推不出来a→b。
  - 本文介绍的向量时钟(Vector Clocks)可以保证反向也能成立
  - Lamport逻辑时钟存在的问题是不能描述事件的因果关系，C(a) < C(b)不能推导出a → b，这样导致即使知道了两个逻辑时钟值，但却不能确定这两个事件的因果关系。
- **向量时钟的思想**是进程间通信的时候，不仅同步本进程的时钟值，还同步自己知道的其他进程的时钟值。

- 分布式系统中每个进程Pi保存一个本地逻辑时钟向量值VCi，向量的长度是分布式系统中进程的总个数。
- VCi (j) 表示进程Pi知道的进程Pj的本地逻辑时钟值，VCi的更新算法如下：
  - 初始化VCi的值全为0：VCi = [0, … , 0]
  - 进程Pi每发生一次事件，VCi[i]加1。
  - 进程Pi给进程Pj发送消息，需要带上自己的向量时钟VCi。
  - 进程Pj接收消息，需要做两步操作。
    - 对于VCj向量中的每个值VCj[k]，更新为 max (VCi[k], VCj[k])。
    - 将VCj中自己对应的时钟值加1，即VCj[j]加1。

- 向量时钟里的向量是一种偏序关系
  - 同一个进程内的两个事件a和b，如果 a → b，那么 VCi (a) < VCi (b)。
  - a是Pi进程的消息发送事件，b是Pj进程该消息的接收事件，那么 VCi (a) < VCj (b)。
  - 对于任意两个事件a和b，如果 a → b，那么 VC (a) < VC (b)。
  - 根据进程内的算法逻辑性和传递性，也很容易得出结论
  - VCa < VCb 推导出 a → b 得证。
- 向量时钟将Lamport逻辑时钟的全序时钟值改成了向量时钟的偏序关系，可以准确刻画事件的顺序，

- 向量时钟有什么作用呢？
- 作用之一是检测数据冲突。分布式数据库中数据存在多个副本，每个副本都可能提供写操作，如果两个副本都对同一个数据进行写操作，就可能造成冲突，向量时钟可以检测这种冲突，但不能解决冲突。
- 作用之二是确定事件间的因果关系。

#### [分布式系统：向量时钟 vector clock](https://blog.xiaohansong.com/vertor-clock.html)

- 本文中的因果关系指的是时序关系，即时间的前后，并不是逻辑上的原因和结果
  - 本文中提及的时间戳如无特别说明，都指的是逻辑时钟的时间戳，不是物理时钟的时间戳
- Lamport 逻辑时钟帮助我们得到了分布式系统中的事件全序关系，但是对于同时发生的关系却不能很好的描述，导致无法描述事件的因果关系。
  - Lamport 逻辑时钟算法，它提供了一种判断分布式系统中事件全序关系的方法：如果 a -> b，那么 C(a) < C(b)，但是 C(a) < C(b) 并不能说明 a -> b。也就是说C(a) < C(b) 是 a -> b 的必要不充分条件，我们不能通过 Lamport 时间戳对事件 a、b 的因果关系进行判断。
  - Lamport 逻辑时钟算法中每个进程只拥有自己的本地时间，没有其他进程的时间，导致无法描述事件的因果关系。
- 向量时钟是在 Lamport 时间戳基础上演进的另一种逻辑时钟方法，它通过向量结构不但记录本节点的 Lamport 时间戳，同时也记录了其他节点的 Lamport 时间戳，因此能够很好描述同时发生关系以及事件的因果关系。

### [计算机的时钟（四）：TrueTime - Yang Blog](http://yang.observer/2020/11/02/true-time/)

- 由于广域网的复杂网络状况，NTP误差可能在100毫秒级别，这么大的误差显然是不适合一些精确度要求高的应用，
  - 一种办法是抛弃物理时钟，使用逻辑时钟解决物理时钟不可靠的问题。
  - 另外一种办法是努力提高物理时钟的精度，将误差降到可以接受的范围。Google设计的TrueTime就是这种方案的代表。
- TrueTime由Google于2012年提出，用于Google的全球范围部署的数据库Spanner。
  - TrueTime由时钟硬件和算法组成。
  - 其中时钟硬件由GPS时钟和原子钟组成。
  - 之所以使用这两种硬件的原因是因为这两种硬件的故障原因不一样，这样可以提高时钟的可靠性。
  - GPS时钟故障的原因有天线和接收器故障，无线信号干扰等。
  - 原子钟可能由于频率问题造成时钟漂移。
  - 这两种原因是不相交的，所以能提高整个硬件的可靠性。整个硬件的成本并不贵，淘宝上原子钟的价格从几千到几万都有。
- 每个数据中心有若干个time master机器。大部分time master机器安装了GPS天线和接收器。剩下的time master机器安装了原子钟。
  - time master之间会相互校验时间，如果某个time master发现自己的本地时间和其他time master相比差异很大，会把自己设置为离线，停止工作。
  - 客户端向多个time master查询，防止某个time master出现故障影响结果。
- 即使使用了GPS时钟和原子钟，也不能保证时钟0误差。2012年Spanner论文发表时，时钟的误差范围 ε 是1ms到7ms，平均4ms。前面我们介绍过NTP的误差在100ms级别，TrueTime的误差相比NTP大大减少了。

- 使用TrueTime API时，需要搭配下面两个规则。
  - Start： 提交事务Ti时，leader必须选择一个大于等于TT.now().latest的时间作为提交时间戳si。
  - Commit Wait： leader必须等待TT.after(si)为true后才能提交数据，也即必须等待si的绝对时间过去了才能提交数据。
- 使用这两个规则可以保证：如果事务 T1 提交后 T2 才开始，那么 T2 的提交时间一定晚于 T1 的提交时间。也就是说事务的提交顺序一定和事务发生的绝对时间上的顺序一致。

- Google Spanner中，对同一个数据进行修改时，需要加锁，TrueTime相当于是把所有并发操作串行化，进行排队。
  - 由于TrueTime的误差在1到7ms之间，平均误差4ms。一次事务需要等待两个 ε，一个是选择提交时间时需要等待TT.now().latest，另外一个是提交数据时需要等待TT.after(s)，平均需要等待8ms。
  - 也就是说对于同一个数据的写事务，Spanner并发量是每秒125个。这是论文发表时的数据，论文中也写到未来希望把误差 ε 降低到1ms。
- We believe it is better to have application programmers deal with performance problems due to overuse of transactions as bottlenecks arise, rather than always coding around the lack of transactions.

### [Distributed Clocks and CRDTs – Adam Wulf](https://adamwulf.me/2021/05/distributed-clocks-and-crdts/)

### more-blogs

# examples

## hlc

- verdant/lo-fi /7Star/MIT/202211/ts/indexeddb
  - https://github.com/a-type/verdant
  - https://github.com/a-type/lo-fi
  - https://verdant.dev/
  - An IndexedDB-powered database and data sync solution for lightweight, local-first web apps.
  - server依赖sqlite、jwt、ws
  - 基于hybrid-logical-clock

- https://github.com/quolpr/harika /ts/hlc/不依赖merkle
  - offline-first, performance-focused note taking app.
  - Synchronization with server. It's done with LWW CRDT per field on top of SQLite
  - using absurd-sql for web version
  - It uses LWW per field CRDT and stores all changes on the server, so time travel is possible to implement.
  - https://twitter.com/quolpr/status/1558848201771319298

- IDBSideSync /8Star/MIT/202104/ts
  - https://github.com/clintharris/IDBSideSync
  - https://idbsidesync-todo-demo.vercel.app/
  - IDBSideSync is an experimental JavaScript library that makes it possible to sync browser-based IndexedDB databases using CRDT concepts

- https://github.com/andymatuschak/orbit/blob/master/packages/backend/src/db/orderedID.ts
  - an experimental platform for publishing and engaging with small tasks repeatedly over time
  - [Project: data architecture improvements](https://github.com/andymatuschak/orbit/issues/192)
    - The salted HLC does seem to be fine for the purposes of our stable listing contracts

- https://github.com/jaredly/hybrid-logical-clocks-example /js
  - https://hybrid-logical-clocks-example.surge.sh/
  - [Hybrid Logical Clocks | Jared Forsyth](https://jaredforsyth.com/posts/hybrid-logical-clocks/)

- https://github.com/jaredly/local-first/tree/master/packages/text-crdt
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.
  - Your approach seems to resemble RGASplit which I believe is bases for
  - Hybric Logical Clocks was very much based on [this go implementation] and [james long's demo]

- https://github.com/daaku/kombat /ts/hlc+merkle-tree
  - Infrastructure for CRDT powered applications.
  - Timestamp for Hybrid Logical Clocks.
- https://github.com/etienne-graveyard/kiip /ts/merkle/inactive
  - An offline-first database (using Hybrid Logical Clock & Merkle Tree)

- https://github.com/Mirror-Labs/MirrorDB /ts/wip
  - An application-centric p2p database with super powers
  - Hybrid Logical Clock (HLC) to track the order of events in a distributed system.
  - Not thread safe. (does not matter in browsers!)

- https://github.com/cmdo-toolkit/events /ts/inactive
  - A distributed event sourcing solution written in TypeScript.
  - Logical hybrid clock timestamp representing the wall time when the event was created.
  - https://github.com/cmdo-toolkit/react-starter
    - A full stack cmdo boilerplate for react.js, node.js and typescript
    - 全家桶架构: client-db + store + api
  - https://github.com/cmdo-toolkit/db
    - Client side database solution written in TypeScript.
    - 依赖mingo(MongoDB query language for in-memory objects)
  - https://github.com/valkyrjs/valkyr /ts
    - toolkit for creating event sourced applications using javascript/typescript.

- https://github.com/iam-kevin/papai /4Star/MIT/202206/ts/wip
  - Local-first storage adapter for JSON-modeled data. 
  - Intended to work with self store implementation
  - Papai is storage provider intended for Local-first use with support for distributed storage implementation.
  - With ever-growing implementations for different storage options like localStorage, AsyncStorage, level, IndexedDB, WebSQL, Papai makes it possible to use the same interface attached to different storage options, leaving you concerned with building the business side of your applications.
  - 基于HybridLogicalClock和State-based CRDTs
  - examples
    - https://github.com/Elsa-Health/mammoth
    - https://github.com/Elsa-Health/ctc-impl

- https://github.com/Mookiies/crdt-exploration-frontend
  - 基于HybridLogicalClock
  - https://github.com/Mookiies/crdt-exploration /ruby/backend

- https://github.com/theproductiveprogrammer/hybrid-logical-clock /js
  - A Hybrid Logical Clock is a resilient and simple distributed clock that provides the ability for identity and ordering of messages in a distributed system.

- https://github.com/atolab/uhlc-rs /rust
  - This library is an implementation of an Hybrid Logical Clock (HLC) associated to a unique identifier. 
  - Thus, it is able to generate timestamps that are unique across a distributed system, without the need of a centralized time source.

## vector-clock

- https://github.com/jlongster/crdt-example-app /201912/js
  - https://crdt.jlongster.com/client/
  - https://github.com/clintharris/crdt-example-app_annotated
  - A full implementation of CRDTs using hybrid logical clocks and a demo app that uses it

- https://github.com/MattLloyd101/ts-vector-clock
  - A Typescript Vector Clock implementation
# impl-consento-hlc
- https://github.com/consento-org/hlc /js
  - a Hybrid Logical Clock implementation in JavaScript. 
  - It is comparable to CockroachDB's implementation. 
    - It creates Timestamps with a nanosecond WallClock (using bigint-time) that supports de-/encoding to fixed size **96bit** Uint8Arrays (compatible with codecs) or JSON object.
  - 依赖biginit-time、longfn
  - https://github.com/rjmackay/vue-todo-kappa-db
    - A Todo PWA using KappaDB and Hypercore for syncing data. 
    - Built with Vue 3 + Vuex + Bootstrap 5.

- The basic of HLC's is that you call .now() multiple times and it will always increment the timestamp, no matter if the .wallTime (the time of the OS) changed not not. This means that two calls will not never the same timestamps after another.

- This is a powerful feature because using HLC's means every document/item will have a unique (per node), sortable timestamp, always!
  - This means that using HLC's you can use timestamps as keys in a single-node system!
- By processing every timestamp we know, we can make sure that the order of nodes is only in question between sync operations!

- Don't use them in hostile environments. HLC's have limited number space and a hostile party could create timestamps that exhaust the given number space. 

- 👉🏻 As the timestamps are sorted only after sync we need node IDs as tie-breaks to deal with the disarray between the sync operations (merge-operation). 
  - Some applications have an easy time with this task automatically, others need manual ordering. For ordering by hand, HLC's may not help.
- HLC's are also not that good for human readability. 
  - The timestamp itself has 96bits and - as mentioned above - node ID's may come into play. 
  - So humans may have to deal with very large numbers or strings which are not that good for short urls or to tell someone over the telephone.

- 💡 Why HLC timestamps are not unique?
- Without syncing or progresses in the wallTime, naturally node1 and node2 produce the same, non-unique timestamps consistently.
  - As you can see all of the node's logical counters increased even though the wallTime didn't making the timestamps unique only per node
  - In practice, time advances which means that two timestamps would need to be created within < 1 nanosecond of time, which is very unlikely.

- The strength of HLC's is revealed when a sync happens.

- Why don't we sync the wallTime?
  - It is a good idea to do that, particularly to reduce the chance of duplicates and it may make a little more sense for users. However, you need to be careful when offsets to the wallTime don't compound(达成协议；同意).
  - In the previous examples, the time for all nodes advanced at the same pace. But in reality it does not. Each node increments at slightly different paces. 
  - This will lead to clocks automatically drifting little by little into the future.

- Synching wallTime will reduce the probability for a non-unique timestamp drastically, but even so it is still possible to have non-unique timestamps: Two nodes that happen to have the same wallTime and logical time.

- 💡 Why the HLC is implemented in 96bits?
- Other HLC implementations use 64bits by combining the logical component with the wallTime. You can do this using the algorithm presented in here as well
- The problem with using 64bits occurs when we reach the end of the number space. 
  - The 64bit number space is not limited and the largest timestamp that we have is 18446744073709552000 (or 0xFFFFFFFFFFFFFFFF). 
  - If this number is exceeded you simply can not increase the timestamp anymore.
- Note how the 64bit representation overflowed! This is the natural limitation of nanosecond numbers as 64bit numbers.

- 💡 why not variable length timestamps?
- to get an unlimited timestamp it does open yet another attack vector. 
  - BigInt numbers can grow to any size practically limited to your systems memory/disc-space.
- Here you can see that the binary representation never exceeds the 96bit limit but the JSON representation does so by a lot. 
  - An attacker could use this to break your system by providing a very large timestamp and every subsequent timestamp would need to be even larger.
# more

# discuss-hlc

- ## 

- ## 

- ## UUIDv7 高位自带了时间戳
- https://twitter.com/fuyufjh/status/1710500237788459100
  - UUIDv7 is a time-ordered UUID which encodes a Unix timestamp with millisecond precision in the most significant 48 bits. 
- 48bits 的时间戳相比 snowflake 已经很够用了，等后续数据库的支持，大部分不需要向用户暴露ID的服务用起来就很方便。
- snowflake 要统一分配 node_id，很劝退
  - 对，这玩意很麻烦为 worker_id 单独搞 zookeeper 也很浪费。

- 所以 UUID 用在分布式系统中到底靠谱吗 
- 感觉直接拿来做 PK 挺好的
- pros: 
  1. 不用像 snowflake 一样维护分配 node_id
  2. 大致是自增，对于大多数 DB 都更友好
  3. 长度 128bit 相比很多文本的key（比如X宝的订单号）已经好太多了
- cons:
  1. UUID类型在语言上的支持远不如 int64 和 string
  2. 打印出来还是有点长，不如自增  id

- v1 高位也有时间戳，不过最高位是时间戳的低位；做个变换弄个私有varaint也能将就一下
  - 私有的方案一大堆，这下有个通用的，可喜可贺
