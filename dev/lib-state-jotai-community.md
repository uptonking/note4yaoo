---
title: lib-state-jotai-community
tags: [community, jotai, state]
created: '2022-01-05T14:25:11.950Z'
modified: '2022-01-05T14:25:35.961Z'
---

# lib-state-jotai-community

# guide

# discuss
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
