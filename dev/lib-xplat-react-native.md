---
title: lib-xplat-react-native
tags: [cross-platform, lib, react-native]
created: '2020-12-29T09:04:40.044Z'
modified: '2021-05-13T03:12:23.257Z'
---

# lib-xplat-react-native

# guide

- 不用过于纠结，集中精力在数据结构+算法，就算view层被替换了，模型抽象、状态管理、协作共享都可以很容易地迁移和复用

- react-native vs electron
  - electron支持直接复用浏览器的几乎所有功能，主流浏览器由强大厂商支持，商业支持多，自己研发的投入就可以变少；而react-native可用组件少，主推大厂只有facebook
  - electron应用方便实现web端，跨平台方便；react-native的windows、macos都由微软支持，linux没有大厂支持，也没有社区支持，并且linux的应用开发比windows更加混乱
  - web的标准化更详细，更主流；原生组件与原生api与各操作系统厂商耦合度过高，难以标准化，比如gtk一套实现、qt一套实现、微软自己就有mfc/wpf/uwp/.net core
  - 仅凭性能上的小提升很难改变行业生态的方向
# faq

## react-native-windows vs electron

- [Goodbye Electron. You won't be missed!](https://www.reddit.com/r/reactnative/comments/gp1385/goodbye_electron_you_wont_be_missed/)
- can you run React native on windows/Xbox Os ? 
  - Yes you can. The same way React Native runs as an abstraction on top of iOS and Android native code, it does the same on UWP, not just desktop Windows 10. 
- Personally I love and hate electron, yes it made it possible to have a nice clean cross platform application but it's a memory hog.
- Why’d they choose RN over React? I thought RN was suited for mobile apps for the most part.
  - React standalone will use html so it needs a browser. So electron is like a chrome sandbox and it uses a lot of ressources.
  - The goal of react native is to compile and use native element. So you don't need the browser part and use less ressources.
- React Native Mobile code cannot be shifted to RN for Windows/MAc since lot of RN mobile libs dont work with RNW
# pieces
- react-native之前是滚动更新式的，定期发布。
  - 现在是做milestone式的，然后发现各种issue互相依赖，扯完皮几个月过去了... 
    - 当然现在这个项目由官方主导变成社区主导也是一个原因
  - 跨平台永远都是没有未来的啊, 除非只有一个平台… 互联网发展几十年，跨平台可不是这几年才开始的
    - 扶不起的QT
  - 各自写一遍其实也没想象的工作量大
    - 如果有图表的话，工作量就大了
# discuss-stars
- ## It's Flutter. But in React Native.
- https://twitter.com/wcandillon/status/1433831742302003227
- How does this new effort differ from react-native-skia
  - this is a single skia canvas and you need to rebuild the world inside that canvas (like Flutter did). 
    - Our effort is to bring Skia views in regular RN. In fact some of the demos in the video feature many skia views at the same time.
  - Makes sense! **This library might then mean that RN can do some things with Skia that Flutter itself can’t** – I remember an issue that you couldn’t lay any Skia views atop of certain native views. e.g. you couldn’t show a toast over a `WKWebView`.
# discuss
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
# hermes
- hermes /6.4kStar/MIT/202106/cpp
  - https://github.com/facebook/hermes
  - https://hermesengine.dev/
  - a JavaScript engine optimized for fast start-up of React Native apps. 
  - It features ahead-of-time static optimization and compact bytecode.

- ## [Why only for Android? What about iOS? ](https://github.com/facebook/hermes/issues/34)
- Apple forced to use JavaScriptCore，not V8_201908
- currently Apple don't force apps to use JSC, it only requires all executed code to be packed in app bundle. 
- V8 is now on iOS_201911

- ref
  - [JSI (JavaScript Interface) & JSC (JavaScript Core) Discussion](https://github.com/react-native-community/discussions-and-proposals/issues/91)
