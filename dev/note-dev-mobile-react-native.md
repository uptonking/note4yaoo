---
title: note-dev-mobile-react-native
tags: [mobile, react-native]
created: '2020-12-29T09:04:40.044Z'
modified: '2020-12-29T09:08:02.870Z'
---

# note-dev-mobile-react-native

# guide

# pieces

- react-native之前是滚动更新式的，定期发布。
  - 现在是做milestone式的，然后发现各种issue互相依赖，扯完皮几个月过去了... 
    - 当然现在这个项目由官方主导变成社区主导也是一个原因
  - 跨平台永远都是没有未来的啊, 除非只有一个平台… 互联网发展几十年，跨平台可不是这几年才开始的
    - 扶不起的QT
  - 各自写一遍其实也没想象的工作量大
    - 如果有图表的话，工作量就大了

# discuss

- ## [2020年跨端开发时 Flutter 和 React Native 哪个更值得选择？](https://www.zhihu.com/question/384934444/answers/updated)
- React Native 基于 JS-Native Bridge 的渲染方案有着没有办法弥补的先天缺陷。性能上优化到 60 fps 都比较成问题，更不用提以后广泛普及的 120 fps 的设备。
  - RN 之前的桥是完全用队列异步的，JS 线程并不会阻塞 UI 线程的 vsync。
  - RN 在 18 年就提到了原有的桥架构不支持同步调用的问题，所以新架构的目的就是完全基于可同步调用的 JSI (JavaScript Interface）来重构原生模块（TurboModules）、渲染（Fabric）与包括初始化在内的残余部分，使得 RN 可以完全去掉「桥」。
- 笼统得说，新架构的做法类似大家常见的宿主环境（浏览器/Node）向 JS 引擎提供原生对象/函数的做法，
  - 是一种编译期的 FFI（foreign function interface），而不像以前的桥是一种动态的运行时机制。
  - 因此其不但支持同步调用，而且通信也不需要序列化/反序列化，可以直接在宿主对象（C++ 对象）和 JS 引擎的堆（JS 对象）之间进行互操作，这带来的性能的提升大概能有两个数量级。
  - 而且你会发现新架构中 RN 的核心部分基本都用 C++ 重写了，JSI 的两端都是 C++，Yoga 布局引擎本来就是 C++，与原生模块（JNI/OC++）的互操作部分现在是通过对 flow 做 codegen 来生成 C++。
  - 这一套零成本抽象下来，在 RN 的核心部分我觉得性能是不虚的。Dart 本身只是个带着 GC 和 RTTI 的 AOT