---
title: lang-rust-community-async
tags: [async, community, rust]
created: 2023-08-28T04:42:35.252Z
modified: 2023-08-28T04:43:22.738Z
---

# lang-rust-community-async

# guide

# discuss
- ## 

- ## 

- ## 

- ## I suppose that Async Rust may properly separate four concepts:
- https://twitter.com/brabalawuka/status/1751100101312094607
1. Libs that are runtime agnostic, e.g. combinators, channels.
2. Libs that bind to a runtime, e.g., timers, IO structs.
3. Runtime that schedules runtime-agnostic future.
4. Runtime that schedules certain tasks.

- > Runtime that schedules certain tasks.
  - More certainly, runtime that drives (IO) tasks. A runtime scheduling common futures cannot move forward such tasks itself. Just like async-executor cannot drive tokio IO tasks.

- ## 大致搞懂了 #Rust Async Runtime 的实现路线。可以先直接拉到最后读结语部分：
- https://twitter.com/tison1096/status/1721354360922546275
  - 目前只有 Future 和 Waker 接口是 Stable 接口，其他的 block_on 和 spawn 也好，async io 和 timer 的实现也好，都是一些最佳实践。这也能看出来目前 Async Rust 不稳定的状态。
  - [Async Rust 的实现 | 夜天之书](https://www.tisonkun.org/2023/11/05/async-rust/)
- 我四年前开始写 Rust 就是这个状态，现在还是
