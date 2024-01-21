---
title: lib-editor-univer-blog
tags: [blog, editor, univer]
created: 2024-01-18T11:56:39.134Z
modified: 2024-01-18T11:56:51.162Z
---

# lib-editor-univer-blog

# guide

# blogs

## [这就是 Univer - 知乎 _202401](https://zhuanlan.zhihu.com/p/666298812)

- Univer中的模块拆分和依赖关系
  - 无依赖环原则: 将项目拆分成不同的模块，各个模块做到关注点分离，同时模块之间有明确的依赖关系，并且依赖关系是一个单向无环图，也就是无依赖环原则
  - 依赖反转: 通过依赖注入的方式，反转依赖，避免了核心层对外层的依赖
- Univer 中 MVC 架构更类似于 MVC with Rails, 因为视图层不直接读取 Model 层数据，也不订阅模型层的改变，而是做了一层数据缓存（类似 ViewModel）

- 了解一个项目，先从其数据结构开始， Sheet相关的数据类型定义在 Interfaces 文件夹中
  - 一个 workbook 包含多个 sheets，sheets 所引用的 styles 字段定义在了顶层 workbook 上，保证了样式的复用，减少内存开销，这也是和 Excel 保持一致
  - cellData 字段，一个二维矩阵，用于持久化单元格信息，也就是 ICellData 中定义的类型信息，p 是指富文本，接口类型 IDocumentData，也就是一篇 univer doc，
  - 这也是 univer 设计的独到之处，univer sheet 的每个单元格都可以转变成一个 univer doc

- Univer 生命周期有四个阶段，Starting、Ready、Rendered 和 Steady

- 如果你对 DI 系统比较陌生，建议 阅读 Univer 项目中所使用的 DI 框架 redi。
  - 项目使用 Rxjs 作为观察者模式，阅读 Rxjs 相关文档 是快速熟悉 Rxjs 的方式

## [Univer 文档架构及模块设计 - 知乎 _202401](https://zhuanlan.zhihu.com/p/677606548)

## [Univer 文档排版设计初探 - 知乎 _202401](https://zhuanlan.zhihu.com/p/677626409)

## [OT 算法 & Univer 协同编辑设计 - 知乎 _202401](https://zhuanlan.zhihu.com/p/678454714)

# more
