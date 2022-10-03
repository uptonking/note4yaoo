---
title: lib-editor-prosemirror-community-stars
tags: [community, editor, prosemirror]
created: 2022-08-30T01:46:03.984Z
modified: 2022-08-30T01:46:22.149Z
---

# lib-editor-prosemirror-community-stars

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## props to plugin views__202206
- https://discuss.prosemirror.net/t/props-to-plugin-views/4672
  - What’s the best way to pass props into plugin views so that they update when props change (not only when state changes)?
  - I mean plugin view specific props. Like if user preference for accent color is stored higher up in the app, and its passed as a prop to a view for a plugin. Not editor state props, basically.
  - [Some thoughts on Prosemirror's API to improve it](https://tanishqkancharla.dev/thoughts/prosemirrorapi)

- Plugin views have their `update` method called as normal when the editor’s props change. Except when the state is reconfigured—then they are destroyed and recreated entirely.
- That sounds like a concept entirely outside ProseMirror. 
  - 👉🏻️ Put it in a state field and update it when it changes using a transaction, if you want to tie it into ProseMirror’s update cycle.

- This is Prosemirror tied into a bigger system, and the problem I’m having. 
  - I can’t pass props i.e. app state (or app services, but I didn’t show them here) into editor plugin views.
  - Like state about the theme colors, or global user font preference, etc.
- Here are four possible options to fix the problem.
- You can use a “props” plugin which goes into the editor state, and you just have to make sure to update it every time the app state changes.
- The second option is to just lift plugin views out of prosemirror and just make it your app view’s responsibility. 
  - Now you just read the plugin state through the editor state and use whatever services you need. 
  - Basically you make it the App’s responsibility to render the plugin views.
  - This is, imo, the “right” approach. 
  - In an ideal world, you shouldn’t even need the EditorView component when integrating Prosemirror into a bigger system. 
  - It gets replaced by the App view and EditorState gets rendered as part of it.
- The third approach is using observables/subscriptions like cole suggested or in my initial post. 
  - I didn’t bother to figure out how to draw this, but in mount you pass in those subscriptions as the “initial” props to the Editor View.
- The fourth approach is inventing some new concept in Prosemirror to support this. I’m not really sure what it would look like; Maybe the EditorView becomes a function of state and props where props is any object.

- Plugin views have their update method called as normal when the editor’s props change. Except when the state is reconfigured—then they are destroyed and recreated entirely.
- That sounds like a concept entirely outside ProseMirror. Put it in a state field and update it when it changes using a transaction, if you want to tie it into ProseMirror’s update cycle.

- ## I'm curious what you would consider "Prosemirror regrets" -- things that you'd do different or things you dont like about the current implementation
- https://twitter.com/moonriseTK/status/1487832468308774918
- Writing correct document-changing commands, especially schema-agnostic ones, is ridiculously hard right now. 
- Also the extension system is not as powerful as that in codemirror 6.

- Can you talk more about the formalisms ProseMirror adopts that you admire?
  - I'm still discovering it but mostly the transaction and NodeView systems. Make it really easy to add custom behaviour. I just added checkbox support for my notetaking app in a few lines of code.

- ## Remove contenteditable completely?
- https://discuss.prosemirror.net/t/remove-contenteditable-completely/1766
- using contenteditable for rendering/cursor tracking reduces complexity by avoiding the need to implement layout. 
  - However, this means **ProseMirror is not aware of where things are rendered on the screen**.
  - For most use cases, this is not a problem. 
  - However, this makes implementing certain features that rely on knowing where things are rendered more difficult. 
  - From what I’ve seen, commercial close-sourced word processors such as Google Docs and MS Word Online handle rendering/cursor tracking instead of delegating to contenteditable.
- Some example use cases:
  - Break up document to fixed-size pages

    - can’t do this without knowing the height of each line being rendered

  - Multiple cursor placement in collaborative editing

    - the browser can only render one cursor, to render multiple cursors we need to be able to project document position to screen coordinates, expensive to do without having rendered layout information cached

  - More sophisticated marks such as inline highlighting and commenting 

    - as far as I know, marks in ProseMirror are rendered by wrapping inline text with spans and decorating the wrapper spans, 
    - if you want to render more complex structures, such as a popover comment box centered/above the highlighted text, you’d have to render the highlight as a span, and then determine the wrapper span bounding box position after the mark is rendered and append the popover comment box, which I think is a workaround to the system

- I have been exploring the possibility of handling layout/rendering instead of delegating to contenteditable. 
  - It seems this involves breaking up the document into boxes that cannot be broken up further and laying them out as lines with the document’s size constraints, before finally rendering them. 
  - I don’t think this can fit with the current APIs of ProseMirror, since the concept of box and layout are missing and model toDOM simplify returns DOM specifications with no layout information.
  - Is there any recommendation for bridging the gap here? I’d love to use ProseMirror for its beautiful model and state implementation, but I’d also like to have more control over the view layer.
- I was hoping there might be a way to implement a custom view layer that deals with layout. But if not, I’ll take a stab at implementing this as a different project.
  - https://github.com/yuzhenmi/taleweaver
  - I’ve been experimenting with this, now I can better appreciate why you’re using contenteditable, it does greatly simplify capture of inputs, especially for mobile.
  - My requirement is to be aware of where things are rendered, so that there is more flexibility with fixing the page height and rendering complex UI overlays on top of the document. 
  - I no longer think it conflicts with adopting contenteditable.
  - I’m starting to experiment with determining the document layout (words + lines + pages) myself but have them inside a contenteditable, and expose an API that allows convenient/efficient conversion of document position to screen coordinates (and vice-versa). Any thoughts on this approach? 
- I’m curious how you’re planning to do the positioning, and how you’ll address the potential disruptive effect on the editing experience this may have. 
  - You might be able to get quite far with decorations adding CSS (or even break nodes) to specific elements in the document.
  - I don’t expect the core library will be doing things like this, but if you find a promising approach and run into problems caused by the library, we can certainly discuss them.
- I’ve been experimenting in a new project without prosemirror as a dependency.
  - So far, the same model implementation seems to work - I’m using the same flat token model for applying transformations, and I’m constructing a tree model from the tokens for convenient access to nodes.
  - When it comes to the view layer, things start to diverge. I’m introducing the concept of “words” - a range of tokens that cannot be split for line wrapping. A list of “words” is constructed for each block-level node, and each word may reference multiple inline nodes (if, say, the first half of a word is bolded and the second half is not). The screen size of each word is then computed. Knowing the width of each word and the width of the document, I group them into lines.
  - I’m also playing around with adding “pages” to the document. With lines built from words, I then group lines into pages, based on the height of each line and the height of each page.
  - I haven’t looked into performance optimization yet, but the screen size of each word is cached. With this information, I’m able to map document position to screen coordinates and vice-versa without repeatedly calling getBoundingClientRect.
  - As for cursor handling, I’m still experimenting, but it seems it’s better to let the browser capture cursor-related events and we can map it to changes to the cursor state. 
  - And for rendering the cursor, I think it’s more useful to do it ourselves, since there is little cross-browser/device concerns. 
  - This is assuming there is only one editing cursor that we need to listen to events for, which I think is a fair assumption for WYSIWYG. 
  - For collaborative editing, additional observing cursors can be easily rendered the same way as the editing cursor.
  - Not sure how exactly this can fit with prosemirror yet. The view module would have to be completely replaced. The Node class will probably also have to be modified, since right now it defines to-DOM for the node. I don’t think there is much conflict with the other modules.

- All the editing apps need to use contenteditable to some extent because certain text editing features (IME, etc.) don’t really work without it. 
  - It is true that some hide contenteditable a lot more than others, but as of today, one cannot live completely without it. 
  - There have been some early proposals by some of the major vendors to add more basic level support for editing in browsers over the last few years, but so far it has all been at an early draft stage and it did not develop beyond that.

- Honestly, I wish the specification for contenteditable would better handle primitive positioning and selection problems, 
  - you wouldn’t believe the amount of CSS & decoration stuff I had to code to get something even-approaching word-style selection behaviour.
  - In terms of complex UI overlays, inline highlighting/commenting, etc. I thought I’d pipe in, you can quite nicely implement sophisticated overlays with decorations and Vue.js where that’s concerned.
  - Obviously, you can switch out Vue and implement reactivity with a different framework

- ## [主流的开源「富文本编辑器」都有什么缺陷？](https://www.zhihu.com/question/404836496/answers/updated)

- [关于 slate 和 prosemirror_by-杨振兴](https://www.zhihu.com/question/404836496/answer/1319381793)
- 美团的学城、印象笔记的超级笔记都是 ProseMirror。
  - 另外，PM并不是一个开箱即用的编辑器，需要写Schema定结构；其渲染出来的内容是完全的html；标准用法就是按照Schema中确定的结构来渲染DOM，特殊用法比如表格，或者自定义元素渲染可以使用 Angular、React 这种做视图层。
- 我必须要再提下最新 slate 5.* 以上的版本，大概做了下面几件事：
  - 使用TypeScript重构。
  - 使用immer替换immutable，数据就是纯粹的JS对象，调试的时候再也不用.toJS()了。
  - 新的插件机制，以前的插件机制我定义为仿洋葱模型，包装了太多层的调用栈，新插件机制就是简单的高阶函数实现的，很容易就能定位到代码实现。
  - 使用WeakMaps记录DOM元素与Node节点与节点Path之间的关联，不再依赖于nodeRef以及DOM的data-key属性。
  - 不得不说新的API更优雅了。
  - Slate最核心的针对数据处理操作基本实现测试覆盖
- 特别想研究Prosemirror是因为Confluence的编辑器技术用的是Prosemirror
  - ProseMirror是CodeMirror作者打造的另外一款编辑器。
- 区别一：定位不同
  - Prosemirror是一款可以直接用的编辑器，而Slate是底层框架，它不提供编辑器功能实现和预设
- 区别二：框架
  - Prosemirror是基于原生JS和HTML的实现，而Slate是框架之上的产物。
  - 看过一些Prosemirror实现的介绍，它也有虚拟DOM的概念，它的设计思想、基于编辑器业务的地位，类似于React之与它之上的业务地位是一样的，粗略的认为Prosemirror和React是同级别的。
- 区别三：可扩展性
  - Slate的扩展能力更强，主要是想说它的实现方式更多更灵活、更容易理解，不是说Slate能做而Prosemirror做不了。
- 区别四：细节处理
  - 因为定位不同，所以Prosemirror无疑更稳定有些特殊场景Prosemirror处理的非常到位。
  - 比如Slate中最困扰我的就是块级元素前后无法设定焦点的问题（没有焦点就无法在元素前后按Enter创建空段落），前后有焦点会让编辑器使用起来更流畅，这方面语雀做的最好，Prosemirror也提供了一个gapcursor的模块专门处理这个问题
- 时间已经来到2021年，不得不说真快，主要更新下前面提到的闪烁的焦点问题，这个需求在Slate中已经有方案，而且交互效果要比Prosemirror的gapcursor要好一点点，足以体现Slate的扩展能力还是可以的

- 基于 contentEditable 的主要可能有以下问题：
  - 格式不可控，
    - 如加粗一段文字，在html里有很多种实现
  - 难以对内容做序列化，基本只能以html为输出
  - 在编辑过程中会很容易产生脏标签及数据，基本很难做到干净的输出
  - 选区操作及复位，
    - 比较老的如KindEditor直接bug遍地
  - 对后续扩展基本不怎么友好
- 脱离 contentEditable，基于抽象数据结构的
  - 因为数据结构或架构上的限制，可能有很多格式或插入内容实现不了
  - 因为很难覆盖所有操作，可能在某个时间点或操作点上，出现难以预料的bug
  - 性能，由于基本都是由数据模型渲染到视图，其中的更新算法基本都会造成性能问题

- 美团学城，其富文本编辑器是基于prosemirror来实现的，我在其中开发了内部团队接入版本及当前正在开发的block化新版本。
- prosemirror的schema系统还是非常强大，主要分为marks及nodes两类，整个文档是由nodes构成的，schemaSpec定义了节点自身类型(inline / block等)及其所能包含的nodes类型（content），marks是对inline content比如(text*)的一种修饰
- pm有一个默认的设定：inline和block在schemaSpec的content中是不能mixed的
  - 一个典型的例子就是list标签的tab嵌套，这要求li的content是ul这类block级别的schema - list，所以哪怕是纯文本的输入，也必须加上paragraph这类block级别的schema - paragraph
  - 纯文本的li标签下必须有paragraph标签，这会导致类似列表居中在内的一些布局因为这层paragraph异常。
- 渲染层是富文本编辑器很重要的一层，在prosemirror中非文档内容的渲染由decoration层完成，而文档内容的渲染由toDOM或者nodeview来提供，
  - toDOM适合轻量的展示如blockquote、link等，对于复杂如calendar之类的节点，nodeview的能力就体现出来了，毕竟谁也不喜欢在toDOM里写一大堆的冗余的无法理解的节点关系
- 对于Decoration层，widget、inline及node的api能非常便利的处理placeholder等简单渲染，
  - 在复杂节点渲染上还是不得不依靠reactDOM.render等方式hack或者以直接以node+特定attribute的方式去代替decoration实现比如上传附件在内的中间态。
- 另外decoration的contenteditable=false属性还非常容易带来浏览器的各类光标问题，overlap的decoration的互相感知能力不足。decoration的事件机制缺乏，导致在decoration在更多的场景下仅仅能处理非常简单的渲染。
- 麻烦的光标系统。。。prosemirror的indexing系统是一套基于整型的下标索引，在整个html标签和textcontent层面精细化的索引系统
  - 如果希望获取基于pos位置的详细信息，通过Node.resolve能获取到该pos下的详细信息。
  - 由于富文本编辑的过程就是在文本的什么位置做了什么操作，所以编辑过程中所涉及到的插入，拖入，拖拽，拖出，光标选区，复制，粘贴，macro等都需要pos的信息。
  - pos => Node，pos => Dom， pos => resolvedPos, 都具备强大的api，但是Node作为编辑器对文档节点的描述，Node节点实例并不直接包含实例的pos。
  - 所以prosemirror mutation API几乎都以pos和dom为参数，posByNode很多时候不得不接触child，forEach，descendants等api转化，如果能支持互相的映射会极大的便利开发。pos <==> Node.
- prosemirror中的选区有textSelection，nodeSelection，allSelection，充分的支持了选区range的不同情况。尽管在contentDOM这类边界情况下的选择还有一些奇怪的非预期行为(部分来自浏览器，部分来自prosemirror)，总体是完善简单直接的，配合schema中的spec还能丰富节点的各种行为。即使如此，代码中还是不可避免的会有pos + 1, pos - 1等不怎么优雅的代码。咋说呢。。。pos +- n, n > 2就做好注释吧。。
- 由光标产生另一个问题就是，prosemirror是基于plugin/extension去开发的，各个plugin/extension可以利用很多的工程化能力让他们解耦和可插拔，在cursor这类基础功能插件中，如果真的有很多自定义特定node的边界光标要处理，还是要尽量避免耦合，这可能不是一件很难的事，但是是一件很麻烦的事。
- plugin系统极大的丰富和扩展了编辑器的行为和能力。
  - 除了定义鼠标键盘行为以外，每个plugin可以维护自己的state，这有点类似react中state的感觉。
  - 对于prosemirror来说，setMeta/getMeta/getState/apply 等API可以方便的修改和获取state，并且是可以跨越plugin去操作的。
  - 但是有一个明显的感觉是，react中setState及单向数据流让组件状态的修改和影响范围可控又较易于理解，
  - 然而在prosemirror中这种基于链式的插件事件流体系下，配合上view层及nodeView层，使得状态的变更起始点和终结点不直观，
  - 对于复杂的插件，比如键盘唤醒的可输入搜索菜单，基于plugin state的维护终究还是略显杂乱。
  - 不过prosemirror plugin系统带来了极大的开发和设计自由度，并不完全是缺陷。
- 复制的之后的走向分为对内粘贴和对外部粘贴两类，由于上述的schema及parseDOM的解析规则，对内粘贴剪切板slice只要携带必要信息就会自动重走pm的解析逻辑，类似二次加载，所以不存在展示和适配问题。
  - 但是对外粘贴的兼容（如复制到word，wps等）如果仅仅基于clipboard html就很难做到适配和兼容了，比如富文本编辑器中的附件卡片，如果复制到word中下载事件和卡片本身可能就无法被word理解解析了。
  - 这就涉及到对剪切板的修改过程让内容同时满足对内对外的支持，prosemirror的这个能力主要来自clipboardSerializer层，形式上等同于schemaSpec的toDOM，这一层可以理解成在复制场景的特殊转移规则，
  - 可以想象，一个形态为`<div data-attachment-link="xx" class="pm-attachment" />`如果希望在word中也是一个可以被理解的附件链接，那么在复制的时候自然是希望在剪切板中的内容是`<a src="xxxx">attachment filename</a>`。 
  - prosemirror的ClipboardSerializer API的设计很好的补充丰富了schema。
  - prosemirror在设计上很多的API既可以实现在plugin也可以直接整合至EditorView, 在不同的维度上很方便的支持了场景化的需求。
  - 总体来说，prosemirror对剪切/复制等行为的支持程度还是不错的。
- 基于crdt算法的yjs对prosemirror提供了y-prosemirror库，在prosemirror编辑器中的操作都被映射成yjs的type比如yxml的变化，客户端ydoc的变化在各端同步op，作用于各端的ydoc进而变成prosemirror的transaction。
  - 相关的另一个方案就是prosemirror-collab官方库，prosemirror是一套mvc的模式，对state的修改触发view的渲染，修改state的方式为dispatch transaction，有些类似redux的工作方式。
- collab库就是基于transaction的各端同步，区别在于yjs的ydoc接管了文档的形态，基于op/update还原文档的操作历史而不是传统的json或者htmlstring，
  - 这使得prosemirror的tojson在yjs方案下的实时编辑编辑器中变得略显鸡肋，也让server（非node）端对文档的掌控力大大削弱，比如清洗文档id，过滤不和谐内容等等变得复杂。
- 另一方面，基于transaction的方式，编辑器能在操作维度上做到非常细粒度的控制，例如version或者操作历史等方面。
  - 在没有实时编辑的版本，我写了一个基于结果(base、 remote、 local)的automerge合并逻辑以替代之前的合并冲突逻辑，但是这种基于结果的历史版本对比仅仅能在内容的差异上完成对比，颗粒度最小也仅仅能在childNodes级别，
  - 如果涉及到Node. TEXT_NODE，由于基于结果diff本身的颗粒度限制，在string层面实现单字节这种操作变更展示几乎不太可能，
  - 但是如果借助yjs的update或者pm transaction，就能在单用户维度上完整展示编辑历史和操作过程
- 这种区别本质上是把文档视为某个确定时间点上的状态，还是一个时间轴上的操作集合。
  - 基本上，实时编辑在用户体验上无疑更好，但本质更是对非实时文档无法解决的问题的一个解决方案。
- hex2rgb、br标签，unicode等问题在富文本编辑过程中也是常见问题，部分来自浏览器默认处理行为，部分来自prosemirror本身的逻辑限制。

- 首先说下我会注重从定制二次开发方面来评价，而不是开箱即用。
  - 另外我只是对这两个项目进行了调研和写了几千行DEMO，并没有最终完成产品化
- schema
- ProseMirror是有schema的，所以定义好了schema以后ProseMirror可以替你实现自动化parser，但是对于结构不好的数据，parse过程中可能会丢弃大段的内容，这样以来如果你希望你的编辑器能够支持从别的编辑器里粘贴东西进来还能尽可能保持格式，就会有点头疼。
- Slate是无schema的，意味着它实现简单，但容错能力就看二次开发者的normalize以及反序列化的过程下多少功夫了。如果遇到上面那种需要支持粘贴来自别的编辑器的富文本的情况，可以写各种兼容逻辑，只要舍得花功夫，堆代码量，可以有更高的上限。
- 光标系统
- ProseMirror使用的是一个整数来“绝对定位”一个光标，它的好处是光标本身的定义是描述元素之间的“缝隙”的，这非常符合直观感受，并且在表示光标的线性移动，比如“向右移动5下”这种场景会很好实现；但是算法实现复杂，在表达“父节点”、“兄弟节点”、“第i个子节点”这些看起来很直观的操作的时候也需要一系列运算。
- Slate使用的是path数组+offset来表示光标。基本上优缺点反过来，在实现基于树的变换的时候很直观也很简单，但在线性移动会比较复杂。表示“缝隙”会不那么直观，尤其是需要表示两个相邻顶级元素，比如[0]和[1]之间的“缝隙”的时候，需要一些技巧，导致算法显得不那么“洁癖”。
- ProseMirror对于节点的定义比Slate更完整，比如Slate里的void元素竟然还要求返回children，简直搞笑。而ProseMirror里可以良好地定义void，以及所谓isolate。
  - 比如两个`<td>之间的“缝”是不能容纳光标的，这样的逻辑，ProseMirror可以通`过schema定义来描述，而在Slate里就得靠自己去normalize
- 另一方面，ProseMirror对于选区的定义比Slate来得更加完整，它的“选区”可以是普通的range，也可以是node，也可以是多range（比如现在很多代码编辑器都支持多光标）。
  - 而Slate只支持单range，node selection是靠一些技巧与特殊逻辑搞出来的，多range则没有提供，
  - 这样一来，Slate是无法准确还原W3C的DOM Selection API的，而ProseMirror可以。
- 输入层
- ProseMirror在输入层的API丰富程度完爆Slate，结合ProseMirror强大的选区定义，可以实现很多复杂的光标与选区逻辑。
- 二次开发难度
- 最重要的是光标算法相关，ProseMirror的光标系统设计决定它的算法更复杂，尤其是因为我们平常的理解大多都是“文档树”，而path + offset的光标表达方式是对树结构更友好的
- 另一方面是和外部业务系统开发过程的结合。
  - Slate新版完全拥抱了React，你可以（也只可以）完全用React来开发定制的编辑器，并且可以把React的UI生态赋能到自己的编辑器上，
  - 比方说你要做一个超链接的节点，点一下可以弹出一个框来修改它的链接，这时候AntDesign的文本框、按钮什么的，可以很容易整合进你的编辑器UI里面。
  - 但这也有一些缺点，一方面是富文本编辑部分（可以接收光标的部分）和编辑器UI（比如内联的属性编辑框、图片尺寸缩放控制柄这类的不接收光标的部分）是混在你的React代码里的，Slate通过一些奇怪的data-slate-*属性来区分富文本和UI
  - 另一方面就是如果你需要基于原生DOM编程（在编辑器这种场景，其实还不少）的时候，因为React拦了一层，就没那么方便了，得到处ref什么的。
- ProseMirror则正好相反，用它的时候你是首先基于原生的JS来开发富文本的部分，
  - 而如果想加UI，它给你一种叫View的东西，你可以用任何方法去实现view，最后抠一块出来，传一个contentDOM回去作为富文本部分。
- 举个例子，上面的图里，是我开发的Tabs组件。
  - 橙色线框是“富文本编辑部分”，因为它们可以接收富文本编辑器的光标；
  - 绿色线框部分是“编辑器UI”，它们只在编辑模式下出现；
  - 而其它那些蓝色的部分是自定义组件的UI，它们会最终输出到文档里，具有一定的可交互行，但在编辑模式下不会接收光标。
- 我个人是比较赞同ProseMirror这种设计的，因为我的设计目标是最终输出的文档内容需要能不借助视图层框架能运行，那么用原生JS来实现文档内容的那些自定义组件是比较合适的。
- 但是Slate那样做也有好的一面，一方面是集成度更高，可以把整个编辑器完全当作一个React组件来使用，给他传prop，监听它的事件，就完事儿了（当然这是理想情况）。
  - 另一方面是可以借助React自身的一些SSR生态更方便地去实现SSR，而SSR对很多文档系统来说都是刚需。

- 做了将近两年的在线PPT，从最初调研到深入扩展，感觉选quill是一个不错的道路，
  - 最初选择quilljs是因为他的扩展性和star量以及相对不错的文档内容。
- quilljs自带一套数据系统来支撑内容生产，parchment和delta。
  - parchment是抽象的文档模型，是与DOM树相对应的树形结构，Parchment树由Blot组成，Blot即是DOM Node的对应物，Blot可能包含结构、样式、内容等。
  - Delta是一个扁平的JSON数组，用于保存（描述）编辑器中的内容数据，delta中的每一项代表一次操作，它能很清晰的告诉你当前选中的文本是粗体还是斜体，以及文本内容。
- 如果想要保留一些word的样式等，可能需要你去改造clipboard模块了
- 后面一直对第三代编辑器念念不忘，第三代编辑器的特点：
  - 使用XML严格定义数据
  - 编辑时，数据层与视图层分离
  - 不依赖原生的selection/range，自实现NoteRange和NoteSelection方法
  - 不依赖contenteditable，自实现中间层对接输入法
  - 细粒度的undo/redo，占用更少的内存

- 稍微深度的用过 Draft.js，淘宝内容平台的富文本编辑器就是我之前基于 Draft.js 封装的，然后做了一些魔改适应业务需求
- Draft.js 的硬伤在于性能和体验，根源在于它底层的设计和富文本的描述 schema。
  - 它的架构在当时比较新颖，脱离了常用的 contenteditable 的方案，直接按照 React 的模式去做的，
  - 是通过拦截光标和键盘等操作，然后更新到内部 immutable 的 state 上面，然后在 render 出来。通过 immutable 来提升渲染性能。
  - 因此可以在富文本编辑器里面可以渲染任意的 React 组件并且进行交互
- 不过这只能说明 Draft.js 跟 React 生态比较贴合，实际体验相比传统实现会差一些。
  - 首先是这个富文本协议的描述能力，那么基于这个设计，我想渲染一个自定义 React 组件要怎么做呢？就需要用他们的 Atomic 的 block 来实现，其实底层实现就是将 text 变成一个空字符串，然后利用 entityRanges 将这个空字符串指向一个自定义的 entityMap 的值，然后当你写在编辑器里面渲染的组件的时候，就需要通过一个 API 来获取这个 entity 的具体数据，然后作为 props 进行渲染。
- 如果你想要实现一个 inline 的 image 效果你怎么做呢？
  - 官方突发奇想，用 emoji 来替代空格来做 text 区分这种“黑科技”，总之这套协议慢慢变成了限制。
- 基于这个协议和架构，实现中又出了一些体验性问题。
  - 首先就是性能，短一点的内容还好说，但长文章性能就可以体现了，内容越长性能越差。immutable 能提升，但本身也是有大量运算，在大量突然的编辑下，粘贴复制各种操作，仍然能明显感觉到卡顿。
  - 而 contenteditable 的实现，是浏览器原生的实现，不管你内容多长多多，基本你是感觉不到有什么性能问题的，因为浏览器本身就是做富文本内容渲染的，只不过让你可以改一些内容而已，所以性能很好。
  - 还有就是 React 重新渲染的过程中一些刷新状态可能会被触发，比如知乎的编辑器编辑的时候就会闪烁。。
- 糅合了大量自定义block等的内容，光标就变得很难处理了
- 那么 Draft.js 这类编辑器一无是处吗？
  - 当然不是。如果你的编辑器需要限制内容类型不能胡乱插入内容，并且需要存储结构化的数据而非 HTML，Draft.js 等仍然是可以选择的。
  - 因为使用 contenteditable 意味着你需要 parse 大量的 HTML 场景来控制，而且内容比较静态，难以在表面之外附加 meta 信息，你需要设计隐藏的 HTML 属性来存储而且还要验证，攻击伪造也很简单，直接查看源代码改一下提交，而 Draft.js 等的设计，天然的就解决了这个问题。
- 所以还是要根据业务特性来选择最佳方案，没有最好，只有更合适。
  - 淘宝内容平台当时的需求就是为了保证质量对内容形态和能力有强约束的规范，一步步放开，不同于微信公众号自定义程度很高，所以 Draft.js 还算是比较合理的选择。
- 其实除了现在的这些编辑器的实现，前段时间开始使用 Notion，发现他们的思路也挺有意思。
  - 也是翻看了下他们的代码了解了下，他们是将每一个元素每一块都当作一个独立的 block，然后内容部分使用一个 contenteditable 的 div 来实现更新，解析你输入的字符来做特殊处理和转换。
  - 这种实现也非常有意思，直接将富文本的复杂性降低了几个层次，尤其是对光标的处理等。
  - 当然也有致命缺陷，没法实现 inline image 这样在传统富文本编辑器天然支持的需求。
  - 但仍然是挺适合他们业务场景和受众的设计，不过对长文章性能也有点问题。
- Notion 通过教育用户别去用 Inline 图片，降低了实现难度，甚至现在大家都开始搞模块化笔记了，未来再无 Inline Image
- Inline图片可以的，用entity
