---
title: lib-db-linvodb-dev
created: 2022-12-22T15:21:49.223Z
modified: 2022-12-22T15:22:15.191Z
---

# lib-db-linvodb-dev

# guide

- why web db
  - db适合复杂业务模型
  - db适合类似excel/多维表格的场景

- 放开思路，可以将insert/find视为key-value映射表的get/set

- nedb与linvodb的区别
  - nedb是内存优先，dml操作会同时持久化op，也提供了全量持久化的方法
  - linvodb是存储优先，没有全量持久化的方法，所以每个dml操作要持久化，要从代码上确认下❓

- find方法是异步，要放在insert/save的回调函数里面，不能写在顶层或同层

- Yes, you have to set both index/unique in the model or ensureIndex

- 依赖level-js-v2
  - chrome-linux的idb本地位置: `~/.config/google-chrome/Default/IndexedDB/`, 每个domain对应一个本地文件夹，典型的leveldb格式
  - 在idb里面key是_id字符串，value是一个document对象序列化后的字符串，符合leveldb的设计
# faq
- 如何存储图片，可参考[pr: added support for Buffers (BLOB) to nedb_201408](https://github.com/louischatriot/nedb/pull/167)
  - I think buffers don't have their place in nedb. 
  - There is already a quite simple way to store a BLOB, and that is to serialize it (as your code does in hex format). 
  - Also, buffers are Node only and don't work in node webkit or the browser
