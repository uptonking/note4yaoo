---
title: tool-dev-webpack
tags: [tool, engineering, webpack]
created: '2020-11-20T19:29:35.880Z'
modified: '2020-11-20T19:30:56.804Z'
---

# tool-dev-webpack

## guide

- Webpack Incremental Builds
  - Use webpack's watch mode. Don't use other tools to watch your files and invoke webpack. 
  - The built-in watch mode will keep track of timestamps and passes this information to the compilation for cache invalidation.
  - In some setups, watching falls back to polling mode. 
    - With many watched files, this can cause a lot of CPU load. 
    - In these cases, you can increase the polling interval with watchOptions.poll.
  - 可实现类似ts project references的快速增量编译
  - The following utilities improve performance by compiling and serving assets in memory rather than writing to disk:
    - webpack-dev-server/webpack-hot-middleware/webpack-dev-middleware

## webpack-config

## webpack-dev-server
