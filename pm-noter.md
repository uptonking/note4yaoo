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

# features

- ## text-editing
- 选择多行文字，批量在行首添加`- `，转换成列表显示
- 选择一段文字，将其中的空格替换成`-`，方便区分比较双方，如 a-b vs c-d

# draft

- 功能或菜单太多容易使人迷茫，考虑设计多个版本的前端：lite、pro、customized

- unlocalizable
  - 移动本地文件时，自动更新其他文件中引用的链接
  - 图床

# faq

- 如何不使用图床而将图片直接嵌入到笔记生成的html中

- 参考
  - jupytext: jupyter notebooks as readable, editable documents
  - executable document

# discuss

- ## [在线编辑器, 多人同时编辑, 如何设计undo/redo的逻辑?](https://www.zhihu.com/question/367915946)
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

- ## [Notion 编辑器原理分析](https://zhuanlan.zhihu.com/p/359122473)
- 先了解怎么设计一款编辑器，做下铺垫，参考 facebook draft-js 的介绍视频
  - 文章讲了做一款编辑器为什么不直接使用 contenteditable，但又不能完全抛弃 contenteditable 的原因。
- 文章所指的主要原因是 contenteditable 中 DOM = State ，这里的 State 指存储用户输入的内容，为 html 格式；
  - 从用户操作发起到数据修改整个过程都由浏览器控制，但是各浏览器存在实现差异，造成 State 的结果不一致，兼容性问题多。
  - contenteditable 又有很多原生能力，速度快且支持所有的浏览器、如光标与选区、输入法事件等；ipad 下 contenteditable 也提供较多有意思的能力，如左右分栏时可直接从其它应用拖动文字到 contenteditable 中
  - 最终 draft-js 通过自定义 State，抛弃掉原生提供的 html 形式的 State，通过 contenteditable 提供的能力负责文字排版与用户事件接收，定义一套 op(Operation) 来修改 State ，同时把数据模型通过 react 渲染到 html 中，达到 controlled contenteditable。
- notion 也自定义数据层，设计了基于 Block-tree 的数据模型；
  - 渲染层用 React 把数据渲染成 html；
  - 使用 React 提供的事件(onInput\onCopy\onCut)或者工具条接收用户的操作指令，用户指令转换成 op；
  - 操作经过执行并修改数据模型 ，op 也会实时提交到服务端中改变后端数据库中的数据；
  - 服务端通过协同把 op 传给其他用户，达到一起编辑同一篇文章目的。
- 所以整个notion可以分两层，数据层专门负责存储数据；
  - 渲染层负责把数据渲染成界面，接收用户的事件并转化成 op 操作交给数据层执行。

- ### 数据层
- 在notion里一切都为block，如表格、图片、文字段落等，
  - block 通过 parent_id 来指向父 block，以此表达层级，如文章下有段落、表格、表格下有行、分栏下又可以圈套表格等。
  - 通过这种层级关系，就形成一棵 block-tree。
- 一个 block 最基本的几个属性为：
  - block_id
  - properties: 属性值，如段落中用户输入的文字
  - parent_id: 指向父 block id，形成 block tree
  - type: block 的类型，如表格、行、列、图片、段落等
  - version：版本，用于协同
- block 和 dom 节点对比，反过来想，dom tree 可以表达所有的用户界面，理论上来说 block tree 也能完成大部份编辑器的需求
- 有了数据模型后，接下来是需要对这棵数据模型进行修改，
  - 在 dom api 里，浏览器提供了节点的删除、增加、修改(属性)、移动等功能 。
  - 在 notion 里也一样，数据层通过提供 op 的方式给到渲染层来修改数据，常规对树的操作可以有两类
  - 节点位置移动、增加、删除
  - 节点属性修改
- 总结
  - 数据存储基于 tree，称为 block-tree，类似于 dom-tree
  - 定义一套 op 来表达修改数据意图，通过执行 op 来修改 block-tree

- ### 表现层/view
- 在打开一篇文档时会通过 blockId 去服务端拿到前 50 个子 block ，本地把这 50 个 block 缓存到内存中。
  - 此时服务端传回的和存在本地 store 的 block 并没有树形概念，而扁平化存储在 map 中，block id 为 key，block 值为 value；
  - 树形的构建是在渲染期建立，通过 block id，去 map 中找出所有的子节点递归渲染。
- 表现层的渲染大致流程为，第一步从服务端取出当前页的子 block 存放在 block cache 内存中，第二步从最顶上的 block 依次递归到叶子节点进行渲染。

- notion在产品能力上很优秀，打破了传统的笔记软件固化思维，与其说提供给用户的是一套笔记工具，而不如说是一套设计笔记软件的系统。
  - 但通过 block 能力的增强，能力更多了，可以用来做日常工作管理，团队 wiki 等。
  - notion整个软件架构的基建能力是把 block 的渲染、block 的存储、数据修改等都处理好，后期功能的增加可快速迭代，在基础上增加更多的 block 类型。

# pieces
