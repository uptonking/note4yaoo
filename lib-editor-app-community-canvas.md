---
title: lib-editor-app-community-canvas
tags: [canvas, community, editor]
created: 2023-03-13T08:04:56.829Z
modified: 2023-03-13T08:05:09.453Z
---

# lib-editor-app-community-canvas

# guide

- tips
  - 基于dom的组件比canvas组件对agent更友好
# [Google Docs will now use canvas based rendering: this may impact some Chrome extensions_202105](https://workspaceupdates.googleblog.com/2021/05/Google-Docs-Canvas-Based-Rendering-Update.html)
- We’re updating the way Google Docs renders documents. 
  - we’ll be migrating the underlying technical implementation of Docs from the current `HTML-based` rendering approach to a `canvas-based` approach 
  - to improve performance and improve consistency in how content appears across different platforms.

- ## [Google Docs will now use canvas based rendering__20210512](https://news.ycombinator.com/item?id=27129858)
- canvas comes with very real trade offs though:
  - Cost of implementation and maintenance is much higher with canvas. This is particularly the case with WebGL, there have been very few contributions to xterm.js (the terminal frontend component) in the WebGL renderer because of the knowledge required. 
  - Accessibility needs to be implemented from scratch using a parallel DOM structure that only gets exposed to the screen reader. Supporting screen readers will probably also negate the benefits of using canvas to begin with since you need to maintain the DOM structure anyway.
  - Plugins/extensibility for webapps are still very possible but requires extra thinking and explicit APIs For xterm.js we're hoping to allow decorating cells in the terminal by giving embedders DOM elements that are managed/positioned by the library.
- More recently I built an extension for VS Code called Luna Paint which is an image editor built on WebGL, taking the lessons I learned from working on the terminal canvas renderer to make a surprisingly capable image editor embedded in a VS Code webview.

- A good open-source example of this type of problem is CodeMirror (a code-editing widget for the web). 
  - To achieve syntax highlighting and everything else, it basically fakes every single aspect of text editing in a browser context - even the cursor and text highlighting - replacing the native versions with pixel-placed DOM elements driven by JS. 
  - It receives raw events from an invisible textarea and does everything else itself.
  - This is just about the worst possible use-case for the DOM: you get almost none of the benefits, and still get most of the costs.
# discuss-stars
- ## [canvas富文本，为什么只有google doc在答卷？ - 知乎](https://www.zhihu.com/question/567085593/answers/updated)

- 主要是开发难度大，并且几乎没有什么收益。
- 现在的富文本编辑器都会有各种眼花缭乱的组件，例如视频、表格、日历等等，如果使用canvas来做渲染，那这些高级组件用什么方式开发呢？
  - 用canvas开发的话难度高得离谱，用传统方式开发，那整个就是个缝合怪，一部分用canvas渲染，一部分用原生渲染，意义何在。
- 要想完全在canvas上模拟dom的各种交互，难度也是非常高的，怎样模拟选区？怎样在输入聚焦能ctrl+a全选，并能使用右键菜单？这些看似简单的问题能折腾死你。
- canvas做富文本，性能方面也没有显著优势，
  - 一个简单的道理：你用浏览器提供的API去模拟浏览器本身就有的渲染能力，性能竟然还能远远超过浏览器原生的渲染能力？这可能吗。
  - 除非你舍弃掉复杂的交互，单纯绘制图形，这样性能才有可能超过浏览器的原生渲染能力，但这明显不是富文本的场景
  - 所以我觉得用canvas去做富文本编辑器就是邪路，投入产出比极低

- 一般用canvas的都是EXCEL表格，如果用DOM去实现那么需要渲染的节点也太多了，非常影响性能，一个DOM节点就算是空的也会初始化很多东西，在页面重绘的时候，最少上万个DOM元素，渲染任务该有多重，使用canvas就是为了优化这一方面。使用canvas在少量数据的时候也许没有DOM性能高，但是在大量数据渲染的时候一定比DOM好多了
  - DOM同样能用做只渲染可视区域的优化，虚拟列表就是类似的技术，事实上很多性能很强的前端excel方案并没有用canvas
- 你这是纸上谈兵了，你没做过富文本编辑器，可能不知道处理输入、输入法、选区之类的难度，哪怕不用contenteditable都是非常难的，何况是用canvas

- figma或者蓝湖的mastergo，跟富文本不是同一个场景，这些设计类软件侧重于图形渲染，这才是真正适合canvas和webgl的场景，并且它们里面对文字排版的支持都非常弱，你可以了解一下webgl渲染文本的难度，绝对超出你的想象。用这些图形技术去做富文本渲染，纯粹是自找麻烦

- canvas富文本，并不是只有google doc在答卷。
- 其实在十年前，onlyoffice在microsoft、google之前就基于canvas在浏览器里实现了ms word的大部分编辑功能。
- onlyoffice使用canvas渲染文档，并不是为了防止复制、粘贴、爬虫。
  - 完全是为了更好的还原ms word的排版。例如文字绕图，在浏览器里只能左绕图右绕图，但ms word里有四周绕图，怎么办？onlyoffice给的答卷是，使用canvas，自己控制排版
- 基于“更好的还原ms word的排版”这个目标，canvas做富文本对无障碍访问不友好是次要的缺点，并且可以类似pdf.js那样用隐藏文字层在一定程度上弥补（不过onlyoffice还没有这样做）。
- 除了onlyoffice，对ms word的排版还原度比较高的是ms office在线文档 和 wps在线文档，可能是为了在工作量和呈现效果上取一个平衡，目前（2022年）ms office在线文档是部分html+canvas，wps文档甚至没有用canvas，用的是html+svg。这样做也可以理解，html+css可以实现的排版就html+css，html+css实现起来别扭的就上svg。
- 至于 腾讯文档，虽然编辑时用了canvas，但目前（2022年）数据保存时却存的是html格式。我非常奇怪，因为html+css难以实现某些排版才使用canvas，那么数据存储最好是用自有格式（例如json）来标记那些特殊的排版，您用html存，难道html就足以表达用到的排版了？使用canvas的意义何在？真的仅仅是为了防止复制？——我的推测，腾讯文档对ms word的特殊排版效果的支持不如onlyoffice、wps在线文档，可能未来还会有大的改进，充分利于canvas来控制排版。
- 还有google文档。google对ms word的特殊排版效果的支持甚至不如onlyoffice、wps在线文档，估计google也不care这些。可能google的想法是“我要控制好排版，但并不是为了兼容ms word”

- 其实 ms office 网页版也（部分）用了 canvas 富文本，但是 office 网页版属于是能 DOM 的地方就 DOM 做的，实在不行才上 canvas。
  - 使用dom: word, ppt
  - 使用canvas: excel

- 为什么不全盘用 canvas？因为对于 automation 和 accessibility 是灾难啊。
  - mozilla的pdf.js在使用canvas绘制pdf页面时，还额外绘制了一个不可见的文本层解决文本选取和无障碍问题，但是性能优势就没了
  - 比如浏览器的翻译、朗读、页面内查找、右键搜索选词、页面内快捷键、锚点跳转功能
  - 口口声声说为了性能，用户体验都没了
  - 广告屏蔽插件不就没用了吗

- 写一套canvas渲染库，能有效防止复制粘贴、爬虫。
  - 客户端上传视窗对象，服务器返回canvas对象，客户端渲染UI界面，挺好的。
  - 对于讲究速度的小企业来说，根本不可能有人去做！

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

- ## 如何看待 Google Docs 将从 HTML 迁移到基于 Canvas 渲染？
- https://www.zhihu.com/question/459251463/answers/updated

- canvas不等于canvas2d，有可能是 canvas3d，对于大型文档，用 WebGL 渲染不香么
  - WebGL是没有文字能力的纯光栅化API，渲染大型文档不香
  - canvas 2d 渲染东亚文字，性能也是灾难，所以不用 DOM 真的很奇怪，除非真的是遇到什么绕不过去的坎了
  - 你用过 WebGL 和 Skia 吗？两者不在一个抽象层级上。Flutter 是在 WebGL 上面跑了 Skia，用Skia这套类似 Canvas 2D 的 API 来做绘制。Flutter Engine 本身既不需要也不应该直接调 GL 这层级的东西
  - 直接拿 WebGL 来做文字，除了 2D 地图 SDF Text 之类要特殊优化的场景，基本是自讨苦吃

- Google Docs 会采用 canvas 是否标志着网页三剑客（HTML、CSS、JS）的没落？
  - 肯定不是，采用 canvas 渲染取决于 Google Docs 的项目复杂度和特殊性，99.9999%的项目用网页三剑客无疑是更好的选择，
  - 文本处理器（Google Docs）有超高的一致性和性能要求，这些要求绝大多数应用根本不需要考虑，
  - 可惜，Google Docs 就是那 0.0001% 它是极其特殊的存在
  - 而且我个人认为 Google Docs 并不会重新造一个类似于 flutter 的 UI 系统，而是重写「字体解析」「字体整形」「文本布局」「文字处理渲染引擎」等一系列相关的引擎
- Google Docs 之前的技术选型有什么问题？
  - Google Docs 2010 之前基于 contenteditable ，之后不基于 contenteditable 但仍基于DOM。
  - 基于 contenteditable 的富文本编辑器会产生非常多的问题，已经是老生常谈了
  - Google Docs 在 2010 年也解释了[为什么抛弃 contenteditable](https://drive.googleblog.com/2010/05/whats-different-about-new-google-docs.html)
  - 简单而言就是为了一致性、高级功能（标尺、脚注、分页）、协同编辑。
- 我们重点谈抛弃了 contenteditable 之后为什么依然有问题？
  - 首先，我们解释一下在线文档的一致性是什么？
  - 如果你的在线文档基于浏览器，那么必然会用到浏览器实现的特性，而各大浏览器实现的方式不同，呈现的效果也不同，这就导致了不同浏览器编辑同一份文档会出现不一致
  - 当然你可以用各种方法把这些不一致性抹平，比如拖蓝选区的一致性问题也可以解决，那就是自己写一个相关的库替代浏览器自带的拖蓝选区功能，但是这就像一个无底洞，你不知道像浏览器这种庞然大物到底有多少不一致性，每一次更新都可能带来变化。
  - 越多的依赖浏览器的能力，就越多的受到浏览器一致性问题的困扰
  - 2010 年后 Google Docs 计算出文本的大小进行绝对定位排版，实现了自己全新的文本布局引擎，包括选区、光标、排版都进行了自研，似乎已经彻底摆脱了浏览器的控制，但是事实却不是这样。
  - 现在的 Google Docs 的文本布局引擎是基于 「div+span+绝对定位」 的方式实现的，实际上并没有脱离 DOM，这就到了大量的操作依然依赖于浏览器的底层提供的能力。
- 双向文本（BIDI）
  - 古代汉语、传统蒙语等是纵向排版的，这需要文本处理器可以识别不同的文字进行不同的处理。
  - Unicode 有相关的 BIDI 算法，而 Google Docs 选择了基于浏览器的能力，大家看看这段阿拉伯文， Google Docs 的处理方式，利用了 CSS 的属性，而并非自己实现
  - CSS 基于浏览器提供的底层算法，苹果系统需要 CoreText 提供支持，而 Linux 下则是 fribidi
- 字体解析与渲染
  - Google Docs 的字体解析与渲染依然是基于浏览器的
  - 浏览器在不同平台依赖的底层库也不一致，比如 windows 下的 DirectWrite，Mac 下的 Core Text 等等。就存在一个可能由于解析+渲染导致的不一致问题。
  - 由于 Google Docs 依赖的浏览器提供的底层能力（浏览器的能力部分来自于操作系统），导致了这种不可控的 Bug。
- 性能
  - 目前 Google Docs 依然是我们上面所说的依赖 DOM，那么 Google Docs 的文字处理区域的回流、重绘依然是依靠浏览器自带的能力，
  - Google Docs 目前除了文本布局是由自己接管之外，还得依靠浏览器，
  - 虽然对于绝大多数人浏览器提供的能力已经很够用了（我就觉得挺够用的 ），但是如果自己彻底接管整个文字处理区域的布局、排版，那么优化的上限会很高
- Google Docs 背后技术升级的猜想
- 接管字体相关的一切工作
  - 从字体解析一直到光栅化必须由 Google Docs 自己控制，而非浏览器控制。
  - 字体解析：这需要一个字体解析器，兼容 TrueType 和 OpenType 标准 ，并实现标准中的一系列特性
  - 文本整形（text shaping engine）：文本整形是将一串字符代码（例如Unicode代码点）转换为正确排列的字形序列的过程，这些字形序列可以呈现在屏幕上或最终输出形式以包含在文档中
  - 高级文本布局：目前 Google Docs 倒是实现了这一步，依靠绝对定位 + span 实现了对文本布局的控制，但是我猜想 Google Docs 用的方法是从 TextMetrics 倒推出文本前进宽度进行排版的（应该也没别的办法了），但是  TextMetrics 是个残废 API，很多属性都没有提供
  - 为了适应 Google Docs 的要求，必须实现包括但不限于：
    - dibi 双向文本布局
    - 文本断行
    - 制表符
    - 字间距、行间距、段间距等排版
    - 页码、页眉、脚注等等
- 高性能渲染引擎
  - 浏览器提供了非常便捷的 DOM 直接供我们操作，但是用 canvas 你必须自己实现精灵、事件、动画，并自定义一系列控件，比如「列表」「表格」「按钮」「选区拖蓝」等等等，也就是 DOM 的一切现有的东西都无法复用，必须用 canvas 从头造一遍
  - 可以性能优化的点可能如下：
    - 图形拾取优化
    - 局部渲染
    - 分片渲染
  - 除此之外还有光标处理、对象模型、复制粘贴、撤销等一系列问题应该都不是重点
- Google Docs 向传统桌面文字处理软件比如 WPS、Word 继续贴近了一大步，进入了 Web 文字处理软件的终极形态，从此之后应该不会有大的变化，只有小修小补了。
  - 做这种事情需要大量人力、物力、时间
  - Google 真有钱！

- canvas啥时候被开除出html了，人家是h5的重要标准
  - 应该说是从基于dom转向基于canvas了
  - 之前做视频弹幕我们直接做了两个方案，一个基于css，操作dom移动，一个基于canvas。
  - 最后还是选择了canvas，因为canvas更灵活，更容易实现功能扩展，而且浏览器的canvas环境标准几乎没有区别，无论你是chrome还是ie还是firefox。而如果你用dom的话，哪怕是ul标签都有差异。比如：弹幕暂停，弹幕加边框

- 想做到跨平台表现一致非常难。
  - 特别是涉及到精细排版、文本亚像素渲染什么的，
  - HTML本来就不规定这些事情，各个网页引擎想想就是百花齐放的样子。这些玩意的逻辑全自己写，绝对是必经之路。
  - 我唯一的问题就是：wasm依然是跑在虚拟机上的，和编译到native code的网页引擎性能还是会有点差距，不知道这方面的代价有多大。
- 涉及到图文排版的东西单用HTML搞不定啊，每个系统每个浏览器在字体绘制上都不一样，想要显示出一致的效果必须从头自己动手，这事跑不掉的。

- Web提供的能力和文档编辑的能力需求重合度不高
  - Figma 和 Flutter Web 的出现给未来的 Web 应用指出了一个新的道路，既然 DOM 不适合画出来那就全部自己来画。
  - 至于说是不是弯路，我觉得不是，只是一个更合适的解决方案而已。乐观点，历史总是螺旋上升的，如果未来哪年标准完善+性能过剩到 Web 技术栈能随便写出一个所见即所得的编辑器，我也不会觉得现在的 canvas 是一个弯路的。
# discuss-canvas-dev
- ## 

- ## 

- ## 

- ## 

- ## Nice to see excitement around the proposed html-in-canvas feature, but remember you can already put canvas behind/atop HTML elements.
- https://x.com/jaffathecake/status/2040365428338303225
- The benefits of this new feature are:
  - Readbacks (eg sending to a VideoEncoder)
  - Showing HTML on non-planar shapes
  - Using shaders on HTML
- 🐛 There are a number of optimisations the browser cannot do if you render html to a canvas, such as partial painting, optional painting, texture size management… so you should only do it if there's good reason.
- partial painting is the one that hurts most at scale — a small DOM change triggers a full canvas repaint. 
  - but the deeper issue is accessibility: canvas has no accessibility tree, so anything rendered into it becomes invisible to screen readers regardless of how faithful the visual output looks. 
  - the layering approach you mentioned works precisely because it preserves those separate compositing contexts. 
  - html-in-canvas seems like a unified model but it's actually trading away the optimizations that make both systems fast in order to get a feature that layering already handles.

- I'm watching people rediscover Flash in real time and I have many mixed feelings.

- I thought the whole excitement was mainly because of the whole shaders-on-html thing? Maybe you could make a podcast ep with Surma on this as a follow-up for the "Canvas-based Web Apps" episode? Excited to see the performance and accessibility gains that come out of this !

- https://x.com/shuding/status/2040446529623015743
  - These are real WebGL shaders on top of interactive DOM elements without the HTML-in-Canvas API (works in Safari too). There’re rough edges still but worth sharing

- https://x.com/CantBeFaraz/status/1599096000777318401  _202212
  - Another stab at correctly occluded interactive HTML inside of @threejs with R3F 
  - A fully interactive instance of @tldraw behaving like a normal plane with shadows at 60fps on iOS
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🌰 [飞书文档前端使用了什么技术呢? - 知乎](https://www.zhihu.com/question/548405585)
- 飞书文档 Doc 还是用的 DOM，表格用了自研 Canvas 进行绘制。看了一下多维表格，主要是参考了 Flutter 实现一套基于 Widget 的渲染引擎。
- 多维表格和Excel表格是基于Canvas的。 富文本文档还是基于DOM的；之前开过F12看了下富文本，发现可能是Slatejs魔改来的，连data-slate-editor这些节点属性都还在。

- 渲染引擎和协同框架都是自研的
- 同步协作时 ws 传的是二进制数据

- ## For the last couple months, our team has been working hard on a few paradigm-changing features for HTML Canvas.
- https://x.com/JungleSilicon/status/1798424695068569766
  - One of them is the ability to have HTML elements in a canvas.
  - Here's a ThreeJS demo with a live HTML texture.

- Does this mean apps like Google Docs can now simplify their code that renders documents to canvas? Earlier it was all DOM but they moved to canvas with their own rendering pipeline. Does this mean they could use their DOM rendering pipeline itself to render onto canvas?
  - i don't think it would help for their use case.
  - google docs does their own rendering engine so they have more control of the outputs, by rendering the dom to the canvas you would still need to obey the rules of the dom.
  - i'm hoping this means we can save images of portions of the dom for use in things like 3d scenes without needing to use hacks.
- That's a great usecase. I'm also hoping this will somehow help headless PDF generation from HTML. Is this a separate HTML renderer with canvas draw instructions as output or is this just the browser's DOM renderer tuned to play nicely with canvas? I guess it's the latter.

- ## 简单看了下字节公司内的渲染引擎还不少，不说 lynx，单论 js 实现的 web canvas 渲染器，就有三个。
- https://twitter.com/XGHeaven/status/1783023772771270919
  - 但感觉大体思路基本一致，都是以 flutter 这种父节点决定位置，子节点决定大小的布局方式
- lynx是字节内部的吧
  - 是的

- ## [用 SVG 实现的富文本编辑器有什么优势？DOM 和 Canvas 实现又有什么劣势？ - 知乎](https://www.zhihu.com/question/367165828/answers/updated)
- iCloud Pages 和 WPS（web 端）的核心编辑区域直接用 SVG 渲染

- 首先SVG也是DOM，普通的div反过来本质上也是一个长方形的SVG。这两者本质上没有太大区别，在浏览器里就是当作矢量图渲染的（矢量图性能很差）。
- wps（web端）之所以选用svg是为了解决移动端长按文字内容选中的问题，
  - 根据我的测试发现，目前世面上除了金山解决了移动端选择内容的问题。
  - 其他同类产品包括石墨、一起写、office、google doc等都没有解决移动端的兼容问题。
  - 传统的html编辑器通过contenteditable=true来实现富文本编辑器基本很难实现移动端选择部分内容。
- 然而并不是

- Canvas的劣势我认为有以下两点：
  - 一，对文字的渲染能力较弱，不能使用css合成元素Canvas内的图元，也就是各种文字，图片的大小都需要通过canvas API来调整，，可能会有性能问题。
  - 二，处理失真问题Canvas要复杂很多。

- 文字是可以转成路径用 SVG 控制的，只是渲染成本比较高而已
  - 不转路径的话，相当于字体排版全部交由浏览器默认控制，可能满足不了硬核富文本编辑的需求…比如默认的换行中划线斜体这些都不一定符合得了 wysiwyg 的预期，word 里某种排版的文档直接导到浏览器里可能变成另一种，这个坑真要填就太深了…

- ## carota: Rich text editor implemented in JavaScript that uses HTML5 Canvas
- https://www.reddit.com/r/javascript/comments/1zjfcg/rich_text_editor_implemented_in_javascript_that/
  - [Structured Editing: Cross-browser javascript text editor](https://www.fluffy.co.uk/stediting/)
- wouldn't it have been easier to make something that just used the DOM to render the document?
  - That is what `contenteditable` is for. 
  - Problem is that `contenteditable` is a pain in the ass to work with. 
  - Using the DOM to output the rich text is easy until you have to implement the idea of "where is my cursor, what is my selection state, what happens when I press a key?"
- Those problems remain regardless of whether you use canvas or the DOM for rendering.
  - Without using the `contenteditable` , how do you put a cursor into a DOM element?
  - [Fabric.js tests · IText tests](http://fabricjs.com/test/misc/itext.html)

- ## Google docs is apparently moving to a canvas based editor. 
- https://twitter.com/devongovett/status/1392597989768585218
  - This is horrible for accessibility and a great example of what *not* to do. 
  - I’m surprised no one flagged this
  - [google docs canvas preview](https://docs.google.com/document/d/1N1XaAI4ZlCUHNWJBXJUBFjxSTlsD5XctCz6LB3Calcg/preview)
- They could have worked with the Chrome team to help improve standards where they are lacking and make the web better for all of us, 
  - but instead decided to reimplement the browser themselves. Very disappointing.
  - Well, to be fair, the old one was also very broken. But at least it had the potential for improvement. Switching to canvas kinda prevents that.
- Would you say that implementing web apps with the canvas API no-go? Are there other downfalls to be aware of? (aside of a11y problems)
  - Text selection, copy/paste, find in page, spell checking, dictionary, system wide text replacement/auto correct, etc would all need to be rewritten and would not integrate as expected with the system.
- I’ve thought about this approach on Paper in the past (especially for intensive things like tables), but accessibility is one of the bigger issues. 
  - We use content-editable for mutations so it gives us a lot of functionality out of the box (undo/redo, keyboard shortcuts, etc)
  - This approach limits us when trying to do any kind of optimization like virtualization, especially when you add the real time collaboration aspect to it. Its a love/hate relationship 🙂
  - Oh yeah, contenteditable is horrible as well. I’ve written a rich text editor in the past and it was painful. I can see how they reached this approach, but it seems like they didn’t really consider all users.

- ## It sure will be hard to keep telling developers "no, Wasm is not meant to replace JS, no, please don't ship your whole app as one huge canvas" after this 
- https://twitter.com/RReverser/status/1392813653200678914
- JS will be delegated to the entry point + WASM bindings
  - So basically Flash, but using WASM.
- Rendering PDF to canvas used to be easier than generating a proper HTML version. 
  - Sounds like poor Office Word developers could do their web port much slower in smaller steps to be future-ready already.
- Flutter Web (or Flutter, in general) is currently doing this right now since it's whole render engine runs on any implementation of Canvas.
- Regardless of wasm, doing Docs on canvas totally makes sense. 
  - Specially with all the interactivity around dragging elements.
  - Google sheets has always been canvas. 
  - Anything that can be potentially huge and full of data (1000s of nodes) should be run thru canvas not DOM!
  - imagine how much worse it would be on the DOM. It's unimaginably expensive to render hundreds or even thousands of Dom nodes with event listeners to represent huge tables. Virtualisation doesn't compare to the perf of not having em at all.
  - virtualized scrolling is laggy if fast. 
  - canvas: no cost of removing/adding Dom nodes.
  - render low level pixel graphics at the speed of the user, like an endless scroller game.
  - dom wasn't designed for these things, canvas makes perf trivial. 

- ## Just been looking at iCloud.com’s new web Notes app. Turns out the text editing is done in WebGL._202002
- https://twitter.com/danlucraft/status/1225763866765905922
- I have so many questions
  - Getting my editor layout to play well with the iOS onscreen keyboard HAS been a nightmare (even with the new visualViewport APIs), and I’m still not completely happy with it, so I can see the temptation to just bypass it all and do it in WebGL
- Is this a standard thing in Apple web apps? Why this way? What could they not accomplish in HTML? How do they even convince the onscreen keyboard to open when the canvas is tapped? (The onscreen keyboard is not easy to manipulate or interrogate) Where is text input sent??
  - Oh god it looks like… they create an invisible `contenteditable` div that they update to always contain the text of the line you are working on, and that has the focus and is where text input is sent.
  - This looks like a similar method to what the Google Docs suite uses. **Sheets is rendered in a canvas, Docs in regular HTML, and Slides in SVG** , or at least they were when I last checked.
  - That’s kind of how pdfjs works for viewing PDFs on the web - draw a picture in a canvas of what the text should really look like and then put invisible divs behind it so you can select it.
  - All modern editors work like this — CKEditor 5, Quill, prosemirror, slateJS - internal model, contenteditable just for input
  - I have had my fair share of struggles with WebGL text
- See also: Lucidchart. My guess is they did this for the web versions of Pages/Keynote/etc and then reused it for notes. Font rendering is notoriously impossible to match pixel-for-pixel across browsers, so rolling your own is the only option. That’s why Lucid did it, at least.
  - I would guess that they maybe wouldn’t have done this in Notes if it hadn’t already been done for Pages, a note taking app probably doesn’t need pixel/perfect rendering across browsers or advanced layout (e.g. 3D transforms, etc)
- Lucidchart uses canvas for most stuff as well?
  - The shape canvas (shapes, lines, text, etc) is webgl, all the chrome is Angular.
  - And worth noting that while they did roll their own text editing, it was an endless source of bugs and UI/keybinding inconsistencies across OSes. Definitely not for the faint of heart.
