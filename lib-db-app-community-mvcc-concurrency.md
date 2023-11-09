---
title: lib-db-app-community-mvcc-concurrency
tags: [community, concurrency, database-design, mvcc]
created: 2023-11-01T10:14:25.622Z
modified: 2023-11-01T10:15:06.245Z
---

# lib-db-app-community-mvcc-concurrency

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Cool thread-safe triple buffering approach made lock-free by atomically swapping the pointers to the buffers
- https://twitter.com/zack_overflow/status/1722275195594133817
  - Thinking about using this for my code editor when I add LSP support
  - The main render thread needs to get data from the second thread which manages the LSP server process

- ## 今年 gopher 大会上的分享：Building a Highly Concurrent Cache in Go: A Hitchhiker's Guide
- https://twitter.com/kscooooo/status/1719976363166498889
- LRU、LFU 都简单过了一下，还有俩者的结合 LRFU (Least Recently/Least Frequently) ，工作原理类似于 LFU，每个项都持有一个值，叫 CRF(Combined Recency and Frequency)，通过一个参数 λ 来决定对最近 entry 的权重。
  - 然后着重介绍了 DLFU (Decaying Least Frequently Used)，是 LFU 的变体，随着时间的推移，entry 的访问计数会衰减。对比 LFU 会把长期不用的热门 entry 干掉。
- 其次就是老生常谈的伪共享。伪共享就是多个 cpu 访问了一个 cache line 上不同的变量，一个 cpu 修改了那么其他的 cpu 的缓存就失效了，就得走 cpu 同步的协议(mesi)，这个就慢了。
  - 如果设计的数据结构比如像 struct 的俩成员都会修改的话，就空间换时间，给这俩成员变量中间塞无用字节把位置给占了，让这俩成员变量在不同的 cache line 上。这样多核 cpu 修改各自的成员变量最大程度就避免了 mesi 这种同步。
- xsync. Map 我之前看到过，是 java 写的那个时序数据库 QuestDb 主程写的并发库，核心思想就是数据结构基于 CLHT(Cache-Line Hash Table) 设计的，跟原生的 map 和 sync. Map 相比，它的桶是独占 cache line 的，空间换时间。
  - sync. Map 我记得也是空间换时间，但是思路不同，弄了一个 read map 专门并发读，写的话就是往 dirty map 写，然后同步，在 read map 读不到就往 dirty map 里读，key 删的话多个会攒在一起删，细节要多很多。 
  - xsync. Map 就侧重于并发环境下写多的情况。
- 然后就是单独开 goroutine 弄缓存清理，避免阻塞主逻辑。驱逐缓存的过程换了排序算法，不是用的标准库的 pdqsort，用的 quickselect 算法，是线性算法，只对 N 个最小元素进行排序，不对整个数组进行排序。
  - 相当于剪枝了。这个印象还是蛮深刻的，当时在频道里作者讨论的时候，社区里就有人立马回答了这个，当时看到还是觉得妙啊，还是糊 crud 久了基本都是 sort 标准库一把梭。当时 go runtime 的主程 michael 说随机驱逐蛮好的，都不用排序了，作者回复说随机驱逐是蛮好的，还能简化 80% 的实现
- 还有常见原子操作替换锁，这里 go 并发库主程 bryan 当时特意在频道里强调了一个点，如果使用原子操作在每次访问时更新共享变量，其实也不会从原子操作中提到蛮大的提升。原子写入只是将锁定从显式（在代码中)移动到隐式(CPU 缓存一致性协议 mesi)，还是最后会碰到锁定 cache line 产生竞争。
- 所以大部分篇幅都是强调伪共享、cpu 缓存一致性协议。
  - 其他的技巧有每次操作记得有超时兜底，缓存操作时记得要及时检查 ctx，超时了就立马释放锁返回。
  - 写好 go bench(RunParallel) 、善用 pprof、benchstat 对比新旧 bench 的实现等。然后差不多就没了
- 结合了社区频道的讨论和 ppt 的总结，视频今年 gopher 大会还没放出来，总体比较简单，都是社区老生常谈的。做个笔记方便自己
