---
tags: [react, rewrite]
title: note-react-rewrite
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-01T06:09:16.202Z'
---

# note-react-rewrite

## react-core

## react-hooks

- ref
  - [使用 React Hooks 重构你的小程序](https://aotu.io/notes/2019/07/10/taro-hooks/index.html)

- Hooks是React函数内部的函数，要实现Hooks最关键的问题在于两个:
  - 找到正在执行的React函数
  - 找到正在执行的Hooks的顺序
- 可以设置一个全局对象 `CurrentOwner` ，它有两个属性，第一个是current，是正在执行的Taro函数，我们可以在组件加载和更新时设置它的值，加载或更新完毕之后再设置为null；第二个属性是index，它就是CurrentOwner.current中Hooks的顺序，每次我们执行一个Hook函数就自增1
  - 在React中其实也有这么一个对象，而且你还可以使用它，它叫做 __SECRET_INTERNALS_DO_NOT_USE_OR_YOU_WILL_BE_FIRED. ReactCurrentOwner
- 接下来实现 `getHook` 函数找到正在执行的Hook，如果CurrenOwner.current是null，那这就不是一个合法的hook函数，我们直接报错。如果满足条件，我们就把hook的index + 1，接下来我们把组件的Hooks都保存在一个数组里，如果index大于Hooks的长度，说明Hooks没有被创造，我们就push一个空对象，避免之后取值发生runtime error。然后我们直接返回我们的Hook
- 实现 `useState` 。首先如果initState是函数，直接执行它。其次调用我们我们之前写好的 `getHook` 函数，它返回的就是Hook的状态。接下来就是 useState 的主逻辑，如果hook还没有状态的话，我们就先把正在执行的组件缓存起来，然后 useState 返回的，就是我们的hook.state, 其实就是一个数组，第一个值当然就是我们initState，第一个参数是一个函数，它如果是一个函数，我们就执行它，否则就直接把参数赋值给我们的hook.state第一个值，赋值完毕之后我们把当前的组件加入到更新队列，等待更新

``` typescript
// 全局对象存放正在执行的hook函数和其在hooks数组中的顺序
const CurrentOwner: {
  current: null | Component<any, any> ,
  index: number
} = {
  // 正在执行的 Taro 函数,
  // 在组件加载和重新渲染前设置它的值
  current: null,
  // Taro函数中hooks的顺序每执行一个Hook自增
  index: 0
}

// 查找正在执行的hook
function getHook(): Hook {
  if (CurrentOwner.current === null) {
    throw new Error( `invalid hooks call: hooks can only be called in a taro component.` )
  }
  const index = CurrentOwner.index++ // hook 在该 Taro 函数中的 ID
  const hooks: Hook[] = CurrentOwner.current.hooks // 所有的 hooks
  if (index >= hooks.length) { // 如果 hook 还没有创建
    hooks.push({} as Hook) // 对象就是 hook 的内部状态
  }
  return hooks[index] // 返回正在执行的 hook 状态
}

// hook实现
function useState<S>(initialState: S | (() => S)): 
[S, Dispatch<SetStateAction<S>> ] {
  if (isFunction(initialState)) { // 如果 initialState 是函数
    initialState = initialState() // 就直接执行
  }
  const hook = getHook() as HookState < S > // 找到该函数中对应的 hook
    if (isUndefined(hook.state)) { // 如果 hook 还没有状态
      hook.component = Current.current! // 正在执行的 Taro 函数，缓存起来
        hook.state = [ // hook.state 就是我们要返回的元组
          initialState,
          (action) => {
            hook.state[0] = isFunction(action) ? action(hook.state[0]) : action
            enqueueRender(hook.component) // 加入更新队列
          }
        ]
    }
  return hook.state // 已经创建 hook 就直接返回
}
```

## reinvent the wheel

- ref
  - [从零开始的 React 再造之旅](https://segmentfault.com/a/1190000021689852)
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
