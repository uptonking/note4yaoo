---
title: lib-editor-slate-community-stars
tags: [community, slate-editor]
created: 2022-05-15T18:41:58.641Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-community-stars

# guide

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render
# discuss
- ## 

- ## 【 Heterodoc 编辑器 】支持自定义 Emoji 显示
- https://twitter.com/Shenqingchuan/status/1649622854705758208
- 这个功能的定制需要 ProseMirror 的更进阶的知识，我也踩了很多坑。比如 mark 的 左边默认且不可改 inclusive 需要加零宽字符、用 Mark 实现时需要保证一个 Emoji 一个 Mark 等等 ...

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

- ## I work at Notion and recently rebuilt much of the editor core, _202206
- https://news.ycombinator.com/item?id=31814983
  - and I don’t think Slate is a good choice because it considers nice, simple code more important than CJK or Android support. 
  - Notion doesn’t use Slate or any other editor framework. I just study a lot of editor core code.

1. Android also has a browser. It is an important platform with many users.
2. Building an editor is so complicated that most organizations want to do it only once. They build a web editor, and wrap it in a native app. The shell like file browser, sharing screens, etc are “native” but the editor surface is a webview. This is how Quip, Dropbox Paper, Google Docs, Notion, etc work. Even iOS worked this way initially for all editable styled text (per https://twitter.com/kocienda/status/1400484473540513792?s=21&t=9Ac5954Qlz-NG-qf4kre2Q)
3. If you are going to bet the core competency of your business on a framework, it’s important to understand the motivations and limitations of said framework.

- Slate has a nice, approachable API from a React perspective. I think depending on your project it could be an okay trade off.
  - I co-wrote a post about our editor internals after finishing up the recent re-work but we decided not to publish it to conserve our Competitive Advantage.

- What are your thoughts on TipTap?
  - Since it doesn’t implement editing itself I haven’t studied its source. Under the hood it’s ProseMirror so it should be okay, although I’d be uneasy about stacking abstractions too high: Your code —> TipTap React —> TipTap Extension —> ProseMirror Plugin —> ProseMirror Core —> DOM feels like there’s a lot of incidental complexity to learn all of the APIs across these layers. Right now the docs site is returning HTTP 502 to me 

- ## [tinymce: execCommand() is deprecated. What will TinyMCE do?_202203](https://github.com/tinymce/tinymce/discussions/7718)
- This API has been deprecated for a long time. Many many websites depend on it, it's not going away anytime soon. 
  - Having said that the majority of the calls to execCommand within the TinyMCE codebase are handled internally not by the browser. 
  - We might look at renaming the method in a future release to clear up this confusion.
  - Our long-term plan to address this deprecation is the new editor model developed for real-time collaboration: https://www.tiny.cloud/blog/real-time-collaborative-editing-slate-js/
  - Once the model is ready for general use it will be added to our open source offering and the plan is it will eventually become the default for TinyMCE.

- ## [Store paths instead of keys on selection data for `set_selection` operations](https://github.com/ianstormtaylor/slate/issues/1567)
- In a collaborative environment, keys can appear and disappear, but paths can be transformed and stay valid. In order to support both collaboration and undo / redo, set_selection needs to store both the old selection and the new selection as paths, instead of keys.
- Yep, for OT I'm already completely ignoring keys

- ## [consider using paths instead of keys_201711](https://github.com/ianstormtaylor/slate/issues/1408)

- PROS
  - For many things, like "find node by key", the "find node by path" equivalent would actually be much quicker, since you wouldn't have to search the entire tree, you'd just know exactly where to descend by just following the path.
  - It would also make operations expressed in the same terms as the local changes are applied.
  - When inserting fragments or nodes, we wouldn't have to do the current behavior where we iterate all the new nodes, insuring that their keys aren't already in the document—which would save performance.
  - I think a lot of the logic in the "at current range" transforms that determines what the selection will be after the change has applied could be simplified, because path changes are deterministic, compared to key changes which cannot be guessed ahead of time since they are unique.

- CONS
  - Finding a node in the DOM currently searches for its "key", which doesn't change across renders. But if paths were used instead then whenever a node was inserted, each node after it would have to re-render to update DOM attributes. This could potentially be mitigated by moving the key generation into the view layer, as a view-level concern instead of the data layer. Keeping it around only for locating nodes in the DOM.
  - To update a specific node, you no longer have the key reference. 
    - This could be solved by either searching for the node instance itself (with the same performance). 
    - Or it could be by passing the path to places that need the node. The path approach is awkward though, since it means the information needed can change without the node itself changing. But that's okay, because comparing by instance would work still I think, so not really an issue.

- Right now we use the concept of unique "keys" to keep track of the anchor and focus of a node in a range. And we use them to look up a node by key in the document, for updating, etc.
  - But keys are local-only, and once we convert the change information into operations, we convert "keys" into "paths", which are just an array of indices that locate a node in the document—like [2, 1, 2]. Because these don't rely on local information.

- One alternative would be to actually keep the keys, but move to using paths for most of the internal things and for operations. This might be the best of both worlds, keeping lookups fast for things like change.insertText() and so on. But allow the more precise ByKey(key, ...) behavior to persist across changes. Although those ByKey methods would be much slower by comparison. 

- I don't really depends on keys in my use case, but paths do have similar problem domain with operation transform: all paths that are stored in memory have to be transformed if an operation is performed on the editor, in order to maintain its integrity. 
  - I think translation between keys and paths might be simpler and saner implementation while improving internally using paths. If it ever reach a point where key become obsolete, it could be remove then?
- I was thinking of not storing any of the path information in the node itself. So the only things that keep paths are referencing the node from outside itself, like a range. I'm not totally sure I understand the second part you mentioned, but I agree that if there are ways to transition without removing the keys that make it much easier, we should definitely consider them

- the place I'd be most worried about would be anywhere where you grab a node, run some changes, and then get updated nodes by key from the new change.value for the rest of your function. Right now, keys make that easy. It'll take more thought without them, to make sure your paths or nodes are still valid.
  - very good point. Normalizing currently uses this technique.

- I am in favour of keeping keys, because it makes it possible to have a completely different data structure for the data storage - that doesn't necessarily map 1:1 to the Slate structure. With keys you will always know exactly what to target. I would actually prefer if the the operations too dealt with keys in stead of paths. We store and patch our documents a completely different format and using the operation's paths can be a challenge sometimes to know what do target in our document structure.

- https://github.com/TheGuardianWolf/treepack
  - v1 of changing the index of an object causes a lot of adding and deleting. This is a limitation of the path based scheme.

- ## [Unique identifier for Nodes_202002](https://github.com/ianstormtaylor/slate/issues/3489)
- the API was rewritten to effectively not rely on keys to locate nodes anymore, instead this is done with paths. 
  - This alleviates the need for the API to recursively search the node hierarchy to locate a node by its key and is a performance improvement. 
  - If you would like to bind keys to your nodes, the API allows this because you can freely add arbitrary properties to your nodes as you see fit (as long as you don't run into name collision with properties on the core interface). You can use this to write your own locate by key utilities and then that should yield you a path. 
- A good example on how to do this can be found in the embedded example.

- ## [How to have unique node ids?](https://github.com/ianstormtaylor/slate/discussions/4462)
  - to have a unique, stable identifier for each node.

- I have a similar problem in my project where each node has a unique id, but it would not work correctly when copying and pasting.
  - My solution was to override editor.insertFragment which could be called when pasting node and mark these nodes, then I am able to know which nodes are pasted and modify their ids on `onChange`.
- a general idea on how to archive something like this in a performant way by intercepting `editor.apply`. 

- plate提供了参考方案
  - https://www.npmjs.com/package/@udecode/plate-node-id

- ## [Collaborative editing](https://github.com/ianstormtaylor/slate/issues/259)
- I've started some preliminary exploration of a slate-ottype library
- The rich-text ottype isn't quite expressive enough to encode a Transform object, because it's limited to just insert, delete, and retain (format). It's fundamentally a string with attributed ranges rather than a tree structure.
- The json0 ottype isn't sufficient to granularly express the operations indicated by a Transform object. As a list of operations, however, it seems like a relevant starting point.
- Comparing the approaches taken by rich-text and json0, I quite like the "sparse traversal" format of a rich-text delta over the "list of operations" format of json0 as a way to encode a changeset. The time complexity of a "sparse traversal" should be lower than that of a "list of operations" implementation. 
- If taking the "list of operations" approach, is seems like there needs to be a transform function for each pair of fundamental operation types. With 13 different operations (addMark, insertNode, insertText, joinNode, moveNode, removeMark, removeNode, removeText, setMark, setNode, setSelection, splitNodeAtOffset, splitNode), that's 78 different functions (13 choose 2)! Is that right? Maybe there are some shortcuts or symmetry to take advantage of.

- ## [next v0.50, remove immutablejs_201911](https://github.com/ianstormtaylor/slate/pull/3093)
- Plugins are now plain functions that augment the Editor object they receive and return it again.

- ## [remove all `key` usage from Slate's core](https://github.com/ianstormtaylor/slate/issues/2864)
- Right now we use keys all over the place, because we didn't use to have "paths" as a concept. 
  - Often the key usage is a crutch( 依) for logic that can be made even simpler and more performant by using paths—although this isn't always true. Either way we need to eliminate keys to for #2495 to be able to remove the instantiation step.

- ## [switch from immutablejs to plain JSON models_201812](https://github.com/ianstormtaylor/slate/issues/2495)
- [consider migrating from Immutable.js "Records" to plain objects](https://github.com/ianstormtaylor/slate/issues/2345)
- immutablejs-cons
  - makes debugging harder.
  - Reading values is more expensive
  - requires a fromJS step to build the collections/records

- ## [Modeling RichText with Automerge](https://github.com/automerge/automerge/issues/193)
- I have spent a while thinking about this too, and I also think that a single document sequence with marker characters is the way to go. 
  - If you represent a document as a tree, there are a lot of operations that require deleting and re-inserting nodes (e.g. hitting enter in the middle of a paragraph, causing it to split into two paragraphs), which don't merge well in a concurrent setting. 
  - If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence.
- My intention was that Automerge. Text should be usable for this purpose. That is, I want Automerge. Text to be able to contain marker objects as well as characters from the text
- Maybe I am overlooking something, but "If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence." means we can not express tree structures. I can not imagine WYSIWYG without at least an anchor which has to be split as well.

- there is new development going on: next month, @geoffreylitt and @sliminality will be kicking off a research project to figure out the best way of handling rich text in CRDTs such as Automerge, with the support of the @inkandswitch research lab. 

- ## [Lazy loading Slate components that are offscreen?](https://github.com/ianstormtaylor/slate/issues/3234)
- Closest thing we can do now appears to be:

```JSX
return (
  <LazyLoad
    placeholder={<MyPlaceholder {...attributes}>{children}</MyPlaceholder>
    <MyActualComponent {...attributes} />
  </LazyLoad>
)
```

- ## Dynamic Rendering Feature (performance improvement); only render visible blocks and not render blocks hidden within the y-overflow.__201705
- https://github.com/ianstormtaylor/slate/issues/790
- The Ace Editor: ajaxorg/ace does this by rendering two divs: 
  - a full height "scroller" div and then a "content" div that dynamic adjusts based on scrolls while updating it's content (removing hidden dom nodes and adding newly shown dom nodes).
  - https://github.com/ajaxorg/ace/blob/master/src/virtual_renderer.js
  - https://github.com/clauderic/react-tiny-virtual-list

- I don't think it's possible to arbitrarily render any part of a Slate Document at a given scroll position because it is difficult, possibly impossible, to tell how much space a Slate block will take until after it is rendered. 
  - Ace editor is an editor for monospace text so it is easy to predict how much space text will take before we render it.
- That said, what could work and could improve performance, is to render the visible portion of the page first before giving control back to the user. The rest of the content could fill in afterwards.
  - I think this might be a good low hanging fruit. Just render up to the visible portion, then use setTimeout to render a few blocks at a time for the rest without blocking the UI.

- For anyone needing this, I would highly recommend looking into other performance improvements in the general rendering case first, because they are probably much lower-hanging fruit.

- Rendering is very fast, almost instantly, with or without react-window, and deserializeHugeText is also fast. But before rendering, loading it to slate is slow.

- Interested to know everyones thoughts on a deferred rendering method (Such as described in this article on Twitter Lite)

- ## 📝🏘️ [Slate – A completely customizable framework for building rich text editors | Hacker News_202107](https://news.ycombinator.com/item?id=28000086)
- The recent changes to the API in 0.50 look good. The number of iteration passes really shows. Out of the available open source editor frameworks, 🆚️ Slate is probably most similar to Notion’s internal editor system. If I had to rebuild on a framework tomorrow, it’d be Slate or ProseMirror. Still if I used Slate it would be with the expectation that I’d end up owning an aging fork of a forgotten version at some point.
- I've been using Slate heavily this year. I'm not a Slate developer, but I've read a lot of the source code, follow all the Github issues, etc., and I'm "owning an aging fork".
  - I ended up forking only the React part of Slate, which is officially a plugin, and massively rewriting it to support virtualized windowing, so we can work with very large possibly complicated to render documents. I also added fairly generic realtime collaboration support. This is currently used in https://cocalc.com for WYSIWYG editing of Markdown documents. I also have plans to extend my use of Slate with windowing to Jupyter notebooks and other document types.
  - I chose Slate over Prosemirror because the source code of Slate is Typescript written in a clear modern style, and I was able to start reading any part of it and understand it easily, whereas I find Prosemirror's core source code more difficult (this may just be a reflection of my shortcomings). I spent a lot of time initially just reading Slate PR's claiming to fix bugs, then integrating the PR's into my fork, often in a way that makes sense for my project, but likely wouldn't in general (I left helpful remarks on Github).
  - I have no plans to switch from Slate to Prosemirror. Getting virtualized windowing to work with Slate was quite difficult, but it's really table stakes for what I plan on doing longterm, and I don't even know where to begin to do virtualized windowing in Prosemirror.

- How does virtualization play with text search? Did you end up having to roll your own?
  - Yes, I very much have to implement my own text search. There are many custom elements, so I would have to roll my own anyways at some point.

- What features of Slate put it closest to Notion's editor compared to other frameworks besides the obvious one that Slate's view layer is built on top of React? Is it somehow that Slate is more suitable handling asynchronous data (e.g. server generated uuids for each block, recursively fetching content for each block and its children)?

- Initially started with Quill, but Quill is really limited and for example can't support rich text inside tables, only simple text.
