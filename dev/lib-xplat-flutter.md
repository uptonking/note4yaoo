---
title: lib-xplat-flutter
tags: [cross-platform, flutter, lib]
created: '2021-04-21T16:07:56.389Z'
modified: '2021-05-13T03:10:56.112Z'
---

# lib-xplat-flutter

# guide

- 保守方案：native + webview

- Skia支持硬件加速，Android应用的绘图引擎是Skia，Chrome的2D页面绘图引擎也是 skia。

## react-native

- 跨平台
- 系统架构有缺陷

## flutter

- 跨平台
- 基于非主流的dart语言

- Flutter本身就是因为谷歌不满于webview的性能和html css js的一系列遗留问题，而去重新实现了渲染和ui书写。
  - 我觉得长期而言前端还是会往Flutter这上面走的。
  - 利用flutter render去重新实现web来接着写js总觉得有点削足适履了。

## jetpack compose

- 支持android原生，后续支持win/linux/macOS
  - 基于kotlin，能直接调用丰富的java库
  - swiftui不开源，且对ios版本要求高

- android: When using images for API 27 or later, the emulator can render the Android UI with Skia, which can render more smoothly and efficiently.

- [Compose for Desktop](https://www.jetbrains.com/lp/compose/) targets the JVM, and supports high-performance, hardware-accelerated UI rendering on all major desktop platforms (macOS, Windows, and Linux/x64) by leveraging the powerful native Skia graphics library.

- [Any possibility of releasing Jetpack Compose for Kotlin multiplatform mobile support (Android and iOS) ?](https://www.reddit.com/r/Kotlin/comments/jox14m/any_possibility_of_releasing_jetpack_compose_for/)
- I've started a project like that for iOS. 
  - https://github.com/cl3m/multiplatform-compose
- I don't think we need another Flutter. 
  - Dart sucks and Flutter is very opinionated. Compose is not, it's strictly UI only
- Actually there is POC port of compose on js and they're looking for developers to make it production ready solution. So why not ios/multiplatform later?

## [skia](https://skia.org/)

- Skia is an open source 2D graphics library which provides common APIs that work across a variety of hardware and software platforms. 
- It serves as the graphics engine for Google Chrome and Chrome OS, Android, Flutter, Mozilla Firefox and Firefox OS, and many other products.

- Skia is used by both Flutter and Fuchsia.
  - the versions of Skia being used by Flutter and Fuchsia must be “source compatible” 
# discuss-stars

- ## Flutter 与 React Native 深入对比分析__201912
- 曾有人问我：“他即写 Java 又会 Object-C ，在 Android 和 IOS 平台上可以同时开发，为什么还要学跨平台呢？”
  - 而我的回答是：跨平台的市场优势不在于性能或学习成本，甚至平台适配会更耗费时间，但是它最终能让代码逻辑（特别是业务逻辑），无缝的复用在各个平台上，降低了重复代码的维护成本，保证了各平台间的统一性， 如果这时候还能保证一定的性能，那就更完美了。
- 实现原理
  - 在 Android 和 IOS 上，默认情况下 Flutter 和 React Native 都需要一个原生平台的 Activity / ViewController 支持，且在原生层面属于一个“单页面应用”， 
  - 而它们之间最大的不同点其实在于UI构建渲染流程
- React Native
  - jsx > vdom > c++ bridge > android/ios
  - 默认情况下会在 Activity 下加载 JS 文件，然后运行在 JavaScriptCore 中解析 Bundle 文件布局，最终堆叠出一系列的原生控件进行渲染。
  - 简单来说就是 通过写 JS 代码配置页面布局，然后 React Native 最终会解析渲染成原生控件，如 `<View>` 标签对应 ViewGroup/UIView ，`<ScrollView>` 标签对应 ScrollView/UIScrollView ，`<Image>` 标签对应 ImageView/UIImageView 等。
  - js中的操作都会通过bridge通知native ui
- Flutter中只需平台提供一个 Surface 和一个 Canvas
  - framework(dart) widgets > engine(c++) skia
  - Flutter中绝大部分的 Widget 都与平台无关， 开发者基于 Framework 开发 App ，而 Framework 运行在 Engine 之上，由 Engine 进行适配和跨平台支持。
  - 这个跨平台的支持过程，其实就是将 Flutter UI 中的 Widget “数据化” ，然后通过 Engine 上的 Skia 直接绘制到屏幕上 。
- Flutter中写的Widget，其实并非真正的渲染控件，这一点和 React Native 中的标签类似，Widget更像配置文件， 由它组成的 Widget 树并非真正的渲染树。
  - Widget在渲染时会经过 Element 变化， 最后转化为 RenderObject 再进行绘制， 而最终组成的 RenderObject 树才是 *真正的渲染Dom*，每次 Widget 树触发的改变，并不一定会导致RenderObject 树的完全更新。
- 所以在实现原理上 React Native 和 Flutter 是完全不同的思路，虽然都有类似“虚拟 DOM 的概念” ，但是React Native 带有较强的平台关联性，而 Flutter UI 的平台关联性十分薄弱。


- 在跨平台开发中，就不得不说到接入原有平台的支持，比如 在 Android 平台上接入 x5 浏览器 、接入视频播放框架、接入 Lottie 动画框架等等。
- 这一需求 React Native 先天就支持，甚至在社区就已经提供了类似 lottie-react-native 的项目。 
  - 因为 React Native 整个渲染过程都在原生层中完成，所以接入原有平台控件并不会是难事
- 而 Flutter 在就明显趋于弱势，甚至官方在开始的时候，连 WebView 都不支持，这其实涉及到 Flutter 的实现原理问题。
  - 因为 Flutter 的整体渲染脱离了原生层面，直接和 GPU 交互，导致了原生的控件无法直接插入其中 ，
  - 而在视频播放实现上， Flutter 提供了外界纹理的设计去实现，但是这个过程需要的数据转换，很明显的限制了它的通用性，所以在后续版本中 Flutter 提供了 PlatformView 的模式来实现集成。
  - PlatformView 的设计必定导致了性能上的缺陷，最大的体现就是内存占用的上涨，同时也引导了诸如键盘无法弹出#19718和黑屏等问题，甚至于在 Android 上的性能还可能不如外界纹理。
  - 所以目前为止， Flutter 原生控件的接入上是仍不如 React Native 稳定。
- 编译和产物
  - 可以看出在 React Native 同等条件下， Android 比 IOS 大很多 ，这是因为 IOS 自带了 JSCore ，而 Android 需要各类动态 so 内置支持，而且这里 Android 的动态库 so 是经过了 ndk 过滤后的大小，不然还会更大。
  - Flutter 和 React Native 则是相反，因为 Android 自带了 skia ，所以比没有自带 skia 的 IOS 会小得多。


- 有一点需要注意，抛开场景说性能显然是不合适的，因为性能和代码质量与复杂度是有一定联系的。
- 先说理论性能，**在理论上 Flutter 的设计性能是强于 React Native** ，
  - 这是框架设计的理念导致的，Flutter 在少了 OEM Widget ，直接与 CPU/GPU 交互的特性，决定了它先天性能的优势。
- 注意不要用模拟器测试性能，特别是IOS模拟器做性能测试，因为 Flutter 在 IOS模拟器中纯 CPU ，而实际设备会是 GPU 硬件加速，同时只在 Release 下对比性能。
- 代码的实现方式不同，也可能会导致性能的损失，
  - 比如 Flutter 中 skia 在绘制时，saveLayer 是比较消耗性能的，比如 透明合成、clipRRect 等等，都会可能需要 saveLayer 的调用， 而 saveLayer 会清空GPU绘制的缓存，导致性能上的损耗，从而导致开发过程中如果掉帧严重。
- 额外补充一点，JS 和 Dart 都是单线程应用，利用了协程的概念实现异步效果，
  - 而在 Flutter 中 Dart 支持的 isolate ，却是属于完完全全的异步线程处理，可以通过 Port 快捷地进行异步交互，这大大拓展了 Flutter 在 Dart 层面的性能优势。

- React Native 在 0.59 版本开始支持 React Hook 等特性，并将原本平台的特性控件从 React Native 内部剥离到社区，这样控件的单独升级维护可以更加便捷
- Flutter UI 平台的无关能力，让 Flutter 在跨平台的拓展上更为迅速，尽管 React Native 也有 Web 和 PC 等第三方实现拓展支持，但是由于平台关联性太强，这些年发展较为缓慢， 而 Flutter 则是短短时间又宣布 Web 支持，甚至拓展到 PC 和嵌入式设备当中。
- Flutter Web 保留了 大量原本已有的移动端逻辑，只是在 Engine 层利用 Dart2Js 的能力实现了差异化， 不过现阶段而言，Flutter Web 仍处在技术预览阶段，不建议在生产环境中使用 。
- 
- 
- 

- ## It's Flutter. But in React Native.
- https://twitter.com/wcandillon/status/1433831742302003227
- How does this new effort differ from react-native-skia
  - this is a single skia canvas and you need to rebuild the world inside that canvas (like Flutter did). 
    - Our effort is to bring Skia views in regular RN. In fact some of the demos in the video feature many skia views at the same time.
  - Makes sense! **This library might then mean that RN can do some things with Skia that Flutter itself can’t** – I remember an issue that you couldn’t lay any Skia views atop of certain native views. e.g. you couldn’t show a toast over a `WKWebView`.
  - that is true! nesting native views inside skia surface is hard. flutter introduces "hybrid composition" to do this but still with some limitations
- https://github.com/react-native-skia/react-native-skia
  - Cross platform React Native solution to draw graphics based on Skia
  - The project is still in proof of concept and requires lots of work.
  - Only macOS and Linux (Ubuntu 18) is supported in the mean time, but the most implementation is cross platform.

- As far as I understand, this is different from react-native-skia:
  - react-native-skia renders the whole RN app in Skia
  - this new solution may build new declarative primitives that are not in RN core? (or allow you to build your own)
- What I don't grasp though with this project, is that the difference with react-native-skia seems small. Like in theory with this new approach my whole app could just be one "skia view" too.
- yes somehow, but does it make sense to force your whole app to be Skia from day 1? This approach is more likely to succeed as it allows incremental adoption.
  - In the same way, **React-Native-Web is more successful than React-Native-DOM**: you can mix dom + RN elements in the same webapp, and can even decide to just implement your design system in RNW, not the root web pages
- React-native-skia is aiming to help support new platforms like Linux. That would be mostly complimentary.

- Drop shadows in android. AND performant blur view… 😱😱😱 holly shit.
  - Drop Shadows are already (somewhat) possible with SVG (e.g. react-native-shadow2). Would this work without explicitly specifying width and height? Would be amazing if so
- This is really great. How does it compare with with ART tho ? Isn’t it basically the same thing?
  - The community ART module has pretty much been depracted in favour of RNSVG, which doesn't support advanced features like filters or shaders.
  - Except the deprecation part it is pretty similar isn’t it?
  - From what I understand this is more of a low-level solution for 2D graphics in general. I guess we'll see when it actually becomes public, until then I suggest watching the video if you are interested

# discuss
- ref
  - [twitter: JetPack compose flutter ](https://twitter.com/search?q=JetPack%20compose%20flutter%20min_replies%3A1&src=typed_query&f=live)

- ## 

- ## [如何评价 Flutter for Web？](https://www.zhihu.com/question/323439136/answers/updated)
- Flutter for Web和Flutter在上层都是Dart环境，两者不同的是，
  - Flutter的Dart代码运行在Dart虚拟机中，界面由Flutter引擎处理，通过Skia绘图引擎经由GPU绘制到屏幕上。
  - 而Flutter for Web的Dart代码编译成Java，界面上部分转换成标准的html标签，部分转换成通过Canvas绘制的自定义标签，最终构成一个dom树。
  - 如果Flutter for Web追求（和Flutter）完美的一致性，势必需要大量使用Canvas去绘制，而Canvas去绘制组件的性能（尤其在移动端）至少不会比html标签好。
  - 如果FFW追求性能极限而使用大量标准的html标签，这就会带来和Weex、RN等一样的一致性问题

- ## Jetpack Compose is going to use Skia for rendering the UI. High hopes for the multiplatform
- https://www.reddit.com/r/androiddev/comments/g6gjug/jetpack_compose_is_going_to_use_skia_for/
- Compose front end is decoupled from Android. 
  - Drawing to android canvas is an implementation detail just like drawing to Skia canvas is. 
  - While this desktop UI implementation (contributed by JetBrains) uses skia there can be other renderers too.
- Android has been using Skia as its 2D library since Android 1.0. Jetpack Compose therefore uses Skia already
- Flutter also uses Skia underhood. 
  - What the point to have 2 basically identical technology for one company? 
  - Oh... it's Google... so very likely one of the project will be killed sooner or later.
- Flutter's future is tied to how successful Dart and Fuchsia teams end up being.
  - It's the opposite. Dart's future is tied to how successful Flutter is. 

- ## 老板们不同意将应用最低部署版本从 iOS 10 提高到 iOS 11，这意味着如果我们想在公司项目中使用SwiftUI 可能还需要等到6、7年以后。
- https://twitter.com/ainopara/status/1382614339106918405
  - Flutter 在中国这么火，可能也有这层原因吧。

- ## [如何评价 SwiftUI？](https://www.zhihu.com/question/327763737/answers/updated)
  - SwiftUI简单来说是一个未完成的无生态的闭源UI框架。。。

- ## [Kotlin、Java和Flutter在安卓项目中的使用情况?](https://www.zhihu.com/question/377409430/answers/updated)
- 对于Android而言， Java至今还是只支持 Java8 而已
  - 安卓上的java本身是阉割版的java，java11之后的特性，基本上安卓上的java没有继续跟进了
  - 而是转向kotlin，以补充低版本java特性的不足
- flutter的owner是谷歌自己，跟kotlin，java的owner不是谷歌自己就不一样
- 当你学会 Java 之后，学习 Kotlin 语言大概就是一周的上手时间，Kotlin 通过大量的语法糖可以加快你的开发速度
- 自己考虑下未来研发的方向，转行Java的工作机会更多

- ## [flutter凉了吗?](https://www.zhihu.com/question/374113031/answers/updated)
- Flutter2.0出来了，Ubuntu选flutter为应用的默认选择
  - Flutter将成为Canonical创建的未来移动和桌面应用程序的默认选择。

- ## [Jetpack Compose or Flutter... which is the safest bet?](https://www.reddit.com/r/androiddev/comments/judj8o/jetpack_compose_or_flutter_which_is_the_safest_bet/)
- Flutter pros:
  - Easy to learn
  - Used by Google themselves in Google Pay, Google Assistant, Google Ads, etc.
  - Used by Ebay, Alibaba, Baidu, Square, Tencent
  - Used by popular apps like Insight Timer
  - Will work on Fuchsia OS

- Flutter cons:
  - Devs seem to prefer Kotlin over Dart
  - If Google drops Flutter, your investment in learning Dart will be for nothing
  - iOS animation bugs
  - Not many first party plug-ins, and some of the few that exist have issues

- Jetpack Compose pros:
  - Similar to SwiftUI, so easier to get into for new iOS devs and current Android devs
  - Built by Google and Jetbrains, who have a track record of excellent products
  - devs who prefer native android won't have much of a problem with this

- Compose cons:
  - Younger project, currently in Alpha, so who knows if it'll catch up to Flutter by the time it's mature
  - If Flutter continues to grow, it'll be harder to convince Flutter devs to switch
  - With so many companies (including Google) already invested in Flutter, what reason do they have to even consider Compose?
  - If Fuchsia turns out to be a success and not a toy project, Flutter will be ahead in this new OS. Doesn't mean Android will just disappear though

- ## Kotlin multiplatform： A new ReactNative/Flutter/cross-platform contender is here
- https://twitter.com/sebastienlorber/status/1300700261359521794
  - Kotlin multiplatform allows to share logic (business or other) between Android and iOS and access native Apis. 
  - No shared UI yet, but that could come later (Jetpack Compose cross platform?)
  - For Swift cross-platform there's also http://scade.io
- Mobile webview tech is still there, and there's a new Cordova alternative pushed by Ionic team
  - https://capacitorjs.com/
  - Capacitor is an open source native runtime for building Web Native apps. 
  - Create cross-platform iOS, Android, and Progressive Web Apps with JavaScript, HTML, and CSS.
  - 既然是基于webview，那对native框架的依赖就会降低

- ## Is Jetpack Compose hot reload possible like Flutter?
- https://twitter.com/MehmetPekerrr/status/1375231185127944204
  - I know Jetpack Compose uses the Skia engine to draw on the screen. But jetpack compose preview is not fast as needed. Is it possible technically?
- Hot reload is technically possible, but is currently constrained primarily by build times, and Gradle is especially slow.  
  - Improving hot reload would require improving build times or using an interpreter to bypass builds altogether - possible but requires more engineering.
  - Hot reload in flutter is powered directly by Dart’s ability to directly inject updated source code into the Dart VM when the app is already running.
  - The JVM has the ability to inject new class/method/field definitions. This is how debuggers work in Java.

- ## Flutter Developers working with Jetpack Compose
- https://twitter.com/Fbillionare/status/1375113097388638212
- The similarities aren't super surprising, as we had ongoing discussions with the Flutter team when designing Jetpack Compose. Thankful for all their help and friendship!
