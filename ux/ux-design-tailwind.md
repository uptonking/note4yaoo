---
title: ux-design-tailwind
tags: [design, ux]
created: 2020-10-03T15:29:12.552Z
modified: 2021-01-03T17:11:47.916Z
---

# ux-design-tailwind

# guide

- ref
  - [Theme Configuration](https://tailwindcss.com/docs/theme)
  - [tailwind default theme](https://github.com/tailwindlabs/tailwindcss/blob/master/stubs/defaultConfig.stub.js)
# dev-xp
- 标准化的css原子类可方便ai快速设置样式

## opinions for tailwind

- [Don't use Tailwind for your Design System_202103](https://sancho.dev/blog/tailwind-and-design-systems)

- [Tailwind CSS，从入坑到退坑 - GeekNote](https://geeknote.net/Rei/posts/1995)
  - 依然需要组件样式
    - 有很多样式是使用率很高，又不足以抽取公共模版的，这时候最好是抽取组件样式，例如 button，card 等等。而这些组件样式越写越多，逐渐写了两百多行，这时候就遇到下一个问题。
    - 组件样式增多的时候，我想能把组件样式拆分文件。但是 Tailwind 本身不支持多文件合并，官方文档对此的建议是使用 postcss，把 Tailwind 作为插件使用。
  - 需要记忆具体值
    - 虽然在初次编写的时候使用预置的 token 很方便，但是第二次就麻烦了。上次用的颜色是什么
    - 怀念以前的做法，用 button--primary form__field 等样式可以确保整站的样式一致
  - Tailwind 的一大串样式很难阅读
# unocss
- tips
  - 不推荐使用, 与很多第三方tooling工具的集成缺失, 会在工具集成上花费过多时间

- [feat(webpack): support rspack/rsbuild · Pull Request · unocss/unocss _202409](https://github.com/unocss/unocss/pull/4173)
  - `import { UnoCSSRspackPlugin } from "@unocss/webpack/rspack";`
# discuss-usage-xp
- ## 

- ## 

- ## [How to use calc() in tailwind CSS? - Stack Overflow](https://stackoverflow.com/questions/65976223/how-to-use-calc-in-tailwind-css)
- Don't put space in calc
  - Or you can use underscores _ instead of whitespaces
  - class="w-[calc(100%+2rem)]"
  - class="h-20 w-[calc(100%_-_10rem)]

- border-[rgba(16, _24, _40, _0.1)]
# discuss-author
- ## 

- ## 

- ## 

- ## 7 years in to this thing and still at $0 MRR
- https://x.com/adamwathan/status/1906035220052156506
- you might need to start buying some of these SaaS starter kits/courses

- Tailwindui is in stalled mode for years now. Start charging for yearly updates and ship new ui every few months. Also include a vanila javascript library for interactivity - just like preline, so that we can use it on any framework. Current react only offering is not enough.
# discuss-v4
- ## 

- ## 

- ## 

- ## 

- ## Why do vibe coded buttons NEVER have cursor:pointer? removed in v4.
- https://x.com/akinkunmi/status/2047922960749519046
- tailwind is a styling solution - using it in your component system ala shadcn is the sensible thing to do, so i  would say its shadcn’s fault - alltough you can easily add it yourself 

- Buttons native behaviour is not to have it...
- Button doesn’t have the pointer by default only Link/anchor tag. You can try this by setting up a plain HTML file and add in the button element

- ## [Padding and margin are not working on Vue.js _ TW v4.0 · tailwindlabs/tailwindcss _202501](https://github.com/tailwindlabs/tailwindcss/discussions/15728)
  - I had a similar issue where a lot of my styles seemed to be alright but margin and padding were obviously very wrong. 
  - In v3, my main CSS file had reset styles like the ones below. I like to reset all margin and padding to 0 and handle those manually for each element and this worked fine in v3. 
  - I think v4 brought quite a few specificity changes because of the substantial use of CSS `@layer` and this made it so all my elements always had 0 margin and padding, even when using a tailwind class like `<div class="p-4"></div>` .

# discuss
- ## 

- ## 

- ## 

- ## What's the steelman case for Tailwind going forward?
- https://x.com/svpino/status/1908252064633020666
- AI prefers to write tailwind, it’s literally the reason Tailwind is going to continue to grow even more popular.

- Much less context window required for the LLM to understand the design Everything is in that one component, inline vs having to pass the entire massive css file each time

- ## A ton of confusion amongst Tailwind users comes from not realizing that if you are using CSS modules, or `<style>` blocks in Vue/Svelte/Astro, your CSS pipeline separately for every single one of those blocks.
- https://x.com/adamwathan/status/1890404835888910467
  - 50 Vue components using `<style>` means Tailwind runs 50 separate times.
  - For the best build performance, don't use Tailwind features in CSS modules or Vue/Svelte/Astro `<style>` blocks, just rely on CSS variables.
  - Or even better, just use the classes in your markup like you're supposed to 
  - 💡 The same thing happens by the way by just importing multiple CSS files in JS. Don't do that — import them all into one CSS file and load that one file in JS instead.

- ## 🌰 [Using group-hover with a css child selector · tailwindlabs/tailwindcss](https://github.com/tailwindlabs/tailwindcss/discussions/13309)

- ## [Child Selector Tailwind CSS · tailwindlabs/tailwindcss](https://github.com/tailwindlabs/tailwindcss/discussions/9917)
- You might be looking for variant groups but Tailwind does not support this
  - You could try adding the classes directly to the elements instead of the parent, but I understand there are circumstances where this is not possible.
  - You could also abstract the arbitrary variant to a plugin via addVariant to make it less verbose.

- ## 继续在浏览器扩展中尝试 tailwindcss，非常不适合 content-script，
- https://twitter.com/rxliuli/status/1751903441549438996
  - 它依赖一些全局属性，遇到某些奇葩的网站（例如百度的 rem）字体大小就会爆炸，还有类名被网站覆盖了（例如 py-4/gap），或者发现某些元素的样式炸了（例如 ul 边距）。
  - 结论：往第三方网站插入的 css 还是自行编写更容易控制。

- ## 🆚️ [What is the difference between Tailwind UI and Headless UI?](https://twitter.com/samselikoff/status/1380593139484872712)
  - Tailwind UI = Library of Prototyping components or full Layouts
  - Headless UI = UI Components that are fully accessible, with no styling
  - Tailwind UI - > Presentation(TailwindCSS)
  - Headless UI - > Behaviour(React, Vue, Alpine coming soon)
- So Tailwind UI is Headless UI but also with layouts?
  - components like these with the proper keyboard controls are prebuilt for you in Headless UI.
- I don't like the sound of it, but you could compare Tailwind UI more to something like bootstrap, prebuilt, prestyled components you could plug and play into a website, intended for prototyping a layout.
- The same level as Stripe (or even better) 

- ## [Tailwind the switch statement](https://lukejacksonn.github.io/blog/oceanwind)
- Oceanwind is my very own runtime implementation of Tailwind.
- Tailwind (like Tachyons before it) takes advantage of atomic styles.
- The idea, generally, is that instead of using class names like btn-primary which might add a multitude of style rules to a given element, we'd use more granular class names like, for example p-10 bg-blue border-1 font-bold which are often more self explanatory and usually map to a single CSS rule.
- Tailwind will swap these directives out at build time with all of its generated CSS. 
- ## Has anyone used DaisyUI? It looks decent.
- https://twitter.com/clem_mas/status/1624592566607044610
- It's the best Tailwind UI library I found. CSS only unlike Flowbite that uses JS. Great for easy components like dropdowns but forces the drawers or carousel's HTML to be very different. I ditched it in the end to customize it more and tree-shake it

- ## [Why Tailwind Isn't for Me_202101](https://dev.to/jaredcwhite/why-tailwind-isn-t-for-me-5c90)
- The problem I keep running into however is this increasing popular sentiment that Tailwind is the future (man). It's the way things should be done.
- Reason 1: Tailwind promotes ugly-ass HTML.
- Reason 2: @apply is fundamentally incompatible and non-standard (and largely unnecessary).
- Reason 3: Tailwind's focus on design systems and tokens could mostly be replaced by CSS Custom Properties (aka variables)—which IS a standard.
- Reason 4: Tailwind forgets that web components exist.
- Reason 5: Finally, Tailwind encourages div/span-tag soup.
  - custom elements are fully supported and enabled by modern browsers.
- Conclusion: If you like Tailwind, use it! But don't try to convince me it's the future.

- ## [Why I Love Tailwind_202012](https://mxstbr.com/thoughts/tailwind/)
- We have had atomic CSS frameworks for almost a decade but none of them have been as critically acclaimed as Tailwind. 
- What makes it different?
- The key to Tailwind's popularity is the painstakingly constructed system of design tokens at the core of the framework
  - The system's carefully selected constraints give developers just the right guardrails(护栏，扶栏). 
  - They make it obvious whether a choice is good or bad by offering only discrete steps.
- However, we have learned over the past decade that atomic CSS has downsides:
  - Users still have to add a separate setup for the custom CSS they inevitably need (coined "bailwind"). 

    - You cannot get by on just Tailwind in the real world. 
    - Not having a dedicated place for custom styles in the same system can cause maintenance issues down the line.

  - Due to file-size considerations, Tailwind does not include all variants (e.g. hover:, sm:) for all utilities by default. 

    - It leaves it to you to manually configure which ones you need for every single CSS property.

  - Atomic CSS is not ideal for performance. 

    - No tooling can extract the per-page critical CSS, so you end up shipping more CSS to the browser than necessary. 
    - The bigger and more dynamic the app, the more unnecessary code you will ship.

- Atomic css was created before React was released and was intended for use in template-based user interfaces, including Rails and PHP. 
  - It was never designed for functional component-based UI and doesn't take advantage of this new paradigm.
- Tailwind without the downsides
  - You can use Tailwind's marvelous system and fantastic developer experience without the downsides of atomic CSS.
  - How? twin.macro.
- You get to use Tailwind's system and developer experience and take advantage of all the benefits of CSS-in-JS
  - Extending your elements with custom styles is as simple as using the css prop, no extra separate setup required to "bailwind"
  - You can use all variants in all combinations with all utilities allowing for even more expression within the system.
  - You get fully automatic critical CSS extraction and code splitting.

    - Users will only load exactly the styles they need for the page they requested — nothing more and nothing less! 
    - CSS performance does not get better

- ## [Why Tailwind CSS_202010](https://dev.to/swyx/why-tailwind-css-2o8f)
- I once complained to @samselikoff that Tailwind caused ugly unreadable classname soup and said zero-runtime CSS-in-JS could do more with a lower learning curve.
  - I was wrong on 2 counts: Tailwind is easier to learn than I thought, and CSSinJS's flexibility can be a negative.
- "System" Values reduce Magic Numbers: 
  - Decrease hardcoded values, Increase consistency.
- Responsive Design in the Browser: 
  - Prototype in browser, copy and paste to codebase, using consistent system values.
- Inlining Styles Optimizes for Change: 
  - Make code easy to delete and move, by eliminating all reliance on the cascade.
- Inlining Styles reduces Naming: 
  - Ship faster by solving one of the known hard problems in Computer Science!
- Zero JS & Sublinear Scaling of CSS: 
  - Scale at O(log N), not O(N).
- Utility-First, not Utility-Only: 
  - Respect the Principle of Least Power, use CSS-in-JS only when warranted.
- The Bad Parts
- Is Tailwind perfect? No, of course not. But the good outweighs the bad
  - Setting up Tailwind means fiddling with build tooling.
  - The Tailwind API surface area is big and constantly growing.
  - The classnames do get rather verbose. 
  - CSS abstraction leak 

    - Tailwind let's you use classes like inline styles, but they are NOT inline styles in one critical respect - what happens when they clash
    - The order of classes generated by Tailwind matters, even though it is invisible to you. This is an abstraction leak.

- discussion
  - https://twitter.com/swyx/status/1312603851581652994

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
# ref
- [TailwindCSS: Adds complexity, does nothing.](https://dev.to/brianboyko/tailwindcss-adds-complexity-does-nothing-3hpn)
