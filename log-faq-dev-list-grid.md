---
title: log-faq-dev-list-grid
tags: [faq, grid, list]
created: '2020-11-05T08:16:43.492Z'
modified: '2020-12-23T09:54:05.607Z'
---

# log-faq-dev-list-grid

## faq-not-yet

- 无限滚动列表时，极限条件下会导致dom元素过多，该如何提高性能
  - 采用throttle策略，每隔一段时间，删除不可见的元素
  - 使用virtualized显示屏幕某区域内的列表项

- 开发list组件和tree组件，是先开发list然后用多个list创建tree更好，还先开发tree然后用深度为2的tree创建list更好？
  - react-virtualized: List uses a Grid internally to render the rows
