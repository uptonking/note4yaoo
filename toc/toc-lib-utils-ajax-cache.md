---
title: toc-lib-utils-ajax-cache
tags: [ajax, cache, swr, toc, utils]
created: 2023-02-07T09:42:21.490Z
modified: 2023-02-07T09:43:01.972Z
---

# toc-lib-utils-ajax-cache

# guide

# query-cache
- https://github.com/bufbuild/connect-query
  - Connect-Query is an expansion pack for TanStack Query (react-query), written in TypeScript and thoroughly tested. 
  - a Tanstack Query extension to seamlessly integrate Protobuf
  - It enables effortless communication with servers that speak the Connect Protocol.
  - One of the best features of this library is that once you write your schema in Protobuf form, the TypeScript types are generated and then inferred.

- https://github.com/msolvaag/redux-db
  - a normalized redux store and easy object management.
  - redux-db uses internal indexes to speed up lookups and is quite fast at the current state.
  - inspired by libraries such as normalizr and redux-orm.

# query-react
- https://github.com/data-client/rest-hooks
  - Normalized state management for async data. Safe. Fast. Reusable.


# fetch/axios
- https://github.com/sindresorhus/ky /ts
  - Tiny & elegant JavaScript HTTP client based on the browser Fetch API
  - fetch catch需要自己封装，默认不会进入到 reject 分支
    - 不能设置超时
    - 不能取消请求
    - 不支持上传进度
    - Retries failed requests
    - 这些大部分在 Ky 中都解决了
  - 个人小项目用一用还是很不错的，因为 fetch 确实有些痛点；
    - 如果是公司内部的话，还是自己封装一个，因为开源库的普适性在这里并不需要，公司用到的请求库只需要和后端配合好、便于前端开发使用即可。
    - 当然开发内部请求库的时候，参考一下这些开源库的设计思路也是很不错的。

- https://github.com/developit/redaxios /js
  - The Axios API, as an 800 byte Fetch wrapper.
# more
