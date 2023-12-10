---
title: thread-dev-pattern-cache
tags: [cache, pattern, thread]
created: 2021-08-27T07:44:27.021Z
modified: 2023-12-10T14:20:42.600Z
---

# thread-dev-pattern-cache

# guide

# discuss
- ## 

- ## 

- ## 7 concepts you need to master Cache.
- https://twitter.com/RaulJuncoV/status/1733531023005110576
- Cache Hit Ratios
  - This is the answer to how effective your cache strategy is. 
  - A high hit ratio indicates that the Cache frequently contains the requested data. A high hit ratio minimizes fetching it from slower layers.
- Eviction Policies
  - They determine which data stays in the Cache and which gets removed; it's about efficiency.
  - Common policies include:
  - Least Recently Used (LRU)
  - Most Recently Used (MRU)
  - Least Frequently Used (LFU)
- Cache Coherence
  - Of course, it gets more complex In distributed systems.
  - Maintaining data consistency across these caches is critical.
  - Cache coherence ensures that all copies of a data item reflect the most recent version.
- Cache Granularity
  - This is about the size of the data units stored in the Cache. Granularity decisions impact the Cache's efficiency and hit ratio. 
  - How much data do you need to store in each operation?
- Cache Warm-up
  - Preloading the Cache with data expected to be in high demand will improve performance.
  - Especially in systems where cache hits are critical for speed.
- Cache Partitioning
  - In a well-organized toolbox, you'd have separate compartments or trays for different tools.
  - Cache partitioning is the same. It's about dividing the Cache into different sections, each tailored for a specific data type or request.
  - This organization improves the Cache since retrieving the data is easier and faster.
- Cache Compression
  - When space is at a premium, compressing cached data allows you to store more information.
  - But, this comes with the trade-off of processing overhead during compression and decompression.
- Caching isn't just dumping data somewhere and forgetting about it.
  - It's about being smart with what, how, and when you store data to make everything run smoother and quicker.

- ## Service worker didn't work for me as caching mechanism b/c of the following limitations:
- https://twitter.com/maxkoretskyi/status/1430958854754480129
  - can be destroyed at any time so can't use web sockets inside
  - cache API doesn't support POST methods while matching requests by HTTP header values
