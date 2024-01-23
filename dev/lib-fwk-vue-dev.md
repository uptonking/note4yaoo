---
title: lib-fwk-vue-dev
tags: [framework, frontend, lib, vue]
created: 2021-01-04T19:29:51.724Z
modified: 2021-01-04T19:34:22.729Z
---

# lib-fwk-vue-dev

# guide

# roadmap

# vue-state-management

## [Vue3学习笔记（七）—— 状态管理、Vuex、Pinia - 张果 - 博客园](https://www.cnblogs.com/best/p/16906357.html)

- 虽然我们的手动状态管理解决方案在简单的场景中已经足够了，但是在大规模的生产应用中还有很多其他事项需要考虑：
  - 更强的团队协作约定
  - 模块热更新 (HMR)
  - 服务端渲染支持
  - 与 Vue DevTools 集成，包括时间轴、组件内部审查和时间旅行调试

- Pinia 就是一个实现了上述需求的状态管理库，由 Vue 核心团队维护，对 Vue 2 和 Vue 3 都可用。
  - 现有用户可能对 Vuex 更熟悉，它是 Vue 之前的官方状态管理库。
  - 由于 Pinia 在生态系统中能够承担相同的职责且能做得更好，因此 Vuex 现在处于维护模式。它仍然可以工作，但不再接受新的功能。对于新的应用，建议使用 Pinia。
# discuss-stars
- ## 

- ## 

- ## [Is there a library like Preact for React, but for Vue? : vuejs](https://www.reddit.com/r/vuejs/comments/pp4o1s/is_there_a_library_like_preact_for_react_but_for/)
- Not a direct comparison but this exists: https://github.com/vuejs/petite-vue

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Got Vue 3 JSX working in Vite 2... with HMR!
- https://twitter.com/youyuxi/status/1345972081025036290
  - (via https://github.com/vuejs/jsx-next)
- For those who are not familiar, Vue has always supported JSX and render functions, 
  - this is mostly about HMR support and the dedicated babel transform that can leverage Vue 3 specific optimizations
- When *should* you use JSX? 
  - Maybe never - it depends on your preference. 
  - If templates are working for you, stick to it because Vue can produce more efficient code from it. 
  - JSX/render functions can be useful when writing abstract and logic heavy components though.
