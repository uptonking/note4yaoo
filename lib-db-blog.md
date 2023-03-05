---
title: lib-db-blog
tags: [blog, database]
created: 2022-12-20T05:38:59.782Z
modified: 2022-12-20T05:39:08.948Z
---

# lib-db-blog

# guide

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
# more
- [处理海量数据：列式存储综述（存储篇） - 知乎](https://zhuanlan.zhihu.com/p/35622907)

- [Using TTL to Manage Data Lifecycles in ClickHouse](https://clickhouse.com/blog/using-ttl-to-manage-data-lifecycles-in-clickhouse?utm_source=twitter&utm_medium=social&utm_campaign=blog)
  - Databases should make it easy to delete stale data, whether to save on storage costs or for compliance reasons.
  - Read about how you can use TTL (time-to-live) clauses in ClickHouse to delete, reset, or compress old data that’s no longer necessary.

- [Database in the Browser, a Spec](https://stopa.io/post/279)
- [A Graph-Based Firebase](https://stopa.io/post/296)
