---
title: lib-xplat-react-native
tags: [cross-platform, lib, react-native]
created: 2020-12-29T09:04:40.044Z
modified: 2021-05-13T03:12:23.257Z
---

# lib-xplat-react-native

# guide

- 基于webview是验证想法最快速的方案
  - react-native-webview、capacitor

- who is using #react-native
  - shopify
  - wix: nav/calendar
  - @AmazonPhotos , @AmazonKindle , and @AmazonAppDev
  - [Showcase · React Native](https://reactnative.dev/showcase)
  - abandoned
    - airbnb 

- [搞不定移动端性能，全球爆火的 Notion 从 Hybrid 转向了 Native__202207](https://www.infoq.cn/article/kiiff9kot0jttljpl93u)

- web版和移动版要不要基于react-native复用大量代码
  - web支持的标准非常丰富，移动版只是其中的子集，只使用子集没有充分利用web特性，资源利用不充分
  - css的子集和css-in-js的实现方案
  - 状态管理可复用
  - 很多html元素如details在react-native中不存在，若全部重新实现，会在web端产生div soup，也增加了很大复杂度
  - 如果强行限制使用web特性的某些子集感到很不灵活，不如分开单独开发web版和移动版，只复用基础的样式tokens和配置对象

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
# dev
- react-native之前是滚动更新式的，定期发布。
  - 现在是做milestone式的，然后发现各种issue互相依赖，扯完皮几个月过去了... 
    - 当然现在这个项目由官方主导变成社区主导也是一个原因
  - 跨平台永远都是没有未来的啊, 除非只有一个平台… 互联网发展几十年，跨平台可不是这几年才开始的
    - 扶不起的QT
  - 各自写一遍其实也没想象的工作量大
    - 如果有图表的话，工作量就大了
# NativeScript
- ## 

- ## 

- ## 

- ## [如何评价NativeScript？ - 知乎](https://www.zhihu.com/question/29468045/answers/updated)
- 虽然NativeScript越来越成熟了，也加入了对vue的支持

- ## [为啥国内很少人用NativeScript？ - 知乎](https://www.zhihu.com/question/268684469)
- 坑太多了，实在是做不下去....
  - 姑且不说组件你要想自定义非常麻烦（得写原生），有些组件是没有开源的。
  - 生态的缺失就是一个大问题。

# examples

## xplat-solutions

- https://github.com/OpenNative/open-native
  - For our first integration, we've enabled NativeScript to use React Native native modules the same way one would use them in React Native.
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
