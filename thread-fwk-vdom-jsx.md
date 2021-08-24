---
title: thread-fwk-vdom-jsx
tags: [framework, jsx, thread, vdom]
created: '2021-08-21T06:13:22.806Z'
modified: '2021-08-23T09:58:18.490Z'
---

# thread-fwk-vdom-jsx

# discuss

- ## 

- ## 

- ## 

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
