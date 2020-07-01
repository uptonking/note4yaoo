---
tags: [react, rewrite]
title: note-react-rewrite
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-01T06:09:16.202Z'
---

# note-react-rewrite

## react core

## reinvent the wheel

- ref
  - [React 实践揭秘之旅，中高级前端必备(上)](https://github.com/xd-tayde/blog/blob/master/ReactGL-1.md)
  - [React 实践揭秘之旅，中高级前端必备(下)](https://github.com/xd-tayde/blog/blob/master/ReactGL-2.md)
- 框架最核心的 `JSX - Render - Diff - Update` 的渲染更新机制
  1. `JSX` 是一种 **动态模板语法**，通过 `Babel` 编译为 `createElement` 函数；
  2. `createElement` 将 `JSX` 转换为 **虚拟Dom(VNode)**，包含完整的标签信息 (类型、属性、子级列表)；
  3. **虚拟DOM** 是一种 **牺牲最小性能与空间，换取 架构优化** 的方式，其 **组件化** 以及 **解耦** 的思想，提高了项目的拓展性、复用性与可维护性，同时为 **跨平台渲染** 奠定基础；
  4. 通过实现 `createElm` 与 `render` ，完成 `VNode` 的 **初次渲染**；
  5. `Diff` 是一种 **计算得出两个 VNode 差异** 的算法，使用 **同层比对、唯一标识、组件模式** 优化了算法比对性能，将时间复杂度降低为 `O(n)` ；
  6. 列表比对 ( `diffChildren` ) 采用 **两端比对算法 + Key值比对** 算法，大大提高了 `Diff` 效率；
  7. 实现 `diffVNode` 、 `diffProps` 、 `diffChildren` ，完成 `VNode` 的 **动态更新**；
- `Component` 保持了动态UI与逻辑的分离，同时方便复用element
- `setState` 中更新状态，调用render生成新虚拟节点(newVNode)，触发diff更新。
  - 每执行一次setState，就需要重新生成newVNode进行diff，当组件复杂时或者连续更新时，可能会导致主进程的阻塞，造成页面的卡死
  - setState异步化，避免阻塞主进程
  - setState合并，多次连续调用会被最终合并成一次
- 为了让业务方能够编写业务逻辑插入组件的渲染工作流中，可以为组件设计添加生命周期方法
