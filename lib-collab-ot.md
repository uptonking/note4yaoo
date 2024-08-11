---
title: lib-collab-ot
tags: [collaboration, lib, ot]
created: 2021-10-14T10:55:05.828Z
modified: 2022-04-05T10:09:36.436Z
---

# lib-collab-ot

# guide22

- who is using #ot
  - ckeditor, tinymce, typewriter
  - odoo/o-spreadsheet
  - mongodb realm Atlas Device Sync Protocol
- who is using #sharedb
  - am-editor

- tips
  - 就算使用ot，大多产品都会使用定制的ot或变体，如ckeditor, prosemirror
  - 除了ot冲突处理逻辑，对op的存储、同步、业务实体抽象逻辑也很重要

- 🔲 not-yet
  - otjs示例
    - ❓ undo/redo未分析计算逻辑，以及ot里undo和cm组件undo的执行流程
    - codemirror内容的变更changes事件转换为TextOperation的流程
    - 中文输入法优化

- 🆚️ ot vs crdt
  - **ot的主流实现依赖中心服务器决定op的接收顺序，server根据版本号判断是否接收op**
    - server发送到客户端的是转换后的op，opPrime
    - op在不同客户端的apply顺序可能不同
    - crdt的op可乱序到达其他节点

- 协作方案参考
  - Liveblocks, synced-store, FluidFramework, gun
  - automerge (2017), yjs (2015), sharedb (2013)

- [SharedPen 之 Operational Transformation，基于ot.js](http://objcer.com/2018/03/05/SharePen-Operational-Transformation/)
  - 比较全面地介绍了operation指令、apply、compose、transform、undo/redo、服务端时序

- [浅谈在线文档的那些事儿： ot.js + easysync](https://www.cnblogs.com/cangqinglang/p/16016117.html)
  - 使用示例解释了 diff-match-patch 和 ot.js 的原理，ot.js是针对纯文本的一种实现
  - 分析循环过程解释了ot transform
  - 简单解释了easysync，easysync也是OT算法的一种实现，它被使用在etherpad中，定义了changeset的概念去描述文档的变更。

- [腾讯文档 揭开在线协作的神秘面纱 – OT算法_201907](http://www.alloyteam.com/2019/07/13659/)
  - 解释了ot.js的transform代码、时序控制

- [协同编辑 - OT算法](https://github.com/z2014/Blog/issues/28)
  - compose + transform 流程图
  - compose一般是同一用户的两个操作且有序，transform一般是不同用户的两个操作且可无序，注意分析baseLength和targetLength的关系

- [协同编辑冲突处理算法之OT算法](https://www.douzhixuan.com/xie-tong-bian-ji-chong-tu-chu-li-suan-fa-zhi-otsuan-fa/)
# dev

## Transform Property 2

- [TP2 Properties](https://github.com/ottypes/docs#tp2-properties)
- Transform property 2 is an additional requirement on your `transform` function. 
  - Specifically,  `transform(op3, compose(op1, transform(op2, op1))` == `transform(op3, compose(op2, transform(op1, op2))`
- If your OT type supports transform property 2, set the `tp2` property to true and define a prune function.
  - `tp2`: (optional) Boolean property. Make this truthy to declare that the type has tp2 support. Types with TP2 support must define prune.
  - `prune(op, otherOp)`: The inverse of transform. Formally, apply(snapshot, op1) == apply(snapshot, prune(transform(op1, op2), op2)). Usually, prune will simply be the inverse of transform and prune(transform(op1, op2), op2) == op1.

- [OT wiki](https://en.wikipedia.org/wiki/Operational_transformation)

- Various transformation properties for ensuring OT system correctness have been identified. 
  - These properties can be maintained by either the transformation control algorithm or by the transformation functions.
  - Different OT system designs have different division of responsibilities among these components. 
  - The specifications of these properties and preconditions of requiring them are given below.

- Convergence properties
  - CP1/TP1: For every pair of concurrent operations {\displaystyle op_{1}}op_{1} and {\displaystyle op_{2}}op_{2} defined on the same state, the transformation function T satisfies CP1/TP1 property if and only if
  - CP2/TP2: For every three concurrent operations {\displaystyle op_{1}, op_{2}}op_{1}, op_{2} and {\displaystyle op_{3}}op_{3} defined on the same document state, the transformation function T satisfies CP2/TP2 property if and only if

- Inverse properties
