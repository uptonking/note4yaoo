---
title: thread-dev-engineering-cache
tags: [cache, devops, engineering]
created: 2023-11-21T15:41:08.226Z
modified: 2023-11-21T15:41:26.460Z
---

# thread-dev-engineering-cache

# guide

# discuss
- ## 

- ## Have to admit designing my own read cache, in the absence of a kernel page cache, is absolutely kicking my ass.
- https://twitter.com/LewisCTech/status/1761840475114479825
  - A circular buffer of bytes is one thing. 
  - A circular buffer of bytes which back events of various different sizes, that has to be contiguous, is another.

- ## It is great to lead the transition from LRU caches to FIFO-based caches
- https://twitter.com/1a1a11a/status/1744465104807088533
  - A lot of interest in our new cache eviction algorithm, SIEVE https://sievecache.com.

- ## [Scaling smoothly: RevenueCat's data-caching techniques for 1.2 billion daily API requests_202310](https://www.revenuecat.com/blog/engineering/data-caching-revenuecat/)
