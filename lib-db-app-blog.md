---
title: lib-db-app-blog
tags: [blog, database]
created: 2022-12-20T05:38:59.782Z
modified: 2023-09-16T17:49:13.534Z
---

# lib-db-app-blog

# guide

- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
  - ranks database management systems according to their popularity. The ranking is updated monthly.
# blogs

## [数据库计算向量化 | plantegg](https://plantegg.github.io/2021/11/26/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%A1%E7%AE%97%E5%90%91%E9%87%8F%E5%8C%96/)

- 在做向量化之前数据库一直用的是volcano模型来处理SQL
- volcano火山模型
  - 对于如下一条SQL, 数据库会将它解析成一颗树，这棵树每个节点就是一个operator(简单理解就是一个函数，进行一次计算处理)
  - 火山模型实现简单，只需要根据不同的计算提供一堆算子(operator)就可以了，然后根据不同的SQL只需要将operator进行组装（类似搭积木一样），就能得到一个递归调用结构（火山模型），
  - 每行数据按照这个调用逻辑经过每个operator进行嵌套处理就得到最终结果。
- 火山模型不但实现简单，框架结构性也非常好容易扩展。
- 但是火山模型效率不高:
  - 每个operator拆分必须到最小粒度，导致嵌套调用过多过深；
  - 嵌套都是虚函数无法内联；
  - 这个处理逻辑整体对CPU流水线不友好，CPU希望你不停地给我数据我按一个固定的逻辑(流程)来处理，而不是在不同的算子中间跳来跳去。

- 向量化加速的CPU原理
  - 内存访问比CPU计算慢两个数量级
  - cpu按cache_line从内存取数据，取一个数据和取多个数据代价一样
  - 以及数据局部性原理
- 局部性原理: CPU访问存储器时，无论是存取指令还是存取数据，所访问的存储单元都趋于聚集在一个较小的连续区域中。 

- 向量化执行的思想就是不再像火山模型一样调用一个算子一次处理一行数据，而是一次处理一批数据来均摊开销：
  - 这个开销很明显会因为一次处理一个数据没用利用好cache_line以及局部性原理，导致CPU在切换算子的时候要stall在取数据上，表现出来的结果就是IPC很低，cache miss、branch prediction失败都会增加。
- 向量化之后的版本不再是每次只处理一条数据，而是每次能处理一批数据，而且这种向量化的计算模式在计算过程中也具有更好的数据局部性。
- 向量化核心是利用数据局部性原理，一次取一个和取一批的时延基本是同样的。
  - volcano模型每次都是取一个处理一个，跳转到别的算子；而向量化是取一批处理一批后再跳转。整个过程中最耗时是取数据（访问内存比CPU计算慢两个数量级）
- 如果把向量化计算改成批量化处理应该就好理解多了，但是low，向量化多玄乎啊
- 为了支持这种批量处理数据的需求，CPU设计厂家又搞出了SIMD这种大杀器，SIMD (Single Instruction Multiple Data，单指令多数据)
- SIMD指令的作用是向量化执行(Vectorized Execution)，中文通常翻译成向量化，但是这个词并不是很好，更好的翻译是数组化执行，表示一次指令操作数组中的多个数据，而不是一次处理一个数据；向量则代表有数值和方向，显然在这里的意义用数组更能准确的表达。

## [What is a Vector Database? | Pinecone](https://www.pinecone.io/learn/vector-database/)

### 👥🔥 [What is a Vector Database? (2021) | Hacker News_202305](https://news.ycombinator.com/item?id=35826929)

# blogs-data-model-lsm/btree
- [What is a LSM Tree? - DEV Community](https://dev.to/creativcoder/what-is-a-lsm-tree-3d75)
  - Sled is another embedded key value store in Rust, that uses a hybrid architecture of B+ Trees and LSM Tree (Bw Trees)

- [Bw-Trees](https://sinsay.github.io/db/chapter_6_6_bw_trees.html)
  - Bw-Tree 是 B-Tree 的一个有趣的变种，做了许多重要的优化：写放大，非堵塞的访问以及缓存友好性。一个修改过的实现版本是 Sled，CMU 数据库组织实现了一个基于内存的 Bw-Tree 版本，称为 OpenBw-Tree
# blogs-concepts

## 🧩 [Write amplification - Wikipedia](https://en.wikipedia.org/wiki/Write_amplification)

- Write amplification (WA) is an undesirable phenomenon associated with flash memory and solid-state drives (SSDs) where the actual amount of information physically written to the storage media is a multiple of the logical amount intended to be written.
# more
- [Linearizability versus Serializability | Peter Bailis_201409](http://www.bailis.org/blog/linearizability-versus-serializability/)
  - Linearizability and serializability are both important properties about interleavings of operations in databases and distributed systems, and it’s easy to get them confused.
  - Linearizability: single-operation, single-object, real-time order
    - Linearizability is a guarantee about single operations on single objects. It provides a real-time (i.e., wall-clock) guarantee on the behavior of a set of single operations (often reads and writes) on a single object (e.g., distributed register or data item).
    - Linearizability for read and write operations is synonymous with the term “atomic consistency” and is the “C,” or “consistency,” 
  - Serializability: multi-operation, multi-object, arbitrary total order
    - Serializability is a guarantee about transactions, or groups of one or more operations over one or more objects. 
    - It guarantees that the execution of a set of transactions (usually containing read and write operations) over multiple items is equivalent to some serial execution (total ordering) of the transactions.
    - Serializability is the traditional “I,” or isolation, in ACID.

- [处理海量数据：列式存储综述（存储篇） - 知乎](https://zhuanlan.zhihu.com/p/35622907)

- [Database in the Browser, a Spec](https://stopa.io/post/279)

- [Things DBs Don't Do - But Should](https://www.thenile.dev/blog/things-dbs-dont-do)

- [Database Systems: 8Base, Dolt, MindsDB, Xata – SQL Rob](https://sqlrob.com/2023/04/17/database-systems-8base-dolt-mindsdb-xata/)
  - [15 futuristic databases you’ve never heard of - YouTube](https://www.youtube.com/watch?v=jb2AvF8XzII)
