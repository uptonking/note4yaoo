---
title: lib-editor-community
tags: [community, editor, lib, text-editor]
created: '2021-05-14T12:04:27.547Z'
modified: '2021-05-14T12:04:55.412Z'
---

# lib-editor-community

# guide

# discuss-stars
- ## [如何不借助 contenteditable 实现富文本编辑器？](https://www.zhihu.com/question/366666295)
- 在浏览器里，打开了 contentEditable 不等于借助了 contentEditable。
- 粗略看来，一个 DOM 元素加上 contenteditable 属性后，就大致具备了这些能力：
  - 选区的拖选编辑和光标闪动支持
  - 方向键控制时的默认行为
  - 输入文字时的默认行为（牵扯到输入法）
  - 复制粘贴时的默认行为（牵扯到富文本剪贴）

- 主流富文本编辑器都可以改成不借助 contenteditable 实现，，以 ProseMirror 为例进行改造，
- 学习 prosemirror-view/src/domobserver.js 文件代码，将其逻辑应用在编辑器外的不可见的 input 标签上。
  - 如果不特别纠结 contenteditable，使用设置了 contenteditable 的 div 标签可能会好些。
  - 也可以使用 beforeinput 事件代替脏检测，方案参考 slate。
- 删除 prosemirror-view 中对 contenteditable 的依赖，主要是文本选区相关逻辑。
- 处理编辑器焦点问题，模拟输入法样式，模拟光标和选区。
  - 选区渲染可以参考各种编辑器协同选区的实现方案，ProseMirror 也有模拟光标的实现方案。
  - 至于确定点击后的选区位置，ProseMirror 有坐标映射到 Position 的工具函数。
- 注意回避方向键上下移动光标、双击选中词语、拼写检查和 bidi 等问题，人多可以正面解决，人少 case by case。
- 没有使用原生选区的 ProseMirror 相关插件应该可以正常使用。
- 一个人一两个月应该可以搞定主流程。以上纯属脑洞，未经任何可靠调研，如有错误或遗漏，欢迎大家指正。

- contenteditable方案
- 优势：就是浏览器对于光标、选区方面基本上都帮忙做好了，输入方面要做的事情主要是对于所有可能造成文档模型修改的地方一一处理，将浏览器行为映射到程序的数据里，保持数据与视图的一致正确。
- 劣势：数据、视图、输入是高度耦合的，而且跨浏览器几乎没有标准可言。受到浏览器限制较多，比如如果要实现代码编辑器里场景的多光标，就很难了。另外就是，因为视图是contenteditable来排版的，要搭载自己实现的排版引擎就几乎不可能。
- 隐藏textarea方案
- 优势：它只负责接收输入事件，其他视图输出全靠自己，相对来说，更容易解耦。因为基本脱离了浏览器原生的光标，这块可以实现出更强大的功能。排版引擎可以自己搞，只要码力够强，想搞一个从从上往下从右往左的文言富文本也没问题。
- 劣势：要处理输入是一个巨大的课题，光是处理好光标就够头疼了，更不用说还有选区。另外就是因为接管了输入、点选、拖拽等各种操作，在移动端这种光标操作不同平台各自高度定制的场景，要搞起来工作量是很恐怖的。

- 首先打开chrome的f12点击settings，勾选Shadow Dom，再看看原生的input元素，你会发现，input在原生的封装下，里面是这样的

```html
<div>
  <div>为空的占位</div>
  <div>输入的内容</div>
</div>
```

- 记得开源onlyoffice的word编辑器都是canvas渲染一部分，光标、选择文字等是模拟，细节可以看看源码，不过跟Google docs还是有差距的。

- ## 开源富文本编辑器技术的演进（20201024）
- https://zhuanlan.zhihu.com/p/268366406
- 在2019年8月份左右的时候，我们开始开发自己的知识库产品PingCode Wiki，然后对于在线文档、知识库以及背后的富文本编辑器技术都有了更深刻了解和认识
- 大家公认的富文本编辑器领域在前端里面是天坑的存在，落后的生产力与人们日益增长的需求之间的矛盾
- 落后的生产力：
  - 编辑内容相关标准推进缓慢
  - 浏览器厂商对于相同操作或者场景实现方式的不同，导致兼容性的问题
  - 使用HTML DOM描述富文本内容有太多不可控制的情况
- 日益增长的需求：
  - 不确定的交互意图，比如按Delete键，不同的焦点位置有不同的情况需要考虑
  - 内容输入的多样性，比如有：打字键入、粘贴、拖拽等，每个处理起来都相当复杂
  - 大量需要拦截阻止和代理的浏览器默认行为，保证数据的完整性和正确性
  - 用户对于编辑器的使用要求越来越高，比如：合并单元格、列表多级嵌套、协同编辑、版本对比、段落标注，大家都认为这是基本需求，其实这里面的技术难度是超出大家的想象的。
- 这里我主要从技术实现以及编程思想的演变，介绍编辑器这10年间的变化与发展。
  - CKEditor 1-4（2008）
  - UEditor (2012)
  - Quill.js（2012）
  - CKEditor 5（2014）
  - Prosemirror（2015）
  - Draft.js（2015）
  - Slate（2016）
- CKEditor 1-4可以代表传统编辑器的技术路线（同类型技术的主要是UEditor），
  - 主要依赖于浏览器原生的编辑能力，用户内容的输入是浏览器直接处理，加粗、斜体、回车等这类的处理则是捕获浏览器的事件来覆盖浏览器默认行为来实现，
  - 再辅以一些DOM的嵌套规则（dtd）和复杂数据输入（如粘贴）的过滤规则来约束数据的正确性，这类编辑器整体思路还是比较清晰的。
  - 内容的可编辑主要依赖DOM的contentEditable属性，基于原生execCommand或者自定义扩展的execCommand去操作DOM实现富文内容的修改。

- ## Which one was the one with the bad performance on long documents? ProseMirror or CodeMirror?
- https://twitter.com/thomasaull/status/1314484953686695936
- CodeMirror is normally much faster for big documents, 
  - but from the context, I suspect that in this case the magic layered on top to make CodeMirror behave like a rich text editor is the source of the slowness.

- ## Why is CodeMirror not based on or replaced by ProseMirror?
- https://twitter.com/tjconceptdk/status/1035585261198041088
- They solve different problems -- `structured rich text with configurable schema` versus `plain text with syntax highlighting and lazy rendering` . 
  - On the web you don't want to ship big, overly general code for a smaller problem

- I was doing some research and I was wondering why you didn't use the same textarea technique in ProseMirror as you did in CodeMirror? Is it planned or impossible to implement in a rich text editor? 😊
  - Because it is a more problematic hack than just using contenteditable. CodeMirror 6 will do the same
# discuss
- ## 

- ## 

- ## Curvenote - scientific editor, explorable explanations & floating comments
- https://discuss.prosemirror.net/t/inlining-a-node-for-a-comment-plugin-or-best-to-use-marks/2391
  - Interactive widgets using web-components
  - Suggestion framework
  - sidenotes
- Right now the inline references are a decoration, but if that reference gets lost (e.g. through a cut/delete), the comments fall back to being referenced at the “block” level, which seems ok for now. The sidenote framework does work with multiple inline references pointing to the same note/comment though, so looking forward to getting this feature in. I will see if there is anything we can do to make it generalizable.
- how do you manage syncing? Do you use some library that utilizes IndexedDB (such as RxDB)
  - With regard to syncing, we are currently just using the standard prosemirror collaboration module. Our product is built on top of firebase at the moment, and we are using their real-time infrastructure to help keep things in sync. All of our changes are dispatched to our redux state as a middleware of sorts to prosemirror - and that is where we add the collaboration, and keep various views of the editor in sync.
- With regard to the web-components, we were using them as just other nodes (not even node-views) for a while, and then wrapped them in this class which basically adds right click ability. The only reason we didn’t do that in the web-components directly was that it is a different library and that was out of scope. 
- Making everything flow through Redux seems appropriate as it avoids managing various event listeners. It seems you’ve separated the UI & API state into Redux stores and PM specific state into plugins?
  - To connect back up to application logic, we are just using the same redux store in both places (including relevant prosemirror-plugin state). That redux store is also responsible for the editor state (just holds a reference to prosemirror-state). This also means that the state is available for other application components through selectors/actions/etc.

- ## [在线编辑器, 多人同时编辑, 如何设计undo/redo的逻辑?](https://www.zhihu.com/question/367915946)
- 感觉有三种模式:
- 按action撤销. 
  - 甲/乙撤销, 会消失一个c. (这样做我觉得容易做, 所有状态容易管理)
- 只撤销自己做的. 
  - 甲撤销, 消失一个c; 乙撤销, 消失一个B. 
  - Google docs是这么做的, 但是交叉修改后再撤销重做, 应该会造成极大的混乱, 如何解决?
- 一路撤销到自己做的. 
  - 甲撤销, 消失一个c; 乙撤销, 变成aaaBB. 这样就是有点绝情了. 甲想恢复自己的编辑, 需要乙重做.
- 一般采取的是第 2 种方式，即只撤销自己产生的操作。
  - 那么怎样才能实现只撤销自己产生的操作呢？这就不得不说说 OT（Operational Transformation）和 CRDT（Conflict-Free Replicated Data Type）算法了。
  - CRDT 在 2006 年被提出，用于解决分布式计算结果的最终一致性问题。
  - 相比较还存在很多边缘场景需要打补丁的OT算法，CRDT 可以说是更加先进一些。也有非常多开源的库可以选择，比如 yjs , automerge , gun 或者 teletype-crdt
  - 简单来说，OT 需要一个中心服务器（用于保证正确性），而 CRDT 则可以支持点对点直接传输数据。

- ## Editor.js – Block Styled Editor
- https://news.ycombinator.com/item?id=19555633
- From a data management and flexibility standpoint, I see why block editors are becoming popular with some people. 
  - But as a user, it feels like a downgraded experience.
  - When writing multi-paragraph prose, the first draft isn't always the final draft. Quite often there's some shuffling around of parts of the content. 
  - With blocks, the user can't highlight part of one paragraph and into part of the next one because of the artificial container boundary.
  - Perhaps with some well planned keyboard shortcuts and other UI improvements, the friction can be reduced. Maybe also it will require a change in the way some of us think about content (although I still object to the user needing to think of content in terms of its subtypes and storage structures).

- I'm the current maintainer of https://github.com/madebymany/sir-trevor-js which we started in 2012. 
  - At the time we had a fully block based approach and migrated to more of a document based approach when medium.com gained traction.
  - Since then we've debated what's the best approach for cross block selection as now the expected behaviour is very much that of a text editor such as word rather than a block based editing tool which it started out as. 
  - A couple of years ago we embarked on a rewrite that saw us look for a solution to the problem that would solve this. 
  - Not just a block based selection, but a cursor based selection between blocks, but this never got to a level we were happy with.
  - I think with the evolution of online editing over the years and editors such as notion.so the approach they've taken with the multiple contenteditable elements is a good first step. 
  - Over time we'll see how far they are able to take it. Adding features such as cross browser support, undo/redo and keyboard navigation.
- I'm a maintainer of Editor.js. Regarding to your questions:
- Editor.js doesn't support nested blocks.
  - We keep structure flat and want Tools API to be as simple as possible for new developers. 
  - The target audience of the Editor.js is media and blogs, usually you don't need complex structure there. 
  - However, you can implement some complex plugins for your needs, nested lists as example.
- We consider development of the editor very serious and understand importance of the test coverage. 
  - At the moment we don't have unit neither e2e tests but this is the one of our next steps on the way.

- Two long established predecessors to this: Sir Trevor JS and Colonel Kurtz
- I've used Kurtz extensively and it's been brilliant. 
  - The only downside of all these block-based editors is that you can't easily create layouts where images float to the left or right of text. 
  - Well, you can create them but you don't get a WYSIWYG idea of what it looks like right in the editor. I can live with that!
  - I've explored all sorts of editors and Colonel Kurtz is the one that's worked best: Trix, Draft, TinyMCE, CKEditor, ContentEditable, ProseMirror - just off the top of my head.

- ## Announcing: Work is underway on CodeMirror 6, a full rewrite with accessibility, mobile support, and modularity as design goals. 
- https://twitter.com/teppeis/status/1034581567551631361
- How will this affect ProseMIrror project? What is the difference?
  - ProseMirror is for structured text, CodeMirror for plain text and code. They don't really affect each other
- Will it support the native browser spellchecker?
  - Somewhat. The main issue is that in many browsers, the spell checker gets completely confused (removes most of its underlines) when you programmatically touch the DOM. And in typical situations, CodeMirror will do that to adjust the highlighting.
  - Still, we do take care to only mess with the DOM when necessary, so when in content that doesn't change it highlighting during typing (Markdown without markup, HTML text nodes) it might work pretty well. Haven't done that much testing there yet
- Monaco still doesn't support even arrow keys on iPad/iOS. Ace and codemirror are at least usable.

- ## I have tested/worked with some #javascript rich text editors, here is my feedback. 
- https://twitter.com/nurlannurmanov/status/1409361282889928707
- My criteria were as follows:
  1. Can be used in #React  web apps;
  2. Out of box example which covers most of the use cases (image, formatting, code addition);
  3. Production-ready; 
