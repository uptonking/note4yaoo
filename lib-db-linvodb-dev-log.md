---
title: lib-db-linvodb-dev-log
tags: [dev-log, linvodb]
created: 2023-01-09T15:39:41.013Z
modified: 2023-01-09T15:41:34.578Z
---

# lib-db-linvodb-dev-log

# guide

# done
- 迁移 full-text-search
  - db.textSearch
  - db.textIndex，支持搜索图片元数据
  - search-text-cn
    - [ ] 中英文混合索引的构建与优化

- 较大的源码改动
  - 去掉了 construct 事件，因为每个doc对象都是普通js对象，而不是Model对象，与nedb一致
# dev-log
- fix-tests: db.test.ts, Can't insert key **, it violates the unique constraint
  - 具体测试用例测的就是异常场景，所以属于预期行为，可以把手动console.error关掉
