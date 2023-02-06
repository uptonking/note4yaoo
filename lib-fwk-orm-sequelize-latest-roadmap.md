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
- Sequelize v7 supports Node ^14.17.0 || >=16.0.0, and TypeScript >= 4.5.
- Sequelize v7 restricts which files can be imported.

- Sequelize's CLS implementation has been migrated to use Node's built-in `AsyncLocalStorage`.

- Data Types have been completely rewritten to be more TypeScript-friendly, and make them more powerful.
- Instance methods cannot be used without primary key.

## v6
