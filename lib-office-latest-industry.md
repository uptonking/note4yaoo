---
title: lib-office-latest-industry
tags: [documentation, latest, office]
created: '2021-05-13T02:38:54.706Z'
modified: '2021-05-14T18:47:24.054Z'
---

# lib-office-latest-industry

# guide

- ## [Google Docs will now use canvas based rendering: this may impact some Chrome extensions](https://workspaceupdates.googleblog.com/2021/05/Google-Docs-Canvas-Based-Rendering-Update.html)
- We’re updating the way Google Docs renders documents. 
  - we’ll be migrating the underlying technical implementation of Docs from the current `HTML-based` rendering approach to a `canvas-based` approach 
  - to improve performance and improve consistency in how content appears across different platforms. 

- ## Just been looking at iCloud.com’s new web Notes app. Turns out the text editing is done in WebGL._202002
- https://twitter.com/danlucraft/status/1225763866765905922
- I have so many questions
  - Getting my editor layout to play well with the iOS onscreen keyboard HAS been a nightmare (even with the new visualViewport APIs), and I’m still not completely happy with it, so I can see the temptation to just bypass it all and do it in WebGL
- Is this a standard thing in Apple web apps? Why this way? What could they not accomplish in HTML? How do they even convince the onscreen keyboard to open when the canvas is tapped? (The onscreen keyboard is not easy to manipulate or interrogate) Where is text input sent??
  - Oh god it looks like… they create an invisible `contenteditable` div that they update to always contain the text of the line you are working on, and that has the focus and is where text input is sent.
  - This looks like a similar method to what the Google Docs suite uses. **Sheets is rendered in a canvas, Docs in regular HTML, and Slides in SVG**, or at least they were when I last checked.
  - That’s kind of how pdfjs works for viewing PDFs on the web - draw a picture in a canvas of what the text should really look like and then put invisible divs behind it so you can select it.
  - All modern editors work like this — CKEditor 5, Quill, prosemirror, slateJS - internal model, contenteditable just for input
  - I have had my fair share of struggles with WebGL text
- See also: Lucidchart. My guess is they did this for the web versions of Pages/Keynote/etc and then reused it for notes. Font rendering is notoriously impossible to match pixel-for-pixel across browsers, so rolling your own is the only option. That’s why Lucid did it, at least.
  - I would guess that they maybe wouldn’t have done this in Notes if it hadn’t already been done for Pages, a note taking app probably doesn’t need pixel/perfect rendering across browsers or advanced layout (e.g. 3D transforms, etc)
- Lucidchart uses canvas for most stuff as well?
  - The shape canvas (shapes, lines, text, etc) is webgl, all the chrome is Angular.
  - And worth noting that while they did roll their own text editing, it was an endless source of bugs and UI/keybinding inconsistencies across OSes. Definitely not for the faint of heart.

- ## MathJax Turns 3.0
- https://news.ycombinator.com/item?id=22582343
- MathJax 3 is about twice as fast as MathJax 2, but still slower than KaTeX.
- One relatively clear thing is that MathJax supports more features
- One thing I remember reading is that MathJax takes a fundamentally different approach, and that a lot of the time it spends is in measuring things on the page to get things exactly right, while KaTeX is looser about things. 
- Both MathJax and KaTeX support server-side rendering, and the speed differences vanish(消失) (for the reader at least) when nothing is being done client-side.

- [Switching From MathJax to KaTeX](https://www.xaprb.com/blog/switching-mathjax-katex)
  - MathJax is sophisticated(复杂巧妙的，先进的；水平高的), but it’s large and has a lot of dependencies. It’s not slow, but KaTeX is a lightweight drop-in replacement that’s even faster.
  - MathJax is simple to install with a one-line `<script>` tag
  - KaTeX is slightly more involved. js, css, setup
# discuss-stars
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
# discuss
- ## 

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

- ## Google Docs will now use canvas based rendering
- https://news.ycombinator.com/item?id=27129858
- canvas comes with very real trade offs though:
  - Cost of implementation and maintenance is much higher with canvas. This is particularly the case with WebGL, there have been very few contributions to xterm.js (the terminal frontend component) in the WebGL renderer because of the knowledge required. 
  - Accessibility needs to be implemented from scratch using a parallel DOM structure that only gets exposed to the screen reader. Supporting screen readers will probably also negate the benefits of using canvas to begin with since you need to maintain the DOM structure anyway.
  - Plugins/extensibility for webapps are still very possible but requires extra thinking and explicit APIs For xterm.js we're hoping to allow decorating cells in the terminal by giving embedders DOM elements that are managed/positioned by the library.
- More recently I built an extension for VS Code called Luna Paint which is an image editor built on WebGL, taking the lessons I learned from working on the terminal canvas renderer to make a surprisingly capable image editor embedded in a VS Code webview.

- A good open-source example of this type of problem is CodeMirror (a code-editing widget for the web). 
  - To achieve syntax highlighting and everything else, it basically fakes every single aspect of text editing in a browser context - even the cursor and text highlighting - replacing the native versions with pixel-placed DOM elements driven by JS. 
  - It receives raw events from an invisible textarea and does everything else itself.
  - This is just about the worst possible use-case for the DOM: you get almost none of the benefits, and still get most of the costs.

- ## Google docs is apparently moving to a canvas based editor. 
- https://twitter.com/devongovett/status/1392597989768585218
  - This is horrible for accessibility and a great example of what *not* to do. 
  - I’m surprised no one flagged this
  - [google docs canvas preview](https://docs.google.com/document/d/1N1XaAI4ZlCUHNWJBXJUBFjxSTlsD5XctCz6LB3Calcg/preview)
  - [Google Docs will now use canvas based rendering](https://news.ycombinator.com/item?id=27129858)
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

# pdf
- [Announcing react-pdf v2.0](https://react-pdf.org/blog/announcing-react-pdf-v2)
- Motivation
  - Separate Layout from Rendering
  - Embracing Immutability
  - Boost
  - Better Testing
- Solution
  - Redefining Rendering Process
  - Functional Approach
- What's New
  - SVG Support
  - New Hook API
  - More styles
