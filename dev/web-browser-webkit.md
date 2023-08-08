---
title: web-browser-webkit
tags: [web, webkit, webview]
created: 2019-10-17T09:05:43.329Z
modified: 2021-01-01T20:11:00.889Z
---

# web-browser-webkit

# guide

- tips
  - 不建议基于electron实现自定义浏览器，要考虑支持各浏览器自带的扩展商店

- resources
  - [History of Web Browser Engines from 1990 until today](https://eylenburg.github.io/browser_engines.htm#)
  - [WebKit | User Agents](https://user-agents.net/rendering-engines/webkit)
  - [WebKit for Developers_201302](https://www.paulirish.com/2013/webkit-for-developers/)
  - [Applications using WebKit/GTK+](https://trac.webkit.org/wiki/ApplicationsGtk)
  - [List of web browsers - Wikipedia](https://en.wikipedia.org/wiki/List_of_web_browsers#WebKit-based)
    - 开源浏览器很难生存和持续
    - android: dolphin
    - linux: epiphany(flathub/snap), otter,midori(webkit2blink),konqueror(khtml/webkit)
    - win: otter,midori, Playwright with WebKit mini browser,split,ultralight,Maxthon(webkit2blink), run Linux's Surf browser on WSL2.
    - 以键盘操作为主: qutebrowser, vimb
    - 基于QtWebEngine/blink: Falkon,Dooble,qutebrowser
    - 基于Webkit: otter-old, midori-old
      - On qt5-webkit : otter-browser, qutebrowser
      - On webkit2-gtk3 : epiphany,midori,surf-browser,badwolf
  - geco: firefox, icecat
  - [Google and Mozilla are working on iOS browsers that aren't based on WebKit | Hacker News_202302](https://news.ycombinator.com/item?id=34690788)

- **all Chrome variants except iOS now use Blink**
  - The restriction to use WebKit as the rendering engine for 3rd party Web browser apps exists solely on iOS. 
# read: WebKit技术内幕_2014
- 浏览器的功能越来越丰富，包括网页浏览、网络请求、资源管理、多页面管理、插件和扩展、书签管理、历史记录管理、设置、下载、账户同步、安全隐私、外观主题、开发者工具等
- html5的标准包含10个大的类别
  - offline、storage、connectivity、file access、semantics、audio/video、3d/graphics、presentation、performance、nuts and bolts(其他)
- 浏览器的内核，也被称为渲染引擎
  - 浏览器的渲染引擎就是能够将HTML/CSS/JavaScript文本及其相应的资源文件转换成图像结果的模块
  - 主流的渲染引擎包括 Trident、 Gecko 和 WebKit
- 渲染引擎模块
  - html解释器
  - css解释器
  - layout布局信息计算
  - js引擎更新渲染结果
  - paint
- 渲染引擎还包括如何使用依赖模块的部分，如网络、存储、2d/3d等
- 渲染引擎的渲染过程
  - 构建DOM树
  - CSSOM
  - 内部表示
  - layout + paint
  - rerender重复渲染过程来更新
- 苹果fork了KHTML源码，成立了新项目WebKit，2005年开源
  - 狭义的webkit指的是在WebCore(包含html解释器、css解释器、layout模块)和js引擎之上的一层绑定和嵌入式编程接口，可以被各种浏览器调用
  - WebCore 部分包含了目前被各个浏览器所使用的 WebKit 共享部分
- webkit2不是webkit的简单修改版，苹果抽象出了一组新的编程接口
  - 该接口和调用者代码与网页的渲染工作不在统一进程
- googlefork了webkit，独立运作blink项目
- JavaScriptCore 引擎是 WebKit 中的默认 JavaScript 引擎
  - WebKit 中对 JavaScript 引擎的调用是独立于引擎的
  - Chromium 开源项目中，它被替换为 V8 引擎
- WebKit Ports 指的是 WebKit 中的非共享部分
  - 包括硬件加速架构、网络栈、 视频解码、图片解码等
- 在 WebKit 内核之上，Chromium 率先在 WebKit 之外引入了多进程模型。
  - 避免因单个页面的不响应或者崩溃而影响整个浏览器的稳定性
  - 第三方插件崩溃时不会影响页面或者浏览器的稳定性，因为第三方插件也被使 用单独的进程來运行
  - 方便了安全模型的实施，也就是说沙箱模型是基于多进程架构的
- Chromium的多进程模型
  - Browser进程和页面的渲染是分开的，这保证了页面的渲染导致的崩溃不会导致浏览器主界面的崩溃
  - 每个网页的渲染进程是独立的进程，这保证了页面之间相互不影响
    - Renderer进程的数量是否同用户打开的网页数量一致呢？
    - 答案是不一定。Chromium 设计了灵活的机制，允许用户配置
  - 插件进程也是独立的，插件本身的问题不会影响浏览器主界面和网页
  - GPU 硬件加速进程也是独立的
- Browser进程和Renderer进程都是在WebKit的接口之外由Chromium引入
  - Renderer, 它主要处理进程间通信，接受来自 Browser 进程的请求， 并调用相应的 WebKit 接口层。同时，将 WebKit 的处理结果发送回去
- Web Contents 表示的就是网页的内容
- 每个进程内部，都有很多的线程
  - 多线程的主要目的就是为了保持用户界面的高响应度，保证 UI 线程（Browser 进程中的主线程）不会被任何其他费时的操作阻碍从而影响了对用户操作的响应。
  - 为了利用多核的优势，Chromium将渲染过程管线化，这样可以让渲染的不同阶段在不同的线程执行
- WebKit2 是一套全新的结构和接口
  - 它的主要目的和思想同 Chromium 类似，就是将渲染过程放在单独的进程中来完成，独立于用户界面
  - WebKit提供嵌入式接口，该接口表示其他程序可以将网页渲染嵌入在程序中作为其中的一部分，或者用户界面的一部分
  - WebKit2 接口不同于 WebKit 的接口，它们是不兼容的，但目的却是差不多 的，都是提供嵌入式的应用接口。
- Chromium 使用的仍然是 WebKit 接口，而不是 WebKit2 接口，也就是说 Chromium 是在 WebKit 接口之上构建的多进程架构
- Chromium 中每个进程都是从相同的二进制可执行文件启动，而基于WebKit2 的进程则未必如此
# 浏览器的渲染过程
- 浏览器将HTML，CSS，JavaScript代码转换成屏幕上所能呈现的实际像素，这期间所经历的一系列步骤，叫做关键渲染路径（Critical Rendering Path）
1. DOM Tree的构建
  - 从网络或者磁盘下读取的HTML原始字节码，通过设置的charset编码，转换成相字符
  - 通过词法分析器，将字符串解析成Token，Token中会标注出当前的Token是开始标签，还是结束标签，或者文本标签等。
  - 浏览器会根据Tokens里记录的开始标签，结束标签，将Tokens之间相互串联起来（带有结束标签的Token不会生成Node）
  - Node包含了这个节点的所有属性
  - 事实上，在构建DOM树时，不是要等所有的Tokens都转换成Nodes后才开始，而是一边生成Token一边采取深度遍历算法消耗Token来生成Node
  - 从bytes到Tokens的这个过程，浏览器都可以交给其他单独的线程去处理，不会堵塞浏览器的渲染线程。但是后面的部分就都在渲染线程下进行了，也就是我们常说的js单线程环境
2. CSSOM Tree的构建
  - CSSOM的生成过程和DOM十分相似，也是：1. 解析，2. Token化，3. 生成Nodes并构建Tree
3. Render Tree的构建
  - Render Tree上的每一个节点被称为：RenderObject。
  - RenderObject跟DOM节点几乎是一一对应的，当一个可见的DOM节点被添加到DOM树上时，内核就会为它生成对应的RenderObject添加到Render Tree上。
  - 其中，可见的DOM节点不包括：
    - 一些不会体现在渲染输出中的节点（如 `<html><script><link>…` ），会直接被忽略掉。
    - 通过CSS隐藏的节点。例如上图中的span节点，因为有一个CSS显式规则在该节点上设置了 `display:none` 属性，那么它在生成RenderObject时会被直接忽略掉。
  - Render Tree是衔接浏览器排版引擎和渲染引擎之间的桥梁，它是排版引擎的输出，渲染引擎的输入
  - 浏览器渲染引擎并不是直接使用Render树进行绘制，为了方便处理Positioning, Clipping, Overflow-scroll, CSS Transfrom/Opacity/Animation/Filter, Mask or Reflection, Z-indexing等属性，浏览器需要生成另外一棵树：RenderLayer
  - 浏览器会为一些特定的RenderObject生成对应的RenderLayer，其中的规则是：
    - 是否是页面的根节点 It’s the root object for the page
    - 是否有css的一些布局属性（relative absolute or a transform) It has explicit CSS position properties (relative, absolute or a transform)
    - 是否透明 It is transparent
    - 是否有溢出 Has overflow, an alpha mask or reflection
    - 是否有css滤镜 Has a CSS filter
    - 是否包含一个canvas元素使得节点拥有视图上下文 Corresponds to canvas element that has a 3D (WebGL) context or an accelerated 2D context
    - 是否包含一个video元素 Corresponds to a video element
  - 当满足上面其中一个条件时，这个RenderObject就会被浏览器选中生成对应的RenderLayer。
  - 至于那些没有被命运选中的RenderObject，会从属与父节点的RenderLayer。
  - 最终，每个RenderObject都会直接或者间接的属于一个RenderLayer。
  - 浏览器渲染引擎在布局和渲染时会遍历整个Layer树，访问每一个RenderLayer，再遍历从属于这个RenderLayer的 RenderObject，将每一个RenderObject绘制出来。
  - 可以理解为：RenderLayer树决定了网页绘制的层次顺序，而从属于RenderLayer的 RenderObject决定了这个Layer的内容，所有的RenderLayer和RenderObject一起就决定了网页在屏幕上最终呈现出来的内容。
4. Layout
  - 布局最后的输出是一个“盒模型”：将所有相对测量值都转换成屏幕上的绝对像素
5. Paint
  - 将渲染树中的每个节点转换成屏幕上的实际像素
  - 浏览器通过发出“Paint Setup”和“Paint”事件，将渲染树转换成屏幕上的像素
- 浏览器内部实现了Render Object
  - 每个Render Object和DOM节点一一对应。
  - Render Object上实现了将其对应的DOM节点绘制进位图的方法，负责绘制这个DOM节点的可见内容如背景、边框、文字内容等等。
  - 同时Render Object也是存放在一个树形结构中的。
- 如果有层叠、半透明等等情况的元素（具体哪些情况请参考无线性能优化：Composite）就会从Render Object提升为Render Layer
  - 不提升为Render Layer的Render Object从属于其父级元素中最近的那个Render Layer
  - 根元素HTML自己要提升为Render Layer
- 浏览器渲染引擎遍历Layer树，访问每一个RenderLayer，然后递归遍历negZOrderList里的layer、自己的RenderObject、再递归遍历posZOrderList里的layer。就可以将一颗 Layer树绘制出来。
- Layer树决定了网页绘制的层次顺序，而从属于 RenderLayer 的 RenderObject 决定了这个 Layer 的内容，所有的 RenderLayer 和 RenderObject 一起就决定了网页在屏幕上最终呈现出来的内容。
- 上面的过程可以搞定绘制过程。但是浏览器里面经常有动画、video、canvas、3d的css等东西。这意味着页面在有这些元素时，页面显示会经常变动，也就意味着位图会经常变动。
- 每秒60帧的动效里，每次变动都重绘整个位图是很恐怖的性能开销。
- 因此浏览器为了优化这一过程，引出了Graphics Layers和Graphics Context，前者就是我们常说的合成层(Compositing Layer)
- 每个合成层Graphics Layer 都拥有一个 Graphics Context，Graphics Context会为该Layer开辟一段位图，也就意味着每个Graphics Layer都拥有一个位图。
- Graphics Layer负责将自己的Render Layer及其子代所包含的Render Object绘制到位图里。然后将位图作为纹理交给GPU。所以现在GPU收到了HTML元素的Graphics Layer的纹理，也可能还收到某些因为有3d transform之类属性而提升为Graphics Layer的元素的纹理。
- 现在GPU需要对多层纹理进行合成(composite)，同时GPU在纹理合成时对于每一层纹理都可以指定不同的合成参数，从而实现对纹理进行transform、mask、opacity等等操作之后再合成，而且GPU对于这个过程是底层硬件加速的，性能很好。最终，纹理合成为一幅内容最终draw到屏幕上。
- 所以在元素存在transform、opacity等属性的css animation或者css transition时，动画处理会很高效，这些属性在动画中不需要重绘，只需要重新合成即可。
# 浏览器的渲染过程 - Composite
- DOM Tree：浏览器将HTML解析成树形的数据结构。
- Style Rules：浏览器将CSS解析成树形的数据结构，对应我们的CSSOM。
- Render Tree：DOM和CSSOM合并后生成Render Tree。
- Layout： 布局。有了Render Tree，浏览器已经能知道网页中有哪些节点、各个节点的CSS定义以及他们的从属关系，从而去计算出每个节点在屏幕中的位置。
- Paint： 渲染。按照算出来的规则，通过显卡，把内容画到屏幕上。
- Reflow（回流/重排）：当浏览器发现某个部分发生了点变化影响了布局，需要倒回去重新渲染，这个回退的过程叫reflow。
- Dirty位系统
  - 为了避免所有细小的更改都要从根节点进行整体布局，浏览器采用了一种“dirty 位”系统。
  - 如果某个RenderTree上的Node发生了更改，便将自身标注为“dirty”，表示需要进行布局
  - 有两种标记：“dirty”和“children are dirty”。“children are dirty”表示尽管呈现器自身没有变化，但它至少有一个子代需要布局reflow时，浏览器会对Render Tree进行遍历，而仅仅只对标注了“dirty “的Node进行布局。
- repaint（重绘）：改变某个元素的背景色、文字颜色、边框颜色等等不影响它周围或内部布局的属性时，屏幕的一部分要重画，但是元素的几何尺寸没有变
- Chrome拥有两套不同的渲染路径：硬件加速路径和旧软件路径。
- 硬件加速路径会将一些图层的合成交给GPU处理，比CPU处理更快，而我们的RenderLayer（有些地方又称作PaintLayers）并不能作为GPU的输入，这里会将RenderLayer转换成GraphicsLayers
- 与RenderObject转换成RenderLayer一样，浏览器也是根据“某些规则”，选中一些特殊的RenderLayout节点（天选之子），这些节点将被称为Compositing Layers，Compositing Layers与其他的普通节点不一样的是他们拥有自己的GraphicsLayer，而那些没有被选中的节点，会和父层公用一个GraphicsLayer。
- 每个GraphicsLayer都拥有GraphicsContext，GraphicsContext输出的位图会作为纹理上传到GPU中。
- 什么是纹理？可以把它想象成一个从主存储器(例如 RAM)移动到图像存储器(例如 GPU 中的 VRAM)的位图图像(bitmapimage)
- Chrome 使用纹理来从GPU上获得大块的页面内容。通过将纹理应用到一个非常简单的矩形网格就能很容易匹配不同的位置(position)和变形(transformation)。这也就是3DCSS的工作原理，它对于快速滚动也十分有效
- 提升到合成层后合成层的位图会交GPU处理，但请注意，仅仅只是合成的处理（把绘图上下文的位图输出进行组合）需要用到GPU，生成合成层的位图处理（绘图上下文的工作）是需要CPU。
- 当需要repaint的时候可以只repaint本身，不影响其他层，但是paint之前还有style， layout, 那就意味着即使合成层只是repaint了自己，但style和layout本身就很占用时间。
- 仅仅是transform和opacity不会引发layout和paint，那么其他的属性不确定。
# blogs

## [手把手教你实现一个浏览器引擎（一）Start [译文] - 知乎](https://zhuanlan.zhihu.com/p/106494297)

- https://github.com/mbrubeck/robinson /rust/201408
  - A toy web rendering engine
# reflow
- reflow
  - 如果引起reflow，样式首先必须重新计算，因此重排会触发两种操作
  - force reflow 
    - https://gist.github.com/paulirish/5d52fb081b3570c81e3a
- 当在js中调用（requested/called）以下所有属性或方法时，浏览器将会同步地计算样式和布局，进行重排( `reflow` 或layout thrashing)，通常是性能瓶颈
- element
  - 盒子计算
      - elem.offsetLeft/offsetTop, elem.offsetWidth/offsetHeight
      - elem.offsetParent
      - elem.clientLeft/clientTop, elem.clientWidth/clientHeight
      - elem.getClientRects(), elem.getBoundingClientRect()
  - frame/image
      - height, width
  - 滚动相关
      - elem.scrollBy(), elem.scrollTo()
      - elem.scrollIntoView(), elem.scrollIntoViewIfNeeded()
      - elem.scrollWidth/scrollHeight, elem.scrollLeft/scrollTop

  - 焦点
    - elem.focus() 可以引起两次重排
  - 获取其他属性
      - elem.computedRole, elem.computedName
      - elem.innerText
- window.getComputedStyle()
  - 通常会引起样式重新计算
  - 元素在shadow tree中
  - 使用了media queries（viewport相关的一种），特别是以下某一属性
      - width, height
      - aspect-ratio,device-pixel-ratio, resolution, orientation
  - 获取以下的某一种属性
      - width, height，top, right, bottom, left
      - margin,padding
      - transform, translate, rotate, scale
      - x, y, rx, ry
- window
  - window.scrollX, window.scrollY, scrollBy(), scrollTo(), scrollX/Y
  - window.innerHeight, window.innerWidth
  - window.getMatchedCSSRules() 仅重新计算样式
  - webkitConvertPointFromNodeToPage(), webkitConvertPointFromPageToNode()
- form
  - inputElem.focus()
  - inputElem.select(), textareaElem.select()
- mouse
  - mouseEvt.layerX/layerY, mouseEvt.offsetX/offsetY
- document
  - doc.scrollingElement 仅重新计算样式
- range
  - range.getClientRects(), range.getBoundingClientRect()
- svg
  - computeCTM(), getBBox()
  - getCharNumAtPosition(), getNumberOfChars()
  - getComputedTextLength(), getSubStringLength(), selectSubString()
  - instanceRoot
  - 很多
- contenteditable
  - 非常多，包含复制图片到剪切板
- 如何避免reflow
  - for循环里触发重排或改变DOM性能最差
  - 使用DevTools Timeline分析性能问题的位置
  - 合并读写DOM操作，参考[FastDOM](https://github.com/wilsonpage/fastdom)，或使用虚拟DOM
- ref
  - https://jinlong.github.io/2015/09/30/what-forces-layout-reflow/
  - https://www.zcfy.cc/article/fastersite-how-not-to-trigger-a-layout-in-webkit
# electron-chromium
- products
  - midori-next: 桌面版基于wexond, 移动版基于gecko
  - [Is Duckduckgo privacy browser based on chromium, gecko or webview ? : androidapps](https://www.reddit.com/r/androidapps/comments/gwpb9n/is_duckduckgo_privacy_browser_based_on_chromium/)
    - The DuckDuckGo browser uses WebView, the OS-provided rendering engine. In its essence, it's just a UI slapped on to WebView, which is why it's so small. 
    - At the moment, the only WebView options are Chrome and Chromium, so basically, DDG uses Chrome/Chromium.

- https://github.com/samuelmaddock/electron-browser-shell /ts
  - A minimal, tabbed web browser with support for Chrome extensions—built on Electron.
  - forks
  - https://github.com/fvulich/electron-chrome-extensions

- https://github.com/wexond/browser-base /ts/最近版本v5.2_202102/更新到202201/archived
  - Wexond Base is a modern web browser, built on top of modern web technologies such as Electron and React, that can also be used as a framework to create a custom web browser
  - wexond: We've also moved to Chromium as Electron just lacked many important browser features._202111
    - https://twitter.com/sentialx/status/1457867597156917251
    - And we had our fork of Electron which tried to import those features from Chromium, but it was just too much to manually implement all of them, at least for me alone.
  - Wexond has been acquired_202211
    - https://twitter.com/sentialx/status/1588103883494227971
  - [forks](https://github.com/wexond/browser-base/forks)
    - https://github.com/Alex313031/promethium
    - https://github.com/skyebrowser/skye
    - https://github.com/Nalem14/browser-base

- https://github.com/TrueHerobrine/SwiftBrowse /python
  - Fast, Private, Lightweight browser based on PyQt5/QtWebEngine
  - [Making a browser using Webkit and Python : browsers](https://www.reddit.com/r/browsers/comments/14u8jf3/making_a_browser_using_webkit_and_python/)
  - QtWebEngine is chromium but significantly easier to maintain. All-in-all, with a tab system and cookies
# firefox-gecko
- https://github.com/Floorp-Projects/Floorp
  - https://floorp.app/
  - Firefox-based, flexible browser developed in Japan with a variety of features!

- https://github.com/dothq/browser-desktop
  - https://www.dothq.org/
  - web browser with rugged privacy features out-of-the-box
# webkit-browsers
- https://github.com/OtterBrowser/otter-browser /cpp/GPLv3
  - https://otter-browser.org/
  - Otter Browser aims to recreate the best aspects of the classic Opera (12.x) UI using Qt5

- https://github.com/kapouer/node-webkitgtk /js/deprecated
  - webkitgtk bindings for Node.js
  - see express-dom version >= 6 to prerender web pages using playwright.
  - Typically, express-dom can run on webkitgtk's jsdom mode - developers can work on other platforms where jsdom builds fine.

## webkit-apps

- https://github.com/sonnyp/Playhouse
  - Playground for HTML/CSS/JavaScript
  - GTK, GLib, Flatpak, GtkSourceView, libadwaita, GJS, Blueprint, WebkitGTK

- https://github.com/vikdevelop/photopea_app
  - Photopea Desktop App for Flatpak (Electron + WebKitGTK wrapper)

- https://github.com/devongovett/node-wkhtmltopdf
  - A wrapper for the wkhtmltopdf HTML to PDF converter using WebKit
# discuss-💡webview
- ## 

- ## 

- ## 

- ## [what is the difference between Webview, Chromium and Gecko based browers? : androidapps](https://www.reddit.com/r/androidapps/comments/121q81o/what_is_the_difference_between_webview_chromium/)

- Webview is a component for Android apps to show web content. It is based on Chromium, but has less features and depends on the system.

- What is webview? It's a core app of Android that uses chromium to provide web content inside other apps. 
  - Non browser applications use webview to show webpage features (logins, ads, payment etc.) without going to an external browser. 
  - It has no interface of its own, no browser-like features, no settings. It uses relatively very less memory to render webpages.
  - Chrome and Webview use the same library (Trichrome Library) but they don't share data between each other.
- About webview-based browsers
  - You'll see many browsers that are based on webview. They claim to be small in size, faster than light etc etc. But they don't provide all the features and security of a dedicated browser. 
  - I see a lot of Browsers which are based on Webview and not Chromium, requires a very little size. Like Via, Lighting and Fulguris where size ranges from merely 1Mb to 5Mb while the Chromium based browsers like Bromite, Mulch and Chrome are around 130 to 180Mbs.

- ## [基于webview和基于chromium实现一个android浏览器，哪个更好？ - 知乎](https://www.zhihu.com/question/319347088/answers/updated)
- 如果你是指android上的话，webview在4.4以后默认也是基于chromium实现的，
  - 但是webview缺乏一些常见的浏览器功能比如下载管理，tab等，它只是个view，而chromium是一个完整的浏览器，完整到你可能需要花大力气去掉一些不要的功能，比如登陆同步等。

- ## [webview和webkit是什么关系？ - 知乎](https://www.zhihu.com/question/53343196)

- 为了可跨平台开发一次可以部署iOS、Android等平台；发布更新快；在服务器端发布；还能够实时更新终端展示；便于快速升级以及紧急修复bug；排版复杂的内容等等。WebView诞生并开始逐渐发展起来。

- 从IOS2开始，UIWebView出现了，开发者只需创建一个 UIWebView 对象，便可将其附加到窗口，然后向其发送加载 Web 内容的请求。
  - 从IOS8之后，WKWebView出现，UIWebView慢慢不再被使用
- WKWebView是一个现代的支持最新Webkit 功能的网页浏览控件
  - 采用跨进程方案
  - Nitro JS解析器，60fps的刷新率，性能和safari比肩，对h5实现了高度支持
  - 内存开销更小
  - 和safari使用相同的js引擎 JavaScriptCore

- Android（4.4 KitKat 版本之前）使用的是Webkit作为其引擎，4.4开始（API 级别 targetSdkVersion 19）引入了基于 Chromium 的新版 WebView，自此包括了 V8 JavaScript 引擎，并支持以前在旧 WebViews 中缺少的现代 Web 标准。
  - 新的 WebView 与安卓上的Chrome for Android有一样的引擎，因此 WebView 和安卓里的 Chrome 之间的渲染更加一致
  - 从 Android 7（API 级别 24）开始，WebView在Google Play 商店中作为单独的应用程序提供。我们可以安装它们的任意组合来测试几个即将发布的 WebView 版本以及最新的稳定版本。

- ## [为啥安卓原生开发要倒腾那么一大堆布局？直接Webview+js桥不香么？ - 知乎](https://www.zhihu.com/question/425726082)
- 原生开发的优势，在于可以更好地调用手机底层资源（摄像头、通讯录、存储等），而非样式布局。

- 安卓团队诞生于2003年10月
  - 而HTML5正式发布是在2008年。

- 已经有这样的技术了，Google的flutter就是朝着这个目标努力，为啥不用webview其他人回答过了，webview没法提供像原生一样的流畅感，更关键的是Javascript桥接的速度不咋样。
  - 原生安卓的弊端也是对于不同分辨率设备适配的问题，就算你用webview适配不同分辨率也够让人头疼的。

- ## [为什么android不采用NB的chromium或者blink作为缺省内核，而采用webview? - 知乎](https://www.zhihu.com/question/23955365)
- WebView是Android提供的API，是为了方便程序员使用的浏览器引擎封装。至于WebView的实现，可以有多种方法，比如自Android 4.4之后就使用了blink引擎。
  - chromium有一大特点，就是极耗内存，在硬件配置不那么高的机器上，渲染性能是比不上原来的webkit内核的。
  - 在chrome新版本中(201703)，webview已经由chrome for android驱动，还没有研究是怎么做到的。也就是说以后只要chrome for android版本升级，就是系统的web引擎升级了。再也不用等android版本升级

# discuss-webkit-browsers
- ## 

- ## [Why are there no open source browsers using Webkit as the core engine? | The FreeBSD Forums](https://forums.freebsd.org/threads/why-are-there-no-open-source-browsers-using-webkit-as-the-core-engine.88112/)
- Webkit, while OSS, is corporate owned and driven by Apple - also the reason why Google created their own fork, Blink, to get free of Apple's influence
- Building Webkit takes forever, even on a quite powerful machine, 

- ## [Why did Google decide fork Webkit instead of Gecko? : browsers](https://www.reddit.com/r/browsers/comments/12usnvw/why_did_google_decide_fork_webkit_instead_of_gecko/)
- Back then (and now), Mozilla code base was quite large and slow. Compared to webkit, much smaller and easier to develop new features for.

- ## [Frequently asked questions | qutebrowser](https://qutebrowser.org/doc/faq.html)
- qutebrowser uses Qt and `QtWebEngine` by default (and supports `QtWebKit` optionally). 
  - `QtWebEngine` is based on Google’s Chromium. With an up-to-date Qt, it has much more man-power behind it than WebKitGTK+ has, and thus supports more modern web features - it’s also arguably more secure.
  - While Qt only updates to a new Chromium release on every minor Qt release (all ~6 months), every patch release backports security fixes from newer Chromium versions
- QtWebKit is also supported as an alternative backend, but hasn’t seen new releases in a while. It also doesn’t have any process isolation or sandboxing.

- ## [Browser engine in Otter_202206](https://www.reddit.com/r/browsers/comments/vdq7td/browser_engine_in_otter/)
  - I have a question - Wiki says that Otter supports both QtWebkit (not supported by Qt anymore) and QtWebEngine (which is the Blink engine as used in Chromium).
  - When I downloaded the Windows version of Otter it seems to use the Webkit version, with no option to change. The user agent string says "AppleWebKit/602.1". I don't know how old the 602 is but according to this website it corresponds to Safari 10.0 from 2016.
- AFAIK, Otter Browser uses the latest QtWebkit-ng on Windows. It scores 341 points in HTML5Test. There is also an experimental Qt WebEngine backend.

- [affected by chromium dropping support ?](https://dndsanctuary.eu/index.php?PHPSESSID=1233ccab74c6651ba984e00c892d6b4a&topic=3969.0)
  - The default is QtWebKit, but you can switch either specific domains or everything to QtWebEngine if it was compiled with support for that. 
