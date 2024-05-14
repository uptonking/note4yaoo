---
title: lib-fwk-vue-dev
tags: [framework, frontend, lib, vue]
created: 2021-01-04T19:29:51.724Z
modified: 2021-01-04T19:34:22.729Z
---

# lib-fwk-vue-dev

# guide

# blogs-internals-vue

## [vue3源码分析二 生成ast（编译总览） - 掘金 _202012](https://juejin.cn/post/6911692308563886087)

# roadmap

# changelog

## v3.0_20200908

- 
- 
- 
- 

## v2.0_20160930

- 
- 

## v1.0_20151027

- v1.0_20151027
- 

## v0.x

- v0.6_20231208
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

- ## 

- ## ✨ [Refactor reactivity system to use version counting and doubly-linked list tracking · Pull Request · vuejs/core _20240224](https://github.com/vuejs/core/pull/10397)
- This PR refactors the core reactivity system to use version counting and a doubly-linked list data structure inspired by Preact signals.

- our priority is making improvements while retaining backwards compatibility, not "winning" in arbitrary micro-benchmarks. We will appreciate any constructive feedback, but being a tongue-in-cheek jerk won't help your library get more adoption.

- The result seems to be based on Vue 3.4.x rather than this PR. I'm also curious as to why 3.4 produces unnecessary recalculations

- ## [Is there a library like Preact for React, but for Vue? : vuejs](https://www.reddit.com/r/vuejs/comments/pp4o1s/is_there_a_library_like_preact_for_react_but_for/)
- Not a direct comparison but this exists: https://github.com/vuejs/petite-vue

# discuss-nuxt
- ## 

- ## 

- ## [What are some large-scale Nuxt 3 open-source projects : r/Nuxt _202401](https://www.reddit.com/r/Nuxt/comments/1af9aok/what_are_some_largescale_nuxt_3_opensource/)
- Elk is a Mastodon client that has a lot of notable contributors.
- NocoDB
- agency-os is a fairly robust template project using Nuxt on the frontend + Directus on the backend
- uninbox is growing to be quite an app

# discuss
- ## 

- ## 

- ## 

- ## 今天为了熟悉一个项目用了下 Vue3，发现代码里可以直接使用 this.userStore，
- https://twitter.com/_Xheldon/status/1790214162041524474
  - 而我并没有搜到 userStrore 的赋值和定义（包括 data 等上的属性也没有类似的值），然后我注意到有个 mapStore 心想它不会给我拼字符串吧？搜了下文档，果然，definedStore('user', {}) 后你可以 this.userStore，魔法时刻！
- Vue3 直接用 composition api 感觉会更好，项目后期用 option api 编写的代码可读性就降低了
- 直接 setup写法 就不存在 this 了

- ## Got Vue 3 JSX working in Vite 2... with HMR!
- https://twitter.com/youyuxi/status/1345972081025036290
  - (via https://github.com/vuejs/jsx-next)
- For those who are not familiar, Vue has always supported JSX and render functions, 
  - this is mostly about HMR support and the dedicated babel transform that can leverage Vue 3 specific optimizations
- When *should* you use JSX? 
  - Maybe never - it depends on your preference. 
  - If templates are working for you, stick to it because Vue can produce more efficient code from it. 
  - JSX/render functions can be useful when writing abstract and logic heavy components though.
