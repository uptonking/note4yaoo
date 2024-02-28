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
# discuss
- ## 

- ## 

- ## I am reviewing the literature around LSM based storages as I am planning to write a toy etcd compatible DB.
- https://twitter.com/tangledbytes/status/1762732282627203233
- Today's read was "WiscKey". The basic ideas of the paper are:
  - Store values in a separate vLog file to reduce amplifications. 
  - Replace regular log file with vLog file.
  - To reduce the cost of randomized IO on the vLog file use prefetching (exploit SSD parallelism).
- I am not sure how GC on vLog will affect performance when the system is under high write workload. My concern is not the algorithms or locks but GC saturating the Disk bandwidth.

- I found the original 97 paper a really good read
  - Yeah, I did too. I started last week with the original paper and then went through the "BigTable" paper (just to read the origins of the terms like "SSTable", "memtable", etc).

- fyi Badger is the WiscKey implementation in Go
