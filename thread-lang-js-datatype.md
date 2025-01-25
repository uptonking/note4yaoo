---
title: thread-lang-js-datatype
tags: [data-type, lang-js]
created: 2024-03-16T14:11:24.927Z
modified: 2024-03-16T14:11:57.461Z
---

# thread-lang-js-datatype

# guide

- [细说 JavaScript 七种数据类型 - 一像素 - 博客园](https://www.cnblogs.com/onepixel/p/5140944.html)
# discuss-stars
- ## 

- ## 

- ## apparently JavaScript coerces numeric property types... cursed behavior
- https://x.com/aidenybai/status/1878474267295142281

```JS
const obj = {
  0.12e3: 'i hate js'
}

obj[0.12e3] // 'i hate js'
obj['.12e3'] // undefined
obj['120'] // 'i hate js'
```

- TS warns about this!
- You can use Map
- Use a map not an object, but even then using a float for key is bad in any language and any platform due to floating point error.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## This is a way better default than using `Number.parseInt` directly.
- https://twitter.com/cpojer/status/1768807456782876808 
-  I’m using `Number.isFinite` though.
- What‘s the advantage over checking for a finite number or !isNaN?
  - For me it’s forgetting to check for NaN because it’s typed as number. Returning null forces me to deal with it at every call site.
