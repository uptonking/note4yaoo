---
title: thread-dev-enginnering-perf-optimization
tags: [engineering, optimization]
created: 2022-03-18T20:55:57.435Z
modified: 2022-03-18T20:56:35.254Z
---

# thread-dev-enginnering-perf-optimization

# discuss

- ## 

- ## Have a lag radar that tells you if something takes longer than some interval, in real-time, no profile recordings.
- https://twitter.com/fabiospampinato/status/1650188305248518148
- I like your visualizing and framing as a "performance radar". I've built this FPS meter for the same purpose
  - https://twitter.com/schickling/status/1617637913935884290
- I had implemented an FPS meter too at some point, but it was harder to spot drops in frame rate (green vs red on the bar is more evident), and things can still be slow while fitting within one frame, the FPS meter won't spot that.

- I've seen stuff like this, but I'm always curious, how is it actionable? With log statements, you'd be able to look back through the history, and see which things took the most out of your time budget
- I'm using it like this:
  1. I play with my components.
  2. I take a note of which interactions cause the lag radar to show me some red.
  3. Lastly I turn on the profiler and see exactly what's going on.
  - The radar is good for knowing when to profile, it's not a replacement for it.

- ## If importing an SVG is the best thing for you ergonomically, choose a solution that returns a URL for use with `<img>`, or extracts them into `<defs>` for use with `<use href="#">`.  
- https://twitter.com/_developit/status/1382838803866521601
  - Unlike JS, SVGs inlined into HTML are pretty cheap.
  - SVG in HTML is fine - it gets parsed and rendered once by the browser. 
  - SVG in JSX requires the JS to download & execute first, generate VDOM for the SVG, render that to DOM

- ## #最最简单的性能改善方法
- https://twitter.com/ThaddeusJiang/status/1511151150095298560
  1. frontend 分页请求数据
  2. frontend 不要重复请求相同 API
  3. backend 精简 response，提高 networking 响应速度
- 进阶：
  1. frontend 缓存从 API 请求的数据

- ## How to write fast code: reduce memory access. 
- https://twitter.com/devongovett/status/1504476131818237967
- All of these tips stem from that:
  01. Reduce the size of your data structures so more can fit in CPU cache.
  02. Replace strings with numbers.
  03. Make use of bit flags. Don’t waste space on booleans.
  04. Access memory linearly.
  05. Make judicious use of the heap. Inline the most commonly accessed values, move large or less common ones to the heap.
  06. Model data like a database. Normalize commonly used structures and pass ids rather than copying them around.
  07. Consider using a struct of arrays rather than an array of structs. For example, if you have two types of value, store them in separate arrays instead of a single one with a type field. This reduces memory usage and makes iterating by type linear.
  08. Maybe obvious, but avoid copying things, especially strings. Use pointers for substrings, and reference counting or interning to avoid multiple copies of the same string.
  09. Don't store data you can recompute quickly. It's often faster to do more CPU work with smaller data structures than it is to compute less but with more memory use. Memoizing and caching often _reduces_ performance. Always measure first.
  10. Use indexes rather than pointers. This expands on tip 6. Indexes often use less memory than pointers (e.g. <= 32 bit vs always 64 bit), allowing structures to be packed tighter, among many other advantages (e.g. all values of a type in one place)

- Another one to add: prefer sorted arrays to unsorted arrays

- the #1 rule for a fast code: choose the right algorithm and data structure for your problem.
  - You can also improve performance by increasing memory usage, for example by using Memoization
  - Re memoization, it's overused IMO. Measure first.

- Avoid branches as much as possible. Frequently is better to put number crunching code before and out of if-blocks even if there are cases that this calculations wouldn't be used.
