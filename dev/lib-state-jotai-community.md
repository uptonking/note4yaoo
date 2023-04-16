---
title: lib-state-jotai-community
tags: [community, jotai, state]
created: 2022-01-05T14:25:11.950Z
modified: 2022-01-05T14:25:35.961Z
---

# lib-state-jotai-community

# guide

- jotai-examples
  - https://github.com/dai-shi/katachidraw
# discuss-stars
- ## Demystifying the internal of jotai https://jotai.org, an atomic state management solution for @ReactJS .
- https://twitter.com/dai_shi/status/1484835169475653634
  - Here's a simplified version of the core.
  - Notice that this simplified version of jotai core is **not** pseudo code. It actually works!
  - https://codesandbox.io/s/zealous-field-z2xk6?file=/src/App.js

- in the `useAtom` hook, there is still a `useState`. how does this behave in nested components when this useAtom hook is accessed on the top level? does it still cause a rerender to all children? if yes, what is the advantage/difference of jotai from react's `context+useState`?
  - Yes, all child components under the tree re-render, unless they are memoized (or stable). 
  - The advantage is 1) simpler syntax, and 2) dynamic atom creation without re-mounting the entire tree (which is impossible with context).

- Jotai implementation uses useReducer instead of useState. 
  - It's slightly different in terms of timing when it reads atomState.value, which confuses people with extra re-renders without commits. 
  - Here's updated simplified Jotai implementation.
  - https://twitter.com/dai_shi/status/1552819673716375552

- this simplified version of zustand is **not** pseudo code. It's usable.
  - https://codesandbox.io/s/purple-tree-noyy6?file=/src/App.js
  - https://twitter.com/dai_shi/status/1484851943696924677

- a simplified version of valtio 
  - https://twitter.com/dai_shi/status/1484496249776934917
  - valtio is my take with the same mental model as mobx.
- here's the full version of the simplified version of Valtio
  - https://codesandbox.io/s/modest-currying-mu0j7
  - https://twitter.com/dai_shi/status/1485036663290368002

- ## Everyone seems excited about React without memo presented at React Conf 2021? Here's jotai approach to eliminating memo.
- https://twitter.com/dai_shi/status/1468875799327817730
  - https://codesandbox.io/s/jotai-approach-to-react-without-memo-0ue18
- Yeah, there are some drawbacks, and it's not something to recommend right away for production. 
  - The mental model is the one, another is probably the lack of devtools support. there can be some others. 
  - All that said, I guess the approach is valid and effective.
# discuss
- ## 

- ## 

- ## 

- ## 我觉得jotai的逻辑是每个atom不是真正的数据，而是数据的accessor，具体是什么值靠的是依赖注入的store（默认defaultStore）。
- https://twitter.com/himself_65/status/1647292653187334146
  - 我这里要封装一层模块级别的atoms（类似于atomsFamily），方便团队开发和测试
- 赞这个描述。jotai 是一个依赖注入的方式，而不是单纯的替换 useState 乱扔的全局变量。

- ## Jotai https://jotai.org atoms are primarily for bottom-up approach, but it can do top-down approach like zustand. 
- https://twitter.com/dai_shi/status/1477593623156105217  /20220102
  - So, I created a ToDo app with a single store with jotai. 
  - As a bonus, it uses `atomWithHash` , so the state is persisted in the URL.
  - https://codesandbox.io/s/jotai-single-store-pmi40

    - store的定义基本类似redux的单store，更新方法也类似redux
      - 在顶层实现了useSelector、useDispatch
    - 取值 useSelector(useCallback((state) => state.filter, []));
    - 更新 dispatch({ type: "REMOVE_TODO", id }
    - 写法上
      - store的更新方法行数更多
      - App.tsx应用层思路更清晰，取值只需要确定正确的路径，更新方法是统一的
      - 需要考虑如何合并多个switch-case条件，特别是在更新方法很多时

  - Does zustand have something like atomWithHash?

    - no, not handy like atomWithaHash.

- I made another variant of the demo. 
  - https://twitter.com/dai_shi/status/1477796451900358657  /20220103
  - It's single state and top-down approach, but yet somewhat atomic. Thanks to `focusAtom` and `splitAtom`. And, persisted with atomWithHash. Jotai is very flexible!
  - https://codesandbox.io/s/jotai-todos-focus-atom-ledxb
    - store的定义和redux类似，但之后定义了根据顶层state定义了小的派生state作为单独atom
      - 更新方法可以直接取到小的派生state然后解构得到setState
    - 取值 useAtom(splitAtom(filteredTodosAtom))
    - 更新 const [, addTodo] = useAtom(addTodoAtom);
    - 写法上
      - store的每个小的派生state都需要写繁琐的set方法
      - App.tsx应用层要每次都要获取atom的setState，然后更新，更新逻辑不可复用
      - splitAtom的实现有点小bug，作者在示例中也标出了自己有疑问的地方

- ## i was initially hesitant to use valtio with its proxy-based APIs 
- https://twitter.com/_paulshen/status/1478792368274821122
  - but i've now replaced all jotai usage with valtio and may do the same with zustand
  - most of my usage are single-value atoms. i use an object with a single key `value` so valtio can observe changes (downside of proxy APIs).
  - valtio watches for all updates via proxies by default so i wrap objects with valtio's `ref` function to bypass the nested proxy.
- jotai is a great library but you're exposed to the complexity of react context. you can't read/write to atoms anywhere like you can with zustand and valtio.
  - Yeah, the fact that jotai is based on context is essential and that's why we created a new library even if we already had zustand.
  - The demand on reading/writing anywhere is high, and we are planning to expose a new experimental api
