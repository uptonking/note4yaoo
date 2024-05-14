---
title: lib-editor-code-cursorai-community
tags: [community, cursorai]
created: 2024-05-14T03:19:08.192Z
modified: 2024-05-14T03:19:17.644Z
---

# lib-editor-code-cursorai-community

# guide

# discuss-stars
- ## 

- ## [为什么我觉得 AI 写代码纯属添乱? - 知乎](https://www.zhihu.com/question/590636216)
- 首先我是Copilot重度用户, 有Copilot的白嫖使用资格, 在仅支持VSCode时使用的比较少, 在Visual Studio 2022有copilot插件后, 基本是每次代码必用, 我日常基本使用C语言，总结一下copilot写C代码的一些特点:
  - 第一、如果说Copilot的代码能用，当且仅当Copilot写的代码刚好是你想写，想这么写，你写出来和Copilot的生成的代码基本一样的情况，你必须审计并清楚的知道生成代码每一行的所有细节及意义，这个代码才能够使用。如果靠给注释直接生成稍微长一点点的功能代码，翻车几率极高。
  - 第二、Copilot非常擅长生成类比代码，比如你写了一个NodeRotateLeft（树节点左旋），那么之后你写一个一样的函数NodeRotateRight（树节点右旋），那么Copilot帮你补全的概率极高
  - 第三、如果你自己写的代码有逻辑漏洞或bug，那么Copilot生成出来的代码极大可能也带有同样的逻辑漏洞与bug
  - 第四、那种非常常见的代码和逻辑功能代码，copilot的补全成功率很高，但一些高度定制化的功能代码，一般需要前面已经写过类似代码提供给copilot“联想”，否者生成的基本不太靠谱。
  - 第五、用的久了你几乎猜得到哪些代码Copilot是能够补全的，哪些代码是可以比较放心让Copilot帮你补全的，这个时候Ctrl+alt+\这个快捷键就很好用了。

- AI写代码最大的问题还是事实检测的问题，它不考虑当前的代码对不对，尤其是变量名，函数名补全，它可以非常肆意妄为。
  - 而这个是传统IDE补全代码的强项，因为它们只会检索你声明过的东西。

- 
- 
- 

- ## [请问cursor-IDE与copilotX两个工具使用体验如何？相比较而言哪个对程序员帮助更大一些呢？ - 知乎](https://www.zhihu.com/question/593171282/answers/updated)
- [AI编程工具Copilot、Tabnine、Codeium和CodeWhisperer之间的竞争 - 知乎](https://zhuanlan.zhihu.com/p/630213524)

- 更喜欢cursor聊天式帮忙生成代码。

- 做工程不会拿着ai一路问到底的，cursor 就项目初开的时候用得多，路走顺了，就一个copilot帮补一下。
# discuss
- ## 

- ## [集成 GPT-4 的代码生成器 Cursor 使用体验如何？怎么用更高效？ - 知乎](https://www.zhihu.com/question/590152131)
- Cursor 之所以能火起来，就是因为它主打一个亮点：通过 GPT-4 来辅助你编程，完成 AI 智能生成代码、修改 Bug、生成测试等操作。
- cursor 让我感觉爽的点主要是：
  - 能够准确理解需求：如 “先构建 return 矩阵，然后一次性计算相关性” 这样的 instruction，人都不一定能第一时间 get 到我在说什么。
  - 自动纠错：贴报错堆栈就能自动修复问题。
  - 生成速度快：这一点在高频使用时还是比较重要的。
  - 另外 cursor 能够自动生成单元测试和文档，这对于广大不爱写测试和文档的程序员简直是福音！

- 交互体验一般般，就是一个demo级的工具应用。可以用它来生成模版代码，但没法用它来写工程代码

- cursor就两个mit毕业生开发的，上周提交的hello world是真的有点hello的意思了。
  - cursor好像在1月拿到了openai的风投，想乘着市场热度尽快上线，代码质量别想了，和vscode不知道相差多少个层次，现在只是用electron套了个codemirror来实现，一行测试用例都没有。
  - 它目前最大优势是理解项目工程和免费（这个优势已经没了），相比之下可能还是copilot x靠谱点

- 期待看到完整架构都自动实现的那一天, 目前的单个文件还不够

- 体验很好，让Cursor自动生成过C、C++、python、Arduino、latex公式、简单的markdown文稿，至于怎么样使用最高效，我觉得应该是和自己的知识体系有关

- 
- 
- 

- ## [如何评价Cursor？ - 知乎](https://www.zhihu.com/question/590754839/answers/updated)
- Cursor 编辑器在 GitHub 上是开源的，可以自由访问。
  语法高亮
  自动完成
  智能缩进
  括号匹配
  多光标编辑
  远程文件编辑
  可拓展性
