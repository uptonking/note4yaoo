---
title: lib-ui-spectrum-codebase
tags: [adobe-spectrum, codebase]
created: '2021-04-12T16:38:36.775Z'
modified: '2021-04-12T18:06:54.456Z'
---

# lib-ui-spectrum-codebase

# guide
## coding-style

- 函数内大多数局部变量都是let块级可再赋值的变量，特别是props参数
  - https://github.com/adobe/react-spectrum/pull/93
  - Creating a new variable is a recipe for bugs in this case. I'd immediately forget to use the new variable not named props and keep using props later in the code, not realizing that it isn't actually all of the props. Already did this several times.

# pieces

# state

# docs

- 几乎所有文档都在mdx文件中，部分文档从组件源码的注释中提取
  - 各种文件以及特殊的import形式，参考.parcelrc配置
