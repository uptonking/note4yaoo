---
title: pattern-lib-callbag
tags: [callbag, pattern]
created: '2020-12-15T09:40:19.722Z'
modified: '2020-12-20T15:41:43.270Z'
---

# pattern-lib-callbag

# guide

# callbag-basics

- [callbag](https://github.com/callbag/callbag)
  - A standard for JS callbacks that enables lightweight observables and iterables
  - Not a library, just a standard (for real libraries, see callbag-basics)
  - [callbag utilities](https://github.com/callbag/callbag/wiki)

- Callbag is a function of signature:
  - `(type: 0 | 1 | 2, payload?: any) => void`

- Summary
  - Every producer of data is a function 
    - `(type: number, payload?: any) => void`
  - Every consumer of data is a function 
    - `(type: number, payload?: any) => void`
  - `type === 0` means "start" 
    - (a.k.a. `subscribe` on Observables)
  - `type === 1` means "data" 
    - (a.k.a. `next` on Observers)
  - `type === 2` means "end" 
    - (a.k.a. `unsubscribe` on Subscriptions)

- [callbag-basics](https://github.com/staltz/callbag-basics)
  - Basic callbag factories and operators to get started with.
  - Faster than xstream and RxJS
  - Extensible: no core library! Everything is a utility function

# callbag-pieces

- How to visual debug callbag? 
  - RxJS, xstream and others have visual debugging tools, 
  - but callbag are just a function message passing convention, so, how can we debug them?
  - 寻找第三方实现的调试工具
