---
title: ux-design-tailwind
tags: [design, ux]
created: '2020-10-03T15:29:12.552Z'
modified: '2021-01-03T17:11:47.916Z'
---

# ux-design-tailwind

# guide

# pieces

- ## [Tailwind the switch statement](https://lukejacksonn.github.io/blog/oceanwind)
- Oceanwind is my very own runtime implementation of Tailwind.
- Tailwind (like Tachyons before it) takes advantage of atomic styles.
- The idea, generally, is that instead of using class names like btn-primary which might add a multitude of style rules to a given element, we'd use more granular class names like, for example p-10 bg-blue border-1 font-bold which are often more self explanatory and usually map to a single CSS rule.
- Tailwind will swap these directives out at build time with all of its generated CSS. 

# discuss

- ## [如何评价CSS框架TailwindCSS？](https://www.zhihu.com/question/337939566/answers/updated)
- 优点就不说了，简单说一下缺点。
  - 在平时的项目中完全用Tailwind会让模板看起来冗长且支离破碎。
  - 另外 Tailwind 的的体积很大，很多类冗余，而且其中一些类的尺寸值可能并不符合项目要求（比如 padding、margin），归根到底就是要定制化。
  - 个人觉得 Tailwind 更多的是给一个参考，根据自己的业务需求编写一套 helper 可能是更好的方式。
  - 后期用 @apply 指令和 PurgeCSS 可以解决你说的问题，最大问题是，写到后来，实际上你会非常怀念Boostrap，因为有个默认样式总比没有强。
    - 我的意思并不是 Tailwind 没有解决的办法，通过 config 就能做定制化，只不过折腾一圈下来，你会发现根据自己实际的业务需求定制一套 helper 可能更简单更实用。
- 首先 Tailwind 和 Bulma 并不是一个东西。和 Bulma 是一个东西是 Bootstrap，只不过它比较老了，我提它很少，也几乎不用。
  - Bulma让你不写样式的方式是将自己类添加到标签中。如果一个组件相对复杂，还得按它的结构组装出这个组件。当你把类都添加好了，这个组件自然而然就成了它的样子。
  - Tailwind 让你不写样式的方式是把 CSS 用类的形式添加到标签中。它没有封装任何组件样式。它仅仅让你换一种方式添加样式而已。
  - 你可以基于 Tailwind 创造出 Bulma，但是反过来却不行。
  - 简单的说，Tailwind 提高了手写 CSS 的效率，并且我个人感觉是大幅度提高。
    - 它没有自以为是的帮你封装一层样式，降低你的定制性。
  - 很多集成的大框架都有这种缩写性质的css，然而一次性样式不如直接写style来的直接，也不好维护

# tailwind-examples

- https://github.com/tailwindlabs/tailwindcss
  - /28kStar/MIT/202009
  - https://tailwindcss.com/
  - A utility-first CSS framework for rapidly building custom user interfaces.
- https://github.com/tailwindlabs/headlessui
  - /1.4kStar/MIT/202009
  - https://headlessui.dev/
  - Completely unstyled, fully accessible UI components, designed to integrate beautifully with Tailwind CSS.
- https://github.com/lukejacksonn/oceanwind
  - /153Star/NALic/202010/js
  - compiles tailwind like shorthand syntax into css at runtime
  - This library takes inspiration from Tailwind and utilizes Otion to provide means of efficiently generating atomic styles from shorthand syntax and appending them to the DOM at runtime.
  - Server side rendering and static extraction is also supported.
- ref
  - https://tailwindui.com/
    - Fully responsive HTML components
