---
title: lib-db-app-community-mvcc-concurrency
tags: [community, concurrency, database-design, mvcc]
created: 2023-11-01T10:14:25.622Z
modified: 2023-11-01T10:15:06.245Z
---

# lib-db-app-community-mvcc-concurrency

# guide

- [高并发系统设计 40 问 | JAVA 架构师笔记](https://zq99299.github.io/note-architect/hc/)
# discuss-stars
- ## 

- ## 

- ## 
# discuss-transactions
- ## 

- ## 💡 How do atomic transactions work in a database?
- https://twitter.com/Franc0Fernand0/status/1759563991540494663
- Atomicity makes it possible for a transaction to have only 2 results:
  - it successfully executes all the operations and commit
  - it aborts because of a failure and undoes all the changes
- In a single database, atomicity is possible by saving all the changes to the data in a write-ahead log (WAL).
  - Every time changes are made, the WAL saves them on the disk so that they will last.
  - Each entry of the WAL contains all the information to undo all the changes.
- However, the WAL approach is insufficient if the transaction involves more than one database. 
  - In these situations, the two-phase commit protocol (2PC) is often used. 
  - The protocol says that one process should be the coordinator and the others should be participants.
  - Most of the time, the coordinator is the client process that requires the transaction.
- 2PC protocol has 2 steps:
- 1. Prepare
  - The coordinator requests everyone to get ready to complete the transaction. Each participant answers if they can commit or not. 
  - After answering, the participants wait for further instructions.
- 2. Commit
  - If all participants are ready, the coordinator sends them a commit request. Otherwise, it will ask to abort.
  - This step is a point of no return: the transaction has to be committed or aborted.
- The 2PC protocol works but has some drawbacks: 
  - it's slow since it requires multiple round trips between the processes
  - it gets blocked if the coordinator fails or a participant fails in the commit step
- Replicating the involved processes makes 2PC more robust but adds complexity.

- ## Relies on a global logical clock and claims that an MVCC visibility check can be as simple as an integer comparison. 
- https://twitter.com/sunbains/status/1757617183218442588
  - Order transaction on their “recentness” which speeds up GC.
- Would love to see a comparison to LMDB, as its the best one(currently) in terms of random read perf.

- ## What is a Transaction
- https://twitter.com/DominikTornow/status/1759623957291147331
  - A transaction is a sequence of a read or a write of a data object that ends in exactly one commit or exactly one abort.

- ## What are transactions in a database?
- https://twitter.com/Franc0Fernand0/status/1754422259869974682
  - Transactions are a way for databases to group a set of operations into one.
  - This is helpful in many ways and simplifies the programming model at the application level.
  - In a single relational database, transactions make sure that the following ACID conditions are met

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🌵 Are there databases which let you continue the execution of a transaction on connection failures or machine restarts? 
- https://x.com/iavins/status/1801450141993628092
  - Why don’t databases support such a feature?
- This is doable once your client-commit is entirely optimistic. My stuff does this, so it supports what you're asking for without actively doing it.
- WAL integrity checks might be able to do this fr

- Such a design would imply in-memory transaction state actually gets persisted somewhere. Git is an example of a “database” that does this, in the form of branches. @DoltHub extends the idea to a proper structured database. A branch is just a long-lived transaction.

- Technically such databases exist: Git or really any DVCS.
  - The idea requires 2 assumptions to make them feasible:
  1. Outdated reads are acceptable.
  2. Transactions don't rollback on write conflicts.
  - Apply to CRDTs and local-first systems - but few of them support transactions.

- FWIW, I’ve seen this implemented in a proprietary database that I worked on. It used an optimistic commit protocol. It worked just fine, there is technical barrier.
  - There is “no technical barrier”, it’s just that people are more used to pessimistic commit and therefore see everything through that lens.
  - The problem is on the db side, not about whether the client’s operation completed on the db or not. The latter is easy to resolve by rollback by default. The real problem is that the db can’t tell if the client will retry or resume. The db can’t keep holding resources on behalf of the client forever. There is usually timeout mechanism before the db will release any resources that were held on behalf of the client.
- A distributed database can do this partially, if a storage node goes down. A query that needs data from that node will retry from the new leader. Not the same thing exactly but at least in spirit. If a client fails over to another node because of a SQL node crash, XA IIRC does support this for transactions that are in XA Prepared state.

- Oracle has this feature - called Application Continuity. Client-side logic adds a lot here.
- Oracle RAC has transparent application failover since 2017 and application continuity but it seems too much money for avoiding optimizing application code making it re-run friendly.

- Very interesting question. The whole Distributed SQL was invented because we didn't want to solve this problem. But if we go back to on Prem database days, Tandem used to sell "bulletproof" DBs back in the day. Let me check if their architecture supported such failures

- One argument against building out such a feature in the distributed database or as some proxy layer on top of it is that its as or more likely that the code running the transaction dies. The system needs to do something reasonable in that case too.
  - If there’s way more db nodes, then the complexity might be worth it. But how do you even recover? Ideally the client recover, but getting db client drivers to be more sophisticated is hard work. Low risk tolerance, legacy code and many langs.
  - If an http-based, request-response oriented protocol sat underneath your sql drivers, then maybe you’d see more such recovery protocols built into transaction protocols. Tl; dr to do it right it’s probably gotta be in the driver, and that’s a hard place to innovate
- For many distributed databases, you won’t see a failure unless the transaction coordinator node dies. It’d be unreasonable if any node dying lead to all transactions failing, but it’s hard to do better than that and it’s arguably not so bad given the app can die too.

- To get good performance, transactions (both read-only and read-write) must "flow".  They need to be "short" (time-wise) and "small" (data-wise).  With this in mind, failing-fast is a better option than allowing "resumable" transactions. 
  - There might be use-case for "resumable" transactions, but to me, and with the information I have, this is not a feature I would invest much in

- Not the full support but Redshift with scheduling queries does something similar. You can schedule query have a event bridge and then use that to get the query execution status.

- ## Here's a new post walking through an implementation of MVCC and major SQL transaction isolation levels, in 400 lines of Go code.
- https://x.com/eatonphil/status/1791225675287867742
  - These ideas might sound esoteric, but they impact almost every developer using any database.
  - [Implementing MVCC and major SQL transaction isolation levels | notes.eatonphil.com](https://notes.eatonphil.com/2024-05-16-mvcc.html)
- Why do we set all the visible versions as deleted when using “set” and “delete”? The mvcc implementations I saw usually only modify the most recent value.
  - It's a good question. I'm not sure! I decided until I knew for sure it was best to mark them all.

- ## Are there any databases which do MVCC at page level granularity and have multi writer concurrency? Or any research papers on the same?
- https://twitter.com/iavins/status/1775532839179633076
  - Only one I know is SQLite's `BEGIN CONCURRENT` (alpha) feature
- SQLite also does single writer MVCC with pages.. but I am interested in learning more about multiple writers.

- I don’t understand the question. MVCC is usually associated with transactions and the versions are usually of rows (don’t have to be). A page can be made up of many rows and versions of these rows from many different transactions. Some active and some completed or rolled back. Note rollback doesn’t imply that the changes are undone. The changes are “invisible”, that’s the job of the MVCC.
- AFAIK, Oracle uses row versioning for MVCC, InnoDB copies that design.
- It’s still row version based. The head of the row version list is in the block. That’s all. It makes no sense to log both blocks and row versions. 
- Postgres stores the versions in the table and that’s why vacuum is a pain.

- ## 🆚️ Trying to get a sense for thread architectures:
- https://twitter.com/eatonphil/status/1773518000043299309
- Single-threaded: Cache-friendly and scales decently if you use some form of async io. Good for tasks with little-to-medium CPU-work since cache won't get busted. i.e. works fine with shared data between tasks. Too much CPU-work though limits your ability to scale.
- Work-stealing & work-sharing: Cache-unfriendly, works fine with sync or async io, since cache is core-local and work-switching threads (to another core) thus busts the cache/makes it ineffective. Fine for tasks with little CPU-work where cache doesn't matter as much. Scales well for little CPU-work tasks.
- Thread-per-core: Cache-friendly so long as work is independent, works fine with sync or async io. Scales best among all options for small or large CPU-work. Even if there is shared data, still probably scales better than work-stealing/sharing and single-thread.
- Multi-process: Basically the same as thread-per-core, if processes are 1:1 with cores?

- cache is not important compared to blocking IO(disk>network) wait, which is the origins async-io is used for. But concurrent programming includes the threading/cache thing, while the `concurrent` concept covers the syntax sugar async/await.

- Thread-per-core with blocking I/O is going to end up leaving lots of cores idle so you pretty much have to use async. I wonder if the cache friendliness/unfriendliness has ever been measured or if it's propaganda. Sadly, results are going to be different between Intel & AMD.

- If you want to build intuition, think about how you are mapping hardware resources (CPU and memory) to your application logic and state.

- ## If you are interested in exploring Race Conditions & Data Races, I recommend Testing for Race Conditions via SMT Solving
- https://twitter.com/DominikTornow/status/1758921755807437258

- ## The diagram below explains what ACID means in the context of a database transaction.
- https://twitter.com/alexxubyte/status/1732783270855876654

- ## 🏘️ When Uber created their in-house database (known as Schemaless), they wanted high-availability writes.
- https://twitter.com/ProgressiveCod2/status/1726136613468852376
  - This was difficult to achieve because all writes in their setup went to the Leader node.
  - And if the Leader node goes down, HA becomes difficult to achieve.
  - To get around this issue, Uber used a technique known as Buffered Writes.
  - Buffered Writes meant that every write request was stored on at least two nodes: - The Primary Leader - The Secondary Leader
  - But there's a lot that goes behind the scenes to make the whole thing work
  - [PC#16 - The Secret Trick to High-Availability_202310](https://progressivecoder.beehiiv.com/p/the-secret-trick-to-high-availability)

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
