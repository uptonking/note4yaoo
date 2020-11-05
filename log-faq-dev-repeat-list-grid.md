---
title: log-faq-dev-repeat-list-grid
tags: [dev, grid, list, repeat]
created: '2020-11-05T08:16:43.492Z'
modified: '2020-11-05T08:19:21.899Z'
---

# log-faq-dev-repeat-list-grid

## faq-not-yet

- 无限滚动列表时，极限条件下会导致dom元素过多，该如何提高性能
  - 采用throttle策略，每隔一段时间，删除不可见的元素
