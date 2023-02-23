---
title: lib-editor-wangeditor-blog
tags: [blog, slate-editor, wangeditor]
created: 2023-02-22T19:49:43.377Z
modified: 2023-02-22T19:49:55.242Z
---

# lib-editor-wangeditor-blog

# guide

- resources
  - [王福朋 blogs](https://juejin.cn/user/1714893868765373/posts)
# blogs

## [wangEditor5 多级列表 - 设计与实现](https://juejin.cn/post/7152330067706642445)

## [wangEditor v5 渲染逻辑 - Model ，DOM，HTML 三者的关系_王福朋_202201](https://juejin.cn/post/7055206586175717390)

> 暂不支持移动端。

- wangEditor v5 是基于 slate.js 为内核进行开发的，slate.js 输入输出的数据一直是 JSON 格式，没有 HTML 格式。所以，我也就基于这一点，一直坚持用 JSON 格式数据。
- slate.js 能基于 JSON 格式，本质原因是它完全依赖于 React 框架，使用 React 来渲染页面。而 React 本身就是一个“数据驱动视图”的框架，所以 slate.js 提供 JSON 作为数据，交给 React 来渲染视图，这很合理。
- 而 wangEditor 虽然基于 slate.js 为内核，但它没有基于 Vue React 等任何框架。既然没有框架要求，那就需要自己去考虑渲染逻辑，那也就需要 HTML 。
- 很不幸，HTML 格式就是“乱来”的代名词。
- 但是呢，对 HTML 的支持又是势在必行的，所以这个问题我想了好久，最终得出一个虽不完美但可行的方案：HTML 仅支持 wangEditor 输出的格式（包括 V4 和 V5），其他的格式就保证了。

- JSON 数据就是编辑器的 Model 。可以把编辑器认为是一个黑盒，输入输出的可以是 HTML ，但其内部数据是规定格式的 JSON 数据。
  - 现代富文本编辑器的 Model 都是基于一种 DSL 的，不会直接基于 HTML 。因为 HTML 格式过于灵活，不好控制，而自己的 DSL 是完全可控的。
- Model（即 JSON 数据）需要实时的渲染到编辑器视图中，即把 Model 渲染为 View 。而且不同的组件要渲染为不同的 DOM 类型
- 数据驱动视图，这一点和 Vue React 一样，所以我们也做了类似的设计：第一，把 Model 转换为 vdom ；第二，把 vdom patch 到真实 DOM 中（使用 snabbdom.js）
- 但是还要考虑各个组件渲染为不同的 DOM 类型，所以需要让各个模块注册自己的 Render 函数，再统一渲染。

## [与WangEditor作者的交流会_202111](https://juejin.cn/post/7035920256522518559)

## [基于 slate.js（不依赖 React）设计富文本编辑器_王福朋_202105](https://juejin.cn/post/6968061014046670884)

- 为何要基于 slate.js ？ 为何不是自研内核？
  - 核心目的，是做出一款稳定、易用、高扩展性的开源产品，并不是搞极客精神和造轮子。
  - 自研成本非常高，耗时长，bug 多。
  - PS：如果你有深度的技术追求，可以先从解读源码、写 demo 开始，看个人精力和能力
- 基于 slate.js 并不意味着就很简单
  - 不依赖 React ，重写 View
  - 设计各种操作功能，如 toolbar 、tooltip 等
  - 设计扩展性，全面插件化
  - 开发各个富文本编辑器功能，特别是复杂的功能，如表格、代码高亮

- 整体设计
- 底层依赖
  - slate.js - 编辑器内核
  - snabbdom - view model 分离，使用 vdom 渲染 view
- view core
  - core 本身没有任何实际功能。需要通过 module 来扩展 formats、menus、plugins 等，来定义具体的功能。
  - editor - 定义 slate 用于 DOM UI 的一些 API
  - text-area - 输入区域 DOM 渲染，DOM 事件，选区同步，
  - formats - 输入区域不同数据的渲染规则，如怎样渲染加粗、颜色、图片、list 等。可扩展注册。
  - menus - 菜单，包括 toolbar、悬浮菜单、tooltip、右键菜单、DropPanel、Modal 等。可扩展注册。
- view-core 。它的核心作用：
  - 劫持用户输入和修改，使用 editor API 去触发 model 修改（或者 selection 修改）
  - editor change 要实时更新到 DOM ，保持 DOM 和 model（或 selection）的同步
  - 定义扩展机制（它本身没有什么实际功能），通过扩展 module 来实现具体的功能

- beforeinput 是一个比较新的 DOM 事件，去年还没有得到普遍支持。当前看来，主流浏览器已经支持了，特别是 FireFox 87 发布之后，参考 caniuse 
  - 对于还不支持的浏览器，可以用 keydown/keypress 来兼容
  - 监听 beforeinput 事件，然后根据不同的 inputType 执行不同的 editor API 。
- selection同步
  - DOM selection 变化会触发 document.addEvenListener('selectionchange', fn)
  - editor selection 变化会触发 editor.onChange事件。这样就可以做到相互同步。
- updateView 同步视图
  - editor onChange 时会触发更新视图，以保证 view 和 model 实时同步。分为两步：
  - 根据 model 生成 vnode
  - patch vnode
  - 第二步很简单，我们利用 snabbdom.js 来做 vdom 渲染
  - 关键在于第一步，生成 vnode 。 我们将逻辑拆分为两段： renderElement 和 renderText
- menu 应该是一个抽象，基于它来生成各种类型的菜单：
  - 传统的工具栏
  - 选中文字、元素之后的悬浮菜单
  - 右键菜单等
  - 还要支持各种类型：button select 等
- editor API 和 plugins
  - 参考 slate-react 源码，定义了一些全局 command ，在渲染 DOM 时很有用
- module 的设计
  - core 没有任何基础功能，所有功能都是 module 来扩展实现。module 可扩展的有：
  - menu
  - formats
    - renderElement
    - addTextStyle
  - plugin（即 slate plugin）
- 后续计划
  - 粘贴
  - 上传
  - i18n

## [富文本编辑器 L1 能力调研记录_王福朋_202104](https://juejin.cn/post/6954896971370856485)

- 写demo基于两个前提
  - 拆分 model 和 view ，使用 vdom 渲染页面
  - 抽象 selection 和 range

- 一开始想要自己绘制光标，不用 contenteditable
  - 通过 range.getClientRects()可以获得选区的位置
  - 在该位置绘制一个 absolute div ，内部 append 一个闪烁的 div 和 input
  - 监听 input keydown ，然后执行文本输入、删除，回车，光标的上下变化

- 后来放弃，因为拖拽选择时，无法同时 focus input ，也就无法监听到 keydown 。
  - 后来经过调研，自己绘制光标的编辑器，都需要使用 iframe （作为第三方 lib 我不想用 iframe），有些甚至需要自己绘制选区（有道云笔记？？）
  - 主要是移动端问题、粘贴问题

- 经过调研，经典的编辑器 Quill slate proseMirror tinyMCE 等都使用 contenteditable 。所以选择它，方向应该不会错。
- 依据我当初想弃用 contenteditable 的想法，就得自己处理文本。我设想的方式是：
  - 监听 input keydown （会考虑防抖）
  - 修改 model ，更新视图，更新 selection
- 使用 contenteditable 之后，编辑区域的修改就变的开放了，在想去劫持 keydown ，范围就会很大，很容易漏掉什么。
- 于是我就把编辑器的修改内容的操作分为两类：
  - 外部调用 API ，例如 js 执行加粗、标题 command
  - 编辑区域内部的改动，因为是 contenteditable ，修改的是开放的，键盘可随便输入、删除、换行等
  - 第二类，我可以用 mutation observer 来监听，不用再去劫持各种 keydown
- 我花费了两天的业余时间，尝试去解读 mutation observer 对于回车换行的处理，但是没搞定。 两天之后我就放弃了，不是知难而退，而是这种情况，即便真的废力气解决了，那也是一个很复杂的设计。
  - Quill 只用 mutation observer 监听文本改动。其他的 enter delete 等，都还是劫持 keydown ，修改 model 。

- 调研其他产品，应该同时多看几个，可以相互弥补。因为只看一个你不可能看懂 100% 。
  - 我花了几天业余时间看了看 Quill slate proseMirror ，从主流程上大概了解了，但还需要进一步探索细节。
- 不是修改 model ，而是重新生成（不可变数据，如用 immer）。副作用会变得不可控，越大越乱。
- command 不会直接修改 model ，而是 command -> operation -> model -> vdom & patchView
- model 并不是 DOM 结构的样子，而是扁平化甚至线性化，这样才能更好的进行 range 操作

- 调研其他作品的关键是什么？精力有限，请务必抓住核心、抓住主要矛盾。
  - 它的重要概念和数据结构，如 Quill 的 Delta
  - 它从 command 到最终 view 渲染的完整流程，以及各个中间阶段

## [Web 富文本编辑器 embed 卡片机制的设计与实践_王福朋_202103](https://juejin.cn/post/6939724738818211870)

## [slate.js - 从基本使用到核心概念_王福朋_202101](https://juejin.cn/post/6917123466307698696)

## [【译】自己实现 document.execCommand 富文本编辑器核心 API_王福朋_202008](https://juejin.cn/post/6864916875390910472)

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

- `beforeinput`表示可编辑的dom在被修改前触发
- 为什么要弃用`MutationObserver`而选用`beforeinput`？
  - 早期页面并没有提供对监听的支持，所以那时要观察 DOM 是否变化，唯一能做的就是轮询检测，比如使用 setTimeout 或者 setInterval 来定时检测 DOM 是否有改变。
  - 直到 2000 年的时候引入了 Mutation Event，Mutation Event 采用了观察者的设计模式，当 DOM 有变动时就会立刻触发相应的事件，这种方式属于同步回调。
  - 这种实时性造成了严重的性能问题，因为每次 DOM 变动，渲染引擎都会去调用 JavaScript，这样会产生较大的性能开销。
  - 从 DOM4 开始，推荐使用 MutationObserver 来代替 Mutation Event。MutationObserver API 可以用来监视 DOM 的变化，包括属性的变化、节点的增减、内容的变化等。
- 我觉得（可能有错）有两点原因：
  - MutationObserver虽然很优秀，但是他的监听如果数据发生变化还需要比较，拿不到最新的变化值，并且还会产生很多无用的节点，不适合slate 的体系
  - 主动操作menu修改样式等无需监听，直接更改slate 的数据模型即可
  - beforeinput 他除了能拿到当前改变的值，还能通过inputType知道当前输入的类型
  - 监听到输入之前的事件之后，就能根据不听的类型调用不同的slate 的api 改变slate 的内部数据模型，在触发回调函数，触发path 渲染dom
# more
- [wangEditor - 开发web富文本编辑器的坑有哪些_202104](https://juejin.cn/post/6951364054224994312)
- 存在的问题
  - 核心代码没有与(业务)功能代码区分开，我们现在不管是处理issue还是新增功能，都是直接在项目中修改。长此以往下去，我们项目最终会演变成一个巨石项目（这也是做插件化的初衷）。
  - 插件与菜单存在强耦合关系，如果用户不需要菜单，把功能去掉后（editor.config.menus = []），功能也会失效。（实际案例：issue#3117）
