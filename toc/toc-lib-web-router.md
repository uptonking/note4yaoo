---
title: toc-lib-web-router
tags: [router, toc, web]
created: 2020-12-10T20:41:35.691Z
modified: 2020-12-12T18:59:54.950Z
---

# toc-lib-web-router

# guide
- tips
  - 一般ssr方案都会提供自己的router, nextjs将file-based-routing作为卖点
  - 没必要寻找前后端通用的router，前端、后端框架都有自己的，routing常和prefetch耦合
# popular
- https://github.com/unjs/radix3 /MIT/202402/ts
  - fast router for JavaScript based on Radix Tree.
  - https://github.com/yoshuawuyts/sheet-router /MIT/201702/js
    - fast, modular client-side router with radix-trie

- https://github.com/TanStack/router /202402/ts
  - typesafe Router for React (and friends) w/ built-in caching, 1st class search-param APIs, client-side cache integration and isomorphic rendering
  - 🆚️ [Comparison | TanStack Router & TanStack Start vs Next.js vs React Router / Remix](https://tanstack.com/router/latest/docs/framework/react/comparison)
  - [TanStack Router React Docs](https://tanstack.com/router/latest/docs/framework/react/installation)
    - TanStack Router is currently only compatible with React (with ReactDOM) and Solid. 
    - If you would like to contribute to the React Native, Angular, or Vue adapter, please reach out to us on Discord.
  - [Are there any plans to support vue? _202405](https://github.com/TanStack/router/discussions/1568)
    - Currently no. Right now, Tanner's diving into Start and RSCs for Router.

- https://github.com/molefrog/wouter /202402/js
  - a tiny router for modern React and Preact apps that relies on Hooks.
  - Supports both React and Preact
  - Mimics React Router's best practices by providing familiar Route, Link, Switch and Redirect components.
  - hook-based API for more granular control over routing (like animations): useLocation, useRoute and useRouter.

- https://github.com/visionmedia/page.js /202004/js/单文件/inactive
  - Tiny Express-inspired client-side router
  - 示例丰富，基于script标签
  - [is this project still active?](https://github.com/visionmedia/page.js/issues/611)
    - I've been using this in production since 2018 and it's all been perfect.
    - I guess we are not used that a project can just be working and completed.
    - I consider this project as just stable and long-term.

- https://github.com/router5/router5 /MIT/202004/ts/inactive
  - router5 is a framework and view library agnostic router.
  - view/state separation: router5 processes routing instructions and outputs state updates.
  - universal: works client-side and server-side

- https://github.com/kriasoft/universal-router /MIT/202306/ts
  - https://www.kriasoft.com/universal-router/
  - A simple middleware-style router that can be used in both client-side and server-side applications
  - It has simple code with only single path-to-regexp dependency.
  - It can be used with any JavaScript framework such as React, Vue, Hyperapp etc.
  - It uses the same middleware approach used in Express and Koa, making it easy to learn.
  - It supports both imperative and declarative routing style.

- https://github.com/flatiron/director
  - A routing library that works in both the browser and node.js environments with as few differences as possible.
  - Simplifies the development of Single Page Apps and Node.js applications. 
  - Dependency free (doesn't require jQuery or Express, etc).

- https://github.com/alshdavid/crayon
  - Simple framework agnostic UI router for SPAs
  - Clientside Router with express like syntax, no dependencies
# navigation
- https://github.com/virtualstate/navigation
  - Native JavaScript wicg navigation implementation
# more
