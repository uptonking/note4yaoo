---
title: note-react-router-dev
tags: [dev, react-router]
created: 2021-09-17T19:30:13.866Z
modified: 2023-01-09T15:41:17.179Z
---

# note-react-router-dev

# guide
- features
  - support react-native
  - support ssr

- react-router
  - 支持react-native

- tanstack-router
  - 暂不支持react-native
  - 支持ssr

- url as state-management

- [Trailing Slashes on URLs: Contentious or Settled?](https://twitter.com/sebastienlorber/status/1488568747447181315)
  - Trailing slashes are complicated and non-std:
    - depends on output: /path/index.html VS /path.html
    - depends on host behavior
  - [TRAILING SLASHES ON URLS: CONTENTIOUS OR SETTLED?](https://www.zachleat.com/web/trailing-slash/)
    - resource/index.html is marginally safer than resource.html
# not-yet
- 最新 Link 总是会重复添加 path，如 http://localhost:8999/dashboard/basic/basic/basic
  - 此问题在v6 beta版会出现，后面已修复
# changelog
- resources
  - [CHANGELOG.md for React Router Releases](https://github.com/remix-run/react-router/blob/main/CHANGELOG.md)

- [v7.0.0_2024-11-21](https://reactrouter.com/upgrading/v6)
  - The v7 upgrade has no breaking changes if you have enabled all future flags. 
  - The react-router-dom, @remix-run/react, @remix-run/server-runtime, and @remix-run/router have been collapsed into the `react-router` package
  - The react-router-dom-v5-compat and `react-router-native` packages are removed starting with v7
  - The `json` and `defer` methods are deprecated in favor of returning raw objects.
  - The Remix Vite plugin is the proper way to build full-stack SSR apps using React Router v7. The former `esbuild`-based compiler is no longer available.
  - React Router v7 includes a new `prerender` config in the vite plugin to support SSG use-cases. 
  - [React Router v7 release blog](https://remix.run/blog/react-router-v7)
    - v7 brings everything you love about Remix back into React Router
    - We encourage all Remix v2 users to upgrade to React Router v7
    - For React Router v6 users, this release brings a wealth of features from Remix back into React Router in the form of "framework mode".

- [v6.0.0-beta.4](https://github.com/remix-run/react-router/releases/tag/v6.0.0-beta.4)
  - Absolute nested path support
  - Removed the ability for nested route paths to begin with a / 

- [v6.0.0-beta.3 NavLink: replace activeClassName + activeStyle props](https://github.com/remix-run/react-router/pull/7985)
  - replace them by allowing either `style` or `className` to accept functions with the active state. 
# issues

# discuss-stars
- ## 

- ## TIL the browser treats cached Requests fired via refresh and pressing enter in the URL differently:
- https://x.com/wesbos/status/1892641489366175832
  - First Visit: sends cache-control: no-cache
  - Page Refresh: sends cache-control: max-age=0 - bypasses local cache
  - Press enter in URL Bar: Loads from Disk Cache

- Enter in URL bar is good (if not the only) way to re-apply the location # hash anchor fucus jump position. (But #:~:text fragment highlight worked differently on re-enter across browsers last time I tested, though.)

- GitHub and YouTube seem to [ab]use this. Enter in the address bar is faster than whatever they are doing for the reload and progress bar sometimes.

- ## [Can we use react-router-dom in next.js app and still achieve server side rendering? : r/nextjs _202306](https://www.reddit.com/r/nextjs/comments/13xct3y/can_we_use_reactrouterdom_in_nextjs_app_and_still/)
- file based routing is probably the Nextjs' biggest selling point. As you said, use react-router-dom cause every component to be client-side rendered, which mostly defeats the whole purpose of Nextjs. This is dumb.

- I think the best you can do is tell your client that nextjs can’t do both, ask them to list out which page to have SSR (calls to getServerSideProps), which page is not, maybe a few of them are required for SEO, most other page isn’t required can be stay with react-router-dom
# discuss-news
- ## 

- ## For Remix 3, we’re going all-in on runtime-first simplicity: no bundler in dev, and likely none in prod either thanks to native ESM + modern CDN strategies.
- https://x.com/mjackson/status/1928297364726632499
  - No HMR, just clean, fast reloads. The goal is minimal tooling, zero critical deps, and a framework that feels closer to the platform. 
  - We don’t think Vite is necessary to deliver a great DX, though folks can layer it in if they want.
  - On Preact: it’s a conscious tradeoff for simplicity and control. React’s ecosystem is huge, but so is the complexity. We’re betting that a lighter core + stable APIs + great defaults can make the framework more approachable without sacrificing power and flexibility.

- people can always throw Vite into the mix if they feel they need it.

- “No HMR, just clean, fast reloads. The goal is minimal tooling, ” so your in-memory router will keep reseting to base route after every change. Correct me if I am wrong please
  - Why would it reset to base route? There’s this nifty thing called the URL that keeps track of where you are.

- ## Remix 3 is a new thing that reuses the name because you should buy our merch(商品/货物 (merchandise))
- https://x.com/ryanflorence/status/1928190268148248815
- Reminds me of Angular vs AngularJS. I think I'll call the new thing Premix.

- Broken API for the 7rd time this year?

- RRv7 is exactly what Remix v3 would have been, that is what you should do

- https://x.com/flybayer/status/1928441254678806614
  - I think re-using a name for something totally new is a huge mistake. Redwood has done this recently too. 
# discuss
- ## 

- ## 

- ## 

- ## I don’t understand why the JavaScript community is obsessed with file based routing. It’s not needed and you can clearly see the complexity it creates in every real world implementation.
- https://twitter.com/zeeg/status/1749869213089714558
  - Having a route be in a single file is fine, controlling routing and inheritance based on that files location is the complexity.
  - it’s good for simple apps, especially content based stuff.

- ## File-based routing is great for defining convention and boundaries. It forces you to pre-split functionality and think hierarchically.
- https://twitter.com/tannerlinsley/status/1749511216345833763
  - It's severely limited however for actually defining how routes are matched because there's only so much you can unpack from a string (in a type safe way too) to handle highly dynamic conditions. I have yet to see a file-based routing solution really  lean into search params for matching and I believe this is part of the equation. 

- That's why PHP MVC Framework evolved from constraints raw .php files directory structure.

- ## fter tearing @Tan_Stack Router's internals to the ground and rebuilding them over the last few weeks, somehow my defer/Awaited promise streaming logic survived perfectly _20231206
- https://twitter.com/tannerlinsley/status/1732155612962882012
- is it possible to control the rendering of route components? With something like AnimatePresence?
  - Haven’t tried, but theoretically yes.
- Are actions and loaders running on the server side now? Or can we choose to run them on the server ?
  - TSR has built-in loaders that *can* run on the server. But it does not have "actions".

- ## Route-based dialogs are not great. But breadcrumbs are great ... btw...
- https://twitter.com/kentcdodds/status/1679936799291084801
  - I've removed route-based dialogs from the Epic Stack in favor of full-page routes and breadcrumbs. 
  - [Remove Route-based Dialogs (and breadcrumbs are great)](https://github.com/epicweb-dev/epic-stack/discussions/309)

- Agreed that dialogs are a UI/UX crutch(支撑物, 支柱). But if you're using them... giving your dialogs their own route is an ice bath of simplicity for your codebase
- Main use case for route-based dialogs is to prevent the "lost focus on the main page" , normaly happen during Back button or Click the link back to home page. Reddit is good example of using route-based dialog.

- ## Am I the only one that doesn't like file system routers? 
- https://twitter.com/devongovett/status/1626635855199600660
  - Seems like a step backwards from components to be thinking in terms of "pages". 
  - You end up rebuilding each route from the inside out rather than composing naturally. 
  - If there were no URLs, we wouldn't do it this way, right?
  - Some frameworks try to add nested routes on top of file system routers, but then it just gets even more confusing. Things do get composed, but you can't see where or how. There are lots of special reserved file names and symbols. Too much magic.
- I think React Router got it mostly right – routes are just components that you compose together naturally. The problem is this leads to loading waterfalls. Perhaps this is a good reason for fs routers, but I think there is a missing bundler primitive that could also solve this.
- A big benefit of file system routers is the ability to browse the codebase easier. When a developer has to fix a bug happening in page with a given URL, they can quickly find the related file.
- There are no URLs in React Native, and we indeed don’t do it that way.
  - However, that comes with its own (rather major) drawbacks. For example, not being able to deeplink easily to specific screens. Ever noticed how native apps don’t seem to link inside them very well? That’s because of this.
- The Expo Router project is moving to file/folder based routing. Fairly popular idea right now.
- I like @emberjs approach, where the urls and routes themselves are defined in one file, but those definitions match up to files either in a topic based layout or more grouped approach (called pods). The files don't in themselves have the url (Symbols and stuff).
  - Similar to Rails.

- ## I find it interesting that React Router is synchronous and essentially knows nothing about the route tree until it attempts to render it. 
- https://twitter.com/tannerlinsley/status/1492155286240456710
  - This is very different from RL which knows about your entire route tree when the router is rendered (but maybe not the route elements, etc)
  - Knowing about the entire route configuration up front has some benefits. In RL namely, we use that info to support colocation of search filters and fetching logic with routes (at the cost of not supporting lazy-routes like RR does with Suspense. So there's definitely a balance...
