---
title: lib-db-app-community-data-structure
tags: [b-tree, community, data-structure, database, LSM-Tree]
created: 2023-09-17T17:44:07.206Z
modified: 2023-09-17T18:17:41.377Z
---

# lib-db-app-community-data-structure

> about database internal data structure like btree/lsm/index

# guide
- mysql
- postgresql
  - b-tree index
- sqlite
  - b-tree index
- mongodb
# discuss-stars
- ## 

- ## 

- ## 

- ## 🤔🔥 [Why databases use ordered indexes but programming uses hash tables | Hacker News_201912](https://news.ycombinator.com/item?id=21738802)
- 
- 
- 

- ## 🔥 [Foundations of Databases (1995) | Hacker News_201904](https://news.ycombinator.com/item?id=19726520)
- 
- 
- 

# discuss-tree
- ## 

- ## 

- ## Interested in sorted maps? (Binary Search Trees, AVL Trees, RB Trees, B Trees, etc.)
- https://twitter.com/eatonphil/status/1728890043438395712
- 2-3 trees is all you need, saying as a long AVL follower.

- ## Reading the Adaptive Radix Tree paper - Having the realisation that trie is such an underrated data structure. 
- https://twitter.com/debasishg/status/1725966931830923489
  - Wondering why we should use any other data structure for in memory database indexes.
- Here are some rough notes from the paper ..
- Tree based indexes (e.g. binary search tree or b-tree needs special care for cache friendliness), are expensive for updates and can show pipeline stall(熄火) for branch misprediction.
- Hash based indexes are great for point queries, not so for range queries, are expensive to grow with O(n) complexity for reorganisation.
- Tries have O(k) complexity where k is the size of the key, which means independence from n (that is a HUGE plus). 
  - The trie height can be controlled through the span s of the radix tree and is usually smaller than the height of a binary search tree. 
  - Hence search can be faster - O(k) compared to O(k lg n) in BSTs. 
  - 🛑 One problem with tries is they can have higher space consumption compared to trees. 
  - But Adaptive Radix Tree manages this through variable sized data structures for inner nodes and leaves.
- 🌰 Oh yes, Cassandra recently moved to tries for memtables and SSTables and I wrote about it a few days ago
- That is what @duckdb supports if I’m not mistaken.
- DuckDB has good article on ART and compression.
  - Also, in latest Cassandra release they have Trie based implementation which seems to do better than B Trees, even on storage if I am not wrong. they also have included byte comparable keys to get performance gain on comparisons.
- Here’s an initial impl in Swift as well from FoundationDB team

- https://twitter.com/debasishg/status/1727963715952402658
  - TIL: A persistent version of the Adaptive Radix Tree exists, a map data structure designed for in-memory analytics that supports efficient fine-grained updates without compromising immutability. 

- ## 🌲 [Hierarchical Structures in PostgreSQL (2020) | Hacker News_202106](https://news.ycombinator.com/item?id=27631765)
- A great overview of the pros and cons of different approaches is given in [Models for hierarchical data | PPT](https://www.slideshare.net/billkarwin/models-for-hierarchical-data)

- many RDBMS's have gotten support for recursive CTE's as of recently. It's definitely not a niche(针对特定小群体的) feature anymore.
  - Recursive CTEs are almost never what you want. They're the database equivalent of pointer-chasing in code. If you design your schema such that you need a recursive CTE to query it, be prepared for bad performance unless your CTE only ever does a handful of iterations over a handful of rows.
  - I like paths for representing hierarchy, but closure tables can also be a good idea, depending on what you're modelling and how you query it.

- I'm a big fan of the nested set representation. 
  - It hits the sweet spot of compactness and expressivity - queries for parents, children, ancestors and descendants are simple integer comparison and pretty fast with the right indices. 
  - The only downside is that this requires updates of a large number of rows whenever the tree changes (not all rows though). If you have a sharded table that could be problematic.

- Most hierarchies are shallow in practice. Keep it simple.
  - tl; dr: I agree and healthy human organizations should never scale beyond ~5 degrees of hierarchy, which is totally manageable via basic recursive JOINs in a RDBMS without fancy stored procedures or graph theory.

- This is cool - I hadn't seen the materialized view + CTE trick before, or the ltree extension. 
  - I've implemented this in the past using the classic adjacency list, materialized path or nested sets mechanisms - all by using Django Treebeard, which offers a very robust implementation of all three of them
- [django-treebeard — django-treebeard 4.7 documentation](https://django-treebeard.readthedocs.io/en/latest/)
  - Includes 3 different tree implementations with the same API: Adjacency List, Materialized Path, Nested Sets

- Most datasets have relationships forming a graph, but few need to be analyzed as a graph. Graph databases specialize for the latter usecase, with large datasets.
  - But you could always traverse graphs with recursive SQL — it’s just less pleasant, and perhaps less performant — but often that’s all you need (and often people confuse having a graph relationship with needing a graph-specialized database)

- This is use case dependent, but one of my favorite methods for implementing e.g. threaded comments is closure tables

- ## 🌲 [Representing Trees in PostgreSQL | Hacker News_201411](https://news.ycombinator.com/item?id=8642035)
- If you're storing a tree in an RDBMS, please look into the closure table algorithm rather than adjacency, nested set, or materialized paths.
  - None of the other approaches above have even remotely similar performance characteristics. If your tree is small (tens of nodes), you won't care. If it's bigger, you will.
- Another option for storing tree structures is the closure table. It acts as a sort of "many-to-many" junction table between the tree nodes, storing the relationships between each.

- I've done nested set before; it's interesting - very fast for queries, but requires a lengthy insert/update cost. Also, team members were absolutely clueless as to what was really going on. I'm not sure nested sets are really much faster than what modern rdbms's can provide today.
  - In addition to expensive insert/update, it is necessary to keep the left and right boundaries across ALL of your entries in perfect order. If the boundaries get out of whack, fixing the tree is a nightmare scenario. 
  - I worked on a multi-tenant application with distinct trees present in one table and with one tree per table and so on. Fun fun fun!
- I think the nested intervals model, a refinement of nested sets, solves this slow update problem
- One just needs to be aware that nested sets eventually hit a limit.
  - I experimented with a variation by Vadim Tropashko using something called "Farey fractions" . These represent the intervals as a 2x2 matrix of four integers rather than two floating point values. The numbers are effectively limited to 32-bit values in the matrix since a multiplication is required (resulting in 64-bit intermediate results).

- The project I'm on used materialized paths, which lead to great pain. I investigated nested intervals ... and they could't achieve the tree depths we needed (we were modeling a file system tree).
  - We are back to adjacency lists (using a parent ID) but redesigned to avoid the need for recursive ancestor and descendant queries.
- Can you elaborate on how materialized path caused pain? Was it more performance or maintenance? I would have expected MP to be a good fit for modeling a file system.
  - First, renames and moves require updating all descendants.
  - Second, the materialized path's length exceeded the database's indexable length limit. (MySQL, the DB in question, has a default index limit of 767 bytes, so only first 767 bytes are indexed.)
  - There are ways around these issues (like using "UPDATE ... WHERE" rather than using an ORM to walk the tree and update... sigh). We also had other app-specific / design-specific issues too that swamped these issues performance wise.

- We have used these for our discussion features on Pathwright. With ltree, you don't have as much flexibility when sorting by multiple values. With the Recursive CTE, you can go nuts and still end up very efficient.

- Neo4j is a great database, and I use it myself for a project that involves lots of deep hierarchies. But it has a fairly(相当) sparse(稀少的；匮乏的) feature-set where schema enforcement and data integrity checking are concerned; you basically have to add all that stuff yourself at the application level which can amount to a lot of work.
  - To second this, if you're using multiple languages to write to your database, you almost certainly want that schema enforcement at the DB level. We decided not to go with Neo as our canonical database for exactly that reason. Its main strength is probably as a follower or slave to a RDBMS or log file, which is how it seems to be used in enterprise - when you want to do graph-based analytics, you bulk-load a snapshot of your non-graph-stored DB into Neo, then run read-only workloads.

- ## 💡🌲 I am endlessly fascinated with content tagging systems. 
- https://twitter.com/hillelogram/status/1534301374166474752
  - They're ubiquitous in software and have so many nuances, but I can't find anything on how to design and implement anymore more than the barebones basics of a system.
  - A tag is a metadata label associated with content, primarily used for querying and grouping. The tag name is also the id: two tags with the same name are the same tag.
  - Tags appear everywhere: #hashtags, wikipedia categories, blog post labels, AWS infra tags...
- we need some kind of relationship between tags
  - The simplest relationship is tag aliases: if A is aliased to B, then querying A is identical to querying B. The only system I know that does that is the fanfiction site AO3
- A harder problem: tag hierarchies, or "subtags".
- There's also implementation considerations. 
  - First, transitive queries are expensive, how do you optimize them? 
  - Second, how do you prevent cycles in the tag hierarchy, where A and B are both transitive subtags of each other?
  - It gets even more complex if tags can have multiple parents, like Wikipedia categories. 

- Postgres "LTREE" data type and associated query operators are an absolute godsend for this
  - You can write a recursive CTE query that traverses an LTREE node hierarchy, and use a combination of custom alias rules, PG trigram/Levenshtein distance to build a simple but robust system

- You should look at WordPress' data structures. Ignore the taxonomy(分类法) stuff (which is tags in the traditional sense), but the `Post: PostMeta` relationship is implemented as AV and there's a system for querying it. It's the basis of some power features + plugins.

- wikidata might be the solution to your problem.

- One way I think about it is, if you have key-value pair style tags, you basically are implementing entity-attribute-value. That kind of data can be in a triple store, and advanced queries could be semantic web queries, datalog, etc.

- I suspect semantic hashing/search is probably the best way to solve the problems tagging tries to solve - doesn't require maintenance of tag ontology, lets you find documents that don't use the exact word but are v similar
  - search is basically tagging but better
  - [Tagging is Broken - Forte Labs](https://fortelabs.com/blog/tagging-is-broken/)

- I implemented a system once that made use of tagging. We ended up with "tags mean whatever the groups/teams using them want them to mean". Remarkable subcultures arose. All were valid, all were useful.
# discuss-tree-lsm
- ## 

- ## 

- ## Any recent papers related to compaction in Log Structured Merge (LSM) or similar trees?
- https://twitter.com/strlen/status/1723065927951110182
  - An idea I am experimenting with: split the key space into ranges (can use range stats or helps if the application does it), enqueue the ranges, if the IO and/or run CPU load is low, pop a range of the queue, run full manual compaction (levels 0-6 in case of rocksdb) on that range.
  - Allowing scheduling this at off peak hours. Do not start the process at all if the load is high at the start or the process. Simplest thing that could possibly work?

- Another possibility is to separate new entries from updates to existing keys. If you can do this on the app level (if the app knows what is new and what is an update) you can use bulk load insertion for appends and batch a lot of updates together before doing compaction.

- https://twitter.com/strlen/status/1729586441322168506
  - FWIW, this is a pattern I've seen implemented successfully. Super useful with high-overwrite / high-deletion workloads (e.g. implementing queue-like patterns).

- ## Revisiting Bloom Filter Efficiency in LSM Trees
- https://twitter.com/debasishg/status/1726912592437035478
- Almost all LSM based storage structures use bloom filters in front of their memtable structures to reduce IO overhead at least for the target keys not present in the underlying secondary storage. 
  - This decision to use bloom filters is based on the fact that accessing data on secondary storage, e.g., hard disk drives (HDD) or solid-state drives (SSD), is several orders of magnitude more expensive than probing the filter in memory. 
  - Overall, BFs reduce the number of disk accesses and the overall query latency at the price of additional memory footprint and CPU computation.
- The question is - is this scenario likely to change in the context of newer and faster storage devices ? 
- Faster storage devices like SSDs and non-volatile memories (NVMs) - These can turn out to be the game changer. Quoting from this paper
  - Taking into account that current SSD devices have several orders of magnitude lower access latency than disk, and that future SSDs and NVMs are bound to be faster, hashing latency is on its way to becoming comparable with data access latency.
- And this LSM hashing overhead gets further magnified as each lookup in the tree needs multiple bloom filter queries, at least one per level in the current implementations. Such repeated hash calculations turn querying over fast storage (or cached data) into a CPU-intensive operation.
- In order to address this issue we are seeing quite a few improvements and optimizations being suggested in various research papers and some of them have possibly been implemented in current LSM based stores as well (e.g. RocksDB). 
- Here are a few of them
  1. Reducing the computational complexity of hashing. ​​Bloom filters are based on a number of hash functions and for each LSM tree we need to have multiple bloom filters
  2. Improving cache efficiency of bloom filters. A Bloom filter using k hash functions performs the same number of memory accesses.
  3. Hash Sharing. Once the CPU computational complexity of hash computation is reduced as in 1 above, this efficiency can further be extended to implement sharing hash computations across multiple LSM levels 

- If you’re going to have 1kb keys (somewhat avoidable if you’re building a database system on top of LSM storage), you could speed up hashing for bloom filters by hashing only a fixed-size tail of the keys.
  - true, but the idea is that u still have to compute hash for *all* the bloom filters and you will have one per level. Hence still CPU computation intensive.

- ## 🔥 [Understanding LSM trees: What powers write-heavy databases (2020) | Hacker News_202202](https://news.ycombinator.com/item?id=30269286)
- 
- 
- 

# discuss-tree-btree
- ## 

- ## 

- ## 

- ## I would like to understand write-amplification in B Tree vs LSM Tree. Is there any survey/research paper explaining the same? or a blog post?
- https://twitter.com/iavins/status/1726563472522244518
  - [TiKV | B-Tree vs LSM-Tree](https://tikv.org/deep-dive/key-value-engine/b-tree-vs-lsm/)

- Did you see the MyRocks experiment from Meta a few years back? This showed MyRocks (MySQL but with LSM) as “10x more write efficient”.
  - For another perspective, you can also cf. the recent TreeLine paper. However, I believe the evaluation of block size vs queue depth in there may have a lurking variable—you need to benchmark past the overprovisioning of the flash device, to get a real sense of sustained throughput—the YCSB data set is probably too small to show this.
  - Beyond write performance, LSM does have some nice systems architecture properties in that it follows the general memory hierarchy (snapshots can be easier, as well as hot/cold data tiering).

- LSM trees have lower write amplification than b-trees. LSM trees write data sequentially on disk in large chunks, while b-trees usually need small in-place data updates, which result in high write amplification on SSD drives

- ## 🤔🍃 [为什么 MongoDB 使用 B 树 · Why's THE Design? · /whys-the-design-mongodb-b-tree](https://github.com/draveness/blog-comments/discussions/581)
- 本文说的不太对。现在mongo默认使用WiredTiger作为存储引擎。
  - WiredTiger实际是用B+树。

- MongoDB官方版本中，WiredTiger仅会使用B-Tree（我用作者给的createCollection做了试验，用stats看到存储结构仍旧是B-Tree）。
  - 仅有Percona Server for MongoDB的个别版本对WiredTiger开启了LSM，以及支持了另一个用LSM-Tree的RocksDB引擎
- 我又确定了一下这个问题，使用的是最新版本的 MongoDB，wiredTiger.type 确实是 lsm，默认情况是 file

- 我感觉只讲读多写少一个原因是没办法解释 MongoDB 为什么使用 B-tree 而不是 LSM 的，因为按照这个逻辑，OLTP 数据库就不应该用 LSM，而现实是 TiDB 和 CockroachDB 之类的数据库都选择了 LSM。
- TiDB 解释说 LSM 写放大、空间放大要相比 B-Tree 好一些，另外 RocksDB 本身牛逼（社区、接口等），还提到说使用缓存提高读性能要比提高写性能简单。
- CockroachDB 直接就说选 RocksDB 跟它用 LSM 关系不大，主要是 RocksDB 本身牛逼。

- LevelDB 看起来只有一个 LRU Cache
  - RocksDB 里的 Cache 还挺多的
- Influxdata 做了一个 LevelDB 和 RocksDB 的基准测试，结果表明 LevelDB 在磁盘磁盘空间利用率方面有优势，而 RocksDB 在读写上都优于 LevelDB，其中 RocksDB 的写入比 LevelDB 好很多，从这个结果来看 RocksDB 确实比 LevelDB 牛逼，不过正向文中说的，基准测试不够可靠，尤其是别人做的基准测试...
- HackerNews 的讨论中说 WiredTiger 跑的 Benchmark 目前已经过时了，但是我还没有找到其他来源的可靠 Benchmark。

- ## This document from ScyllaDB makes a strong case why B-trees make a good choice for in-memory collections as well
- https://twitter.com/debasishg/status/1688551567044251648
  - B-trees are usually used for disk based storage. 
  - [The Taming(驯服) of the B-Trees - ScyllaDB_202111](https://www.scylladb.com/2021/11/23/the-taming-of-the-b-trees/)
- Also TIL: Google has implemented a C++ template library that implements B-tree containers with an analogous interface to the standard STL map, set, multimap, and multiset containers
- I tested several B-tree implementations on the JVM in https://github.com/szeiger/forest/tree/master/main/src/main/scala/forest/mutable. 
  - I don't remember the exact benchmark results but there was no conclusive case to use them instead of the red-black trees in Scala's TreeMaps.

- Obvious in retrospect, but I just realized that if you use prolly trees for your DB indices, you can run queries against any historical state of your DB (by simply not GC'ing old data). And in fact, @DoltHub supports that
# discuss
- ## 

- ## 

- ## 8 data structures powering modern databases
- https://twitter.com/sahnlam/status/1730117267822965056
1. Skip List
A skip list is a probabilistic data structure that enables fast search within an ordered sequence of elements. It is commonly used in in-memory databases like Redis because of its efficient average-case lookup and insert operations.
2. Hash Index
The hash index, commonly used in-memory databases, is an index data structure that uses a hash table to associate key values with specific data. It's a common solution for fast in-memory key-value lookups.
3. SSTable (Sorted String Table)
An SSTable is an immutable sorted data structure typically found in disk-based databases. SSTables are a crucial component in the LSM tree.
4. LSM Tree (Log-Structured Merge-Tree)
The LSM tree combines SSTables with an in-memory structure like MemTable. This hybrid disk and memory architecture provides excellent write performance for high-volume writes. However, periodic compaction of SSTables can impact read efficiency if not properly tuned.
5. B-Tree
Perhaps the most popular on-disk database index structure, the B-tree is optimized for systems that read and write large blocks of data. Its balanced structure allows for efficient insertion, deletion, and lookup of records. B+ tree is a common variant.
6. Inverted Index
Used in search engines like Lucene, an inverted index stores a mapping from content, such as words or numbers, to their locations within a database. It enables fast full-text search.
7. Suffix Tree
A specialized string indexing data structure, the suffix tree allows for rapid substring searches.
8. R-tree
Ideal for spatial indexing, the R-tree is a tree data structure used for indexing multi-dimensional data such as geographical coordinates, rectangles, and polygons. It's commonly used to optimize nearest neighbor and geospatial searches.

- ## 🔥 [Are You Sure You Want to Use MMAP in Your Database Management System? (2022) | Hacker News_202307](https://news.ycombinator.com/item?id=36563187)
- 
- 
- 

- ## 🔥 [Are You Sure You Want to Use MMAP in Your Database Management System? [pdf] | Hacker News_202205](https://news.ycombinator.com/item?id=31504052)
- 
- 
- 

- ## 🔥 [Are you sure you want to use MMAP in your database management system? [pdf] | Hacker News_202201](https://news.ycombinator.com/item?id=29936104)
- 
- 
- 

- ## 🔥 [But how, exactly, do databases use mmap? | Hacker News_202101](https://news.ycombinator.com/item?id=25881911)
- 
- 
- 

- ## 🔥 [BTrDB: Berkeley Tree Database | Hacker News_201906](https://news.ycombinator.com/item?id=20280135)
- 
- 
- 

- ## 🔥 [Memory-Efficient Search Trees for Database Management Systems [pdf] | Hacker News_202003](https://news.ycombinator.com/item?id=22543125)
- 
- 
- 

- ## 今天发现 在 DB 里面对于 时间/空间或者多维的数据操作 , 用 R tree 来减少工作量似乎是个冷知识了.
- https://twitter.com/fuergaosi/status/1658470145109680132
- 已经见过好几次有老哥为了计算时间区间, 把数据拉到内存里面 For loop 计算了
- 当年 LBS 跟现在的 AIGC 一样火的时候，R tree 都可以写到简历上来吹牛逼了。

- ## 🔥 ["I've isolated the bug to a database query" | Hacker News_201111](https://news.ycombinator.com/item?id=3215317)
- 
- 
- 
