---
title: lib-react-table-discuss
tags: [discuss, react-table]
created: '2021-02-24T10:09:46.820Z'
modified: '2021-02-24T10:10:02.012Z'
---

# lib-react-table-discuss

# pieces

## 

- ## I think I've built a type-safe plugin system for #ReactTable v8.
- https://twitter.com/tannerlinsley/status/1364251586956943361
  - Not only typed for app devs, obvi, but also fully typed for plugin authors as well.
  - You can customize just about any part of the core React Table functionality that you want, encapsulate all of that logic into a single object, then ship it around your app, the internet, etc
  - Pretty typical plugin system. It's the fact that it's fully typed that's special.
- Why is static typing so important in plugin systems?
  - Plugin systems are traditionally very difficult to type if they involve changing the public API of the thing which they are extending, especially with TypeScript.
  - Types themselves offer a myriad of benefits to any system. There's ample amount of blog posts on TS out there.
