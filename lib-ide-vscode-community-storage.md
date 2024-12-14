---
title: lib-ide-vscode-community-storage
tags: [indexeddb, storage, vscode]
created: 2024-12-14T17:28:04.868Z
modified: 2024-12-14T17:28:23.214Z
---

# lib-ide-vscode-community-storage

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-wasm
- ## 

- ## 

- ## [VSCode-WASM: Implement a first version of a WebShell | Hacker News _202305](https://news.ycombinator.com/item?id=35768210)
- The goal of the extension is great, as it allows developers to use WASI easily when creating new extensions
  - > WASI stands for WebAssembly System Interface. It's an API designed by the Wasmtime project that provides access to several operating-system-like features, including files and filesystems, Berkeley sockets, clocks, and random numbers, that we'll be proposing for standardization.

- It is kind of sad that Monaco (VS Code's editor as a JS web component) still doesn't support tree-sitter.
  - Tree-sitter grammars take more effort than textmate ones for the most basic highlighting, but provide less accurate parse trees than a compiler could use for more advanced features and highlighting. I understand what they were going for but I don't "get" the trade-off.
  - At least as long as the parse trees are inherently worse: Even ignoring context-dependent grammars, last time I checked tree-sitter parsers had many edge cases in which they'd accept invalid syntax but not mark the parse trees as bad, which makes them unsuitable for compiler use.
- Using compilers for highlighting basically doesn't happen because they are too slow. They are used for progressive improvement as a result (depending how fast, it can take at least 5-10 seconds post-update to get a result. For slower languages, minutes).
  - Tree-sitter is faster than textmate on initial parse in lots of cases, and update a lot faster than textmate (since they can be incrementally updated and textmate can't).
  - They are not meant as compiler replacements.
  - compilers are slow, and rarely incremental. Using tree sitter for folding/highlighting/etc, and compilers for additional progressive type info, is the right path.

- Tree sitter grammars generate a complete/concrete syntax tree with incremental updates, they necessarily have to be able to represent invalid source text (because users will type it!).
  - If you're using a tree-sitter grammar as the input to a compiler (which is not what its designed for) you need to write a pass to convert from CST to AST, as you normally would.
# discuss
- ## 

- ## 

- ## 
