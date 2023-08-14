---
title: lang-rust-community
tags: [community, lang, rust]
created: 2022-11-11T06:56:49.694Z
modified: 2022-11-11T06:57:09.670Z
---

# lang-rust-community

# guide

# discuss
- ## 

- ## 

- ## a Rust macro that generates JS code to access struct fields directly in memory via a typed array
- https://twitter.com/devongovett/status/1687941873821007872
  - Hoping something like this can help speed up JS plugins in native build tools by avoiding serializing and deserializing things.
- It's so similar to the flatbuffers
  - sort of but it's a bit different. there's no wrapper on the rust side, they are just normal structs/enums/etc. it's also designed for in memory storage and mutation, not serialization, so you can have things like resizable vectors etc.

- Been toying with building something similar in just JS to share memory across contexts (tabs and worker)

- V8 supports external strings, so you can create JS strings from native ones without copying. But yeah you have to copy the other direction.

- What is the underlying library that's letting you map buffers directly into JS objects?
  - No library, it’s built from scratch

- something worth experimenting with: utf16-le for strings in the native code
  - It might be cheaper because JS strings can internally be utf16

- ## 3位研究人员在C语言中创造了一种替代Rust的方案。它的名字叫C-rusted
- https://twitter.com/blackanger/status/1687150565351116800
- 这个挺有意思的。思路跟typescript是一样的，相当于非侵入式增强了类型系统，如果能做到ts那种带any又能保证安全边界，我觉得应用价值还是很高的

- 然而这个文章没说具体技术细节怎么做的，还需要观望。

- ## If not for speed, Rust will be net negative for frontend tools 
- https://twitter.com/youyuxi/status/1644677516312072194
  - because it significantly increases contribution barrier and maintenance load.

- Some Rust projects (like Zellij) ease the contribution barrier by using a WASM plugin system. You can write plugins in any language that can run on WASI. Of course that doesn't solve needing to know Rust to contribute to the main package.

- ## 工作之余的想学新语言可以试试 Rust，虽然属于入门最容易放弃的语言，也不太适合用于找国内工作，
- https://twitter.com/HiTw93/status/1590856832779591680
  - 但很适合用于提高你的工程师能力或者玩转潮流开源，开始可以从《Rust 语言圣经》看起，这个教程挺不错。
  - [Rust语言圣经(Rust Course)](https://course.rs/about-book.html)
  - https://github.com/sunface/rust-course
