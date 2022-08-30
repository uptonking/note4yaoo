---
title: lib-app-tiny-write-rewrite
tags: [app, rewrite, tiny-write]
created: 2022-08-22T16:23:21.438Z
modified: 2022-08-22T16:23:59.496Z
---

# lib-app-tiny-write-rewrite

# guide
- block拖拽如何实现？
  - 跨block选择部分文本通过编辑器内置选区实现
  - 注意将段落拖拽到列表和将列表项拖出列表

- 基于block保存数据

- 基于electron如何实现crdt
# codebase

# solidjs-dev

- 对solidjs的依赖

```JS
// tiny-write
import { Show, onCleanup, createEffect, createSignal, onError, onMount, untrack, For, Switch, Match, splitProps } from 'solid-js';
import { createContext, useContext } from 'solid-js';

import { Store, createStore, createMutable, unwrap } from 'solid-js/store';

import { render } from 'solid-js/web';

// noteworthy
import { createResource, Suspense } from "solid-js";
```

- component functions run only once in Solid.
  - In Solid, if we want to conditionally display JSX in a component, we need that condition to reside within the returned JSX.

- Solid's JSX compiler doesn't just compile JSX to JavaScript; 
  - it also extracts reactive values and makes things more efficient along the way.
  - This is more involved than React's JSX compiler, but much less involved than something like Svelte's compiler. 
  - Solid's compiler doesn't touch your JavaScript, only your JSX.

- destructuring props is usually a bad idea in Solid. 
  - Under the hood, Solid uses proxies to hook into `props` objects to know when a prop is accessed.
  - When we destructure our `props` object in the function signature, we immediately access the object's properties and lose reactivity.

- createMemo
  - 当一个signal被多次取值时，memo后只执行一次，不memo则每次取值都执行
  - Memos are both an observer, like an effect, and a read-only signal. 
  - Since they are aware of both their dependencies and their observers, they can ensure that they run only once for any change. 
  - This **makes them preferable to registering effects that write to signals**. 
  - Generally, what can be derived, should be derived.

- stores: proxy objects that allow a tree of signals to be independently tracked and modified.
- When nested objects are accessed, stores will produce nested store objects, and this applies all the way down the tree. 
  - However, this only applies to arrays and plain objects. 
  - Classes are not wrapped, so objects like Date, HTMLElement, RegExp, Map, Set won't be granularly reactive as properties on a store.
- Objects are always shallowly merged. Set values to `undefined` to delete them from the Store.

- Context provides a form of dependency injection in Solid. It is used to save from needing to pass data as props through intermediate components.
  - The value passed to provider is passed to useContext as is. That means wrapping as a reactive expression will not work. 
  - You should pass in Signals and Stores directly instead of accessing them in the JSX.
# more
