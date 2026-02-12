---
title: algs-hashmap-dev
tags: [algorithms, data-structure, hashmap]
created: 2024-11-16T11:03:51.577Z
modified: 2024-11-16T11:04:25.525Z
---

# algs-hashmap-dev

# guide

# dev

# blogs

# more

# discuss

- ## 

- ## 

- ## 

- ## 

- ## SwissTable, a high-performance open-addressing hash map originally developed by Google, is becoming more popular in the industry.
- https://x.com/ohmypy/status/2021256902554857489
  - First, Rust adopted it for its HashMap type. 
  - Then Go started using a custom version of SwissTable for its map type.
  - Now, Valkey (a Redis fork) has rewritten its core hash table data structure, switching from the old chained implementation to SwissTable.

- nteresting that the overall reduction was only in memory, not in throughput. I wonder what page table sizes they used in the allocator, and whether the process was pinned to a core.

- The SIMD-powered probing is what makes SwissTable so wild -- you check like 16 slots in parallel instead of chasing pointers through a linked list. Curious if Python's dict will eventualy follow suit or if their compact dict layout already gives them enough wins

- base type deep optimized with runtime model. its a trending

- ## When have you been using a switch case the last time?
- https://x.com/rwieruch/status/1856380442242326542
- Object is slower to parse, slower to traverse, unnecessarily takes a lot of heap memory and defies the flow. 
  - Switch is THE correct tool, faster, memory efficient and honours flow. 

- 
- 
- 
- 
