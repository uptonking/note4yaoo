---
title: lib-db-dolt-dev
tags: [database, dolt]
created: 2023-08-25T21:16:18.064Z
modified: 2023-08-25T21:16:48.485Z
---

# lib-db-dolt-dev

# guide

- pros
  - version control: branch/fork/merge
  - time travel history

- cons
  - ？

- features

- branching
  - document文档领域的branch实现可不必定制，可在应用层创建新文档实现，参考yjs/upwelling
  - 一种实现思路，保存各branch的name/delta-changes/baseBranchId，然后根据以上数据获取分支对应的所有delta-changes，然后计算出对象数据
# more
