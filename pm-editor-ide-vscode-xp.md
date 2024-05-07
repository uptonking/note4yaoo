---
title: pm-editor-ide-vscode-xp
tags: [ide, pm, vscode, xp]
created: 2021-06-02T17:28:01.491Z
modified: 2021-06-02T18:24:50.218Z
---

# pm-editor-ide-vscode-xp

# guide

# draft
- 兼容现有浏览器的扩展
# xp-file-manager
- 难以直接将当前文件移动到父目录
# xp-editor

# discuss-cloud-ide

- ## 

- ## 

- ## 

- ## 

- ## 如果有哪位熟悉 web 前端开发的同学有兴趣，可以一起来做个这样的东西：就是集成一个类似 vscode 的源码显示，加一些交互调试的控制功能，再使用 vscode 一致的调试接口。
- https://twitter.com/cloudwu/status/1787723615720681846
  - 这样就可以直接打开浏览器调试 Ant Engine 开发的游戏了。当然也可以不只用在 Ant Engine 上，可以扩展到一切 Lua 开发的项目。
- 实现一个 DAP（Debug Adapter Protocol）就行了，找一个支持 dap 的前端，比如 vscode，不用写一行代码就能可视化调试你的游戏了
  - 已经实现了。我只是想把前端直接集成在引擎内。
  - Lua 调试器其实是集成在 app 内部的，对外暴露了若干调试接口。这部分 Ant Engine 已经很完善了。只需要一个调试器客户端使用这些接口，展示给程序员看：比如下断点、显示变量状态、输入一些交互指令，等等。目前已经可以和 vscode 对接调试。上面这个想法只是锦上添花做点好玩的东西，或许也更方便。

- 单步调试需要实现gdb那样的远程调试协议api，代码生成还需要适配devtools的source map规范，inspector的话也同样需要一套基于json的远程协议

- 阿里就有这个东西，我们自己的游戏引擎也是基于这个做的 OpenSumi

- ## [AutoDev for VSCode 预览版：精准 AI 编程提示词与编辑器的完美融合 - 知乎 _20240506](https://zhuanlan.zhihu.com/p/696080970)
- 我们将 AutoDev for Intellij IDEA 平台的非凡开发者体验带到了 VSCode 平台。在 IDEA 版本中通过构建非常精准的提示词，以及与编辑器的完美融合， 以帮助开发者更好地编写代码。
- 在设计 IDEA 版本时，我们一直致力于避免使用聊天窗口，以提供更好的用户体验。在 VSCode 版本中，我们将这一理念继续发扬光大。
- 不断地重构我们的架构，以实现精准测试生成所需要的上下文件：
  - 输出准确的测试文件路径
  - 与编辑器的完美融合
  - 函数的相关代码类（输入和输出）表示
  - 基于依赖工具的测试框架分析
- 如下是基于上述的设计理念的 Prompt 示例：
  - 通过读取依赖文件，如build.gradle，我们能够准确地知道项目的依赖，以及测试框架的使用。
  - 通过对函数的上下文分析，我们能够准确地知道函数的输入和输出，以及函数的相关代码类。
  - 通过精准的上下文，可以有非常高的信心直接生成测试代码。

- 在当前的 VSCode 0.1.0 版本中，我们实现了以下的核心功能：
  - 自定义 AI 指令，即通过自定义 prompt 来实现自定义的 AI 指令。
  - 测试生成，即通过 AI 生成测试代码。
  - 注释生成，即通过 AI 生成注释。
  - 语义化搜索核心逻辑，尚未集成到功能中。

- 
- 
- 

- ## [如何看待华为云 Cloud IDE 和 VSCode online 高度相似？ - 知乎](https://www.zhihu.com/question/383168806)
- 首先要明确一点，华为云CloudIDE 是基于 Eclipse Theia 开发，而不是 VS Code。
- Eclipse Theia 使用了 Monaco Editor
  - Eclipse Theia 支持 Language Server Protocol（LSP）
  - Eclipse Theia 支持 Debug Adapter Protocol（DAP）
  - Eclipse Theia 支持运行 VS Code 的插件（支持大部分的 VS Code 插件 API）
