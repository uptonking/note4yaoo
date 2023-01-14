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
- [[方案]造一个富文本 简介](http://luo0412.gitee.io/core/nav.4-2.ui/ch5-toolbox/02-5047253998648002.html)

- [哔哩哔哩 从零开始的富文本编辑器（上）_slate_202209](https://www.bilibili.com/read/cv18606877)
  - [哔哩哔哩 从零开始的富文本编辑器（下） - 列表-图片_slate_202210](https://www.bilibili.com/read/cv19147722)

## [CKEditor 5 - comparing Revision History with Track Changes](https://ckeditor.com/blog/ckeditor-5-comparing-revision-history-with-track-changes/)

- These two features of CKEditor 5 include Revision History and Track Changes, also known as Suggestion Mode.
- Both Track Changes and Revision History are premium plugins and features within CKEditor 5
- Track Changes is the ability to work collaboratively with others, not necessarily in real time, by seeing the suggestions they made to a document and being able to accept or reject them.
- Revision History revolves around the ability for users to analyze earlier versions of a document, compare them with one another and revert to a chosen version if desired.
  - Writers will need to periodically save states, or versions of their document, so that they show up on the chronological list 

- they are used at different stages of a document editing workflow. 
  - Track Changes enables users to apply suggestions that need to be reviewed by another user. This mode suggests what could be changed in the future; 
  - Revision History looks at what was already changed in the past. However, it may also include suggestions that haven’t been accepted yet within the revisions, if both features are enabled simultaneously.

- Revision History, on the other hand, focuses on providing users with three additional and key functionalities that Track Changes does not have. 
  - creating snapshots (revisions) of content, where such a snapshot is the state of the content at the time the user makes a save
  - comparing individual revisions with each other
  - restoring individual revisions

- In summary, Track Changes is more of a functionality improving the aspect of collaboration between users, 
  - while Revision History extends the application’s capabilities with content audit-trail and versioning functionality.

## [从流行的编辑器架构聊聊富文本编辑器的困境_202003](http://yoyoyohamapi.me/2020/03/01/%E4%BB%8E%E6%B5%81%E8%A1%8C%E7%9A%84%E7%BC%96%E8%BE%91%E5%99%A8%E6%9E%B6%E6%9E%84%E8%81%8A%E8%81%8A%E5%AF%8C%E6%96%87%E6%9C%AC%E7%BC%96%E8%BE%91%E5%99%A8%E7%9A%84%E5%9B%B0%E5%A2%83/)

- 几年前，Medium Editor 的开发者写过一篇著名的博文：Why ContentEditable is Terrible?，当中列举了一些 contenteditable 存在的一些问题：
- 视觉内容（用户所见）与实际内容（DOM）的一对多关系
  - 将编辑行为都托管给了浏览器，那么在不同的 DOM 结构下，执行相同的操作，浏览器要能够输出一样的视觉内容。
- 视觉选区与实际选区的多对多关系
  - 一个视觉选区可能映射为多种 DOM 选区，而一个 DOM 选区也可能映射为多个视觉选区

- Why ContentEditable is Terrible? 还有一个副标题： How Medium Editor Works?，它不仅仅描述了 contenteditable 存在的缺陷，还以此为引，阐述了 Medium Editor 的工作机制。
  - 近年来社区活跃度颇高的 Slate.js，Draft.js 、ProseMirror 以及 CKEditor 等也使用了类似的机制，来规避 contenteditable 缺陷，
- 这个机制可以被简单描述为：
- 模型与视图相分离
  - 让编辑器决定数据结构（内容 + 选区），保证视觉与实际一致
  - 方便同样的内容在不同设备设备展示
- 自定义命令
  - 脱离实现不一的浏览器命令（document.execCommand），自行划定编辑器的操作范围
- 这种机制最小程度使用了 contenteditable —— 仅仅让一个节点的 HTML 内容允许被编辑，而如何编辑，编辑器结果则收敛到了编辑器治理

- 防患未然：基于行为的同步策略
- 编辑器使用了视图模型相分离的架构，就需要处理视图与模型间的同步，当用户在编辑器完成了操作后，编辑器据此更新数据模型，再通过数据模型渲染出新的页面视图即对视图
- 编辑器是如何知道用户执行了哪个操作呢？答案就是 DOM 事件，假设监听到了 keyCode = 8 的 keydown 事件（Event），就推测用户是在执行退格（Intent），从而调用自定义的删除指令（Command），修改数据模型，最终用户看到光标前的字符被成功删除了。
- 基于事件拦截的数据同步，是理想型的同步链路，先更新模型，再渲染视图，由于模型和视图一一对应的关系，用户执行了相同的操作，总能获得一致的 DOM 结构，
- 然而，由于 DOM Event 的规范仍然在发展，各个浏览器对其的实现也不尽相同，因此，基于事件拦截的同步也不完全可靠。
- 举个例子来说，beforeinput event 是非常有用的一个事件，该事件在 Input Events Level 1 被定义，并在 Input Events Level 2 中获得完善，规范希望能帮助类似 Web 富文本编辑器这样的应用更容易地处理用户输入。
- beforeinput event 能让开发者在输入反馈到 UI 之前，通过事件的 inputType 属性知悉用户输入意图（例如，当 inputType 是 deleteContentBackward 时，我们就知道用户正在向前删除内容）， 但尴尬的是：
  - 要么浏览器不支持这个事件
  - 要么部分支持这个事件：例如覆盖到的 input type 不全
- 因此，DOM Event 本身的不完美，也就让编辑器难以完全摸清用户意图。
- 而对用户意图的模糊，也会造成：
  - 无法理解 ：编辑器忽略了某个用户操作
  - 理解错误 ：将用户的操作理解为了另一个操作，例如用户是在输入，但被编辑器理解为了删除，造成数据模型发生非预期变更，用户看到错误的视图
- 因此，基于事件的同步模型也是一个理想型模型，受限于浏览器支持，在实际应用中并不完全可靠。

- 亦敌亦友：输入法
- 输入法本身又不受控于编辑器，它完全由第三方厂商实现，其实现也只和操作系统有关
- 输入法和操作系统交互来合成文本，浏览器也通过操作系统，获得输入法状态，在输入过程中抛出对应事件。
- 输入法繁多 ：不同的操作系统版本、浏览器内核，和输入法能形成众多的组合，每种组合在 contenteditable 元素上进行文本合成的时候，难以形成一致的事件流
- 输入方式多样 ：除了键盘能够进行文本合成，还要支持手写、语音等输入方式
- Android 因为其生态紊乱，系统版本分布广泛，使用不同内核的浏览器众多，应用市场的第三方输入法层出不穷，让基于事件进行同步的策略更加脆弱。
- 在 Android 下使用某个第三方浏览器配合上某个第三方输入法编写内容时，可能遇到：
  - 浏览器不会抛出 beforeinput 事件 ：编辑器无法通过 beforeinput 事件中的 inputType 属性知悉用户行为
  - 浏览器没有传递正确的虚拟键盘响应 ：很多 Android 输入法都支持字词联想，当虚拟键盘呼出后，开始进入 Composing 状态，此时 keydown 事件的 keyCode 都会被设置为 229，那么编辑器无法也无法从 keydown 事件知悉用户行为
- 这就会造成比较恶性的现象，举个例子，当用户将光标放置在图片之后时，输入法被唤起，用户通过虚拟键盘按下了退格键希望能够删除图片。但由于编辑器既无法拦截 beforeinput 事件来判断用户是不是在执行删除，也无法通过 keydown 事件判断判断键盘的退格是否被按下，因此，也就不会生成对应的命令去修改数据模型，删除对应节点。此时，用户无论怎么疯狂点按退格，都不能把图片删掉。
- 因此，基于事件的同步策略，在面对输入法时，变得更加不可靠，社区目前流行的开源编辑器也仍在和 Android 输入法作斗争

- 亡羊补牢：基于现象的同步策略
- 编辑器之所以希冀于事件去同步数据模型和视图，是期望在浏览器对页面执行变更前，尽早将用户行为同步到数据模型上，实现实际内容与视觉内容的统一。但我们发现，这个本就不健壮的策略再遇到输入法之后，无法响应用户操作的概率更高了。
- 如果回到架构之前，仍然托管 contenteditable 的控制权给浏览器，那么，我们发现，输入法的增删改查还是能正确响应的，这也就说明了，托管给浏览器去处理 contenteditable，用户最基本的编辑诉求还是可以保障的。
- 当浏览器处理了用户的行为并更新了视图后，我们要尽快的去 “纠正” 数据模型，亡羊补牢，犹未为晚。
- 浏览器提供了 Mutation Observer 来让开发者监听 DOM 变更，它的 API 非常简单，初始化观察者之后，在适当时机开始观察即可，每次观察到的变更序列，其中的元素都是 MutationRecord 对象
- 借助于 Mutation Observer，编辑器在观察到 DOM 变化后，可以根据变化（现象）来反推用户行为，从而生成对应的命令，去修缮数据模型
- 这种 事后同步 ，弥补了浏览器无法派发正确事件时，我们仍能推测用户行为 —— 通过现象去反推用户行为。但是，由于现象的成因可能有多个，因此我们就可能造成错误的推断
- 我们的是人肉学习，为了获得更多特征，去更精确的映射用户行为，开发者将疲于应付不同的 Android 设备，不同的浏览器，以及不同的输入法形成的种种组合。
- 综上，基于现象去同步数据模型，是更不牢靠的手段， 即便开发者投入了大量精力去获得现象和意图间的关联关系，但难免还是有 “漏网之鱼”，导致模型 同步错误 ，这也许比不能响应操作更加严重。
- 而基于事件的同步模型，因为事件本身就表达了用户意图，所以推测会更加精准，所以，只有当事件系统不完善时（例如在 Android 设备下），我们才使用基于现象的同步做兜底，保证用户在编辑器能进行最基本的输入。

- DOM 的虚实调和
- 现代化的前端开发中，已经很少使用真实 DOM 来表达一个组件了，如果选用了类似 React 这样的解决方案去描述实现编辑器视图（Slate.js、Draft.js 就倾向于此），就会让视图的表达 “虚实并存”
- 在 Android 设备上，为了解决输入法问题，编辑器将输入先托管给浏览器，并 Mutation Observer 观察 DOM 变化，而后再去同步数据模型。在这样的策略下，用户的输入过程在没有结束之前，都是浏览器在处理，当中发生许许多多的变更，不再受 React 控制，很容易造成 “虚实不调”，引起编辑器崩溃。
- 因此，当使用了类似 React 这样的方案之后，编辑器需要更加 谨小慎微地 处理数据同步，在容易引起虚实不调的场合（例如段落分裂与合并），强刷（rerender）编辑器组件，调和虚实，让 DOM 与 VDOM 保持一致。
  - 而对于预料不到的场合，可能还需要借助 componentDidCatch 这样的 hook 去俘获异常，强刷组件。
  - 有 React 开发经验的同学都知道，对于编辑器这样内部子孙繁多的组件，重绘的开销是非常的，最终，在终端用户一侧，就是看到页面闪烁和卡顿。

- 上文对 Web 富文本编辑器困局的讨论，还仅仅局限单机版的富文本编辑器，如果还要为编辑器支持多人实时协同，那么面对的挑战更加艰巨。
- 面对这样的生态，做不到抛弃，编辑器只能去适应和妥协，但在其领域范围内，似乎还可以有一些突破：
  - 是否能通过交互绕开缺陷？
  - 是否能脱离 contenteditable 的架构？

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
- [编辑器背后的数据结构 | Tuesday.](https://dontpanic.blog/data-structures-under-editors/)
  - 部分Emacs使用了Gap Buffer，包括古老的 Emacs on TECO、现代的GNU/Emacs及其前辈Gosling Emacs。
  - Scintilla (即包括Code:: Blocks在内的很多IDE/编辑器使用的代码编辑控件) 也使用了Gap Buffer
  - Emacs进入由Lisp实现的时代后，一些Emacs版本使用了LinkedLine。
  - Vim使用的是一种基于行的数据结构，但行与行之间不是简单地使用链表连接，而是用一种树结构进行管理。
  - KDE的Okteta 16进制编辑器使用了Piece Table Buffer

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

- [Over 14 years of todos recorded in text: My productivity app is a never-ending .txt file](https://jeffhuang.com/productivity_text_file/)

- [前端富文本基础及实现, 偏综述，基于contenteditable+document.execCommand](https://juejin.cn/post/7124839474575441934)

- [WebAssembly 在在线文档分词场景中的解决方案](https://github.com/YingshanDeng/wasm-cppjieba/issues/1)

- [VS Code、ATOM这些开源文本编辑器的代码实现中有哪些奇技淫巧？ - 知乎](https://www.zhihu.com/question/272156541/answers/updated)
