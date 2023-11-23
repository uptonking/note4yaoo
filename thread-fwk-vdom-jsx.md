---
title: thread-fwk-vdom-jsx
tags: [framework, jsx, thread, vdom]
created: 2021-08-21T06:13:22.806Z
modified: 2021-08-23T09:58:18.490Z
---

# thread-fwk-vdom-jsx

# guide

# discuss
- ## 

- ## 

- ## [Is there any good standalone implementation of the Virtual DOM? : javascript_201410](https://www.reddit.com/r/javascript/comments/2jav2q/is_there_any_good_standalone_implementation_of/)
- jsdom?

- ## Panapasi (alpha) is the first I see based on @builderio Mitosis
- https://twitter.com/sebastienlorber/status/1534221702502178816
  - Mitosis: compiling a "JSX Lite" dialect to native frameworks 

- ## I would never want JSX standardized. 
- https://twitter.com/trueadm/status/1502326881487626253
  - It would be a huge mistake and three steps backward. 
  - The innovation around JSX has come from it being safe from being standardized. 
  - Inferno, Solid, Prepack, my React Compiler, all showed the potential of doing more at build time.
- also, it would destroy any potential future in which JSX could be compiled to some more optimal representation - a Record, or maybe even a Struct (crossing my fingers)
- Exactly. Then they can be passed around web workers for almost zero cost plus have guarantees during diffing.
- I also don't want JSX to be standard because the structure behind this is very different, like Fre is a linked list, Preact is a tree, Solidjs is another completely different tree.

- ## 到底哪种 diff 算法更快？
- https://www.zhihu.com/pin/1412784357996572672
- 其实 diff 算法目前无非就三个级别
  - 1. keymap，=> react 做的级别
  - 2. 预处理 + keymap => fre/vue2 的级别
  - 3. 预处理 + keymap + lcs/lis => inferno/vue3 的级别
- 在 2017 年左右，那时候 3 的优势很明显，所以 inferno 成为了最快
  - 但现在 2021 年，nokeyed 并不总是慢，实际上有人做过对比，2 已经和 3 差不多快了
- 但注意，任何算法的前提都是结构，vdom 和 dom 不同，如果是做 vdom diff，无疑级别越高越好，因为 vdom 更轻量，从算法得到的收益更多，所以级别 3 是最合适的
  - 但是如果做 dom diff，其实是适得其反的，dom 不适合用复杂度高的算法，级别 2 是最合适的
  - fre 使用的级别 2 的算法，实话说理论上要比 vue 慢的，但却换来了更好的复杂度，未来我可能会切换到切换到级别 3

- 不懂就问，lit-html 属于哪一种呢？
  - lit-html 是级别 2

- ## I'm playing round with the idea of "async JSX". 
- https://twitter.com/ebey_jacob/status/1428942743405961218
  - So far at a whopping 2kb for something that works. 
  - But what does this look like and mean for components? I'm not quite sure yet...
