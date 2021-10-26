---
title: thread-web-mobile
tags: [job, mobile, thread, web]
created: '2021-09-29T06:38:20.588Z'
modified: '2021-09-29T06:38:35.002Z'
---

# thread-web-mobile

# discuss

## 

## 

## 

## 

## [JavaScript检测手机浏览器的五种方法](https://www.ruanyifeng.com/blog/2021/09/detecting-mobile-browser.html)

- navigator.userAgent
  - if (/Mobi|Android|iPhone/i.test(navigator.userAgent)) 
  - 最简单的方法就是分析浏览器的 user agent 字符串，它包含了设备信息。
  - 只要里面包含mobi、android、iphone等关键字，就可以认定是移动设备。
  - 优点是简单方便，缺点是不可靠，因为用户可以修改这个字符串，让手机浏览器伪装成桌面浏览器。
- window.screen，window.innerWidth
  - if (window.screen.width < 500) 
  - if (window.innerWidth < 768)
  - window.screen对象返回用户设备的屏幕信息，该对象的width属性是屏幕宽度（单位为像素）。
  - window.innerWidth返回浏览器窗口里面的网页可见部分的宽度，比较适合指定网页在不同宽度下的样式。
- window.orientation
  - if (typeof window.orientation !== 'undefined')
  - 第三种方法是侦测屏幕方向，手机屏幕可以随时改变方向（横屏或竖屏），桌面设备做不到。
- ontouchstart
  - 'ontouchstart' in document.documentElement
  - 手机浏览器的 DOM 元素可以通过ontouchstart属性，为touch事件指定监听函数。桌面设备没有这个属性。
- window.matchMedia()
  - window.matchMedia("only screen and (max-width: 760px)").matches
  - 最后一种方法是结合 CSS 来判断。
  - 如果某个针对手机的 media query 语句生效了，就可以认为当前设备是移动设备。
  - window.matchMedia()方法接受一个 CSS 的 media query 语句作为参数，判断这个语句是否生效。
- 工具包
  - https://github.com/duskload/react-device-detect
