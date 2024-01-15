---
title: note-react-preact-latest-roadmap
tags: [preact, react, roadmap]
created: 2021-06-20T13:23:52.853Z
modified: 2021-06-20T13:24:35.295Z
---

# note-react-preact-latest-roadmap

# guide

# changelog

## v10.0.0-201910

- v10.5.13-202103
  - Add ESM entry for compat/server
  - Fix unable to render `bigint` numbers
  - Fix reordering issue of memoized component when the component initially render null
- v10.5.0-202009
  - New jsx-runtime functions
- v10.4.2-202005
  - HMR (=hot module reloading) prototype up without any changes to Preact
- v10.1.0-201912
  - adds support for preact-devtools extension
  - SuspenseList is a new component that can control the order in which any child suspensions are revealed

- https://github.com/preactjs/preact/releases/tag/10.0.0
- https://github.com/preactjs/preact/releases/tag/10.0.0-alpha.0
- Preact X is the next major version of Preact fully packed with features like Fragments, Hooks, componentDidCatch, Test-Utils, Debug-Warnings, many compatibility fixes 
- [Upgrading from Preact 8.x to 10](https://preactjs.com/guide/v10/upgrade-guide/)
- preact/hooks addon
- preact/test-utils addon
- compat moved to core
- Fragments
- createContext API
- componentDidCatch
- Same 3 kB size as Preact 8
- v9原本计划作为过渡，但兼容性实现得很好就直接发布v10了

## v8.0.0-201704

- Significantly increased performance, Better compatibility, Fewer edge cases
- Pure Functional Components now have backing instances
- `preact/aliases` is no longer necessary. `createElement()` is now an alias of `h()` right out of the box!
- DOM element recycling has been removed.
- No more Symbol. Instead of try to use `Symbol.for('preactattr')`,  `__preactattr_` is always used.
- Render debouncing now uses setTimeout(0) instead of Promises. It's smaller, doesn't swallow rendering errors in Safari, and was already the fallback
- `onXxxCapture` is now supported for registering capturing event handlers.
- Re-rendering a compositional child with a different `key` prop now triggers a remount
- JSX children passed to a Component are preserved rather than normalized
