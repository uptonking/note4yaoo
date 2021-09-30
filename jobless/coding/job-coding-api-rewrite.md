---
title: job-coding-api-rewrite
tags: [coding, job, rewrite, 手撕代码]
created: '2021-09-21T19:38:21.895Z'
modified: '2021-09-21T19:45:01.472Z'
---

# job-coding-api-rewrite

# guide

# instanceof

```JS
function _instanceof(a, b) {
  const bPrototype = b.prototype;

  let aProto = Object.getPrototypeOf(a);

  while (aProto) {
    if (aProto === bPrototype) {
      return true;
    }

    aProto = Object.getPrototypeOf(aProto);
  }

  return false;
}
```
