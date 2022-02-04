---
title: note-react-router-dx-log
tags: [dx, issues, react-router]
created: '2021-09-17T19:30:13.866Z'
modified: '2021-09-19T15:14:45.954Z'
---

# note-react-router-dx-log

# stars

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
