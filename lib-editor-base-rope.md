---
title: lib-editor-base-rope
tags: [data-structure, editor, rope]
created: 2023-01-12T11:32:47.117Z
modified: 2023-01-12T11:33:28.084Z
---

# lib-editor-base-rope

# guide

- https://github.com/JokerLHF/piece-table
  - ts 版实现 mini piece-table

- [Rope理论与实践 for Java String](https://web.archive.org/web/20160306020543/https://www.ibm.com/developerworks/cn/java/j-ropes/)
# rope-impl
- https://github.com/huntwj/rope-ts /ts
  - implementation of the Rope data type

- https://github.com/Conaclos/cow-list /ts
  - Cow List provides a Copy-On-Write iterable list that supports logarithmic searches.
  - It provides also a mutable iterable List with versioning capabilities.
  - Cow List naively supports lengthy values (objects with a length property). 
  - This makes Cow List a perfect fit to implement a `rope`.
    - 提供了rope实现的示例
  - I wished to have a generic building block to implement Dotted LogootSplit. 
    - Dotted LogootSplit is a replicated data structure designed for collaborative editing. 
    - The data structure combines a search tree and a rope.
    - For now, Cow List uses a partially persistent AVL tree.

- https://github.com/linkdotnet/ts-stringoperations /ts
  - Implementation of some known string algorithms and data structures like: Rope, Trie, Knuth Morris Pratt, Boyer Moore, Levenshtein

- https://github.com/component/rope /js
  - an implementation of the rope data structure in JavaScript.

- https://github.com/cessen/ropey /rust
  - a utf8 text rope for Rust, designed to be the backing text-buffer for applications such as text editors
  - 🚨 Ropey is not good at:
    - Ropey is an **in-memory** data structure.
    - Handling texts smaller than a couple of kilobytes or so
  - Ropey is good at:
    - Handling frequent edits to medium-to-large texts. 
    - Handling Unicode correctly

- https://github.com/noib3/crop /rust
  - crop's Rope is backed by a B-tree, ensuring that the time complexity of inserting, deleting or replacing a piece of text is always logarithmic

- https://github.com/josephg/librope
  - C library for heavyweight utf-8 strings (rope).
# blog
- [Rope --高效字符串处理数据结构](https://blog.csdn.net/ai_xiangjuan/article/details/79246289)

- [绳索数据结构（字符串快速拼接）](https://blog.csdn.net/sinat_36246371/article/details/72719174)

- [xi-editor: Rope science - Introduction](https://xi-editor.io/docs/rope_science_00.html)

- [Fleet: Data Structures in the Fleet Editor | Hacker News](https://news.ycombinator.com/item?id=30415868)
  - [Fleet Below Deck, Part II – Breaking down the editor: Ropes everywhere](https://blog.jetbrains.com/fleet/2022/02/fleet-below-deck-part-ii-breaking-down-the-editor/)
