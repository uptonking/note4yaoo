---
title: toc-rs-js-toolchain
tags: [lang-js, rust, toolchain]
created: 2024-03-16T13:09:30.978Z
modified: 2024-03-16T13:10:04.287Z
---

# toc-rs-js-toolchain

# guide

# popular

# rust2js

- resources
  - 不要执着于编译到js，使用一门语言除了语法更多得是生态工具库，如果用了binding后很难编译
  - [List of languages that compile to JS](https://github.com/jashkenas/coffeescript/wiki/List-of-languages-that-compile-to-JS)

- https://github.com/freemasen/jsyn /201902/rust/inactive
  - An experimental crate for converting rust to javascript
  - This crate is an attempt to convert the output of syn (a rust parsing library) to the AST defined by ressa. That would allow a user to pass this AST to resw to generate javascript.
# more
- https://github.com/aalykiot/dune /MIT/202401/rust/js
  - https://aalykiot.github.io/dune/
  - A hobby runtime for JavaScript and TypeScript
  - open-source, cross-platform, shell around the V8 engine, written in Rust and capable of running JavaScript (dah) and TypeScript code out of the box.
  - Dune embraces the V8 Inspector Protocol, a standard employed by Chrome, Edge, and Node.js
  - JSX/TSX files are also supported for server side rendering.
  - Unfortunately, debugging TypeScript programs in Dune is currently suboptimal due to the absence of source maps during the transpilation process to JavaScript
