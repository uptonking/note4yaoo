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
- https://vivaxy.github.io/examples/algorithms/rope/implement-1/index.js

- https://github.com/huntwj/rope-ts /ts
  - implementation of the Rope data type

- https://github.com/Conaclos/cow-list /ts
  - Cow List provides a Copy-On-Write iterable list that supports logarithmic searches.
    - **提供了rope实现的示例**
  - It provides also a mutable iterable List with versioning capabilities.
  - Cow List naively supports lengthy values (objects with a length property). 
    - This makes Cow List a perfect fit to implement a `rope`.
  - 👉🏻 I wished to have a generic building block to implement Dotted LogootSplit. 
    - Dotted LogootSplit is a replicated data structure designed for collaborative editing. 
    - The data structure combines a search tree and a rope.
    - For now, Cow List uses a partially persistent AVL tree.

- https://github.com/linkdotnet/ts-stringoperations /ts
  - Implementation of some known string algorithms and data structures like: Rope, Trie, Knuth Morris Pratt, Boyer Moore, Levenshtein

- https://github.com/component/rope /js
  - an implementation of the rope data structure in JavaScript.

## rope-rs

- https://github.com/josephg/jumprope-rs /rust
  - Simple, fast rope (fancy string) library built on top of Skiplists
  - A rope is a data structure for efficiently editing large strings, or for processing editing traces.
  - similar to ropey. Ropey supports a few more features (like converting line/column positions).
  - 提供了crdt测试
    - [bench npm jumprope](https://gist.github.com/josephg/bcb2e74e52dc9c4651249fdffc48d1cf)
  - This code is based on an older skiplist based C rope library I wrote several years ago
    - Instead of simply being implemented as a skiplist, jumprope is a skiplist where each leaf node contains a Gap Buffer.

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
  - [Announcing crop, the fastest UTF-8 text rope for Rust](https://www.reddit.com/r/rust/comments/11cdi6b/announcing_crop_the_fastest_utf8_text_rope_for/)
    - author of Jumprope here! Jumprope still doesn't support using line + column numbers, so it sounds like thats something both of your libraries have that I don't.

- https://github.com/josephg/librope
  - C library for heavyweight utf-8 strings (rope).

## rope-crdt

- logootsropes
  - https://github.com/coast-team/mute-structs/blob/master/src/logootsropes.ts
  - https://github.com/coast-team/mute-structs/blob/master/test/logootsropes.test.ts
  - https://github.com/coast-team/mute-structs/blob/master/test/ropesnodes.test.ts
  - https://github.com/coast-team/mute-structs/blob/master/test/tree.test.ts
- [more-logoot-rope](https://www.npmjs.com/~matthieunicolas)
  - https://www.npmjs.com/package/logootsropes-crdt
  - https://www.npmjs.com/package/editorcrdt
  - https://www.npmjs.com/package/texteditor-crdt-server
  - https://www.npmjs.com/package/logoots-texteditor-client
  - https://www.npmjs.com/package/mute-demo

- https://github.com/bazed-editor/bazed /rope
  - the baz editor.
  - The editor consists of a backend including the core data structure on which modifications are made consistent through CRDT and plugin engine (stew).

- https://github.com/cfcs/ocaml-xi-rope
  - The aim of this library is to implement a (immutable) "rope" data structure based on the one used in xi-editor
  - Xi's rope type is a CRDT (based on WOOT) permitting decentralized collaborative editing without vector clocks.
# blog
- [Rope --高效字符串处理数据结构](https://blog.csdn.net/ai_xiangjuan/article/details/79246289)

- [绳索数据结构（字符串快速拼接）](https://blog.csdn.net/sinat_36246371/article/details/72719174)

- [xi-editor: Rope science - Introduction](https://xi-editor.io/docs/rope_science_00.html)

- [Fleet: Data Structures in the Fleet Editor | Hacker News](https://news.ycombinator.com/item?id=30415868)
  - [Fleet Below Deck, Part II – Breaking down the editor: Ropes everywhere](https://blog.jetbrains.com/fleet/2022/02/fleet-below-deck-part-ii-breaking-down-the-editor/)
