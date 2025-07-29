---
title: toc-repos-lang-rust
tags: [lang, rust, toc]
created: 2025-02-26T15:04:23.310Z
modified: 2025-02-26T15:04:31.107Z
---

# toc-repos-lang-rust

# guide

# popular
- https://github.com/khonsulabs/sediment
  - A low-level MVCC file format for storing blobs.
  - This storage format is meant to provide a foundation for building ACID-compliant databases.
  - Uses a write-ahead log for efficient, atomic, durable writes.

- https://github.com/getditto/safer_ffi /MIT/202311/rust
  - http://getditto.github.io/safer_ffi
  - a framework that helps you write foreign function interfaces (FFI) without polluting your Rust code with `unsafe { ... }` code blocks while making functions far easier to read and maintain.
# rs-fwk
- https://github.com/loco-rs/loco /apache2/202502/rust
  - https://loco.rs/
  - The one-person framework for Rust for side-projects and startups
  - Loco is strongly inspired by Rails.
  - Loco is feature complete, but features are still being added rapidly.

- https://github.com/spring-rs/spring-rs /MIT/202412/rust
  - https://spring-rs.github.io/
  - a application framework written in rust inspired by java's spring-boot
  - provides an easily extensible plug-in system for integrating excellent projects in the Rust community, such as axum, sqlx, sea-orm, etc.
  - Lightweight: The core code of spring-rs does not exceed 5, 000 lines, and the binary size of the release version packaged in rust is also small.

- https://github.com/Cassielxd/cassie_axum /38Star/apache2/202303/rust
  - 一个基于rust axum的web 框架 高性能易上手 可用于构建任何web后端项目 
  - 供rust爱好者学习使用, 基础缓存定义, redis, orm框架选用Ribatis, casbin-rs集成, 适配器编写 , 用户权限jwt 融合casbin-rs websocket
# rs-web
- https://github.com/mitsuhiko/minijinja /apache2/202410/rust
  - https://docs.rs/minijinja/
  - MiniJinja is a powerful but minimal dependency template engine for Rust compatible with Jinja/Jinja2
  - https://x.com/mitsuhiko/status/1849891716070805981
    - this took me 5 minutes to write. Basically all cursor generated. Because it has embedded dependencies, I can just use uv run to execute it

- https://github.com/Hexilee/roa /MIT/202209/rust/inactive
  - async web framework inspired by koajs, lightweight but powerful.
  - Based on hyper, runtime-independent, you can chose async runtime as you like.
  - (Default) tokio runtime and TcpStream.
    - (Optional) async-std runtime and TcpStream.
# async
- https://github.com/fMeow/maybe-async-rs /MIT/202402/rust
  - https://docs.rs/maybe-async
  - A procedure macro to unify SYNC and ASYNC implementation for downstream application/crates
  - maybe-async help unifying async and sync implementation by procedural macro.
  - https://github.com/nvksv/maybe-async-cfg /MIT/202208/rust

- https://github.com/fereidani/kanal /MIT/202310/rust
  - The fast sync and async channel that Rust deserves
  - a Rust implementation of channels of the CSP (Communicating Sequential Processes) model, designed to assist programmers in creating efficient concurrent programs. 
  - The library has a focus on unifying message passing between synchronous and asynchronous portions of Rust code through a combination of synchronous and asynchronous APIs while maintaining high performance.
  - Kanal employs a highly optimized composite technique for the transfer of objects. When the data size is less than or equal to the pointer size, it utilizes serialization, encoding the data as the pointer address. Conversely, when the data size exceeds the pointer size, the protocol employs a strategy similar to that utilized by the Golang programming language, utilizing direct memory access to copy objects from the sender's stack or write directly to the receiver's stack. 
  - Kanal utilizes a specially tuned mutex for its channel locking mechanism, made possible by the predictable internal lock time of the channel. 
  - Kanal is using Unsafe. If you are not ok with that in your project we suggest using safe-only alternatives.

- https://github.com/zkat/cacache-rs /apache2/202402/rust
  - A high-performance, concurrent, content-addressable disk cache, with support for both sync and async APIs
  - First-class async support, using either async-std or tokio as its runtime. Sync APIs are available but secondary.

- https://github.com/modal-labs/tokio-par-util /202504/rust
  - Utilities for running computations in parallel on top of Tokio
  - This library adds utility methods and stream transformers to `Stream`s and `TryStream`s, to make it easier to run many futures in parallel while adhering to structured parallelism best-practices. 
# rs-patterns
- https://github.com/rust-unofficial/patterns /MPLv2/202403/Handlebars
  - https://rust-unofficial.github.io/patterns/
  - An open source book about design patterns and idioms in the Rust programming language

- https://github.com/Cassielxd/moduforge-rs /paid/202507/rust
  - http://mf.vv-xj.com/
  - 一个基于 Rust 的状态管理和数据转换框架，专注于不可变数据结构和事件驱动架构。
  - 它提供了无业务绑定的编辑器核心实现，可以通过扩展进行定制和扩展，支持任何业务场景的需求。
  - 灵感来自prosemirror , deno
  - 工作方式: 定义基础节点、标记和约束，然后定义扩展添加行为。
  - 使用 im-rs 进行基础数据定义，保证数据的不可变性，提供安全的并发访问和高效的结构共享。。
  - zen: 规则引擎管理，解除业务硬编码耦合（如果使用）。
  - 可扩展性: ModuForge 设计为高度可扩展，允许开发者根据需求自定义编辑器的功能和行为。这包括插件系统，使得添加新功能变得简单，任何功能都可以扩展。例如：历史记录，撤销，重做。
  - 模块化: 整个框架被分解成多个独立的模块，每个模块负责编辑器的一个特定方面，如模型、状态管理、命令执行等。
  - 事件驱动: 基于事件驱动架构，所有状态变更都通过事件系统进行，确保系统的响应性和可预测性。
  - 命令模式: 使用命令模式来处理编辑操作。每个编辑操作都被封装成一个命令对象，这样可以方便地撤销或重做操作，同时也有助于实现复杂的编辑逻辑。
# more
