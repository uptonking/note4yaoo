---
title: lib-editor-prosemirror-blog-stars
tags: [blog, editor, prosemirror]
created: 2021-10-12T08:12:56.213Z
modified: 2023-03-02T14:25:34.817Z
---

# lib-editor-prosemirror-blog-stars

# guide

# blogs-pref

## 🌰✏️🎨 [从浏览器源码开始实现 Canvas 富文本编辑器 - 知乎 _202307](https://zhuanlan.zhihu.com/p/642703113)

- https://github.com/WaiSiuKei/neditor /MIT/202308/ts
  - https://waisiukei.github.io/neditor/
  - rich text editor aimed at running in Canvas.
  - 在事件模型和 DOM 模型都准备好之后，移植 ProseMirror 就非常容易了。

- 作为行业的跟随者，效仿业界的标杆公司去做同样的事情往往会让你在技术评审中胜出。
  - 因此，我也选择了走向同一条技术路线：在浏览器中运行另一个浏览器。

- 最终，我发现了 YouTube 的 Cobalt 项目，它能够运行 HTML5 标准的子集。
  - 他们最初也是维护一个基于 Chromium 移植版，但为了在游戏主机、机顶盒等资源受限的环境中实现基于 HTML5 的视频浏览和播放应用程序
  - 他们从头开始构建了一个简化的 HTML 子集实现和 CSS Box 模型所需的代码，没有使用复杂的 Blink 内核，也没有使用 Chromium 复杂的合成器和渲染管线的代码。
  - DOM层：这是实现 W3C 标准子集的地方，可以支持常用的 HTML 标签，布局方面支持流式布局和 Flex 布局。 
  - 布局引擎：基于 DOM 树计算布局树，并进一步生成用于指示绘图的渲染树，以发送到渲染器。 
  - 渲染器/Skia：渲染器遍历布局引擎生成的渲染树，使用 Skia 图形库对其进行绘制、光栅化输出

- 在将 Cobalt 内核移植用于渲染后，我可以使用 HTML 来描述 DOM 结构，然后渲染内核就可以在 Canvas 元素内绘制出界面内容，但是这只是一个单纯的数据展示层，我还需要完成完整的架构设计，将各个分层模块组合起来才能形成富文本编辑器。

- 我使用了 Vue 来构建 DOM 树。然而，在现在这个基于移植的虚拟 DOM 的富文本编辑器中，我们可以选择一些没有虚拟 DOM 层的前端框架（例如 Svelte），以减少不必要的层级。我选择了 Pettie-vue 项目，它类似于 Vue，可以将响应式对象转换为想要的页面，但比 Vue 更简单，更容易移植到我所定义的虚拟 DOM 层上。

- Model -> ViewModel -> View（DOM 树）-> Layout 树数据 -> Render 树数据
- 上述搭建的 MVVM 架构只完成了编辑器使用链路中的半条链路——将数据更新到视图，而另一半链路是如何通过用户在视图上的鼠标键盘交互来更新数据。
  - 在解决后半条链路的问题时，首先需要解决的是如何将 Canvas 内的鼠标键盘事件发送到外部这个问题。
  - 如果直接在对象上添加事件监听器，会让编辑器忙于增加和删除事件监听器，这样的设计会非常麻烦。在前端开发实践中，一种解决这种问题的方法是采用事件委托。例如，VSCode 的 Monaco 编辑器内部的事件模型，也使用事件委托的方式在 View 层集中处理事件。

- 在完成了上述事件机制之后，我回头结合之前研究的浏览器源码来对 ProseMirror 进行移植。
- Cobalt 源码中没有 Chromium 中所有与文本编辑相关的部分，但是两者都是基于遵守 HTML 标准去实现 Node、Text、Element 和 HTMLElement 这些类。
  - 这使得我可以直接从 Chromium 的 Editing 模块中复制与 Range 和 Selection 相关的代码来使用。
  - 在事件模型和 DOM 模型都准备好之后，移植 ProseMirror 就非常容易了。

- 作为一个练手项目，这个编辑器已经验证了将浏览器应用移植到 Canvas 中的可行性。

## ⚡️ [ProseMirror Collab Performance | Blog _202307](https://stepwisehq.com/blog/2023-07-25-prosemirror-collab-performance/)

- https://github.com/stepwisehq/prosemirror-collab-commit /MIT/202307/ts/inactive
  - Commit-based collaborative editing plugin for ProseMirror.

- ProseMirror-Collab collects unconfirmed steps and sends them to an authority so they can be recorded to the document’s source-of-truth. 
  - this is the exact issue people hit early on with prosemirror-collab performance; some producers get starved out by constant authority rejection while others are getting their changes in consistently.
- In 2020 user benaubin wrote on discuss. ProseMirror about creating a new commit-based collab backend. 
  - The technique was based on a referenced Apache Wave paper. This ended with the release of prosemirror-collab-plus which has not been updated since August 2020.
  - The gist is that we can batch updates(steps) into commits, apply those as the atomic changes on the back-end, and map/apply the commits on the back-end instead of rejecting them and sending them back to the clients.
  - With this, client round-trip latency no longer factors into accepting or rejecting updates; client commits can be applied in the order they arrive based on any committed document version
- We took the ideas from prosemirror-collab-plus, the Apache Wave paper, and built a new plugin based on the structure of prosemirror-collab. 
  - This new project has brought over the full test suite from prosemirror-collab, with some tweaks to account for server-side step mapping

- https://news.ycombinator.com/item?id=36959889
  - A commit-based collab plugin that's far more performant under heavily active client loads than stock. I'm a fan of YJS, but not a fan of state-based CRDT layer on top of ProseMirror for my use cases
  - I also translated the core ProseMirror projects of model, transform, and test-builder to C#
  - I spent quite a bit of time as an FTE building out a robust-ish and efficient Yjs backend POC. 
  - At the end of it all my personal takeaways were:
  * State-based CRDT isn't great when you want a central authority in the mix anyway and are fundamentally trying to work with operations
  * The exchange rate between ProseMirror's currency, steps, and some other replication strategies building blocks is too high
  * ProseMirror should add the concept of range-relocation to its mappings; this is a bit of an aside but it would help retain user intent when reconciling concurrent edits involved in block relocations
# 💬 [Prosemirror: Highlights & Comments_202205](https://medium.com/collaborne-engineering/prosemirror-highlights-comments-20ce820149ed)

> Model highlights/comments as marks instead of annotations to allow for collaborative editing
> We open sourced our annotation feature as a Remirror extension

- tldr
  - 默认用marks实现comment或highlight
  - 对于需要自定义颜色形状的comment，marks中只保存id
  - 飞书的comment不参与undo/redo，但高亮/背景色很可能需要

- When we built our initial version of highlighting, we modeled them as annotations: We stored the highlighted sections as a separate data structure in our database. 
  - Each highlight contained a.o. the position where it started and where it ended (from/to). 
  - On opening the editor, we injected the highlights as Prosemirror decorations. 
  - Whenever a highlighted section changed, we updated the database accordingly.
- Collaborative editing allows multiple users to work in the same Prosemirror document. 
  - We shared the two data structures about the same document via two communication channels: The Prosemirror changes were distributed via yjs/webrtc; whereas highlights were written directly to the database and then sync’ed back via websocket subscriptions.
- And this blew up annotations in every way possible.
  - For a starter, the **communication channels have very different latencies**: webrtc is basically instant while calling database and awaiting can take 1–2 seconds. This meant that the document might have already been updated whereas the highlight still pointed to the old position. 
  - Worse, if one of the channels failed, we ended up with a corrupted document.

- We concluded that both data structures had to be communicated via the same communication channel. 
  - Luckily, yjs isn’t Prosemirror-specific but provides generic shared data structures.
  - This allowed us to add the array of highlights to the yjs document, and get both data structures sync’ed together.

- This did indeed resolve our biggest synchronization issues. 
- Unfortunately, those had just shadowed everything else that could go wrong with our annotation-based approach. 
  - For example, copy/paste works flawless in the Prosemirror document but supporting the same for highlights proved to be a nightmare. 
  - Undo was another really hard one.

- In the end, we concluded that communicating both data structures via the same channel alone could never fully solve the issue. 
  - What we need was to merge the data structures: Instead of storing highlights separated from the Prosemirror document, we had to store the highlights as part of the document.
- To achieve this, we attach a Prosemirror mark to the highlighted text. By making the highlights part of the document, the from/to positions are bound to be correct.

- What complicates matters: We have to show highlights also outside the context of the document. 
  - For this, **we still need to store the highlights in a database**, so we can easily query them. 
  - Yet, the database contains only derived data: The source of truth is always the Prosemirror document. 
  - So, even if data gets out of sync, it will be eventually consistent.

- One final challenge came when users wanted to add some highlight meta data outside the context of the editor. 
  - For example, change the color of the highlight. 
  - This meant that the Prosemirror document can’t be the source of truth for the complete highlight. 
  - Instead, we define for each highlight field what the source of truth is. 
  - For the color, we store in the mark only an ID identifying the highlight but the color itself is stored directly in the database.

## 💬 [If I want to implement the comment function, is mark the best way?](https://discuss.prosemirror.net/t/if-i-want-to-implement-the-comment-function-is-mark-the-best-way/3831)

- Keeping the comments in a data structure outside of the doc and showing them as decorations might make them easier to manage when they can cross block boundaries. 
  - But using marks should also work, especially if you want them to be part of the document and automatically included in collaborative editing and the undo history.

- Can mark customize a view? Similar to nodeview
  - No, marks can’t do most of the things nodeview can. You can only change the element used to render the mark.

- In my experience it’s best to move this functionality “out” from ProseMirror, a mark just stores the threadId, and make a plugin which captures clicks in the editor, checks if the click was on a “thread” mark, if that’s the case then it sets it’s internal state the thread’s id & position. 
  - Then you watch editorState changes, and if the “thread” plugin is signaling that you’ve clicked on the mark then you display the thread component in whatever framework you’re using.
  - You will need posAtCoords / coordsAtPos to determine the thread component’s position / to get if the click was inside a thread mark.
# [ProseMirror - 入门_lastnigtic_202008](https://lastnigtic.cn/prosemirror-first/)
- prosemirror-model：
  - 负责prosemirror的内容结构。
  - 定义了编辑器的文档模型，用于描述编辑器内容的数据结构，并实现了对编辑器内容的一原子的操作。
  - 实现了一套索引系统，用于处理位置信息。
  - 同时提供了从DOM -> ProsemirrorNode的Parser以及反向的Serializer。
- prosemirror-transfrom：
  - 负责对编辑内容的修改操作。文档的改动由step实现。
  - transform基于step封装了一系列对内容进行操作的API。
  - step执行了对文档内容的操作，通过StepMap记录了改动的信息，可用于追溯位置的变化。
- prosemirror-state：
  - 负责描述整个编辑器的状态。
  - 包括文档内容，选区信息，所有的节点类型以及并基于Transform实现了Transaction，Transaction主要增加了对选区的管理以及状态记录。
  - 同时提供了强大的插件系统，实现用户对状态更新流程干预的可能性。
- prosemirror-view：
  - 负责视图的渲染，实现了从state到视图的渲染。
  - 监听或者劫持用户的操作并修正，并创建相应的对state的改动，最终比对dom与state的决定最终渲染结果。

- prosemirror 中渲染出的节点必须在 Schema 中有相应的定义，而 Scheme 中的可以定义的节点分为两种，node和mark
- Node
  - 常规意义上的节点，分为块级或者是行内。

```JS
paragraph: {
  group: "block",
  content: "text*",
  parseDOM: [{ tag: 'p' }],
  toDOM(node) { return ['p', 0] }
}
```

- group 表示其为 block 组；content 表示其可以包含任意文字；
  - parseDOM 表示其解析`<p>xxx</p>`；
  - toDOM 表示其渲染为`<p>xxx</p>`，子节点从 0 的位置开始插入
  - content 是一个类正则字符串，可以使用 node 的名称或者是 group 名

- Mark
- 主要作用于行内节点，用于给行内元素增加样式或者附加其他信息，他不像 Node 会占据文档位置，更像是一种对文档描述的补充

- Attributes
  - Node 以及 Mark 都可以附加一些信息，但需要在初始化是定义好支持的属性
  - attrs 中包含 align 的 paragraph 节点，可以用作单纯的信息存储，也可以配合 toDOM 修改渲染输出。

- prosemirror的内容被描述成一棵树，他的特征属性（isBlock、isInline 等）由我们所定义的节点特征来确定
- Node 的 content 由一个 Fragment 表示，Fragment 的 content 则是由 Node 组成的数组，prosemirror 通过这样嵌套形成的树形结构来描述一个文档。

- prosemirror 实现了一套索引系统用于表示文档中某个位置，主要分为两种：
  - 第一种是比较像是访问 DOM，利用 content 的数组的特性去访问节点，把文档当成一棵树去遍历。
  - 第二种是强大的索引系统，把文档打平后的索引，prosemirror 文档中的任何位置，都可以用一个唯一的整数表示。
- 在 prosemirror 的索引系统中，把这棵树打平了，规定：
  - 整个文档的第一个节点前的位置为零。
  - 进入或离开不是叶节点（即可以包含其他内容）的节点视为一个 token。因此，如果文档以一个段落开头，则该段落的内容开头算作位置 1。
  - 文本节点中的每个内容都使做是一个 token。
  - 叶子节点（不能包含其他节点内容）也视作是一个 token。
- 按照这个规则，想象我们有一个指针，从开头 0 开始进入一个节点时索引加 1，每越过一个文本内容加 1，退出一个节点时也加 1，通过这样的形式，就可以描述文档中的每个位置。
  - `nodeSize` 可以理解为我们的指针从进入到退出节点时走过的距离

- 如何修改文档
  - 可以是修改doc的content属性或者是直接修改文字内容亦或是删除内容后再插入，我们选择第一种方式来实现。
- prosemirror中的数据更新实际上都是对 state 的修改，通过 state 提供的 updateState 的 API 接受一个新的 state 来更新 state，编辑器实例 view 中帮我封装好了这一步操作，对外暴露出来的 API 是 dispatch。
- 修改文档的操作是由prosemirror-transform来实现的，而prosemirror-state中的tr属性继承了 transform，state 又是作为prosemirror-view实例的一个属性
  - 所以更新操作都可以通过 view 来实现，翻阅API 文档，看到`replaceRangeWith`这个 API 符合我们的需求，
- replaceRangeWith 做了什么操作呢？
  - 实际上创建了一个 ReplaceStep 去修改文档。
  - step对文档的修改不一定是成功的，结果由 StepResult 表示，
  - 如果失败了，会抛出一个 TransformError，
  - 如果成功了，则会返回新的文档的内容，
  - transform 会把旧文档内容保存在 `docs` 属性中，新的应用到 `doc` 属性中，并把 step 保存在 steps 属性中，可以实现撤销的操作。
- 最后通过 dispatch 更新到 state。
  - 因此，我们可以把 state.tr 可以看成是一个事务，每一个 step 可以看作是一次原子操作，通过 dispatch 提交事务并应用到 state 上生效，实现了对文档的修改。

- [ProseMirror - 入门](https://zhuanlan.zhihu.com/p/263454334)

- prosemirror中渲染出的节点必须在Schema中有相应的定义，而Scheme中的可以定义的节点分为两种，node和mark，
- node即为常规意义上的节点，分为块级或者是行内
- 定义一个'paragraph'节点：
  - group表示其为block组；
  - content表示其可以包含任意文字；
  - parseDOM表示其解析`<p>xxx</p>`；
  - toDOM表示其渲染为`<p>xxx</p>`，子节点从0的位置开始插入，更多的配置可以查看NodeSpec，
  - content是一个类正则字符串，可以使用node的名称或者是group名。

```js
paragraph: {
  group: "block",
  content: "text*",
  parseDOM: [{ tag: 'p' }],
  toDOM(node) { return ['p', 0] },
  attrs: {
    align: {
      default: 'left'
    }
  }
}
```

- Mark主要作用于行内节点，用于给行内元素增加样式或者附加其他信息，
  - 他不像Node会占据文档索引位置，更像是一种对文档描述的补充。

```js
bold: {
  parseDOM: [{ tag: 'strong' }],
  toDOM(node) { return ['strong', 0] },
  attrs: {
    align: {
      default: 'left'
    }
  }
}
```

- attributes对Node以及Mark都可以附加一些信息，但需要在初始化时定义好支持的属性
- prosemirror的内容被描述成一棵树，他的特征属性（isBlock、isInline等）由我们所定义的节点特征来确定
- Node的content由一个Fragment表示，Fragment的content则是由Node组成的数组，prosemirror通过这样嵌套形成的树形结构来描述一个文档。

- prosemirror实现了一套索引系统用于表示文档中某个位置，主要分为两种：
  - 第一种是比较像是访问DOM，利用content的数组的特性去访问节点，把文档当成一棵树去遍历。
  - 第二种是强大的索引系统，把文档打平后的索引，prosemirror文档中的任何位置，都可以用一个唯一的整数表示。
- 在prosemirror的索引系统中，把这棵树打平了，规定：
  - 整个文档的第一个节点前的位置为 0。
  - 进入或离开不是叶节点（即可以包含其他内容）的节点视为一个token。因此，如果文档以一个段落开头，则该段落的内容开头算作位置1。
  - 文本节点中的每个内容都使做是一个token。
  - 叶子节点（不能包含其他节点内容）也视作是一个token。
- 按照这个规则，想象我们有一个指针，从开头0开始进入一个节点时索引加1，每越过一个文本内容加1，退出一个节点时也加1，通过这样的形式，就可以描述文档中的每个位置。

- 我们来尝试修改文档的数据。我们来把官网的内容替换成Hello Prosemirror！。
- 我们要做的可以是修改doc的content属性或者是直接修改文字内容亦或是删除内容后再插入，我们选择第一种方式来实现。
- prosemirror中的数据更新实际上都是对state的修改，通过state提供的updateState的API接受一个新的state来更新state，
  - 编辑器实例view中帮我封装好了这一步操作，对外暴露出来的API是dispatch。
- 上面我们说到修改文档的操作是由prosemirror-transform来实现的，而prosemirror-state中的tr属性继承了transform，state又是作为prosemirror-view实例的一个属性。
  - 所以更新操作都可以通过view来实现，翻阅API文档，看到`replaceRangeWith`这个API符合我们的需求，
  - 根据上面的分析，实现节点替换的操作

```JS
const { dispatch, state } = view;
const { schema, tr, doc } = state;
const { paragraph } = schema.nodes;
// 创建一个新的文本节点
const textNode = schema.text('Hello Prosemirror!');
const newParagraph = paragraph.create(undefined, textNode);
// 触发更新
dispatch(tr.replaceRangeWith(0, doc.content.size, newParagraph));
```

- transform对文档的操作都是通过step去实现，所以这一步实际上创建了一个`ReplaceStep`去修改文档。
- step对文档的修改不一定是成功的，结果由`StepResult`表示，如果失败了会抛出一个TransformError，如果成功了，则会返回新的文档的内容，
  - transform会把旧文档内容保存在`docs`属性中，新的应用到`doc`属性中，并把step保存在`steps`属性中，可以实现撤销的操作。最后通过dispatch更新到state。
  - 因此，我们可以把`state.tr`可以看成是一个事务，每一个step可以看作是一次原子操作，通过dispatch提交事务并应用到state上生效，实现了对文档的修改。
# [ProseMirror - 如何对state进行修改__202010](https://lastnigtic.cn/posts/prosemirror-state-modify/)
- doc就是当前整篇文档的数据内容，
  - doc是一个Node类型元素，Node可以理解为prosemirror文章树中的一个节点，代表着一个文档中的元素。
  - Node包含一个content属性，代表它的子节点，是一个Fragment类型的元素，它代表着一个文档片段，可以理解为当前节点的所有子元素的一个集合。
  - prosemirror通过Node以及Fragment类型完整地描述文档中数据内容。
- selection
  - 当前文档中选取的信息，由于contenteditable对光标位置的处理不尽如人意，所以绝大多数的编辑器都会维护自己的选区信息，用于抹平浏览器原生处理带来的问题。
  - prosemirror中提供了一个Selection基类，并在此基础上扩展出TextSelection，NodeSelection，AllSelection这几种 selection 类型，也支持自行扩展出其他类型。
  - 与浏览器自带的 selection 类似，prosemirror 中的 selection 也存在 anchor，head 用于指示选区方向，标明选区在文档中的位置，
  - 并且提供了强大的ResolvedPos结构，可以获取当前选区位置在文档中的各种信息，包括位置，当前相对于上层元素的路径，相邻元素等等信息，可以方便地对文档内容做处理。
- tr(Transaction)
  - Transaction继承自Transform，Transform 代表着对文档的一系列操作，每个操作的原子为一个Step，
  - 每个 Step 都提供了 apply，invert，merge 等方法（支撑 prosemirror 的协同编辑），step会保存当前操作的Slice内容，生成新的 doc 并把旧的 doc 信息存储在 tr.docs 属性中，tr 关注的 doc 内容本身，而不关心具体 selection 的位置。
- Schema
  - schema这种包含当前文档所支持的所有内容，分为 node 和 mark，node 即使元素类型，mark 可以理解为是 node 的附加属性，更多是相当于一种标记，常用于标记加粗，斜体这类属性。

- State 更新过程
- prosemirror-view是prosemirror中另外一个核心模块，主要负责处理着用户与编辑器交互行为，更新state以及state渲染到 DOM。
  - 首先我们先了解一下prosemirror是如何监听事件的
- 中文输入时 + 空格
  - IE，Chrome，Safari：触发keydown，不触发keypress
  - keyup > keydown > beforeinput > input
- 中文输入时 + enter
  - keyup > keydown > keypress > beforeinput > input
- 英文输入时
  - keydown > keypress > beforeinput > input > keyup
- 非字符键
  - 会触发keydown，不会触发keypress
- 经过上面的分析，我们可以看到，使用keypress事件来作为输入监听是比较合适的，可以区分大小写，不会重复触发，且非字符键也不会触发。
- prosemirror中对于输入事件的处理也是通过的keypress的监听，keydown和keyup主要用于监听一些功能按键。
  - prosemirror中使用的的是charCode这个属性用于获取输入的内容

```JS
editHandlers.keypress = (view, event) => {
  if (inOrNearComposition(view, event) || !event.charCode ||
    event.ctrlKey && !event.altKey || browser.mac && event.metaKey) return

  if (view.someProp("handleKeyPress", f => f(view, event))) {
    event.preventDefault()
    return
  }

  let sel = view.state.selection
  if (!(sel instanceof TextSelection) || !sel.$from.sameParent(sel.$to)) {
    let text = String.fromCharCode(event.charCode)
    if (!view.someProp("handleTextInput", f => f(view, sel.$from.pos, sel.$to.pos, text)))
      view.dispatch(view.state.tr.insertText(text).scrollIntoView())
    event.preventDefault()
  }
}
```

- keypress事件发生时，prosemirror会判断当前selection是否是TextSelection或者光标的起始和中止位置是否相同为了判断选中了内容，选中了内容需要进行删除处理）
- 简单的输入事件prosemirror进行一个insertText的操作去修改state。会调用 replaceSelectionWith()
- insertText可以选择在当前位置插入或者选中位置插入，插入的逻辑就是替换当前选中的内容，还有一些处理就是继承插入位置的 mark 属性，插入后选区的位置处理等。
  - 可以看到两个处理分支的最后都会流向replaceRangeWith这个方法，不同在于一个需要删除当前选区位置内容，一个要删除指定位置的内容而已。
- slice是文档的一个切片，代表文档的一个片段，保存着文档的片段信息以及节点嵌套的深度信息。
- 可以看到replaceRange的主要工作就是找到到适合插入的位置，进行插入操作。
- replace创建了一个step去修改doc的内容。在prosemirror中，所有对文档的修改都是由Step去实现的，在Step.apply中调用了Node.replace的方法，
- 实际上的操作都是对Node的操作， 通过cut，replace，slice等方法构造出一个新的节点。
  - 可以看到了close返回的一个新的节点，这个节点的content是复用旧的数据。
  - 这样 prosemirror 就实现了一个简单的 immutable 结构，既可以保存修改前的文档，又不会占用过多的内存。

- 对于中文的输入，由上文可以知道，各个浏览器的实现不一致，
  - prosemirror判断到当前在composition事件时，并不做具体处理，而是使用MutationObserver，监听到到DOM的变化，具体的判断比较复杂，这里不做详细说明，但最后还是会转换成对state的修改。

- 上面的**更新流程可以简单归结为** 拿到插入的内容 -> 寻找适合插入的位置 -> 返回新的文档。
  - 这里面主要的难点是在寻找适合的插入位置这一步，由于简单的输入depth都是 0，
- 下面详细剖析若depth非零状态下，如何寻找适合的插入位置。
  - openStart和openEnd指的是当前切片的深度  

- prosemirror通过维护自己的文档数据树，并把所有对dom的操作都转换成对state的操作，抹平了不同浏览器带来的数据结构不一致的问题，
  - 并提升了prosemirror本身的视图层的可移植性，理论上可以通过自身实现视图层在任何平台上都实现编辑器。
  - 维护自身文档数据结构也可以说是一个比较主流解决方案，因为它让内容可控，状态可以变，并且为实现协同编辑提供了结构上的支撑。
# [ProseMirror - 从State到DOM__202009](https://lastnigtic.cn/posts/prosemirror-state-to-dom/)
- 使用prosemirror时我们有以下三种定义编辑器内视图渲染的方式：
  - 直接使用 nodeType/markType 中的 `toDOM` 属性，实际渲染由`prosemirror-model`提供的`DOMSerializer.renderSpec`负责
  - 使用 `nodeView` 渲染自定义的节点
  - 使用 `decoration` 渲染与 doc 内容无关的节点

- 从使用者的角度看，我们在doc插入了什么内容，dom中就会渲染出相应类型的内容，这一种方式看起来很像React的数据驱动视图的形式。

- ​prosemirror内部存在一种用于描述视图对象的特殊结构——ViewDesc，
  - 他会绑定在编辑器的 DOM 中的 pmViewDesc 属性上，整篇文档的 desc 挂载在 view 实例的 docView 上。
  - 作者在文档中没有提供这部分的介绍，但这部分时 view 中最重要的一环，直接与我们看到的内容相关。
- 💡 ViewDesc可以看作是dom与编辑器state的中间层，相当于是 prosemirror 的virtual-dom。
  - ViewDesc会挂载到相应的dom的 `pmViewDesc` 属性上，并保存相应的 dom 和 node
- prosemirror-view 总共定义了 7 种 viewDesc：
- NodeViewDesc
  - prosemirror 基本节点的 desc，涉及 dom 与节点的绑定，更新和销毁等
- CustomNodeViewDesc
  - 继承 NodeViewDesc，主要扩展了 update 的判断，以及暴露诸如 select，destroy 等的钩子，NodeView 对应
- TextViewDesc
  - 继承 NodeViewDesc，文本节点的 desc
- MarkViewDesc
  - mark 的 desc，为了简化和可预测，有固定的嵌套顺序
- WidgetViewDesc
  - decoration 的 desc，为 state.doc 中的数据无关
- CompositionViewDesc
  - 联想输入的 desc，用于表明和保护输入节点
- BRHackViewDesc
  - 插入一个 br，用于处理空段落的高度高度问题
- viewDesc主要提供了匹配节点，获取索引，状态标记等等方法，帮助 prosemirror 更好地处理 state 与 dom 的状态同步
- 视图更新
  - 对于prosemirror来说，视图的更新面向的不是用户做了什么操作，而是面向 state。
  - 用户做了什么操作这部分由 DOMObserver 去处理并应用到 state 上，视图显示的状态与 state 强相关，抹平了处理用户行为的复杂性，简化了更新的处理，
  - 但同样会带来一些问题，如对用户的行为无法感知导致的节点不能复用的问题等。

-  这里我们从插入一个节点开始，探究 prosemirror 视图更新的过程。
   - 这篇文章略去 DOMObserver 对 Mutation 的分析，直接从视图更新开始，
   - 假设我们已经拿到了新的 state，接下来我们来分析下 prosemirror 是如何将新的 state 应用到视图上的。
- 拿到新的state之后会调用view.updateState(newState)，updateState会调用docView.update更新视图。
  - docView实际上就是 NodeViewDesc 的一个实例，默认的 NodeViewDesc 的更新方法 update(node, outerDeco, innerDeco, view)
- 这一步会判断当前节点的数据是否发生变化，如果发生变化，返回 false，会重建整个节点。
  - 返回 true 则证明更新成功，进行子节点的更新。
- updateInner会先更新外部的 decoration，然后进行更新过程中最核心的处理updateChildren
- updateChildren
  - 首先会根据 docView 创建一个 updater，主要服务于更新过程（代表当前的节点更新树，拥有子节点的子节点会创建自己的 updater）。updater 中会匹配 docView 中的 node 和 descs，从后往前匹配，保存相同的 desc（preMatched）和最后一个匹配的 desc 的 offset（preMatchedOffset）。
  - 根据 doc 和 decorations 的信息顺序遍历更新，根据匹配到的 node 和 deco 的分别调用 onNode 以及 onDeco 方法更新。
  - 若 updater 中有更新，属性 changed 会被置为 true，并进行子节点的渲染（根据实际的 dom 以及更新后的 descs）
  - 从上面的描述，可以看到最核心的方法在第二部份，我们主要分析下第二步中 onNode 做的事情
- onNode
  - syncToMarks()用于更新 mark。
- 之后便开始对 Node 的更新操作，总结起来就是三步
  - findeNodeMatch：在 updater 中寻找是否有 viewDesc 的 node 等于当前 node
    - （最多匹配当前位置的后四位，不匹配最后一位。至于为什么最多只匹配后四位？可能是出于性能考虑吧，作者没有明确说这一点），若没有，进入下一步
    - 如何确定是同一个节点？主要就是判断是内存地址，节点属性，`decorations`，自元素是否是一致的。
  - `updateNextNode`：若 updater 的 children 中当前位置是 NodeViewDesc 类型，分两种情况
    1. 若在 updater 的 preMatched 中存在且索引 preMatch 加上 preMatchOffset 等于当前 node 再 docView.children 中 index，尝试更新节点，否则视为流转到下一步（这一步这么判断的原因是：如果 preMatch+preMatchOffset != index，则证明 updater 中的数据有误，docView.children 中的数据可能有修改，此时以 state 的数据为准）
    2. 若在 updater 的 preMatched 中不存在，尝试更新节点，否则视为流转到下一步
  - `addNode`：这一步就是直接在 updater 的 children 中当前索引的位置直接插入新创建的 viewDesc

- 渲染到视图 renderDescs(parentDOM, descs) 
  - 若有需要重建的节点或者删除的节点，updater.changed 会被置为 true，进入 dom 层面的操作。
  - 此时的操作以 update 后的 viewDescs（此时即为 docView.children）的数据为准，调整当前视图中 dom 展示的节点，不会有位置的调整，不匹配就销毁，不存在就重建。

- 通过上面我们了解 prosemirror 中视图更新处理的过程，实际上就是 state 到 DOM 的过程，prosemirorr 中视图的更新都通过这个过程完成。

## 更新过程

- 基于上面说到的规则，我们分析下以下几种输入行为下的更新过程
- 新增
  - 新增节点不能在 findNodeMatch 找到，会在当前位置重建，
  - 其他的节点都能在旧的 docView 找到，不用重建
- 更新
  - 与新增节点一致，主要区别在于 updateNextNode 这一步，
  - 调用就 viewdesc 的 update 方法，若 update 返回 false，增视为需要重建节点，否则视为成功更新。
  - 若这一步为 customNodeView，我们则可以干预这个过程
- 删除
  - 删除节点后旧的 viewdesc 中能匹配到所有的 node，匹配到 node 会销毁新旧 index 之间的所有的 viewdesc
- 移动
  - 移动的情况比较特殊，跟拖动的距离以变化的位置都有关系（主要和 findNodeMatch 的处理有关系）
  - 把节点从前面移动到后面! 这种情况下，重建的节点会是拖动的节点
  - 把节点从后面拖动到前面，这时候的处理分情况：
  - 非最后一位移动，且距离小于 4，这种情况下，因为 4 在 findNodeMatch 中可以被找到（index: 0, found: 4)，会导致 0 到 4 之间的节点被销毁。所以这种情况下，1、2、3 会被重建，而 4 不会被重建。
  - 最后一位移动或者是距离大于 4，这种情况下，由于 5 不会在 findNodeMatch 中找到，所以会在首位重建节点。匹配到 4 之后遍历结束，销毁剩余节点。所以这种情况下 5 会被重建。

## Mark 更新过程

- Mark 的更新过程与 Node 的更新有比较大的区别，Mark 在 state 中是作为 node 的一个属性，
  - 而在 ViewDesc 中，他则是作为一个高层级的节点，他可以包括其他节点（包括自己本身）, 所以他在 state 和 docView 中的结构是不一致的。
- 而 prosemirror 在对 dom 做渲染时，是以更新后的 ViewDescs 为准，所以 promirror 更新的逻辑是这样：
- 在每次 onDeco，onNode 都会调用`SyncToMarks`
  - 当前有 marks，匹配后两位内是否存在相同的 mark
  - 存在：销毁当前位置与匹配到的位置之间的内容，帮当前顶层和位置推入 updater.stack，位置重置为 0，把 MarkViewDesc 放到 updater.top，开始对 MarkViewDesc 中的内容做更新。
  - 不存在：创建一个新的 MarkViewDesc
  - 当前没有 marks，updater.stack 中有内容，MarkViewDesc 出栈，updater 状态恢复
- 所以会有一个奇怪的现象：当后面第二位有同样的 mark 时，会导致中间的节点没有必要的重建：
  - 这个行为自然是不应该的，作者的解释是为了修复其他bug
  - 重用 mark 时做了更激进的匹配（这也是一个优化的点，贡献代码的机会 XD）。

- ​这篇文章主要讲了 prosemirror 是如 state 与 DOM 之间的关系，举了几个比较简单的例子，
  - 实际情况下，还需要考虑 Decoration 的渲染，mark 与 decoration 与 node 嵌套的渲染，以及 ltr，rtl 的顺序等等的处理，节点的比对和渲染复杂度指数上升。
  - 节点复用在这些情况下无法保证，所以开发一些功能时，不应当依赖某个视图的生命周期。

- 初窥prosemirror的渲染流程，与 react 一样，使用 prosemirror 时我们一般不需要关心到视图这一层，这也是现在各主流富文本编辑器框的一套思路。
- 后面的文章会继续探究用户形如何被捕获，state内部如何更新，索引如何构建等的流程。
