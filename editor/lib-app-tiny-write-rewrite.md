---
title: lib-app-tiny-write-rewrite
tags: [app, rewrite, tiny-write]
created: 2022-08-22T16:23:21.438Z
modified: 2022-08-22T16:23:59.496Z
---

# lib-app-tiny-write-rewrite

# guide

# codebase

# solidjs-dev

- 对solidjs的依赖

```JS
import { Show, onCleanup, createEffect, createSignal, onCleanup, onError, onMount, untrack, For, Switch, Match, splitProps } from 'solid-js';
import { createContext, useContext } from 'solid-js';

import { Store, createStore, createMutable, unwrap } from 'solid-js/store';

import { render } from 'solid-js/web';
```

- Solid's JSX compiler doesn't just compile JSX to JavaScript; 
  - it also extracts reactive values and makes things more efficient along the way.
  - This is more involved than React's JSX compiler, but much less involved than something like Svelte's compiler. 
  - Solid's compiler doesn't touch your JavaScript, only your JSX.

- destructuring props is usually a bad idea in Solid. 
  - Under the hood, Solid uses proxies to hook into props objects to know when a prop is accessed.
  - When we destructure our props object in the function signature, we immediately access the object's properties and lose reactivity.
# more
