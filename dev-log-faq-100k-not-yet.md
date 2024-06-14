---
title: dev-log-faq-100k-not-yet
tags: [faq, not-yet]
created: 2020-01-03T10:25:55.928Z
modified: 2021-03-29T19:30:08.250Z
---

# dev-log-faq-100k-not-yet

# dev

- nextjs的 `reactStrictMode: true` 时，导致时光机动画播放速度加快一倍

- useLayoutEffect用vanillajs如何实现

- js的generator可中断函数，如果在call site执行一半就不需要了，那原函数执行上下文是否存在内存泄露

## maybe

- 如何开发时import index.ts，发布时import dist/index.js
  - 不要纠结太久，sourcemap就是解决这个问题的
# more
- 不同tab页面同步数据的方案

- 闭包和class的实例变量
  - class调试方便，闭包调试时查看不便

- http和rest的区别是什么

- reselect vs useMemo

- 对于智能开关类产品，如灯泡、风扇等，若通过app执行开关命令后，自身硬件的开关状态就会出现不一致的问题
  - 可参考类似local-first的协作设计

- 对于颜色模式HSL和HSB(HSV)，H含义与范围均相同，表示色相(0-360)，为什么有的软件HSL的H最大值只有255，如wps, inkscape

- linux上Sogou Cloud Pinyin为什么会导致fcitx占满一个CPU到100%，然后笔记本风扇狂转
