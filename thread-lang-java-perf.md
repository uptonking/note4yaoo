---
title: thread-lang-java-perf
tags: [java, perf, thread]
created: 2023-12-14T04:24:38.641Z
modified: 2023-12-14T04:24:56.899Z
---

# thread-lang-java-perf

# guide

# discuss
- ## 

- ## ⚡️ Which tools and techniques do folks use for analyzing off-heap memory issues within Java apps (say, with RocksDB)? 
- https://twitter.com/gunnarmorling/status/1756233380360835449
  - JFR and related tooling are great for managed memory analysis, but I feel the story is lacking when it comes to native memory. Any tips?
- Initial support for Native Memory Tracking is also going to land in @GraalVM Native Image soon
  - Unfortunately, when I've used NMT in the past, I didn't find it detailed enough to be really helpful in this situation, as it wouldn't tell me where exactly memory gets allocated by a native component (or maybe I just didn't know where to look).
  - LOL, even wrote about that myself not too long ago: "the one thing which NMT does not report, despite what the name might  suggest, is any memory allocated by native libraries, for instance  invoked via JNI".

- jemalloc/jeprof, I wrote about RocksDB off heap profiling here
  - [7 Tips For Optimizing Apache Flink Applications _202203](https://shopify.engineering/optimizing-apache-flink-applications-tips)

- How about RocksDB specific tools
  - Or if in the context of @ApacheFlink state in RocksDB, some suggestions here?
  - [How to manage your RocksDB memory size in Apache Flink _202002](https://www.ververica.com/blog/manage-rocksdb-memory-size-apache-flink)

- ## We have this premature optimization problem as well (from ancient times). `new HashMap<>(8)` smells. Why? 
- https://twitter.com/tagir_valeev/status/1734972551426605479
- Long ago it looked like a reasonable optimization to preallocate HashMap. Unfortunately, this never worked. First, it easily could be outdated. You can see by yourself that 10 entries are added to this map. So one needs to update the constructor every time a new entry is added.
  - But more important is that for HashMap and HashSet, the constructor parameter specifies the initial table capacity, not the expected number of elements. Even when there were 8 elements, the rehashing still occurred.
  - With default load factor 0.75, only 6 elements could be stored, so rehashing occurs when 7th element is added. In contrast, with default constructor, table for 16 elements is allocated initially, and no rehashing happens. So adding constructor parameter actually made code slower!
- Since Java 19, you can use `HashMap.newHashMap(capacity)` instead of constructor to specify the expected number of elements. But it's much better to use `Map.of` or `Map.ofEntries` to create a constant map today
- The problem with initial capacity is that it's hard to test it, so it's very often wrong.

- Frozen dictionary was introduced in . NET 8. It's an immutable, read-only dictionary optimized for fast lookup and enumeration. Does constant map in JVM provide the same features? It looks like frozen collections ideally match the code from the start topic.
