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
# rust-fwk
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
# rust-web
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
# rust-patterns
- https://github.com/rust-unofficial/patterns /MPLv2/202403/Handlebars
  - https://rust-unofficial.github.io/patterns/
  - An open source book about design patterns and idioms in the Rust programming language
# more
