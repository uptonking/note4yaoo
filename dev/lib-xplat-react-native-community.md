---
title: lib-xplat-react-native-community
tags: [community, cross-platform, react-native]
created: '2021-09-10T14:15:11.809Z'
modified: '2021-09-10T14:15:55.903Z'
---

# lib-xplat-react-native-community

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Why isn’t there a react native for Linux yet?__202009
- https://www.reddit.com/r/reactnative/comments/j855s7/why_isnt_there_a_react_native_for_linux_yet/
- Market share. There just aren't enough users on other platforms.
- Another thing to consider is that **there isn't really a single unified "Linux" graphical toolkit API**. 
  - We have GTK 3 for Gnome/elementary/XFCE apps - which one with their own UI guidelines - QT for KDE apps and lots of smaller options. 
  - Thus, React Native would have to target one or more of those specific APIs, which I don't think would be feasible.
- I think flutter's approach makes more sense in this regard, since it doesn't use native toolkits for the UI widgets and instead implements their own, thus making it easier to develop cohesive experiences across a different myriad of platforms - which would basically solve a similar problem to what electron currently does.
- I for one being a GNOME user would love to see a GTK integration for RN backed for some big company, unfortunately I don't think that will happen anytime soon.
- You could use Proton native, but it's definitely not mature enough right now. Plus there's nodegui as well, which uses QT to render UIs
- Google have their own cross platform technology called Flutter, and making RN compatible with chrome os will kill their own product. Btw you must try Flutter once its really good.

- ## [2020年跨端开发时 Flutter 和 React Native 哪个更值得选择？](https://www.zhihu.com/question/384934444/answers/updated)

- flutter招得到人？ RN直接js前端能上，dart不行
  - 如果涉及到具体业务的计算，flutter生态太差，如格式转换、文档读写

- React Native 基于 JS-Native Bridge 的渲染方案有着没有办法弥补的先天缺陷。性能上优化到 60 fps 都比较成问题，更不用提以后广泛普及的 120 fps 的设备。
  - RN 之前的桥是完全用队列异步的，JS 线程并不会阻塞 UI 线程的 vsync。
  - RN 在 18 年就提到了原有的桥架构不支持同步调用的问题，所以新架构的目的就是完全基于可同步调用的 JSI (JavaScript Interface）来重构原生模块（TurboModules）、渲染（Fabric）与包括初始化在内的残余部分，使得 RN 可以完全去掉「桥」。
- 笼统得说，新架构的做法类似大家常见的宿主环境（浏览器/Node）向 JS 引擎提供原生对象/函数的做法，
  - 是一种编译期的 FFI（foreign function interface），而不像以前的桥是一种动态的运行时机制。
  - 因此其不但支持同步调用，而且通信也不需要序列化/反序列化，可以直接在宿主对象（C++ 对象）和 JS 引擎的堆（JS 对象）之间进行互操作，这带来的性能的提升大概能有两个数量级。
  - 而且你会发现新架构中 RN 的核心部分基本都用 C++ 重写了，JSI 的两端都是 C++，Yoga 布局引擎本来就是 C++，与原生模块（JNI/OC++）的互操作部分现在是通过对 flow 做 codegen 来生成 C++。
  - 这一套零成本抽象下来，在 RN 的核心部分我觉得性能是不虚的。Dart 本身只是个带着 GC 和 RTTI 的 AOT
