---
title: lang-rust-dev
tags: [lang, rust]
created: 2022-11-11T06:56:49.694Z
modified: 2022-11-11T06:57:09.670Z
---

# lang-rust-dev

# guide

- resource
  - [Rust语言圣经(Rust Course)](https://course.rs/about-book.html)
  - [24 days from node.js to Rust](https://candle.dev/blog/javascript-to-rust/javascript-to-rust-day-1-rustup/)
  - https://github.com/google/comprehensive-rust
    - Rust course used by the Android team at Google
  - https://github.com/Mercateo/rust-for-node-developers
    - I initially wrote this tutorial in the summer of 2016 for Rust 1.0, though I haven't added new chapters.
# tips
- rustup自带版本管理
  - [Rustup 镜像安装帮助 清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/rustup/)
  - [Rust crates.io 索引镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/crates.io-index.git/)
# dev

# examples
- tips
  - 经典示例可参考wasm、tauri、数据库、搜索、reader/parser/generator/stream

- https://github.com/tw93/Pake
  - Turn any webpage into a desktop app with Rust with ease.
  - 很简单的用 Rust 打包网页生成很小的桌面App

- https://github.com/asg017/sqlite-loadable-rs
  - A framework for writing fast and performant SQLite extensions in Rust

- https://github.com/x2bool/xlite /202210/rust
  - SQLite extension for querying Excel (.xlsx, .xls, .ods) files as virtual tables

- https://github.com/skyzh/type-exercise-in-rust
  - 包含了一整套数据库执行器的类型设计
  - [用 Rust 做类型体操 (上篇) - Alex Chi](https://www.skyzh.dev/posts/articles/2022-01-22-rust-type-exercise-in-database-executors/)

- https://github.com/erikgrinaker/toydb /202205/rust
  - Distributed SQL database in Rust, written as a learning project
  - 内部自己实现了SQL Parser、Query Planner、Storage（包括一个B+Tree）和Raft，都是直接编写的（简化版本）的源码而不是用外部库，确实很适合用来学习

- https://github.com/risinglightdb/risinglight /rust
  - An OLAP database system for educational purpose
# blogs

## why rust

- [Why Turborepo is migrating from Go to Rust – Vercel](https://vercel.com/blog/turborepo-migration-go-rust)
# more
