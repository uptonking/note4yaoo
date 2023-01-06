---
title: job-coding-api-rewrite
tags: [coding, job, rewrite, 手撕代码]
created: 2021-09-21T19:38:21.895Z
modified: 2021-09-21T19:45:01.472Z
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

## [setTimeout的原理和实现](https://github.com/sisterAn/JavaScript-Algorithms/issues/98)

> 思路是基于 `requestAnimationFrame` 和计算时间差实现

- 用来指定某个函数在多少毫秒之后执行。
  - 它会返回一个整数，表示定时器的编号，同时你还可以通过该编号来取消这个定时器

- setTimeout 和 setInterval 都不是 ECMAScript 规范或者任何 JavaScript 实现的一部分。 
  - 定时器功能由浏览器实现，它们的实现在不同浏览器之间会有所不同。 
  - 定时器也可以由 Node.js 运行时本身实现。

```JS
function _setTimeout(fn, delay, ...args) {
  const start = Date.now();

  let timer;
  let now;

  const loop = () => {
    timer = requestAnimationFrame(loop);

    now = Date.now();

    if (now - start >= delay) {
      fn.apply(this, args);
      cancelAnimationFrame(timer);
    }
  };

  requestAnimationFrame(loop);

  return timer;
}
```
