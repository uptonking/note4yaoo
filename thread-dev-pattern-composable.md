---
title: thread-dev-pattern-composable
tags: [composable, pattern]
created: 2024-03-15T03:17:37.941Z
modified: 2024-03-15T03:18:05.227Z
---

# thread-dev-pattern-composable

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [为什么我不推荐你用 React Query - 知乎](https://zhuanlan.zhihu.com/p/591906893)
- 网络请求的需求基本都差不多，把这些功能全部整合到一个库中用起来很方便，这些 api 用习惯了扫一眼就知道干什么了，
  - 而组合的方式千变万化，需要阅读代码才知道代码干了什么，如果这个功能到处都在用，反而效率更低。
  - 大而全的 systemd 已经取代了小而美的 unix 小工具了
- 组合的方式挺适合应付那些需求不确定的场景，组合的粒度越细，就更能满足复杂场景的需求，比如前端页面越是没有固定的套路，headless hook + component 比 Antd 这种能满足需求。
  - 但是现实中前端网络请求的需求绝大多数都差不多，出于学习的目的自己设计一套可组合的 Hook 是挺好玩的，但如果所有地方都用组合的方式维护起来挺浪费自己时间，浪费其他维护者时间。react-query 基本能 cover 99% 的需求
