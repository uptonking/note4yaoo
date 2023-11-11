---
title: lib-utils-git-dev
tags: [git]
created: 2021-06-01T16:55:33.625Z
modified: 2023-08-29T10:11:26.348Z
---

# lib-utils-git-dev

# guide

- pros
  - branching
  - revision history

- cons
  - 体积会越来越大

- features
  - git并不记录每一个操作的change，而是一次commit的所有changes
    - 可以拆分大commit为多个小commit来添加各个子文件的修改描述

- tips
  - git的广泛使用一个原因是与现有的文件和工具都集成方便，设计架构时要考虑现有格式与集成
    - 拆分核心内容和周边功能，split git-src and issues/pr/wiki, split txt/docx/xlsx and api
    - 用户评论数据不同平台的用户很难合并
    - 将更多精力投入 core content 的创作，以及格式兼容、平台兼容
    - 与用户现有的系统集成，如postgresql
  - merge与撤销要花费大量精力
  - 基于文件和基于数据库最大的区别是引用数据块的方式，数据库中的数据块很容易获取id，文件中的位置不容易描述位置或id
  - 设计合适的数据结构和传输协议，都可以实现离线合并

- 将git自动生成的.git文件夹改为自定义database，将snapshot改为crdt-changes，似乎可以实现支持时间旅行和协作合并的新工具，参考fossil
  - 离线编辑再合并，在ui交互上会增加复杂度，使用体验真的会方便吗，基于db实现同步不难
  - 对所有数据实现自动冲突解决和合并不实际，特别是二进制数据或不重要的评论数据

- 基于delta/patch
  - Pijul
  - Darcs

- resources
  - [精通Git | 汪图南](https://wangtunan.github.io/blog/books/git/)
# rewrite
- 在实现branching时使用structural sharing，尽可能复用数据

- event/patch-based

- [Write yourself a Git!](https://wyag.thb.lt/)
# fossil
- features
  - 支持离线编辑和合并，可以基于通用的数据结构和传输协议自己实现
  - 基于rdbms-sqlite
  - share everything, not only one branch
  - 不支持 rebase, 坚持 merge workflow
  - 缺少code review的功能
  - Single binary. Cross platform. Runs with it's own server with web interface. Has issue tracking, wiki, chat.

- tips
  - 可以将fossil的db看成一种程序打包格式
  - 优点是功能丰富，缺点是数据opinionated，tickets/pr/wiki/chats都保存在数据库未遵循规范或最佳实践
  - fossil和自定义的git-like产品并没有太大区别，参考gitea/gogs，数据库的设计都是项目具体的
  - 新产品最好兼容git规范的commits

- [Chisel - Fossil SCM Hosting，类似github](http://chiselapp.com/)
# dev

# more
