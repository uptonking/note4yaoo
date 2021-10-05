---
title: job-coding-repeat-everytime
tags: [coding, job, repeat]
created: '2021-10-04T14:16:22.069Z'
modified: '2021-10-04T14:43:10.710Z'
---

# job-coding-repeat-everytime

> 练习 [2020年中大厂前端面试总结](https://wangyaxing.cn/blog/interview/%E9%9D%A2%E7%BB%8F/2020-%E9%9D%A2%E8%AF%95.html)
> [手写代码系列](https://wangyaxing.cn/blog/jsCode/)
> 超高频：面过的公司每家都问到了

# guide

# 防抖 debounce

- 不管事件触发频率多高，一定在事件触发n秒后才执行
- 使用场景
  - window 的 resize、scroll
  - mousedown、mousemove
  - keyup、keydown
  - 调整浏览器窗口大小时，resize次数过于频繁，造成计算过多，此时需要一次到位，就用到了防抖
  - 登录、发短信等按钮避免用户点击太快，以致于发送了多次请求，需要防抖
  - 文本编辑器实时保存，当无任何更改操作一秒后进行保存

- 非立即执行
  - 多次触发事件，只会在最后一次触发事件后等待设定的wait时间结束时执行一次
- 立即执行
  - 多次触发事件，第一次会立即执行函数，之后在设定wait事件内触犯的事件无效，不会执行。
  - 立即执行是第一次触发事件就执行然后n秒内不再执行，非立即执行是最后一次触发事件才执行，每次触发事件都会取消上一次的setTimeout任务

```js
/**
 * * 非立即执行版，每次事件触发后，若存在timer就 clearTimeout，重新创建任务
 */
function debounce(fn, wait) {
  let timer;

  return function(...args) {
    const that = this;

    if (timer) clearTimeout(timer);

    timer = setTimeout(() => {

      fn.apply(that, args);
    }, wait)
  }
}

// * 立即执行版
function debounce2(fn, wait, immediate) {
  let timer = null;

  return function(...args) {
    const that = this;

    // 每次触发事件时都取消之前的定时器
    if (timer) clearTimeout(timer);

    // 第一次会立即执行函数，之后在设定wait内触发事件无效，不会执行
    if (immediate) {
      const callNow = !timer;

      // 第一次触发后timer就存在，
      timer = setTimeout(() => {
        timer = null;
      }, wait);

      // 第一次触发才执行，之后等待wait毫秒timer清空了才会再次执行
      if (callNow) fn.apply(that, args);
    } else {
      timer = setTimeout(() => {
        fn.apply(that, args)
      }, wait)
    }

  }
}
```

# 节流 throttle
- 不管事件触发频率有多高，只在单位时间内执行一次。
- 使用场景
  - resize/scroll 事件，每隔一秒计算一次位置信息等
  - 浏览器播放事件，每个一秒计算一次进度信息等
  - input框实时搜索并发送请求展示下拉列表，没隔一秒发送一次请求 (也可做防抖)

```JS
/**
 * * 每次事件触发后，若存在timer则不执行，执行事件后timer=null
 */
function throttle(fn, wait) {
  let timer;

  return function(...args) {
    const that = this;

    if (timer) return;

    timer = setTimeout(() => {

      fn.apply(that, args);

      // 节流重在开关锁 timer=null
      timer = null;
    }, wait)

  }
}

// 基于时间戳实现
function throttle(fn, wait) {
  let prevTime = 0;

  return function(...args) {
    const that = this;

    const nowTime = Date.now();
    if (nowTime - prevTime < wait) return;

    fn.apply(that, args);
    prevTime = nowTime;

  }
}

// 立即执行版; https://juejin.cn/post/6844904071028228103
function throttle(fn, wait, immediate) {
  let timer;

  return function(...args) {
    const that = this;

    if (timer) return;

    if (immediate) {
      const callNow = !timer;

      timer = setTimeout(() => {
        timer = null;
      }, wait)

      if (callNow) fn.apply(that, args)
    } else {

      timer = setTimeout(() => {

        fn.apply(that, args);

        // 节流重在开关锁 timer=null
        timer = null;
      }, wait)
    }

  }
}
```
