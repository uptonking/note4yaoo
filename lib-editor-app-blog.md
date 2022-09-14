---
title: lib-editor-app-blog
tags: [blog, editor]
created: 2021-05-13T04:44:23.155Z
modified: 2022-08-21T10:11:37.453Z
---

# lib-editor-app-blog

# guide
- tldr: Unless browsers will open for the Web multiple crucial features (such as IME, keyboard, selection, touch, on-screen keyboard, spellchecker, etc.) contentEditable is the only sane way to handle text editing.

- contenteditable gives you one very important feature that you can't fake yourself: access to the browser's spell check and corrections
- Yep, we do use contentEditable as an input source and also as the view to which we render (you wouldn't be able to reliably handle the keyboard otherwise).
# repeat

## [ContentEditable  —  The Good, the Bad and the Ugly_201508](https://ckeditor.com/blog/ContentEditable-The-Good-the-Bad-and-the-Ugly/)

- ### ContentEditable is evil and the Selection API is its evil twin. Avoid them as much as possible. 
- You need a custom selection system. 
  - It must be doable nowadays to get position (represented by a range, but we’ll simplify this in a moment) in the DOM on mousedown/mousemove. 
  - You’ll display your custom caret (whoa… you can control its style now) and text selection (it’s a simple ).
- You need to handle typing. 
  - Let’s listen to the keyboard events and insert given character into the editor.
- You need to handle navigation using the Arrow keys. 
  - Left and right seem easy, up and down a bit trickier but if you have point 1, you’ll do this too. 
  - Wait, there’s the Alt modifier which makes the Left and Right Arrow keys jump entire words. 
  - But of course you’ll look for spaces in the text and that’s it — told you, it’s trivial!
- Then you need to do something with pasting. 
  - You see that with the Clipboard API you can listen to the paste event on the document and retrieve the data from the data transfer. 
  - You can also use the old paste bin mechanism.

- ### ContentEditable — the Good Parts
- It’s amazing that adding one attribute to an HTML element enables typing, selection, keyboard navigation, spell checking, drag and drop, pasting, undo manager. 
  - That all of this is integrated with the OS, 
  - that such editor can be used with a screen reader or on a touchscreen device 
  - and that it’s well internationalised. 

- ### CKEditor
- Over the past years, while working on CKEditor I noticed that we were gradually replacing native features with our own implementations. 
- Since version 4.0, CKEditor has its custom “insert HTML into selection” mechanism and a feature allowing reaching non-editable places.
- CKEditor 4.1 introduced highly customisable content filtering (no more mess on paste). 
- CKEditor 4.3 brought support for non-editable islands with editable islands inside which required overriding many native systems (selection, keyboard, focus, clipboard).
- Finally, just a few weeks ago we made a final takeover of the clipboard, which means that in some browsers copy, cut and paste operations are fully handled by CKEditor.
- It means that today CKEditor does not let the browser do anything to the content except handling typing, some deleting and that’s basically it. 
  - At the same time, it still uses the native selection system, keyboard navigation and other APIs such as those related to clipboard or focus management.

- With CKEditor 5 we are planning to conclude this process by letting the browser insert text only, but with CKEditor’s control.
# blogging

## [最近迷上了富文本编辑器！_202111](https://juejin.cn/post/7027040695827300360)

- 于是想起了咱们的国产之光，wangeditor ，因为他们的功能类似，原理指定也类似，区别的地方其实就是设计思路的一些差别
- 在开始wangeditor 的心路历程之前，我们先要明确一定，富文本编辑器之所以可以编辑，其实是得益于 HTML contenteditable 属性 正是由于有了它我们才能实现在标签里面编辑内容。这是实现一个富文本的根本
- wangeditor 从第三个版本开始我基本也都看过，见证了他一步步的从一js到ts 的重构、从重视拓展性到到面向对象再到现在社区流行的函数式、从必须兼容ie到抛弃兼容ie 、从传统的webpack 的工程化构建到 rollup +monorepo的工程化构建
- 刚开始读v4的时候最最高兴的就是他每个方法都有注释, 至少咱知道从哪里入手，然后就是经典的面向对象设计。
  - 整体的设计架构就是利用面向对象的思想，将一个个的功能对象，组合成富文本的功能，主要实现以下功能对象
- 最近在拜读v5的源码，还还整理规划了v5的执行流程的思维导图，当然还没整理完毕
  - v5在slate他提供内核的基础上去自己实现view 的渲染
  - 从v4到v5 能明显的感觉到函数成了一等公民，这也与像vue3这类优秀的开源项目不谋而合。通过不同函数的组合，减少项目中由于引用类型带来的副作用
- 我主要想说的是为什么v5为什么要使用vdom？
  - 在v4 中主要就是利用MutationObserver 去监听dom树的改变，从而触发编辑器的功能
  - 整个v4是有自己的一套渲染规则，并且没有模型整个概念，他的所有的操作都是深深的绑定在当前这个富文本中，无法抽离
  - 而由于v5是基于slate， 所有完美的继承了slate 优点，将模型和视图分离，就可以随意的选用选用现有的效率比较高的view 渲染器去做视图的渲染，在v5中就是用了和vue2同款的snbbdom
- 我觉得（有可能不对）v5中之所以使用snbbdom 的原因有两点
  - 基于slate， 能拿到Slate 的数据模型 ，用最小的成本利用现有渲染器去渲染dom, 并且能通过操作menu等功能修改vdome从而渲染视图
  - 模型视图分离是一个趋势，也是一个更高的抽象思想，能让代码的架构更加清晰，便于理解
- **beforeinput**表示可编辑的dom在被修改前触发
- 为什么要弃用MutationObserver而选用beforeinput ？
  - 早期页面并没有提供对监听的支持，所以那时要观察 DOM 是否变化，唯一能做的就是轮询检测，比如使用 setTimeout 或者 setInterval 来定时检测 DOM 是否有改变。
  - 直到 2000 年的时候引入了 Mutation Event，Mutation Event 采用了观察者的设计模式，当 DOM 有变动时就会立刻触发相应的事件，这种方式属于同步回调。
  - 这种实时性造成了严重的性能问题，因为每次 DOM 变动，渲染引擎都会去调用 JavaScript，这样会产生较大的性能开销。
  - 从 DOM4 开始，推荐使用 MutationObserver 来代替 Mutation Event。MutationObserver API 可以用来监视 DOM 的变化，包括属性的变化、节点的增减、内容的变化等。
- 我觉得（可能有错）有两点原因：
  - MutationObserver虽然很优秀，但是他的监听如果数据发生变化还需要比较，拿不到最新的变化值，并且还会产生很多无用的节点，不适合slate 的体系
  - 主动操作menu修改样式等无需监听，直接更改slate 的数据模型即可
  - beforeinput 他除了能拿到当前改变的值，还能通过inputType知道当前输入的类型
  - 监听到输入之前的事件之后，就能根据不听的类型调用不同的slate 的api 改变slate 的内部数据模型，在触发回调函数，触发path 渲染dom

## [在线协作软件的三个核心引擎](https://juejin.cn/post/7002595221103968293)

- 优秀的协作软件必然由三个核心引擎构建：渲染引擎，协同引擎以及数据引擎
- 渲染引擎
  - 富文本编辑器
  - 表格编辑器
  - ppt/mind-map：图形编辑器
  - bi：布局设计器 + 图标设计器
- 协同引擎
  - 即时性、一致性、健壮性
  - 协同引擎存在的目的，本质就是保持各个终端在展示同一个内容模型时，能够在单个操作消费到模型之后，模型保持一致
  - 阶段1 - 客户端发送操作，
    - 操作等待同步给Server(其他协作者) pendingCommmands
    - 操作同步给Server（其他协作者） sendingCommands
    - 操作已同步给Server（其他协作者） sentCommmands
  - 阶段2 - 客户端模型消费操作
    - 操作作用于Model之后，客户端的Model应当与服务端的Model保持一致
- 数据引擎
  - Word - openxml的设计
  - Etherpad - 采用字符串 Z:1>6b|5+6b$Welcome to Etherpad!
  - Google Docs Word - 采用一个commands集合的设计
  - Google Docs Spread - 设计比较像Excel，但是使用的protobuf
  - Notion - 很明显是结构化的属性数据，并且使用CRDT的冲突解决数据结构
- 在Startup阶段，找到对应领域的合适技术选型，选择做出你协作软件的MVP，当自研能够成为你的壁垒或者优势，再选择自研
# editor-ide

## [LSP-language-server-protocol规范学习](https://zhuanlan.zhihu.com/p/343218679)

- LSP(Language Server Protocol) 语言服务协议，该协议定义了在编辑器或IDE与语言服务器之间使用的协议，该语言服务器提供了例如自动补全，转到定义，查找所有引用等的功能；语言服务器索引格式的目标是支持在开发工具中进行丰富的代码导航或者一个无需本地源码副本的WebUI。

- 每个开发IDE，都要为语言实现类如自动补全，转动定义，悬停在单词上提供文档的功能，传统上，需要个IDE根据自己的API实现上述工作，即使是相同的功能，也要根据不同IDE实现一遍重复的功能，代码却不同。
- LSP设计的目标是使该语言服务器和开发工具进行标准化的通信，这个语言服务可以在多个开发工具中重复使用，从而以最小的改动支持多种语言。语言服务器后端可以用PHP，Python或Java编写，LSP可以轻松地将其集成到各种工具中，该协议提供通用抽象级别的协议，以便工具可以提供丰富的语言服务，从而无需完全理解特定于底层域模型的细微差别。

- 语言服务器会作为单独的进程运行，同时开发工具使用基于JSON-RPC的语言协议与服务器进行通信。
  - 用户在IDE中打开文件时: IDE会通知语言服务器文件已打开(textDocument/didOpen)，此时文档的内容不会存在于真实的文件系统中，而是保存在IDE内存中。必须在IDE和语言服务器之间同步内容。
  - 用户编辑文件时：IDE会通知语言服务器文件更新(textDocument/didChange)，并且语言服务器会更新文件的语言表示。之后语言服务器会分析此消息，并将检测到的错误和警告，响应(textDocument/publishDiagnostics)通知IDE。
  - 用户执行"Goto Definition" 指令时: IDE发送带有参数的请求(textDocument/definition), params: {documentURI, position} 到语言服务器，语言服务器以文档URI和definition的Location作为响应。
  - 上述示例说明了协议如何在文档引用（URI）和文档位置级别与语言服务器进行通信。这些数据类型与编程语言无关，适用于所有编程语言。
- 当用户使用不同的语言时，IDE会为每种编程语言启动语言服务器
  - 并不是每种语言服务器都可以支持协议定义的所有功能，因此LSP提供了capabilities，一个capabilities可以将一组语言capability组合在一起，IDE和语言服务器使用能力宣布其支持的功能。
  - 需要注意：语言服务器到特定IDE的实现集成不是由语言服务器协议定义的，而是由IDE实现者决定

### [如何评价微软的 Language Server Protocol？](https://www.zhihu.com/question/50218554)

- 我只有一个问题， 这玩意会上传代码到服务器么？
  - 服务器就在你本地。。。懂了没？？只是和编辑器分开了，通过通信来交流
  - 网络传输会让你的ide跑的慢死 目前的都是本地服务器也就是个跨进程通讯而已
# more
- [Text Rendering Hates You](https://gankra.github.io/blah/text-hates-you/)
- [TEXT EDITING HATES YOU TOO](https://lord.io/text-editing-hates-you-too/)

- [为什么 ContentEditable 很恐怖](https://www.oschina.net/translate/why-contenteditable-is-terrible)

- [Slate.js - 革命性的富文本编辑框架](https://s1973.top/blog/0015499011852838c3eb8e0d6d14a3f97bee6e61fa1cd26000)

- [富文本编辑器的技术演进之路_UC-Hugo.js_201908](https://developer.aliyun.com/article/712971)

- [How we use WebAssembly at Fiberplane_202205](https://fiberplane.dev/blog/how-we-use-webassembly-at-fiberplane/)
- [Creating a Rich Text Editor using Rust and React_202204](https://fiberplane.dev/blog/creating-a-rich-text-editor-using-rust-and-react/)
  - We used to use Slate.js — a fine editor — but as we’re implementing our own rich text primitives for collaborative editing, we discovered the disconnect between our own primitives and Slate’s data model to be somewhat of a hindrance. So we got to thinking - what if we just built our own Rich Text Editor (RTE)?
  - From a very high-level perspective, a rich text editor is comprised of two components:
  - A data model and the core logic to operate on it.
  - A view that renders the state of said data model and that handles the user interactions.

- [Text Rendering Hates You](https://gankra.github.io/blah/text-hates-you/)
