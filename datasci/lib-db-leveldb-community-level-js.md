---
title: lib-db-leveldb-community-level-js
tags: [community, level-js, leveldb]
created: 2022-12-18T09:56:37.193Z
modified: 2022-12-18T09:57:02.567Z
---

# lib-db-leveldb-community-level-js

# guide

# discuss
- ## 

- ## [Decide on naming of modules · Issue #6 · Level/abstract-level](https://github.com/Level/abstract-level/issues/6)
- With abstract-level, there is no "down" or "up" anymore. For example, memdown does not have to be wrapped with levelup. This means level-mem could just do module.exports = require('memdown') to export (largely) the same functionality as before.

- ## [LevelUp, LevelDown, LevelDB_201811](https://blog.elsdoerfer.name/2018/11/10/levelup-leveldown-leveldb/)
- This ecosystem is super confusing. Here is the low-down:
  - LevelDB is a (K/V-Store) database
  - leveldown is a NodeJS binding.
  - levelup is another NodeJS module, which wraps leveldown. However, it allows leveldown to be replaced with another backend.
- In this way, you can use a single library and API – levelup – but with all kinds of different storage backends, from Redis, to SQL databases.
