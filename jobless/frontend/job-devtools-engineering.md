---
title: job-devtools-engineering
tags: [devtools, engineering, job]
created: '2021-10-10T09:23:56.665Z'
modified: '2021-10-10T09:48:05.563Z'
---

# job-devtools-engineering






## babel原理

- Babel就是一个编译器，执行了和其他编译器类似的编译工作：
- 解析（parse）
  - 将代码字符串解析成抽象语法树
- 变换（transform）
  - 对抽象语法树进行变换操作。实现代码转换的重点在变换阶段
  - Babel会对 AST 进行DFS，在遍历结点的过程中，如果遇到了不支持的语法，Babel 会对其进行变换，相当于修改 AST 结点。
  - Babel会维护一个 Visitor 对象，这个对象定义了用于获取 AST 中具体节点的方法，由 Visitor 判断并进行变换操作。
- 重建（rebuild）
  - 根据变换后的抽象语法树再生成字节码

