---
title: lib-lowcode-nocobase-codebase
tags: [codebase, lowcode, nocobase]
created: 2023-03-31T02:08:23.939Z
modified: 2023-03-31T02:08:36.730Z
---

# lib-lowcode-nocobase-codebase

# guide

# dev-to
- not-yet
  - spa在刷新页面时无法恢复，路由配置存在问题
  - 表格分页后，只会在第N页的数据过滤
    - 只有源表分页显示正常

- questions
  - yarn nocobase install 触发的逻辑在哪里

- later
  - 插件市场仍在开发中
  - block protocol
# overview
- 界面上一张表对应数据库中一张表

```shell
# nocobase server
ts-node-dev -r dotenv/config -r tsconfig-paths/register ./packages/app/server/src/index.ts start --port=13001

# client
cross-env PORT=13000 APP_ROOT=packages/app/client PROXY_TARGET_URL=http://127.0.0.1:13001 umi dev
```

# codebase

# more

- nocobase使用webpack打包失败
  - 了解umi的配置后，需要全部自己打包，不能一部分自己打包一部分用dist，这样容易出现多份react导致异常

```JSON
// nocobase默认插件
const plugins = {
  "data": [
    "file-manager",
    "sequence-field",
    "verification",
    "workflow",
    "export",
    "import",
    "china-region",
    "iframe-block",
    "math-formula-field",
    "excel-formula-field",
    "duplicator",
    "audit-logs"
  ]
}
```
