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
