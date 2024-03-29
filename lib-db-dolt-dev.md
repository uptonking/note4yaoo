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

- 将git自动生成的.git文件夹改为自定义database，将snapshot改为crdt-changes，似乎可以实现支持时间旅行和协作合并的新工具，参考fossil

- branching
  - 🤔 显示地区分draft/publish/versioning是否是比branching更易理解的产品形式
  - document文档领域的branch实现可不必定制，可在应用层创建新文档实现，参考yjs/upwelling
  - 一种实现思路，保存各branch的name/delta-changes/baseBranchId，然后根据以上数据获取分支对应的所有delta-changes，然后计算出对象数据
  - json/tree branching merge
  - 参考方案1: [Upwelling: Combining real-time collaboration with version control for writers](https://www.inkandswitch.com/upwelling/)

- versioning
  - 多版本的实现方式通常是添加新的列同时复制旧数据，等到数据和api访问都迁移到新的，就废弃旧的
# more
