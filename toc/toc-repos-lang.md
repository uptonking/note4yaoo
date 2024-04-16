---
title: toc-repos-lang
tags: [lang, repos, toc]
created: 2020-10-05T06:25:05.942Z
modified: 2020-11-03T06:56:19.448Z
---

# toc-repos-lang

# cpp

- https://github.com/open-source-parsers/jsoncpp
  - /14.9kStar/MIT/202009
  - allows manipulating JSON values, including serialization and deserialization to and from strings.
- https://github.com/Tencent/rapidjson
  - /9.8kStar/MIT/202008
  - JSON parser/generator for C++ with both SAX/DOM style API
  - https://github.com/miloyip/json-tutorial
    - 从零开始的JSON库教程，教程对象适合学习过基本 C/C++ 
  - ref
    - https://github.com/miloyip/nativejson-benchmark
- https://github.com/yandex/ClickHouse
  - /12.3kStar/Apache2/202009
  - column-oriented database management system that allows generating analytical data reports in real time.
- https://github.com/google/leveldb
  - /21.8kStar/BSD/202009
  - a fast key-value storage library written at Google that provides an ordered mapping
- https://github.com/protocolbuffers/protobuf
  - /43.9kStar/202009/cpp
  - Protocol Buffers - Google's data interchange format
- https://github.com/grpc/grpc
  - /27.7kStar/Apache2/202009
  - The C based gRPC (C++, Python, Objective-C, PHP, C#)
- https://github.com/electron/electron
  - /86kStar/MIT/202009/cpp
  - Build cross-platform desktop apps with JavaScript, HTML, and CSS
- https://github.com/tensorflow/tensorflow
  - /149kStar/Apache2/202009/cpp
  - An Open Source Machine Learning Framework
- https://github.com/pytorch/pytorch
  - /42.8kStar/BSD-style/202009
  - Tensor computation (like NumPy) with strong GPU acceleration
  - Deep neural networks built on a tape-based autograd system
- https://github.com/BVLC/caffe
  - /30.9kStar/BSD/202002
  - a fast open framework for deep learning.
  - https://github.com/BUPTLdy/Caffe_Code_Analysis

- https://github.com/ipkn/crow /6kStar/BSD/201712
  - Crow is very fast and easy to use C++ micro web framework (inspired by Python Flask)
- https://github.com/the-moisrex/webpp /cpp
  - a web framework written in C++ that uses multiple underlying protocols.
- https://github.com/drogonframework/drogon /cpp
  - A C++14/17/20 based HTTP web application framework running on Linux/macOS/Unix/Windows
  - Use a non-blocking I/O network lib based on epoll (kqueue under macOS/FreeBSD) to provide high-concurrency, high-performance network IO
  - Based on template, a simple reflection mechanism is implemented to completely decouple the main program framework, controllers and views.
  - Support cookies and built-in sessions; 
  - Support AOP with build-in joinpoints.

- https://github.com/lemire/Code-used-on-Daniel-Lemire-s-blog/tree/master/2023/10/07/Lithium /cpp/7900loc
  - https://twitter.com/lemire/status/1710793694981361921
  - Shamefully, I was stuck for a long time, unable to write a small web app in C++. Turns out that it is easy enough.
  - I am unhappy about the boost dependency. I avoid anything having to do with boost in my own code because it is a difficult dependency to satisfy.

- more
  - https://github.com/ariya/phantomjs
    - Scriptable Headless Browser
  - https://github.com/google/googletest
    - Google Testing and Mocking Framework
  - https://github.com/boostorg/geometry
    - defines concepts, primitives and algorithms for solving geometry problems
  - https://github.com/leezhxing/tiny-httpd
    - c语言版的tiny-httpd，按照自己的理解添加了注释并且修复了一些bug
  - https://github.com/nlohmann/json
    - JSON for Modern C++
  - https://github.com/imyouxia/Source.git
    - 记录阅读过的开源代码程序和注释
    - webbench、tinyhttp、cjson、jwsmtp
  - https://github.com/microsoft/STL
    - MSVC's implementation of the C++ Standard Library.
  - https://github.com/leethomason/tinyxml2
    - C++ XML parser that can be easily integrated into other programs
# c
- https://github.com/DaveGamble/cJSON
  - /4.9kStar/MIT/202009
  - Ultralightweight JSON parser in ANSI C.
- https://github.com/redis/redis
  - /45.4kStar/BSD/202009/c
  - an in-memory database that persists on disk.
- more
  - https://github.com/git/git
    - Git Source Code
  - https://github.com/obsproject/obs-studio
    - open source software for live streaming and screen recording
  - https://github.com/libuv/libuv
    - Cross-platform asynchronous I/O
  - https://github.com/taosdata/TDengine
    - big data platform designed and optimized for the Internet of Things (IoT).

- https://github.com/antirez/smallchat /c
  - A minimal programming example for a chat server
  - https://github.com/smallnest/smallchat /go
  - https://github.com/iamshaynez/ChatRoom /java
# python
- https://github.com/pallets/flask
  - /52.2kStar/BSD/202009
  - Python micro framework for building web applications.
- https://github.com/dpgaspar/Flask-AppBuilder
  - /3kStar/BSD/202009
  - rapid application development framework, built on top of Flask
- https://github.com/keras-team/keras
  - /49.9kStar/MIT/202009
  - Deep Learning for humans
- more
  - https://github.com/scrapy/scrapy
    - a fast high-level web crawling & scraping framework for Python.
  - https://github.com/ansible/ansible
    - IT automation platform that makes your applications and systems easier to deploy
  - https://github.com/django/django
    - The Web framework for perfectionists with deadlines.
# rust
- https://github.com/khonsulabs/sediment
  - A low-level MVCC file format for storing blobs.
  - This storage format is meant to provide a foundation for building ACID-compliant databases.
  - Uses a write-ahead log for efficient, atomic, durable writes.

- https://github.com/getditto/safer_ffi /MIT/202311/rust
  - http://getditto.github.io/safer_ffi
  - a framework that helps you write foreign function interfaces (FFI) without polluting your Rust code with `unsafe { ... }` code blocks while making functions far easier to read and maintain.

## fwk

- https://github.com/loco-rs/loco /apache2/202403/rust
  - https://loco.rs/
  - The one-person framework for Rust for side-projects and startups
  - Loco is strongly inspired by Rails.
  - Loco is feature complete, but features are still being added rapidly.

## async

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

## rust-patterns

- https://github.com/rust-unofficial/patterns /MPLv2/202403/Handlebars
  - https://rust-unofficial.github.io/patterns/
  - An open source book about design patterns and idioms in the Rust programming language
# more
