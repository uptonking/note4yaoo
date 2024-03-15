---
title: lib-excel-tanstack-virtual-community
tags: [community, tanstack-virtual]
created: 2024-03-15T03:25:20.567Z
modified: 2024-03-15T03:25:43.756Z
---

# lib-excel-tanstack-virtual-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-not-yet
- ## 

- ## 

- ## [List size is capped by browser/memory _202307](https://github.com/TanStack/virtual/issues/565)
- When trying to create a list with a large count of rows, one of two things happens:
  - A. If the count is over an arbitrary number, capped by each browser individually, the scroll won't go over that row. For instance, for Chrome that number is 479348, and you can't scroll to the remaining items if there are any.
  - B. If the number is too large (for instance 150 mil), the tab will simply crash. I believe this is caused by the getMeasurements function from the virtual-core library, as it tries to create an array of the count size.
- I experienced this issue, and enabling `debug: true` show that all the time is spent is `getMeasurements` . I have timings around 100ms in this method, and the scrolling is laggy 
  - I worked around this problem by providing a smaller `count` to the virtualizer, increasing it as more pages are fetched. Scrolling is fast even with thousands of items loaded.

# discuss
- ## 

- ## 

- ## 
