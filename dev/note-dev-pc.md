---
title: note-dev-pc
tags: [dev, pc]
created: 2019-06-09T05:28:24.696Z
modified: 2020-07-14T09:32:35.359Z
---

# note-dev-pc
- 跨平台可选技术栈
  - qt
  - java swing/javafx
  - chrominum embedded framework
  - electron
# tips
- 基于系统自带的webview实现类似electron的应用
  - 不考虑，普通第三方实现的webview功能有限，不如直接用厂商开发的chrominum
  - 考虑webview是否支持webgl、视频、音频等功能
- electron vs chrome apps
  - Google Chrome will be removing support for Chrome Apps
  - 使用electron可自己自由分发，不依赖浏览器
  - app依赖浏览器且只支持chrome浏览器，不同版本的浏览器所支持feature不一样，google还会限制部分功能
  - 使用electron能开发更灵活的功能
# features
- 跨平台一致的ui体验
- svg/canvas支持
- webgl支持
- 视频/音频播放
- 截图
- 输入法切换
- 获取焦点
- 鼠标悬停提示
- 手势操作支持
- 调用特殊硬件
# dev
- OSR渲染模式 Off Screen Rendering
  - 创建真窗口，将整个页面渲染到一张位图上面
  - 可以通过osr模式来进行视频录像
- 在swing组件中显示javafx组件： 通过 **JFXPanel** 来实现
- 在javafx组件中显示swing组件： 通过 **SwingNode** 来实现
- java跨平台渲染
  - java 2d api
  - javafx prism
  - nativefx
  - efxclipse-drift
- electron问题
  - 包太大，因为electron会自动塞入Chromium和nodejs，一个什么也不做的electron项目压缩后也大概要50mb
  - 内存消耗过大，因为Chromium本身就很吃内存，再加上提供操作系统访问能力的nodejs，很可观的内存消耗，对小工具类的项目不友好
- electron替代方案
  - [neutralinojs](https://github.com/neutralinojs/neutralinojs)
    - 前端嵌入一个webview，后端直接实现一个c++实现的http server
  - [Chromely](https://www.zhihu.com/question/396199869)
    - 前端嵌入一个CEF，后端使用.net
    - building apps based on Xilium.CefGlue, CefSharp implementations of embedded Chromium (CEF) without WinForms or WPF, but can be extended to use WinForms or WPF
  - [electrino](https://github.com/pojala/electrino)
    - 使用系统的webview，并实现一个后端（windows下似乎也是基于.net)。
    - using the system's own web browser engine
  - [tauri](https://github.com/tauri-apps/tauri)
    - Tauri is a framework for building tiny, fast binaries for all major desktop platforms.
    - Developers can integrate any front-end framework that compiles to HTML, JS and CSS for building their user interface. 
    - The backend of the application is a rust-sourced binary with an API that the front-end can interact with.
    - The user interface in Tauri apps currently leverages Cocoa/WebKit on macOS, gtk-webkit2 on Linux and MSHTML (IE10/11) or Webkit via Edge on Windows. 
  - [go-astilectron](https://github.com/asticode/go-astilectron)
    - 仍然基于Electron，但后端换成go语言
    - It is the official GO bindings of astilectron and is powered by Electron.
  - [wails](https://github.com/wailsapp/wails)
    - provides the ability to wrap both Go code and a web frontend into a single binary.
# javafx/swing/awt
- AWT/Swing are used for desktop Java apps or applets. They both require JVM to run.
- GWT is used to translate Java code to Javascript. This only runs on Javascript engines, i.e. browser.
- AWT是一个非常简单的具有有限GUI组件、布局管理器和事件的工具包
- Swing是在AWT组件基础上构建的，Swing使用了AWT的事件模型和支持类
- awt优点
  - part of java, stable
  - 组件线程安全
- awt缺点
  - 有些经常使用的组件，例如表、树、进度条等，都没有提供
- swing优点
  - part of java, stable
  - cross platform
  - The integration of Swing components within JavaFX is easier.
- swing缺点
  - 组件在不同平台上行为不一致
  - heavy components (native/awt) hide swing components
  - Swing 无法充分利用硬件 GUI 加速器和专用主机 GUI 操作的优点
  - swing组件不是线程安全的
- swt优点
  - has an integrated awt/swt bridge to allow use of awt and swing components
- swt缺点
  - requires native libraries for each supported system
  - 不同平台可能某些行为不支持
  - 使用SWT只能自顶向下地构建GUI。因此，如果没有父容器，子控件也就不存在了
  - SWT组件也不是线程安全的
  - SWT 和 JFace 并不是 Java 技术的标准配置
# javafx-tips
- JavaFX 13提供了节点使用native（eg opengl，qt，vulkan）渲染功能
- javafx以后可以跟其他任何一个渲染工具集成了，它提供一个内存块（writable image），然后你可以用任何一个你会的渲染工具，无论这个渲染的工具是opengl，vulkan还是d3d，metal或者是webgl 等等，来渲染这一个内存块，然后再将这个image交给javafx，剩下的就是javafx的日常代码了，就跟普通的image一样用
- 当然它这里还只是writable image，还要给集成到node上去，node就是javafx的最基础组件，那要集成到node上去，有两个项目提供了选择
- NativeFX /Apache2/201908
  - https://github.com/miho/NativeFX
  - 用native api来渲染node的例子，javafx 13之后，渲染效率会提升50%
- efxclipse-drift  /EPL1.0/201908
  - https://github.com/eclipse-efx/efxclipse-drift
  - 直接使用javafx的图形引擎prism的内部api，好处是更快，它的渲染直接在显存中处理，基本上没有内存和显存之间的拷贝
# Java Chromium Embedded Framework (JCEF) 
- CEF(Chromium Embedded Framework)，是基于Google Chromium项目的开源WebBrowser控件，支持Windows, Linux, Mac平台。除了提供C/C++接口外，也有其他语言的移植版。
- CEF优点
  - 可以使用最新的html5特性来制作UI，并显示在PC端
  - OSR离屏渲染
- CEF缺点
  - Chrome的缓存设计成只能有一个进程读写，可能导致同一文件被下载多次
  - osr对gpu加速、css 3d的支持有限
  - cef体积较大
- jcef works only with AWT/Swing, not javafx. (**jcef -> SwingNode -> JavaFX** no)
- but you can embed JavaFX components in Swing using JFXPane(**jcef -> SwingNode JavaFX -> SwingPanel** yes)
- With JCEF-based projects you'd have to think about supported platforms. There're different variants of natives and platform-specific problems, 
- JCEF into JavaFX
  - https://github.com/dzikoysk/Pandomium/issues/8
  - https://bitbucket.org/chromiumembedded/java-cef/issues/163/provide-javafx-node-for-jcef
  - what are the plans to support JCEF as a JavaFX node? NO.
# JavaFX Webview
- Oracle created JavaFX WebView component — its own wrapper for the open source WebKit engine. By default WebKit doesn't support web page rendering. In order to render and display HTML content Oracle had to write its own renderer using Java Graphics 2D API.
- One of the disadvantages of this approach is that some modern web pages might not be displayed correctly in WebView because the mentioned renderer does not always support the latest web standards and CSS/JavaScript/HTML frameworks. WebView in JavaFX has not been updated for years.
# JxBrowser 
- Unlike JavaFX, JxBrowser is based on Chromium engine, which is also based on WebKit, but provides its own renderer implementation. With Chromium engine JxBrowser does not have to render web pages using Java Graphics 2D API. 
- JxBrowser API provides many more features comparing to JavaFX WebView API. To name just a few of the popular:
  - Intercepting HTTP request/response headers, 
  - Handling SSL Certificates and errors, 
  - Proxy, Basic, Digest, and NTLM authentication, 
  - Geolocation, 
  - Flash and PDF Viewer support, 
  - Chromium remote debugging port support, etc.
# swing

## jIconFont

- jIconFont is a API to provide icons generated by any IconFont. 
- These icons can be used in Java GUI toolkits, such as Swing and JavaFX.
# electron
- based on Node.js and Chromium 
  - In Electron, Node.js and Chromium share a single V8 instance
  - Electron uses Chromium's rendering library rather than all of Chromium. This makes it easier to upgrade Chromium but also means some browser features found in Google Chrome do not exist in Electron.
- showcase
  - Atom Editor

## electron vs cef

- The Chromium Embedded Framework (CEF) is a project that turns Chromium into a library, and provides stable APIs based on Chromium's codebase. 
  - Very early versions of Atom editor and NW.js used CEF.
- To maintain a stable API, CEF hides all the details of Chromium and wraps Chromium's APIs with its own interface. 
- So when we needed to access underlying Chromium APIs, like integrating Node.js into web pages, the advantages of CEF became blockers.
- So in the end **both Electron and NW.js switched to using Chromium's APIs directly**.
- Even though Chromium does not officially support outside projects, the codebase is modular and it is easy to build a minimal browser based on Chromium. The core module providing the browser interface is called Content Module.
- As a user of Content Module, Electron does not need to modify Chromium's code under most cases, so an obvious way to improve the building of Electron is to build Chromium as a shared library, and then link with it in Electron. In this way developers no longer need to build all off Chromium when contributing to Electron.
- reference
  - https://electronjs.org/blog/electron-internals-building-chromium-as-a-library

## electron vs nw.js

- 参考 
  - https://zhuanlan.zhihu.com/p/34250289
- NW.js is an app runtime based on Chromium and node.js
- Electron is based on Node.js and Chromium and is used by the Atom editor
- 区别
  - 程序入口。在NW.js中，应用的主入口是网页或者js脚本；在Electron中，入口是一个js脚本
  - 构建系统。Electron通过libchromiumcontent来访问Chromium的Content API，避免了构建整个Chromium带来的复杂度
  - 与Node集成。在NW.js，网页中的Node集成需要通过给Chromium打补丁来实现，Electron通过各个平台的消息循环与libuv的循环集成，避免了直接在Chromium上做改动
  - 多上下文语境。NW.js包括Node上下文和web上下文，自从0.13以来NW.js选择性支持多上下文。通过使用Node的multi-context特性，Electron不需要在网页中引入新的js上下文

- node app on PC: Electron, NW.js
- react-desktop
  - React UI Components for macOS High Sierra and Windows 10
  - linux也可用，但linux发行版界面样式风格不统一，所以没有为linux定制专门的样式
- proton-native 
  - https://github.com/kusti8/proton-native
  - Same syntax as React Native
  - Works with existing React libraries such as Redux
  - Cross platform
  - Native components. No more Electron
  - Compatible with all normal Node.js packages
  - 基于Libui-node，Creates the native widgets using GTK3, Cocoa, or Windows API
# Chromium Embedded Framework(CEF)
- ## [使用Chromium Embed Framework做桌面程序开发前景如何？](https://www.zhihu.com/question/46946853)
- 其实就现在的带宽和存储来说，尺寸并不是太大的问题，别人的app5-10m，你的app 50m，并无影响。
- 开发效率和开发体验非常重要。
- 如果nwjs和electron可以无缝集成很多系统特有的功能，相信会有更多的人用这个来开发。
  - 毕竟css的布局能力远远快于cocoa的autolayout和windows的wpf，而且还能跨平台，开发体验配合hotreload，好的掉渣，开发效率提升n倍。
  - 唯一的缺点就是集成很多系统特有功能的时候，如果框架本身没有实现，就比较麻烦。但大多数app应该都用不到。
# kotlin
- [如何看待Kotlin 桌面 UI Jetpack Compose for Desktop？](https://www.zhihu.com/question/430328747/answers/updated)
  - JetBrains在Kotlin生态的推进上，经常东一榔头西一棒子。Kotlin for JVM, Javascript, Native 四面开花，很多开源项目做个demo或alpha版，就渐渐搁置了。
# qt

## [是什么让 Ubuntu 选用 Qt 而不是 GTK？ - 知乎](https://www.zhihu.com/question/20153991/answers/updated)

- 要开发 C++ 就选QT
  - 要开发 C就先GTK
  - 👉🏻 并不是因为它们之间不兼容，是因为 GTK是用C写的, QT是用C++写的, 开发的时候利用起来比较“顺手”不用再做语言之间的转换。

## [Chromium is developing support for using Qt on Linux_202204](https://www.reddit.com/r/linux/comments/u3m7s0/chromium_is_developing_support_for_using_qt_on/)

- For some time now, Chromium loads GTK at runtime (and you can switch between GTK3 and GTK4)
  - Now it seems, they will add support for Qt

- GTK is dead as a dev platform after they killed the community with repeated API breaking; devs can't trust GTK. At is nowadays the only sensible way forward.

- [Did you know chromium is developing a QT backend?](https://www.reddit.com/r/kde/comments/yaesom/did_you_know_chromium_is_developing_a_qt_backend/)
# kde/qt
- who is using #kde
  - kubuntu
# gnome/gtk
- who is using #gnome
  - ubuntu, debian, fedora, redhat, oracle-solaris

- ## 

- ## 

- ## 

- ## 

- ## [Linux的GTK+值得学吗？还有MFC和Qt呢？ - 知乎](https://www.zhihu.com/question/28008048/answers/updated)
- 你看看除了gnome，gtk+有什么大型应用？ 
  - gtk+的跨平台性简直就是个笑话，api也难用的要死，和qt完全没有可比性。
  - gui是非常非常需要oop思想的，gtk+强行用c语言来面向对象，在结构体里面套一大堆东西，给人的心智造成极大的负担。
- 硬要用gtk+，我也选择vala和gtk-rs，
  - 其实vala确实不错，语法类似c#，用来写图像界面很好用，可惜，以gtk社区的尿性，7，8年了连个能用的ide都没有，
  - 每天把几个api折腾来折腾去，说好的gtk+4也是一再跳票，缩放也是至今只能整数倍
- 说实话，要不是qt过去有协议问题，连gnome都不会用gtk+...

# discuss-linux-desktop
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 💡 [用 KDE 的人为什么没有用 Gnome 的人多？ - 知乎](https://www.zhihu.com/question/20238837/answers/updated)

- Gtk用的GPL协议，Qt用的协议有闭源风险。
  - 开源社区和系统厂商们不愿意将自己系统的未来置于Qt的收费风险之下，大部分默认桌面都给了Gnome，那些不会、不需要或者不愿意换桌面环境的人就会沿用Gnome。

- RHEL、SLES均采用Gnome作为默认桌面环境，同样作为受众比较广的发行版，Canonical的业务重心基本全在Server版上，采用Gnome也就不难理解了。
  - 最简单的优势就是，作为各商业发行版的默认桌面，你可以开箱即用而不会遇到大量bug

- 莫非是因为GNOME是GNU默认桌面？

- ## [2022年用gtk写gui怎么样？ - 知乎](https://www.zhihu.com/question/536281724)
- 目前使用gtk3在windows平台开发。比起qt，gtk的一些组件用起来稍微有点绕
- 个人感觉gtk3挺好用，gimp的新版本已经使用gtk3进行重写了，下载使用后，感觉还不错。
- 个人感觉，gtk3即使在windows上也挺稳定的，linux上没用过，应该问题会更少。如果对性能要求很高的话，可能要另选方案了。

- ## [2022 年了，WPF 还有前途吗？ - 知乎](https://www.zhihu.com/question/508552392/answers/updated)
- wpf没有前途，但短期不会凉。原因是wpf不支持winui3标准。
  - wpf是很早的很先进的东西，但它的ui是据于鼠标和键盘开发的。
  - 微软升级xaml标准，改标准支持触屏并且被应用到各个平台，但却没有应用到wpf，而是搞出来另外的winui3和maui框架。
  - 目前来说，因为winui3项目和maui项目不能用在win7下，wpf依然是首选，但是，未来都是win10时，谁会去新开发一个xaml不标准而且触屏支持很烂而且只能用在windows上的wpf，maui不香么，winui3也比它香啊。

- 放心winui会比wpf先死
  - 是的，最低支持win10 发布的是APPX格式的
