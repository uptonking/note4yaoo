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

- https://github.com/developit/redaxios /apache2/202208/js/inactive
  - The Axios API, as an 800 byte Fetch wrapper.
  - [Is the goal to be 100% compatible with axios?](https://github.com/developit/redaxios/issues/14)
    - Aside from uploadProgress and downloadProgress, the goal is to support most/all features
    - `.interceptors` for instance is missing on a redaxios instance
  - [Put request doesnt work](https://github.com/developit/redaxios/issues/81)
    - get, post works as expected. But put doesnt work.
  - [Support axios Config Defaults](https://github.com/developit/redaxios/issues/62)
    - FWIW defaults are supported, we just don't prepopulate the headers object. You can do this: instance.defaults = { headers: { 'Content-Type': 'application/json' } };
- https://github.com/divyam234/feaxios /MIT/202402/ts
  - tiny 2KB fetch wrapper of axios
  - a lightweight alternative to Axios, providing the same familiar API with a significantly reduced footprint 
  - It leverages the native fetch() API supported in all modern browsers, delivering a performant and minimalistic solution.
  - supports interceptors, allowing you to customize and augment the request and response handling process.
  - Retries: Axios retry package is integrated with feaxios.

- https://github.com/Netflix/falcor /202105/js/inactive
  - http://netflix.github.io/falcor
  - A JavaScript library for efficient data fetching
  - Falcor lets you represent all your remote data sources as a single domain model via a virtual JSON graph. You code the same way no matter where the data is, whether in memory on the client or over the network on the server.
  - A JavaScript-like path syntax makes it easy to access as much or as little data as you want, when you want it. 
  - Falcor transparently handles all network communications, opportunistically batching and de-duping requests.
  - [Is Falcor being actively maintained?](https://github.com/Netflix/falcor/issues/1016)
    - there are many mentions of netflix moving away from falcor. while they certainly have their reasons falcor still has its place and has no real alternative in many usecases where graphQL is not a good fit!
    - graphQL is too complex to automatically map to simple plain old js object interactions plus i dont want to write schemas for everything up front 
    - falcor has the same scaling capabilities as graphQL. They neeeded to raplace their monolithic falcor backend with a new architecture and happened to chose graphQL, they could also have rewritten a new falcor server with a different architecture and solved those issues. So falcor is not inherently less scalable.
# cache
- https://github.com/yfractal/ccache /202406/rust/ruby
  - Ccache is a Redis client-side caching based on Etag for providing a better consistency guarantee
  - Ccache, short for Conditional Cache, works like HTTP conditional requests, providing client-side caching without sacrificing consistency.
  - Ccache caches data locally, and for subsequent requests, it sends the key with the cached data's ETag to Redis. If the key's data in Redis hasn't changed, Redis returns "no change" and Ccache uses the locally cached data.
  - Redis offers client-side caching to reduce latency and Redis load. However, it only guarantees weak consistency. For example, when clients request different backend servers, they can receive inconsistent data.
# more
