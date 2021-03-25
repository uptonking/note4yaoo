---
title: pm-noter
tags: [note-taking, pm]
created: '2020-11-24T07:44:16.296Z'
modified: '2020-11-24T07:46:00.967Z'
---

# pm-noter

# guide

- 主要功能模块
  - file-explorer
    - 复刻vscode的文件管理器
    - 支持多个sidebar
    - 支持多种排序，包括创建时间、修改时间、tag

- 特色功能点
  - api doc
    - 生成openapi/swagger ui风格的文档
  - term block
    - 类似在一页ppt上只显示一个大号的单词/短语，以醒目突出
  - examples as notes

# faq

- 如何不使用图床而将图片直接嵌入到笔记生成的html中

- 参考
  - jupytext: jupyter notebooks as readable, editable documents
  - executable document

# features

## 协同编辑

- [在线编辑器, 多人同时编辑, 如何设计undo/redo的逻辑?](https://www.zhihu.com/question/367915946)
- 感觉有三种模式:
  - 按action撤销. 
    - 甲/乙撤销, 会消失一个c. (这样做我觉得容易做, 所有状态容易管理)
  - 只撤销自己做的. 
    - 甲撤销, 消失一个c; 乙撤销, 消失一个B. 
    - Google docs是这么做的, 但是交叉修改后再撤销重做, 应该会造成极大的混乱, 如何解决?
  - 一路撤销到自己做的. 
    - 甲撤销, 消失一个c; 乙撤销, 变成aaaBB. 这样就是有点绝情了. 甲想恢复自己的编辑, 需要乙重做.
- 一般采取的是第 2 种方式，即只撤销自己产生的操作。
  - 那么怎样才能实现只撤销自己产生的操作呢？这就不得不说说 OT（Operational Transformation）和 CRDT（Conflict-Free Replicated Data Type）算法了。
  - CRDT 在 2006 年被提出，用于解决分布式计算结果的最终一致性问题。
  - 相比较还存在很多边缘场景需要打补丁的OT算法，CRDT 可以说是更加先进一些。也有非常多开源的库可以选择，比如 yjs , automerge , gun 或者 teletype-crdt
  - 简单来说，OT 需要一个中心服务器（用于保证正确性），而 CRDT 则可以支持点对点直接传输数据。

# pieces
