---
title: job-js-repeat
tags: [frontend, job, js, repeat]
created: '2021-09-21T19:54:16.072Z'
modified: '2021-10-10T09:31:09.831Z'
---

# job-js-repeat

# guide

- js语言特性与设计
- web基础
- 场景题

# faq


## [async await 和 promise 的关系](https://github.com/sisterAn/JavaScript-Algorithms/issues/149)

- async/await 应该就是个语法糖，是对 Promise + Generator 的更好的封装，async/await 是后面才出现的(ES2017)，在这以前用 Generator 可以实现异步任务，如dva库的 effects 实现。
  - Promise 相当于是 JS 引擎的底层异步 API，其它的异步方案是在它的基础上构建
- 通过 typescript 或 babel 的 playground，编写 async/await 代码转换到 ES2015 的语法就会发现，可以看到输出代码内部用的其实就是迭代器去实现的
