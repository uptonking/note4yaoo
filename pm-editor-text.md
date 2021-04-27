---
title: pm-editor-text
tags: [editor, pm, product]
created: '2020-07-13T13:50:42.498Z'
modified: '2021-04-19T15:06:33.233Z'
---

# pm-editor-text

# guide

- block-style editor
  - 内容视觉上为block，默认互不影响
  - 能够选择多个block/card，然后一起拖拽移动
    - 优点是灵活，缺点是凌乱，还可以参考masonry布局

# 编辑器开发体验

- 编辑器大致分为两种: 源代码编辑器和富文本编辑器，可以基于富文本实现源代码编辑器
- 基于HTML DOM的Contenteditable属性来实现(传统方式)
  - 代表是UEditor、TinyMCE、Quill
  - contenteditable是浏览器DOM的一个原生属性，值为true时表示该元素变为可编辑状态
  - 因此原生就直接支持很多内容编辑操作，包括光标位移、内容选择的行为、键盘事件（如方向键控制光标）等等
  - 辅以iframe技术，可以将编辑器放在一个独立的docment对象下，与页面的document对象分离
  - 问题
    - 编辑器中存在不可编辑元素，会有浏览器兼容性的问题，如火狐浏览器下光标无法正确移动甚至无法删除这个元素
    - 用户行为难以控制，难以抽象编辑器内的视图逻辑关系并将它们映射到代码模型中
    - 光标（选区）的视觉位置与逻辑位置可能不吻合
- 基于自定义Model的实现
  - 代表是draft.js、trix
  - 定义一套编辑器内部使用的数据结构（model），与用户在编辑器内所见的Dom视图相映射
  - 通过捕获用户的操作行为，由原先的直接操作Dom，改为更新数据结构状态，再将更新后的状态映射至视图的方式，来实现编辑器的所见即所得
  - 由于用户操作实际影响的是内部的数据结构，且每次操作产生的结果都被控制在一定范围内（只影响部分节点），可以较为容易的通过锁和diff算法来合并短时间内的多次修改
- ref
  - https://zhuanlan.zhihu.com/p/37051858
  - https://www.zhihu.com/question/24328297
  - https://www.oschina.net/translate/why-contenteditable-is-terrible

# text-editor-solution-catalog

- react-page
  - renderer package基于slate实现

# discuss

- [主流的开源「富文本编辑器」都有什么缺陷？](https://www.zhihu.com/question/404836496/answers/updated)

- https://www.zhihu.com/question/404836496/answer/1319381793
- 美团的学城、印象笔记的超级笔记都是 ProseMirror。
  - 另外，PM并不是一个开箱即用的编辑器，需要写 Schema 定结构；其渲染出来的内容是完全的 html；标准用法就是按照 Schema 中确定的结构来渲染 DOM，特殊用法比如表格，或者自定义元素渲染可以使用 Angular、React 这种做视图层。

- 我必须要再提下最新 slate 5.* 以上的版本，大概做了下面几件事：
  - 使用TypeScript重构。
  - 使用immer替换immutable，数据就是纯粹的JS对象，调试的时候再也不用.toJS()了。
  - 新的插件机制，以前的插件机制我定义为仿洋葱模型，包装了太多层的调用栈，新插件机制就是简单的高阶函数实现的，很容易就能定位到代码实现。
  - 使用WeakMaps记录DOM元素与Node节点与节点Path之间的关联，不再依赖于nodeRef以及DOM的data-key属性。
  - 不得不说新的API更优雅了。
  - Slate最核心的针对数据处理操作基本实现测试覆盖

- 特别想研究Prosemirror是因为Confluence的编辑器技术用的是Prosemirror
  - ProseMirror是CodeMirror作者打造的另外一款编辑器。
- 区别一：定位不同
  - Prosemirror是一款可以直接用的编辑器，而Slate是底层框架，它不提供编辑器功能实现和预设
- 区别二：框架
  - Prosemirror是基于原生JS和HTML的实现，而Slate是框架之上的产物。
  - 看过一些Prosemirror实现的介绍，它也有虚拟DOM的概念，它的设计思想、基于编辑器业务的地位，类似于React之与它之上的业务地位是一样的，粗略的认为Prosemirror和React是同级别的。
- 区别三：可扩展性
  - Slate的扩展能力更强，主要是想说它的实现方式更多更灵活、更容易理解，不是说Slate能做而Prosemirror做不了。
- 区别四：细节处理
  - 因为定位不同，所以Prosemirror无疑更稳定有些特殊场景Prosemirror处理的非常到位。
  - 比如Slate中最困扰我的就是块级元素前后无法设定焦点的问题（没有焦点就无法在元素前后按Enter创建空段落），前后有焦点会让编辑器使用起来更流畅，这方面语雀做的最好，Prosemirror也提供了一个gapcursor的模块专门处理这个问题
- 时间已经来到2021年，不得不说真快，主要更新下前面提到的闪烁的焦点问题，这个需求在Slate中已经有方案，而且交互效果要比Prosemirror的gapcursor要好一点点，足以体现Slate的扩展能力还是可以的
