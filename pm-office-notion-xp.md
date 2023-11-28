---
title: pm-office-notion-xp
tags: [notion-like, office, pm, xp]
created: 2022-03-17T17:49:28.980Z
modified: 2023-11-28T14:48:45.910Z
---

# pm-office-notion-xp

# inspiring

- 使用多维表格组件进行文档管理，而不是用文档树、文件夹
# usage

# pros

- powerful database views and organization
# cons
- 缺少类似flomo、tldraw这样的快速笔记入口
# features

## 文本格式类

- notion不支持左中右对齐
  - [How to center text alignment like this?__202201](https://www.reddit.com/r/Notion/comments/rry43b)

## block操作类

# notion教程-沙牛清单
- notion三大特性
  - 模块化操作：拖拽、转换、分栏
  - 内容结构化：子页面
  - 数据化
# guide
- [Notion保姆级公开课](https://www.bilibili.com/video/BV1EP4y1s7Bp/)

- [Obsidian的保姆级公开课](https://www.bilibili.com/video/BV1H44y1n71k/)
# blogs

## [Notion编辑器原理分析](https://zhuanlan.zhihu.com/p/359122473)

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

- ref
  - [探索 Notion 的实现](https://zhuanlan.zhihu.com/p/152964640)
# discuss
- ## 

- ## 

- ## 

- ## Craft 对开发者太不友好，社区也没运营起来，因此我又从 Craft 转移到 Notion 了。
- https://twitter.com/_Xheldon/status/1637481908136468480
  - 本来想找个现成的迁移工具，研究了一下 Notion API，发现它不支持图片上传，然后正当要放弃的时候，尝试了 Notion 导入 Word，发现它可以把 Word 中内嵌的图片上传到自己的 AWS 服务上，因此我想了个曲线救国的办法，
  - 就是先将 Craft 全部文件导出到 Markdown 格式，同时它会在导出的时候，将文件中引用的图片放到 .md 文件的同级目录，之后我再使用 pandoc 工具，将 Markdown 文件转成 docx 文件即可。当然，Notion 导入 Word 不支持嵌套文件夹，所以我只能将所有文件到处到同一个目录后，手动调整层级。
  - 需要注意的是，Notion 不支持超过 50M 的文件导入，因此你可能需要分割一下大文件，导入后再合并。

- ## Front-end Practical Q: Has a particular algorithm in a function body ever been the reason your app is slow?
- https://twitter.com/jitl/status/1615423205380091904
  - e.g. I used `Array.indexOf` instead of keeping track of nodes I've seen in an object.
- indexOf very well could be faster in most cases than using a set

- Yes in @NotionHQ:
  - O(n^3) checks against a block's ancestors; always lock up the UI or cause backend latency spikes
  - O(n^2) checks for "closest neighbor UI element" in list of UI elements; caused jank on large pages
  - Array.indexOf -> Set.contains is a win in inner loops with big N
- Another case is searching our tree-like data model, eg for "what is the next block with a comment after this block, in DFS order?". 
  - For that use-case, I built a memoized, reactive subtree traversal. Substantially reduced jank on larger pages for a bunch of systems.

- My exp: large app had a lot of perf problems stemming for inefficient uses of simple loops, for instance: instead of using Array.filter folks would Array.forEach into another array and return the new array. Do this nonsense enough times and you will see perf issues. Sometimes for virtualized lists. They did this when chunking (lazy display) of data for instance. Some loops were simply unbound. Others were nested. It was just poorly architected across the board

- In Flutter Apps working with long lists or graphics based on lots of data, the types of loops I use and how I keep track of things I've seen and can disregard on future iterations makes a huge difference in rendering performance.
