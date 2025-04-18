---
title: lib-ide-lsp-blogs
tags: [blog, lsp]
created: 2025-01-05T15:00:23.481Z
modified: 2025-01-05T15:00:32.524Z
---

# lib-ide-lsp-blogs

# guide

# blogs-lsp

## 🌰 [Using Language Servers with CodeMirror 6 · hjr265.me _202103](https://hjr265.me/blog/codemirror-lsp/)

- The goal was to provide code completion, diagnostics, and hover tooltips. And, CodeMirror 6 makes it easy to do all three.

- Language Servers speak JSON-RPC 2.0 over standard IO. To invoke a method or send a notification to a language server, you can write to the process’s standard input.
  - A JSON-RPC request contains some headers (at least `Content-Length`) followed by an empty line, followed by the payload.
- The language server process responds by writing to standard output
  - Notifications are similar, except that you do not expect any response from them.

- 👥 discussion

- how the LSP keeps in sync with the editor text, since it's not in the same "filesystem"? What happens if you have multiple files or "packages"?
  - The thing about being able to manage multiple files did come up previously. As a way to accommodate that use case the `languageServer` extension allows you to reuse the same `LanguageServerClient`.

## 🌰 [如何创建集成 LSP 支持多语言的 Web 代码编辑器 - 米开朗基杨 - 博客园 _202309](https://www.cnblogs.com/ryanyangcs/p/17693108.html)

- 对于一个云开发平台来说，一个好的 Web IDE 能很大程度地提高用户的编码体验
- 在这篇文章中，我们会开发一个最小最轻量的编辑器 Demo 作为演示，架构非常简单，就是前端创建一个 Monaco Editor，后端创建一个语言服务器，二者之间通过 vscode-ws-jsonrpc 和 WebSocket 服务进行传输

- 
- 
- 
- 
- 
- 
- 
- 

## 🦀 [Three Architectures for a Responsive IDE _202007](https://rust-analyzer.github.io/blog/2020/07/20/three-architectures-for-responsive-ide.html)

- rust-analyzer is a new "IDE backend" for the Rust programming language. 
  - In this post, we’ll learn how to make a snappy IDE, in three different ways

- we’ll look at the backbone infrastructure of an IDE which serves two goals:
  - Quickly accepting new edits to source files.
  - Providing type information about currently opened files for highlighting, completion, etc.

- 💡 Map Reduce
  - The first architecture is reminiscent of the map-reduce paradigm. The idea is to split analysis into relatively simple indexing phase, and a separate full analysis phase.
  - The core constraint of indexing is that it runs on a per-file basis. The indexer takes the text of a single file, parses it, and spits out some data about the file. The indexer can’t touch other files.
  - Full analysis can read other files, and it leverages information from the index to save work.
  - This approach combines simplicity and stellar performance. The bulk of work is the indexing phase, and you can parallelize and even distribute it across several machine. Two examples of this architecture are IntelliJ and Sorbet.
  - The main drawback of this approach is that it works only when it works — not every language has a well-defined FQN concept. 

- 💡 Leveraging Headers
  - The second approach places even more restrictions on the language. It requires:
  - a "declaration before use" rule, 
  - headers or equivalent interface files.
  - Two such languages are C++ and OCaml.
  - The idea of the approach is simple — just use a traditional compiler and snapshot its state immediately after imports for each compilation unit. 
  - The two examples of this approach are Merlin of OCaml and clangd.
  - The huge benefit of this approach is that it allows re-use of an existing batch compiler. The two other approaches described in this article typically result in compiler re-writes. 
  - The drawback is that almost nobody likes headers and forward declarations.

- Intermission: Laziness vs Incrementality
  - Note how neither of the two approaches is incremental in any interesting way. It is mostly "if something has changed, let’s clear the caches completely".

- 💡 Query-based Compiler
  - Rust has procedural macros, which means that even surface analysis of code can take an unbounded amount of time. And there are no header files, so the IDE has to process the whole crate.
  - It seems that purely laziness based models do not work for Rust. The minimal feasible unit of laziness, a crate, is still too big.
  - For this reason, in rust-analyzer we resort to a smart solution. We compensate for the deficit of laziness with incrementality. Specifically, we use a generic framework for incremental computation — salsa.
  - The idea behind salsa is rather simple — all function calls inside the compiler are instrumented to record which other functions were called during their execution.
  - Using this engine, we were able to implement a rather fancy update strategy. 
  - The main drawback is extra complexity, slower performance (fine-grained tracking of dependencies takes time and memory) and a feeling that this is a somewhat uncharted territory yet 
# blogs-xp

## [解锁LSP协议原理，打造你的IDE _202503](https://mp.weixin.qq.com/s/slJyLUDeXfvWz1XKhTzS1Q)

- Demo 看 lsp-bridge 源码吧

## [【go】搞明白cursor卡慢问题](https://mp.weixin.qq.com/s/78R596lJl7YxCFj3TEnUiw?scene=262&from=industrynews#rd)

# more
