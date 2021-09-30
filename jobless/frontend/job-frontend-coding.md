---
title: job-frontend-coding
tags: [coding, frontend, job]
created: '2021-09-24T16:33:42.242Z'
modified: '2021-09-24T16:34:14.601Z'
---

# job-frontend-coding

# guide

# 延迟打印

```JS
// ❌️ 等待2s后一次性打印5个5
for (var a = 0; a < 5; a++) {
  setTimeout(() => console.log(a), 2000);
}

// 方案一：保存参数
// 原理 setTimeout(function[, delay, arg1, arg2, ...]);
for (var a = 0; a < 5; a++) {
  setTimeout((a) => console.log(a), 1000 * a, a);
}

// 方案二：使用let，每次都是块级变量
for (let a = 0; a < 5; a++) {
  setTimeout(() => console.log(a), 1000 * a);
}
// 方案三：使用promise
for (var a = 0; a < 5; a++) {
  Promise.resolve(a).then((value) => {
    setTimeout(() => {
      console.log(value);
    }, 1000 * value);
  });
}
// 方案四：使用立即函数
// 使用IIFE函数体充当块级作用域，内部匿名函数成为IIFE闭包
for (var a = 0; a < 5; a++) {
  (function(i) {
    setTimeout(() => console.log(i), 1000 * i);
  })(a);
```

# 实现动画：淡出-平移-放大

> 一个三角形从透明到实体，持续一秒，然后匀速前进五秒，然后变大持续两秒

- 注意每一个关键帧中要声明不变的属性，假如只在 100% 中声明 scale(2)，这个放大会开始于 0%

```css
.triangle {
  width: 0px;
  /* ● forwards 表示动画结束时保持结尾帧 */
  animation: change 8s linear 1 forwards;
}

@keyframes change {
  0% {
    transform: translateX(0) scale(1);
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 85px solid transparent;
  }

  12.5% {
    transform: translateX(0) scale(1);
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 85px solid orange;
  }

  75% {
    transform: translateX(300px) scale(1);
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 85px solid orange;
  }

  100% {
    transform: translateX(300px) scale(2);
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 85px solid orange;
  }
}
```

# modal 弹窗+动画
- 遮罩的实现需要靠fixed布局，指定 left top 为 0，声明颜色时需要使用 rgba()，第四个代表透明度

```html
<style>
  .cover {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgb(128, 128, 128, 0.7);
    z-index: 0;
  }

  .popup {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    background-color: tomato;
    padding: 50px 80px;
    z-index: 1;
    animation: goAbove 0.5s;
  }

  @keyframes goAbove {
    0% {
      margin-top: 100%;
    }

    100% {
      margin-top: 0;
    }
  }
</style>
<div>被遮罩掩盖</div>
<div class="cover"></div>
<div class="popup">这是一个弹窗</div>
```

# 判断元素是否在可视区
- 方法一： el.offsetTop - document.documentElement.scrollTop <= document.documentElement.clientHeight
  - offsetTop 是元素盒子边缘距离其 offsetParent padding 的距离，scrollTop 是元素被卷起来的顶部距离当前视口顶部的距离，当 offsetParent 就是 body 时，二者差值就是元素距离当前视口顶端的距离，当这个差值大于 body 的 clientHeight（元素非滚动区域的 padding+content），说明元素还在可视区下方

```JS
function checkInView(el) {
  // viewPortHeight 兼容所有浏览器写法
  const viewPortHeight = document.documentElement.clientHeight
  const offsetTop = el.offsetTop
  const scrollTop = document.documentElement.scrollTop
  const top = offsetTop - scrollTop
  return top <= viewPortHeight
}
```

- 方法二： elem.getBoundingClientRect().top >= top 说明未进入可视区
  - 一般认为 gBCR right 和 left 的差值与 offsetWidth 的值相等（content+padding+border+scrollY)，而 bottom 和 top 的差值与 offsetHeight 相等（content+padding+border+scrollX）
  - elem.getBoundingClientRect().top < -elem.clientHeight：垂直方向，元素已离开可视区
  - elem.getBoundingClientRect().left >= body.clientwidth：水平方向，元素未抵达可视区
# 实现搜索框

```HTML
<div class="container">
  <div class="flex">
    <input id="ipt" />
    <button id="btn">search</button>
  </div>
  <ul id="result-list"></ul>
</div>
```

- 使用flex布局自适应，flex 容器和 `<ul>` 并列实现答案位置对齐
- jsonp+防抖：直接将防抖包装后的函数作为 input 回调，防抖中进行 jsonp 查询，注意
  a. 查询无结果时需要处理，否则 for-of 报错
  b. 每次需清空前一次 ul 中内容
- 对 ul 添加 focus 和 blur 监听，修改 visibility 属性，实现结果列表的自动展开收起
# 实现拖拽组件
- 要求
  1. 监听组件上 `mousedown` 事件：回调中添加对文档中 `mousemove` 事件和组件上 `mouseup` 事件的监听、
  2. 当鼠标移动：执行 `moveAt()`，设置当前元素的绝对定位偏移坐标为指针坐标
  3. 当鼠标松开：移除对于文档中 `mousemove` 事件和组件上 `mouseup` 事件的监听
# 使用一个 div 实现width为200px, height为0的的正方形？

```CSS
.div1 {
  width: 200px;
  /* padding-top会导致背景色消失 */
  padding-top: 200px;
  background-color: coral;
}

.c2 {
  /* 如果注释掉width，正方形会占满整个屏幕 */
  width: 25%;
  aspect-ratio: 1 / 1;
  background-color: coral;
}
```

```HTML
<!-- 这里只能用padding-bottom，而不能用padding-top -->
<!-- 这个正方形尺寸会随着viewport响应式缩放 -->
<div style="height:0; width:20%; padding-bottom:20%;background-color:beige">
  <div>
    Content goes here
  </div>
</div>
```

- 盒模型规定，任何元素的padding和border都是在此指定的宽度和高度内布置和绘制。
  - 内容宽度和高度是通过从指定的“宽度”和“高度”属性中减去相应边的边框和padding值来计算的。
  - 然而对于宽度和高度的值是不能为负值的，所以0 - padding-top的极限值就是0. 故高度就一直会是0

- padding-top的百分比是基于父元素的width来计算的。
