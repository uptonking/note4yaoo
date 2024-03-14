---
title: thread-lang-rust-perf
tags: [perf, rust]
created: 2023-12-14T04:24:00.996Z
modified: 2023-12-14T04:24:23.700Z
---

# thread-lang-rust-perf

# guide

# discuss
- ## 

- ## 

- ## Rust 的性能主要还是上限可以无限 hack 和 unsafe 的，实际你用这些库，里面不知道给你 Box 了几层 Clone 了几次。
- https://twitter.com/tison1096/status/1768109965112414224
  - 我读到这个 GreptimeDB 的优化以后大受震撼 .. 算了一下性能，优化之后还是比不上 Golang 捏
- 但是很 Safe 呀
  - Safe 个大头鬼，该 unwrap 还是 unwrap 的 .. 还有各种性能上来了就开始 xxx_uncheck
- Rust 的优势是所有权，如果 clone 满天飞，性能到天可能就是引用计数的 GC 语言，比可达性分析的 GC 语言（例如 Go Java 这类）当然要慢。
