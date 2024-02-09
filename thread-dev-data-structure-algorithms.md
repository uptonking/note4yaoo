---
title: thread-dev-data-structure-algorithms
tags: [algorithms, data-structure, thread]
created: 2023-03-15T08:06:18.268Z
modified: 2023-03-15T08:06:35.541Z
---

# thread-dev-data-structure-algorithms

# guide

# discuss-stars
- ## 

- ## 

- ## There are two main groups of data structures: • linear, like arrays and linked lists; • non-linear, like graphs and tree
- https://twitter.com/Franc0Fernand0/status/1755866411061141567
- How are they different? 5 key points 
- 1. Arrangement of elements
  - Linear: the elements are linked sequentially and can be moved through in a single run
  - Non-linear: the elements are linked in a hierarchy and set up at different levels
- 2. Hierarchy
  - Linear: all the elements are on the same level and don't follow a hierarchy.
  - Non-linear: the elements are set up in multiple levels
- 3. Traversal
  - Linear: all the elements can be traversed in a single run
  - Non-linear: it takes more than one run to go through all the elements
- 4. Memory consumption
  - Linear: you need to know ahead of time how much memory you'll need (except for linked lists)
  - Non-linear: make more efficient use of memory and don't require a memory declaration in advance
- 5. Time complexity
  - Linear: the time complexity of most common operations increases linearly with its size
  - Non-linear: the time complexity of most common operations stays the same as the input size grows

- In a nutshell:
  - Choose linear structures for sequential data with known memory needs.
  - Go with non-linear structures when dealing with hierarchical data, efficient memory use, and better time complexity.
# discuss
- ## 

- ## 

- ## 

- ## [Designing a SIMD Algorithm from Scratch_202311](https://mcyoung.xyz/2023/11/27/simd-base64/)

- ## Hash maps and sets are must-to-know data structures for coding interviews.
- https://twitter.com/Franc0Fernand0/status/1726224177219117468
  - You have to learn only two scenarios where to use them.
- 1️⃣ Determining if an element exists.
  - Checking the existence of an element in an array is a linear time operation. 
  - Hash sets make it possible to do the check with amortized constant time.
  - With an array, the time complexity of this algorithm would be O(NM). 
  - With a hash set, only O(M).
  - You can practice this scenario in the following Leetcode problems
  - Two Sums
  - Counting Elements
  - First Letter to Appear Twice
- 2️⃣ Counting the frequency of the elements.
  - A hash map can be used to translate keys to integers. 
  - Each integer represents the occurrences of the corresponding key. 
  - For example, suppose you want to verify if all characters in a string have the same frequency. A hash map is the ideal data structure to count all character frequencies in linear time. You can check if the frequencies are unique with a single iteration over the map.

- ## 要实现一个最高性能的hashtable，这个博主做了一个惊艳的video，
- https://twitter.com/sundyli1/status/1635672480819077120
  - 涉及很多可取优化点，很多 idea 我们已经在#databend 运用上了
  - [Faster than Rust and C++: the PERFECT hash table - YouTube](https://www.youtube.com/watch?v=DMQ_HcNSOAI)
