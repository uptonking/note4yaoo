---
title: viz-base-canvas
tags: [canvas, viz]
created: 2020-07-17T13:36:32.433Z
modified: 2020-12-21T07:46:54.190Z
---

# viz-base-canvas

# guide

- tips
  - 可以在页面布局上使用dom，在节点密集或操作、更新密集的布局使用canvas
    - 比如窗口型应用window manager可以在布局用dom，窗口中内容的渲染使用canvas

- ui渲染
  - canvas是一种立即模式的渲染方式，不会存储额外的渲染信息。
    - Canvas受益于立即模式,允许直接发送绘图命令到 GPU。直接由显卡来渲染， 而不必经过层层规则计算。
  - 在HTML中，由于元素存在顺序，以及CSS中存在z-index，因此是很容易实现的。 
  - dom渲染是一种保留模式，保留模式是一种声明性API，用于维护绘制到其中的对象的层次结构。
    - 保留模式API的优点是，对于你的应用程序，他们通常更容易构建复杂的场景，例如DOM。
    - 通常这都会带来性能成本,需要额外的内存来保存场景和更新场景，这可能会很慢

- 技术选型
  - 全局canvas自绘制，还是部分自绘制+部分基于现有框架/dom的混合绘制
  - 比如，基于canvas的data-grid很多只有行列部分是canvas，其余部分是基于dom实现
# blogs

## 🎨💡 [浅谈 Canvas 渲染引擎 - 知乎_202302](https://zhuanlan.zhihu.com/p/608415829)

- 用过 Canvas 的都知道它的 API 比较多，使用起来也很麻烦，比如我想绘制一个圆形就要调一堆 API，对开发算不上友好。
- 为了解决这个痛点，诞生了例如 PIXI、ZRender、Fabric 等 Canvas 库，对 Canvas API 进行了一系列的封装。
- 今天主要介绍一下社区几个比较有代表性的 Canvas 渲染引擎的设计原理。

- Canvas 渲染引擎一般包括下面几个特点：
  - 封装 将 Canvas API 的调用封装成更简单、清晰的形式，贴近于我们使用 DOM 的方式。
  - 性能 虽然封装之后的 API 很贴近 HTML 语法，但也意味着开发者很难去做一些底层的性能优化。因此，大部分 Canvas 渲染引擎都会内置了一些性能优化手段。有离屏渲染、脏区渲染、异步渲染等等
  - 跨平台 一些渲染引擎为了更加通用，在底层做了更多抽象，不仅支持 Canvas Renderer，甚至还支持 WebGL、WebGPU、SVG、CanvasKit、小程序等等，真正实现了一套代码多种渲染。

- 虚拟节点
  - 目前主流的 Canvas 渲染引擎都会将要绘制的图形封装成类，以方便开发者去调用，复用性也比较强。调用方式类似于 DOM，每个实例可以当做一个虚拟节点。

- 包围盒
  - 有了虚拟节点，那知道每个虚拟节点的位置和大小也比较重要，它会涉及到判断两个图形是否相交、事件等等。
  - 如果直接对不规则元素进行碰撞检测会比较麻烦，所以就有了一个近似的算法，就是在物体外侧加上包围盒
  - 目前主流的包围盒有 AABB 和 OBB 两种。
  - AABB 包围盒： 实现方式简单，直接用最大最小的横纵坐标来生成包围盒，但不会跟着元素旋转，因此空白区域比较多，也不够准确。 也是目前 Konva 和 AntV 使用的方式。（适合表格业务）
  - OBB 包围盒： 实现方式相对复杂，通过构建协方差矩阵来计算出新的坐标轴方向，将其顶点投射到坐标轴上面来得到新的包围盒。 所以 OBB 包围盒更加准确一些，也是 cocos2d 使用的方式。

- 排版系统
  - 绘制 Canvas 的时候一般是通过相对坐标来确定当前要绘制的位置，所以都是通过各种计算来拿到 x、y。 即使是 Konva 也是依赖于 x、y 来做相对定位。
  - 因此，在 AntV 和 SpriteJS 这类 Canvas 渲染引擎里面，都内置支持了盒模型的语法糖，底层会将盒模型属性进行一次计算转换成 x、y。
  - 以 AntV 为例子，排版能力是基于 Facebook 开源的 Yoga 排版引擎（React Native）来实现的，支持一套非常完整的盒模型和 Flex 布局语法。
  - 在腾讯开源的 Hippy 里面自己实现了一套类似 Yoga 的排版引擎，叫做 Titank。

- 事件
  - 由于 Canvas 渲染引擎都会封装虚拟节点，每个节点都有自己的包围盒，所以为实现 Canvas 的事件系统提供了可能性。
  - 主流的 Canvas 渲染引擎都是针对 Canvas 节点或者上层节点进行事件委托，监听用户相关的事件（mouseDown、click、touch等等）之后，匹配到当前触发的元素，将事件分发出去，并且拥有一套向上冒泡的机制。
  - 目前主流的两种事件实现方式分别是取色值法和几何法。
- 取色值法
  - 取色值法是 Konva 采用的实现方式，它的实现方式非常简单，匹配精确度很高，适合不规则图形的匹配。
  - 在主 Canvas 绘制一个图形的时候，会为这个图形生成一个随机的 colorKey（十六进制的颜色），同时建立类似于 `Map<colorKey, Shape>` 的映射。
  - 绘制的同时会在内存里的 hitCanvas 同样位置绘制一个一模一样的图形，填充色是刚才的 colorKey
  - 当用户鼠标点击 Canvas 画布的时候，可以拿到鼠标触发的 x、y，将其传给内存里面的 Canvas
  - 对于不规则图形的匹配依然很精确，但缺点也很明显，每次都需要绘制两份，导致绘制性能变差。
  - getImageData 耗时比较高，在频繁触发的场景（onWheel）会导致帧率下降严重。
- 几何法
  - 几何法有很多种实现方式，这里主要讲解引射线法
  - 几何法是 AntV 和飞书文档采用的实现方式，实现方式相对复杂一些，针对不规则图形的匹配效率偏低。
  - 基于当前虚拟节点的包围盒来构建一棵 R Tree
  - 当用户触发事件的时候，利用 R Tree 来进行空间索引查找，依据 z-index 找到最顶层的一个图形
  - 从目标点出发向一侧发出一条射线，看这条射线和多边形所有边的交点数目
  - 如果有奇数个交点，则说明在内部，如果有偶数个交点，则说明在外部
  - 几何法的优势在于不需要在内存里面进行重复绘制，但依赖于复杂的几何计算，因此不适合有大量不规则图形的情况。
  - 在 AntV 里面支持对不规则图形的匹配，但飞书文档由于是表格业务，所以可以将所有图形都当做矩形来处理，反而更简单一些。

- 性能
  - 由于 Canvas 渲染引擎都会进行大量的封装，所以开发者想针对底层做性能优化是非常难的，需要渲染引擎自身去支持一些优化。
- 异步批量渲染
  - 在飞书文档 Bitable 和 Konva 里面都支持异步渲染，将大量绘制进行批量处理。
- 离屏渲染
  - 离屏渲染我们应该都比较熟悉了，就是两个 Canvas 来回用 drawImage 绘制可复用部分，从而减少绘制的耗时
  - 在 Konva 中的离屏渲染主要是针对 Group 级别来做的，通过调用 cache 方法就能实现离屏渲染。
  - 飞书在底层之上封装了虚拟列表的 Widget，也就是基于业务定制的 Widget，这也是一种有趣的思路。
- 脏区渲染
  - 对于 Konva 来说，每次重新渲染都是对整个 Canvas 做 clearRect 清除，然后重新绘制，性能相对比较差。
  - 更好的做法是检测到当前的改动影响到的范围，计算出重绘范围后，只清除重绘区的内容重新进行绘制。
  - 在 Canvas 中可以通过 rect 和 clip 限制绘制区域，从而做到只对部分区域重绘。
  - 飞书文档多维表格没有做 Canvas 渲染分层，但对各种交互响应速度非常快，也是得益于底层渲染引擎对脏矩形渲染的支持，它的性能也是所有同类产品里面最好的
- 除了上述的这些，还有在文档这边使用的一些优化手段，比如合并相同属性的图形绘制（线、矩形、文本等）、Canvas 分层等等，这些就不多做阐述了。

- 跨平台
  - 很多 Canvas 渲染引擎并不满足于只做 Canvas，一般还会支持一些其他的渲染模式，比如 SVG 渲染、WebGL 渲染、WebGPU 渲染等等。
  - 在 AntV 里面通过引入对应的 package 来实现加载渲染器的，在 ZRender 中则是通过 register 来注册不同的渲染器。
- 主流的服务端渲染方式有两种，一种是用 node-canvas 来输出一张图片，在 echarts 等库中都有使用，缺陷在于文本排版不够准确，对于自适应浏览器窗口的情况无法处理。因此它不适用于文档直出的场景。
- 另一种就是通过 SVG 来模拟 Canvas 的效果，输出 SVG DOM 字符串。但它的实现会比较麻烦，也无法 100% 还原 Canvas 的效果。
- 对于更加通用的场景来说，在浏览器端使用 Canvas 渲染，服务端使用 SVG 渲染是更合理的形式。
- 在新版 ECharts 里面，针对 SVG 服务端渲染的能力，还支持了 Virtual DOM 来代替 JSDOM，最后转换成 DOM 字符串。
- 在飞书文档中使用了一种完全独立于 node-canvas 和 SVG 的解决方式，非常值得我们借鉴。
- 由于飞书多维表格底层统一了渲染引擎，所有绘制元素都是 Widget（对齐 Flutter），可以脱水转换成下面 FVG 格式。

- 一般来说，文档业务首屏加载是下面这么几步：
  - 获取首屏数据 -> 资源加载 -> 首屏数据反序列化 -> 初始化 Model 层 -> 计算排版数据 -> Canvas 渲染
# faq

## 要不要全局 all in canvas ?

- dom pros
  - dom的a11y实现更简单
  - dom的提供了事件系统
  - dom和css配合很好
  - 实现动画很方便
  - 维护成本低，招人容易

- dom cons
  - 内存占用高
  - 使用html元素部分属性值有限制，可修改的属性也是固定的，灵活度有限

- canvas pros
  - better render performance，因为不是保留模式不需要处理额外信息
  - 灵活度高，可控制渲染的细节
  - 占用内存少，因为不是保留模式不需要保存过多的额外信息

- canvas cons
  - 学习成本高、维护成本高
  - 重绘的区域过大时，性能可能会很慢

## [DOM vs. Canvas](https://www.kirupa.com/html5/dom_vs_canvas.htm)

- When to Use Which?
  - You can choose just one, the other, or even both.

- When I Use the DOM
  - simple

- When I Use a Canvas
  - Complex visualizations
  - Animations involving content that nobody needs to interact with
  - Pixel manipulation 

- ### dom pros
- Easy to use. 
  - The DOM abstracts away a lot of the details that would otherwise get you bogged down. 
  - Examples of details that can bog down even the best of us include layout, event handling, clean up, selection/highlighting, accessibility, being DPI friendly, and so on.
- Redrawing is handled for you. 
  - You only specify what you want to display on the screen. 
  - The details of how to do that and how often to refresh are all left to the Graphics API to handle.
- CSS! CSS! CSS! You can easily modify the visuals of your DOM elements using CSS.
- Animations are easy to define and modify. 
  - Because of the CSS support, you can easily define animations or transitions, specify an easing function, make a few other tweaks, and you are good to go. 
  - This applies to JavaScript-based animations as well. 
  - If you are using JavaScript to animate an element's properties, you just have to get your requestAnimationFrame loop setup to update the property values. Everything else is taken care off...such as when to redraw or how to maintain a smooth frame rate.

- ### dom cons
- Memory intensive. 
  - You know all of the details that get taken care of for you when using a DOM element? Well, that care doesn't come cheap. 
  - Your DOM elements are very complex little things, and all of this complexity takes up space in your browser's memory. 
  - The more elements you are dealing with, the more resource hungry it all gets.
- Less control over how things get drawn. 
  - For certain graphics-related tasks, the default rendering may be a bit limiting. 
  - Browsers optimize for their particular needs, and those optimizations may go counter to what you want to do.

- ### canvas pros
- Fast. Really fast. 
  - Because an immediate mode system doesn't maintain its own model, your code is all that stands between you and the browser redrawing. 
  - The many layers of abstraction that slow operations down simply do not exist in the immediate mode world.
- You have a lot of flexibility. 
  - Since your code controls all aspects of when and how something is drawn to the screen, you can tweak and customize the output any way you would like.
- Great for dealing with many elements. 
  - Compared to a retained mode system where every little addition to your scene takes up extra memory, immediate mode systems don't have that problem. 
  - Generally, an immediate mode system will always use less memory than a retained mode system

- ### canvas cons
- It can be slow when drawing to large areas. 
  - How quickly a redraw completes is proportional to the number of pixels you are re-drawing. 
  - If your addressing a really large area, things could get slower if you are not careful and do not optimize appropriately.
- It is complex. 
  - Because you are handling more of what it takes to get something to display on the screen, there are a lot more details for you to keep track of. 
  - Getting up to speed with the various draw commands and how they are used is no picnic either.

## [What are the advantages/disadvantages of Canvas vs. DOM](https://stackoverflow.com/questions/2266416)

- ### dom pros
- rendering by the browser, so less error-prone; 

- ### dom cons
- could do simple animation with CSS only, that makes the game not fluent; 
- no good for manipulating hundreds of DOM elements; 

- ### canvas pros
- could manipulate pixel and apply filter effect, so easy for image processing; 
- very efficient for small size but hundreds of elements in the game
- many libraries for game could be found using canvas, such as box2dweb, and could make awesome games such as angry bird

- ### canvas cons
- it's stateless, so you have to record the states of the elements in the canvas, and handle the hit test by yourself.
- low efficient for very large size but with one a few elements in the game
- great ability, great responsibility. the freedom to draw, brings in you have to charge of all the drawing staff. Fortunately, there are many libraries there, such as cocos2d-html5, IvanK.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 当年基于flex技术的webAPP几乎在那个时候成为的业界主流，但是随着flash技术的没落，为什么H5中取代flash的canvas技术并没有成为业界进行webAPP开发的主流呢？
- https://www.zhihu.com/question/55357068/answers/updated
- 众所周知浏览器处理DOM是相对较慢的，而在canvas内部的绘图布局的处理会快很多
  - flipbroad的webAPP使用过react-canvas来制作网站，但是目前的主流依然是dom+css
- canvas确实能实现一些复杂动画，但是实现的同时也付出了代价：代码无法做到标签化，语义化。
  - 可能你需要写一堆数学公式来计算轨迹什么的，想过没有，维护这样的代码又是什么样的体验？
  - 如果canvas整站真的火了，估计也会有人发明一套和html css差不多的东西来简化编程。于是乎，又绕回来HTML CSS了。
  - 我觉得大可不必全站canvas，那些需要绚丽效果的地方使用canvas足矣
- 人家发明 html 和 css 本来就是为了让你尽量不要自绘，因为这事儿开发成本太高，为了解决特殊需求，人家又给你提供了 canvas。
  - 如果非要完全自绘，干嘛还要用 webview 呢？
- Flipboard 2年前就这样做了，而且效果拔群
  - 不过伴随虚拟 DOM 的出现和 React 的火热， Flipboard 开源了 react-canvas，对 React 渲染层的封装，简化了 DOM树 → 虚拟DOM → Canvas 的这一流程。但是毕竟是 JS 写的渲染层， 所以和 react-native 在原生环境一样，都有一定的局限。

- canvas本身学习成本高，开发思维和一般意义前端不同，诚然尖端的游戏引擎、渲染、数据可视化、webgl方面肯定是需要人才的，
  - 但是低端的可替代性，其陡峭的学习曲线，是否可以说明其生态的恶化？低端的人没有实践场景我觉得是很难走到高端的。
  - 题主工作是金融方向，接触过一些数据可视化的东西，刚好项目需要，所以满心欢喜的去学canvas与svg等相关技术，但是真做需求发现自己写出来的东西还不如ui用设计软件做出来的，于是很迷茫，是不该选择这个方向吗？

- ## 虽然对于 Terminal 这样的纯字符 UI，很多人一开始都会想，既然 @code 基于 @electronjs ，那么 Terminal 应该和其他类似的项目一样，直接使用 DOM 来渲染
- https://twitter.com/LeaskH/status/1216221586291863554
  - 事实上刚开始的确是如此， @AtomEditor 到今天依然大量采用 DOM。
  - 但是在 VSCode 1.17 之后，微软已经改为通过 Canvas 实现了
- 这样有几个好处，
  - 首先是因为 Canvas 可以做 delta 渲染，虽然绘制逻辑更加复杂，但是可以做到只渲染变动部分；
  - 第二是因为 Canvas 在目前主流的机器上可以天生使用 GPU 加速。

    - 所以 DOM 版本的 Terminal 由于需要节约 CPU 只能限速到 10 FPS 左右，但是 Canvas 版本可以轻松飞到 60 FPS

  - 还有一点优化很有意思，为了避免每次对字体做栅格化，VSCode 对所有的 ASCII 字符 X 颜色数，做了一个渲染好的位图缓存，

    - 这样就可以直接使用显卡的贴图功能来显示文字，而不需要 CPU 操心。
    - 微软果然是花了不少的心思，我开始理解为什么 VScode 可以比 Atom 快那么多
    - [Integrated Terminal Performance Improvements_201710](https://code.visualstudio.com/blogs/2017/10/03/terminal-renderer)

- ## [实战：在Canvas中实现动画](https://www.zhihu.com/market/pub/119647264/manuscript/1182364509212303360)
- 在Canvas中，动画是通过一系列连续的画面按顺序呈现的。
- 而这些连续的画面是即时绘制出来的，为了让动画更加流畅，可能需要在很短的时间内重新绘制动画很多次。
- 动画的大致实现流程可以分为以下几个步骤
  - 清空画布。
  - 改变绘图的状态，包括变换坐标系统、修改各种属性等。
  - 重新绘制图形。
  - 回到第一步。
- 在上面几个步骤的轮回中，需要将绘制动作放在一个定时器里。JavaScript提供了两个定时器方法，分别是 `setInterval` 和 `setTimeout`

- 为了方便绘制图像，可能需要频繁修改绘图的状态，及时保存和恢复状态可以让你方便许多。

- ## [Canvas动画简介](https://www.zhihu.com/pub/reader/119583977/chapter/1058119929794027520)
- Canvas 动画实际上就是一个「不断清除、重绘、清除、重绘的过程」。也就是说，想要实现 Canvas 动画，也就只有两步。

# blogging

## [KonvaJS 原理解析 - 掘金](https://juejin.cn/post/7016559372331401253)

## [The Future Web: Will Canvas Rendering Replace the DOM?_202105](https://medium.com/young-coder/the-future-web-will-canvas-rendering-replace-the-dom-847be872884c)

- There’s been a lot of hand-wringing recently about Google’s decision to use the HTML `<canvas>` for all of its rendering in Google Docs.
  - Once upon a time the web was supposed to be system for sharing carefully structured information, full of sensible metadata and collaboration. 
  - Instead, we turned it into an semi-opaque app delivery model running in a browser sandbox.
  - Google’s decision — to switch from writing HTML elements on a page to painting pixels on a canvas — isn’t anything developers haven’t seen before.
- Other leading-edge web apps already reach far beyond the traditional confines(限制；便捷) of HTML elements. 
  - Google Maps has been rendering on the canvas for years. 
  - VS Code uses it to draw a pixel-perfect terminal. 
  - And then there’s Google’s emerging Flutter toolkit, which lets you build a cross-platform UI that renders through the canvas by default in a web browser.
- The canvas rendering approach will spread
  - There’s a saying: Where Google goes, others follow.
- Now, Google’s shift to drawing UI on a canvas will legitimatize the approach for a new generation of web developers.
- Google has reimplemented huge swaths of functionality that most programmers take for granted, such as features for precise layout, text selection, spell checking, and optimized repainting.
- The biggest challenge is accessibility.
  - The canvas-based version of Google Docs still needs to give first-class support for screen readers, screen magnifiers, high-contrast settings, and low-dexterity features. 
  - One way they do that is by implementing an invisible DOM that shadows the real canvas-rendered content, but exists only to inform assistive tools. 
  - And of course these two models need to be kept perfectly in sync.
- The semantic web is dead
  - According to HTML5, the web included whatever standards the browser makers could agree on. 
  - It was grouped with a collection of a practical JavaScript APIs (geolocation, local storage, web sockets, backgrounds workers, and so on) that could snap into pages like building blocks. 
  - but the only truly ambitious feature for embedding information was microdata, which was ripped out of the standard shortly after (mostly because Google and Apple weren’t interested in implementing it).
  - canvas is a black box that gives the browser no information or context about what’s happening inside.
- The future is WebAssembly and binary blobs
  - Even if you think canvas rendering is a big deal, it’s dwarfed by even bigger shifts if the web development landscape. 
  - And the biggest is undoubtedly WebAssembly, a low-level binary instruction format that all modern web browsers understand.
- Today, WebAssembly needs a clumsy layer of JavaScript interop to access the DOM. 
  - But the next step is WebGPU, an optimized successor to the now-abandoned WebGL project. 
  - Both WebGPU and WebGL take the same approach — they provide optimized access to a canvas rendering surface.
  - Combine that with hardware acceleration implemented by the browser, and you have a low-level drawing surface that you can use to build the next generation of web applications.
- Even as the future of web apps evolves, the traditional ideas of the web will live on with those sites that suit it — namely, content-heavy sites (everything from tech publications to amazon’s product catalog). 
  - For these sites there’s no reason to reinvent the wheel, customize the rendering process, and re-solve the challenges of accessibility. 
  - But in the future, these websites will no longer define our expectations of content on the web.
- Instead, the app model will have broken completely free of today’s HTML/CSS abstraction. 
  -  This change will probably return developers to a free but fragmented world where they will choose between a wide range of different languages and UI models for their applications. 

## [Figma is powered by WebAssembly. WebAssembly cut Figma's load time by 3x_201706](https://www.figma.com/blog/webassembly-cut-figmas-load-time-by-3x/)

- WebAssembly is a new binary format for machine code that was specifically designed with browsers in mind. 
- Because apps compiled to WebAssembly can run as fast as native apps, it has the potential to change the way software is written on the web.
- Because our product is written in C++, which can easily be compiled into WebAssembly, Figma is a perfect demonstration of this new format’s power. 
  - If you haven’t used Figma before, it’s a browser-based interface design tool with a powerful 2D WebGL rendering engine that supports very large documents.
- Before WebAssembly, C++ code could be run in the browser by cross-compiling it to a subset of JavaScript known as asm.js. 
  - The asm.js subset is basically JavaScript where you can only use numbers (no strings, objects, etc.).
  - WebAssembly is a drop-in replacement for asm.js that is more efficient in every way. 
- There are many benefits to running C++ code using WebAssembly instead of cross-compiling it to JavaScript:
  - The format is very compact so it takes less time to transfer over the network
  - The format was designed to be as fast as possible for the browser to parse. This isn’t true for JavaScript syntax
  - C++ code is heavily optimized by the LLVM toolchain before it’s even encoded in WebAssembly. 
  - It’s trivial for browsers to cache the translation of a WebAssembly module to native code. 
    - This means the second time you load a page using a WebAssembly module, there’s virtually no load time at all! 
    - This isn’t true for asm.js, which is mixed in with regular JavaScript and requires a complex verification pass to validate that it actually follows the asm.js restrictions.
  - WebAssembly has native support for 64-bit integers. 
    - JavaScript only has 64-bit floating-point numbers so it only supports 53-bit integers.
# ref
- [canvas动画](https://zhuanlan.zhihu.com/p/73561191)
  - canvas动画原理：快速切换的静态画面
  - 动画步骤：绘制 - 清空 - 绘制 - 清空 - 绘制...
  - 控制函数：setTimeout, setInterval, requestAnimationFrame
  - 运动效果：线性、变速、函数运动如正弦、环形
- [SpriteJS —— Canvas动画从未如此简单](https://zhuanlan.zhihu.com/p/38265264)
  - SpriteJS是一款由360奇舞团开源的跨终端canvas绘图库，可以基于canvas快速绘制结构化UI、动画和交互效果，并发布到任何支持canvas环境的平台上（比如浏览器、小程序和node）
  - Sprite为图形创建类似于DOM的对象模型，因此我们可以像创建DOM元素一样，创建Sprite元素，并将它们append到layer上，从而将元素呈现到画布上
  - 如果只是绘制静态图形，SpriteJS还体现不出优势，但如果要给图形增加动画效果，那么SpriteJS内置了Transition API和标准的Web Animation API
