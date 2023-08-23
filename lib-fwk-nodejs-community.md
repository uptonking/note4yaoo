---
title: lib-fwk-nodejs-community
tags: [community, framework, nodejs]
created: 2021-07-28T18:05:41.354Z
modified: 2022-12-19T01:49:21.542Z
---

# lib-fwk-nodejs-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Node.js 内存飙涨以及 OOM 的问题，只要业务流量稍微复杂，一般都会遇到。
- https://twitter.com/Barret_China/status/1694172176273097115
  - 如果是堆内内存，在 OOM 之前可以打一个 Heap Profiling 进行分析，如果是 OOM 之后，可以利用 llnode 对 corefile 进行分析，
  - 但如果是堆外内存飙涨呢？这一块内存通过 Chrome Devtool 工具是分析不出来的。
  - 有个团队做了个工具，叫做 andb，目前已经开源
