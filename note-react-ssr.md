---
title: note-react-ssr
tags: [react, ssr]
created: 2023-05-08T14:48:31.220Z
modified: 2023-05-08T14:48:55.886Z
---

# note-react-ssr

# guide

# dev
- 数据的注水与脱水
  - 注水指的是服务端请求数据后，将数据传递给客户端，
  - 脱水就是客户端使用数据的过程。
# blogs

## [说说React-SSR的原理](https://www.cnblogs.com/beifeng1996/p/16894687.html)

- 所谓同构，简而言之就是，第一次访问后台服务时，后台直接把前端要显示的界面全部返回，而不是像 SPA 项目只渲染一个 `<div id="root"></div>` 剩下的都是靠 JavaScript 脚本去加载。这样一来可以大大减少首屏等待时间。

- 客户端渲染的优劣势
- 优势：
  - 前端负责渲染页面，后端负责实现接口，各自干好各自的事情，对开发效率有极大的提升；
  - 前端在跳转界面的时候不需要请求后台，加速了界面跳转的速度，提高用户体验。
- 劣势：
  - 由于需要等待 JS 文件加载以及后台接口数据请求因此首屏加载时间长，用户体验较差；
  - 由于大部分内容都是通过 JS 加载因此搜索引擎无法爬取分析网页内容导致网站无法 SEO 。

- SSR 是服务端渲染技术，它本身是一项比较普通的技术， Node.js 使用 ejs 模板引擎输出一个界面这就是服务端渲染。
  - 每次访问一个路由都是请求后台服务，重新加载文件渲染界面。
  - 服务端渲染的本质就是页面显示的内容是服务器端生产出来的。
- 优势：
  - 整个 HTML 都通过服务端直接输出 SEO 友好；
  - 加载首页不需要加载整个应用的 JS 文件，首页加载速度快。
- 劣势：
  - 访问一个应用程序的每个界面都需要访问服务器，体验对比 CSR 稍差。

- 我们会发现一件很有意思的事，服务端渲染的优点就是客户端渲染的缺点，服务端渲染的缺点就是客户端渲染的优点，反之亦然。
  - 那为何不将传统的纯服务端直出的首屏优势和客户端渲染站内跳转优势结合，以取得最优解？
  - 这就引出了当前流行的服务端渲染（ Server Side Rendering ），或者称之为“同构渲染”更为准确。

- 所谓同构，通俗的讲，就是一套 React 代码在服务器上运行一遍，到达浏览器又运行一遍。
  - 服务端渲染完成页面结构，客户端渲染绑定事件。
  - 它是在 SPA 的基础上，利用服务端渲染直出首屏，解决了单页面应用首屏渲染慢的问题。
- 💡 服务端 ReactDOMServer.renderToString
  - 客户端 ReactDOM.hydrate

- `ReactDOM.hydrate(<Home/>,document.getElementById("root"));` 入口
  - hydrate 与 render() 相同，但它用于在 ReactDOMServer 渲染的容器中对 HTML 的内容进行 hydrate 操作。 
  - React 会尝试在已有标记上绑定事件监听器。

- ReactDOMServer.renderToString(element)
  - 将 React 元素渲染为初始 HTML 。 React 将返回一个 HTML 字符串。你可以使用此方法在服务端生成 HTML ，并在首次请求时将标记下发，以加快页面加载速度，并允许搜索引擎爬取你的页面以达到 SEO 优化的目的。
- 为什么服务端加载了一次，客户端还需要再次加载呢？
  - renderToString 并没有做事件相关的处理，因此返回给浏览器的内容不会有事件绑定，渲染出来的页面只是一个静态的 HTML 页面。
  - 只有在客户端渲染 React 组件并初始化 React 实例后，才能更新组件的 state 和 props ，初始化 React 的事件系统

- 让我们更加深入的学习它，手写一个同构框架，彻底理解同构渲染的原理。
- 同构项目中当在浏览器中输入 URL 后，浏览器是如何找到对应的界面？
  - 浏览器收到 URL 地址例如： http://localhost:3000/login ；
  - 后台路由找到对应的 React 组件传入到 renderToString 中，然后拼接 HTML 输出页面；
  - 浏览器加载打包后的 JS 文件，并解析执行前端路由，输出相应的前端组件，发现是服务端渲染，因此只做事件绑定处理，不进行重复渲染，此时前端路由路由开始接管界面，之后跳转界面与后台无关。

- 服务端如何可获取到数据？既然 useEffect 不会在服务端执行，那么我们就自己创建一个 “Hook” 。
  - 在 Next.js 中 getInitialProps 就是这个被创建的 “Hook” ，它的主要职责就是使服务端渲染可以获取初始化数据。
  - 在 getInitialData 中做的事情同 useEffect 相同，都是去发送后台请求获取数据。

- 明明服务器已经拿到数据了为什么刷新浏览器会一闪一闪呢，原因在于，客户端渲染接管时，初始化的用户列表依然是个空数组，通过发送后台请求获取到数据这个异步过程，导致的页面一闪一闪的。它的解决方案有一个术语叫做数据的脱水与注水。
  - 在渲染服务端时，已经拿到了后台请求数据，通过 INITIAL_STATE 全局变量把后台请求到的数据存起来。客户端创建 store 时，当做初始化的 state 使用即可

- 总结
  - 同构渲染其实就是将同一套 react 代码在服务端执行一遍渲染静态页面，又在客户端执行一遍完成事件绑定。
  - 优势是，加快首页访问速度以及 SEO 友好，如果你的项目没有这方面的需求，则不需要选择同构。
  - 缺点是，不能在服务端渲染期间操作 DOM 、 BOM 等 api ，比如 document 、 window 对象等，并且它增加了代码的复杂度，某些代码操作需要区分运行环境。

## [React Streaming SSR 原理解析](https://www.cnblogs.com/ClientInfra/p/17022997.html)

- React 18 提供了一种新的 SSR 渲染模式： Streaming SSR。
- Streaming HTML
  - 服务端可以分段传输 HTML 到浏览器，而不是像 React 18 以前一样，需要等待服务端渲染完成整个页面后才返回给浏览器。这样，浏览器可以更快的启动 HTML 的渲染，提高 FP、FCP 等性能指标。
  - HTTP 支持以 stream 格式进行数据传输。当 HTTP 的 Response header 设置 `Transfer-Encoding: chunked` 时，服务器端就可以将 Response 分段返回
- Selective Hydration
  - 在浏览器端 hydration 阶段，可以只对已经完成渲染的区域做 hydration，而不需要等待整个页面渲染完成、所有组件的 JS  bundle 加载完成，才能开始 hydration。
  - 这样可以更早的对已经完成渲染的区域做事件绑定，从而让页面获得更好的可交互性。

- 总结一下 ， React Streaming SSR ，会先传输所有  以上层级的可以同步渲染得到的 html 结构，当  内的组件渲染完成后，会把这部分组件对应的渲染结果，连同一个 JS 函数再传输到浏览器端，这个 JS 函数会更新 dom ，得到最终的完整 HTML 结构。
  - 只有当 的 children，需要被异步渲染时，SSR 返回的 HTML 才会被分段传输。

- React 18 之前，SSR 实际上是不支持 code splitting 的，只能使用一些 workaround，常见的方式有：
  - 1. 对于需要 code splitting 的组件，不在服务端渲染，而是在浏览器端渲染；
  - 2. 提前将 code splitting 的 JS 写到 html script 标签中，在客户端等待所有的 JS 加载完成后再执行 hydration。
- 当前 Modern.js 对于这种情况的处理，采用的是第 2 种方式。Modern.js 利用 @loadable/component 在 SSR 阶段，收集做了 code splitting 的组件的 JS bundle，然后把这些 JS bundle 添加到 html script 标签中，@loadable/component 提供了一个 API loadableReady ，在等待 JS bundle 加载完成后，才执行 hydration 。

- 总结一 下，React 18 的 hydration 阶段，当渲染到 Suspense 组件时，会根据 Suspense 的 children 是否已经渲染完成，而选择是否继续向子组件执行 hydration。未渲染完成的组件待渲染完成后，会恢复执行 hydration。 Suspense 的 children 异步渲染的两种场景：1. children 组件做了 code splitting；2. children 组件中有异步操作。

## [React SSR 全流程原理：从 renderToString 到 hydrate - 知乎](https://zhuanlan.zhihu.com/p/622415299)

- ssr是一项很古老的技术，很早之前服务端就是通过 JSP、PHP 等模版引擎，渲染填充数据的模版，产生 html 返回的。只不过这时候没有组件的概念。
- 同样的组件在服务端渲染了一次，在客户端渲染了一次，这种可以在双端渲染的方式，叫做同构渲染。
- 服务端渲染组件为 string，拼接成 html 返回，浏览器渲染出返回的 html，然后执行 hydrate，把渲染和已有的 html 标签关联。
- 服务端renderToString就是拼接 html 的过程，组件和元素分别有不同的渲染逻辑：
  - 组件的话就传入参数执行
  - 元素的话就拼接字符串
  - 这样递归渲染一遍，结果就是字符串了
- 客户端渲染的 hydrate 部分
  - 我们也经常把 React Element 叫做 vdom
  - react 会把 vdom 转成 fiber 的结构，依次处理不同 React Element 转 fiber，这个过程也是reconcile
  - reconcile 的过程分为 beginWork 和 completeWork 两个阶段，beginWork 从上往下执行不同类型的 React Element 的渲染，而 completeWork 正好反过来，依次创建元素、更新属性，并组装起来。
  - hydrate 会在 beginWork 的时候对比当前 dom 是不是可以复用，可以复用的话就直接放到 fiber.stateNode 上了。
- React SSR 是服务端通过 renderToString 把组件树渲染成 html 字符串，浏览器通过 hydrate 把 dom 关联到 fiber 树，加上交互逻辑和再次渲染。
- 服务端 renderToString 就是递归拼接字符串的过程，遇到组件会传入参数执行，遇到标签会拼接对应的字符串，最终返回一段 html 给浏览器。
- 浏览器端 hydrate 是在 reconcile 的 beginWork 阶段，依次判断 dom 是否可以复用到当前 fiber，可以的话就设置到 fiber.stateNode，然后在 completeWork 阶段就可以跳过节点的创建。

## more-ssr

- [现代前端框架的渲染模式 - 掘金](https://juejin.cn/post/7241027834490437669)
# blogs-seo

## [浅谈：SPA 及其 SEO 优化方案](https://github.com/jtwang7/React-Note/issues/36)

- SSR 服务端渲染
  - 将组件或页面通过服务器生成 html，再返回给浏览器，如 nuxt.js，next.js 等。
- 静态化
  - 目前主流的静态化主要有两种：
  - （1）一种是通过程序将动态页面抓取并保存为静态页面，这样的页面的实际存在于服务器的硬盘中
  - （2）另外一种是通过WEB服务器的 URL Rewrite的方式，它的原理是通过web服务器内部模块按一定规则将外部的URL请求转化为内部的文件地址，一句话来说就是把外部请求的静态地址转化为实际的动态页面地址，而静态页面实际是不存在的。
  - 这两种方法都达到了实现URL静态化的效果
- 使用Phantomjs针对爬虫处理
  - 原理是通过 Nginx 配置，判断访问来源是否为爬虫，如果是则搜索引擎的爬虫请求会转发到一个 node server，再通过 PhantomJS 来解析完整的 HTML，返回给爬虫。

## [Single Page Application: Dispelling SEO Myths | HackerNoon](https://hackernoon.com/single-page-application-dispelling-seo-myths)

- Request Indexing
- In this section, we’ll ask Google to:
  - Confirm that each SPA page can be indexed, 
  - Accept a request to index each SPA page.
- Both confirmation and acceptance will be obtained by using Google URL Inspection Tool which is a part of GSC.

- Now let’s switch from a plain SPA to the one with the landing page prerendered. 
  - Crisp React builds such SPA to combine landing page prerendering with CSR for other pages.

- ### [How to achieve SEO for React SPA without SSR or prerendering](https://stackoverflow.com/questions/70390808/how-to-achieve-seo-for-react-spa-without-ssr-or-prerendering-and-preferably-kee)
- The answer is meant to demonstrate an easily reproducible set of steps to get a React SPA indexed by Google without any need of SSR or prerendering. 
- It's split into two parts with headings:
  - Website Deployment
  - Requesting Google to Index the Website
- The first part is all about building a deploying a sample React application. 
  - Only one bullet point (that deals with title and canonical) is specific to SEO.
- The second part is all about SEO, however it's not specific to SPA or React.

> Requesting Google to Index the Website

- You can choose either passive(消极的；被动的) approach and simply wait until Googlebot discovers your website or proactively(主动的，抢先的) ask Google to index it. 
  - If you choose the latter, use Google Search Console (GSC)

## more-seo

- [用了react 或者 vue，如何做SEO优化呢？ - 知乎](https://www.zhihu.com/question/51949678/answers/updated)
  - SEO有个最基本的要求，就是相关内容（例如：信息流的列表部分，或者新闻的正文部分），必须对搜索引擎的爬虫可见。
  - 千万别针对爬虫，单独写另外一套页面。也就是爬虫看到的和用户看到的不一样。这就是搜索引擎明确禁止的作弊。会带来搜索引擎的惩罚和降权。
# discuss
- ## 
# more
