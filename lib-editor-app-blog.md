---
title: lib-editor-app-blog
tags: [blog, editor]
created: 2021-05-13T04:44:23.155Z
modified: 2022-08-21T10:11:37.453Z
---

# lib-editor-app-blog

# guide
- tldr: Unless browsers will open for the Web multiple crucial features (such as IME, keyboard, selection, touch, on-screen keyboard, spellchecker, etc.), contentEditable is the only sane way to handle text editing.
- contenteditable gives you one very important feature that you can't fake yourself: access to the browser's spell check and corrections
- Yep, we do use contentEditable as an input source and also as the view to which we render (you wouldn't be able to reliably handle the keyboard otherwise).
# blogs

## [谈谈编辑器的架构设计 - 知乎](https://zhuanlan.zhihu.com/p/681850367)

- 我大致参考过的框架包括两个： lexical/Codemirror
- 有种设计模式叫MVC。编辑器的架构与其非常相似，我将其分解为三个层次的概念

## [Bike: Innovative Rich Text Editing](https://www.hogbaysoftware.com/posts/bike-rich-text/)

- Bike Outliner now supports rich text!
- link button
  - 点击text可编辑link文本
  - 点击末尾icon可以跳转
- typing affinity
  - 当光标在mark边缘时，会显示短下划线指示当前位置会与前面还是后面样式相同
- floating format toolbar
  - 支持快捷键和左右箭头
- visible typing attributes
  - 在光标位置会显示当前format的名称和样式

## 📋 [如履薄冰的复制粘贴-clipboard详解 - 掘金](https://juejin.cn/post/6903698870694313991)

- 本文将从浏览器自身的复制粘贴功能出发，带领大家了解复制粘贴背后的功能实现，对比多个富文本文档实现，在浏览器的各种限制下，如何实现一个基于JSON-MODEL数据并且适用于类富文本的剪切板。

- 当我们在表单元素，例如input，textarea中实现一次完整的复制粘贴，调用的就是浏览器的默认能力。

- MIME类型/媒体类型（通常称为 Multipurpose Internet Mail Extensions）是一种标准，用来表示文档、文件或字节流的性质和格式；
  - MIME的结构实际上也非常简单：由类型和子类型组成，两个字符串中间用'/'分割组成type/subtype。不允许空格存在。
  - 常见的MIME类型有：text/plain，text/html，image/png，application/json等；
- 也就是说浏览器想知道你的数据是什么类型的数据，需要做什么样的解析或者下载处理（例如解析到媒体或者文档文件，一般会当成资源下载），需要通过MIME获知；
  - 在复制粘贴过程中，实际上，也是需要通过MIME去进行对应的解析处理。

- DataTransfer，除了drag events还可以在paste，copy, cut等事件上获取。
  - DataTransfer有多个属性和方法，但是大部分都是在drag下产生或者才能使用的。例如files只适用于drag事件，如果拖动操作不涉及拖动文件，则属性为空数组

- clipboardEvent是浏览器支持的通用剪切板事件。

- 在浏览器下，一般复制粘贴会使用浏览器通用的标准MIME格式
  - 在input和textarea复制粘贴中都只接收text/plain的MIME类型，这也可能是所有软件（还没遇见过不支持这种格式的）都会支持的默认文本格式。

- 在富文本中，除了纯文本也就是text/plain这种类型之外，一般还需要支持另外两种MIME类型，分别是text/html和image/png（这里单纯指复制粘贴）
- text/html：
  - 例如实现一个功能：从word之类的文档复制粘贴一段文本，要求样式和格式保持一致性，这应该是富文本很常见的功能；
  - 这时候，如果我们直接获取text/plain的话，只能获取到对应的纯文字版本。这时候就需要我们去拿text/html类型的文本。
  - 值得注意的是，一般的文字编辑器（word，ppt，金山文档......），获取到的并不是标准的html格式，或者说，带有大量的多余数据，这时候，我们可能需要主动去进行一次数据清洗，只保留我们需要的数据。
  - 一般可以在获取数据后，使用正则去清除多余的数据，在ueditor、wangeditor等常见的富文本中可以看到对应的数据处理。
- image/png：
  - 复制图片，一般是从外部进行复制粘贴；

- 需求
  - 首先我需要在一个类似PPT文档下实现一个复制粘贴的功能包括，可复制文本和图片并粘贴到我们的页面上，
  - 其次需要支持内部定义好的其他元素，
  - 最后需要支持跨标签页甚至是跨浏览器在我们的页面上保持一致性的复制粘贴交互；
- 由于JSON数据与html数据之间并不相通，例如在普通的富文本编辑器中，直接复制，基本都是直接拿到的html数据；而当前的场景下，因为使用了MVVM框架的原因，我们是将所有的dom转化成单个的model数据，因此你复制出来的数据需要做单独的处理，并不能直接粘贴到任何富文本上。

- 浏览器对于剪切板是有严格的安全限制的：不允许直接读取剪切板内容，除非使用提案中的navigator.clipboard.readText / navigator.clipboard.read进行权限的询问，用户主动通过后，可以直接读取
- 如果想要定制化菜单，当然可以监听contextMenu事件，然后主动阻止默认行为，例如腾讯文档或者Google Slides那样。但是有些浏览器的行为就会被隐藏甚至无法主动调用：例如复制粘贴。

- 基于以上两点，是需要有自己的一套内存数据，在剪切板和右键菜单提供数据，然后在必要的时候主动更新clipboard，让系统的粘贴内存数据和内部的内存数据达成统一。
  - 这里有一个技巧，就是可以使用document.execCommand('copy/cut')去主动更新clipboard里的数据。
  - 当你在右键点击复制的时候，倘若需要主动更新数据到剪切板上，可以主动调用，获取cut/copy事件抛出的clipboardData，然后使用该对象下的setData，对内外数据统一，在跨标签页上保持数据的流通很有作用。

- 为什么我们要自己设置MIME呢？
  - 首先通用的MIME除了text/plain之外，其余的类型都会主动添加该类型下所需的数据，例如text/html的话，会在首尾添加对应的xml格式数据，而其他的在前面也说过，会经过一次MIME解析，对于标准但特殊的MIME格式可能会有一些特殊添加数据或者解析操作。
  - 其次，跨浏览器目前为止我只看到text/plain和text/html是可以传递数据的，其余的一律被过滤...... 但是如果直接设置text/plain是会造成，所有的复制内部数据都会暴露在外面的粘贴事件上，如果是普通的文本数据倒还好，如果是内部的保存的格式化数据，就会让用户感觉很奇怪。

- 如果不需要处理跨浏览器，那么并不需要那么麻烦，只需要保持一个自定义的MIME类型即可。

- 一般来说，我们获取剪切板内容判断，是会先从内部数据开始判断的，也就是自定义的MIME类型，然后是图片类型，最后才是纯文本类型；

- 在多个平台下，支持的程度不同，甚至实现起来，获取到的数据也完全不同。
  - Google Slides 、腾讯文档等web应用不支持复制图片，需要单独解析text/html数据里的图片，也就是需要做字符串解析，实际上是可以做到；
  - 金山文档、office等web应用不支持文本框和文本的原因是，这些应用使用了内部协议，我们一般不针对特殊协议（MIME）做处理；
  - windows系统不支持图片和音视频复制粘贴，经测试，在该系统下只能拿到纯文本；

- 基于内部数据的信任，一开始你或许只想着复制数据，序列化之后塞到我们定制好的MIME类型里面，下一次再拿出来反序列化就好了。
  - 然而，一开始我们的产品对多媒体的文件（音视频、图片）做了特殊处理：在一上传到我们页面的时候单纯转成blob，保存在内存里，等下一次同步的时候再去做一次上传到云端的处理。这种做法一定程度上可以提高用户的体验，毕竟不需要一上传就必须要经过一次上传云端的操作。
  - 在这里就有一个弊端了：跨标签页的时候，如果上一个的标签页关闭，那么势必blob链接会失效，因为blob的内存或者说引用地址是保存在上一个标签页的，但是如果这时候去改动的话，影响范围会变得比较广。
  - 这时候，只能采取降级方案：已经上传到云端上的，直接获取链接地址；还未上传的，是blob链接的只能先复制blob地址，在新的标签页，先通过fetch下载到当前页面，然后就可以跟普通文件一样处理了。
- Google slides就是blob在转url的做法，而腾讯文档就是直接上传，语雀则是先用一张base64展示在上传。

- 当然或许有人会说，可以先将文件转成base64的格式，但是我们复制一般可能会有多个媒体文件，这时候base64就会耗费时间生成，而且数据量可能会超过剪切板内存大小。
  - 毕竟找不到可以在浏览器间传递二进制文件的方法，只能先采用这种恶心的方法。

- 直接使用一个DataTransfer对象，然后往里面塞数据，经测试也是不行的。
- 当然，倘若你了解clipboardItems，你可能会觉得clipboardItems可以往剪切板里塞数据。
  - 是的，完全可以，不过clipboardItems看起来像个数组，用起来也是个数组，就是数据是只支持长度为1的数组.

- 在浏览器里，我们通过image/png拿到的永远是单一的图片格式，因为浏览器为了支持、兼容图片格式，都会将图片转成bitmap给你，这样一来你在image/png里拿到的只是bitmap的blob格式，这会产生两个问题：
  - 你无法获取图片原来的格式，永远只能拿到png，也就无法进行格式判断；
  - bitmap在不同平台下的转换不同，这会造成图片有可能会增大体积，例如一张20m的图片，通过getAsFile方法获取到的，可能超过30m......
  - 在mac和window下测试可能会得到两个不同的结果。
- 果然还是要通过input才能完整的获得浏览器的文件能力。

- 当然，还有一些其他的问题存在，例如复制粘贴外部的表格实际上需要单独做一层解析，这个过程会更加麻烦；
  - 序列化和反序列化的数据需要慎重考虑，因为有些数据在格式化后会有转变的风险......

- 事实上，整个的复制粘贴并无法做到完美，在浏览器的各种限制下，会有很多无法保持一致性的问题存在，只能在夹缝中生存。
  - 倘若原来需要复制粘贴的内容是符合html规范的，那么处理起来就会很简单；
  - 若是跟我遇到的场景一样，数据基本都为JSON，那么势必需要花大精力去处理数据之间的转换和处理一些边界问题。

## [基于表达式的程序设计](https://plantain-00.github.io/blogs/?src=./contents/program-design-based-on-expression.md)

- 对于某些业务，例如：
  - 复杂查询，例如 JIRA 任务的 filter
  - “规则”相关的需求，例如定义类似 cron 的定时任务
  - “关联”相关的需求，例如设置一段文字的颜色总是等于另一段文字的颜色

- 如果按照普通定义数据模型的方式，当业务越来越复杂，定义的数据模型、数据传输结构、数据库结构、GUI 等都需要随之进行扩展。

- 而如果使用表达式作为业务的内部存储、实现方式，数据模型、数据传输结构、数据库结构里就只是表达式字符串，不再需要频繁扩展，执行查询、规则的代码也不再需要频繁修改，需要修改的只是 GUI，从而大幅提高开发、维护效率。
- 例如：
  - 条件表达式，name = 'foo' AND status = 'SUCCESS'
  - 行为表达式，例如设置 text2 的文字颜色属性为 text1.color
- 设置表达式时，可以：
  - 对表达式进行 parse，根据 parse 出的数据，显示对应的输入 GUI
  - 提供高级模式，或自定义模式，以供用户可以直接输入表达式

- 对于“关联”相关的需求，使用表达式也可以更容易分析各个“关联”之间的依赖关系

```JS
get width() {
  return this.parent.width - this.marginLeft - this.marginRight
}

// 使用表达式，这种内置关联关系可以表示为：
width = 'this.parent.width - this.marginLeft - this.marginRight'
```

- 在对用户设置的关联关系、内置关联关系进行依赖分析时，表达式形式的内置关联关系，可以通过 parse 出的 AST 进行分析，和对用户设置的关联关系分析方式一致；
  - 而 getter 代码形式的内置关联关系，就无法提供这些数据，只能额外的代码检查来进行分析，随着内置关联关系越来越复杂，额外的代码检查也需要保持相应的更新，从而增加了维护成本。

## [拖拽交互的程序设计](https://plantain-00.github.io/blogs/?src=./contents/drag-program-design.md)

- 这里说的拖拽交互是指拖拽元素触发的交互，例如：
  - 拖拽元素改变位置
  - 拖拽元素边缘改变元素大小
  - 拖拽滑块设置一个数值
  - 拖拽时钟指针设置时间

- 这类问题的直接思路是，在待拖拽的元素上设置 drag 相关的事件处理程序，例如：
  - mousedown 事件：记录初始位置
  - mousemove 事件：根据当前位置和记录的初始位置，改变元素的位置或大小
  - mouseup 事件：根据最后的位置和记录的初始位置，返回需要的数据
- 这种思路某些复杂需求下会有缺点，包括：
  - 如果拖拽区域较小，且用户拖拽速度较快，会导致拖拽结束前就离开了拖拽区域，导致没有触发 mousedown 事件
  - 拖拽到别的不相关的元素上，触发不相关的元素的意外行为

- 透明蒙版可以解决上面所说的问题，具体思路为：
  - 增加覆盖整个页面的透明蒙版，初始位置数据一旦设置，透明蒙版就出现，清空初始位置数据时透明蒙版就会隐藏
  - 拖拽元素的 mousedown 事件：记录初始位置
  - 透明蒙版的 mousemove 事件：根据当前位置和记录的初始位置，改变元素的位置或大小
  - 透明蒙版的 mouseup、mouseleave 事件：根据最后的位置和记录的初始位置，返回需要的数据，清空初始位置数据

- 如果拖拽过程有耗时操作
  - 例如一个元素从初始尺寸拖拽成一个新的尺寸，元素内容需要复杂的计算才能得到新尺寸下的显示效果，而拖拽时会频繁触发 mousemove 可能导致性能问题。解决思路有：
  - 拖拽时只更新元素框，拖拽结束时才更新元素内容：交互效果不完美，但可以接受。
  - 通过 debounce 限制更新元素内容的频率，提高交互效果的同时，避免性能问题。

- 拖拽时产生的大量数据记录到操作历史中，会导致回撤基本不可用，解决思路为：
  - 拖拽时返回的数据直接存储在组件本地 state 上，元素框根据这个 state 的数据显示
  - 拖拽时返回的数据 debounce 后存储在组件本地 state 上，元素内容根据这个 state 的数据做复杂计算后显示
  - 拖拽结束后返回的数据存储在编辑器操作历史 state 上，元素内容根据这个 state 的数据做复杂计算后显示，清空本地 state
  - 元素内容的计算中，如果本地 state 上有数据，说明在拖拽中，使用这个数据进行计算，否则拖拽已经结束，使用编辑器操作历史 state 上的数据进行计算

- 如果元素内容的计算耗时不可控
  - 可能出现拖拽完成后的计算结束后，拖拽中的数据的计算结果才返回。
  - 解决方案是，拖拽中的数据的计算后，如果已经拖拽结束，丢弃计算结果。

## [撤销重做的程序设计](https://plantain-00.github.io/blogs/?src=./contents/undo-redo.md)

- 在编辑器类的程序中，撤销重做是非常普遍的功能。对其进行抽象、复用可以大幅提高开发效率。
- 基于 snapshot 的撤销重做
  - 这是最简单、有效的实现方式。
  - 把所有可撤销重做的状态集中到一个 object 里，修改状态后，产生一个新的 object 并放到操作历史数组中，增加游标来指示当前的状态，移动游标即可实现撤销重做。
- 基于 patch 的撤销重做
  - 当有多个用户进行同时编辑时，业务上要求不能撤销别人的修改，这时基于 snapshot 就没法实现撤销重做了。
  - 基于 patch 来实现时，如果多个用户改的不是同一个分支，撤销 patch 就不会互相影响了。
  - 基于 patch 来实现时，记录的不再是状态修改结果，而是 patch 和反向 patch 历史，每次 patch 都记录操作者，以实现用户操作的隔离。

## [富文本编辑器框架ProseMirror、Slate和Lexical横向比较 - 掘金](https://juejin.cn/post/7140921781380415501)

- 比较了 
  - editorState, selection, normalize, operation
  - prosemirror, slate, lexical

## 📝 [How to implement a web-based rich text editor in 2023?](https://letsken.com/michael/how-to-implement-a-web-based-rich-text-editor-in-2023)

- Since 2011 I’ve been spending a great junk of my time taming web browsers to behave correctly and predictably when editing rich text
- If you wanted to take control over how contentEditable behaves, you have to write your own code. 
- The challenges
  - Define a custom model
  - Selection Mapping: You need to have some sort of internal coordinate system to address content (e.g. second paragraph at character 5) and map that to a corresponding position in the DOM and vice versa.
  - Keyboard input: Instead of letting contenteditable do its thing, you want to intercept each keystroke, update your internal model first, and then calculate the minimum update to be made to the DOM to reflect that change.
  - Copy and paste: People will paste all imaginable HTML content from MS Word, Google Docs or other websites. 
  - Undo/redo: Every change made to the document must be reversible.
- ProseMirror
  - Before ProseMirror he released CodeMirror, a web-based editor for source code editing.
- Lexical
  - While Lexical is framework agnostic, I suspect they have a “slight” bias towards React, so some decisions might have been made in favor of what will translate best to React. 
- Substance.js
  - It was designed to solve extremely demanding use-cases, as we were building a structured editor for scientific content 
  - Unlike ProseMirror (which uses a hierarchical data model similar to HTML), Substance uses directly addressable properties. So for instance you can refer to an image caption by its unique node id and property name (e.g. [‘image_32’, ‘caption’]). That model allows data bindings, such as updating and sorting a reference list, based on the order the citations were placed in the document.
  - Substance also allows documents with multiple editor surfaces. Because in many cases you may want to maintain a title and some metadata, such as author names, that are outside of the document’s body. Still you want a shared undo/redo history and store all data as one self-contained document.
  - While you can create a Substance document iteratively through a sequence of operations, you can also load and store snapshots of it as XML. Most other frameworks use JSON or HTML as a serialization format. The problem with JSON is, that it can get quite large, as it’s not optimized for hierarchical content. The problem with HTML is, that it is designed to display a document, not to represent its content.
  - Substance is not under active development anymore

- Stay close to the metal
  - I learned to resist the urge to fit the Rich Text Editor into my higher-level Javascript framework’s paradigm. 
  - I strongly believe that in the case of rich text editors it is a good idea to stick to native Web API’s and write plain Javascript. 
  - Why? Because you have full control over rendering and nothing is getting in between. You want to manipulate the DOM at the granularity of text nodes. 
  - Unopinionated editor libraries help you with that.
- Better be conservative
  - You’ll find that you can build basic features rather quickly. But you will also find that once you leave the common path, like what the editor libraries’ examples are providing, you’ll end up breaking things without noticing it. 
  - Hence, I’d always start with the smallest possible featureset, and get that stable and tested. 
  - Then carefully add more functionality, one little step at a time. 
  - It’s easy to make a move forward (e.g. add support for image captions) but it’s almost impossible to make a step back, because once you introduced a new content type, you’ll have user data to maintain and migrate.
- Develop in isolation
  - I’ve been involved in many projects where the editor component was developed within a complex application setup. 
  - What usually happens is that developers call custom APIs from within editor-specific code. This is a recipe for disaster.
  - The solution is to develop the editor within in a lightweight sandbox, and do integration as a separate step. 
  - If you deal with any data that’s not part of the editor’s internal content model, you need to come up with a synchronous proxy that shields the async operations from messing with the editor operations. Better yet, you manage to keep all your editor content self-contained.

- How would I build my next editor?
  - My current editor implementation at Ken is based on ProseMirror.
  - However Ken is built with React, and I wanted to use React components for everything
  - So I’m tempted now to build an easy to understand reference implementation of a complete text editor. It’d be based off my existing code for the Ken editor, but entirely framework agnostic, fast and future-proof. Instead of a higher level wrapper around ProseMirror (such as TipTap)
  - Another approach that’s tempting for me is to revive Substance.js, but remove the rendering part of the library and use Svelte instead. 

## 👥 [How to implement a web-based rich text editor in 2023?](https://discuss.prosemirror.net/t/how-to-implement-a-web-based-rich-text-editor-in-2023/5271)

- 
- 
- 
- 
- 

## [Why ContentEditable is Terrible. Or: How the Medium Editor Works | by Nick Santos | Medium Engineering_201405](https://medium.engineering/why-contenteditable-is-terrible-122d8a40e480)

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

## [一文带你了解富文本是如何协同工作的 - 掘金](https://juejin.cn/post/7159204268770230303)

- 国外notion使用了块级编辑器，一切皆组件，一炮走红。之后块级编辑器的思路被认可。
  - 做L1的notion一样可以有自己排版布局，再加上现代浏览器国内的不断加强，似乎L1没有足够的动力升级为L2编辑器了。
  - 典型的例子有飞书和语雀，他们是有足够人力和时间来升级到L2，但实际上他们引入更多的块级组件。
  - 用来实现“一切皆对象”概念，很好的实现了互联网最大的需求，“把信息连接起来”。

- 我们文档拥有自己mvc模式，model层有8种基础的原子操作，所有操作都可以分解成这8种，yjs存储的其实就是这些操作，前端展示的时候，会一步步重现这些操作，形成用户可以看到的文档
- slate中Text相关的操作是通过String所自带的函数实现的，比如splice。YText为了内容不被一下子覆盖掉，也做了类似的处理
- 我们建立了独立的撤销栈（undo）和重做栈（redo），并把用户输入的原子操作放入撤销栈，撤销后的操作再放入重做栈。当用户撤销时候，我们把 undo 栈最上面的操作取出，并反转执行。

- Op-based CRDT 的思路为：如果两个用户的操作序列是完全一致的，那么最终文档的状态也一定是一致的。所以索性让各个用户保存对数据的所有操作(Operations)，用户之间通过同步 Operations 来达到最终一致状态
- 但我们怎么保证 Op 的顺序是一致的呢，如果有并行的修改操作应该谁先谁后？答案是按照用户加入时的id进行排序。
  - 显然，yjs是按照clientID的顺序，来实现覆盖的。
  - 我去翻源码也证实了这一假设
- yjs会按照clientID的排序来，划重点，和时间没有关系，一个clientID可能比较晚产生，但是他可能会排在前面。当然，一次连接中，这个顺序是固定的。
  - 这时候，可能有人要说，这不对了。这样岂不是，一个人的数据永远会被另一个覆盖~~
  - 实际使用中，双方是持续不断输入的，绝大多数情况下，不会在同一次合并中，同时修改一个值。当然，如果真的触发了，则会覆盖。至于，做到不覆盖又体验良好，那恐怕只能人工了，像git一样。有时候，结合实际的妥协也是一种方案。

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

## [Concept of Block Style Editor](https://domino-editor.psyhyde.vercel.app/docs/)

- https://github.com/psyhyde/domino-editor
  - A Playbook for Block Style Editor (BSE): Text Styling, Block Components, Misc Functions & Theme Switcher

- Background of Block-Style Editor：
  - Markdown, for its high readability and simple syntax, has been adopted widely; 
    - Pure Markdown editing is WYSIWYM
  - Most Web-based RTF editors follow WYSIWYG interaction pattern
  - Block Style Editors provide a Markdown-like but WYSIWYG editing experience
  - On UX and interaction level, BSE provides a similar experience to Typora, MarkText, but with integrated Mini-App Blocks

- Features of Block-Style Editor：
  - Follow a structure of Markdown (Template) + CSS + Fonts
  - Inherent the text styling rules of Markdown, 
    - keep its simplicity and content-focusing approach; 
    - Remove features like: line spacing, font size, font color
  - Expand text editing into Text Editing & Styling and Mini-App Customization
  - Mini-App Blocks: table, image container, advanced code block, prefabricated UI view, embeds.
  - A web-based Content Editor that, take Interactive Document and Modular UI as guideline, 
    - use Block or Paragraph as content unit, 
    - use Markdown as its Template Structure.

- Block-Style Editor has its roots in CMS(content management system), SSG (static site generator), GitHub& Markdown, MDX, JSX, and Low-code Site Building.
- In a sense, a Block Style Editor is a Modular CMS for web document use case.
# blogs-typesetting

## 🆚️⚖️ [On Typesetting Engines: A Programmer's Perspective _202410](https://blog.ppresume.com/posts/on-typesetting-engines)

- [排版引擎纵谈：程序员的视角](https://blog.ppresume.com/posts/zh-cn/on-typesetting-engines)

- Spent two weeks writing a super looooong post: "On Typesetting Engines: A Programmer's Perspective", just to answer one question: why we chose LaTeX as the default typesetting engine.
  - In this post I compared 5 typesetting engines from a programmer's perspective: HTML/CSS, LaTeX, LaTeX.js, Typst and react-pdf with 4 judgement criteria: 1) line breaking, 2) CJK support, 3) pagination, 4) instant preview.

- 📌 The goal of PPResume is to be a professional resume builder that offers top notch typesetting quality, with native support for multi languages.
  - 必须生成顶级、高质量的 PDF
  - 必须提供对多语言的原生支持
- 为了生成顶级、高质量的 PDF，排版引擎必须具备优秀的换行算法，而为了实现多语言的原生支持，排版引擎必须能够处理具有庞大字符集的语言（如中文、日文和韩文，即 CJK）。
  - 还有一点，排版引擎必须支持分页，才能生成 PDF。
- 简而言之，我会通过检查排版引擎是否符合以下评估标准来对其进行评判：
  - adopt Knuth Plass line breaking algorithm
  - support CJK with respect to best typesetting practices
  - support pagination
  - (optional) support instant preview

- 换行算法是排版引擎的核心技术之一。主要目的是决定段落中文本换行的最佳点。
- 评估换行算法质量有三个关键指标：
  - 对齐：换行算法与对齐技术结合使用，以创建间距均匀的文本行。
  - 断词：许多高级算法都采用断词来改善换行，特别是对于长单词的语言。
  - 优化：算法通常会尽量减少整段文字之间难看的间隙或过于紧凑的间距。
- 换行算法有两类：
  - 最少行数：一种贪婪算法，将尽可能多的单词放在一行上，然后移动到下一行并重复此过程，直到没有更多单词可放置。这种方法被许多现代文字处理器使用，如 LibreOffice Writer 和 Microsoft Word。
  - 最小锯齿：一种动态规划算法，最早在 TeX 中使用，旨在最小化行末空格长度的平方和，以产生比贪婪算法更美观的结果，后者并不总是最大限度地减小行末空格长度的平方和。
- 从技术上讲，最少行数算法速度更快，而最小锯齿算法则产生更具视觉吸引力的结果。
- 在所有换行算法中，Knuth Plass 换行算法是最小锯齿方法的黄金标准。它被各种排版引擎广泛采用，如 TeX、SILE 和 Typst 等。

- CJK（中文、日文和韩文）语言的排版通常被认为比拉丁字母语言更为复杂。这一点在 koreader 项目的经典讨论中得到了体现。
  - [Chinese, Japanese and Korean typography: some questions · Issue · koreader/koreader _202505](https://github.com/koreader/koreader/issues/6162)
  - 这种复杂性的根本原因在于 CJK 语言的字符集远远大于拉丁字母语言。根据 CJK 统一表意文字，截至 Unicode 16.0，Unicode 定义了总共 97680 个字符。这实在是庞大无比。相比之下，拉丁字母表的字符数量仅有几百个

### HTML + CSS

- 从技术上讲，HTML（超文本标记语言）并不是一个排版引擎，而是一种用于创建网页结构和内容的标记语言。它的主要目的是定义文档的结构，例如标题、段落、列表和链接等。
  - 它无法处理复杂的排版任务，例如：
  - 断词：HTML 不处理断词。
  - 分页：HTML 不是为分页设计的。
- 虽然 HTML 本身不能作为排版引擎使用，但结合 CSS（层叠样式表）后，可以视为一个初级的排版引擎。
  - 从工程角度来看，HTML 和 CSS 并未实现 Knuth Plass 换行算法，因此无法满足 PPResume 的需求。
  - 虽然也有一些 Knuth-Plass 换行算法的 JavaScript 实现，但似乎没有一个准备好用于生产环境
- 建议在 CJK 和西文字符之间留出一些空格，而纯 HTML 和 CSS 无法自动做到这一点——这需要 JavaScript 的帮助。
- 优点
  - 普适性：HTML 和 CSS 是 web 的基础，使其在任何带有浏览器的设备上都可访问。
  - 响应式：HTML 和 CSS 是响应式的，可以适应任何大小的视口。
  - 灵活性：HTML 和 CSS 非常灵活，可以通过丰富的标准 API 进行编程。
  - 实时预览：HTML 和 CSS 支持实时预览。
- 缺点
  - 排版控制有限：与专用排版引擎相比，HTML/CSS 在细微排版细节上提供的控制较少。
  - 浏览器兼容性：不同的浏览器可能会以不同的方式渲染相同的 HTML 和 CSS，使得跨设备保持一致性具有挑战性。
  - 无原生分页：HTML 和 CSS 不是为分页文档设计的，因此不提供导出为 PDF 的一流工具。
  - 换行效果差：如前所述，HTML 和 CSS 未实现 Knuth Plass 换行算法。
  - CJK 排版需要额外努力：HTML 和 CSS 需要额外的库和努力才能遵循 CJK 的最佳排版实践。

### LaTeX

- TeX 是由 Donald Knuth 在 20 世纪 70 年代末创建的排版系统。它专为创建高质量排版的文档而设计，特别是那些包含复杂数学和科学符号的文档。
  - LaTeX 是一个建立在 TeX 之上的文档编制系统。它由 Leslie Lamport 在 20 世纪 80 年代初创建，以简化文档编制过程。LaTeX 在 TeX 的低级编程语言之上提供了一组更高级的宏，使其更易于使用和更直观。
  - TeX 拥有黄金换行算法——Knuth Plass 换行算法。毕竟 Knuth 是 TeX 的作者，对吧？
- LaTeX 在一些新引擎和一些宏包的帮助下对 CJK 提供了相当好的支持： 新引擎如 LuaTeX 和 XeTeX, 宏包如 xeCJK、CTeX 和 LuaTeX-ja
- LaTeX 从一开始就是为排版分页文档而设计的，所以它对分页有出色的支持，你可以轻松调整纸张大小、方向、边距等。
- LaTeX 默认在服务器端运行，因此从请求生成 PDF 到响应生成的 PDF 会有往返时间。
  - 然而，确实有方法可以缓解这一问题。魔法在于WebAssembly。
  - texlive.js：最初的将 LaTeX 编译为 wasm 的尝试，仅支持 pdfTeX 引擎
  - SwiftLaTeX，一个最近的尝试，让 LaTeX 引擎在浏览器中运行，支持带有 CJK 的 XeTeX。
  - TeXpresso：支持实时渲染和错误报告的 LaTeX，这里有一些 录屏演示
- 市场上基于 LaTeX 的简历生成器选择非常少
- 优点
  - 精确和控制：LaTeX 提供无与伦比的文档布局和排版控制。
  - 黄金换行算法：Knuth Plass 换行算法是最优换行算法的黄金标准，且其是由 TeX 作者发明的。
  - 广泛的 CJK 支持：有大量的宏包扩展了 LaTeX 对 CJK 的支持。
- 缺点
  - 学习曲线陡峭：与所见即所得编辑器相比，LaTeX 对新用户的入门门槛更高。
  - 没有实时预览：默认情况下，LaTeX 需要在服务器上进行编译，因此没有实时预览。
  - 陈旧且晦涩的开发体验：LaTeX 的编译日志有时难以阅读，只能通过二分搜索方法进行调试。

### LaTeX.js

- LaTeX.js 是一个将 LaTeX 转换为 HTML5 的工具，旨在直接在浏览器中渲染 LaTeX 文档，而无需服务器端处理。
  - [LaTeX.js Live Playground | LaTeX.js](https://latex.js.org/playground.html)
    - 在线示例渲染的文档没有分页效果
    - LaTeX.js 不使用 Knuth Plass 换行算法，而是采用 text-align: justify 来最小化段落的锯齿。
    - 页面的概念不适用于 HTML，因此与分页相关的任何宏都会被忽略，也就是说，你无法使用 LaTeX.js 生成分页文档，这对于简历生成器应用来说是致命的。
    - LaTeX.js 支持 CJK，因为它本质上是 HTML 和 CSS 的一个转译器。然而，和 HTML、CSS 一样，它并不遵循 CJK 的最佳排版实践，且想要调整它以便遵循这些最佳实践时，会更为困难。
    - LaTeX.js 提供实时预览，因为它是一个客户端库，能够在浏览器中运行。
- LaTeX.js 仅提供有限的 TeX/LaTeX 解析能力，换句话说，许多 LaTeX 宏包无法在 LaTeX.js 中使用。
- 当我在 2022 年 12 月我开始创建 PPResume 时，我也尝试了一段时间 LaTeX.js，但在发现其致命限制后，我迅速放弃了它，转而使用服务器端 LaTeX。我个人认为，LaTeX.js 是一个很好的想法，但远未成为生产环境下的 LaTeX 替代品。
- 优点
  - 实时预览：LaTeX.js 完全在客户端处理 LaTeX 文档，这意味着它可以在浏览器中实时渲染文档，消除了对服务器端 LaTeX 安装和编译的需求。
  - 可扩展性：该项目用 JavaScript 实现，易于集成到 Web 应用程序中。新的宏也可以很容易地通过 JavaScript 来添加。
- 缺点
  - 功能有限：LaTeX.js 仅涵盖有限的 LaTeX 功能，远未成为生产环境下的 LaTeX 替代品。许多 LaTeX 宏包无法与 LaTeX.js 一起使用。
  - 缺乏分页：一些 LaTeX 功能，如粘连和分页，无法转换为 HTML，这对于生成像 PDF 这样的分页文档来说是一个致命缺点。
  - 换行效果差：LaTeX.js 基于 HTML 和 CSS，并没有实现 Knuth Plass 换行算法。
  - CJK 排版需要额外的工作：同样，由于 LaTeX.js 基于 HTML 和 CSS，因此需要额外的工作才能遵循 CJK 的最佳排版实践，而且比纯 HTML 和 CSS 更麻烦一些。

### Typst

- Typst 是一个现代排版系统，旨在成为 LaTeX 的直观高效替代品。它的语法深受 Markdown 的启发，使得那些觉得 LaTeX 语法复杂的用户更容易上手。
- Typst 提供两种换行选项：
  - #set par(linebreaks: "simple")：以简单的首次拟合风格进行换行。
  - #set par(linebreaks: "optimized")：优化整个段落的换行，此选项实现了 Knuth Plass 换行算法。
- Typst 的分页功能开箱即用，作为一个专用排版引擎，这一点相当不错。
- CJK 支持尚不如 LaTeX 成熟。因此，Typst 社区中存在许多暂未解决的问题。
- Typst 提供了 typst watch 命令，结合增量编译，PDF 可以在毫秒内更新。此外，还有一些扩展如 tinymist，可以在编辑器中实现实时预览。
- 它也可以在浏览器中运行，因为该项目是用 Rust 编写的，并设计为能够编译为 WebAssembly。实际上，官方的 Typst web app 就是通过 WebAssembly 在浏览器中运行的。然而，这一部分并未开源, 但社区提供了开源替代方案

- 优点
  - 用户友好的语法：Typst 的语法比 LaTeX 更直接和一致，使初学者更容易学习和使用。
  - 快速编译：Typst 具有增量编译，编译速度在毫秒级而非秒级。
  - 可定制的换行：Typst 提供选项让用户选择 Knuth Plass 换行算法。
- 缺点
  - 有限的生态系统：作为一个较新的工具，Typst 缺乏 LaTeX 提供的丰富的宏包生态系统，这可能限制高级排版需求的功能。
  - 不稳定的 CJK 排版：Typst 在 CJK 排版方面仍存在许多问题，并在不断演进中。
  - 实时预览是私有的：Typst 并未开源其 WebAssembly 绑定，因此在浏览器中没有官方的实时预览功能。

### react-pdf

- React renderer for creating PDF files on the browser and server
- react-pdf 内部实现了 Knuth Plass 换行算法。默认情况下，它会对英文单词进行断词处理。
- 支持分页，因为它是一个生成 PDF 的库。它还提供选项来指定页面大小、DPI、样式等。
- 在默认设置下，react-pdf 不支持 CJK 字符，你需要注册字体并在样式中引用它。
- 如果在客户端使用，你就可以享受实时预览，你可以再次查看 playground 以获取实时演示。否则，如果在服务器端与 Node.js 一起使用，由于请求到响应的往返时间，就无法实现实时预览。

- 看起来 react-pdf 将是简历生成器的理想排版引擎选择。
  - 但并不是一个专用的排版引擎。它缺乏许多仅在专用排版引擎中可用或运行良好的功能。例如，它没有内置的列表项。
  - 最重要的是，尽管它已经实现了 Knuth Plass 换行算法，但排版不仅仅是将段落断词换行，对吗？你仍然需要调整段落之间的间距、字体大小/样式，并遵循 CJK 最佳排版实践等。
  - 所有这些调整都需要大量的工作，而 LaTeX 已经开箱即用地提供了这些功能。
  - 实际上，有一个开源的简历生成器 open-resume，它使用这个库实时生成和更新简历 PDF，你可以自己检查其生成的 PDF，并与 LaTeX 生成的 PDF 进行比较。
- 优点
  - React 集成：react-pdf 允许开发者使用 React 创建 PDF 文档。
  - 实时预览：在客户端运行时，react-pdf 提供实时预览。
  - 良好的换行：react-pdf 内部实现了 Knuth Plass 换行算法，效果优于普通 HTML 和 CSS。
  - 分页支持：react-pdf 开箱即用支持分页，具有可定制的页面大小、边距等。
- 缺点
  - 有限的排版能力：毕竟 react-pdf 是一个 React 库，既不是专业的也不是专用的排版引擎
  - 对 CJK 的支持有限：react-pdf 可以通过手动注册字体渲染 CJK，但默认并不遵循 CJK 最佳排版实践。

### 总结

- HTML & CSS 和 LaTeX.js 都不支持 Knuth Plass 换行，而 react-pdf 和 Typst 的 CJK 支持尚未成熟，因此 LaTeX 是我们唯一的选择。

| Typesetting Engine | Knuth Plass line breaking |   CJK   | Pagination | Instant Preview |
|--------------------|---------------------------|---------|------------|-----------------|
|     HTML & CSS     |            No             |   Yes   |  Partial   |       Yes       |
|       LaTeX        |            Yes            |   Yes   |    Yes     |       No        |
|      LaTeX.js      |            No             |   Yes   |     No     |       Yes       |
|       Typst        |            Yes            | Partial |    Yes     |     Partial     |
|     React-pdf      |            Yes            |   No    |    Yes     |       Yes       |

- Both HTML & CSS and LaTeX.js do not support Knuth Plass line breaking, react-pdf and typst's CJK support is not production ready, hence LaTeX is our only option.
- In the long run if there're better choice, it is possible for PPResume to add support for other typesetting engines.
- Last but not least, having fun with polytype, a Rosetta stone for typesetting engines.

- https://x.com/xiaohanyu1988/status/1852215462979080551
  - Conclusion here: LaTeX is still the best choice for PPResume's case. 
  - HTML/CSS pros: flexible/responsive, cons: poor line breaking implementation, deal breaker
  - LaTeX pros: mature typesetting ecosystem, production-ready CJK typesetting support, cons: no instant preview for now
  - LaTeX.js pros: based on HTML, flexible and extensive, instant preview; cons: slightly better line breaking but still not in parallel with LaTeX, not full compatible with LaTeX, lacking some key capability, no pagination support.
  - Typst pros: modern syntax, better DX and UX experience, instant preview in official web app; cons: CJK typesetting is far from production-ready, instant preview feature is private and not open sourced
  - React-pdf pros: based on react, flexible, with instant preview, with good line breaking algorithm; cons: you have to reinvent the wheels for many typesetting structures like enumeration list, etc, poor CJK typesetting support.
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
# editor-non-js

## ✏️🇨 [kilo: Build Your Own Text Editor](https://viewsourcecode.org/snaptoken/kilo/)

- https://github.com/antirez/kilo /c
  - a small text editor in less than 1K lines of code

- https://github.com/vruss/Hecto /rust
  - This is a personal project mainly to learn Rust by implementing a text editor

- https://github.com/ilai-deutel/kibi /MIT/rust
  - Kibi: A text editor in ≤1024 lines of code, written in Rust
  - A configurable text editor with UTF-8 support, incremental search, syntax highlighting, line numbers and more
  - Kibi is compatible with Linux, macOS, and Windows 10
  - This project is inspired by kilo
  - Porting the kilo source code from C to Rust and trying to make it idiomatic was interesting
  - https://github.com/slashdotted/kibi
    - In this fork, simple collaboration features based on Melda have been implemented. 
    - The implemented paradigm is save and refresh: when the user saves the local copy, changes from other users are merged. 

- [kilo: Build Your Own Text Editor | Hacker News_201908](https://news.ycombinator.com/item?id=20603567)

- This is an instruction booklet that shows you how to build a text editor in C.

## ✏️🦀 [Hecto: Build your own text editor in Rust_201911](https://www.flenker.blog/hecto/)

- This is a series of blog posts that shows you how to build a text editor in Rust. 
  - It’s a re-implementation of kilo in Rust

## 🦀 [My Experience Building an Editor in Rust _](https://jimmyhmiller.github.io/editor-experience)

- 
- 

- I tried out lots of interesting ideas and they worked pretty darn well. But I think my biggest takeaway is that there is so much opportunity here. Text editors have largely remained unchanged in terms of user experience. Now with language servers, they can offer better static analysis and refactoring tools, but the ways of interacting with them have largely not changed.
# more
- [Rich text editors from backend perspective](https://habr.com/en/articles/533956/)
  - in this article I’m going to overview the most popular types of rich text editors, tradeoffs of their use from a backend perspective
  - Streaming of content from the rich text editor to other infrastructure tools like full-text search, warehouses, etc.
  - Retrieving of content to clients: mobile, web, desktop.
  - Storing of content in some kind of storage (SQL database in my case)
  - Analyzing of content, which includes point 1, but also analyzing it from the perspective of our application
  - My hybrid solution
    - As I don’t find any Json based free editors, and there was not enough markdown functionality, I decided to make a hybrid solution.
    - I use a rich text editor, but I implement parsers on the backend side so that I have my custom JSON structure inside the backend as well as raw HTML structure.
    - I have enough flexibility, because even if text editor implementation will change — it won’t affect guys who use JSON content type from the backend, because it remains the same, but yes, I would need to update the parsers.
    - As a trade-off — it costs because you need to implement parsing from HTML to JSON and vice versa along with tests
    - JSON costs more space in your storage, but as I said, the choice of editor is about trade-offs.
    - Have you seen GoogleDocs developers.google.com/docs/api for inspiration. Looks well structured and at least well documented for me

- [[方案]造一个富文本 简介](http://luo0412.gitee.io/core/nav.4-2.ui/ch5-toolbox/02-5047253998648002.html)

- [哔哩哔哩 从零开始的富文本编辑器（上）_slate_202209](https://www.bilibili.com/read/cv18606877)
  - [哔哩哔哩 从零开始的富文本编辑器（下） - 列表-图片_slate_202210](https://www.bilibili.com/read/cv19147722)

- [重学编辑器 - 掘金](https://juejin.cn/post/7231476258163900476)

- [How to choose a text editor for a digital-first newsroom?](https://autentika.com/blog/how-to-choose-a-text-editor-for-a-digital-first-newsroom)

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

- [Over 14 years of todos recorded in text: My productivity app is a never-ending .txt file](https://jeffhuang.com/productivity_text_file/)

- [前端富文本基础及实现, 偏综述，基于contenteditable+document.execCommand](https://juejin.cn/post/7124839474575441934)

- [WebAssembly 在在线文档分词场景中的解决方案](https://github.com/YingshanDeng/wasm-cppjieba/issues/1)

- [VS Code、ATOM这些开源文本编辑器的代码实现中有哪些奇技淫巧？ - 知乎](https://www.zhihu.com/question/272156541/answers/updated)

- [Web富文本编辑器演进 - 掘金](https://juejin.cn/post/7116899761340284936#heading-11)
  - vscode 的编辑器（monaco）是基于L2实现的

- [从零写一个富文本编辑器（二）——文档模型 - 掘金](https://juejin.cn/post/6934368266382999565)
  - [从零开始写一个富文本编辑器（一） - 掘金](https://juejin.cn/post/6924346082797289480)

- [富文本编辑器：TinyMCE、Editor.js、Lexical、CKEditor与CodeMirror对比 - ercwang](https://0x763ad28bc4436590fd61998561730b0f7790e955.xlog.app/TinyMCEEditorjsLexicalCKEditorCodeMirror)

- [Ask HN: How to do cross platform GUI? | Hacker News](https://news.ycombinator.com/item?id=24242412)

- [Future Text Publishing](https://futuretextpublishing.com/)
  - The aim is to inspire a powerfully rich future of text in a multitude of ways today, and for the work to still have value in a thousand years & beyond.
