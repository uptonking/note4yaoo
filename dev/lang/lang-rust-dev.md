---
title: lang-rust-dev
tags: [lang, rust]
created: 2022-11-11T06:56:49.694Z
modified: 2022-11-11T06:57:09.670Z
---

# lang-rust-dev

# guide 🦀

- classic-examples-rust
  - tips: 比cpp更安全的语言, 在 编辑器/ide/存储层 有探索，业务开发速度慢
  - editor: kilo-editor, treesitter, ripgrep, xi-editor/lapce/zed
  - db: 🌹 turso, rust-kv, terminusdb-store, 
  - crdt
  - git-like
  - utils: mdx, mdBook/rustdoc, persistent-data-structure, arrow
  - toolchain: rspack+unplugin
  - ui: gpui(by zed), tauri/pake
  - more: wasm, json-parser, tree, kanban, remark

- tutorials 🧑‍🏫
  - [Rust Language Cheat Sheet](https://cheats.rs/)
  - https://github.com/donbright/rust-lang-cheat-sheet
  - [The Complete(sh) Rust Cheat Sheet - DEV Community](https://dev.to/moekatib/the-completesh-rust-cheat-sheet-4fnn)

- who is using #rust
  - 国内: tikv
  - db:influxdb
# rust-resources
- [24 days from node.js to Rust](https://candle.dev/blog/javascript-to-rust/javascript-to-rust-day-1-rustup/)
  - https://github.com/Mercateo/rust-for-node-developers
  - I initially wrote this tutorial in the summer of 2016 for Rust 1.0, though I haven't added new chapters.

- [Blessed.rs - An unofficial guide to the Rust ecosystem](https://blessed.rs/crates)
  - https://github.com/nicoburns/blessed-rs
  - a common complaint from new Rust developers is that they don't know where to start, which crates they ought to use, and which crates they ought to trust. This list attempts to answer those questions.
  - [Blessed.rs – An unofficial guide to the Rust ecosystem | Hacker News_202211](https://news.ycombinator.com/item?id=33506132)

- [Rust语言圣经(Rust Course)](https://course.rs/about-book.html)
  - https://github.com/google/comprehensive-rust
  - https://google.github.io/comprehensive-rust/index.html
  - 👨🏻‍🏫 Rust course used by the Android team at Google

- [This Week in Rust](https://this-week-in-rust.org/)

- https://github.com/KaiserY/trpl-zh-cn
  - https://kaisery.github.io/trpl-zh-cn/
  - Rust程序设计语言（2021 edition）简体中文版
  - 对照源码位置：https://github.com/rust-lang/book/tree/main/src
  - 由 mdbook-typst-pdf 生成

- [Experiment: Improving the Rust Book](https://rust-book.cs.brown.edu/)
  - This website has the same structure as the Rust Book, but interactive quizzes are added in each section
# draft
- toys
  - salsa-rust-code-database
  - codemirror-ast port
# changelog
- [Generators are dead, long live coroutines, generators are back | Inside Rust Blog_202310](https://blog.rust-lang.org/inside-rust/2023/10/23/coroutines.html)
# rust-env
- rustup自带版本管理
  - [Rustup 镜像安装帮助 清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/rustup/)
  - [Rust crates.io 索引镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/crates.io-index.git/)

- [上海交通大学 Linux 用户组 软件源镜像服务](https://mirror.sjtu.edu.cn/docs/rust-static)

- [字节 RsProxy](https://rsproxy.cn/)
  - ~/.cargo/config
# dev

# examples
- tips
  - 经典示例可参考wasm、tauri、数据库、搜索、reader/parser/generator/stream

- https://github.com/tw93/Pake /tauri
  - Turn any webpage into a desktop app with Rust with ease.
  - 很简单的用 Rust 打包网页生成很小的桌面App
  - [这个项目和直接在浏览器里面打开有什么区别](https://github.com/tw93/Pake/issues/5)
    - 适合分发app，浏览器url不适合分发和记录
    - 没啥区别，相当于快速做了一个网页mac app，不适合所有场景
    - 底层使用的 Rust tauri.app 这个框架

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

- https://github.com/sxyazi/yazi
  - yazi，一个新的终端文件管理器，使用 Rust 开发，基于 async I/O
  - 目标是同时兼顾性能、功能，核心部分完全 Rust 实现，减少外部依赖以避免性能瓶颈和体验劣化。
  - 要不要看看 #OpenDAL，顺手支持一把更多存储服务？
    - OpenDAL 是一个 rust lib，提供了各种存储服务的访问能力。没有直接提供这些功能，不过本质上就是一堆 seek & read 操作，是可以实现的

- https://github.com/rust-lang/rustlings
  - https://rustlings.cool/
  - Small exercises to get you used to reading and writing Rust code
# rs-data-structure-algorithms
- https://github.com/joaoh82/rust_sqlite /1kStar/MIT/202207/rust/代码不多
  - a simple embedded database modeled off SQLite, but developed with Rust. 
  - The goal is get a better understanding of database internals by building one.
  - [SQLRite – SQLite clone from scratch in Rust | Hacker News_202104](https://news.ycombinator.com/item?id=26749737)

- https://github.com/Shaance/rust-simple-log-append-db /rust
  - Simple db using append only log file. 
  - This runs in a single thread
  - Implemented for learning purpose
  - When log file exceeds a certain size (1 MB in the main.rs file usage of the db), compaction process will kick-in.

- https://github.com/josephg/skiplistrs
  - high performance skiplist implementation packed with useful features
  - Skip lists are super fun structures which can be used in a similar way to a B-Tree, but with an arguably simpler implementation.
  - You can use a secondary index to refer to items in the skiplist. 
# blogs

## why rust

- [Why Turborepo is migrating from Go to Rust – Vercel](https://vercel.com/blog/turborepo-migration-go-rust)

- [Why Discord is switching from Go to Rust _202002](https://discord.com/blog/why-discord-is-switching-from-go-to-rust)
# changelog
- v1.39
  - [Are we async yet?](https://areweasyncyet.rs/)
    - async/await syntax has been stabilized in Rust 1.39.
    - You can use it with the active ecosystem of asynchronous I/O around futures, mio, tokio, and async-std.
# more
