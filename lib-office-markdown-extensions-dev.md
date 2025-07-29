---
title: lib-office-markdown-extensions-dev
tags: [extensions, markdown, mdx]
created: 2021-06-01T13:12:14.966Z
modified: 2021-06-02T15:29:52.268Z
---

# lib-office-markdown-extensions-dev

# guide

- 集合markdown的灵活性和asciidoc的规范性
# 🆚 comparison for md parser
- marked /ts
  - 默认允许不安全的内容
  - 对CommonMark和GFM的支持不够好
- markdown-it /js
  - 支持 CommonMark
  - 解析方式基于规则而不是基于状态机, 可以方便自定义新的解析规则
  - 中间产物是一个号牌流，而不是AST
  - 🐛 似乎一次必须解析整块markdown文本
- remark /js
  - 插件驱动的架构。
  - 以 AST 为默认输出标准。可以进行lint等操作。
  - micromark是底层引擎， 最小化的遵循CommonMark的解析器，带有位置信息和具体的符号。使用状态机来将整个markdown解析成具体的号牌。

- resources
  - [Remarkjs 处理 markdown - Redoc's Space](https://redoc.top/article/1200-Remarkjs%20%E5%A4%84%E7%90%86%20markdown)
# mdx
- knobs for components
  - 在组件预览图周围显示修改配置属性值的工具条
# code-block

# code-related
- code-screenshot
# export
- 有的 link url 实在太长了，应该提供工具**在格式化时或导出时**，统一将所有url移到当前文件末尾
# blogs
- [Why is Markdown popular? - Russell Beattie's Notes](https://www.russellbeattie.com/notes/posts/why-is-markdown-popular.html)
