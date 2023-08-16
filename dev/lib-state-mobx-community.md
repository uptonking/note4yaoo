---
title: lib-state-mobx-community
tags: [community, mobx, state]
created: 2023-04-07T03:10:07.950Z
modified: 2023-04-07T03:10:33.378Z
---

# lib-state-mobx-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## vue3的响应式和mobx的响应式存在同样的问题，即在使用proxy的情况下，对数组的修改操作不是原子的，一次shift可能会产生多次proxy的set操作。
- https://twitter.com/wulianwen1/status/1691810099738677532
  - 因此mobx自己在内部写了一套数组的操作，保证数组的api只产生一次reaction。
  - 有没有更好的方法呢
