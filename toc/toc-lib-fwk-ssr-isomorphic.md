---
title: toc-lib-fwk-ssr-isomorphic
tags: [isomorphic, server-side-rendering, ssr, web]
created: 2020-11-22T13:29:51.265Z
modified: 2020-12-19T13:04:40.865Z
---

# toc-lib-fwk-ssr-isomorphic

# guide

# ssr
- https://github.com/jaredpalmer/after.js /202111/ts/inactive/代码少
  - Next.js-like framework for server-rendered React apps built with React Router

- https://github.com/Aslemammad/vitext /202201/ts/inactive
  - The Next.js like React framework for better User & Developer experience!
  - Vitext (Vite + Next) is a lightning fast SSG/SSR tool that lets you develop better and quicker front-end apps.

- https://github.com/vikejs/vike /MIT/202401/ts
  - https://vike.dev/
  - Like Next.js / Nuxt but as do-one-thing-do-it-well Vite plugin.
  - The vite-plugin-ssr project has been renamed Vike

- https://github.com/sanyuan0704/island.js
  - Vite & MDX powered static site generator. Base on islands architecture
  - [如何看待最近正式发布的 Web 全栈框架 Fresh? - 知乎](https://zhuanlan.zhihu.com/p/556336887)
  - Fresh 中关于 Islands 架构的实现是基于 Preact 的，我本人也借鉴了 Fresh 的思路，通过拦截 React.createElement 方法在 React 当中也实现了 Islands 架构

- https://github.com/childrentime/island-architecture
  - a demo of implementing the Island Architecture in React.

- https://github.com/floodfx/liveviewjs /646Star/MIT/202306/ts
  - https://www.liveviewjs.com/docs/overview/introduction
  - LiveViewJS is an open-source framework for "LiveView"-based, full-stack applications in NodeJS and Deno.
  - The LiveView pattern, as popularized in Elixir’s Phoenix framework, shifts your UI’s state management, event handling to the server, calculating minimal diffs to drive updates in your HTML over WebSockets.
  - a LiveView is a server-rendered HTML page that, when loaded, connects back to the server via a persistent web socket. As the user interacts with the LiveView, the client to sends user events (click, keys, etc) via the websocket back to the server and the server responds with diffs to the HTML page in return.
  - LiveViewJS is a protocol compliant, implementation of Phoenix LiveView but written in Typescript and runs on NodeJS and Deno. We want to bring the magic and productivity of LiveView to the NodeJS and Deno ecosystems

- https://github.com/winwiz1/crisp-react /202201/ts
  - Crisp React can optionally split a monolithic React app into multiple Single Page Applications (SPAs) and selectively prerender the landing/index page of any SPA at the build time.
  - Helps to split a monolithic React app into multiple SPAs and avoid vendor lock-in.
  - in each SPA the routing is managed by a separate instance of React Router 
  - By default SSR is enabled for the first SPA and disabled for the second SPA.
  - On the contrary to popular belief that SEO requires SSR, this solution innovatively demonstrates how to get all SPA pages indexed by Google and specific
  - [How to achieve SEO for React SPA without SSR or prerendering](https://stackoverflow.com/questions/70390808/how-to-achieve-seo-for-react-spa-without-ssr-or-prerendering-and-preferably-kee)
  - [Single Page Application: Dispelling SEO Myths | HackerNoon](https://hackernoon.com/single-page-application-dispelling-seo-myths)

- https://github.com/MrWangJustToDo/react-ssr-setup
  - React ssr setup, new ssr for react-18
  - 灵活的渲染方式 SSR CSR

- https://github.com/plantain-00/router-demo
  - Multiple-application SPA and SSR demo

- https://github.com/rakkasjs/rakkasjs
  - a bleeding-edge full-stack React framework powered by Vite. 
  - You can consider it an up-and-coming alternative to Next.js, Remix, or Gatsby.

- https://github.com/fusionjs/fusionjs
  - Uber’s open source universal web framework, represents the fusion of the client and the server. 

- https://github.com/electrode-io/electrode
  - Web applications with node.js and React
  - universal webapp with server side rendering powered by node.js
  - https://github.com/electrode-io/electrode-native
    - A platform to ease integration&delivery of React Native apps in existing mobile applications

- https://github.com/kapouer/express-dom /js
  - Express middleware for (pre)rendering web pages with playwright.

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

## examples

- https://github.com/htdangkhoa/react-ssr-starter /js/inactive
  - A React boilerplate for a universal web app with a highly scalable, offline-first foundation 
  - our focus on performance and best practices.
  - Using SWC will give build times 1.5x faster for the server and 2.2x for the client instead of using Babel.

## solutions

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
- https://github.com/zhangyuang/ssr
  - 此框架脱胎于 egg-react-ssr 项目和 ssr v4版本（midway-faas + react ssr），在之前的基础上做了诸多演进，通过插件化的代码组织形式，支持任意服务端框架与任意前端框架的组合使用

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
# react-ssr
- https://github.com/panDaxiang/ssr
  - react服务端渲染demo
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
