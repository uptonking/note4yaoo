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
# discuss-data-structure
- ## 

- ## 

- ## Most programming languages have arrays for their efficient random access. 
- https://twitter.com/Franc0Fernand0/status/1761374170275893375
- Here are 6 key points about arrays
- 1. Introduction
  • An array is a contiguous block of memory storing elements of the same type
  • It's a primitive data structure but a building block for many others (i.e., queues, stacks)
  • It's a linear data structure where the elements are stored sequentially

- 2. Indexing 
  • the elements can be accessed in constant time by using an integer index
  • the index of the first element is 0 
  • the index of the other elements represents their offset to 0
  • accessing an index exceeding the array size causes a memory access error

- 3. Static vs. Dynamic
  • Static arrays have fixed sizes that can't be changed. The number of elements they hold shall be defined in advance
  • Dynamic arrays can resize when adding more elements. Typically, a dynamic array doubles in size when it gets full

- 4. Multidimensional Arrays
  • arrays whose elements are arrays
  • the dimension is given by the number of nested arrays
  • elements are accessed using an index for each dimension
  • the total number of elements is computed by multiplying the size of all the dimensions
  • a 2D array is used to represent a matrix; elements are accessed using 2 indexes
  • multidimensional arrays are still a single contiguous block of memory

- 5. Pros and cons
  + Fast lookups: retrieving an element at a given index takes O(1) time
  + Cache-friendly: elements are next to each other in memory, making efficient use of cache
  - Adding and removing elements is not possible for static arrays and is slow for dynamic

- 6. Main operations
  • Accessing an element (r/w) using its index takes O(1) time
  • Adding an element is impossible for static arrays or requires a right-shift of all the elements on its right for dynamic. This takes O(n)
  • appending an item is a valid operation only for dynamic arrays
  • when the array is full, each resizing takes O(n) time to copy all existing elements 
  • but this happens so rarely that the amortized time of appending a new element is still O(1)
  • Removing an element is impossible for static arrays. For dynamic, it requires a left shift of all the elements on its right in O(n)
  • Searching for an item requires traversing the array in O(n). For sorted arrays, this can be reduced to O(logn) with a binary search

# discuss
- ## 

- ## A lot of the time, many data structures provide a similar performance with small data sets.
- https://twitter.com/Franc0Fernand0/status/1765656204242571352
  - But selecting the wrong data structure can cause disasters in terms of performance with large data sets.

- Very true. Big O doesn’t matter if N is small.

- There are multiple business cases where you should refrain(克制；抑制) from optimising for larger data sets too soon. The key is to design the code so that it can be easily upgraded as needed.

- ## This is common algorithms knowledge - for solving dynamic programming problems, commonly we have 2 approaches - top down memoized recursive approach and bottom up iterative approach ..
- https://twitter.com/debasishg/status/1761425555289976927
  - However this observation, which I saw first and only in Erik Demaine's 6.006 lecture videos on DP, very enlightening - 
  - the bottom up approach of solving DP problems is a topological sort of subproblem dependency DAG
  - I don't think CLRS states this so succinctly - any other source that made this observation before ?

- Any dependency order is a topological sort of the dag of those nodes(nodes being subproblems here) . Kind of intuitive.

- Isn’t top-down implicitly navigating this DAG too?
  - Sure, in top down approach it's implicitly navigating the DAG. 
  - The key difference lies in the order in which subproblems are solved, with bottom-up being more iterative and top-down being more recursive. 
  - I think the topological sort concept is more explicit in the bottom-up approach, but it's still inherent in the top-down approach due to the order of recursive calls.

- Indeed, I sometimes prefer doing it the bottom up way because it's good validation that the recursion isn't circular - i.e, it really forces you to think through the DAG order...
  - I find the top down recursive version more intuitive but always fall back to the bottom up approach for implementation.

- https://news.ycombinator.com/item?id=14413305
  - Once you have the recursive solution, the DP solution should be fairly easy. Draw out the recursion tree for an example (or do it more generally), convert it to a DAG by combining redundant nodes, and then do a topological sort. That topological sort is the order in which you need to solve the subproblems to get a DP solution.

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
