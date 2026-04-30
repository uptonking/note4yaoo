---
title: lib-xplat-react-native-community
tags: [community, cross-platform, react-native]
created: 2021-09-10T14:15:11.809Z
modified: 2021-09-10T14:15:55.903Z
---

# lib-xplat-react-native-community

# guide

# discuss-stars
- ## 

- ## 

- ## Fun historical fact: JSI was literally designed by the Hermes team so we could replace JSC with Hermes in Facebook apps without breaking source compatibility (and could go back in case Hermes didn't deliver; fortunately it did).
- https://twitter.com/tmikov/status/1760552911812399448

# discuss-lynx
- ## 

- ## 

- ## 

- ## TikTok released ReactLynx, an open-source alternative to React Native or Flutter
- https://x.com/ammarahm_ed/status/1898457534585081944
- It does have a bridge btw and similar multi threaded design like RN however it seems to have integrated reanimated like worklets at core level I think to improve rendering performance

- Yet, no navigation solutions, native module examples are only obj-c, no clue if Swift is supported. CSS support is impressive
  - It seems to be using JSI under the hood (same basis as RN), so it may need object C bindings to call swift, but on principle, it should be possible.
# discuss-internals
- ## 

- ## 

- ## 

- ## 

- ## 

- ## The standard fetch in React Native is a JavaScript polyfill. 
- https://x.com/ReactNativeRwd/status/2049399819127451974
  - Every response gets parsed, decoded, and wrapped in JS before you touch it.
  - react-native-nitro-fetch, developed by the team at Margelo, just hit its 1.0.0 milestone, a drop-in replacement for the standard Fetch API, built on the Nitro Modules core.
  - React Native's built-in fetch is a spec-compliant JavaScript implementation sitting on top of the platform's native networking stack. That means every response goes through JS-side decoding, Response/Blob wrapping, and text parsing before your code sees a single byte. For small JSON payloads, it's fine, but for large responses, streaming, or anything latency-sensitive, that JS work adds up.
  - react-native-nitro-fetch moves that pipeline into C++. By leveraging Nitro's JSI-based architecture, response handling happens natively and hands off to your JavaScript with zero serialisation in between. 
  - 𝗗𝗿𝗼𝗽-𝗶𝗻 𝗥𝗲𝗽𝗹𝗮𝗰𝗲𝗺𝗲𝗻𝘁: It follows the standard Fetch API 
  - 𝗦𝘁𝗿𝗲𝗮𝗺𝗶𝗻𝗴 𝗦𝘂𝗽𝗽𝗼𝗿𝘁: It supports efficient body streaming, which is a game-changer for handling large datasets or real-time AI responses without spiking memory usage.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Five years ago, we @Shopify decided to go all-in on @reactnative . Today(202501), we're sharing how it went.
- https://x.com/mustafa01ali/status/1879177126848680395
  - Building features just once has been a huge productivity boost
  - Native devs and code are crucial for success
  - RN apps are fast!
  - [Five years of React Native at Shopify (2025) - Shopify _202501](https://shopify.engineering/five-years-of-react-native-at-shopify?q=v)

- After the infamous Airbnb article, we @Dream11Engg were skeptical but as more and more people invested in React Native we finally took the big bet and haven’t looked back since.

- With the emergence of Hotwire Native, if you were to start over today would you still go all-in on React Native?

- ## Let's run React Native on the UI thread and see what blows up first
- https://twitter.com/LinguaBrowse/status/1758141910605283492
- I always wanted to try this. With worklets (and careful developers) a synchronous UI architecture could lead to much more performant apps
  - This could become even more relevant with Static Hermes, as JS speed and native interop wouldn't really be a huge bottleneck anymore.

- Seems a shame to go full synchronous when there is a massively capable concurrent UI model in React 18

- BTW, we are also working on a model for sharing objects directly between JS threads. That can enable true multi-threading, but safer, since objects will not be shareable by default. I hope to be able to post more about this when we have more.

- Case-in-point: In NativeScript's official imperative UI library, you can make a virtual list exactly like on native. But with React/Vue/Angular/etc., you have to render into a dummy root and find a way to force all the contents to lay out before the dequeue callback finishes.

- ## Linear Mobile v0.1. A fast, native experience for your cellular device.
- https://twitter.com/artman/status/1757667916474958011
  - We want to create the best in class application for the devices that we support. Even if it means having to write separate clients for iOS and Android.
  - Additionally, we quickly realized that we don't want to replicate the entire web experience on mobile, but focus on the most important use-cases that you need on-the-go, and create a beautiful experience around those.

- Is the collaborative text editor present in the mobile apps ? 
  - We use the same editor, but currently its not collaborative. Shouldn't be hard to make it though.

- ## Why does #ReactNative rely so heavily on #Yoga? 
- https://twitter.com/tomekzaw_/status/1725886444344844673
  - Yes, it’s faster than iOS layout engines in some benchmarks. 
  - But sometimes we need to calculate layout in 60 fps (e.g. resize window). 
  - Wouldn’t it be easier to just map CSS styles to platform-specific layouts like React does on web?
- Yoga is one layout engine for ios and android, plus it's super fast in certain benchmarks.

- It could work well to bypass Yoga for individual nodes but as soon as they have children or there are other nodes in the tree that would need to react to those changing – we end up again needing a layout engine to do its job.
  - We still need to bypass it for Switch, Modal or Screen components which should have size dictated by the platform. On Fabric, we assume the initial size is (0, 0), then we mount the tree and finally we check the actual size. This causes layout jumps and looks bad.

- By using one cross-platform layout engine, you don’t have to implement layout once for each platform, and can be sure of consistency. Also it’s hard enough to implement flexbox from the ground up, let alone having to translate it to AutoLayout

- ## 在 apple store 发布了一个使用 react-native + nodejs 开发的项目，审核一次通过。_202309
- https://twitter.com/hamsterbase/status/1705027776624124315
  - 使用了 hamsterbase docker 版的源码，直接在 iPad 里启动了一个 nodejs 服务器。 
  - 服务器启动后，再通过 webview 访问本地服务器。

- ## 在 iOS 中，React Native 还是非常受欢迎的开发工具，App Store 中 前 100 个饮食类应用中：
- https://twitter.com/vikingmute/status/1705036795594055829
  * 30个是 React Native 写的
  * 9 个是 Cordova 写的
  * 1 个是 Flutter 写的
  * 其余的应该是原生
- 对RN和Flutter都比较熟悉，这个结果的一个可能原因是RN出来更早，技术选型一旦确定就很少/难会切换到其它竞品，迁移成本太高。
- uniapp，已上架苹果，安卓，小程序和 H5 版
- 建议体验下Expo（http://docs.expo.dev ）和Flutter的例子，都各有优劣。
  - 如果是小项目我建议flutter，各端的一致性非常好，RN有时候需要android ios微调。
  - 大项目还是RN，flutter我个人觉得可读性很差

- 关键因素是生态，RN的生态比Flutter好多了，不用各种重复造轮子。
  - js功不可没

- ## Give me your best one-line explanation of why React Native's new renderer "Fabric" is better than the old one "Paper".
- https://twitter.com/jamonholmgren/status/1595530569580179457
- It enables sync rendering, interruptions, and concurrent features
  - Sync rendering: the legacy async architecture didn't play well with UIKit/Android View because they expect things like layout, measurement, and events to be sync. This is the main reason why React Native surfaces "jump" when they load; the UI layer expects it to be sync.
  - Interruptions: the old architecture wasn’t immutable and so it couldn’t handle renders being interrupted. That means if you started rendering a tree and suspended, we wouldn’t be able to handle it. Fabric can!
  - Concurrent features: because the old architecture want immutable or sync, it wasn’t able to render multiple trees for things like transitions, or render components in parallel across multiple threads. Fabric (conceptually) can!
  - React Native Fabric isn’t a perf win on its own. For the initial roll out, we’re targeting neutral perf compared to paper. The benefit of Fabric and the rest of the New Architecture is what that architecture unlocks in the future.
  - tl; dr: the New Architecture interops better with the native platform making React Native even more Native.

- 
- 
- 
- 

- ## React Native's `fetch` could be so much faster.... 👀
- https://twitter.com/mrousavy/status/1502321672296226831
  1. RN's fetch does not support HTTP/3, QUIC, FTP or other protocols
  2. RN's fetch is just a bunch of slow JS polyfills. Mine would be fully native C++ JSI
  3. RN's fetch does not natively support Blobs with access on the JS side (ArrayBuffer streaming). I can support that.

- ## Why isn’t there a react native for Linux yet?__202009
- https://www.reddit.com/r/reactnative/comments/j855s7/why_isnt_there_a_react_native_for_linux_yet/
- Market share. There just aren't enough users on other platforms.
- Another thing to consider is that **there isn't really a single unified "Linux" graphical toolkit API** . 
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
