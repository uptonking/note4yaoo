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

- ## 

- ## We have this premature optimization problem as well (from ancient times). `new HashMap<>(8)` smells. Why? 
- https://twitter.com/tagir_valeev/status/1734972551426605479
- Long ago it looked like a reasonable optimization to preallocate HashMap. Unfortunately, this never worked. First, it easily could be outdated. You can see by yourself that 10 entries are added to this map. So one needs to update the constructor every time a new entry is added.
  - But more important is that for HashMap and HashSet, the constructor parameter specifies the initial table capacity, not the expected number of elements. Even when there were 8 elements, the rehashing still occurred.
  - With default load factor 0.75, only 6 elements could be stored, so rehashing occurs when 7th element is added. In contrast, with default constructor, table for 16 elements is allocated initially, and no rehashing happens. So adding constructor parameter actually made code slower!
- Since Java 19, you can use `HashMap.newHashMap(capacity)` instead of constructor to specify the expected number of elements. But it's much better to use `Map.of` or `Map.ofEntries` to create a constant map today
- The problem with initial capacity is that it's hard to test it, so it's very often wrong.

- Frozen dictionary was introduced in . NET 8. It's an immutable, read-only dictionary optimized for fast lookup and enumeration. Does constant map in JVM provide the same features? It looks like frozen collections ideally match the code from the start topic.
