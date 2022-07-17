---
title: lib-editor-prosemirror-blog
tags: [blog, prosemirror]
created: 2021-06-15T00:07:35.640Z
modified: 2021-06-15T00:07:49.228Z
---

# lib-editor-prosemirror-blog

# guide

## [ContentEditable困境与破局 prosemirror的基础实现原理](https://zhuanlan.zhihu.com/p/123341288)

- 现在市面上针对富文本编辑器的方案大概分为以下三种
  - textarea
  - contenteditable
  - Google Doc
- 首先，我们来思考一下，一个编辑器要包含什么？
  - 最基础也要有：可编辑的DOM，外部修改DOM的API
  - 这两个要素浏览器都提供了，分别是ContentEditable和document.execCommand
- contentEditable实际上是浏览器厂商提供的一个富文本编辑器的实现方案。
  - 通过设置一个dom的contenteditable属性为true，可以让这个DOM变得可以编辑。
- document.execCommand
  - 当一段document被转为designMode（contentEditable 和 input框）的时候，document.execCommand的command会作用于光标选区（加粗，斜体等操作），也可能会插入一个新的元素，也可能会影响当前行的内容，取决于command是啥。
- 一个contentEditable的DOM配合document.execCommand可以实现修改DOM的标签，调整DOM的背景色等等一系列操作。

- 厂商实现差异
- 对同一个标准（contentEditable，同时是相对不够完善的标准），各个浏览器厂商的实现方案是不同的。
- 当我们在一个空的contentEditable的dom里面打一个回车，那么预期的表现是什么？换行。那么承载这个新的行的标签是什么？
  - Chrome/Safari 是 div 标签
  - Firefox 在60版本之前，是在当前的行级标签中加一个br
  - Firefox 在60版本之后，趋同于Chrome/Safari，是div标签
  - IE/Opera 是 p 标签

- 不可预测的表现
  - 先回车再换行时可能生成额外标签，如span

- 行内标签嵌套
  - 在没有明确的规则约束的前提下，用户在contentEditable的dom中编写出什么样的结构都是有可能的
  - 视觉上等价，但是在DOM结构上不是等价的。
  - contentEditable生成的DOM不总是符合我们的预期的。

- 基于现代前端框架开发 ui = f(state/data)，操作一个简单的JS对象一定是比操作DOM要简单的，这屏蔽了浏览器差异，规避了DOM复杂的特性。
- 首先，我们在View和command之间引入一个state。
  - 在数据存储层面，我们就不需要维护复杂的DOM结构了，可以用一个JS object的结构去维护当前结构
- 这样的树状的结构导致我们操作跨层级的DOM十分不方便
  - 行内标签实际上并不会影响我们解释完整的DOM结构，那么我们实际上是可以把他作为style处理的，比如 strong 我们可以等价于 font-weight: bold, em 可以等价于 font-style: italic。
- 实际上，这样更符合我们人类对于这段文档的认知习惯，而且无论上面那个dom结构怎么变换嵌套形式，我们都会将其解释成同样的一个state。
- 用户的行为是不可以预测的，editable dom里面出现什么样的结构都是有可能的。这显然不是我们想要的。
  - 有序的，规则化的，可解析的结构才是我们开发喜欢的结构。
- 可以设定规则，可以通过指定什么样的DOM标签下可以出现什么样的DOM标签，什么DOM标签可以拥有什么样的marks来约束用户的输入，在这里称作Schema。
  - 如果用户的输入产生了不符合我们设定的schema的标签结构。我们就忽略它（or 转化成我们认可的标签）
- 通过这样的声明，并将其以某种形式应用到EditorState的生成过程中，将不合规的标签移除掉，那么我们的编辑器就应该只出现符合我们刚才schema定义的规则的内容了。

- 有了能够表示编辑过程中不同时间节点的DOM状态EditorState（被Schema约束），有了能够从State映射到View的方法。那么这个链条中差的就是从 StateA 到 StateB 的过程。
- 引入一个概念叫做Transform（tr），由tr来描述一次变更，这个变更可能是代码中生成的，也有可能是用户在contentEditable进行交互的时候自动生成的。
  - 当我们给一个state应用一个tr后，他应该生成一个新的state，新的state来生成新的View。

- 那思考一下这个tr中应该包含什么信息？
  - 当前的选区信息
  - 当前的文档对象
  - 描述一系列动作的步骤
  - 当前正在使用的marks
- 这实际有点类似batch的概念，并不是每做一次修改就会直接应用到UI上，而是一个完整的事件之后才会被应用到UI上。我们把步骤称为Step
  - step实际上就是我们之前提到的document.execCommand在EditorState上的实现，相当于我们这个编辑器的接口，一般来说要实现的功能集很大
- 什么是当前正在使用的marks
  - storedMarks实际上就是提供了这样的一个位置存储这个数据，上面叙述的Step实现的功能集里面应该也要有addStoredMarks和removeStoredMarks这两个方法。

- 本文叙述的只是最为简单的编辑器的实现思路，在我们实现了足够完整的功能集之后，整个编辑器应该可以像堆积木一样，用这些基础的东西组装成一个复杂的编辑器。
- 除此之外，编辑器的复杂性还在于用户行为不可预测，边界Case太多，要思考出一个完备的，囊括所有可能的逻辑实际上是相对困难的，这一方面就需要我们一点点的去慢慢完善我们的编辑器功能

- 请问一下实现事前同步修改model层如何考虑各种输入法呢？比如再beforeinput的时候可以拦截英文输入法，直接修改model层。但是中文输入法要如何拦截呢？
  - 目前是使用的`MutationObserver`监听变化，如果有变化再映射到model层的

- 我捋一捋，就是更改时先改state ，再把state 的内容覆盖到前面的内容里面？会不会有延迟呢？
  - 是会有的，当数据量大的时候就会更新变慢。
  - 这个时候文章中提到的行内标签转化为mark就有一定的性能优化作用。
  - 然后一般都会借鉴diff算法，更新局部而非全部重绘
- 我专门去看过有道云笔记的html，里面全部都是span+style，每个span都把所有的style写到里面去了。不知道这种做法算哪一类？可能存在什么问题
  - 对于一篇文章来说，html是提供了更加清晰，更语义化的标签的
  - 一般做富文本的话，文章内容是需要后台分析处理的，语义化的标签写正则会方便一些，span+style简直不敢想
# [富文本编辑器Prosemirror - 入门](https://zhuanlan.zhihu.com/p/263454334)
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

```

bold: {
    parseDOM: [{tag: 'strong'}],
    toDOM(node) { return ['strong', 0]},
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
# [探究富文本编辑器ProseMirror（一）绪论](https://marvinsblog.net/post/2018-10-06-prosemirror-1/)
- 基于ContentEditable的传统编辑器
- 传统的编辑器大都是基于HTML的ContentEditable特性做成的
  - ContentEditable其实是HTML元素的属性，若ContentEditable为真，那么浏览器会在相应的HTML元素所述内容区域内显示光标（Caret），允许用户使用鼠标和键盘对这些内容进行修改。
  - 同时，对于用户在ContentEditable区域内选中的内容，可以使用Document.execCommand()函数对选中的部分执行一揽子操作，比如把字体改成粗体，改变对齐方向等等。
- 但是，由于ContentEditable存在的缺陷，要让这些富文本编辑器在不同浏览器下变现得一致，则十分困难。
- 核心问题在于ContentEditable只定义了操作，而没有定义操作的效果。
  - 比如对于字体加粗这个操作，一些浏览器会在需要加粗的字体上加上`<strong>`标签，而另外一些浏览器可能会采取另辟蹊径的做法
- 其次，Document.execCommand()支持的命令，大部分都是基于鼠标选取的。鼠标选取（也就是Selection API）在各个平台的表现也不一致。
  - DOM是树形结构，在网页上选取一些内容，就相当于选取了DOM树的一部分子树。表面上看起来同样的选取操作，在不同的浏览器下可能会选中不同的DOM子树，造成处理上的麻烦。
- 传统的编辑器为了应付ContentEditable操作结果不一致的问题，常常需要重新调整编辑后的HTML内容，才能使ContentEditable的显示效果在各个浏览器中比较一致。

- 基于ContentEditable的新式编辑器
- 这个新的方式是像ReactJS那样，在DOM之上加一层类似VirtualDOM的抽象层。
  - 这个新方式的好处在于，把一部分编辑职能从DOM移到了抽象层。
  - 这样ContentEditable可以只负责在各个平台表现一致的操作，其他操作则由抽象层代劳。
  - 基于这种新方式的编辑器除了ProseMirror之外，还包括Medium.com的编辑器、Slate、CKEditor5等等。
- 采用VirtualDOM有一个大前提，那就是所有需要更改DOM的操作，都需要经过VirtualDOM来协调。
  - 换句话说，所有DOM的状态变化都要经由VirtualDOM统筹协调。这为一些更高级的特性打开了大门，协同编辑是其中一个例子。
# [探究富文本编辑器ProseMirror（二）文档结构](https://marvinsblog.net/post/2018-10-06-prosemirror-2/)
- ProseMirror采用类似VirtualDOM的方式来管理和协调用户交互以及DOM修改。
  - 可以给这个类似VirtualDOM的抽象层娶一个名字，叫做编辑浮层（Editing Surface），简称浮层。
  - 这个浮层要映射到DOM，所以必须也是树形结构，然后这个浮层在概念上又要贴合文本编辑
- ProseMirorr的核心数据是Node（节点），它包含以下属性：
  - type（NodeType类型），指定Node的类型
  - content （Fragment类型），包含了子节点
  - attrs （Object类型），包含改节点的属性
  - marks（Mark类型），包含应用于这个节点上的标记
- 每个节点通过自身的content属性，可以包含一系列的子节点。这个节点和节点之间就形成了一个树状结构，跟DOM的结构类似。
- ProseMirror的节点是用来模拟DOM的元素和文本的，所以ProseMirror的节点也有两种类型， inline, block
- 通常而言，文本节点（text node）是属于平铺类型的节点，它的内容从左到右，从上到下平铺开来；然而包含文本的段落节点（paragraph node）是属于行列类型，它把文字以段落的方式分隔开来。
  - 简而言之，平铺类型的节点是用来包含具体内容，而行列类型的节点一般是用来调整文档的结构。
-一个最简单的ProseMirror文档，甚至可以只包含文本节点（平铺类型），而不包含任何段落（行列类型）。
  这有现实的意义，比如你可以把ProseMirror编辑器挂载（Mount）到一个 `<span></span>` 节点上编辑其中的内容
- 通常情况下，ProseMirror编辑器挂载的DOM元素都是行列类型的，比如`<div></div>`。这时候ProseMirror可以在文档内支持更复杂的节点类型
- ProseMirror文档是根据相应的范式(Schema)派生出来的，
  - 范式定义了文档内有多少类型的节点，节点与节点之间的层级结构，以及与HTML的DOM之间的映射。
  - 这个就像是HTML规范与HTML文档之间的关系，HTML规范说明了什么样的文档可以出现在HTML文档中，以及它们的层级关系（比如`<body>`要包含在`<html>`中）。
  - ProseMirror文档是要在HTML的DOM上建立一层编辑浮面，所以它应该模仿HTML的DOM结构，同时又允许做一定的简化。
- ProseMirror用来描述Schema的方式非常像一个书写一个正则表达式。事实上，ProseMirror也是用类似解析正则表达式的技术（NFA/DFA）来解析Schema的。

- HTML源代码可以看出是HTML树序列化成字符串的一种形式，使其可以易于编辑、保存和发送。
  - 如果给事物编号是一门学问，在于其一，你得知道如何表示事物；其二才轮到如何编号
# [探究富文本编辑器ProseMirror（三）节点类型](https://marvinsblog.net/post/2018-10-26-prosemirror-3/)
- ProseMirror的文档（document）要遵从范式（schema）的要求，就像编程语言里面的一个值都有一个相对应的类型一样。
  - 范式规定了文档的结构，同时也规定的文档的节点类型。
  - 在每个ProseMirror的范式中，最基本的节点类型是文本节点（TextNode），也就是只包含文字。
  - 文本节点的内容一定是平铺（inline）的，但是平铺类型的节点并不一定都是文本节点
- 如果节点没有设置content属性，也就是不能包含其他子节点，所以也可以说这个image节点是叶子（leaf）节点。
- ProseMirror中还有文本块（TextBlock）的概念。对于一个行列类型的节点，只要其包含的子节点集（Fragment）包含的都是平铺类型的节点，那么这个节点就算得上一个文本块
- 一个节点可以既是行列节点，又是叶子节点
  - video默认是行列类型，同时又没有子节点。它显示的时候会独占一行，不会和其他的文字平铺在一起。

- 除了树形层次结构以外，ProseMirror会针对文档中所有节点的内容建立一个扁平的、线性的索引。
- 索引是从左往右，从上往下递增的。其递增规则如下：
  - 文档开头，在第一个节点之前(上面例子的`<p>`之前)，索引为0
  - 进入一个非叶子节点，索引加1（里面例子中的`<p>`之后）
  - 离开一个非叶子节点，索引加1（里面例子中的`</p>`之后）
  - 对于文本节点，每跨过一个字符索引加1
  - 每跨过一个叶子节点索引加1
- 节点的大小也反应了上述的索引规则。对于叶子节点，长度为1；对于文本节点，长度为所包含的字符数目；对于行列节点，就算内容为空，长度也至少为2。
- ProseMirror提供一个resolve方法 ，可以从一个索引值获取当前节点的更多信息

- 平铺类型的节点可以附加任意标记。默认情况下，可以添加任意标记，不过也可以在范式中作出规定，只允许某些平铺节点添加制定类型的标记。
- 所谓标记，主要是用来给平铺类型的节点加上各种格式，比如加粗、加斜体。
  - 另一个例子是给超链接文本加上可以点击的效果。
- 在ProseMirror里面，标记不包括在节点层级中，而只是作用于平铺类型的节点。
- 具有不同标记集合的节点是不能合并到一起的。
  - 以文本节点为例，如果一个文本节点原先包含一段不添加标记的文字，然后中间的一部分文字被加粗了（也就是增加了加粗标记），那么加粗的那部分文字就会分裂出来，形成一个新的带有加粗标记的文本。随之而来的是，前面以及后面的文字也会形成单独的文字节点。这样一来，一个文字节点就分裂成三个文字节点
  - 这时候，如果对前面的文字节点也进行加粗操作，ProseMirror会把前面的节点和中间的节点合并，形成一个更大的文字节点。结果是三个文字节点又变成了两个。

- 在state.doc级别调用resolve(pos)，可以获取全局的位置信息；
  - 如果只是在某个子节点调用resolve(pos)，那么resolve所获得的信息就是相对这个子节点而言的。
- 也可以通过当前的selection来获取resolvedPos
- 假设返回resolve(pos)中的pos在一个文件节点中，由于文本节点被视作是扁平的，ResovledPos拥有的信息其实是关于其父节点的。
- ResovledPos.pos返回resolve(pos)调用中的pos信息。
- ResovledPos.depth表示深度。非文本节点才有深度，所以如果是文本节点的话ResovledPos.depth表示的是其父节点（block类型）的深度。
- 通过ResovledPos.node(ResovledPos.depth)可以返回其父节点
- ResovledPos.parentOffset用来表示当前位码在父节点中的偏移。
- ResovledPos.index()返回当前节点在父节点中的索引。
- ResovledPos.marks()返回当前文本节点上应用的标记集合。
- 通过state.doc.selection.content()可以返回一个slice
# [探究富文本编辑器ProseMirror（四）切割文档slice](https://marvinsblog.net/post/2018-10-28-prosemirror-4/)
- 只要给出起始位置的索引，以及结尾位置的索引，就可以获得文档的一部分切片（slice）。
  - 有的元素被切开了！这在HTML里面可是不允许的，于是要对其进行补全
- 但是补全的标签不属于这个文档切片，所以不能算在其的长度里面。事实上，ProseMirror的文档切片，也就是Slice类型，有两个属性用来表示这些个补全的标签
  - openStart，用来表示多少个标签被补在了切片之前
  - openEnd，用来表示多少个标签被补在了切片之后
- ProseMirror大量使用JavaScript的Array（数组）来存储文档内容。
  - 如果要获取一部分文档内容，其实就是从Array从切割一部分出来，使用的是`Array.prototype.slice()`方法，而这个方法执行的是浅拷贝(shallow copy)
- 如果想要执行深拷贝（deep copy），一个简单的方法是使用ES6新增的`Object.assign()`方法
# [探究富文本编辑器ProseMirror（五）管理改动](https://marvinsblog.net/post/2018-10-28-prosemirror-5/)
- ProseMirror是通过Step来管理文档的改动。
  - Step用来表示一个原子级的改动，既可以应用（apply）到现有文档之上，形成一个新的文档。
  - 又可以撤销（invert），把文档恢复到改动之前的状态。
- 在文档上应用Step不一定会成功，它会返回一个StepResult ，包含一个failed属性，用来指示这个Step是否应用成功。
- 多个Step可以还可以合并（Merge）到一起，形成一个新的Step。
- StepMap记住了文档改动的位置信息，里面记载的是一系列信息，主要包括：改动的开始位置, 改动前的大小, 改动后的大小
- 多个StepMap还可以组合起来，用一个Mapping 类型来管理

- Transform可以把多个Steps累计到一起，把它们逐个应用到文档中。
  - 另外，Transform还保留了一个文档列表。因为采用immutable数据结构的关系，每次应用一个Step，就会产生一个新的文档，但是也会留下一个旧的文档。
  - Transform会把这些旧的文档聚拢在一起，形成一个数组。
- 直接使用Step来修改文档会显得有点繁琐，Transform提供了很多方法来方便文档操作

- ProseMirror用一个新的类EditorState来表示状态。
  - 跟这个相搭配的，Transaction （Transform的扩展类）用来管理针对EditorState的改动。
  - Transaction除了处理文档改动之外，还管理选取范围、当前使用标记集合、还有时间戳等等。
  - Transaction可以直接从EditorState的tr属性来生成。
# [探究富文本编辑器ProseMirror（六）文档视图](https://marvinsblog.net/post/2018-11-10-prosemirror-6/)
- ProseMirror文档在Web页面上的呈现是通过视图 来管理的。其中一个核心的类是EditorView
  - 创建EditorView的时候必须指定文档状态
- EditorView自身的DirectEditorProps 中的属性，以及Plugin集合提供的EditorProps 中的属性有重合的地方，到底依据哪个来决定视图的行为呢？
  - EditorView提供了一个someProp方法，可以按次序（先EditorView然后依次注册的Plugin集合）以一定的逻辑（不同属性逻辑不同）遍历Props集合，来决定视图的行为。

- ProseMirror的文档是一颗节点树，在生成视图的时候就要把这些节点树转化为相应的DOM结构。
  - 但是，ProseMirror并没有直接把文档节点树转化为DOM结构，而是在中间加了一层ViewDesc。
- NodeViewDesc就是用来描述文档中的Node，它的子类TextViewDesc用来表述文档中的TextNode。
  - 虽然在文档中，Mark集合是TextNode（或者其他inline内容）的属性，不参与到树形结构的构成，但是在ViewDesc中，由于是要和DOM树同步，所以MarkViewDesc参与树形结构的构成。
- 其实我们可以把ViewDesc理解为VirtualDOM。ProseMirror通过ViewDesc来保持文档和DOM之间的同步。
  - ViewDesc决定了如何响应DOM事件，并形成相应的Transaction；
  - 另外当EditorState更新之后，ViewDesc又通过更新的EditorState来更新DOM结构。
  - 所以ViewDesc具有双向同步能力，从DOM中同步出ProseMirorr文档，反之亦然。
# [探究富文本编辑器ProseMirror（七）编辑器状态](https://marvinsblog.net/post/2019-06-14-prosemirror-7/)
- pm-state通过EditorState.create来创建实例，而不是直接使用new EditorState。
  - 这是因为创建实例后，pm-state要对实例进行配置，所以需要一个包装函数。
  - 所谓配置，主要是把插件加载到状态集合中。
  - EditorState的实例有一个reconfigure方法，可以对状态进行重新配置。
- pm-state的主状态其实是由各个插件的状态一起构成的
  - 每个插件都向总状态贡献一份⁠StateField的实例，所以主状态其实是StateField的集合。
- 所有插件看到的是一样的config，这个config对象包含了所以其他插件。
- init方法是在EditorState.create的时候被调用的。

- ProseMirror的选段selection是基于其对位移（position）和位置（resolved position）的定义
  - ProseMirror定义了一套虚拟的坐标系统，位移就是该坐标系统中针对0坐标的距离；
  - 位置则不仅包含了位移，还包括节点深度信息。
- 在EditorState.create的时候，可以指定一个选段。不过不指定，默认的选段会设置在文档的开始位置，并且长度为0，坍缩成一个光标。
- 一个选段（Selection）可以包含若干个范围（SelectionRange），但至少包含一个。
  - 一个Selection由基点anchor和头部head构成，一个SelectionRange由起始位置$from和结束为止$to构成。一个选段则有若干个属性
- map()方法可以更新选段的范围，可以在文档被修改后保持选段范围的有效性。
- 选段的getBookmark()方法返回一个SelectionBookmark对象。这是一种与文档无关的选段表示方式，可以用于历史记录中。
- 选段可以有不同的类型，
  - 对于文本的话可以有文本选段（TextSelection）；对于单个节点的话可以有节点选段（NodeSelection）；对于整个文档的话有全选段（AllSelection），
  - 因为前面两种选段类型不一定能够用来表示对整个文档的选择。
  - 每一种选段类型，都对应着一种Bookmark类型。

- Transform以steps的方式管理对编辑器状态的改动，一个Transform就是若干个step的集合。
- 为什么要从Transform类派生出一个Transaction呢？
  - 因为Transform看到的是文档的Model，也就是由pm-model中定义的Model，而不是具体的状态。
  - 所以pm-state要派生出一个Transaction，在Transform的基础上，同时管理当前的编辑状态。
- Tansaction管理的状态的例子包括选段（Selection）、当前激活的标记集（storedMarks）等等。
- EditorState的tr()方法可以创建一个针对当前状态的事务。EditorState的apply()方法可以提交一个事务。
  - 因为EditorState其实是插件的状态的集合，所以apply()其实是让每个插件返回一个更新状态，然后构成一个新的EditorState。
# [探究富文本编辑器ProseMirror（八）视图的状态](https://marvinsblog.net/post/2019-06-15-prosemirror-8/)
- 状态可以嵌套：
  - pm-model定义了文档模型，用来管理文档的状态
  - pm-state定义了编辑器状态类型（state），用来管理编辑器的状态，也就是文档状态加上插件状态。
  - pm-view定义了编辑器视图属性（props），用来管理编辑器视图的状态，也就是编辑器状态加上相应的视图状态。
- pm-view中把props分为两类，一个是DirectEditorProps，另一个是EditorProps。
  - DirectEditorProps是EditorProps的超集，前者包含了编辑器状态（state）以及dispatchTransaction这两个只能由编辑器视图来处理的属性；
  - 后者包含的属性则可以由插件参与或贡献。
  - 之所以区分DirectEditorProps和EditorProps，无非是想保留一两个视图属性，不让外部的插件使用。
- EditorView提供了一个`someProp`方法，可以按次序（先EditorView然后依次注册的Plugin集合）以一定的逻辑（不同属性逻辑不同）遍历Props集合，来决定视图的行为。
  - 因此任意一个插件都可以决定编辑器是否处于允许编辑状态，这是在视图的`getEditable()`中实现
  - return !view.someProp("editable", value => value(view.state) === false)
  - 就是问下所有的插件，看有没有插件不同意当前文档不可编辑的。如果有一个不同意的，那么一票否决，编辑器就不能处于编辑状态
- EditorView的props()可以返回DirectEditorProps；
  - update(props)可以用来替换既有的DirectEditorProps；
  - setProps(props)则可以用来部分更新DirectEditorProps。
  - 如果只想更新DirectEditorProps中的EditorState的话，可以使用updateState(state)。
- DirectEditorProps中的编辑器状态（state）和dispatchTransaction是需要特殊处理的。
  - 首先编辑器状态是immutable的，需要从DirectEditorProps单独拎出来作为编辑视图的一个属性；
  - 其次对于dispatchTransaction的话，如果存在，编辑器视图的dispatch(transaction)方法会调用dispatchTransaction来处理transaction，否则直接使用EditorState.apply()来处理transaction。
- EditorView是挂载到DOM树上的，那么它就有一个根节点，这个根节点可以是普通的DOM节点，也可以是ShadowDOM节点。

- 编辑器视图所要做的就是按model中的描述将文档转化为DOM元素，并且在此过程添加上各种装饰（Decoration），就是在文档转化成DOM的时候加上样式的活。
- 文档的装饰可以用于高亮文档之类的目的。
  - 将文档转化为DOM需要自上而下的遍历，所以装饰的过程也是自上而下。
  - 装饰对文档节点的类型是对应的，有节点装饰（Node Decoration）和平铺装饰（inline decoration）
  - 另外，还有一种装饰叫做小部件（Widget），可以在文档的任意位置插入，且跟文档没有直接关系。
- 既然装饰是文档节点的附属，装饰的组织方式要匹配文档的组织方式。
  - 而将多个装饰对应到一个文档节点则是采用数据结构装饰集DecorationSet 
- 在使用DecorationSet.create创建装饰集的时候，会按照文档树的结构形成一套与之对应的装饰树。
  - 装饰集其实是嵌套的，每个装饰集对应文档树的一个层级，并保留有能够应用到当前层级的装饰列表；
  - 此外装饰集还有一个子装饰集做属性，用于表示那些应用于文档下一层级的装饰。
- 每个装饰（Decoration）由一个from和to定义的文档位移构成。
  - 这两个位移指明了该装饰所能应用于的文档节点层级。
  - 装饰集越上层颗粒越粗，越往下颗粒越细，像一个倒三角形。
  - 每层装饰集所拥有的装饰列表所代表的文档位移（from和to）会被调整成相对于当前文档节点层级的位移。
  - 并且上层装饰集会被切块，使之边界上与下层装饰集对齐，这样一来文档的某个范围内，可能有若干个不同层级的装饰集应用于之上。
  - 层级最深的装饰集所带有的装饰列表，可能只应用于文档的几个字符。
- pm-view中使用一个buildTree函数来构建装饰集树。
  - 值得注意的是，生成装饰集树的时候，如果某装饰不能应用于当前文档节点（比如说类型不匹配），则会被丢弃。
- 需要注意的是，装饰集是作用于文档内容的，而不是作用于文档模型的。和文档树一样，装饰集也是immutable数据类型。
  - Leaf类型的节点是没有装饰的。
- 第一层装饰是加在文档的外层节点上的。这个节点的contenteditable会被设置。
  - 另外，这个节点默认会被设置一个ProseMirror的css类。可以通过指定EditorProps.attributes来向这个节点添加额外CSS类，或者其他节点属性。
  - EditorProps.attributes可以直接是一个包含待添加属性的对象，或者一个函数。
  - 如果是一个函数，则这个函数接受编辑器状态为参数，并生成待添加属性对象。
  - 这种细节上的区分对待允许根据编辑器状态的不同来对文档的外层节点设置不同的属性，比如当文档失去焦点时将背景设成灰色等等。

- ProseMirror是根据ViewDesc视图描述来管理视图的DOM，视图描述可以看成是虚拟DOM。
  - ProseMirror会捕捉处于编辑区域的事件，然后更新相应的文档状态，然后再更新相应的视图描述，以此来匹配更新后的文档状态。
- 视图描述采用跟DOM类似的层级结构的，每个描述对象既包含了指向父对象的描述，又包含了子对象的集合。
  - 此外，每个视图描述对象使用dom属性指向它所使用的DOM节点，并且在该DOM节点上添加了一个pmViewDesc属性来反向索引。
  - 这看起来像是一个双向链表。
- 为了支持更复杂的视图表示，视图描述还带有一个contentDOM属性，用来表示当前文档节点的子内容应该放置何处。
  - contentDOM可以和dom一致，指向同一个DOM节点。
  - 对于文档的叶子节点，contentDOM为空。
  - 自定义的视图描述可以指定不同的dom和contentDOM，这样可以在文档的当前节点和其子节点之间增加一层用于其他目的的DOM。
  - contentDOM就是在创建文档节点规格定义中toDOM属性中的0（空洞）所在位置。

- 如何在视图描述和文档节点树之间同步呢？这用到了一个辅助类ViewTreeUpdater。
  - ViewTreeUpdater基本上是采用深度遍历的方式来将视图描述同步到文档节点树的。
- 以文档标记（Marks）为例。ViewTreeUpdater有一个专门的syncToMarks()来将视图标记描述对应到文档节点的标记。
  - syncToMarks()要将文本节点的内容描述，放置到标记描述之下。
  - syncToMarks()是通过一个栈结构来实现这种效果的
- 视图描述只是虚拟DOM，如果一个视图描述节点需要更新时，它会为自己设置一个dirty属性，表示需要更新。
- 视图描述指示文档DOM的更新，深度遍历从叶子节点往上遍历，完成一个层级就调用renderDescs()来更新相应的DOM。
# more-prosemirror-blogs
- [Decouple look&feel from Remirror extensions](https://medium.com/collaborne-engineering/decouple-look-feel-from-remirror-extensions-87a06ad9214e)
  - The Remirror extension thereby exposes an option in the format of `(state) => React.ReactElement` and uses this afterwards to render the component.

- [Why Tag1 Selected ProseMirror_201911](https://www.tag1consulting.com/blog/modern-rich-text-editors-how-evaluate-evolving-landscape)
  - 比较了 prosemirror，draftjs、ckeditor5、quill、slate
# ref
- [Why we picked Remirror/Prosemirror as WYSIWYG editor in our React application](https://medium.com/collaborne-engineering/rich-text-editor-for-react-f7d71746867f)

- [Decouple look&feel from Remirror extensions: render props to the rescue](https://medium.com/collaborne-engineering/decouple-look-feel-from-remirror-extensions-87a06ad9214e)
