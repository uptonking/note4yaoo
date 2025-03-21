---
title: lib-fwk-nextjs-dev
tags: [framework, lib, nextjs]
created: 2020-12-12T19:19:27.854Z
modified: 2020-12-12T19:22:00.735Z
---

# lib-fwk-nextjs-dev
- The React Framework with all the features you need for production
# guide
- meta-framework
  - 功能特性: 打包、路由、布局、请求api、ssr、mock
  - 核心功能: routing, rendering, fetching
  - hot-reload

- features
  - opinionated react framework with features for production out of the box
  - ssr support
    - seo搜索引擎优化、加快首屏显示
    - hybrid static & server rendering
    - Pre-render pages at build time (SSG) or request time (SSR) in a single project
  - Zero config with flexible customization
  - file-system based routing, route pre-fetching
  - Incremental Static Regeneration
    - Add and update statically pre-rendered pages incrementally after build time.

- usecase
  - 针对重消费者业务的seo
  - 落地页(Landing page)
  - 博客页面(Blog posts)
  - 帮助文档(help and documentation)
  - 营销页面、产品介绍页面(Marketing pages)

- who is using #nextjs
  - vercel/nextjs
  - more
    - [Companies/Sites using Next.js](https://github.com/vercel/next.js/discussions/10640)

- examples
  - libs

- tips
  - 考虑引入nextjs的收益是否够高，适合开发应用而不适合库
# dev-xp
- monorepo的paths别名不依赖webpack的打包方案
  - 在顶层tsconfig.json添加 `"~/*": ["libs/d42paas-biz/client/src/*"]`

- 调试方法
  - debugger with vscode/chrome
  - 调试fetch或axios
# blogs
- ## [Gatsby vs Nextjs vs Storybook](https://component-controls.com/blogs/gatsby-vs-nextjs-vs-storybook)
- gatsby is the original static site generator for react and continues to be a leader in this space.
- nextjs was known for SSR, however recent builds allow creating highly optimized static sites.
- while storybook is not a general-purpose SSG, it comes with its own SSG engine under the hood.
# more

# discuss-nextjs-vs 🆚️

- ## 

- ## 

- ## Why Remix is a better framework than Next.js _202501
- https://x.com/_trish_07/status/1877989339574997151
  - 1. Server components looked cool, but Remix's traditional SSR is better. You can do server stuff in a loader, and it’s available throughout your page components.
  - 2. Routing is so much cleaner – file-based or function-based (my favorite).
  - 3. Deploy anywhere. I’ve tried Node servers and Cloudflare Pages, and it works great everywhere.
  - 4. Vite for bundling – way faster than Next’s Turbopack.

- why do you think loader functions are better than server components
  - I get why people like server components, but I found it annoying to create multiple wrapper components just to use Suspense for loading UIs. In Remix, I can just defer any promise and use the Await component – much simpler. Also, loaders being accessible throughout the page is great, no need for prop drilling or context. I do agree though, Next’s font and image optimization is a plus.

- The only thing I dont like about remix is the amount of config to set it up, 95% of web apps behave the same, they can and should standarlize it and allow customization if the user requires.

- Also remix allows traditional SPA paradigm in cases what that shined
# discuss
- ## 

- ## 

- ## 💡 Today I learned that prefetch for ` <Link />` is defaulted to false when using the App-router. But true when using the Page-router.
- https://x.com/emilwidlund/status/1902632753587274017
  - A small correction - default is set to null, not false.
  - prefetch does not default to true when left omitted.
  - Pass `prefetch={true}` to your `<Link />`

- not true, it is null by default and depends on whether a route is static or dynamic
  - for static routes it prefetches the page + data by default
  - for dynamic routes it prefetches a portion of the page + the first loading.js file

- Prefetch is set to null by default - meaning it will prefetch static routes on load and on mouse hover event. It is not set to true. 
  - N. B: if you care about vercel not bankrupting you, probably set it to false kn production cuz those edge requests can add up quickly

- Using `prefetch = true` by default gave us immense issues
  - we had a `<Link />` on each row of a data table, which was causing our db to have cpu overload if you tried to navigate anywhere within 10 seconds of visiting the data table route

- In app-router, you can use Partial Pre Reendering (PPR), "use-cache" directive by enabling Dynamic IO, and use @tan_satck to manage the data fetching, you can do realtime data fetching. Done, instant page navigation, and realtime data fetching.

- ## 哭了啊，升级 nextjs13 到 14 的时候，一直碰到个编译错误，花了 2 个多小时，最后发现解决方法是 rm -rf node_modules && rm -rf ./yarn.lock && yarn install。
- https://x.com/YuTengjing/status/1791870826029240743
  - 我为什么要浪费这么多时间在 yarn 的 bug 上啊，碰到好几次类似的问题了，yarn 1.x 我一定要换 pnpm 了，草！

- 跟我最近玩 expo 差不多, 每次升级最好是把 node_modules 和 native 的东西全都删干净重新跑，不然一堆奇怪的问题
  - 单独删除 lockfile 还不顶用，一定要要把 node_modules 也删了，貌似不存在 lockfile 的时候会复用 node_modules，干

- ## [NODE\_OPTIONS='--inspect' does not work as I expect · vercel/next.js · Discussion #46894](https://github.com/vercel/next.js/discussions/46894)
  - node --inspect ./node_modules/next/dist/bin/next dev

- ## ["NODE\_OPTIONS='--inspect' next dev" won't work correctly, debugging server-side not possiable · Issue #47561 · vercel/next.js](https://github.com/vercel/next.js/issues/47561)

- ## ["NODE\_OPTIONS='--inspect' next dev" won't work correctly, debugging server-side not possiable · Issue #47561 · vercel/next.js](https://github.com/vercel/next.js/issues/47561)

- ## [reactjs - How to debug getStaticProps (and getStaticPaths) in Next.js - Stack Overflow](https://stackoverflow.com/questions/63650473/how-to-debug-getstaticprops-and-getstaticpaths-in-next-js)
- It turns out Next deliberately hides console.log output in getStaticProps functions (and presumably other server-side code).

- ## [next.js - How to turn on NextJS FETCH debugging in console. It was available in Next 13.4.4 and is gone in Next 13.4.19 - Stack Overflow](https://stackoverflow.com/questions/77112134/how-to-turn-on-nextjs-fetch-debugging-in-console-it-was-available-in-next-13-4)
- experimental: { logging: "verbose", }

- ## Looks like we didn't learn our lesson with patching fetch. Now we're breaking built-in browser behavior by overriding the `formAction` property_202310
- https://twitter.com/RogersKonnor/status/1717648866114171180
  - I want to believe this compiles down to: `document.createElement("button").formAction = "/route"` .
- Now I'm even more curious how it can differentiate when it's meant to be used as a string property like the built in, and when it uses the server action....do they have any posts on how they can make the distinction? Because `formAction` is an existing property on form elements.
  - because nextAction would collide with formAction. which one takes priority?
- Now I'm even more confused. Someone's hinting it may just compile to a string, so formAction in the end may just be an actual server endpoint? but if that's the case, how does it work when used an onClick handler?
