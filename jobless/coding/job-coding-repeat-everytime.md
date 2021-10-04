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

- 不管事件触发频率多高，一定在事件触发 n 秒后才执行
- 使用场景
  - window 的 resize、scroll
  - mousedown、mousemove
  - keyup、keydown
  - 调整浏览器窗口大小时，resize次数过于频繁，造成计算过多，此时需要一次到位，就用到了防抖
  - 登录、发短信等按钮避免用户点击太快，以致于发送了多次请求，需要防抖
  - 文本编辑器实时保存，当无任何更改操作一秒后进行保存

```js
function debounce(fn, wait) {
  let timer;

  return (...args) => {
    if (timer) clearTimeout(timer);

    timer = setTimeout(() => {

      fn.apply(this, args);
    }, wait)
  }
}

function debounce2(fn, wait, immediate) {
  let timer = null;
  //  返回一个函数
  return function(...args) {
    // 每次触发事件时都取消之前的定时器
    clearTimeout(timer);
    // 判断是否要立即执行一次
    if (immediate && !timer) {
      fn.apply(this, args);
    }
    // setTimeout中使用箭头函数，就是让 this指向 返回的该闭包函数，而不是debounce函数的调用者
    timer = setTimeout(() => {
      fn.apply(this, args)
    }, wait)
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
function throttle(fn, wait) {
  let timer;

  return (...args) => {
    if (timer) return;

    timer = setTimeout(() => {

      fn.apply(this, args);

      // 节流重在开关锁 timer=null
      timer = null;
    }, wait)

  }
}
```
