---
title: algs-tree-dev
tags: [algorithms, tree]
created: 2023-04-20T08:05:12.746Z
modified: 2023-04-20T08:05:25.098Z
---

# algs-tree-dev

# guide

# dev

# blogs

- [线段树（segment tree)、区间树(interval tree) - 知乎](https://zhuanlan.zhihu.com/p/105368572)

- [Hash Array Mapped Trie（HAMT）简介 - 雪球球 - 博客园](https://www.cnblogs.com/xueqiuqiu/articles/8648853.html)
  - Hash Table 和 List 的一个区别在于 Hash Table 当中保存的元素是散列和稀疏的，不像 List 那样从下标 0 一直排列到 n。
  - 只要把 List 当中下标必须连续的限制条件去掉，Vector Trie 本身就变成了一种相对传统 Array 更好的容器
# more

# discuss

- ## 

- ## 

- ## ⚡️🤔 [WebAssembly 2.0 First Working Draft | Hacker News _202204](https://news.ycombinator.com/item?id=31086217)
- The big thing that makes javascript slow (that the optimizer can’t really fix) is complex data structures.
  - For example, if you want to implement an editable string, you have to do so using an array of smaller strings and hope the optimizer can figure it out, or slice() and re-join a single “immutable” string. Either way, your javascript code will be slower than the C/rust equivalent because the language is less expressive. Javascript has the same problem with b-trees, skip lists, ropes, gap buffers, AABB trees, and so on. You can implement all of this stuff in javascript - you just end up with much more memory indirection than you want. And for trees with different internal nodes and leaves, your code will give the optimizer indigestion.
  - In my experience, basically any of these data structures will run about 10-200x slower than their native counterparts. (If both are well optimized). To me this is the big performance advantage wasm has - that we can make high performance data structures.
  - I’m working on a CRDT in Rust. The fastest JS implementation I know of takes about 1 second to replay an editing trace from a user. In rust I can replay the same trace in 0.01 seconds (100x faster), by using a skip list. In wasm I can do it in about 0.03 seconds.
- I'm building a text editor right now. I'm just using a giant array with one element for each line. I anticipated that it would get slow, and that potentially I can push this into WebAssembly.
  - The problem is that you're going to need to get the data back out of WASM eventually, back into JavaScript and then back to the DOM.
  - I focused on other optimizations and strangely my text editor is able to keep 9 million loC file ( over 500mb ) in memory. The trick is to not render everything to the DOM, just the stuff people are looking at. That's the other bottleneck. V8 is surprisingly smart. Random access for a small section of that 9 million element array is still fast. You'd expect this array to be non linear, too. 
  - Moreover, even localized shifts are fast. I'm puzzled. For comparison, VSCode uses a more esoteric data structure called a `PieceTree` but for me becomes unresponsive at 500k LoC. To be fair, they have other sorts of overhead and processing layers to deal with, namely building an AST with potentially thousands of layer of hierarchical / code folding. Speaking of which, VSCode is built entirely in TypeScript and has a reputation of being a fast and snappy editor.
  - At any rate, I don't buy the argument that because Rust is fast and WebAssembly is comparably fast, then it makes sense to push your data structure, especially a text buffer, down into WebAssembly. The bottleneck is serializing data back and forth between WebAssembly and JavaScript. For text editors, I'm not sure this overhead is worth it, especially when V8 / Chrome is doing some crazy JS optimization behind the scenes. The appealing bit with WebAssembly is potentially that objects will have a smaller memory footprint, therefore we can push further than this 9 million LoC limit where the Chrome tab just runs out of memory, rather than having algorithmic slowdown.
- > At any rate, I don't buy the argument that because Rust is fast and WebAssembly is comparably fast, then it makes sense to push your data structure, especially a text buffer, down into WebAssembly.
  - To store a buffer in a plain text editor, with no syntax highlighting? I'm not going to fight you on that. I'm glad pure javascript is fast enough for your needs.
  - But doing collaborative text editing with a CRDT adds some extra requirements that your text editor's buffer might not have. For example:
  - Hydrating the document state on load. To cut down on file size, diamond types files currently just store the entire editing history. When you open them up, we replay the whole editing history into a buffer. And using Wasm + jumprope, this is <1ms even for very large documents. The same would not be true in javascript, and I might need to use bigger files.
  - Merging concurrent changes. (Like, merging a long lived branch). This currently involves getting fancy with a B-tree. This is fast enough in rust. It would be orders of magnitude slower in javascript.
  - Undo support. When you hit undo, you need to ignore any more recent typing from other users and just undo the local user's last change. This is subtle.
  - When edits happen, we need to convert between your (line, JS column) tuple and whatever the CRDT uses internally. Diamond types specifies edit positions by counting unicode characters from the start of the document. So we need to convert between (line, col) and unicode offsets whenever local or remote changes happen to broadcast or apply the changes.
  - Rust + Wasm let me make all of these operations essentially instant. I can do that because I can use an appropriate data structure & algorithm for each operation.
  - And, sure, Javascript's Array is pretty fast. But if you ever need something more complex than Array, your performance will suffer massively. Personally I feel much better writing this code in rust + wasm.
  - I'd integrate diamond types with your text editor by just passing edits back and forth across the module boundary. I agree that it probably doesn't make sense to share a text buffer between javascript and wasm.
- > Merging concurrent changes. (Like, merging a long lived branch). This currently involves getting fancy with a B-tree. 
  - I guess my point is why do you need balanced trees? Is this a CRDT specific thing? Can you implement CRDT with just an array of lines / gap buffer?
- > Undo support. When you hit undo, you need to ignore any more recent typing from other users
  - From my understanding, the whole point of CDRTs or any command-based design is express changes to the state as the delta. In which case, you only have to stack / remember the set of commands and not have to store the state on every change. I'm not sure if this overlaps with the data structure choice, other than implementation details.
- > And, sure, Javascript's Array is pretty fast. But if you ever need something more complex than Array, your performance will suffer massively. Personally I feel much better writing this code in rust + wasm.
  - I was just looking into TypedArrays. From my understanding, the JS runtime will use a HashMap or DoublyLinkedList if the array elements are homogenous. In the case where the JS runtimes know it is homogenous, they will fallback to those TypedArray / fixed length buffers that are "continuous" in memory. So on the JS side, Arrays can be as fast as TypedArrays thanks to the compiler. Consequently, in some benchmarks they will effectively be the same.
  - The question is whether the speed of a native array is faster than the speed of a TypedArray such that it pays for the WASM<->JS overhead. And I guess this depends on the application and the access patterns of that interop.
- I tried optimizing a physics library a few years ago by putting everything in typedarrays and it was weirdly slower than using raw javascript arrays. I have no idea why - but maybe thats fixed now.
  - TypedArrays are useful, but they're no panacea. You could probably write a custom b-tree on top of a typedarray in javascript if you really want to - assuming your data also fits into typedarrays. But at that point you may as well just use wasm. It'll be way faster and more ergonomic.

- 
- 
- 

- ## 🆚️ [What are the differences between segment trees, interval trees, binary indexed trees and range trees? - Stack Overflow](https://stackoverflow.com/questions/17466218/what-are-the-differences-between-segment-trees-interval-trees-binary-indexed-t)
- Segment tree 线段树 存储区间，查询哪些区间包含给定的点
  - O(k+logn) 查询，O(n logn) 空间
- Interval tree 区间树 存储区间，查询哪些区间与给定区间相交，也支持点查询（Segment tree）
  - O(k+logn) 查询，O(n) 空间
- Range tree 范围树 存储点，查询哪些点落在了给定区间
  - O(k+logn) 查询，O(n) 空间
- Binary indexed tree 二叉索引树 存储每个索引的项目数，查询索引 m 和 n 之间有多少个项目
  - O(logn) 查询，O(n) 空间

- 
- 
- 
