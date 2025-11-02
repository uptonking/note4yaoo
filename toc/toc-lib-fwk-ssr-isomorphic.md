---
title: toc-lib-fwk-ssr-isomorphic
tags: [isomorphic, server-side-rendering, ssr, web]
created: 2020-11-22T13:29:51.265Z
modified: 2020-12-19T13:04:40.865Z
---

# toc-lib-fwk-ssr-isomorphic

# guide
- tips
  - 产品开发前进行技术选型时要多分析使用场景，ssr和csr的技术栈本身就是不同的，jsx只是view层，服务端要考虑routing/cache/streaming/i18n
  - 一般ssr方案都会提供自己的router, nextjs将file-based-routing作为卖点
  - 没必要寻找前后端通用的router，前端、后端框架都有自己的，routing常和prefetch耦合
  - 有的方案支持首屏ssr，之后spa，基于不同的render mode
# ssr
- https://github.com/vikejs/vike /5.2kStar/MIT/202511/ts
  - https://vike.dev/
  - https://vike.land/
  - Like Next.js/Nuxt but as do-one-thing-do-it-well Vite plugin.
  - The `vite-plugin-ssr` project has been renamed Vike
  - do-one-thing-do-it-well architecture: Vike focuses on being an excellent frontend framework while not interfering with the rest of your stack.
    - 💄 Any UI framework (React/Vue/Solid/...)
    - Any server (Express.js, Deno, HatTip, ...)
    - Any deployment (AWS, Cloudflare Workers, Vercel, ...)
  - Filesystem Routing, Data fetching, Pre-rendering, Layouts, HMR, i18n, Link Prefetching, HTML Streaming.
  - ✨ All render modes: SSR, SPA, MPA, SSG, HTML-only. Each page can use a different mode.
  - [Vike + a different bundler other than Vite? (Farm, RsPack) _202407](https://github.com/vikejs/vike/discussions/1737)
    - Actually, the vast majority of Vike's logic is Vite agnostic (more than 99%). So, in principle, making Vike bundler agnostic is much easier than it seems. That said, there is still a lot of glue code so it's a significant endeavour.
    - So, yea, while it's possible to make Vike bundler agnostic it clearly isn't a priority for now.
  - 🆚️ [Comparison with NextJS _202110](https://github.com/vikejs/vike/issues/158)
    - you can use other rendering frameworks, not only React
    - development speed is better because is Vite based plugin (no bundling, native ESM)
    - you can use every possible routing library
  - [Show HN: Vite-plugin-ssr – Do-one-thing-do-it-well alternative to Next.js/Nuxt | Hacker News _202210](https://news.ycombinator.com/item?id=33188372)

- https://github.com/ElMassimo/iles /MIT/202309/ts
  - https://iles.pages.dev/
  - The joyful site generator
  - îles — french word for "islands". 
  - Partial Hydration - zero JS by default, hydrates the interactive bits
  - 🎨 Multi-Framework - vue, preact, svelte, solid
  - Fast - instant reloading powered by Vite
  - Routing - automatically configured from files
  - https://iles-docs.netlify.app/faqs
    - With iles the page is pre-rendered just like in server-side rendering, but JS is automatically added for the interactive bits, more optimal than hydrating the entire page.
    - VitePress has an MPA mode to strip away all JS. In iles that happens automatically if you don't use hydration directives.
  - [question: purpose of this library _202110](https://github.com/ElMassimo/iles/issues/5)
    - The main difference is that îles provides great support partial hydration, so you can ship JS only for the interactive parts of the page by simply adding `client:` directives. In Vitepress partial hydration is still a manual process.
    - It's easier to build blogs in îles than in Vitepress, and if you need a SPA you would go with Vitepress.

- https://github.com/beenotung/ts-liveview /BSD/202402/ts
  - https://liveviews.cc/
  - Build hybrid SSG and SSR realtime SPA/MPA with Typescript
  - ts-liveview supports JSX but it doesn't rely on Virtual DOM. Instead, precise DOM operations are derived from application-specific event handlers, and sent to the browser client(s) for realtime UI updates.
  - Support hybrid rendering mode: pre-rendering, Request-time server-rendering with HTML streaming
  - Support url-based routing architectures
  - Enable interactive UI with minimal amount of javascript to be downloaded
  - Support to develop with JSX, AST, or html template
  - Lightweight WebSocket-based protocols 
  - Built-in locale support (language and timezone)
  - Inspired from Phoenix LiveView, htmx
  - https://github.com/tylerbarker/phoenix_ts /202405/ts
    - The unofficial TypeScript client for the Phoenix web framework - WIP
    - [LiveView Is Not a Zero-JS Framework, It’s a Zero-Boring-JS Framework - Tyler Barker _202406](https://tylerbarker.com/posts/liveview-is-not-a-zero-js-framework-it-s-a-zero-boring-js-framework)

- https://github.com/floodfx/liveviewjs /646Star/MIT/202303/ts/inactive
  - https://www.liveviewjs.com/docs/overview/introduction
  - LiveViewJS is an open-source framework for "LiveView"-based, full-stack applications in NodeJS and Deno.
  - The LiveView pattern, as popularized in Elixir’s Phoenix framework, shifts your UI’s state management, event handling to the server, calculating minimal diffs to drive updates in your HTML over WebSockets.
  - a LiveView is a server-rendered HTML page that, when loaded, connects back to the server via a persistent web socket. As the user interacts with the LiveView, the client to sends user events (click, keys, etc) via the websocket back to the server and the server responds with diffs to the HTML page in return.
  - LiveViewJS is a protocol compliant, implementation of Phoenix LiveView but written in Typescript and runs on NodeJS and Deno. We want to bring the magic and productivity of LiveView to the NodeJS and Deno ecosystems

- https://github.com/plantain-00/router-demo
  - Multiple-application SPA and SSR demo

- https://github.com/kapouer/express-dom /js
  - Express middleware for (pre)rendering web pages with playwright.

- https://github.com/nanojsx/nano /MIT/202401/ts
  - http://nanojsx.io/
  - SSR first, lightweight 1kB JSX library.
  - Partial Hydration: Hydrate and only the parts you really need
  - Pre-Rendering: Renders your app to static html if you want. This is possible, but requires some knowledge.
  - Isomorphic Router Works on Client- and Server-Side
  - Uses Tagged Templates instead of JSX if you prefer
  - Prefetch: Use the built-in Link Component
  - ❓ 不支持streaming, 不支持spa
  - [Nano JSX, Laravel, InertiaJS with SSR _202112](https://github.com/nanojsx/nano/discussions/75)

- https://github.com/inertiajs/inertia /MIT/202311/ts
  - https://inertiajs.com/
  - Inertia.js lets you quickly build modern single-page React, Vue and Svelte apps using classic server-side routing and controllers. 
  - Inertia works great with any backend framework, but it's fine-tuned for Laravel.
  - Inertia isn't a framework, nor is it a replacement for your existing server-side or client-side frameworks. Rather, it's designed to work with them
  - https://discord.com/channels/592327939920494592/758259460920573992/1204350428708339773
    - Inertia SSR is an addition, not a conversion/replacement
  - [How it works - Inertia.js](https://inertiajs.com/how-it-works)
    - At its core, Inertia is essentially a client-side routing library. It allows you to make page visits without forcing a full page reload. 
    - This is done using the `<Link>` component, a light-weight wrapper around a normal anchor link. 
    - When you click an Inertia link, Inertia intercepts the click and makes the visit via XHR instead. 
    - You can even make these visits programmatically in JavaScript using `router.visit()`.
    - When Inertia makes an XHR visit, the server detects that it's an Inertia visit and, instead of returning a full HTML response, it returns a JSON response with the JavaScript page component name and data (props). 
  - [Server-side rendering (SSR) - Inertia.js](https://inertiajs.com/server-side-rendering)
    - Server-side rendering pre-renders your JavaScript pages on the server, allowing your visitors to receive fully rendered HTML

- https://github.com/pmb0/express-tsx-views /MIT/202110/ts/inactive
  - Server-side JSX/TSX rendering for your express or NestJS application
  - With this template engine, TSX files can be rendered server-side by your Express application. 
  - Unlike other JSX express renderers, this one does not rely on JSX files being transpiled by `babel` at runtime. Instead, TSX files are processed once by the `tsc` compiler.
  - For this to work, the templates are imported dynamically during rendering. 
- https://github.com/redexp/express-engine-jsx /MIT/202309/js
  - JSX engine for ExpressJS
  - this component can be rendered to html with `ReactDOM.renderToStaticMarkup()`.

- https://github.com/reactjs/express-react-views /201810/js
  - an Express view engine which renders React components on server.
  - It renders static markup and does not support mounting those views on the client.
  - This is intended to be used as a replacement for existing server-side view solutions, like jade, ejs, or handlebars.
  - This package is no longer maintained. I recommend Next.js or Remix.
  - https://github.com/geemaple/react-server-rendering-example
    - An example of React server-side rendering with express-react-views view engine
  - https://github.com/magalhas/express-react-engine /201704/js

- https://github.com/paypal/react-engine /apache2/201802/js/archived
  - a react render engine for Universal (previously Isomorphic) JavaScript apps written with express
  - renders both plain react views and optionally react-router views
  - enables server rendered views to be client mountable

- https://github.com/airbnb/hypernova /MIT/202204/js/archived
  - A service for server-side rendering your JavaScript views
  - we are no longer using this technology internally
  - https://github.com/ara-framework/hypernova-preact
  - https://github.com/ara-framework/hypernova-hyperapp

- https://github.com/PaulBlanche/frugal /202308/ts
  - https://frugal.deno.dev/
  - Frugal is a hybrid, dynamic and static site generator that aims to minimize the amount of JavaScript served, thanks to partial hydration
  - Static pages rendered at build time: by default Frugal produces static html.
  - Server side pages render at request time
  - Bring your own framework: Frugal works with any UI framework able to compile to html
  - Manual partial hydration for interactive island in pages if you use Preact
  - Incremental build: if both data and code did not change, the page is not rebuilt

## solutions

- https://github.com/yusukebe/hono-spa-react/tree/cloudfare-vite-plugin
  - Hono app renders HTML with React SSR and serves API. The React client will be inserted in the HTML. The Plugin emulates Cloudflare environment.

- https://github.com/janishar/react-app-architecture /ts/inactive
  - Learn to build a complete website for a blogging platform like Medium; OpenSource project by AfterAcademy
  - Isomorphic React web app: The server sends the rendered pages to the client, and then the client renders the subsequent pages on its own. This is a very important feature for SEO and it also makes the first paint super fast.

- https://github.com/vercel/next.js
  - Next.js gives you the best developer experience with all the features you need for production with no config needed.
  - hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. 
  - Pre-render pages at build time (SSG) or request time (SSR) in a single project
  - Every component in the pages directory becomes a route.
  - Optionally create API endpoints to provide backend functionality.

- https://github.com/styfle/react-server-example-tsx
  - https://react-tsx.now.sh/
  - A complex example of how to do server-side rendering with React and TypeScript so that component code can be shared between server and browser (also known as isomorphic javascript).
  - 只依赖react、webpack

- https://github.com/catamphetamine/universal-webpack
  - Isomorphic Webpack: both on client and server
  - https://github.com/catamphetamine/webpack-react-redux-server-side-render-example

- https://github.com/danielstern/isomorphic-react
  - Supports hot reloading and server rendering!
  - Uses React/Redux as main application engine

- https://github.com/redfin/react-server
  - React framework with server render for blazing fast page load and seamless transitions between pages in the browser.
  - React Server is now defunct. Consider Next.js instead.

- https://github.com/alibaba/beidou
  - Isomorphic framework for server-rendered React apps

- https://github.com/zhangyuang/ssr /MIT/202402/ts
  - https://doc.ssr-fc.com/docs/why
  - 此框架脱胎于 egg-react-ssr 项目和 ssr v4版本（midway-faas + react ssr），在之前的基础上做了诸多演进，
  - 通过插件化的代码组织形式，支持任意服务端框架与任意前端框架的组合使用，(Serverless/Midway/NestJS) + (React/Vue2/Vue3)
  - 功能丰富，UI 框架、代码分割、HMR、TS、Serverless、SSR 降级 CSR 开发所需要的功能应有尽有
  - 🧐 core无依赖，但view层的依赖很多, 依赖webpack4
  - 支持返回 Stream
  - 不内置服务端模块, ssr 框架默认提供的示例就是与业界最优秀的两个 Node.js 框架的示例结合。且 ssr 框架仅抛出一个逻辑非常清晰的渲染函数供服务端框架调用，兼容 koa, express 系的所有框架
  - 支持四种渲染模式, 支持服务端渲染与客户端渲染两种模式任意切换。随时安全降级。支持 SSG(预渲染) 能力同时支持生成传统骨架 html 文件独立部署
  - 没有使用类似于 nunjucks ejs 这种模版引擎，根据场景 All in JSX 或者 Vue SFC 来编写 html 布局
  - [Webpack最优化问题 _202306](https://github.com/zhangyuang/ssr/issues/296)
    - 不考虑升 webpack5
  - [可以升级到webpack5吗？ _202207](https://github.com/zhangyuang/ssr/issues/223)
    - 没有升级webpack5的打算，and 微前端搜文档，不看好一切用模块联邦实现的微前端方案

- https://github.com/ykfe/egg-react-ssr
  - 小而美的Egg + React + SSR 服务端渲染应用骨架，同时支持JS和TS
  - 实现方式简洁，生产环境构建出来的bundle为同等复杂度的 next.js 项目的 0.7 倍，生成文件数量相比于 next.js 减少非常多
  - 支持 HMR，支持本地开发以及生产环境 CSR/SSR 两种渲染模式无缝切换
  - [与next.js实现方案的对比](https://github.com/ykfe/egg-react-ssr/wiki/%E4%B8%8Enext.js%E5%AE%9E%E7%8E%B0%E6%96%B9%E6%A1%88%E7%9A%84%E5%AF%B9%E6%AF%94)
    - next.js本地开发读取服务端bundle采用的方式是
      - 将bundle以开发环境的模式构建到本地，
      - 在每次源码有变动时在本地生成新的服务端bundle，
      - 使用hot-middleware + dev-middleware + fs 实现。
    - 本应用是直接采用webpack --watch + inline-sourcemap 的方式将文件写到本地，实现更加简洁。
    - next.js hmr采用hot-middleware + webpackHotDevClient.js实现
    - 本应用hmr直接用社区的热门库webpack-dev-server实现

- https://github.com/FormidableLabs/react-ssr-prepass
  - A custom partial React SSR renderer for prefetching and suspense
  - react-dom/server does not have support for suspense yet.
  - react-ssr-prepass is a partial server-side React renderer that does a prepass on a React element tree and suspends when it finds thrown promises.

- https://github.com/theninthsky/client-side-rendering
  - https://client-side-rendering.pages.dev/
  - a case study of CSR, it aims to explore the potential of client-side rendered apps compared to server-side rendering.

- https://github.com/Lucifier129/react-imvc
  - An Isomorphic MVC Framework supports both SSR and CSR
  - MVC 三者都是 Isomorphic，既是服务端 MVC，也是浏览器端 MVC。
  - https://github.com/Lucifier129/isomorphic-cnode

- https://github.com/next-boost/next-boost /202206/ts/inactive
  - next-boost adds a cache layer to your SSR (Server-Side Rendering) applications. 
  - It was built originally for Next.js and should work with any node.js `http.Server` based application.
  - achieves great performance by rendering webpages on `worker_threads` while serving the cached on the main thread.
  - If you are familiar with Next.js, next-boost can be considered as an implementation of Incremental Static Regeneration which works with getServerSideProps. And it's not meant to be used with getStaticProps, in which Next.js will do the cache for you.
  - Drop-in replacement for Next.js's production mode
# ssr-react
- https://github.com/fusionjs/fusionjs /MIT/202303/ts/inactive
  - Modern framework for fast, powerful React apps
  - Uber’s open source universal web framework, represents the fusion of the client and the server. 
  - It's geared for server-side rendering out of the box, and its plugin-driven architecture allows for complex frontend and backend logic to be encapsulated in a single plugin
  - Because Fusion.js applications are universal, which means that apps have a single entry point, all code from React components to middlewares in Fusion.js plugins by default runs on both the server and browser.

- https://github.com/rakkasjs/rakkasjs /MIT/202402/ts
  - a bleeding-edge full-stack React framework powered by Vite. 
  - You can consider it an up-and-coming alternative to Next.js, Remix, or Gatsby.
  - Rakkas is fairly opinionated. If you need more flexibility, try vite-ssr-plugin/vike.

- https://github.com/electrode-io/electrode
  - Web applications with node.js and React
  - universal webapp with server side rendering powered by node.js
  - https://github.com/electrode-io/electrode-native
    - A platform to ease integration&

- https://github.com/htdangkhoa/react-ssr-starter /js/inactive
  - A React boilerplate for a universal web app with a highly scalable, offline-first foundation 
  - our focus on performance and best practices.
  - Using SWC will give build times 1.5x faster for the server and 2.2x for the client instead of using Babel.

- https://github.com/panDaxiang/ssr
  - react服务端渲染demo

- https://github.com/winwiz1/crisp-react /202201/ts
  - Crisp React can optionally split a monolithic React app into multiple Single Page Applications (SPAs) and selectively prerender the landing/index page of any SPA at the build time.
  - Helps to split a monolithic React app into multiple SPAs and avoid vendor lock-in.
  - in each SPA the routing is managed by a separate instance of React Router 
  - By default SSR is enabled for the first SPA and disabled for the second SPA.
  - On the contrary to popular belief that SEO requires SSR, this solution innovatively demonstrates how to get all SPA pages indexed by Google and specific
  - [How to achieve SEO for React SPA without SSR or prerendering](https://stackoverflow.com/questions/70390808/how-to-achieve-seo-for-react-spa-without-ssr-or-prerendering-and-preferably-kee)
  - [Single Page Application: Dispelling SEO Myths | HackerNoon](https://hackernoon.com/single-page-application-dispelling-seo-myths)

- https://github.com/jaredpalmer/after.js /202111/ts/inactive/代码少
  - Next.js-like framework for server-rendered React apps built with React Router

- https://github.com/Aslemammad/vitext /202201/ts/inactive
  - The Next.js like React framework for better User & Developer experience!
  - Vitext (Vite + Next) is a lightning fast SSG/SSR tool that lets you develop better and quicker front-end apps.

- https://github.com/sanyuan0704/island.js /MIT/202308/ts
  - Vite & MDX powered static site generator. 
  - Base on islands architecture. implement less client bundle and partial hydration
  - Internal MDX support, you can write React component in markdown file.
  - [如何看待最近正式发布的 Web 全栈框架 Fresh? - 知乎](https://zhuanlan.zhihu.com/p/556336887)
  - Fresh 中关于 Islands 架构的实现是基于 Preact 的，我本人也借鉴了 Fresh 的思路，通过拦截 React.createElement 方法在 React 当中也实现了 Islands 架构

- https://github.com/childrentime/island-architecture
  - a demo of implementing the Island Architecture in React.

- https://github.com/MrWangJustToDo/react-ssr-setup /MIT/202403/ts
  - React ssr setup, new ssr for react-18
  - 灵活的渲染方式 SSR CSR, CSR 回退
  - page level 代码分割
  - 静态页面生成 build:static 标记静态页面 export isStatic = true; (目前只支持 webpack)
# ssr-non-js
- https://github.com/floodfx/undead /202312/java/js
  - LiveView server implementation for the JVM
  - Undead is built on top StringTemplates which is a "Preview Feature" of Java 21.
  - No need to write javascript
# microfrontend
- https://github.com/single-spa/single-spa /js
  - The router for easy microfrontends
  - Build micro frontends that coexist and can (but don't need to) be written with their own framework
  - Use multiple frameworks on the same page without refreshing the page (React, AngularJS, Angular, Ember)
  - Lazy load code for improved initial load time.
# more-ssr
- https://github.com/MrWangJustToDo/fullstack-nest-react-ssr-template
  - fullstack ssr template, BE with nestjs, FE with react

- https://github.com/GoogleChrome/rendertron /ts/deprecated
  - Rendertron is a headless Chrome rendering solution designed to render & serialise web pages on the fly.
  - Built with Puppeteer
  - Rendertron runs as a standalone HTTP server. 
  - Rendertron renders requested pages using Headless Chrome
  - Dynamic rendering is not a recommended approach and there are better approaches(ssr) to rendering on the web.
  - [单页面(如react，vue)网站的服务器渲染 SSR 之 SEO 大杀器 Rendertron - 知乎](https://zhuanlan.zhihu.com/p/66672794)
    - 首先，服务器上装有个google-chrome，rendertron把他打开，然后在服务器（官方推荐express）中增加中间件，先判断UA（user-agent）里面有没有带有类似Baiduspider（百度爬虫）等字样，如果没有，就像正常的单页面服务器那样，把原始html推送出去，由客户端浏览器完成js、css渲染的工作；如果带有指定UA头字样，就先把网页推送给本地服务器那个google-chrome，等他渲染好对应页面后，把渲染好的html结果推送出去。不就是为了SEO么，你爬虫来了我再渲染给你总行了吧
- https://github.com/algolia/renderscript /ts
  - An API to render a page inside a real Chromium (with JavaScript enabled) and send back the raw HTML
  - This project was heavily inspired by GoogleChrome/rendertron.
  - It was based on `puppeteer-core` but we switched to `Playwright`.
  - This project is directly written for and consumed by Algolia Crawler.
  - Renderscript has everything abstracted to render a page and login to website with minimal configuration required.

- https://github.com/prerender/prerender
  - Prerender is a node server that uses Headless Chrome to render HTML, screenshots, PDFs, and HAR files out of any web page. 
  - The Prerender server listens for an http request, takes the URL and loads it in Headless Chrome, waits for the page to finish loading by waiting for the network to be idle, and then returns your content.
  - The Prerender server can be used in conjunction with our Prerender.io middleware in order to serve the prerendered HTML of your js website to search engines (Google, Bing, etc) and social networks (Facebook, Twitter, etc) for SEO.
  - Prerender differs from Google Puppeteer in that Prerender is a web server that takes in URLs and loads them in parallel in a new tab in Headless Chrome. 
    - Puppeteer is an API for interacting with Chrome, but you still have to write that interaction yourself. 
    - With Prerender, you don't have to write any code to launch Chrome, load pages, wait for the page to load, or pull the content off of the page. 
    - The Prerender server handles all of that for you so you can focus on more important things!
  - Prerender solves SEO by serving prerendered HTML to Google and other search engines. It's easy:
    - Just install the appropriate middleware for your app (or check out the source code and build your own)
    - Make sure search engines have a way of discovering your pages (e.g. `sitemap.xml` and links from other parts of your site or from around the web)

- react-snap /4kStar/MIT/201905/js/inactive
  - https://github.com/stereobooster/react-snap
  - Pre-renders a web app into static HTML. 
  - Uses Headless Chrome to crawl all available links starting from the root. 
  - Heavily inspired by prep and react-snapshot, but written from scratch. 
  - Zero configuration is the main feature. 
  - **Works out-of-the-box with create-react-app** - no code-changes required.
  - Does not depend on React. The name is inspired by react-snapshot but works with any technology (e.g., Vue).
  - [Behind the scenes](https://github.com/stereobooster/react-snap/blob/master/doc/behind-the-scenes.md)
    - react-snap works concurrently, by default it uses 4 tabs in the browser. 

- https://github.com/jaredpalmer/razzle
  - Universal JavaScript applications are tough to setup. 
    - Either you buy into a framework like Next.js or react-server, fork a boilerplate, or set things up yourself. 
  - Aiming to fill this void, Razzle is a tool that abstracts all complex configuration needed for both SPA and SSR into a single dependency
    - giving you the awesome developer experience of create-react-app, 
    - but then leaving the rest of your app's architectural decisions about frameworks, routing, and data fetching up to you. 
  - Think of a static site generator as a script which takes in data, content and templates, processes them, and outputs a folder full of all the resultant pages and assets.
    - in the SSG proccess we SSR the app and then save result of the SSR into a html file
  - Razzle not only works with React, but also Reason, Elm, Vue, Angular, Svelte, and most importantly......whatever comes next

- https://github.com/nuxt/nuxt.js
  - a framework making web development simple and powerful.
  - Server-side rendering OR Single Page App OR Static Generated, you choose
