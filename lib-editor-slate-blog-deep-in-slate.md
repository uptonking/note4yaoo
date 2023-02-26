---
title: lib-editor-slate-blog-deep-in-slate
tags: [blog, slate-editor]
created: 2023-02-22T11:03:20.711Z
modified: 2023-02-22T19:54:25.348Z
---

# lib-editor-slate-blog-deep-in-slate

# guide

- resources
  - [slate学习总结 insertText源码解读](https://juejin.cn/post/6967301474737094669)
  - [slate 架构设计分析 - 知乎](https://zhuanlan.zhihu.com/p/262209236)
  - [深入 Slate.js 编辑器 - 钉钉文档 - 知乎](https://www.zhihu.com/column/c_1312084184400162816)

- [Slate源码解析（一） slate core - 掘金](https://juejin.cn/post/6978137641401188365)
  - [Slate 源码解析（二） slate-react + tests - 掘金](https://juejin.cn/post/6978141447140671501)
  - [关于 wangEditor-v5 单元测试的总结 - 掘金](https://juejin.cn/post/7079951448812814349)
  - [从 MVC 架构的角度看 Slate - 掘金](https://juejin.cn/post/6952076442649755662)

- [slate.js源码分析（一） —— slate渲染机制 - 知乎](https://zhuanlan.zhihu.com/p/266438572)
  - [slate.js源码分析（四）- 历史记录机制 - 知乎](https://zhuanlan.zhihu.com/p/293061216)

- [从 Slate 的内置特性到洋葱模型 - 掘金](https://juejin.cn/post/7086816312789794846)
# [slate 架构与设计分析 · hullis/blog](https://github.com/hullis/blog/issues/36)
- slate 数据模型（model）的设计
- slate 以树形结构来表示和存储文档内容
- type Node = Editor | Element | Text
- 采用树形结构描述 model 有这样一些好处：
  - 富文本文档本身就包含层次信息，比如 page, section, paragraph, text 等等，用树进行描述符合开发者的直觉
  - 文本和属性信息存在一处，方便同时获取文字和属性信息
  - model tree Node 和 DOM tree Element 存在映射关系，这样在处理用户操作的时候，能够很快地从 element 映射到 Node
  - 方便用组件以递归的方式渲染 model
- 用树形结构当然也有一些问题：
  - 对于协同编辑的冲突处理，树的解决方案比线性 model 复杂
  - 持久化model / 创建编辑器的时候需要进行序列化 / 反序列化

- 选区和光标处理
- 有了 model，还需要在 model 中定位的方法，即选区（selection），slate 的选区采用的是 Path 加 offset 的设计。

- model 变更机制
- 有了 model 和对 model 中位置的描述，接下来的问题就是如何对 model 进行变更（mutation）了
- 通常来说，对 model 进行的变更应当是原子化（atomic）的，
  - 这就是说，应当存在一个独立的数据结构去描述对 model 发生的变更，这些描述通常包括变更的类型（type）、路径（path）和内容（payload），例如新增的文字、修改的属性等等。
  - 原子化的变更方便做 undo/redo，也方便做协同编辑
- 对 model 进行变更的过程主要分为以下两步
- 通过 Transforms 提供的一系列方法生成 Operation
- Operation 进入 apply 流程
  - 记录变更脏区
  - 对 Operation 进行 transform
  - 对 model 正确性进行校验
  - 触发变更回调
- GeneralTransforms，它并不生成 Operation 而是对 Operation 进行处理，只有它能直接修改 model，其他 transforms 最终都会转换成 GeneralTransforms 中的一种

- model 校验
- 对 model 进行变更之后还需要对 model 的合法性进行校验，避免内容出错。
- 校验的机制有两个重点，一是对脏区域的管理，一个是 withoutNormalizing 机制。

- 插件系统
- 看起来 slate 的插件机制非常强大，但它有一个非常简单的实现：覆写编辑器实例 editor 上的方法。
- 用 withReact 修饰编辑器实例，直接覆盖实例上原本的 apply 和 change 方法。~~换句话说，slate 的插件机制就是没有插件机制

- undo/redo 机制
- 实现 undo/redo 的机制一般来说有两种。
- 第一种是存储各个时刻（例如发生变更前后）model 的快照（snapshot），在撤销操作的时候恢复到之前的快照，
  - 这种机制看起来简单，但是较为消耗内存（有 n 步操作我们就需要存储 n+1 份数据！），
  - 而且会使得协同编辑实现起来非常困难（比较两个树之间的差别的时间复杂度是 O(n^3)，
  - 更不要提还有网络传输的开销）。
- 第二种是记录变更的应用记录，
  - 在撤销操作的时候取要撤销操作的反操作，这种机制复杂一些——主要是要进行各种选区计算——但是方便做协同，且不会占用较多的内存空间。
- 在 withHistory 方法中，slate-history 在 editor 上创建了两个数组用来存储历史操作
  - 它们的类型都是 Operation[][]，即 Operation 的二维数组，其中的每一项代表了一批操作（在代码上称作 batch）， batch 可含有多个 Operation。
  - slate-history 通过覆写 apply 方法来在 Operation 的 apply 流程之前插入 undo/redo 的相关逻辑
- undo的主要部分就是对最后一个 batch 中所有的 Operation 取反操作然后一一 apply，再将这个 batch push 到 redos 数组中。

- 渲染机制slate-react
- slate 的 model 本身就是树形结构，因此只需要递归地去遍历这棵树，同时渲染就可以了。
  - 基于 React，这样的递归渲染用几个组件就能够很容易地做到，这几个组件分别是 Editable Children Element Leaf String 和 Text
- Children 组件用来渲染 model 中类行为 Editor 和 Element Node 的 children，比如最顶层的 Editable 组件就会渲染 Editor 的 children
- 用树形结构来组织 model 能够很方便地渲染，且在 Node 和 HTML element 之间建立映射关系（具体可查看 toSlateNode 和 toSlateRange 等方法和 ELEMENT_TO_NODE NODE_TO_ELEMENT 等数据结构），这在处理光标和选择事件时将会特别方便。

- 光标和选区的处理
- slate没有自行实现光标和选区，而使用了浏览器 contenteditable 的能力（同时也埋下了隐患，我们会在总结部分介绍）。
- contenteditable 就负责了光标和选区的渲染和事件。
  - slate-react 会在每次渲染的时候将 model 中的选区同步到 DOM 上
  - `domSelection.setBaseAndExtent()` 使用浏览器api
- 也会在 DOM 发生选区事件的时候同步到 model 当中
  - `ReactEditor.toSlateRange(editor, domSelection)` 工具方法
  - 这里即发生了一次 DOM element 到 model Node 的转换

- 键盘事件处理
- beforeInput 事件和 input 事件的区别就是触发的时机不同。前者在值改变之前触发，还能通过调用 preventDefault 来阻止浏览器的默认行为。
- slate 对快捷键的处理也很简单，通过在 div 上绑定 keydown 事件的 handler，然后根据不同的组合键调用不同的方法。
  - Editable 默认的 handler 会检测用户提供的 handler 有没有将该 keydown 事件标记为 defaultPrevented，没有才执行默认的事件处理逻辑

- 渲染触发
- SlateProvider 在渲染的时候会向全局 `EDITOR_TO_ON_CHANGE` 中添加一个回调函数，这个函数会让 key 的值加 1，触发 React 重新渲染。
  - 然后在withReact加强的onChange中触发

- 总结
- slate 存在着这样几个主要的问题：
- 没有自行实现排版。
  - slate 借助了 DOM 的排版能力，这样就使得 slate 只能呈现流式布局的文档，不能实现页眉页脚、图文混排等高级排版功能。
- 使用了 contenteditable 导致无法处理部分选区和输入事件。
  - 使用 contenteditable 后虽然不需要开发者去处理光标的渲染和选择事件，但是造成了另外一个问题：破坏了从 model 到 view 的单向数据流，这在使用输入法（IME）的时候会导致崩溃这样严重的错误。
  - 我们在 React 更新渲染之前打断点，然后全选文本，输入任意内容。可以看到，在没有输入法的状态下，更新之前 DOM element 并没有被移除。
- 对于协同编辑的支持仅停留在理论可行性上。slate 使用了 Operation，这使得协同编辑存在理论上的可能，但是对于协同编辑至关重要的 operation transform 方案（即如何处理两个有冲突的编辑操作），则没有提供实现。

- 总的来说，slate 是一个拥有良好扩展性的轻量富文本编辑器（框架？），很适合 CMS、社交媒体这种不需要复杂排版和实时协作的简单富文本编辑场景。
# [Deep in Slate.js —— 深入 Slate.js gitbook](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/SUMMARY.md)
- 这本小册基于的 Slate.js 0.44.x 版本，虽然 Slate.js 现在已经渐进到了 0.50.x 版本，但其架构编辑器的方式仍然是统一的，
- 小册的初衷也在于借 Slate.js 分析和讨论 Web 富文本编辑器的架构方式，而不是教导怎么使用 Slate.js

### [拯救 ContentEditable](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/history.md)

- 浏览器所提供的 `<textarea />` 和 `<input />` 都只允许用户输入「纯文本」，能力十分单薄。
- HTML 5 中的 contentEditable 规范
  - editing host：即正被编辑的 HTML 元素。
    - 如果某个 HTML 元素开启了 contentEditable 属性，那么这个元素就是一个 editing host；
    - 而如果 document 开启了 designMode，那么整个 HTML 文档下的元素都是 editing host。
  - editable：即可编辑元素。
    - 若 HTML 元素是 editing host 的子孙，那么它就可以被编辑，
    - 另外，可编辑元素的子孙也是可编辑的（除非这些子孙被声明了 contentEditable 为 false）。
- 浏览器提供的 document.execCommand 并非无所不能，甚至还成为了文本编辑器的实现掣肘，不仅仅是支持的「指令有限」，就连同一个指令，各浏览器的「实现都有可能不同」。因此，更多的编辑功能仍然需要开发者进行事件劫持等操作才能实现。

- 视觉内容与实际内容的一对多关系
  - 比如inline元素的顺序
- 视觉选区与实际选区的多对多关系
  - 比如光标在inline元素的前后位置

- 主流的编辑器架构
  - 模型与视图分离：编辑器自定义视图无关的数据结构，视图的渲染不再由浏览器控制，而是由编辑器控制，从而满足「视觉与实际内容的一一映射」
  - 自定义指令：自定义编辑器的指令集，一方面能扩充编辑器能力，但更重要的一方面，是避免直接调用 document.execCommand 在不同浏览器形成不一致的结果

- 了解主流富文本编辑器的设计和实现
  - Web富文本编辑器的内核模型是怎么设计的，为什么要这样设计
  - 编辑器的模型和视图之间是如何同步的
  - 编辑器是如何通过插件体系扩展能力的
  - 编辑器是怎么支持多人协同编辑的
  - 当前Web富文本编辑器面临的问题

### Slate.js 简介 

- 「非常轻量」的解决方案：Slate.js 几乎没有集成任何功能，只是提供了一个插件扩展机制给开发者去实现想要的功能
- 「视图无关」 的：Slate.js 定义了一套脱离 UI 实现的数据模型，考虑到我们不是要再学习一遍 React 或者 Vue
- 「协同编辑」：Slate.js 的模型设计天然就亲和协同编辑

### [HTML中的富文本](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/rich-text-in-html.md)

- Slate.js 的数据结构设计大量参考了 HTML 中对于 DOM 的设计
- 节点（Node）：节点容纳了我们能看到的富文本内容，富文本容器也是一个节点，容纳了其他节点
- 选区（Selection）：当前选中的区域，如果区域的起点和终点重合，那看到就是一个光标

- 在 HTML 现行规范中，节点（Node）被定义为一个 Node Interface，它是一个抽象基类，继承自 Node Interface 的类将具备访问节点属性、修改节点结构的能力。
- 在 HTML 5 之前，HTMLElement 被分为了:
  - 块级元素（Block Level Element）：块级元素占据了父容器的整个空间，视觉上就是形成了一个 “块”。文档中每新增一个块，首先要新增一个容纳这个块的行。
  - 行内元素（Inline Level Element）：行内元素只占据了内容所需要的空间。
- 而在 HTML 5 之后，HTMLElement 的按照内容类别进行了细化

- 在 HTML 规范中， Text Interface 用来表示 Element 的文本内容，它继承自 CharacterData ，后者描述了 Node 所包含的字符
  - 可以通过 Document.createTextNode() 向节点中插入多个 Text，并通过 Node.textContent 访问节点的文本
  - 创建了多个相邻的文本节点，这些相邻的节点可以通过 `Node.normalize()` 进行合并

- Void Element（空节点），也被称为 Empty Element，是一类特殊的 HTML Element，它不允许包含任何的内容。

- 一个节点，除了可以含有文本内容，还能绑定一些额外数据。
  - 例如我们需要为图片节点设置图片源和尺寸信息，HTML img tag 为此提供了 src 、width、height 等属性。
  - 更一般地，我们可以通过 `data-*` 设置节点的数据

- HTML 规范中，通过 Node Interface 定义了访问当前节点的父节点、孩子节点以及兄弟节点的方式

```JS
Node.parentNode;
Node.childNodes;
Node.previousSibling;
Node.nextSibling;
```

- 选区（Selection）表示的是当前用户选中的内容
  - 通过 window.getSelection() 可以获得当前窗口的 Selection 对象
  - 选区的方向则可以通过 anchor、focus 的位置判定，若 focus 落在 anchor 之后，为向后选择，若落在 anchor 之前，则为向前选择，二者重叠时，即选区被折叠，用户视觉上看到的就是一个闪烁的光标。
- 一个 Range 对象描述了一个包含若干 DOM 节点的「文档区间」
- Netscape 将 Selection 实现为了由多个 Range 所构成，这看似合乎语义，一个选区应当可以包含多个文档片段。假设用户想同时选中一个表格的若干列，这样的设计就是必要的，但是开发者因此要应付许许多多边界问题。
- 因此，现在的浏览器在实现 Selection 时，不再允许一个 Selection 包含多个 Range，考虑到向后兼容 API，还是为 Selection 支持了 removeRange()、getRangeAt() 等方法，只是开发者在使用这些 API 时，一般都只能传入 0 作为 index 操作第一个也是唯一一个 Range 对象。

- 本节分析了 HTML 中富文本内容的组成和实现，一个富文本需要包含节点和选区两个部分，
  - 节点是一棵 DOM 树，树中的节点各有类型；
  - 选区则分为了 Selection 和 Range，前者表示了用户选中的内容，后者则是这些内容的 DOM 表达。

### [Slate.js中的富文本](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/rich-text-in-slate.md)

- Slate.js 在数据模型的设计宗旨是 「Mirror the DOM」，即尽可能按照现行的 DOM 标准去抽象自己的数据模型。
- 这种亲近现行标准的设计理念，降低了开发者接入编辑器的知识负担
- 在 Slate.js 中，同样区分了：
  - Node：最高级的抽象，包含了访问节点和节点内容的方法
  - Element：表示节点容器的 Node。Slate.js 含有 Document、Block 和 Inline 三种类型
  - Text：表示节点文本内容的 Node

- 一个 Node 对象
  - 如何划分节点类型 type
  - 如何处理节点关系 children/nodes
  - 如何表示节点内容 data
  - 如何绑定节点数据 key
- Element Model 同样具有属性
- Text Model 来表示节点的文本内容
  - leaves：文本叶子节点，不同格式（例如加粗，斜体等）的文本，将会被分拆为若干个 leaf
  - marks：文本节点所包含的所有 mark（标记）
- Path Model 来表示节点在节点树中的位置，它是一个数值数组，循着 Path 的每个元素，我们就能找到这个节点
- Range Model 也采用 anchor、focus 来描述一个片段的起终点

### [节点寻址](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/path.md)

- 当节点被创建后，Slate.js 会为其分配一个 key 作为唯一索引，默认是一个单调自增数
  - 每次生成的节点，都会拥有一个在文档中唯一存在的 key，只在部分情况下，会需要重新为节点生成 key，例如一个 Text 节点分裂后，为了避免分裂后的两个 Text 节点共享分裂前的 key，需要为分裂后节点重新生成 key。
- key 作为节点的索引，不依赖于文档结构而存在，因此，它「没有反映节点位置的能力」。如果我们要按照 key 来寻找节点，就要全量遍历当前节点树，直到找到对应 key 的节点为止
- 为此，Slate.js 设计了「Path」 这个模型去描述节点位置，它是一个数字数组
- Slate.js 为 Path 配套了一系列的工具函数，这些工具函数可以分类为
  - 处理路径关系的：例如 Path.isAfter(path, target) 等
  - 变更路径的：例如 Path.increment(path, n, index) 等
  - 执行路径转换的：PathUtils.transform(path, operation)，这个函数非常重要，在对文档的 normalize 和进行协同编辑时，我们都会用到它

- 当开发者调用 xxByKey() 的 API 时，Slate.js 会先根据 key 查找到节点的路径，顺着节点路径找到节点后执行对应操作，这个查找的过程以 getPath(key) 为名封装在了 Node Interface 中
- 节点路径和当前节点树的结构有关，因此，每个节点都维护了一个其子孙的 key-to-path 的 Hash Table，table[x] 就表示了 key 为 x 的节点的「相对路径」，注意，是相对路径，而不是从文档根节点开始的绝对的路径。

- 假设我们的文档很大时，每次查询节点路径，调用 node.getKeysToPathsTable() 重新构建 key-to-paths table 会造成严重的性能问题。
  - 为此，Slate.js 通过 memorize 技术为函数调用做了缓存，这是一种常规的性能优化手段：将函数的执行结果缓存，下一次以同样的「参数」和「上下文」调用函数时，直接返回缓存的结果。
  - Slate.js 通过 WeakMap 创建了对象的函数缓存，每个对象的缓存包含了「有参数调用」和「无参数调用」函数两个 hash map。特别地，对于有参数调用，memoize 需要考虑为不同的参数集合设置不一样的缓存，并且，所有以对象为参数的缓存，都用 WeakMap 构建。
- WeakMap 持有的是对象的 Weak Reference（弱引用），当对象不再被使用，垃圾回收就能自动清理 WeakMap 该对象映射的内存空间

### [Operation](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/operation.md)

- Slate.js 即使用了 Operation 作为文档的最小抽象。
  - 每个指令调用的结果，并非直接生成一篇新的文档，而是生成一系列不同类型的 Operation
  - 指令会生成若干个操作，逐个应用这些操作，即可获得最新的文档

### Normalize

- HTML Element 可以通过 normalize 方法实现节点的标准化，例如合并多个文本节点
- 让文档能够符合标准，我们可以对指令相关指令做修改
- 一种方式是，直接修改 insertText 指令的实现，这种方式需要侵入到指令的实现，并且，为了实现「开发者自定义规则」，还需要将每个指令暴露为 hook，让开发者侵入逻辑进行文档校正
- Slate.js 也没有采用这样的方式实现 normalize，它是在指令完成时对受到指令影响的节点做 normalize。
- Slate.js normalize 的过程是：
  - 每个指令生成的若干 Operation，Slate.js 都会采集这些 Operation 影响到的路径，并把这些路径标记为脏路径（dirty path），放入脏路径栈
  - 当指令执行完毕，Slate.js 会沿着脏路径来做 normalize
  - normalizeDirtyPaths 的过程，就是将脏路径依次出栈，判读对应路径的节点是否违反了了某个规则，若是，则对脏路径上的节点调用其 normalize 方法进行校正（由于可能定义出错误的规则，导致节点的 normalize 一直失败，因此 Slate.js 也对节点的 normalize 限制了次数）
- Slate.js 使用 schema 来表示文档要满足的标准。
  - Slate.js 默认行为如果不是我们期望的，我们还能自行实现节点的 normalize 方法。比如这个例子中，我们希望 image block 违反了规则时，就替代为一个默认的 image block
- 声明式地规则配置并不能应付所有场景，对于更复杂的节点校验，开发者可以为插件实现 normalizeNode 方法
  - 每次 Slate.js 指令执行完成并进行 normalize 时，调用 node.normalize() 时，都会依序调用插件中的 normalizeNode 方法对节点进行 normalize

- 如何任何文档内容的变更，都要对文档树做一次全量的 normalize，开销就特别大
  - 为了缩减 normalize 的范围，加快 normalize 执行效率，Slate.js 就需要标记当前操作影响了哪些节点，受影响的路径被标记为脏路径（dirty path）
  - 将路径依次出栈进行 normalize
- 「新到来的 Operation 会对已经生成的脏路径造成影响」，因此不能直接将该 Operation 生成的脏路径入栈，而应当「基于这个 Operation，先对栈中已有的脏路径做修正」，Slate.js 的 PathUtils 中提供了 transform(path, operation) 函数来完成这个工作
  - 这个函数是非常复杂的，需要根据当前 Operation 操作的位置和 path 的空间关系，对 path 进行不同的转换（截止 Slate.js 0.50.x 版本，这个路径转换也一直在完善）

### Decoration

- 插件通过实现 decorateNode hook 来告诉 Slate.js：视图层需要的数据如何从当前的节点计算得到。
- 一个节点被装饰的序列就来源于：
  - 注入的 decorations：例如父节点注入的 decorations
  - 自己的 decorations：由 decorateNode 生成
- Decoration 的工作机制有下面这些特点：
  - 渲染期计算：decoration 是在渲染期间被计算出的
  - 自顶向下分发 decorations：避免节点遍历超长 decorations 序列
  - 限制计算：由于 Node Component 做了 re-render 频度控制，当编辑器模型变更时，不需要 re-render 的 Node 也不会被计算 decorations。例如我们在处理链接高亮的时候，如果链接节点没有变化，它的 decorations 不会被重新计算。

### Annotation

- Decoration 虽然为节点提供了动态装饰的能力，但是它却有一些限制：
  - 歧义：以 Mark + renderMark 作为装饰手段，开发者难于理清它与文档模型中的 Mark 的异同
  - 不支持协同：假定我们通过 setDecorations(decorations) 为一个图片节点装饰上了 “上传进度”，期望协同者也能看到这个进度，基于 Decoration 实现起来就比较困难了，因为生成 Decoration 不会产生 Operation

- Slate.js 在 0.47 版本后引入了 Annotation 来替代 Decoration
- 为了增加灵活性，减小语义干扰，Annotation 不再使用 Mark 作为装饰类型，而是用了 type 来定义装饰类型，也能通过 data 为节点注入装饰数据。

### 数据模型与视图同步

- Slate.js 拥有一个视图无关的数据模型，这份数据模型可以接入任何视图层解决方案
- 官方则默认提供了 slate-react —— 基于 React 的视图层解决方案。
- 事件在 Slate.js 中的流转历经三个阶段：
  - 预处理：例如当处于输入法时，要阻断 keydown 事件的传播
  - 自定义插件序列：事件被预处理后，将流入开发者声明的自定义插件序列
  - 后置处理：例如 beforeinput 事件最终将在文档模型中插入输入的字符
- 数据模型更新后，Controller 要将新的变更对象（change）倾倒给视图，视图层通过向 `<Editor />` 组件注册的 onChange 回调来获得变更对象，刷新编辑器内容
  - 倾倒新的模型到视图不是同步（立即）发生的，而是使用 Promise 封装为了一个 microtask

- 进行异步调度是因为：
  - 一个 UI 事件作用到模型，可能调用了若干指令，产生了多个 Operation，若每个 Operation 的应用（apply）都进行一次视图同步，代价是十分高昂
  - 单个 Operation 的应用，作用到视图，用户视觉看到的内容未必有变更，因此，Slate.js 会等到所有指令产生的 Operation 都应用完毕，再向视图倾倒新的内容。保证下一次视图变更反映的是当次用户操作的完整影响

- 为什么要选择 microtask 而不是 setTimeout 来创建 macrotask 呢？了解 Event Loop 的同学应该知道，Timer 需要在下一次渲染后才被调度。而 microtask 队列则会在下一次渲染前被调度。亦即 microtask 能让我们的操作在下一次编辑器视图更新前就被调度。

- 当视图层获得新的内存模型后，就尝试重新渲染内容，渲染首先从 `<Content />` 组件开始，从根节点 document 开始，依序渲染节点子树

- 选区模型的同步大抵类似：
  - 监听选区事件更新模型选区
  - 模型更新后，重新绘制 DOM 选区
- 对于选区事件的监听，slate-react 监听了两个事件源：
  - React 组件上的 onSelect 合成事件
  - DOM 原生的 selectionchange 事件：由于 React 组件的 onSelect 并非标准实现，只有用户抬起鼠标按键时，才会回调。但是实际中，选区的变更可能不全来自鼠标事件，因此额外监听 selectionchange 事件保证模型选区和视图选区的同步

### [输入法噩梦](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/hard-structure.md)

- Slate.js 定义的架构要能完美工作，离不开两个重要条件：
  - 能正确理解用户意图：Slate.js 能够正确且详实的 UI Event，推导用户行为
  - 对视图有绝对控制权：视图的所有表现都来源于 Slate.js 供给的数据
- 阻碍 Slate.js 架构稳定应用的原因是什么呢？
  - 输入法（IME）为例

- 除了操作系统的自带的输入法，大部分用户更习惯安装和使用第三方厂商的输入法，例如搜狗输入法，百度输入法等。
  - 不同厂商的输入法实现，只是在完成输入源（键鼠，手写板等）和操作系统之间的互动，例如我们需要为 Android 开发一款输入法，我们只关心 Android OS 提供的接口和协议。
  - 输入法并不直接和浏览器打交道，浏览器也需要通过操作系统去获得输入法状态，再把输入法过程翻译为标准所定义的事件流，例如 compositionstart 、beforeinput event 等。
- 实际中，浏览器尝试转译输入法过程时，却会出现：
  - 无法交付事件：当输入进行时，浏览器可能无法交付 beforeinput 事件，Slate.js 就无法获悉用户意图
  - 无法完整交付事件信息：部分 Android 输入法实现时，无论用户继续按下哪种按键， keyCode 始终是 229，也会导致 Slate.js 无法获悉意图

> W3C KeyCode 规范 定义了 keyCode 为 229 的 Keyboard Event 是表示输入法正在处理按键输入

- 事件或者事件信息的缺失，导致 Slate.js 数据环路的第一步就中断了：到底用户做了什么操作，我该怎样更新模型？
- For clarity, due to the differences in Android's support of the beforeInput event, Android input uses compositions and mutations which is different from other browsers. This means that Android support progresses separately from other browsers and due to it being new, may have more bugs.
- 事件的脆弱，让 Slate.js 无法根据事件推导用户意图。但我们也发现，如果我们先放开事件对于事件的拦截，将输入过程完全托管给 contenteditable 元素（无论是 `<textarea />` 还是 `<div contenteditable="true" />`），那么输入结果是符合预期的。
- 因此 Slate.js 在处理 Android 输入法问题的策略是：放弃「基于事件的同步」策略，改为「基于现象的同步」策略。
- 这很类似于 Prosemirror 等框架，由视图的变更去推导用户意图，进而更新数据模型，是一种视图先于数据的策略。
- Web API 提供了 MutationObserver 来监听 DOM 变更。当通过 MutationObserver 开始监听 DOM 后，每当这个 DOM 发生变化（无论是内容还是结构），都会回调给我们变更序列，变更序列的每个对象都是一个 MutationRecord 对象
- 那么，编辑器就定义：若 DOM 变更具备这样的特征，则用户意图为删除，进而调用删除指令去更新数据模型，以此解除了对于事件的依赖
  - 特征都来源于人肉测试，而无法自己训练去丰富特征。并且由于输入法的繁复，测试阶段也是无法穷举出所有用户行为对应的特征的，往往特征的丰富还来自于用户问题的反馈，每个问题背后对应的机型和输入法，又能得出一系列特征。

- 对于一篇中大型文档，重绘的代价也是十分高昂的。现在，用户虽不再抱怨无法输入或者无法删除了，但又会对频繁的卡顿而叫苦不迭了。
- 👉🏻 因此，Slate.js 仅仅在 Android 这样的场景使用了「基于现象的同步」，其他场景还是依赖于事件去同步模型和视图。
