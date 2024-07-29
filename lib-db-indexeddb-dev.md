---
title: lib-db-indexeddb-dev
tags: [indexeddb]
created: 2022-06-13T02:56:15.518Z
modified: 2022-06-13T02:56:32.537Z
---

# lib-db-indexeddb-dev

# guide

- pros
  - 支持在浏览器处理大量数据

- cons
  - 刷新页面时，会优先使用idb数据，可能存在本地数据陈旧的情况，最好提供refresh按钮支持手动获取最新数据或清空数据
  - 本地idb数据未加密，可能被窃取或篡改

- usecase
  - apps: browser-new-tab, in-browser-notes
  - libs: pouchdb, yjs
# more
