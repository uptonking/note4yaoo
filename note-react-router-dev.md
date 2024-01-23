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

- [Trailing Slashes on URLs: Contentious or Settled?](https://twitter.com/sebastienlorber/status/1488568747447181315)
  - Trailing slashes are complicated and non-std:
    - depends on output: /path/index.html VS /path.html
    - depends on host behavior
  - [TRAILING SLASHES ON URLS: CONTENTIOUS OR SETTLED?](https://www.zachleat.com/web/trailing-slash/)
    - resource/index.html is marginally safer than resource.html
# not-yet
- 最新 Link 总是会重复添加 path，如 http://localhost:8999/dashboard/basic/basic/basic
  - 此问题在v6 beta版会出现，后面已修复
# upgrading
- [v6.0.0-beta.4](https://github.com/remix-run/react-router/releases/tag/v6.0.0-beta.4)
  - Absolute nested path support
  - Removed the ability for nested route paths to begin with a / 

- [v6.0.0-beta.3 NavLink: replace activeClassName + activeStyle props](https://github.com/remix-run/react-router/pull/7985)
  - replace them by allowing either `style` or `className` to accept functions with the active state. 
# issues

# discuss
- ## 

- ## 

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
