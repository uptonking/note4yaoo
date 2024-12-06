---
title: algs-tree-lsm-community
tags: [community, database, LSM-Tree]
created: 2024-02-28T08:22:11.758Z
modified: 2024-02-28T08:22:23.107Z
---

# algs-tree-lsm-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-usecase-lsm
- ## 

- ## 

- ## What are some other popular LSM Tree implementations besides RocksDB? 
- https://x.com/iavins/status/1864296848434851901
  - Do any of the modern LSM Tree stores *not* do level based data storage? What are the alternatives?

- Apache Lucene is LSM-like and widely used (e.g. in Elasticsearch and OpenSearch).

- Cassandra, ScyllaDB, LevelDB from the top of my head.

- Iirc eventstore uses LSMs

- ## Many modern databases use LSM-Tree and RocksDB with adaptations. Here is what YugabyteDB did
- https://twitter.com/FranckPachot/status/1763387123502321950
  - [Enhancing RocksDB for Speed and Scale | YugabyteDB Friday Tech Talk | Episode 88 - YouTube _202311](https://www.youtube.com/watch?v=WwsiDu-qmFU&list=PL8Z3vt4qJTkLTIqB9eTLuqOdpzghX8H40&index=4)

# discuss
- ## 

- ## 

- ## 

- ## I am reviewing the literature around LSM based storages as I am planning to write a toy etcd compatible DB.
- https://twitter.com/tangledbytes/status/1762732282627203233
- Today's read was "WiscKey". The basic ideas of the paper are:
  - Store values in a separate vLog file to reduce amplifications. 
  - Replace regular log file with vLog file.
  - To reduce the cost of randomized IO on the vLog file use prefetching (exploit SSD parallelism).
- I am not sure how GC on vLog will affect performance when the system is under high write workload. My concern is not the algorithms or locks but GC saturating the Disk bandwidth.

- fyi Badger is the WiscKey implementation in Go

- TiKV + Titan is another implementation.
  - Is this plugin based on diffkv paper ?
    - Yes, that is one of the motivations. The Wisckey part is to leverage the SSD IO internal model. One thing I’ve never understood is how does the SSD specific optimizations work on network storage in the cloud infrastructure?

- I found the original 97 paper a really good read
  - Yeah, I did too. I started last week with the original paper and then went through the "BigTable" paper (just to read the origins of the terms like "SSTable", "memtable", etc).
