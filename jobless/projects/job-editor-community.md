---
title: job-editor-community
tags: [community, job, prosemirror, text-editor]
created: '2021-10-01T06:40:08.860Z'
modified: '2021-10-01T06:42:39.302Z'
---

# job-editor-community

# guide
- 编辑器常见问题
  - 光标
  - 选区操作，如高亮，计算选中文字
  - 按键处理，输入文字还是换行删除
  - 输入法选词窗口的位置，输入法编辑内容
  - 复制粘贴时剪贴板操作

- 编辑器选型
  - 良好的性能
  - 可扩展性

- 编辑器开发的难点
  - 实现选区光标、非编辑区的菜单工具栏等等都需要不小的工作量
  - 实现高效的文档数据层，
    - 为了实现logn级别的增删改查，需要使用很多高级的数据结构。
  - 实现高效的文字排版，
    - 这里会涉及文字处理相关的模型和算法，另外还有很多设计模式和工程化的细节。
  - 实现高效的渲染层，
    - 如果用DOM实现，需要考虑如何让每次编辑的DOM修改最少；
    - 如果用canvas，需要实现类似游戏开发的精灵，事件，摄像机等。

- 分页

- 如何处理长文档(参考prosemirror)
# repeat
- 如何不借助 contenteditable 实现富文本编辑器？
# discuss

## [如何不借助 contenteditable 实现富文本编辑器？](https://www.zhihu.com/question/366666295)

- 不使用 contentEditable 无非就以下几件事
  - 自已造一个输入框，并且兼容中英文（还有更多）输入法
  - 自己处理所有的输入事件，如回车、删除等
  - 自己处理光标，如左右移动，上下移动，全要自己算出来
- 剩下的就是做富文本少不了的对 Selection 和 Range 的操作，一般有两种思路，一种是直接基于 DOM 的，一种是数据驱动的。
  - 基于DOM的，操作比较直观，但 DOM 千变万化，难以抽象，后续的维护和扩展更是难上加难
  - 由数据驱动的，难度则由整个架构设计决定开发难度和扩展难度。看到有一些富文本抽象成 Block 和 Inline 加 Style 这种结构的

- 简单地说就是拦截各种操作事件，然后转换成对对象的操作，然后再渲染反映出来。
  - 可以看看 Draft.js 项目和代码。
  - 比如光标和选择，就是有一个内部的 SelectionState 来存储当前状态，你可以找到 offset 等信息
  - 当鼠标点击编辑器的时候，你就需要拦截然后看是单击还是拖拽，然后再计算 offset 等，再拦截键盘事件，把接受到的字符在 ContentState 里面插入到对应的 offset 位置（单击）或者替换内容（拖拽）
  - 之后再利用 React 等渲染出来，看到的就是替换掉了。
- 优势很明显，可完全控制作为数据源的js对象
  - 内容清晰不会混入乱七八糟的HTML，可以对元素额外添加很多描述信息，完全控制交互体验，
  - 支持跨端。
- 劣势也很明显，开发复杂度高，
  - 因为所有操作都需要妥善处理，但这正是最棘手的地方，之前基于这个开发，只能魔改源代码强加判断逻辑。

- 用div加tabindex拦截keydown事件，中文输入可以自己做
  - 如果不考虑中文输入，比如银行卡号、车牌号，这种特殊场景就很方便

- 主流富文本编辑器都可以改成不借助 `contenteditable` 实现，以 ProseMirror 为例进行改造，
- 学习 prosemirror-view/src/domobserver.js 文件代码，将其逻辑应用在编辑器外的不可见的 `<input>` 标签上。
  - 如果不特别纠结 contenteditable，使用设置了 contenteditable 的 div 标签可能会好些。
  - 也可以使用 beforeinput 事件代替脏检测，方案参考 slate。
- 删除 prosemirror-view 中对 contenteditable 的依赖，主要是文本选区相关逻辑。
- 处理编辑器焦点问题，模拟输入法样式，模拟光标和选区。
  - 选区渲染可以参考各种编辑器协同选区的实现方案，ProseMirror 也有模拟光标的实现方案。
  - 至于确定点击后的选区位置，ProseMirror有坐标映射到 Position 的工具函数。
- 注意回避方向键上下移动光标、双击选中词语、拼写检查和 bidi 等问题，人多可以正面解决，人少 case by case。
- 没有使用原生选区的 ProseMirror 相关插件应该可以正常使用。
- 一个人一两个月应该可以搞定主流程。
- 以上纯属脑洞，未经任何可靠调研，如有错误或遗漏，欢迎大家指正。

- 我的想法是只借用原生的选中区域和光标，剩下的所有内容格式全部由我自己插入，这样能够有效的避免乱七八糟的格式问题，现在除了输入法的输入无法拦截之外，其他的事件均能够拦截到

- 在浏览器里，打开了 contentEditable 不等于借助了 contentEditable。
- 粗略看来，一个DOM元素加上 `contenteditable` 属性后，就大致具备了这些能力：
  - 选区的拖选编辑和光标闪动支持
  - 方向键控制时的默认行为
  - 输入文字时的默认行为（牵扯到输入法）
  - 复制粘贴时的默认行为（牵扯到富文本剪贴）

- 我这里拿Apple的Pages网页版举例。
  - Pages手工绘制了光标，文本选择框，还自己画了输入法输入过程中正在编辑的文字的下划线。
- Web技术目前还没有暴露测量某一个字符在屏幕上的位置的能力。
  - 自己下载全部字体，然后用WebAssembly把现有的排版引擎移植到网页端，WebGL硬上。
  - 把渲染丢给浏览器，但是下载字体的元信息，计算字符的偏移位置。
  - 通过大量插入span测量字符位置。
- 输入法选词窗口出现的位置。
  - 这个其实很多人都知道怎么做，你在表面放一个自己画的展示层，底下放一个真正的 contenteditable 接受用户输入，然后用个不透明的 div 盖住。只要确保两层对齐就可以了。
- 输入法当前编辑的内容，
  - 这个需要看 selectionchange 以及 composition，beforeinput/input 应该也有信息
- 获得用户编辑的意图。
  - 使用浏览器的 beforeinput 事件，会包含用户输入什么内容、删除什么内容，最美妙的是，在部分平台上这个事件是可以 preventDefault 的，
  - 也就是说，在获得用户意图之后，你可以阻止 DOM 修改，自己更新，避免 DOM 被搞乱。
  - 这些平台包括了 Safari 和新版本的 Chrome。我不记得哪个版本的 Chrome 楷书支持 cancel beforeinput（也就是 Input Events Level 2）
- 千万不要自己尝试监听键盘，举个例子，还是 emoji，用户按了删除键，前面是个法国国旗，删多少怎么算？前面是个 Unicode combining tone，是删除 tone 还是整个 glyph 一起删掉？这个是不可解的。
- range.getBoundingClientRect() 可以测量字符在屏幕上的位置，是有什么坑吗

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

- 有可能是全程模拟，光标也是模拟的，做了一个隐藏的input接收输入，然后在页面上渲染内容，但是这个太复杂了，没有一个团队做不好的

- 我现在的实现思路是通过修改样式把 textarea 修改成一个光标，悬浮于渲染元素之上，以此解决输入法选词框位置问题。
  - 每个字符都渲染成 span 元素，包括换行符，这样可以通过 getBoundingClientRect 定位。
  - 通过 input 事件监听改动，计算出原始内容和当前内容的差异，以此动态修改 dom。
  - 问题是除了遍历，没有一个高效定位 span 字符的方法。
  - 我试过 querySelectorAll 通过 css 选择器定位，但是查出来的往往不符合预期。比如我想查出第 5 到第 10 个字符，就会想当然的用 querySelector('span.char:nth-of-type(5)')，这样的但是查出来的结果完全不是我想要的那个字符。
  - 可是用遍历我又觉得很浪费，假设一万多个字，每次改动都要遍历一遍。真的头疼。
- 我们这边是按照段落做的，每次修改一个段落就完整地重渲染，性能可以接受。
  - 至于说span定位，回答里说了我是预处理成不可以被换行的span，然后span内部再测量每个glyph的位置。
  - 这个span内部测量glyph位置的部分是被缓存的，而且是按需计算，实际性能感觉尚可。

- 首先打开chrome的f12点击settings，勾选Shadow Dom，再看看原生的input元素，你会发现，input在原生的封装下，里面是多个div
  - 原生也是这么干，比如点击时获得焦点触发focus事件，fom.dispatchEven(new Event('focus'))，再比如光标，如果你也想这么干完全可行啊。

## Composition 事件

- 输入开始时触发 compositionstart
- 选择字/词完成输入时触发 compositionend
- 输入过程中每次击键时触发 compositionupdate，包括 start 事件以后立即触发，end 事件以前立即触发
- Composition 事件以后触发 input 事件

- 通常我们都是监听 input 或者 change 事件来校验用户输入，也就是说在用户输入拼音的过程中就已经触发了相关事件，进而触发校验。
  - 在 compositionend 里校验非直接输入，就能有效地避免不恰当的校验时机产生的用户体验问题

## [slate 编辑器架构 4个角度](https://www.zhihu.com/question/458478254/answer/1953763658)

### 整体架构

### 核心逻辑层

### 插件设计

### 输入处理