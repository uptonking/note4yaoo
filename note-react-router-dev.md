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

- ## I find it interesting that React Router is synchronous and essentially knows nothing about the route tree until it attempts to render it. 
- https://twitter.com/tannerlinsley/status/1492155286240456710
  - This is very different from RL which knows about your entire route tree when the router is rendered (but maybe not the route elements, etc)
  - Knowing about the entire route configuration up front has some benefits. In RL namely, we use that info to support colocation of search filters and fetching logic with routes (at the cost of not supporting lazy-routes like RR does with Suspense. So there's definitely a balance...