---
title: thread-lang-js-runtime
tags: [lang-js, runtime, thread]
created: 2024-03-30T05:55:36.744Z
modified: 2024-03-30T05:55:54.349Z
---

# thread-lang-js-runtime

# guide

# blogs

## [Building runtime-aware JavaScript packages - CodeSandbox _202306](https://codesandbox.io/blog/building-runtime-aware-js-packages)

- With the addition of import paths mapping in Node version 16, we can define a dependency to use determined by whether the module is running in the browser or Node.

- While bundling projects, it's a common practice to use process.env. NODE_ENV to create different builds for production and development
  - if we import the process from `node:process`, then the bundlers and CDNs that build these packages will detect the usage of built-ins and polyfill them accordingly.
  - Note: This is only handled in CommonJS and is generally discouraged! 
  - It is suggested to use conditional exports and imports for branching rather than relying on code analysis.
# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## JavaScript 的生命力来源于去中心化。虽然基础很草台，但是因为浏览器五花八门，没有一家垄断，导致没有一个厂商可以独立为其增加特性或者大刀阔斧地修改。
- https://twitter.com/xicilion/status/1773619873488191937
  - 而对于开发者，因为有那么多浏览器需要兼容，谁也不敢随意尝试一两个厂商支持的新特性。最终达成了目前的行业共识。
- 微信小程序就敢加，只是现在技术能力还不够。
- 小年轻，没人用浏览器。
  - 国人不用不代表全世界人不用
