---
title: lib-db-pouchdb-dev-log
tags: [couchdb, dev-log, pouchdb]
created: 2023-11-08T17:07:24.689Z
modified: 2023-11-08T17:07:50.967Z
---

# lib-db-pouchdb-dev-log

# guide

# not-yet

## ❓ pouchdb初始化的问题，fauxton管理页面和示例页面eg1必须在同一浏览器打开后才能初始化？

- related
  - [PouchDB 7.0.0 breaks cookie authentication](https://github.com/pouchdb/pouchdb/issues/7390)

- 首次初始化可正常访问pdb，手动删除cookie后刷新页面eg1，pdb初始化会失败，401 (Unauthorized)
  - 奇怪的是，此时刷新fauxton管理页面需要重新登录fauxton，
  - 然后，若在同一浏览器刷新页面eg1则pdb可正常初始化，若在其他浏览器刷新页面eg1则pdb仍会初始化会失败

- 原因推断，
  - ~~同一ip下的不同pdb客户端连接同一个couchdb时，只有第一个客户端能通过set-cookie拿到AuthSession，其他客户端无法拿到cookie会认证失败~~
# dev-to

# dev-later

# dev-maybe

# done
