---
title: note-fwk-ssr-isomorphic
tags: [framework, isomorphic, server-side-rendering, ssr]
created: 2020-12-19T13:02:19.041Z
modified: 2020-12-19T13:05:23.294Z
---

# note-fwk-ssr-isomorphic

# guide

- pros-ssr
  - seo搜索引擎优化
    - 更多针对toC消费者业务，对企业管理系统没必要做seo
    - 现在的互联网应用是信息孤岛的趋势，微信公众号的文章内容不让百度收录
    - seo针对SPA的问题，谷歌爬虫已经处理，百度也不远了，还是基于prerender
    - dynamic rendering是解决seo问题的另一种方式
  - 加快首屏显示
    - 使用代码拆分和动态(懒)加载也能实现
  - 提升开发效率，使用同构渲染，一套代码可以运行在服务端和客户端

- cons-ssr
  - ?

- tips
  - 开发前进行技术选型时多分析使用场景，ssr和csr的技术栈本身就是不同的，jsx只是view层，服务端要考虑routing/cache

- usecase
  - 针对重消费者业务的seo，偏离市场主流业务
  - 落地页(Landing page)
  - 博客页面(Blog posts)
  - 帮助文档(help and documentation)
  - 营销页面、产品介绍页面(Marketing pages)
# blogs

## [LiveViewJS Introduction](https://www.liveviewjs.com/docs/overview/introduction)

- LiveViewJS is an open-source framework for "LiveView"-based, full-stack applications in NodeJS and Deno.
- The LiveView pattern, as popularized in Elixir’s Phoenix framework, shifts your UI’s state management, event handling to the server, calculating minimal diffs to drive updates in your HTML over WebSockets.
- a LiveView is a server-rendered HTML page that, when loaded, connects back to the server via a persistent web socket. As the user interacts with the LiveView, the client to sends user events (click, keys, etc) via the websocket back to the server and the server responds with diffs to the HTML page in return.
- LiveViewJS is a protocol compliant, implementation of Phoenix LiveView but written in Typescript and runs on NodeJS and Deno. We want to bring the magic and productivity of LiveView to the NodeJS and Deno ecosystems

## [新时代的 SSR 框架破局者：qwik - 知乎](https://zhuanlan.zhihu.com/p/597473358)

- 所谓 CSR 的意味着当发出一个请求时，服务器会返回一个空的 HTML 页面以及对应的 JavaScript 脚本。
  - 当浏览器下载完成对应的 JS 脚本后才会动态执行对应的 JS 脚本然后在返回的 HTML 页面上进行渲染页面内容。
  - 在页面初始化访问后加载速度极快且响应非常迅速。 

- 基于旧时代的类似 Java 的 JSP 的方式，每个HTML都需要单独请求服务器返回对应的 HTML 内容严格意义上来说这也是 SSR 的方式但是很明显这已经被时代淘汰了。
- 目前广泛应用的服务端渲染技术大概的思路是
  - 首次访问页面时，页面的静态 HTML 是在服务端生成的。
  - 在服务端我们将生成的静态 HTML 以及 HTML 中携带的 JS 脚本发送到客户端。
  - 此时静态 HTML 会立即显示在用户视野中，然后浏览器会利用网络进程下载当前 HTML 脚本中的 JS 脚本。
  - 当 JS 脚本下载完成后，会立即执行同时发生一种被称为 hydration 的过程。
  - 所谓的 hydration 简单来说，也就是客户端下载完成 JS 脚本后，浏览器会执行下载的 JS 脚本这些脚本中有部分内容会将已经存在的 HTML 内容通过执行下载的 JS 脚本添加上对应的事件监听器 从而保证页面的交互。
  - 所以 hydration 的过程是给当前页面中已经生成的 HTML 页面添加上对应的事件监听器。
  - 当 hydration 过程完成后，会由我们的客户端框架接管网站的后续渲染。
- 注意，在 React、Vue 中 hydration 并不意味这重新渲染。因为在 Server 端已经渲染了和 Client 完全相同的 DOM 结构所以完全没有必要在此重新渲染。

- 这篇文章的目的是为了让大家在当前众多 SSR 框架中思考性能方面是否可以有所提升的，在服务器方面不会过多的深入。
- 其实社区内部之前已经有非常多的方案来提升所谓 SSR 框架的性能方案。
  - 比如 Remix 的 HTTP stale-while-revalidate 缓存指令
  - 比如 astro 等新兴框架的 Islands 架构方案，关于 Islands 有兴趣的朋友可以参考神三元的这篇 Islands 架构原理和实践。
- 针对于上面的概念，我们直接来看看 qwik 中提到的 Hydration is Pure Overhead （完全多余的 Hydration）。

- Hydration 过程的难点就在于我们需要知道需要什么事件处理程序，以及将该事件处理程序附加在哪个对应的 DOM 节点上。

- 前三个阶段被称为 RECOVERY 的阶段其实是完全没有必要的，因为在服务端我们已然渲染过对应的 HTML ，但是为了应用程序的可交互性以及服务端仅保留了静态的 HTML 模版导致不得不在 Client 上继续执行一次 Server 端的逻辑。

- Resumability: 更加优雅的 hydration 替代方案

- qwik 中提出了一个全新的思路来规避 RECOVERY 带来的外开销：
  - 将所有必需的信息序列化为 HTML 的一部分。
  - 依赖于事件冒泡来拦截所有事件的全局事件处理程序。qwik 中事件处理程序是在全局处理的，这样我们就不必在在特定的 DOM 元素上单独注册所有事件。
  - qwik 内部存在一个可以延迟恢复事件处理程序的工厂函数。用来识别某个事件处理函数中应该存在什么脚本逻辑。

- 对比传统的 hydration 方案，在客户端获得服务端下发的 HTML 后会立即请求需要的 JS 脚本并执行从而为页面附加对应的交互效果。
- 而 qwik 提出的概念恰恰相反，获取完服务端下发的 HTML 页面后所有的交互效果实际上都是一种惰性创建的效果。
- 因为我们在 HTML 中的每个元素中都已经通过序列化从而在它的标签属性上记录了对应事件处理函数的位置以及脚本内容（自然内容中也包含对应的状态），所以当获得 HTML 页面后其实就可以说此时页面已经加载完毕了而不需要任何实时的 JS 执行。

- 💡 简单来讲Qwik的工作原理就是在服务端序列化 HTML 模版，从而在客户端延迟创建事件处理程序，这也是它为什么非常快速的原因。
  - 序列化这一步是在服务端渲染时完成的，这也就意味着后续客户端可以通过服务端序列化的属性信息进行反序列化从而达到所谓的可恢复性而不需要重复执行组件。

- 🤔 惰性加载脚本会影响用户交互体验吗
  - qwik 中既然选择在触发用户行为时，再惰性加载并执行响应的 JS 脚本。那么难免需要在用户触发交互时动态生成对应的事件处理函数进行执行。
  - 这样的方式相较于传统 hydration 的确会存在一些不足，需要额外生成事件会额外造成交互响应时间的损耗而传统 SSR 方式在页面首次加载时就已经绑定好（相当于生成了）相应的事件处理函数。
  - 针对于动态加载 JS 脚本，其实已经存在诸如非常多的 prefetch 等等预加载技术。
  - 无论是基于传统 Next 方案还是基于 qwik 这种惰性可恢复的方案，利用 prefetch 等预加载技术优先在网络空闲时加载响应重要的 JS 脚本都是非常有必要的，所以这点在我看来并不是特别重要的问题。

- 动态创建事件函数会造成内存泄漏吗
  - qwik 会在每次事件执行完毕后释放函数，相当于每次事件执行完毕都会进行一次“去水合”的过程。

- 延迟加载会带来 bundle 数量的上升吗
  - qwik 推崇的延迟加载其实已经是一项非常成熟的构建技术了。无论是使用 webpack、rollup 又或是其他任何构建工具都存在延迟加载 & 代码分割的技术。
  - 因为 qwik 本身提倡的就是所谓的延迟加载，所以在框架内部已经帮我们足够智能的去处理这个过程。

- 我们可以看出来，qwik 的核心思路还是通过更加细粒的代码控制配合惰性加载事件处理程序以及事件委托来缩短首屏 TTI。

- 文章中我们也讲到了 qwik 其实并不是因为使用了多么牛逼的算法导致它有多么快，而它的速度正是得益于它的设计思路，省略了传统 SSR 下首屏需要加载庞大的 JS 进行 hydration 的过程。

## [Islands 架构原理和实践 - 掘金](https://juejin.cn/post/7155300194773860382)

- MPA(Multi-page application) 即多页应用，是从服务器加载多个 HTML 页面的应用程序。每个页面都彼此独立，有自己的 URL。
  - 当单击 a 标签链接导航到另一个页面时，浏览器将向服务器发送请求并加载新页面。
  - 例如，传统的模板技术如JSP、Python、Django、PHP、Laravel 等都是基于 MPA 的框架，包括目前比较火的 Astro 也是采用的 MPA 方案。
- SPA(Single-page application) 即单页应用，它只有一个不包含具体页面内容的 HTML，当浏览器拿到这份 HTML 之后，会请求页面所需的 JavaScript 代码，通过执行 JavaScript 代码完成 DOM 树的构建和 DOM 的事件绑定，从而让页面可以交互。如现在使用的大多数 Vue、React 中后台应用都是 SPA 应用。

- 性能
  - SPA 需要客户端先请求 JS Bundle 然后执行 JS 以渲染页面。因此，MPA 中的页面的首屏加载性能比 SPA 更好。
  - 但 SPA 在后续页面加载方面有更好的性能和体验。因为 SPA 在完成首屏加载之后，在访问其它的页面时只需要动态加载页面的一部分组件，而不是整个页面。
  - 当页面发生跳转时，SPA 不会重新加载页面，对用户更友好。
- SEO
  - MPA 中服务端会针对每个页面返回完整的 HTML 内容，对 SEO 更加友好
- 路由
  - MPA 在浏览器侧其实不需要路由，每个页面都在服务端都有一份 URL 地址，浏览器拿到 URL 直接请求服务端即可。
  - SPA 则不同，它需要 JS 掌管后续所有路由跳转的逻辑，因此会引入一些路由方案来管理前端的路由，比如基于 hashchange 事件或者浏览器 history API 来实现。
- 状态
  - SPA引入一些规范和限制(比如 Redux 中的 action 机制)来提高项目可维护性。
  - 而 MPA 则会简单很多，因为每个页面之间都是相互独立的，不需要在前端做复杂的状态管理。

- MPA 和 SPA 也并不是完全割裂的，两者也是能够有所结合的，比如 SSR/SSG 同构方案就是一个典型的体现，
  - 首先框架侧会在服务端生成完整的 HTML 内容，并且同时注入客户端所需要的 SPA 脚本。
  - 这样浏览器会拿到完整的 HTML 内容，然后执行客户端的脚本事件的绑定(这个过程也叫 hydrate)，后续路由的跳转由 JS 来掌管。
  - 当下很多的框架都是采用这样的方案，比如 Next.js、Gatsby、公司内部的 Eden SSR、Modern.js。

- 👉🏻 把 MPA 和 SPA 结合的方案也并不是完美无缺的，主要的问题在于这类方案仍然会下载全量的客户端 JS 及执行全量的组件 Hydrate 过程，造成页面的首屏 TTI 劣化。

- 对于一个文档类型的站点，其实里面的大多数组件是不需要交互的，主要以静态页面的渲染为主，因此直接采用 MPA 方案是一个比 MPA + SPA 更好的一个选择
  - 由于页面中有时仍然不可避免的需要一些交互的逻辑，那放在 MPA 中如何来完成呢？这就是 Islands 架构所要解决的问题。
- Islands 架构模型早在 2019 年就被提出来了，并在 2021 年被 Preact 作者Json Miller 在 Islands Architecture 一文中得到推广。
  - 这个模型主要用于 SSR (也包括 SSG) 应用，我们知道，在传统的 SSR 应用中，服务端会给浏览器响应完整的 HTML 内容，并在 HTML 中注入一段完整的 JS 脚本用于完成事件的绑定，也就是完成 hydration (注水) 的过程。当注水的过程完成之后，页面也才能真正地能够进行交互。
- 当一个页面中只有部分的组件交互，那么对于这些可交互的组件，我们可以执行 hydration 过程，因为组件之间是互相独立的。
  - 而对于静态组件，即不可交互的组件，我们可以让其不参与 hydration 过程，直接复用服务端下发的 HTML 内容。

- 在 Astro 中，默认所有的组件都是静态组件
  - 有时我们需要在组件中绑定一些交互事件，那么这时就需要激活孤岛组件了，在使用组件时加上client:load指令即可
- Astro 是典型的 MPA 方案，不支持引入 SPA 的路由和状态管理。
  - 构建的时候，Astro 只会打包并注入 Islands 组件的代码，并且在浏览器渲染，分别调用不同框架(Vue、React)的渲染函数完成各个 Islands 组件的 hydrate 过程。

- Island 架构的实现其实是可以做到框架无关的。
- 从 SSR Runtime、Build Time 到 Client Runtime，整个环节中关于 React 的部分，我们都可以替换成其它框架的实现，这些部分包括:
  - 创建组件的方法
  - 组件转换为 HTML 字符串的 renderToString 方法
  - 浏览器端的 hydrate 方法

- VitePress 会在 hydrate 的过程中把正文的静态部分排除
- 由于 VitePress 采用的是 SSG + SPA 模式，其会根据是否为首屏来分发不同的 JS:
  - 首屏使用 .lean.js，不包含正文部分的 JS，实现 Partial Client Bundle + Partial Hydration，跟 Islands 架构一样的效果
  - 二次页面跳转使用完整的 JS，因为走 SPA 路由跳转，需要拿到完整的页面内容，用 JS 渲染出来。
- VitePress 利用 Vue 的编译时优化以及内部定制的 Hydrate 方案足以解决传统 SSG 的全量 hydration 问题，采用 Islands 架构意义并不大。
- 像 Vue 这种 Shell 优化方案对于包含编译时的前端框架是否通用？这里我们可以先大概总结出 Shell 方案需要满足的条件:
  - 模板编译阶段，将静态节点进行特殊标记
  - 运行时，支持 hydrate 跳过对静态节点的内容检查
- 基于上面这两点，其他的代表性编译时框架如Solid、Svelte 很难实现 Vue 的 Shell 架构(没法标记静态节点)，因此 Shell 方案可以理解为在 Vue 框架下的一个特殊优化了。
  - 对于 Vue 外的其它框架方案，仍然可以采用 Islands 进行特定场景的优化。

- https://github.com/childrentime/island-architecture
  - a demo of implementing the Island Architecture in React.
# discuss
- ## 

- ## 

- ## 

- ## 🧩 [A Gentle Introduction to SSR | Hacker News _202205](https://news.ycombinator.com/item?id=31224226)
- 
- 
- 

- ## 🚀 [Show HN: Vite-plugin-ssr – Do-one-thing-do-it-well alternative to Next.js / Nuxt | Hacker News _202210](https://news.ycombinator.com/item?id=33188372)
- How would you say it compares to Astro? Astro is currently either all-SSG or all-SSR, but this quarter they're working on configuring that per -route.
  - 1) Astro is either all-SSG or all-SSR, while VPS is mix-and-match
  - 2) Astro uses .astro templates by default, while VPS uses .js by default
  - 3) Astro comes out-of-the-box with Typescript, Sass, etc., while VPS requires more configuration (by design)
- VPS is tailored for users who like/want/need control. If you care about control, Astro isn't a good fit. E.g. you won't be able to use Astro with React Server Components. And many other subtleties that, in the end, sum up to a fundamentally different tool.

- What are the differences between this and the ssr in vite?
  - The process in that doc provide the primitives on which SSR can be built. Vite-plugin-ssr is one such implementation. It provides a rather "NextJS-like" experience out of the box. 

- ## 🆚️ [Nano JSX, Laravel, InertiaJS with SSR · nanojsx/nano](https://github.com/nanojsx/nano/discussions/75)
- SSR and hydrating to SPA (like you describe) will never be faster than SSR and partial hydration (how I use NanoJSX).
  - What makes a site fast, is less JavaScript. 
  - The point of Nano JSX is to ship as few bytes as possbile.
- Even if it seems that client-side routing (like in react) is fast. Low end phone and slow connections have to deal with 50+ KB before interacting with your site.
- SSR and partial hydration is basically how web development was few years ago. Render everything on the server and ship only the JavaScript needed for the current page.

- ## 一直不理解 SSR 的 Hydration 水合，看到 Next.js 的这个插图一下了就理解了。文档友好太重要了。
- https://twitter.com/hclj37/status/1623575951773687815
- hydration 的意思是将 SSR 生成出来的html 结构与原本的元数据一一对应起来并且激活其事件。
  - 嗯嗯，感谢分享。我再翻译成我的理解，就是把真实 DOM 和虚拟 DOM 对应起来，并绑定事件。
  - 是的，在《Vue.js设计与实现》一书有详细讲解，React 也是差不多的概念

- ## [React Streaming SSR/Server Components · TanStack/query](https://github.com/TanStack/query/discussions/4623)
- This post tries to outline a rough early draft API for integrating React Query with all the new React APIs while preserving a familiar API and trying to minimize the amount of new things RQ users needs to learn to leverage them, as well as outlining some todos to get there.

- ## [用了react 或者 vue，如何做SEO优化呢？](https://www.zhihu.com/question/51949678/answers/updated)
- 用 Vue 不代表你一定要做成 SPA
  - 对于真正适合做成 SPA 的应用，SEO 反而通常不是问题。
  - 你针对 marketing 的页面应该是静态分开部署的，app 本身则要登陆才能用，SEO 没有什么意义。
  - 少数既需要 SPA 强交互性，又对 SEO 和首屏速度有刚性需求的场景，这时候同构 SSR 就派上用场了。
- SEO的必要性
  - 事实就是这些前端框架最适应的场景就是管理平台，不需要做SEO。
  - 看自己的网站类型及团队架构情况，如果是需要登录才可以使用的，那么SEO意义不大

    - 最多首页放点静态文字和图片让搜索引擎收录即可。
    - 如果是非SPA的，且需要考虑搜索引擎的，要看自己的后端架构，如果是Node，react和vue都有方案。
    - 如果是其它的，可能不太好办，要么给搜索引擎的单独推一套（用户依然体验的是react、vue），要么就用传统的后端直接拍页面方式（放弃react、vue）。

  - seo或许是比较好的网站推广方式，但绝不是唯一的推广方式，还有其他的很多有效的办法的，

    - 以前老说seo是免费的，现在再看，成本已经很高了
    - SEO永远玩不过人民币玩家

  - 如果因为seo的一些限制而造成其他更有价值的东西没办法进展，那就舍弃seo呗

    - 一开始就打算用seo的话就尽量别用这些框架了 不然自己就坑死自己了

  - 比起日益昂贵的SEO，广告联盟反而因为越来越精准而划算
  - 静态信息网站的显示层，通常是直接渲染的，或者干脆就是静态页面。这样方便别人爬取数据。

    - 至于vue，只要用在后台和用户的操作就可以了。比如发布消息，点赞，回复等

- 不说需要维护两份工程，目前百度抓取程序在特定时候会伪装成正常用户，来浏览页面资源，受制于计算和存储资源，百度抓取程序并不能很好的解析JS，会造成站点被百度降低评级；
  - 另外维护一份爬虫白名单，这是个非常细碎的工作，需要UA+IP一起维护，而不是只是维护UA，这样就会非常麻烦。
  - 百度先用公开UA的爬虫来获取页面，然后可能会再模拟用户UA获取页面，如果不一致则判断作弊
  - 可以给用户种cookie，第一次进ssr，第二次就不进了。爬虫即使模拟用户的ua，肯定不会有cookie驻留的功能。
- 对 React 来说核心方法是 renderToString()。
  - 在服务端根据 url 拼出首屏内容发送给前端，到了前端之后就是 SPA 了。
  - 我常用的套装包括 express，react-router 和 redux。
  - 路由交给 react-router，用 redux 的 store 处理 SSR 中的前后数据交换。
  - 如果不用 redux，也有办法实现前后数据交换。原理是把数据拼成一个 JSON 字符串给前端去解析。

- ## SSR vs SSG
- 单页应用不容易实现SEO，近年业界针对此问题提供了两种解决方案：服务器端渲染（SSR）和静态站点生成（SSG）。
- 使用SSR，我们可以在服务器上运行应用程序，它创建由前端获取的HTML。
- 而使用SSG，我们可以在构建时创建应用程序的所有页面，由此，存储在服务器上的文件是静态的，并像标准的非SPA应用程序一样由浏览器获取。
- SSR的最大问题是，在服务器上构建应用程序会占用大量资源，而且速度可能很慢，因此会增加页面加载时间；
  - 而且，每个小的更改都需要重新构建和创建所有应用程序页面。
  - 如果应用程序有很多页面，则该过程很慢且成本很高。
- 现在看来，SSG赢了，SSR（几乎）死了。
  - Next.js是一个流行的全栈框架，将SSG设置为默认框架，并添加了增量构建，以缓解每次更改后重新构建所有页面的问题。
- 此外，像Gatsby这样的静态网站生成器会在其产品中添加增量构建。
- ref
  - https://www.zhihu.com/question/433673833/answer/1622039165
  - 我认为，ssg适合中小型应用，不适合超大型应用，

    - 问题在于若内容超级多，则增量构建也会花费大量时间，同时动态交互的计算量也很大

- ## [有必要使用服务器端渲染(SSR)吗？](https://www.zhihu.com/question/308792091/answers/updated)
- 现代框架的服务端渲染和 jsp、php 这些还是有不少区别的。
  - 因为 nextjs 和 nuxtjs 这种不仅仅是服务端渲染，它们还是同构框架。
  - 什么是同构呢？就是一份代码既可以跑在浏览器端，也可以跑在服务端。这得益于 NodeJS 在服务端的流行。
- 传统jsp、php、django这些服务端渲染框架都是返回html字符串，所以就会造成切换页面的时候重新刷新了，用户体验比较差。
  - 而现在流行的前端开发模式都是SPA，这些都是无刷新切换页面带来更好的用户体验。
- 所以 nextjs 和 nuxtjs 不仅支持服务端渲染，还支持 SPA，常用的是对首页进行服务端渲染，其他页面依然保持 SPA 的无刷新访问模式。
- 服务端渲染也不应该滥用。
  - 比如我们的内部后台管理系统就上了Nuxt，现在每次本地构建要花10分钟，非常影响开发效率。

- ## [为什么现在又流行服务端渲染html？](https://www.zhihu.com/question/59578433/answers/updated)
- 互联网市场像知乎、淘宝、视频等toC直接面向用户的站点 占据整体市场的份额并不多。
- 未来，更多的业务还是在于toB端服务型业务建设。
  - toB型业务不需要seo，不需要首屏渲染。要的是低成本开发ios、小程序多端并用
- 现在并没有真正的回归ssr，现在所说的ssr，是结合传统ssr+spa集两家之长。
  - 阿里前端为什么强势，因为他们给公司做了后台技术做不了的贡献。
  - 前后端团队矛盾冲突升级，说白了，就是部分后端开发人员不思进取，又发现被前端蚕食饭碗。
- 作者还是思维局限，没有看到诸多方向下驱动下来的选择，譬如运维成本，服务器资源成本，开发成本，沟通成本
  - 一个项目，要你开发出来pc应用，小程序，App。在传统模式下，你需要多少人？要开发多久？要多少钱？ 客户愿意给你多少钱？
  - 按照传统技术架构，服务端渲染服务端计算，亿万级的访问，需要假设多少服务器？部分计算渲染交给客户端，省了多少钱？
- SSR开发体验、可维护性(包括组件复用性)上的弊端十分明显，之所以至今还没消失是因为能解决某些业务模式的痛点
  - 比如虎扑这种强依赖搜索引擎流量的(spa + puppeteer预渲染 + 分离爬虫流量也能实现，但成本不比ssr低)；
  - 还比如对性能有极高要求的落地页(细微的载入速度差别就能带来营收上的巨大差异)。
  - 技术本质上是需要服务业务的，不管是它的诞生还是以后的发展反向。
- SPA发往浏览器的是一个很轻量的html，以及大体量的javascript，
  - 搜索引擎只能读取这有限的html，没法读取其他动态生成的URL，就很难爬到其他页面
  - 既然爬不到，那能不能直接告诉搜索引擎我有哪些URL呢？

    - 当然可以，如果你是网站的开发者，可以在搜索引擎的console上传sitemap（站点地图），直接通过一定的格式告诉搜索引擎，我这个Single-page application上面有哪些URL，
    - 不过无法读取动态生成的问题仍然存在。

  - 那能不能通过改革搜索引擎来解决呢？

    - 其实一些搜索引擎已经做了，比如googlebot，是支持读取动态生成html的，但是资源有限，不会让你无限地运行下去，对于异步fetch内容的部分，容易超时。
    - 所以服务器渲染才是解决SEO的根本。

  - 搜索引擎是怎么解析一大堆生成的html的呢？

    - 首先找有没有meta标签来描述网站
    - 没有的话就盲猜，比如你h1里面裹的大概是标题吧
    - 可以把meta部分服务器端渲染，然后其他部分依然动态生成，这也是很多大型网站在做的事情。

  - 如果这只是小网站，只有很少的开发者，不愿意搞服务器渲染怎么办？

    - 还有一个小技巧，就是Dynamic rendering
    - 加入中间件，识别这个request是浏览器发送的还是爬虫发送的，
    - 如果是浏览器发过来的，则正常返回，
    - 但如果是爬虫发送的，那就把渲染好的html发回去
    - 另外一个用服务端渲染的页面叫做"我支持的浏览器"，顾名思义，你用的浏览器太破了，无法支持浏览器渲染，请下载Chrome

- ## [Server Rendering in JavaScript: Why SSR?](https://dev.to/ryansolid/server-rendering-in-javascript-why-ssr-3i94)
- Next, Nuxt, Gatsby, Sapper have all been really popular the last few years along with the rise of JAMStack which promotes the use of Static Site Generation.
- But the thing you probably should be paying attention to is that the frameworks themselves have been investing heavily into this area for the past 2 years. 
  - There is a reason why we've been waiting for Suspense in React, or we see blog stories about Island's Architecture. 
  - Why Svelte and Vue have been pulling meta-framework type projects under their core's umbrella.

- **Why Server Rendering?**
- I mean there are plenty of ways to mitigate the initial performance costs of JavaScript. 
  - I had even made it my personal mission to show people that a well-tuned client only Single Page App(SPA) could outperform a typical Server Rendered SPA in pretty much every metric (even First Paint). 
  - And crawlers now can crawl dynamic JavaScript pages for SEO. 
- So what's the point?
  - Well even with crawlers now being fully capable to crawl these JavaScript-heavy sites, they do get bumped to a second-tier that takes them longer to be indexed. 
  - This might not be a deal-breaker for everyone but it is a consideration. 
  - And meta tags rendered on the page are often used for social sharing links. 
  - These scrapers are often not as sophisticated, so you only get the tags initially present which would be the same on every page losing the ability to provide more specific content.
  - But these are not new.
- So, let's take a look at what I believe are the bigger motivators for the current conversation.

- **Don't Go Chasing Waterfalls**
  - For dynamic client JavaScript pages like a SPA or even the dynamic parts of a static generated site, as you might create with a Gatsby or Next, often this means at least 3 cascading round trips before the page is settled.
  - The thing to note is this isn't only a network bottleneck. 
  - Everything here is on the critical path from parsing the various assets, to executing the JavaScript to make the async data request. 
  - None of this gets to be parallelized.
  - This is further compounded by the desire to keep the bundle size small. 
  - Code splitting is incredibly powerful and easy to do on route boundaries, but a naive implementation ends up like this:
    - Four consecutive round trips! 
    - The main bundle doesn't know what page chunk to request until it executes, 
    - and it takes loading and executing that chunk before it knows what async data to request.
- How does Server Rendering address this?
  - Knowing the route you are on lets the server render right into the page the assets you will need even if code split. 
  - You can add `<link rel="modulepreload" />` tags or headers that will start loading your modules before the initial bundle even parses and executes.
  - Additionally, it can start the async data loading immediately on receiving the request on the server and serialize the data back into the page. 
  - So while we can't completely remove the browser waterfalls we can reduce them to 1. 
- After Initial Load
  - Assets can be preloaded/cached with a service worker. 
  - JavaScript is even stored as bytecode so there is no parsing cost. 
  - Everything except the async data request is static and can already be present in the browser. 
  - There are no waterfalls, which is even better than the best case from server rendering.
- So the takeaway on this whole topic of performance/size is that the client alone has many techniques to mitigate most things other than that first load of fresh content.
  - That will always be constrained by the speed of the network.
  - But as our applications scale, without due consideration, it is easy for our SPA performance to degrade and a naive application of best practices only introduces other potential performance bottlenecks.

- **Modern Tools for Everyone**
- It's just JavaScript frameworks see this as a unique opportunity to create a completely isomorphic experience. 
- The fundamental thing client-side libraries have been solving is state management. 
  - It's the whole reason MVC architectures have not been the right match for the client. 
  - Something needs to be maintaining the state. 
  - MVC with its singleton controllers is wonderful for stateless things like RESTful APIs but needs special mechanisms to handle the persistence of non-model data. 
  - Stateful clients and stateless servers mean reloading the page is not acceptable.
- The challenge for server frameworks is even with mechanisms like Hotwire for partial updates, it alone doesn't make the client part of the equation any less complicated.
  - You can ignore it is a thing, and if your needs are meager this can suffice. 
  - Otherwise, you end up doing a lot of the same work anyway. 
  - This leads to essentially maintaining two applications.
  - This is why the JavaScript frameworks are uniquely positioned to provide this single universal experience. 
  - And why it is so attractive to framework authors.

- Server rendering in JavaScript is the next big race for these frameworks. 
  - But it's still up to you whether you choose to use it.

- ## [Server Rendering in JavaScript: Optimizing for Size_202101](https://dev.to/ryansolid/server-rendering-in-javascript-optimizing-for-size-3518)
- In this article, we will cover all things related to size. 
  - The amount of JavaScript you ship to the client can be heavy on the network, 
  - and it can be heavy on the CPU when you consider both parsing and execution.
- Conclusion
  - The thing to remember about size is, with pretty much every technique your mileage(好处，利益) will vary based on the nature of pages you have and the scale of the project. 
  - There are plenty of applications where these techniques are not worth the effort. 
  - Sometimes due to the framework. Sometimes due to a highly dynamic nature so there are minimal gains. 
  - Sometimes a different architecture is more beneficial and is simpler.
  - This is a pretty tricky thing to test/benchmark independently.
  -  So it might be best to look at examples holistically(整体的，全面的).

- ## [“Single-page” JS websites and SEO](https://stackoverflow.com/questions/7549306/single-page-js-websites-and-seo)
- In my opinion, SPA is done right by letting the server act as an API (and nothing more) and letting the client handle all of the HTML generation stuff. 
  - The problem with this "pattern" is the lack of search engine support. I can think of two solutions:

    - When the user enters the website, let the server render the page exactly as the client would upon navigation. 
    - Let the server provide a special website only for the search engine bots. 

- There are two ways to make sure a single page application is SEO friendly
  - Dynamic rendering is the easiest way. 

    - requests coming from bots are forwarded via a service that can execute JS and render your SPA into a plain HTML page readable by any search engine bot. 
    - This can be done using a headless browser. 
    - An example of such a service is Rendertron that uses headless Chrome. 
    - These days it's probably the best option, and you can easily install it on your server along with your web server (Apache, Nginx, or whatever you use).

  - Server-side rendering (SSR) may appear to be a bit more complicated. 

    - the pre-rendered SPA is also a plain HTML for search engines, 
    - but on the other hand, it's a fully functional application that can continue running once it's loaded into a browser. 
    - SSR probably brings no advantages for SEO compared to dynamic rendering. 
    - Still, a pre-rendered SPA may load faster for users, especially on a slow mobile device, because the device will not have to execute all JavaScript before the user sees the first page.

- ref
  - [SEO with single page application](https://stackoverflow.com/questions/30789799/seo-with-single-page-application)

- ## [google: Implement dynamic rendering for SEO](https://developers.google.com/search/docs/guides/dynamic-rendering)
  - Currently, it's difficult to process JS and not all search engine crawlers are able to process it successfully or immediately. 
  - we recommend dynamic rendering as a workaround solution to this problem.
  - **Dynamic rendering means switching between client-side rendered and pre-rendered content for specific user agents**.

    - Dynamic rendering is good for indexable, public JS-generated content that changes rapidly, or content that uses JS features that aren't supported by the crawlers you care about. 
    - Not all sites need to use dynamic rendering, and it's worth noting that dynamic rendering is a workaround for crawlers.

  - Dynamic rendering requires your web server to detect crawlers (for example, by checking the user agent).

    - Requests from crawlers are routed to a renderer, requests from users are served normally
    - Where needed, the dynamic renderer serves a version of the content that's suitable to the crawler, for example, it may serve a static HTML version. 
    - You can choose to enable the dynamic renderer for all pages or on a per-page basis.

  - Googlebot generally doesn't consider dynamic rendering as cloaking

    - As long as your dynamic rendering produces similar content, Googlebot won't view dynamic rendering as cloaking.
    - When you're setting up dynamic rendering, your site may produce error pages. 
    - Googlebot doesn't consider these error pages as cloaking and treats the error as any other error page.

  - Using dynamic rendering to serve completely different content to users and crawlers can be considered cloaking
  - To setup dynamic rendering for your content, follow our general guidelines. 

    - You will need to refer to your specific configuration details, as they vary greatly between implementations.
    - For a hands on approach, try our new Implement dynamic rendering with Rendertron codelab.
    - Install and configure a dynamic renderer to transform your content into static HTML that's easier for crawlers to consume. 
      - Some common dynamic renderers are Puppeteer, Rendertron, and prerender.io.
      - Rendertron  is an open source solution based on headless Chromium.
    - Choose the user agents that you think should receive your static HTML and refer to your specific configuration details on how to update or add user agents.
    - If pre-rendering slows down your server or you see a high number of pre-rendering requests, consider implementing a cache for pre-rendered content, or verifying that requests are from legitimate crawlers.

  - Configure your server to deliver the static HTML to the crawlers that you selected. 
  - There are several ways you can do this depending on your technology; 

    - Proxy requests coming from crawlers to the dynamic renderer.
    - Pre-render as part of your deployment process and make your server serve the static HTML to crawlers.
    - Serve static content from a pre-rendering service to crawlers.
    - Use a middleware for your server 

- ## [Choosing between client-side rendering, server-side rendering and static site generation for React apps_202101](https://blog.whereisthemouse.com/choosing-between-client-side-rendering-server-side-rendering-and-static-site-generation-for-react-apps)
- CSR vs SSR vs SSG
- CSR simply means that we are using Javascript to render the contents of our app in the browser.
  - Whenever someone visits our app in their browser, they would be able to only see the contents of the (almost empty) index.html file until the necessary Javascript is downloaded and executed. 
  - Afterwards, users will be able to both view and interact with the contents of our app.
- SSR means that we are using a server to render the contents of our HTML files and serve them to the client when requested. 
  - As with SSG, the user does not have to wait for the Javascript to be downloaded and executed before being able to view the page initially.
  - An important difference is that instead of having already generated static files, we are able to dynamically determine the content what is being served to the client. 
  - No rebuilds necessary. 
  - The trade-off is that what we gain in flexibility comes at the cost of an additional server and very possibly some added complexity compared to the other options.
- SSG. when we are creating a static site, we need all the contents and data of our app to be available upfront. 
  - The reason is that using SSG means we generate full-fledged HTML files already during the build step.
  - What we gain with this approach is that the user doesn't have to wait for any Javascript to download and execute before being able to see the initial content
  - On the flip side, needing all the data upfront also means that whenever a change is needed, we have to recreate and redeploy the entire build. 
  - This can quickly become cumbersome if frequent updates are needed.
- Decision time
- **SEO**
  - with CSR the initial HTML file is very minimal and Javascript is needed to render the app. This is bad for SEO.
  - By contrast, with both SSR and SSG, the initial HTML files already contain meaningful content. 
  - This makes them easily crawlable and indexable by search engines. 
  - In addition, creating page-specific link previews when sharing links on social platforms, for example, is trivial with SSR and SSG while downright impossible with CSR (unless we use a service like prerender.io to generate them).
  - Is SEO always a must? Not every app needs to be search engine optimized. 
- **Initial load time**
  - With both SSG and SSR we are able to show initial meaningful HTML on the screen.

    - Even though users cannot immediately interact with it (we need Javascript for that), the perception is that the app loads quickly
    - with the use of a CDN, statically generated sites would probably perform better than SSR since the content is already generated and cached. 
    - However, we also run the risk of it being stale at request time.

  - using CSR means that all the users see is the empty HTML file (or, at best, a loading screen) until the necessary Javascript is downloaded, executed and able to render the content of the app. 

    - This might give users the initial impression that the app is too slow.

- **Dynamic content**
  - how dynamic is the content of the website we are building
  - One of the main drawbacks of the SSG approach is that in order to update the content of the app, we need to rebuild it.

    - This might be perfectly fine if the app consists of mostly static content and is not frequently updated. 
    - A good use case for SSG would be a personal blog or a marketing website

  - With CSR, we are able to fetch the necessary data for the specific user on the client, display it and seamlessly keep it up to date.
  - What if we are building a news site, where the content is both public and constantly updated. 

    - What if, in addition, there is some user generated content involved like comments under the articles, for example? 
    - It would be much preferable to take advantage of SSR instead, with its ability to serve dynamic, non-stale, search engine optimized HTML files and easily reflect updates upon each request.

- **Infrastructure**
  - Probably the simplest approach to deployment is if our app build consists of static files. 

    - This means we could directly deploy it on a CDN service and our website would be live. 
    - With both CSR and SSG this is exactly the case.

  - Using SSR paradigm means we need a server to pre-render the page into HTML on every request. 

    - it is important to keep in mind that as the number of users for our app increases, the infrastructure cost might increase with it.

- As usual, there is no one size fits all solution. 
  - The choice should always be determined by our particular use case.
  - There is also the possibility to mix and match these approaches for different parts of our app
# ref
- [google: Deprecating our AJAX crawling scheme_201510](https://developers.google.com/search/blog/2015/10/deprecating-our-ajax-crawling-scheme)
  - We are no longer recommending the AJAX crawling proposal we made back in 2009.
  - In 2009, we made a proposal to make AJAX pages crawlable. 
  - Today we are generally able to render and understand your web pages like modern browsers. 
  - Serving Googlebot different content than a normal user would see is considered cloaking(隐蔽欺骗), and would be against our Webmaster Guidelines.
- [How do you use React.js for SEO?](https://stackoverflow.com/questions/28252768/how-do-you-use-react-js-for-seo)
