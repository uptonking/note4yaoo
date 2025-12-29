---
title: lang-python-community-concurrency
tags: [community, concurrency, python]
created: 2023-08-28T06:14:45.447Z
modified: 2023-08-28T06:15:00.563Z
---

# lang-python-community-concurrency

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## ["Why Python Is Removing The GIL" (13.5 minutes by Core Dumped) -- good explainer on threads : r/Python _202512](https://www.reddit.com/r/Python/comments/1pxxket/why_python_is_removing_the_gil_135_minutes_by/)
  - The Problem with Python Threads (2:04): Unlike most other programming languages, Python threads do not run in parallel, even on multi-core systems. This is due to the GIL.
  - How the GIL Works (4:46): The official Python interpreter (CPython) is written in C. When Python threads are spawned, corresponding operating system threads are created in the C code (5:56). To prevent race conditions within the interpreter's internal data structures, a single global mutex, known as the Global Interpreter Lock (GIL), was implemented (8:37). This GIL ensures that only one thread can execute Python bytecode at a time, effectively preventing true parallelism.
  - Why the GIL was Introduced (9:48): Guido Van Rossum, Python's creator, explains that the GIL was a design choice made for simplicity. When threads became popular in the early 90s, the interpreter was not designed for concurrency or parallelism. Implementing fine-grained mutexes for every shared internal data structure would have been incredibly complex (10:52). The GIL provided a simpler way to offer concurrency without a massive rewrite, especially since multi-core CPUs were rare at the time (11:09).
  - Why the GIL is Being Removed (13:16): With the widespread adoption of multi-core CPUs in the mid-2000s, the GIL became a significant limitation to Python's performance in parallel workloads. The process of removing the GIL has finally begun, which will enable Python threads to run in parallel.

- I've done python for 10 years and its never been a limiting factor. my workloads have ALWAYS been io bound, and when they arent, C libraries like numpy and Torch that *do release the gil* were always sufficient. Multiprocessing library also existed. and when THAT wasnt enough.. its time to stop using python anyways.

- Shared cache across multiple cpus can be a very good thing. Lets say you need to have a cache of some sort, where you store something by key. Lets say that data is made on startup -> config map for example, or some pre-calculated stuff. This way you can have all of that in L3 or maybe even L2. You might never need this, but web server libs or other libs will use this a lot (object pooling? native connection pooling and so on).

- python 3.13 just dropped with experimental nogil support and we're already seeing real world benchmarks showing 30-50% speedups for multi-threaded workloads
  - for anyone wondering if they should care: if you're doing data processing, web scraping, or running ml inference at scale this is gonna be huge. finally dont need to mess with multiprocessing to get true parallelism
- 15 months ago. 3.14 was released in October and the free-threaded interpreter is no longer experimental.
# discuss-patterns
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Python has the nicest way to do multi-processing; no other language can come even close.
- https://twitter.com/arpit_bhayani/status/1719728043865071651
- So damn true. All intricacies aside, the way to execute is very friendly
- Goroutines and wait groups
