---
title: thread-dev-data-structure-algorithms
tags: [algorithms, data-structure, thread]
created: 2023-03-15T08:06:18.268Z
modified: 2023-03-15T08:06:35.541Z
---

# thread-dev-data-structure-algorithms

# guide

# discuss
- ## 

- ## 

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
