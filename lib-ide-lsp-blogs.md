---
title: lib-ide-lsp-blogs
tags: [blog, lsp]
created: 2025-01-05T15:00:23.481Z
modified: 2025-01-05T15:00:32.524Z
---

# lib-ide-lsp-blogs

# guide

# blogs-lsp

## 🦀 [Three Architectures for a Responsive IDE _202007](https://rust-analyzer.github.io/blog/2020/07/20/three-architectures-for-responsive-ide.html)

- rust-analyzer is a new "IDE backend" for the Rust programming language. 
  - In this post, we’ll learn how to make a snappy IDE, in three different ways

- we’ll look at the backbone infrastructure of an IDE which serves two goals:
  - Quickly accepting new edits to source files.
  - Providing type information about currently opened files for highlighting, completion, etc.

- Map Reduce
  - The first architecture is reminiscent of the map-reduce paradigm. The idea is to split analysis into relatively simple indexing phase, and a separate full analysis phase.
  - The core constraint of indexing is that it runs on a per-file basis. The indexer takes the text of a single file, parses it, and spits out some data about the file. The indexer can’t touch other files.
  - Full analysis can read other files, and it leverages information from the index to save work.
  - This approach combines simplicity and stellar performance. The bulk of work is the indexing phase, and you can parallelize and even distribute it across several machine. Two examples of this architecture are IntelliJ and Sorbet.
  - The main drawback of this approach is that it works only when it works — not every language has a well-defined FQN concept. 

- Leveraging Headers
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

- Query-based Compiler
  - Rust has procedural macros, which means that even surface analysis of code can take an unbounded amount of time. And there are no header files, so the IDE has to process the whole crate.
  - It seems that purely laziness based models do not work for Rust. The minimal feasible unit of laziness, a crate, is still too big.
  - For this reason, in rust-analyzer we resort to a smart solution. We compensate for the deficit of laziness with incrementality. Specifically, we use a generic framework for incremental computation — salsa.
  - The idea behind salsa is rather simple — all function calls inside the compiler are instrumented to record which other functions were called during their execution.
  - Using this engine, we were able to implement a rather fancy update strategy. 
  - The main drawback is extra complexity, slower performance (fine-grained tracking of dependencies takes time and memory) and a feeling that this is a somewhat uncharted territory yet 
# more
