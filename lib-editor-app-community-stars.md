---
title: lib-editor-app-community-stars
tags: [community, editor]
created: 2022-06-12T22:14:05.479Z
modified: 2022-08-21T10:12:02.964Z
---

# lib-editor-app-community-stars

# guide

- 编辑器研发方向
  - 实时协作
  - 版本控制
  - 离线存储
  - features
    - 开放api
    - 双向链接

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render

- not-yet
  - 搜索编辑器内容时，如何搜索带格式的文本，如关键词为 解构`props` 时如何搜索
  - 将bibtex插入编辑器的逻辑实现有问题，如何只在光标点击editor内容后才执行插入bibtex的command，否则就会出现现在的问题，鼠标若不再editor中点击一下就不执行该逻辑

- https://github.com/powcoding/etherpad-core  /仅文档和示意图/无代码
  - etherpad产生diff的2种方式
    - 点击菜单栏上的功能按钮
    - 用户在编辑器内不断的输入文字，那么etherpad通过定时检测来获取内容的变化
  - etherpad内嵌了自己的一个编辑器ace editor，不支持接入第三方富文本编辑器
  - 但etherpad具备了完整的实时协作机制，包括：客户端、服务器端的模型设计，多人冲突的设计，对富文本格式的解析，对输入法的支持等。
  - 如果能利用etherpad的实时协作机制，又能接入第三方编辑器，那就是一个完美的方案
  - etherpad产生diff的2种方式中的第1种方式，完全是etherpad自己的私有机制，没法接入第三方编辑器
  - 但是利用第2种方式，不管第三方编辑器如何改变编辑器内容，只要让etherpad定时去检测到变化，就能生成diff，后续流程完全和原生etherpad一致
  - 将etherpad对内置编辑器的绑定解耦，通过设计api暴露出来，可绑定到第三方编辑器上。这样第三方编辑器就具备了和原生etherpad相同的整套实时协作编辑的能力
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Writing Software to Last 50 Years | Hacker News_202001](https://news.ycombinator.com/item?id=22042186)
- Text files are king! I store every single byte I can in text files. Examples:
  - Tabular data     : TSV   (almost all Un*x/GNU tools handle this out of the box)
  - Simple "records" : GNU Recutils format (https://www.gnu.org/software/recutils/)
  - Formatted texts  : Markdown, LaTeX, ...
- If I need some hierarchical kind of information, I use a folder structure to handle this.
- I know that not everything can be stored as text. But I try to use open, well documented and future proof formats.
- If I really need to preserve original format/design of a web page: PDF

- [GNU Recutils - GNU Project - Free Software Foundation](https://www.gnu.org/software/recutils/)
  - GNU Recutils is a set of tools and libraries to access human-editable, plain text databases called recfiles. 
  - The data is stored as a sequence of records, each record containing an arbitrary number of named fields. 

- ## what's the best hybrid-structure code editor you've seen? an editor that combines tokens (eg values or references) and text
- https://twitter.com/_paulshen/status/1575187234449334273
  - do you back the semantic tokens with text? feels like you want some richer repr but hard for me to see how to make hybrid work

- honestly, soulver is the only hybrid editor I’ve found comfortable enough to use regularly
  - https://soulver.app/
  - Soulver is a notepad calculator app for Mac. It's a notepad that gives instant answers to calculations in your text.
  - Soulver is a better way to work things out than a classic calculator, and a more lightweight tool than a spreadsheet.

- https://www.jetbrains.com/mps/
  - MPS提供的软件开发环境可以创建新的定制语言，也可以扩展现有语言，然后用它们开发面向领域的应用。
  - MPS还可以定义新语言的类型系统、约束和专门的编辑器。MPS用一棵抽象句法树（AST）来维护代码。
  - MPS还采用了代码生成的办法：用新语言在更高的层次上表达，然后MPS生成Java、XML、HTML、JavaScript等语言的可编译代码。 用MPS建立新语言的时候，必须从BaseLanguage扩展。MPS已经提供了一些常用的BaseLanguage扩展，协助开发者处理字符串、容器、日期、正则表达式等语言成分。

- ## [对可多人协同编辑的在线编辑器，如何设计其 undo/redo 的逻辑？](https://www.zhihu.com/question/367915946/answer/985845505)
