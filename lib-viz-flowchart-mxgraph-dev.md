---
title: lib-viz-flowchart-mxgraph-dev
tags: [flowchart, mxgraph, viz]
created: 2023-05-29T15:08:59.025Z
modified: 2023-05-29T15:09:30.865Z
---

# lib-viz-flowchart-mxgraph-dev

# guide

- features
  - 示例丰富

- pros
  - no dependencies
  - 支持多种绘图实现，默认svg，可自己实现canvas
  - 可前端使用

- cons
  - 不适合绘制大量图形元素
  - 代码不够模块化

- tips
  - 主要用于流程图，不必在支持任意图形编辑和pdf编辑上花费过多精力

- resources
# dev
- 插入图形的一般流程
  - graph.insertVertex
  - graph.insertEdge
# not-yet
- plugin设计
# architecture
- dataflow
  - Graph初始化时注册`InternalEvent.CHANGE`事件，会在model更新时更新view
  - 在事务的`endUpdate`方法中，默认会触发 change event

- model-layer GraphDataModel
  - Cell: 内容树节点，用于存储vertex、edge、group等图元的状态信息
  - `root: Cell` 节点树
  - `cells: { [key: string]: Cell }` 映射表
  - currentEdit changes data
  - updateLevel

- view-layer cellRenderer.redraw(state)
  - redrawShape
    - 若shape.style变化，则先`this.node.parentNode.removeChild(this.node);`清空dom
    - 若是新shape，则createShapeSvg + container.appendChild
  - redrawLabel
  - redrawCellOverlays
  - redrawControl
# model-layer

```JS
// as controller/manager
class Graph extends EventSource {

  constructor() {
    this.model = new GraphDataModel();
    this.view = this.createGraphView();
    this.cellRenderer = this.createCellRenderer();

    this.getDataModel().addListener(
      InternalEvent.CHANGE,
      () => {
        this.updateSelection();
        // update dom
        this.view.validate();
        this.sizeDidChange();
      }
    );
  }

}

class GraphDataModel extends EventSource

class GraphView extends EventSource

class GraphSelectionModel extends EventSource
```

# codebase

# blogs

## [mxgraph 系列](https://juejin.cn/post/6844904148379369480)

- [mxGraph 如何实现图形拖动 - 掘金](https://juejin.cn/post/6844904177005674504)

### [mxgraph 系列【3】： 底层状态树 mxCell](https://juejin.cn/post/6844904166817529870)

- mxgraph 内部使用一种树形数据结构记录图形文档的内容，在内容树上，每一个节点代表一个图形元素，元素信息会被存储在节点对象上；
  - 节点的父子关系表示父节点图形包含子节点图形，可以用于实现图形的分层、分组功能。
- 内容树是图形文档的底层数据模型，有点像 vdom 之于 react；vnode 之于 vue。
  - 渲染器 mxCellRenderer 根据内容树渲染出图形文档；
  - 编解码器 mxCellCodec 实现了外部存储格式与内容树之间的互相转换；
  - 各种 布局算法 的基本操作单位也都是内容树节点

- 内容树模型由以下几个类实现：
  - mxGraphModel: 内容树模型，主要实现一系列树结构操作方法。
  - mxCell: 内容树节点，用于存储图形、连接线、分层等图元的状态信息。
  - mxGeometry: 树节点的几何信息，记录了图形元素的宽高、坐标位置；连线的开始节点、结束节点等几何特性。
- 本文主要关注内容树节点 mxCell 的用法

### [mxgraph 系列【4】：事务管理](https://juejin.cn/post/6844904193094860808)

- 事务 是 mxGraph 内部实现的一套更新控制方法，在一次事务过程会持续收集所有变更请求，直到事务结束后一次性推送到渲染器 mxCellRenderer 执行图形UI更新，或者在出现异常时允执行回滚。
  - 技术上来说， 事务 并不是必要的，我们可以直接使用图形更新接口，结果会被即时渲染到图形上

- 事务 本质上是借助某种技术手段，将多个原子操作绑定成单个复合操作，
  - 事务过程中如果所有原子操作都成功执行，则该事务被视为成功，
  - 若其中任何一个出错，则视情况可选择回滚整个事务操作，以保证操作前后系统状态的一致性

- mxGraph 比较推荐的写法，特点是将更新操作放入 try-catch 块中；
  - 将 beginUpdate 调用放在 try-catch 前；将 endUpdate 放在 finally ，这样即使更新过程触发异常，也能正常渲染异常代码行之前的更新操作

```JS
// 启动一次更新事务
const model = graph.getModel();
model.beginUpdate();
try {
  // 插入一个矩形
  const v1 = graph.insertVertex(parent, null, 'Hello,', 20, 20, 80, 30);
  // 插入第二个矩形
  const v2 = graph.insertVertex(parent, null, 'World!', 200, 150, 80, 30);
  // 连接两个矩形
  graph.insertEdge(parent, null, '', v1, v2);
} finally {
  // 结束更新会话
  model.endUpdate();
}

// 上例 try-catch 模板代码同样适用于基于 promise 的异步操作，不过不能用 then 回调风格，而需要改用 async-await 风格
```

- 默认情况下在 try-catch 中出现异常中断时，异常语句之前的更新代码会被正常执行，而之后的代码则没有应用到图形上
  - 此时，视场景需求可选择使用 mxGraphModel.prototype.currentEdit.undo 接口回滚所有操作

- 事务 的实现代码其实特别简单，主要完成：
  - 执行 beginUpdate 时， this.updateLevel++
  - endUpdate 则 this.updateLevel--
  - 在 endUpdate 函数内部，判断若 this.udpateLevel === 0，则
    - 触发 endUpdate 事件
    - 调用 this.currentEdit.notify() 通知 mxGraph 执行图形更新流程
    - 重置 this.currentEdit 对象

- 事务接口支持嵌套调用
  - 为方便讨论，两种情况区分对待，首次调用称作 事务 ，后面的调用统一称为 会话，两种调用时机形成一种栈结构
- 这种设计能够实现无论嵌套了多少次会话，只有最外层会话执行了 endUpdate ，计数器 updateLevel 归0后才开始将更新绘制到图形上，
  - 事务过程中的更新操作不会被立即执行，某种程度上也提升了框架的性能。

- 事务过程触发的事件包括：
  - startEdit
  - beginUpdate
  - execute
  - executed
  - endUpdate
  - endEdit
  - beforeUndo
  - change, 通知渲染层执行更新
  - notify
  - undo

- model 实例内部维护了一个 currentEdit 对象，用于记录单次事务的所有更新操作
  - 通过 changes 属性记录了事务中的更新操作，并提供undo、redo接口用于撤销或重做该次事务变更

## [mxGraph源码学习_201810](https://blog.csdn.net/white_idiot/category_9280005.html)

- [【mxGraph】源码学习：（5）mxGraph](https://blog.csdn.net/White_Idiot/article/details/83034314)

### [【mxGraph】源码学习：（6）mxGraphModel](https://blog.csdn.net/White_Idiot/article/details/83061067)

- graph model充当事务包装器，其中包含所有更改的事件通知，而cell包含用于更新实际数据结构的原子操作。
- 每个cell都包含在一个图层中。如果不需要图层，则应将所有新cell添加到默认图层。
  - 图层可用于隐藏和显示cell组，或用于将cell组放置在显示中的其他cell之上
# more
