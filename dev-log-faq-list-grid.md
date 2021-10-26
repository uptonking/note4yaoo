---
title: dev-log-faq-list-grid
tags: [faq, grid, list]
created: '2020-11-05T08:16:43.492Z'
modified: '2021-03-29T19:16:31.873Z'
---

# dev-log-faq-list-grid

# not-yet

- 无限滚动列表时，极限条件下会导致dom元素过多，该如何提高性能
  - 采用throttle策略，每隔一段时间，删除不可见的元素
  - 使用virtualized显示屏幕某区域内的列表项

- 开发list组件和tree组件，是先开发list然后用多个list创建tree更好，还先开发tree然后用深度为2的tree创建list更好？
  - react-virtualized: List uses a Grid internally to render the rows
# ref
- [「前端长列表」开源库解析及最佳实践](https://juejin.cn/post/6844904015440904200)
