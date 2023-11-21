---
title: thread-algs-usecase
tags: [algorithms, thread, usecase]
created: 2021-02-20T07:29:08.660Z
modified: 2021-02-20T07:30:23.867Z
---

# thread-algs-usecase

# guide

- [Algorithm Visualizer](https://github.com/algorithm-visualizer/algorithm-visualizer) is an interactive online platform that visualizes algorithms from code.
# discuss
- ## 

- ## 10 Graph Algorithms You Must Know
- https://twitter.com/AmigosCode/status/1726941910449672237
01. Breadth-first search: Traverses a graph level by level, exploring all neighbors of a node before moving on to the next level. 
02. Depth-first search: Explores as far as possible along each branch before backtracking, often implemented using recursion. 
03. Shortest path: Finds the most efficient path between two nodes in terms of the sum of edge weights. 
04. Cycle detection: Identifies the presence of cycles (loops) in a graph, crucial for detecting dependencies and avoiding infinite loops. 
05. Minimum spanning tree: Finds the subset of edges that connects all vertices with the minimum total edge weight, forming a tree. 
06. Strongly connected components: Divides a directed graph into strongly connected subgraphs, where each vertex is reachable from every other vertex. 
07. Topological sorting: Orders the vertices of a directed acyclic graph in such a way that for every directed edge, the destination vertex comes after the source vertex. 
08. Graph Colouring: Assigns colors to vertices of a graph such that no two adjacent vertices share the same color, often used in scheduling and resource allocation. 
09. Maximum flow: Determines the maximum amount of flow that can be sent from a designated source to a designated sink in a flow network. 
10. Matching: Identifies edges in a graph such that no two edges share a common vertex, often used in bipartite graph matching or assignment problems.

- ## Here are 7 Search Algorithms you need to know!
- https://twitter.com/RaulJuncoV/status/1726616445826502800
01. Linear Search: This is the simplest searching algorithm.
In a linear order, you search elements one by one. This method is common for small datasets or when the data is unordered.
02. Binary Search: Use this algorithm on sorted arrays.
It involves repeatedly dividing the search interval in half. It's much more efficient than a linear search for larger datasets.
03. Depth-First Search (DFS): DFS traverses graphs or trees.
It explores as far as possible along a branch before backtracking. It's often used to solve problems like:
- Finding paths
- Connected components
- Traversing tree structures.
04. Breadth-First Search (BFS): Like DFS, BFS traverses graphs or trees.
It explores all the nodes at the current depth level before moving on to the next level. BFS is commonly used to find the shortest path in unweighted graphs.
05. Interpolation Search: Similar to binary search, this algorithm works on sorted datasets.
It calculates the probable position of the target element based on its value. It's especially useful when the dataset is uniformly distributed.
06. Jump Search: Jump search is an improvement over linear search.
You divide the array into blocks and determine a step size. The search jumps ahead in blocks until it finds the target element or passes it, and then it performs a linear search within that block.
07. Exponential Search: Use this algorithm on sorted arrays.
It involves finding a range in which the target element exists and performing a binary search. It's useful for quickly narrowing down the search space.

- These search algorithms have various use cases and performance characteristics, making them suitable for different scenarios.

- ## git diff 之类的 diff 算法原来是动态规划的最长子序列问题（LCS）
- https://twitter.com/_a_wing/status/1525155387615236096
- 那种太朴素了，效果不是很好。现在大家都在研究语义化 diff，比如 difftastic 对两份文件分别做 parse，对比生成 AST 的差异

- ## Algorithm question (I have no idea). Given a rectangular plane and a set of rectangles on it, find the “nicest” place for a new rectangle with a given size. 
- https://twitter.com/mourner/status/1362885034085146628
  - By “nicest” I mean “where you would place it” — ideally in the middle of the largest free space. Can’t move other rects.
- this is at least similar to the "pole of inaccessibility"
  - https://github.com/mapbox/polylabel
  - A fast algorithm for finding polygon pole of inaccessibility, 
  - the most distant internal point from the polygon outline (not to be confused with centroid), implemented as a JavaScript library. 
  - Useful for optimal placement of a text label on a polygon.

- ## Given an array of length n, how would you select m ≤ n evenly-spaced samples from the array? Surprise: you can use Bresenham’s line algorithm.
- https://twitter.com/mbostock/status/1380708254586609664
- [Evenly-Spaced Sampling](https://observablehq.com/@mbostock/evenly-spaced-sampling)
