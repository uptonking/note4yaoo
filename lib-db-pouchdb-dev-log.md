---
title: lib-db-pouchdb-dev-log
tags: [couchdb, dev-log, pouchdb]
created: 2023-11-08T17:07:24.689Z
modified: 2023-11-08T17:07:50.967Z
---

# lib-db-pouchdb-dev-log

# guide

- features
  - version history
  - branching
  - partial
  - ivm
  - search
  - aggregation/cube/bi
  - dataflow: git uses dag not tree
# not-yet

# dev-to

## testing

- remove `import-sync`

## migrate

- 将browser/node的nextTick实现迁移到queueMicroTask
- 将pouchdb-fetch的实现迁移到js标准api和自定义精简实现
# dev-later

# dev-maybe

# build/bundling
- 各子包打包时使用external，由用户在使用时打包

- 打包体积过大
  - 重复readable-stream 3000x2
    - sublevel-pouchdb固定在了 v1.1.14
    - levelup.v4依赖 v3.4.0
  - 待迁移node-fetch+fetch-cookie 6000, 通过重构`pouchdb-fetch`包
  - ✅ 重复 levelup
    - 顶层node-polyfill的levelup.v0.1覆盖了pouch-like下的2个子包v4导致打包重复，将顶层去掉后就只打包1次了
# done

## bundling pouchdb-find: Resolve error: Can't resolve 'pouchdb-abstract-mapreduce'

- 原因是 import pouchdb-abstract-mapreduce 发生在内层文件夹
  - rspack的`resolve.alias`只替换顶层

## pouchdb初始化的问题，fauxton管理页面和示例页面eg1必须在同一浏览器打开后才能初始化？

- related
  - [PouchDB 7.0.0 breaks cookie authentication](https://github.com/pouchdb/pouchdb/issues/7390)

- 首次初始化可正常访问pdb，手动删除cookie后刷新页面eg1，pdb初始化会失败，401 (Unauthorized)
  - 奇怪的是，此时刷新fauxton管理页面需要重新登录fauxton，
  - 然后，若在同一浏览器刷新页面eg1则pdb可正常初始化，若在其他浏览器刷新页面eg1则pdb仍会初始化会失败

- 原因推断，
  - ~~同一ip下的不同pdb客户端连接同一个couchdb时，只有第一个客户端能通过set-cookie拿到AuthSession，其他客户端无法拿到cookie会认证失败~~

- 💡 解决方法
  - 初始化pdb时需要传入用户名密码，类似典型的数据库连接url
  - `new PouchDB('http://user:pass@localhost:5984/testdb');`
# more
- 依赖 process.env 的包
  - pouchdb-mapreduce
  - pouchdb-utils
