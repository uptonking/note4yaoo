---
title: lib-fwk-orm-sequelize-latest-roadmap
tags: [orm, roadmap, sequelize]
created: 2023-02-06T09:57:31.836Z
modified: 2023-02-06T09:58:06.200Z
---

# lib-fwk-orm-sequelize-latest-roadmap

# guide

# roadmap
- [v7 Status of merge with sequelize-typescript](https://github.com/sequelize/sequelize/issues/15334)
# changelog

## v7

- [Upgrade to v7 | Sequelize](https://sequelize.org/docs/v7/other-topics/upgrade/)
- One of the major foundational code changes of v7 is the migration to TypeScript.
- Starting with Sequelize v7, we are introducing scoped modules
  - `sequelize`  ->  `@sequelize/core`
- Sequelize v7 only supports the versions of Node.js, and databases that were not EOL at the time of release
  - Sequelize v7 supports Node >= 18.0.0, and TypeScript >= 5.0.0
- Sequelize v7 restricts which files can be imported.

- Sequelize's CLS implementation has been migrated to use Node's built-in `AsyncLocalStorage`.
  - Continuation-local storage works like thread-local storage in threaded programming, but is based on chains of Node-style callbacks instead of threads.
- In order to discourage unmanaged transactions, which we consider to be error-prone,  `sequelize.transaction()` cannot be used to create unmanaged transactions anymore. 
  - You must use `sequelize.startUnmanagedTransaction()`

- Data Types have been completely rewritten to be more TypeScript-friendly, and make them more powerful.
- Instance methods cannot be used without primary key.

## v6
