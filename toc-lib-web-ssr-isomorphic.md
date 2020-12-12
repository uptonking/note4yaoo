---
title: toc-lib-web-ssr-isomorphic
tags: [isomorphic, server-side-rendering, ssr, web]
created: '2020-11-22T13:29:51.265Z'
modified: '2020-12-12T18:45:08.468Z'
---

# toc-lib-web-ssr-isomorphic

- 单页应用不太有助于SEO的实现，在过去的几年中，业界针对此问题提供了两种解决方案：服务器端渲染（SSR）和静态站点生成（SSG）。
  - 使用SSR，我们可以在服务器上运行应用程序，它创建由前端获取的HTML。
  - 而使用SSG，我们可以在构建时创建应用程序的所有页面，由此，存储在服务器上的文件是静态的，并像标准的非SPA应用程序一样由浏览器获取。
  - SSR的最大问题是，在服务器上构建应用程序会占用大量资源，而且速度可能很慢，因此会增加页面加载时间；
    - 而且，每个小的更改都需要重新构建和创建所有应用程序页面。
    - 如果应用程序有很多页面，则该过程很慢且成本很高。
  - 现在看来，SSG赢了，SSR（几乎）死了。
    - Next.js是一个流行的全栈框架，将SSG设置为默认框架，并添加了增量构建，以缓解每次更改后重新构建所有页面的问题。
    - 此外，像Gatsby这样的静态网站生成器会在其产品中添加增量构建。

## react-ssr-solutions

- https://github.com/vercel/next.js
  - Next.js gives you the best developer experience with all the features you need for production with no config needed.
  - hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. 
  - Pre-render pages at build time (SSG) or request time (SSR) in a single project
  - Every component in the pages directory becomes a route.
  - Optionally create API endpoints to provide backend functionality.

- https://github.com/redfin/react-server
  - React framework with server render for blazing fast page load and seamless transitions between pages in the browser.
  - React Server is now defunct. Consider Next.js instead.

- https://github.com/jaredpalmer/after.js
  - Next.js-like framework for server-rendered React apps built with React Router

- https://github.com/alibaba/beidou
  - Isomorphic framework for server-rendered React apps

- https://github.com/ykfe/egg-react-ssr
  - 小而美的Egg + React + SSR 服务端渲染应用骨架，同时支持JS和TS

## ssr-solutions

- https://github.com/GoogleChrome/rendertron
  - Rendertron is a headless Chrome rendering solution designed to render & serialise web pages on the fly.
  - Built with Puppeteer
  - Rendertron runs as a standalone HTTP server. 
  - Rendertron renders requested pages using Headless Chrome

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
  - Aiming to fill this void, Razzle is a tool that abstracts all complex configuration needed for SSR into a single dependency
  - giving you the awesome developer experience of create-react-app, 
  - but then leaving the rest of your app's architectural decisions about frameworks, routing, and data fetching up to you. 
  - With this approach, Razzle not only works with React, but also Reason, Elm, Vue, Angular

- https://github.com/nuxt/nuxt.js
  - a framework making web development simple and powerful.
  - Server-side rendering OR Single Page App OR Static Generated, you choose
