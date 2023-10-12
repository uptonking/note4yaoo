---
title: thread-lang-rust
tags: [lang, rust, thread]
created: 2023-10-06T16:26:26.532Z
modified: 2023-10-06T16:26:57.557Z
---

# thread-lang-rust

# guide

# discuss
- ## 

- ## 

- ## 

- ## 刚刚搜索Rust怎么实现双链表。Rust的某reddit社区坚持认为，Rust不需要双链表，因为XX性能原因，所以你写不出双链表也不是大问题，Rust把这个弄得很难写，不是大问题。
- https://twitter.com/JXQNHZr1yUAj5Be/status/1710474773954768987
  - 但这问题是在双链表上吗？人家是抛砖引玉，问有cyclic引用的数据结构在Rust怎么处理的一般问题。
- 所有循环引用结构在 Rust 都难写，目前我体验最好的 safe 的方案还是 index arena 的形式（需要依赖 unsafe 的 dep）

- 问题是rust连做一棵有环的树，都是天方夜谭啊……链表本身也是树，rust在数据结构方面的局限性不应该被无视
  - 没办法，rust 用了所有权这种东西，循环引用确实很难实现
- 生命周期/所有权要求的偏序结构，和环状数据结构的固有矛盾。

- 我觉得这是对 rust 有点苛求了，难写应该是只考虑使用 safe rust 的部分。如果能在 unsafe 实现的基础上封装出 safe 的 public API ，就够了
- 每次看到这种牺牲自由度，换取安全性的编程语言，我都忍不住想到点别的东西

- 不是bug, 是feature。 双向链表用 `LinkedList<T>` 就好。
# discuss-rs-js
- ## 

- ## 

- ## 

- ## [I rewrote 10k lines of JS into Rust over the last month. Here'a write up about i : rust_202010](https://www.reddit.com/r/rust/comments/k3jy5g/i_rewrote_10k_lines_of_js_into_rust_over_the_last/)
- Overall I've been brainstorming this change for a couple years. So I'd already shifted from a classical OOP mess with Shield/Weapon/Pillar inheriting from Permanent to one where everything is a Thing.
- I'd also moved towards having everything be referenced with integer ids which seems to be something Rust likes. This was originally so that a clone wouldn't need to update any references
- Rewriting let me come across a couple small bugs.

- ## I’m kinda fascinated by how Rust was the harbinger of next-gen JS tooling
- https://twitter.com/DasSurma/status/1712005157611774056
- One that hasn’t been mentioned is that it borrows some ideas from functional languages (sum types, monads, etc.) which makes it more elegant for AST manipulation. Same reason compiler devs love OCaml.

- 

- I think it actually wasn’t Rust. It was esbuild showing the way. SWC existed years before but didn’t really catch on until later. It wasn’t end to end (no bundler). ESBuild showed how fast native tools could be and others had to follow to keep up.

- 
