---
title: toc-lib-fwk-ssr-isomorphic
tags: [isomorphic, server-side-rendering, ssr, web]
created: 2020-11-22T13:29:51.265Z
modified: 2020-12-19T13:04:40.865Z
---

# toc-lib-fwk-ssr-isomorphic

# react-ssr-solutions

- https://github.com/janishar/react-app-architecture /ts/inactive
  - Learn to build a complete website for a blogging platform like Medium; OpenSource project by AfterAcademy
  - Isomorphic React web app: The server sends the rendered pages to the client, and then the client renders the subsequent pages on its own. This is a very important feature for SEO and it also makes the first paint super fast.

- https://github.com/vercel/next.js
  - Next.js gives you the best developer experience with all the features you need for production with no config needed.
  - hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. 
  - Pre-render pages at build time (SSG) or request time (SSR) in a single project
  - Every component in the pages directory becomes a route.
  - Optionally create API endpoints to provide backend functionality.
- https://github.com/jaredpalmer/after.js
  - Next.js-like framework for server-rendered React apps built with React Router
- https://github.com/Aslemammad/vitext
  - The Next.js like React framework for better User & Developer experience!
  - Vitext (Vite + Next) is a lightning fast SSG/SSR tool that lets you develop better and quicker front-end apps.

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
# ssr-solutions
- https://github.com/pmb0/express-tsx-views
  - Server-side JSX/TSX rendering for your express or NestJS application
  - With this template engine, TSX files can be rendered server-side by your Express application. Unlike other JSX express renderers, this one does not rely on JSX files being transpiled by babel at runtime. Instead, TSX files are processed once by the tsc compiler.

- https://github.com/MrWangJustToDo/fullstack-nest-react-ssr-template
  - fullstack ssr template, BE with nestjs, FE with react

- https://github.com/GoogleChrome/rendertron
  - Rendertron is a headless Chrome rendering solution designed to render & serialise web pages on the fly.
  - Built with Puppeteer
  - Rendertron runs as a standalone HTTP server. 
  - Rendertron renders requested pages using Headless Chrome

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

- https://github.com/stereobooster/react-snap
  - /4kStar/MIT/201910/js
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
