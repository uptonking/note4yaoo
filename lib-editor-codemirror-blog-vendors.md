---
title: lib-editor-codemirror-blog-vendors
tags: [blog, codemirror, vendors]
created: 2024-05-17T16:08:34.520Z
modified: 2024-05-17T16:08:45.674Z
---

# lib-editor-codemirror-blog-vendors

# guide

# blogs-replit

## [Replit — Building LLMs for Code Repair _202404](https://blog.replit.com/code-repair)

- At Replit, we are rethinking the developer experience with AI as a first-class citizen of the development environment.
  - we are tightly integrating AI tools with our IDE.
- Currently, LLMs specialized for programming are trained with a mixture of source code and relevant natural languages, such as GitHub issues and StackExchange posts. 
  - These models are not trained to interact directly with the development environment and, therefore, have limited ability to understand events or use tools within Replit. 
  - We believe that by training models native to Replit, we can create more powerful AI tools for developers.
- A simple example of a Replit-native model takes a session event as input and returns a well-defined response.
- In 2018, when Microsoft released “A Common Protocol for Languages, ” Replit began supporting the Language Server Protocol. Since then, the LSP has helped millions using Replit to find errors in their code. This puts LSP diagnostics among our most common events, with hundreds of millions per day. However, while the LSP identifies errors, it can only provide fixes in limited cases. 
- Data sources: OTs, events, and Repl snapshots
  - A Replit session is a stream of data across multiple modalities. 
  - To support multiplayer features, Replit represents code as a sequence of Operational Transformations (OTs). 
  - This representation provides an edit-by-edit history of all the changes made to a file and allows us to “play back” a project’s state. 
  - A regular snapshot of each project’s most recent state allows us to assert the replay’s correctness.
  - Users can replay a project in Replit’s workspace.
  - OT data is merged with session events into a single timeline. Here, we work with LSP diagnostics, but many other events are recorded, including CodeMirror actions (selection, scrolling), package installation, code execution, and shell commands. 
- The goal of our data pipeline is to produce a dataset of (code, diagnostic) pairs. We first recreate the filesystem of a project at the time of the diagnostic, then use LLMs to generate and verify synthetic diffs.

- We synthesize diffs using large pre-trained code LLMs with a few-shot prompt pipeline implemented with DSPy.
  - We chose numbered Line Diffs as our target format based on (1) the finding in OctoPack that Line Diff formatting leads to higher 0-shot fix performance and (2) our latency requirement that the generated sequence should be as short as possible. We compared Line Diffs with the Unified Diff format and found that line numbers were hallucinated in the Unified Diff both with and without line numbers in the input. Furthermore, Unified Diffs would have a higher decoding cost.

- Base model
  - We finetuned starting from an open-weights 7B model trained on code. We chose the model size of 7B to balance model capabilities with our constraints of inference latency and cost. We experimented with base and instruction-tuned models from the Starcoder2 and DeepSeek-Coder families and ultimately settled on DeepSeek-Coder-Instruct-v1.5 based on performance.

## [Replit — Betting on CodeMirror _202203](https://blog.replit.com/codemirror)

- Monaco did not support mobile, which was becoming increasingly important for us to achieve our goal of making programming more accessible.
  - Overall, we’re excited to be placing such a huge bet on the next generation of online code editors and continuing to advance the future of writing software on the web. 

- [Ace, CodeMirror, and Monaco: A Comparison of the Code Editors You Use in the Browser __202112](https://blog.replit.com/code-editors)
- [Replit — A New Code Editor for Mobile - CodeMirror 6 _202109](https://blog.replit.com/codemirror-mobile)
# blogs-vendors

## 🆚️💡 [编辑器探索 - 带你全面了解 Web Editor 架构设计、技术选型 _202309](https://rapidsu.cn/articles/4239)

- 目前开源市场使用较多的编辑器主要有 3 个，分别是 Monaco Editor、Ace 和 Code Mirror(主要指Code Mirror6)。

- Monaco
  - 是一个功能相对比较完整的代码编辑器，实现使用了 MVP 架构，采用了模块化和组件化的思想，
  - 其中编辑器核心代码部分是与 vscode 共用的，从源码目录中能看到有很多 browser 与 common 的目录区分。
  - 使用 MVP （Model View Presenter）架构，分别表示数据层、视图层、发布层。在MVP中View并不直接使用Model，它们之间的通信是通过Presenter (MVC中的Controller)来进行的，所有的交互都发生在Presenter内部。
  - 采用面向对象思想编程
  - 依赖注入，自研实现依赖注入能力
  - 多线程处理，主要分为 主线程 和 语言服务线程（使用了 Web Worker 技术 来模拟多线程，主要通过 postMessage 来进行消息传递）
  - 主线程：主要负责处理用户与编辑器的交互操作，以及渲染编辑器的 UI 界面，还负责管理编辑器的生命周期和资源，例如创建和销毁编辑器实例、加载和卸载语言服务、加载和卸载扩展等。
  - 语言服务线程：负责提供代码分析、语法检查等功能，以及处理与特定语言相关的操作。
  - 基于 textarea 实现输入效果，通过 css 隐藏了默认 textarea 的样式。
  - 光标的交互与样式，通过代码模拟，尤其是多光标的实现，只有其中一个光标下面才放置了 textarea 组件，其它都只是模拟了光标样式。
  - 渲染每一行内容，通过增加标签的形式进行关键字高亮。
  - 将代码背景高亮与行背景高亮使用单独的 DOM 区分。
  - 为了方便控制，横向、纵向滚动条均自己实现。

```HTML
<div class="monaco-editor" role="presentation">
  <div class="overflow-guard" role="presentation">
    <div class="monaco-scrollable-element editor-scrollable" role="presentation">
      <!--实现行高亮-->
      <div class="monaco-editor-background" role="presentation"></div>
      <!--实现关键字背景高亮-->
      <div class="view-overlays" role="presentation">
        <div>...</div>
      </div>
      <!--每一行内容-->
      <div class="view-lines" role="presentation">
        <div class="view-line"><span><span class="mtk18">select</span></span></div>
        <div class="view-line">...</div>
      </div>
      <!--光标-->
      <div class="monaco-cursor-layer" role="presentation"></div>
      <!--文本输入框-->
      <textarea class="monaco-editor-textarea"></textarea>
      <!--横向滚动条-->
      <div class="scrollbar horizontal"></div>
      <!--纵向滚动条-->
      <div class="scrollbar vertical"></div>
    </div>
  </div>
</div>
```

- Ace
  - 高性能，体积小。支持了超过120种语言的语法高亮，超过20个不同风格的主题，与 Sublime 等本地编辑器的功能和性能相匹配。
  - 面向对象
  - 事件驱动, Ace 中提供了丰富的事件系统，以供使用者直接使用或者自定义，并且通过对事件的触发和响应来进行内部数据通信实现代码检查，数据更新等等
  - Ace编辑器将解析代码的任务交给 Web Worker 处理，以提高代码解析的速度并避免阻塞用户界面。在 Web Worker中，Ace 使用 Acorn库来解析 JavaScript 代码，并将解析结果发送回主线程进行处理
  - Ace将编辑器的不同功能分离成不同的类，并使用组合的方式将它们组合在一起。使代码更加模块化、易于维护和扩展。从目录结构可见。
  - 整体 DOM 设计与 Monaco 差不多，都是基于 textarea 实现输入效果。
  - 合并了行背景高亮与代码背景高亮的 DOM 设计。

- CodeMirror6
  - 核心思想是模块化和函数式，支持超过 14 种语言的语法高亮，亮点是高性能、可扩展性高以及支持移动端。
  - 使用 MVVM 架构
  - 函数式编程
  - 单线程
  - 同步增量解析的方式提升性能，每次仅解析视口内（viewport）的代码，从而提升解析性能。
  - 基于 `contenteditable` 属性实现编辑富文本的能力，光标、选区和输入等能力由浏览器默认支持。
  - 代码高亮渲染仍然与上面两个编辑器一致，渲染每一行内容，通过增加标签的形式进行关键字高亮。
  - 对于行背景以及选区背景等高亮，仍然采用单独 DOM 绝对定位的方式实现，减少原有代码 DOM 结构的修改，但是合并了代码背景高亮与行高亮的 DOM，看起来更简洁。

- 可以看出 CodeMirror 相比 Monaco Editor 和 Ace 最大的不同就是使用了 contenteditable，那么基于他做了什么呢？
  - 只关心它的选区 (Selection) 状态。
  - 输入文本时，以 nextState = f(selection, input) 理念计算出新状态。
- 整个编辑器就像是一个 React 中的受控组件了。关键的受控行为大概包括这些：
  - 按键输入被拦截，基于 f(selection, input) 计算出新状态
  - 复制粘贴被拦截，基于 f(selection, input) 计算出新状态
  - DOM 更改被拦截，基于 nextState 单向地渲染出 DOM 状态
- 那么，还有哪些地方需要依赖 contenteditable 呢？其实就是和 Selection 强相关的东西：
  - 选区高亮状态依赖 contenteditable，否则你需要自己渲染那个「拖蓝」区域
  - 点击后的选中状态依赖 contenteditable，否则你需要自己计算某个坐标下对应了哪个文字，意味着要自己去解析字体参数做文本排版。
  - 方向键操作后的状态依赖 contentEditable

- 设计亮点
- Monaco Editor
  - 数据结构：Text Buffer 是一个内存中的数据结构，它保存了编辑器中打开的文本文件的内容。当用户在编辑器中添加、删除或修改文本时，Text Buffer 会跟踪这些更改，并在必要时更新文本内容。
    - 使用 Text Buffer 之前的实现 主要使用 Line Array，即按行存储，按行操作。特点是：查询效率快，开发/操作简单，但行数较多时进行数组操作内存消耗极大，容易出现崩溃。
    - Text Buffer 主要思路 使用 Piece Table 数据结构优化存储 
    - Piece Table：是一个用于存储棋谱数据的容器，它可以保存棋局的初始状态、中间状态和最终状态，它可以存储棋谱的每一步操作，包括落子位置、棋子类型等信息。
    - 通过平衡二叉树的方式来提高查找效率。
  - Monarch（词法分析器） 通过一种基于正则匹配的词法解析来实现，主要负责将输入的代码文本转换为一个个标记（token），以便Monaco Editor后续的语法高亮、智能感知等功能能够对代码进行更加精细的处理
- Ace
  - 移动端支持，但它的移动端实现成本小，而且清晰简单，主要是分为了三点，
    - 在移动端减少了部分逻辑，例如一些比较中的代码分析逻辑，代码提示逻辑。
    - 移动端仅重写了菜单部分的 css，其他 css 自动适配就可达到效果
    - 绑定了 touch 相关的事件，这些事件对应 pc 的 mouse 事件，也主要是与菜单相关的事件
  - Ace 编辑器内部组件通信以及响应用户输入都是通过事件系统来进行的，这种通信方式相比与基于数据响应的方式，更加的精准和节省性能，但相应代码量也会更大，维护成本略高。
  - Ace 中实现了一个可复用的触发器机制 EventEmitter 类，，EventEmitter 类是一个基础类，用于实现事件的注册、注销和触发等功能。所有具有事件处理能力的类都继承自 EventEmitter类，包括 Ace 编辑器中的 Editor 类。

- CodeMirror
  - 函数式核心，命令为外壳
  - 指导 CodeMirror 架构设计的核心观点是函数式代码（纯函数），它会创建一个没有副作用的新值，和命令式代码交互更方便。而浏览器 DOM 很明显也是命令式思维，和 CodeMirror 集成的大部分系统类似。
  - CodeMirror 的 state 表现层是严格函数式的 - 即 document 和 state 数据结构都是不可变的，能操作它们的都是纯函数，view 包将它们封装在一个命令式接口中。
  - CodeMirror 处理状态更新的方式受 Redux 启发，除了极少数情况（如组合和拖拽处理），视图的状态完全是由 EditorState 里的 state 属性决定的。
  - Transactions 由 state 的 update 方法产生

- CodeMirror 在包体积方面有绝对的优势

- 总结
  - 主要应用在 PC 端，功能要求多，使用简单，建议选择 Monaco Editor
  - 主要应用在 移动端，功能要求相对简单，要求高扩展性，建议选择 CodeMirror
  - Ace 因为代码设计、UI等比较久远，会比较过时，并且该库后续也不会再进行更新，不建议选择，但若寻求更高的兼容性与稳定性，那它仍然是一个不错的选择。

## 🌰 [overleaf: Towards the future: a new source editor - Overleaf, Online LaTeX Editor _202211](https://www.overleaf.com/blog/towards-the-future-a-new-source-editor)

- As of June 14 2023, the legacy editor has been retired for all users.
- Overleaf now uses CodeMirror 6, a different underlying technology, to power its source editor.
  - Adopting a new source editor is a crucial step in unifying with our Rich Text editor, allowing us to improve both in parallel.

- [We’re retiring our legacy source editor - Overleaf, Online LaTeX Editor _202304](https://www.overleaf.com/blog/were-retiring-our-legacy-source-editor)
  - There are a few key reasons why it’s important for us to move to the new source editor:
  - Improved mobile support – the new editor has superior support for editing on mobile devices, such as phones and tablets.
  - Better accessibility – the new editor will give us the tools to work better with assistive devices (such as screen readers), paving the way to make Overleaf more inclusive.
  - Enhanced Rich Text functionality – the underlying open source library that the new editor uses (CodeMirror 6) is uniquely able to handle both source code and rich text, allowing us to deliver a much improved Rich Text editor. These improvements include the recently introduced rich-text commenting and tracked changes feature.
  - Better support for non-latin text – including mixing of right-to-left and left-to-right text and special characters (such as those with diacritics).
  - Faster development of new features and fewer issues – having multiple editors means any change we make to our platform has to be done multiple times. This slows down new development and creates more places for problems to arise. By moving to the new editor, we can develop features and deploy them once, seriously speeding up the process of delivering the features you want.

## 🎨🆚 [miro: Why we developed a code block widget in Miro using ace editor _202307](https://medium.com/miro-engineering/why-we-developed-a-code-block-widget-in-miro-f6c5ec23085c)

- Our code widget is a code block with a rich editing experience comparable to a native code editor. It has features like syntax highlighting, auto-closing brackets and indentations, various hotkeys, and more.
- Miro boards are heavily based on Canvas API. 
  - Almost everything visible on the board, except for the user interface on top of the board, is essentially a continuously updated and re-rendered image. 
  - Our custom rendering engine consumes HTML with inline styles and draws text by using `canvasContext2D` API.
- Option 1: Reuse existing approach — Quill Editor
  - It is well-integrated in Miro and has a native plugin for syntax highlighting that uses the highlightjs
  - Highlight.js, which Quill uses for syntax highlighting, isn’t the best library available
- Option 2: Use HTML elements and syntax highlighting libraries
  - By using various approaches based on HTML elements like this one using textarea and highlightjs/prismjs, we can make editable code blocks with real-time syntax highlighting
- Option 3: Integrate a web-based code editor
  - we used the web-based code editor CodeMirror. 
  - we can highlight the heavy weight of the editor, which may result in a longer load time. 
- In the end, we wanted to provide as smooth and rich of an editing experience as possible. We also wanted to future-proof our editor in case we want to support longer text (more than 6000 characters) and extend functionality, such as implementing collaboration or code execution.
  - Considering that both Quill and HTML elements didn’t fully meet our functional requirements, we chose instead to take a risk and invest in integrating a code editor. It has all the desired features out of the box, provides very solid performance and user experience, and offers a lot of extensions.

### [How we integrated a code editor on the Miro canvas using Ace _202310](https://medium.com/miro-engineering/how-we-integrated-a-code-editor-on-the-miro-canvas-a41e0eff7f21)

- The scaling of the rendered widgets is managed by our canvas engine, but in Edit mode we need to scale the HTML element with the editor manually. 
  - The scale factor is a multiplication of the board scale (zoom in/out) and the widget scale (widget size). 
  - To scale the widget, we apply the CSS property on the editor container: `transform: scale($scale)`.
- During the prototyping with CodeMirror 5 and CodeMirror 6, we met this problem: if the editor is scaled, then the mouse events’ positions, as well as the visual elements’ sizes and positions are calculated wrong. Attempts to deal with those issues were unsuccessful: there is no easy fix or built-in support for this in CodeMirror.
  - We discovered that the Ace and Monaco editors, on the other hand, support the CSS transformations.

- To highlight the plain text, we’re using the native static highlighter extension for the Ace editor. It starts a minimal version of the Ace editor that outputs the HTML string.
- 🤔 For us, although it was less attractive at the beginning, the Ace editor was the best and the only option. It is very lightweight, supports scale out of the box, has the static syntax highlighting extension, and has been battle-tested for more than a decade. 

## [Moving to Monaco — A Journey to a Better Code Editing Experience | DataCamp Engineering _202107](https://blog.datacamp.engineering/moving-to-monaco-a-journey-to-a-better-code-editing-experience-8c2aa5360be5)

- The starting point of our journey is a custom code editor built on top of the Ace Editor library. This editor had served as the reliable backbone of Campus — our interactive course application — for several years.
  - Poor accessibility
  - Poor abstraction
  - Bad page performance
- We evaluated several solutions along the way, but ultimately settled on building our editing experience on top of Monaco.
# more
- [低代码之路 —— 公式编辑器](https://rapidsu.cn/articles/3858)
  - 主要功能呢，就是将表单的校验逻辑可视化
  - 完善的编辑器甚至能检验出输入规则的符合法性。这部分呢，我并没有花太多时间去造轮子，而是直接在 npm 库里面物色了一个：formula-editor-react

- [git diff 知道吧？请说说实现原理](https://rapidsu.cn/articles/4437)
  - 本文只是简单探索了一下 diff 的基本原理，想要应用到实际场景肯定还需要大量的工作，很多开源的编辑器，例如 monaco-editor，codemirror 等都自带了 diff 能力，实际场景最好还是借助这些成熟的开源库
  - 使用在线json对比工具的时候，对于这种对比的实现方式产生了好奇，我用脚指头想也知道这功能实现起来肯定不简单，于是小小地研究了一下, 3种实现方式, 最短编辑距离/最长公共子序列/Myers算法
