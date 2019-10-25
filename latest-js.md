---
tags: [js, latest/js]
title: latest-js
created: '2019-10-15T12:20:05.196Z'
modified: '2019-10-15T12:30:36.843Z'
---

# latest-js


- 201907-Hermes JS Engine
    - a new js engine optimized for running React Native on Android
    - JavaScriptCore最初是为桌面浏览器端设计，相较于桌面端，移动端能力有太多的限制，为了能从底层对移动端进行性能优化，Facebook团队选择自建JavaScrip引擎，设计了Hermes，限于iOS AppStore审核限制，目前仅用于Android平台
    - 在移动应用开发中，首次加载启动、内存大小和应用大小都是衡量应用好坏的重要指标
    - Hermes现在并没有JIT编译器
    - Hermes编译的字节码文件比纯文本js文件增大100%
