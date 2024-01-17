---
title: lib-db-pouchdb-codebase
tags: [codebase, pouchdb, rewrite]
created: 2024-01-04T14:39:36.595Z
modified: 2024-01-04T14:40:00.048Z
---

# lib-db-pouchdb-codebase

# guide

# architecture
- 插件架构

- pouchdb-core
  - AbstractPouchDB, plugin, adapter, pouchdb-plugin-changes-filter
- pouchdb-node
  - core, leveldb, http, mapreduce, replication
- pouchdb-browser
  - core, idb, http, mapreduce, replication
# overview

## pouchdb-browser

- browser的`nextTick`实现依赖 immediate
  - node的实现基于 process.nextTick
- pouchdb-md5的实现
  - browser基于spark-md5 + pouchdb-binary-utils
  - node基于内置的crypto

## pouchdb-node

- node实现基于levelup, level, level-write-stream
# data-model

# reactivity

# bundling
- node平台的打包涉及到leveldown二进制，webpack/rspack难以正确打包

- 测试时使用的PouchDB实例在 `tests/integration/utils.js` 中替换了 utils/ajax
# test
- 默认执行node平台的测试
  - node bin/build-modules.js
  - ./bin/test-node.sh > COVERAGE empty
  - tests/integration/node.setup.js
  - pouchdb-adapter-memory

- 测试browser版，CLIENT=chromium
  - Starting chromium on http://127.0.0.1:8000/tests/integration/index.html?remote=1&viewAdapters=memory&couchHost=http%3A%2F%2F127.0.0.1%3A3000
  - 默认使用 dist/pouchdb.js， dist/pouchdb.memory.js
# more
