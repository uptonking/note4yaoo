---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# dev-2023
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-xp
- ui-starter
  - css-only: open-props, glass-ui, 渐变字体
  - react: spectrum, zigzag, ariakit
- dev-starter
  - patterns: react, typescript
- list-grid-starter
  - plain
    - no sort/filter/group
    - no reorder
    - no column width resize
    - custom cell renderer
  - searchable
  - virtualizable
- list-grid-solutions
  - checkbox
  - draggable/reorder list
  - fields menu - filter/groupable
  - inline editing
  - orm integration
  - sortable-filterable-groupable-table
- 产品日历组件
  - headless-date-picker
- module/fwk/server
  - 灵活的tag/bookmark系统
  - cms, tables, bi
- 编辑器参考
  - atlassian-editor
    - https://atlaskit.atlassian.com/packages/editor/editor-core
    - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
    - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - more-editor
    - https://demo.grammarly.com/

```shell
DEBUG=* npm install --legacy-peer-deps --loglevel silly

$$('[contenteditable]')
```

# dev-review
- dev-goals
  - rich-editor: text/code/block
  - pivot-table
  - collaboration
  - local-first-database
  - annotation/comment/whiteboard/pdf
  - 事项--截止日期(0730+休整)--重要性(hml/s1-s3)
  - rich-editor-vanillajs
  - pivot-table-grid--0828--h
    - dropdown-menu vs tabs
  - app-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901

- deep into lib
  - src-code, issues, pr, forks, extensions/alternatives
# dev-2023-方向+方法+时间
- 👉🏻 output: 代码、产品、生态积累
- slate-wangeditor
  - model, view, sync, collab
- 👉🏻 eg-focalboard
  - table view
  - kanban view
- 👉🏻 eg-tanstack-table-v8
  - [x] 数据全内存: nedb, blinkdb
  - [x] 数据全持久: linvodb, tingodb
  - [ ] 方便接入已有的外部数据源
  - tuple-database
  - tinybase

- 若slate-model层采用扁平化Node
  - 如何保持path和key同步，参考 getKeysToPathsTable, getByKey实现上基于getByPath
  - 优化方向可参考tree的crud及协作
  - 协作时还应该考虑 json patch + last-write-win
  - Node定义采用unist
  - lww的字符串改为针对crdt优化的类型

- collab-sync
  - 👉🏻 string-crdt: ?
  - collab-data-structure: lww-with-hlc
  - remoteStorage: google-drive、网盘、七牛对象存储
  - lo-fi-sync-server
  - pouchdb

- sqlite-web
  - evolu(hlc)
  - kikko
  - absurd-sql-ts: read ArrayBuffer

- long-term
  - cms, airtable, lowcode
- techstacks
  - async, stream, buffer, binary, scheduler, arrow

- 支持切换内存和持久化的示例
  - abstract-level, localforage
  - tanstack-table server-side row model
  - tupledb

- 内容的存储与更新如何与数据库集成
  - 编辑器内容自动保存一般通过在onChange方法中执行saveToDB
    - 也可以在onChange方法中创建内存db、更新索引，通过索引提高计算效率
    - 应该避免维护2份数据
  - 将编辑器的计算密集部分的数据模型不使用普通json对象，而直接用类似数据库模型的设计
  - 为了性能，尽量不要直接读写持久化数据源，要使用缓存object pool

- log2022 数据同步、冲突处理、本地存储
  - 07-focalboard-views
  - 08-block-editor-tiny-write
  - 09-prosemirror-examples
  - 10-prosemirror-collab - otjs - crdt-hlc
  - 11-idb-sync-crdt
  - 12-nedb-linvodb
- log2023
  - 01-linvo-search+tinybase-sync-hlc-wip
  - 02-typewriter-quill+tanstack-table+slate-table
  - 03-crdt-rga+slate-yjs

- why use es6 class
  - 运行时类型检查，instanceof
  - 既包含类型定义，又包含逻辑工具方法
    - 注意class有时也需要先定义interface再实现，此时ts type也合理了
    - 但应用层业务代码一般不需要定义单独interface
  - 方便调试，可直接log到对象及方法，函数里面的闭包变量更新难以定位
    - 也可以提前将需要调试的属性或方法添加到闭包暴露的对象上

- dev-xp-editor
  - 不仅要保持编辑器内容和视图同步，还要保持选区和内容同步

- dev-later
  - crdt tutorials
  - 腰包掉到床头版与墙的夹缝中了
  - 默认last-write-win, 出现冲突时，提示用户选择版本
  - 离屏渲染，keep-alive
  - 分层渲染
# dev-03

## 030

- dev-to
  - 拖拽图标的位置在block左上角，而不是垂直居中
  - 拖拽时原布局不变，只显示预期位置的指示线

- dev-to-collab
  - yOffset out of bounds
  - cursor光标位置经常对不上
  - 每次刷新页面，空白行会多一行

- dev-later
  - merge-cells 逻辑优化
  - cell-floating-menu 右上角
  - 将无序列表项拖进数字列表项时，数字列表项会增加？
  - initialDataLong示例，无法删除首行列表项
  - remove ramda

## 0320

- slate Subsequent property declarations must have the same type. Property
  - 问题暂时解决方法是 将library中declare module slate注释掉，然后在应用层添加此声明

- [fix: replace typeof window checks with typeof document by redabacha · Pull Request · TanStack/virtual](https://github.com/TanStack/virtual/pull/516)
  - useLayoutEffect does nothing on the server warnings during ssr when using a deno runtime. this is because deno has a global window object available for browser compatibility (though is being considered for removal
  - this pr replaces all typeof window checks across all packages with typeof document instead which works in all environments.

- [PBFT Practical Byzantine Fault Tolerance 实用拜占庭容错 - 哪吒young - 博客园](https://www.cnblogs.com/NezhaYoung/p/16170948.html)
  - 实用拜占庭容错，是传统BFT的一种可用性实现，其在联盟链中有广泛应用，但由于pbft 不能动态添加删除节点且节点加入需要认证机制(女巫攻击), 时间复杂度等, 其在公链中其算法的效率, 功能仍然不足满足实际需求。
  - PBFT 适合有准入门槛(防止女巫攻击), 节点数量不多的联盟链
  - PBFT 最大容忍网络中 1/3的拜占庭节点
  - PBFT 的时间复杂度 O(n2), 节点数很多时性能急剧下降

- [了解区块链的基本（第一部分）：拜占庭容错(Byzantine Fault Tolerance)](https://medium.com/loom-network-chinese/%E4%BA%86%E8%A7%A3%E5%8C%BA%E5%9D%97%E9%93%BE%E7%9A%84%E5%9F%BA%E6%9C%AC-%E7%AC%AC%E4%B8%80%E9%83%A8%E5%88%86-%E6%8B%9C%E5%8D%A0%E5%BA%AD%E5%AE%B9%E9%94%99-byzantine-fault-tolerance-8a1912c311ba)
  - 每当一个新的交易被广播到网络中时，节点就可以选择将该交易包含在它们的帐簿副本中，或者忽略它。当组成网络的大多数成员统一意见时，达到了共识。
  - 简单讨论一下不可解的两个将军问题（Two Generals Problem）
    - 这个问题（1975首次发行，1978年被命名）描述了两个将军在攻击同一个敌人的场景。将军1号被认为是领导，而另一个被认为是跟随者。每个将军的军队都无法仅靠自己的力量成功打败敌军，所以他们需要合作并同一时间发起攻击。
    - 延伸到无限的ACK，两位将军将无法达成一致。
    - 两个将军问题已被证实无解。
  - 拜占庭将军问题
    - 它描绘了同一个场景，但两个以上的将军需要对攻打他们共同敌人的时间作出同意。增加的一层复杂性就是，其中一个或几个将军有可能是叛徒，意味着他们可以对他们的选择撒谎
    - 两个将军问题中领导者－跟随者的关系变成了指挥官－中尉的组合。为了在这里达成共识，指挥官和每个中尉必须就同一个决定达成一致（为了简单，只有攻击或撤退）。
    - 如果指挥官是叛徒，还是必须达成共识。结果，所有的中尉成为了多数票。
  - 定理：对于任意m，如果有多于3m的将军和至多m个叛徒，算法OM(m)达到共识。
    - 这说明只要2/3的成员是诚实的，算法就能达到共识。
    - 如果叛徒多于1/3，无法达到共识，这些军队无法协调他们的攻击，敌军胜利
    - 重要的是大多数中尉要选同一个决策，哪一个并不重要。
  - 拜占庭容错
    - 前面提到的算法，只要叛徒的数量不超过将军的三分之一，就是拜占庭容错。其他变形的存在使得解决问题更容易，包括使用数字签名或通过在网络中的对等体之间施加通信限制。

## 0319

- bullet list-item前的黑点，自身是cntEdit为false的button
  - 若使用::before伪元素实现黑点，则光标可点击到黑点左边
  - 若使用button普通内容实现，则光标点击不到光标左边，交互正常

- [TypeScript 2.8.3 Type must have a Symbol.iterator method that returns an iterator - Stack Overflow](https://stackoverflow.com/questions/50234481/typescript-2-8-3-type-must-have-a-symbol-iterator-method-that-returns-an-iterato)
  - "lib": [ "es5", "es6", "dom", "dom.iterable" ]

## 0318

- Array.prototype.reverse()
  - Return the reference to the original array, now reversed. 
  - Note that the array is reversed in place, and no copy is made.

- [css button set to unclickable - Stack Overflow](https://stackoverflow.com/questions/46566019/css-button-set-to-unclickable)
  - pointer-events: none; 
  - 默认值 pointer-events: auto; 

## 0317

- dev-to
  - 🚨 修复中文输入法

- [How to iterate over a WeakMap? - Stack Overflow](https://stackoverflow.com/questions/32402837/how-to-iterate-over-a-weakmap)
  - A JavaScript WeakMap does not allow you to get the key, or the length or size, by design.
  - Is it possible to nevertheless loop over entries in some way ?
  - If not .. how does the Chrome console do this ?
- No, as you say, the contents of a WeakMap are not accessible by design, and there is no iterablity.
- The console uses the debugging API of the JS engine, which allows access to the internals of objects (also to promise states, wrapped primitives, etc.) and many more.

- Things are moving and it will soon be possible to create iterable week maps thanks to weak refs. See the iterable WeakMap example in the tc39 weakrefs proposal.
  - (note that it is already possible with nodejs v12.?.? using --harmony-weak-refs flag)
  - WeakRef and FinalizationRegistry are now Stage 4, since the July 2020 TC39 meeting

- [pipeline执行引擎和一些工程优化 - 知乎](https://zhuanlan.zhihu.com/p/614907875)

## 0316

- [Changing the stroke color for an inline SVG - Stack Overflow](https://stackoverflow.com/questions/37940282/changing-the-stroke-color-for-an-inline-svg)
  - The CSS in the SVG is inline CSS and so is being applied after your stylesheet and thus is overriding it.
  - The simplest solution is to extract the CSS from the SVG and put it **all in your stylesheet**

```svg
<svg class="highlight" width="86" height="68" viewBox="0 0 85.7 68.5">
  <polygon points="11 60.7 74.7 60.7 42.8 4.4 " style="fill:none;stroke-width:3;stroke:#491EC4"/>
</svg>
```

```css
.highlight:hover {
  background-color: pink;
}

.highlight:hover polygon {
  stroke: red !important;
}
```

## 0315

- [合成事件 - 图解React](https://7kms.github.io/react-illustration-series/main/synthetic-event/)
  - 从v17.0.0开始, React 不会再将事件处理添加到 document 上, 而是将事件处理添加到渲染 React 树的根 DOM 容器中.
  - 无论是在document还是根 DOM 容器上监听事件, 都可以归为事件委托(代理)
  - 注意: react的事件体系, 不是全部都通过事件委托来实现的. 有一些特殊情况, 是直接绑定到对应 DOM 元素上的(如:scroll, load), 它们都通过listenToNonDelegatedEvent函数进行绑定.

- [javascript - what's different between Object.prototype.toString.call and typeof - Stack Overflow](https://stackoverflow.com/questions/31459821/whats-different-between-object-prototype-tostring-call-and-typeof)
  - You can't override what gets returned from typeof

```JS
typeof(new Array()) === "object";
typeof(new Date()) === "object";
typeof(new RegExp()) === "object";

Object.prototype.toString.call(new Array()).slice(8, -1) === "Array";
Object.prototype.toString.call(new Date()).slice(8, -1) === "Date";
Object.prototype.toString.call(new RegExp()).slice(8, -1) === "RegExp";
```

- [wasm调试 webAssembly介绍大全 - Bigben - 博客园](https://www.cnblogs.com/bigben0123/articles/15753240.html)
  - C/C++ 到 WebAssembly 代码的编译器 Emscripten 则支持在编译时，为代码注入相关的调试信息，生成对应的 source map，
  - 然后安装 Chrome 团队编写的 C/C++ Devtools Support 浏览器扩展，就可以使用 Chrome 开发者工具调试 C/C++ 代码了。

## 0313

- [css - Chrome DevTools converts all HEX Colors to RGB - Stack Overflow](https://stackoverflow.com/questions/29869426/chrome-devtools-converts-all-hex-colors-to-rgb)
  - open preferences, change Color format 

- [Font-size <12px doesn't have effect in Google Chrome - Stack Overflow](https://stackoverflow.com/questions/2295095/font-size-12px-doesnt-have-effect-in-google-chrome)
  - Chrome and Firefox now allow a minimum font size setting of zero. 
  - **Chrome 73** had downstream problems with this, and since then Chrome changed their policy and user interface for this setting. 
  - I don't know the history on Firefox, and I don't know the state of this setting on Safari or other browsers.

- [Urban Dictionary: shit-faced](https://www.urbandictionary.com/define.php?term=shit-faced)
  - The point at which you have consumed so much alcohol, that you are incoherent(无逻辑的；不连贯的), have difficulty remembering simple things
  - Being 'shit-faced' is usually an experience you only want to try once, and never again.

## 0312

- dev-to
  - 将rga的id从string改为number

- crypto.randomUUID(); 
  - 返回 A string containing a randomly generated, 36 character long v4 UUID.
  - 36 = 8-4-4-4-12 (算上4个连字符)

```JS
1 > null // true
0 > null // false
'aa' > null // false
  '0' > null // false
```

- [How do you JSON.stringify an ES6 Map? - Stack Overflow](https://stackoverflow.com/questions/29085197/how-do-you-json-stringify-an-es6-map)

```JS
jsonText = JSON.stringify(Array.from(map.entries()))

map = new Map(JSON.parse(jsonText))
```

- [Property 'replaceAll' does not exist on type 'string' - Stack Overflow](https://stackoverflow.com/questions/63616486/property-replaceall-does-not-exist-on-type-string)
  - "lib": [ ..., "ESNext. String" ]
  - `replace(/-/g, '')`

- [fixed-length array with optional items in Typescript interface - Stack Overflow](https://stackoverflow.com/questions/44461636/fixed-length-array-with-optional-items-in-typescript-interface)
  - late to the party but one can do simply `type X = [string, string?, number?]` to have optional typed array members 

```typescript
[K in keyof T]?: {
  0: T[K];
  1?: ValidatorFn | ValidatorFn[];
  2?: AsyncValidatorFn | AsyncValidatorFn[];
};

```

## 0310

- [Types when destructuring arrays - Stack Overflow](https://stackoverflow.com/questions/31923739/types-when-destructuring-arrays)

```typescript
const [nodes, counts] = getNodesAndCounts(); // problematic line needed type

const [nodes, counts] = <Node[], number[]>getNodesAndCounts();

// 💡 for-of 解构的折中方案，还可尝试明确backend[0]的类型
for (const [k, v] of Object.entries<any>(backend[0])) 
```

- [Difference between index signature and Record for empty object?](https://stackoverflow.com/questions/54100025/difference-between-index-signature-and-record-for-empty-object)
  - `Record<"A" | "B", boolean>` to get the type `{ A: boolean, B: boolean }` 简洁
  - The main part of this question (in my reading) is whether the two types are the same. 
  - They are obviously declared in different ways but are they the same type. 
  - While they are obviously **compatible** (that is you can assign one to the other and vice-versa) the question is are there corner cases where this is not possible.

## 0308

### [图解Gossip: 可能是最有趣的一致性协议 - charlieroro - 博客园](https://www.cnblogs.com/charlieroro/articles/12655967.html)

- Gossip协议是一个通信协议，一种传播消息的方式，灵感来自于：瘟疫、社交网络等。
- 使用Gossip协议的有：Redis Cluster、Consul、Apache Cassandra等。
- Gossip协议基本思想
  - 一个节点想要分享一些信息给网络中的其他的一些节点。
  - 于是，它周期性的随机选择一些节点，并把信息传递给这些节点。
  - 这些收到信息的节点接下来会做同样的事情，即把这些信息传递给其他一些随机选择的节点。
  - 一般而言，信息会周期性的传递给N个目标节点，而不只是一个。
  - 这个N被称为fanout（这个单词的本意是扇出）。
- Gossip协议的主要用途就是信息传播和扩散：即把一些发生的事件传播到全世界。它们也被用于数据库复制，信息扩散，集群成员身份确认，故障探测等。
- Gossip协议下，没有任何扮演特殊角色的节点（比如leader等）。任何一个节点无论什么时候下线或者加入，并不会破坏整个系统的服务质量。
- 然而，Gossip协议也有不完美的地方，例如，拜占庭问题（Byzantine）。
  - 即，如果有一个恶意传播消息的节点，Gossip协议的分布式系统就会出问题。

## 0307

- [Google diff-match-patch源代码解析：听说比GNU diff-patch更厉害？](https://blog.csdn.net/APPTITE/article/details/107691493)
  - 语义化优先的diff计算
  - 效率优先的diff计算（可以设置diff单元的最小粒度）
  - 设置ddl时间的diff计算（在n秒内完成diff计算操作）

## 0306

- [How to change the Content of a <textarea> with JavaScript - Stack Overflow](https://stackoverflow.com/questions/1642447/how-to-change-the-content-of-a-textarea-with-javascript)
  - document.getElementById('myTextarea').value = ''; 
  - myTextArea.innerHTML = ''; 
  - myTextArea.innerText = ''; 

- [Add "contenteditable" attribute to element using Javascript? - Stack Overflow](https://stackoverflow.com/questions/20906895/add-contenteditable-attribute-to-element-using-javascript)

```JS
elemText.contentEditable = "true";
elemText.setAttribute("contenteditable", "true");
```

- [Why does JSON.parse fail with the empty string? - Stack Overflow](https://stackoverflow.com/questions/30621802/why-does-json-parse-fail-with-the-empty-string)

```JS
JSON.parse('""'); // ✅ 解析为空字符串
JSON.parse(''); // SyntaxError: Unexpected end of JSON input
```

- [reactjs - How to avoid \`loaded two copies of React\` error when developing an external component? - Stack Overflow](https://stackoverflow.com/questions/33157904/how-to-avoid-loaded-two-copies-of-react-error-when-developing-an-external-comp)
  - I believe the answer is to specify react and react-dom as `peerDependencies` in your external component's package.json

## 0305

- [认识 Range 和 Selection 对象](https://coldstone.fun/post/2020/12/05/selection-and-range/)
  - 使文档中某些内容不可选
  - 使用 CSS 属性 `user-select: none` 不允许选择从 elem 开始，但是用户可以在其他地方开始选择，并将 elem 包含在内。
  - 阻止 `onselectstart` 或 `mousedown` 事件中的默认行为，这样可以防止在 elem 上开始选择，但是访问者可以在另一个元素上开始选择，然后扩展到 elem。
  - 使用 `document.getSelection().empty()` 方法在选择发生后清除选择范围。

## 0304

- [Object destructuring with types in TypeScript](https://flaviocopes.com/typescript-object-destructuring/)
  - `const { name, age }: { name: string; age: number } = body.value;`

- dev-to
  - 测试光标进出表格

## 0301

- [XML解析之SAX方式解析xml文件 - Chen洋 - 博客园](https://www.cnblogs.com/cy0628/p/14990908.html)
  - DOM , SAX属于基础方法，是官方提供的平台无关的解析方式；
  - JDOM，DOM4J属于扩展方法，他们是在基础的方法上扩展出来，只适用于Java平台；
  - SAX解析方式会逐行地去扫描XML文档，当遇到标签时会触发解析处理器，采用事件处理的方式解析XML (Simple API for XML) ，不是官方标准，但它是 XML 社区事实上的标准
  - 优点是：在读取文档的同时即可对XML进行处理，不必等到文档加载结束，相对快捷。不需要加载进内存，因此不存在占用内存的问题，可以解析超大XML。
  - 缺点是：只能用来读取XML中数据，无法进行增删改。

- [[翻译] Makefile - 失落的艺术 - 知乎](https://zhuanlan.zhihu.com/p/34284231)
  - 挺好，不过在使用 nodejs 的情况下，没有道理不使用 npm scripts (作为 Makefile 的替代品) 
  - nodejs脚本也是跨平台的，但依赖js语言，makefile有自己的语法规则

- [快速的理解MakeFile+读懂一个MakeFile - 知乎](https://zhuanlan.zhihu.com/p/350297509)
  - Make 是一种通用的构建工具，它自40年前推出以来一直在不断完善和改进。 
  - Make 非常擅长简洁的表现构建步骤，此外它并不特定用于 JavaScript 项目。 
  - 它非常适合增量构建，在更改大型项目中的一个或两个文件后重新构建时，Make 可以节省大量时间。

- [plugin-react: is it using esbuild or babel? · vitejs/vite · Discussion #8142](https://github.com/vitejs/vite/discussions/8142)
  - plugin-react uses babel (you can see the code here), there are several pieces of the React ecosystem that still requires it (babel isn't used in Vue or Svelte). 
  - esbuild is still used by Vite when you are using this plugin though.
  - A production build in general is using rollup, so you can't expect it to be as fast as bundling with esbuild. 

- Vite’s default React HMR is still babel-based, _202210
- https://twitter.com/youyuxi/status/1585040270957379585?lang=en
  - while Next/turbopack use swc/rust-based transform, so the HMR performance difference is a bit of apples to oranges.
  - Vite can switch to the swc/rust transform if necessary, we currently chose not to do that because adding swc to the deps list is extra weight, and even without it HMR is fast enough.
  - In the long run we may also consider using turbopack under the hood to replace esbuild/Rollup (where suitable), due to its strong caching capabilities.
  - [feat!: transform jsx with esbuild instead of babel by rtsao · Pull Request #9590 · vitejs/vite_202211](https://github.com/vitejs/vite/pull/9590)
# dev-02

## 0228

- [XMPP协议实现原理介绍 - Healtheon - 博客园](https://www.cnblogs.com/hanyonglu/archive/2012/03/04/2378956.html)
  - XMPP（Extensible Messageing and Presence Protocol：可扩展消息与存在协议）是目前主流的四种IM（IM：instant messaging, 即时消息）协议之一，其他三种分别为：即时信息和空间协议(IMPP)、空间和即时信息协议(PRIM)、针对即时通讯和空间平衡扩充的进程开始协议SIP(SIMPLE)。
  - 在这四种协议中，XMPP是最灵活的。XMPP是一种基于XML的协议，它继承了在XML环境中灵活的发展性。
  - 其实XMPP 是一种很类似于http协议的一种数据传输协议，它的过程就如同“解包装--〉包装”的过程，用户只需要明白它接受的类型，并理解它返回的类型，就可以很好的利用xmpp来进行数据通讯。
  - 1)客户机/服务器通信模式；(2)分布式网络；(3)简单的客户端；(4)XML的数据格式。

## 0227

- 🤔 输入字母时，为什么beforeinput的selection为5，onChange方法里的selection为6，哪里更新的
  - 首先确认更新范围，onChange执行后useEffect才执行将 slateSel-TO-domSel，所以更新sel发生在渲染前
  - 排查定位到，执行op `insert_text`时，顺便就把selection更新了
  - 不要在op-text单独执行op-selection来更新sel

- Unlike a `Range`, a `StaticRange` represents a range which is fixed in time; 
  - it does not change to try to keep the same content within it as the document changes. 
  - If any changes are made to the DOM, the actual data contained within the range specified by a StaticRange may change. 
  - This lets the user agent avoid a lot of work that is unnecessary if the web app or site doesn't need a live-updating range.

## 0225

- [JavaScript中对光标和选区的操作 - 前端简单说 - SegmentFault 思否](https://segmentfault.com/a/1190000040211043)
  - 使用 ::selection 选择器可以匹配被选中的部分。
  - 目前只有一小部分 CSS 属性可以用于 ::selection 选择器：
  - color, background-color, text-shadow

- [重新认识Selection和Range | 漫漫前端路](https://blog.renwangyu.com/2020/10/06/selection-and-range/)

- `getRootNode()` method of the Node interface returns the context object's root, which optionally includes the shadow root if it is available.
  - 一般返回`document`对象，而不是document.documentElement

```JS
document.body.ownerDocument === document // true

document.body.ownerDocument === document.body.getRootNode() // true
```

- [css - How can I inspect and tweak :before and :after pseudo-elements in-browser? - Stack Overflow](https://stackoverflow.com/questions/10174719/how-can-i-inspect-and-tweak-before-and-after-pseudo-elements-in-browser)
  - getComputedStyle(document.querySelector('html > body'), ':before'); 
  - getComputedStyle(element, pseudoElt)

- HTMLElement.contextMenu 
  - Deprecated
  - refers to the context menu assigned to an element using the contextmenu attribute
  - The menu itself is created using the `<menu>` element
  - Deprecated: The `contextmenu` global attribute is the `id` of a `<menu>` to use as the contextual menu for this element.

- contextmenu event fires when the user attempts to open a context menu
  - not deprecated

- [Difference between microtask and macrotask within an event loop context - Stack Overflow](https://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context)
  - Macro tasks include keyboard events, mouse events, timer events (setTimeout) , network events, Html parsing, changing Urletc. A macro task represents some discrete and independent work. micro task queue has higher priority so macro task will wait for all the micro tasks are executed first.
  - Microtasks, are smaller tasks that update the application state and should be executed before the browser continues with other assignments such as re-rendering the UI. Microtasks include promise callbacks and DOM mutation changes. Microtasks enable us to execute certain actions before the UI is re-rendered, thereby avoiding unnecessary UI rendering that might show an inconsistent application state.
  - Separation of macro and microtask enables the event loop to prioritize types of tasks; for example, giving priority to performance-sensitive tasks.

## 0224

- [Difference between mousedown and click in jquery - Stack Overflow](https://stackoverflow.com/questions/19109754/difference-between-mousedown-and-click-in-jquery)
  - onMouseDown will trigger when either the left or right (or middle) is pressed.
  - onClick will only trigger when the left mouse button is pressed and released on the same object.
  - order: onMouseDown, onMouseUp, then onClick

## 0223

- [Phind: AI search engine](https://phind.com/)
  - The AI search engine for developers

### [How to Measure JavaScript Execution Time](https://dev.to/saranshk/how-to-measure-javascript-execution-time-5h2)

- Using Date.now() that returns the total number of milliseconds elapsed since the Unix epoch

- console.time() method starts a timer with a label. And a subsequent call to the console.timeEnd() method with the same label will output the time elapsed since the method was started.

- Console timers do not provide high accuracy. If we want accuracy in 1-millisecond increments, we can use high-resolution timers like performance.now().

## 0222

- [The dataset cannot set dashed names · Issue #1031 · snabbdom/snabbdom](https://github.com/snabbdom/snabbdom/issues/1031)
  - the easiest correction might be using setAttribute/removeAttribute only.
- [dataset module · Issue #90 · snabbdom/snabbdom](https://github.com/snabbdom/snabbdom/issues/90)
  - Both `{attrs: {'data-foo': foo}}` and `{dataset: {foo: 'foo'}}` modify the underlying HTML so I am not sure if it is not be better to simply use some random custom property instead: {props: {datasetfoo: 'foo'}}.

- [Is there a way selecting MULTIPLE areas of text with JS in Chrome and/or IE? - Stack Overflow](https://stackoverflow.com/questions/4985284/is-there-a-way-selecting-multiple-areas-of-text-with-js-in-chrome-and-or-ie)
  - No. Of the major browsers, only Firefox supports multiple ranges within the user selection. 
  - Other browsers (WebKit, Opera, IE9) do have the Selection API to support multiple ranges but do not currently support it. 
  - WebKit is apparently not planning to add support any time soon. As to Opera and IE, I have no idea.

- [How to add more than 1 range to a windows.selection object in chrome browser? - Stack Overflow](https://stackoverflow.com/questions/54437485/how-to-add-more-than-1-range-to-a-windows-selection-object-in-chrome-browser)
  - Not really, actually it's even been removed from specs. This is an old relic from Netscape that FF did keep and which made the Selection API have things like rangeCount or removeAllRanges(), but this behavior is non-standard. 
  - 💡 To do what you wish, you'd have to keep yourself track of what the selected cells were, and to merge their content in a single hidden Node that you'll use as the source for execCommand('copy'). That's a bit of work though...

- [Can you set and/or change the user’s text selection in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/4183401/can-you-set-and-or-change-the-user-s-text-selection-in-javascript)
  - is it possible to select different ranges simultaneously. I want to be able to select multiple parts of text that are discontinuous
  - Yes, but only in Firefox. Call addRange() for each range you want to select

- [Unable to add 2nd selection range (Google Chrome) - Stack Overflow](https://stackoverflow.com/questions/61962880/unable-to-add-2nd-selection-range-google-chrome)
  - in default chrome, multiple selection ranges isn't supported. But this extension can enable it.

## 0219

- [Height limitations for browser vertical scroll bar - Stack Overflow](https://stackoverflow.com/questions/34931732/height-limitations-for-browser-vertical-scroll-bar)
  - The maximum limit for height obtained to render browser scroll bar have various values in all browsers. If increasing 1px from the limited height then the browser scroll won't render in the page.
  - FF: 17895697px
  - IE: 10737418px
  - In Chrome there is no problem to render the scroll bar, but it have always 33554400px height in the layout.

- [javascript - Will ref callbacks always be invoked in the order they are declared in render()? - Stack Overflow](https://stackoverflow.com/questions/60549295/will-ref-callbacks-always-be-invoked-in-the-order-they-are-declared-in-render)
  - React will call the ref callback with the DOM element when the component mounts, and call it with null when it unmounts. Refs are guaranteed to be up-to-date before componentDidMount or componentDidUpdate fires.

## 0215

- You can call `Document.getSelection()`, which works identically to `Window.getSelection()`.
  - getSelection() doesn't work on the content of `<textarea>` and `<input>` elements in Firefox, Edge (Legacy) and Internet Explorer.
  - `HTMLInputElement.setSelectionRange()` or the `selectionStart` and `selectionEnd` properties could be used to work around this.

## 0214

- [How can I use an object literal to make an instance of a class without useing the constructor in JavaScript ES6? - Stack Overflow](https://stackoverflow.com/questions/47881111)
  - I'll guess that this exercise is looking for a solution that uses `__proto__` as an object literal key
  - 👉🏻 The proper solution is to use `Object.create`

```JS
var fakePoint = {
  __proto__: Point.prototype,
  x: Math.random(),
  y: Math.random()
};
console.log(fakePoint instanceof Point) //true
```

- [What is the difference between typeof and instanceof and when should one be used vs. the other? - Stack Overflow](https://stackoverflow.com/questions/899574)
  - Use instanceof for custom types
  - Use typeof for simple built in types

- [Why does instanceof return false for some literals? - Stack Overflow](https://stackoverflow.com/questions/203739/why-does-instanceof-return-false-for-some-literals)
  - Primitives are a different kind of type than objects created from within Javascript.

```JS
var color1 = new String("green");
color1 instanceof String; // returns true
var color2 = "coral";
color2 instanceof String; // returns false (color2 is not a String object)
```

## 0213

- [Impossible to define static 'length' function on class · Issue #442 · microsoft/TypeScript](https://github.com/microsoft/typescript/issues/442)
  - I don't think the properties name, caller and length are doable. They are read-only properties and can't be overridden. All assignments to them will be ignored.

## 0208

- [Wechaty 实现微信机器人的原理 - 知乎](https://zhuanlan.zhihu.com/p/567250559)

- [各类期刊的区别 | J. Xu](https://xujinzh.github.io/2020/10/09/journal-or-transactions/)
  - Journal学报最典型的叫法， 刊登关于某特殊主题的文章的期刊。要求有很大的创新点，比较详细的公式推导。因 Journal 面向的读者较广泛，因此发表在其上的文章需要对背景知识有更加全面的介绍。
  - Transactions 本意为商业交易和谈判，引申为公开发表的大会记录。后来有汇刊的意思。 其具体到一个相对较细的专业方向上，发表在 transactions 上的文章需要有很大的创新和详细的公式推导。
  - Proceedings 表示某行动，或行动过程或方式，引申意之一是学术团体或其他正规团体会议所讨论问题的记录，进一步有会议论文集的意思。有会刊、记录、会议录的意思。但是 IEEE 的 Proceedings 也变成了期刊 (出版周期相对长)，并没有会议支撑。

## 0210

- [rg process taking up all my CPU 100% · Issue #98594 · microsoft/vscode](https://github.com/microsoft/vscode/issues/98594)
  - `"search.followSymlinks": false` solved my issue too

## 0205

- npm ERR! Invalid comparator: github:thecodrr/htmlparser2
  - [[BUG] \`overrides\` in \`package.json\` do not allow file paths of any kind (including fake ones) · Issue #5843 · npm/cli](https://github.com/npm/cli/issues/5843)
  - I really hope this can be fixed. Overrides otherwise only fully work in npm v8.
  - npm v9 最新版已修复
# dev-01

## 0126

- SyntaxError: Named export 'WebSocketServer' not found. The requested module 'ws' is a CommonJS module, which may not support all module.exports as named exports.
  - 原因是 ws 不在dependencies列表里

- ### [Why is there no same-origin policy for WebSockets? Why can I connect to ws://localhost? - Stack Overflow](https://stackoverflow.com/questions/23674199)
- WebSockets can cross domain communication, and they are not limited by the SOP (Same Origin Policy).
- The same security issue you described can happen without WebSockets.
- The evil JS can:
  - Create a script/image tag with a URL to evil.tld and put data in the query string.
  - Create a form tag, put the data in the fields, and invoke the "submit" action of the form, doing an HTTP POST, that can be cross domain. AJAX is limited by the SOP, but normal HTTP POST is not. Check the XSRF web security issue.
- If something injects javascript in your page, or you get malicious javascript, your security is already broken.

- SOP/CORS does not apply to WebSocket, but browsers will send an `origin` header that contains the hostname of the server that served the HTML with the JS that opened the WebSocket connection. A WebSocket server can then restrict access by checking `origin`.

## 0123

- [node.js - Difference between process.nextTick and queueMicrotask - Stack Overflow](https://stackoverflow.com/questions/55467033/difference-between-process-nexttick-and-queuemicrotask)
  - It is the same, in the way of both of them are to execute a task just after the execution of the current function or script.
  - They have different queues. The nextTick's queue is managed by node and the microtask one is managed by v8.
  - The nextTick queue is checked first after the current function/script execution, and then the microTask one.
  - There is no performance gain, the difference is that the nextTick queue will be checked first after the function/script execution 

## 0119

- 💡 a global event emitter (could be replaced by redis, etc)

## 0121

- Downloading ripgrep failed: TypeError [ERR_INVALID_PROTOCOL]: Protocol "https:" not supported. Expected "http:"
  - https://github.com/microsoft/vscode-ripgrep/issues/26#issuecomment-1187663914

```
1. Clone ripgrep locally: git clone git@github.com:microsoft/vscode-ripgrep ~/vscode-ripgrep
2. run yarn in that folder (this seems to work even behind proxy)
3. cp bin/rg ~/vscode-repo-path/node_modules/@vscode/ripgrep
4. run yarn in your vscode repo path again
```

## 0118

### [既然有 HTTP 请求，为什么还要用 RPC 调用？ - 知乎](https://www.zhihu.com/question/41609070)

- rpc是远端过程调用，其调用协议通常包含传输协议和序列化协议。
  - 传输协议包含: 如著名的 [gRPC](grpc / grpc.io) 使用的 http2 协议，也有如dubbo一类的自定义报文的tcp协议。
  - 序列化协议包含: 如基于文本编码的 xml json，也有二进制编码的 protobuf hessian等
- 为什么要使用自定义 tcp 协议的 rpc 做后端进程通信？
  - 要解决这个问题就应该搞清楚 http 使用的 tcp 协议，和我们自定义的 tcp 协议在报文上的区别。
  - 首先要否认一点 http 协议相较于自定义tcp报文协议，增加的开销在于连接的建立与断开。http协议是支持连接池复用的，也就是建立一定数量的连接不断开，并不会频繁的创建和销毁连接。
  - 二要说的是http也可以使用protobuf这种二进制编码协议对内容进行编码，因此二者最大的区别还是在传输协议上。
- 通用定义的http1.1协议的tcp报文包含太多废信息，
  - 即使编码协议也就是body是使用二进制编码协议，报文元数据也就是header头的键值对却用了文本编码，非常占字节数。

- 所谓的效率优势是针对http1.1协议来讲的，http2.0协议已经优化编码效率问题，像grpc这种rpc库使用的就是http2.0协议。这么来说吧http容器的性能测试单位通常是kqps，自定义tpc协议则通常是以10kqps到100kqps为基准
- 简单来说成熟的rpc库相对http容器，更多的是封装了“服务发现”，"负载均衡"，“熔断降级”一类面向服务的高级特性。可以这么理解，rpc框架是面向服务的更高级的封装。如果把一个http servlet容器上封装一层服务发现和函数代理调用，那它就已经可以做一个rpc框架了。

- 用rpc和http跟业务需求有关系，其实rpc可以用http协议实现

## 0116

- 加减乘除表示运算：plus minus multiply divide
- 和差积商表示运算结果：sum difference product quotient

```JS
new Date('1970-01-01T00:00:00').getTime() // local时间， -280000

new Date('1970-01-01').getTime() // 0
```

- ⭐️ new Date().getTime() 总是13位

- [Deterministic length of JS new Date().getTime() string in the modern era: Unix Epoch Time - Stack Overflow](https://stackoverflow.com/questions/69995741/deterministic-length-of-js-new-date-gettime-string-in-the-modern-era-unix-e)
  - The timestamp is milliseconds since 1970-01-01 00:00:00 UTC (the same as the Unix epoch).
  - if it overflows to 14 digits, the , which is 8, 362, 906, 319, 000
  - 10000000000000/1000/3600/24/365 = 317 年

- [encryption - Hashing a string to a specific length - Stack Overflow](https://stackoverflow.com/questions/45221412/hashing-a-string-to-a-specific-length)
  - Non-cryptographic hashes usually have a wider range of sizes available. For a non-crypto hash I often suggest the FNV hash, which is easy to implement and offers a wide range of output sizes: 32 bits to 1024 bits.
  - 自定义编码解码即可，无需加密

## 0115

- [Typescript generic type parameters: `T` vs `T extends {}` - Stack Overflow](https://stackoverflow.com/questions/61648189/typescript-generic-type-parameters-t-vs-t-extends)
  - in TypeScript 3.5 a change was made so that generic type parameters are implicitly constrained by `unknown` instead of the empty object type `{}`
  - If you don't explicitly constrain a generic type parameter via `extends XXX`, then it will implicitly be constrained by `unknown`, the "top type" to which all types are assignable. So in practice that means the `T in funcA<T>()` could be absolutely any type you want.
  - the empty object type `{}`, is a type to which nearly all types are assignable, except for `null` and `undefined`. Even primitive types like string and number are assignable to {}.

## 0113

### [深入理解Vite核心原理 - 知乎](https://zhuanlan.zhihu.com/p/467325485)

- Vite主要利用浏览器ESM特性导入组织代码，在服务器端按需编译返回，完全跳过了打包这个概念，服务器随起随用。
  - 快速的冷启动: No Bundle + esbuild 预构建
  - 真正的按需加载: 利用浏览器ESM支持，实现真正的按需加载
- Vite相比于Webpack而言，没有打包的过程，而是直接启动了一个开发服务器devServer。
  - Vite劫持浏览器的HTTP请求，在后端进行相应的处理将项目中使用的文件通过简单的分解与整合，然后再返回给浏览器(整个过程没有对文件进行打包编译)。所以编译速度很快。
- Snowpack 首次提出利用浏览器原生ESM能力的打包工具，其理念就是减少或避免整个bundle的打包。默认在 dev 和 production 环境都使用 unbundle 的方式来部署应用。但是它的构建时却是交给用户自己选择，整体的打包体验显得有点支离破碎。

- ESM提供了更原生以及更动态的模块加载方案，最重要的就是它是浏览器原生支持的
  - 👉🏻 我们可以直接在浏览器中去执行import，动态引入我们需要的模块，而不是把所有模块打包在一起。
- ESM的执行可以分为三个步骤：
  - 构建: 确定从哪里下载该模块文件、下载并将所有的文件解析为模块记录
  - 实例化: 将模块记录转换为一个模块实例，为所有的模块分配内存空间，依照导出、导入语句把模块指向对应的内存地址。
  - 运行：运行代码，将内存空间填充
- 从上面实例化的过程可以看出，ESM使用实时绑定的模式，导出和导入的模块都指向相同的内存地址，也就是值引用。而CJS采用的是值拷贝，即所有导出值都是拷贝值。

- vite核心原理
  - 当声明一个 script标签类型为 module 时,                                                                                                                    `<script type="module" src="/src/main.js"></script>`; 
  - 当浏览器解析资源时，会往当前域名发起一个GET请求main.js文件
  - 请求到了main.js文件，会检测到内部含有import引入的包，又会import 引用发起HTTP请求获取模块的内容文件，如App.vue、vue文件
- Vite其核心原理是利用浏览器现在已经支持ES6的import, 碰见import就会发送一个HTTP请求去加载文件，
  - Vite启动一个 koa 服务器拦截这些请求，并在后端进行相应的处理将项目中使用的文件通过简单的分解与整合，然后再以ESM格式返回返回给浏览器。
  - Vite整个过程中没有对文件进行打包编译，做到了真正的按需加载，所以其运行速度比原始的webpack开发编译速度快出许多！

- 在Vite出来之前，传统的打包工具如Webpack是先解析依赖、打包构建再启动开发服务器，Dev Server 必须等待所有模块构建完成，当我们修改了 bundle模块中的一个子模块， 整个 bundle 文件都会重新打包然后输出。项目应用越大，启动时间越长。

- 而Vite利用浏览器对ESM的支持，当 import 模块时，浏览器就会下载被导入的模块。先启动开发服务器，当代码执行到模块加载时再请求对应模块的文件, 本质上实现了动态加载。灰色部分是暂时没有用到的路由，所有这部分不会参与构建过程。随着项目里的应用越来越多，增加route，也不会影响其构建速度。

- 目前所有的打包工具实现热更新的思路都大同小异：主要是通过WebSocket创建浏览器和服务器的通信监听文件的改变，当文件被修改时，服务端发送消息通知客户端修改相应的代码，客户端对应不同的文件进行不同的操作的更新。

- 基于esbuild的依赖预编译优化，为什么需要预构建？
  - 支持commonJS依赖，将commonJs的文件提前处理，转化成 ESM 模块并缓存入
  - 减少模块和请求数量
  - Vite预编译之后，将文件缓存在node_modules/.vite/文件夹下。

## 0111

- [--es-module-specifier-resolution=node not working from v13.0.1 · Issue #30520 · nodejs/node](https://github.com/nodejs/node/issues/30520)
  - we have renamed the flag, but we continue to support `--es-module-specifier-resolution=node` which silently aliases to `--experimental-specifier-resolution`

## 0109

- [Feature: Documenting Promises · Issue · jsdoc/jsdoc](https://github.com/jsdoc/jsdoc/issues/509)
  - jsdoc对promise，暂不支持

- [Summary of `process.env.NODE_ENV` and its use with Webpack by markerikson(redux)](https://gist.github.com/markerikson/6776848172c33aaa4db882627c689e18)

- [Can I mark code blocks as production or development only with webpack? - Stack Overflow](https://stackoverflow.com/questions/50997670/can-i-mark-code-blocks-as-production-or-development-only-with-webpack)
  - emphasize again: The code really disappears if the condition is not met. Only an empty if statement appears on the output. 

```JS
var environment = process.env.NODE_ENV || 'development';

if (process.env.NODE_ENV === 'production') {
  // Code will only appear in production build.
}

if (process.env.NODE_ENV !== 'production') {
  // Code will be removed from production build.
  console.log("Looks like you're a developer.");
}

// process.env is a reference to your environment, so you have to set the variable.
// on windows:
SET NODE_ENV = development
// on macOS / OS X or Linux:
export NODE_ENV = development
// cross-env NODE_ENV=development node server.js
```

## 0112

- [exports is not defined in ES module scope - Stack Overflow](https://stackoverflow.com/questions/71478604/exports-is-not-defined-in-es-module-scope)
  - 使用ts-node执行ts却忘了拷贝 tsconfig.json

## 0108

- 测试mocha时，不能稳定复现 Database is not open/closed
  - db.clear: Delete all entries or a range. Not guaranteed to be atomic. 
  - 解决方法不是写多遍，而是使用 `try-catch`

```JS
// ❌
await d.store.close();
await d.store.close();

// ✅
try {
  await d.store.close();
} catch (e) {
  await d.store.close();
}
```

## 0107

- mocha的异步测试异常
  - Error: Timeout of 2000ms exceeded. For async tests and hooks, ensure "done()" is called; if returning a Promise, ensure it resolves.
  - 对于async的callback方法cb1，若cb1内部有await，可尝试在await后expect断言前使用`setTimeout(done, 50)`，让done方法异步被执行

- [Correct way to use done() while testing asyc/await with mocha - Stack Overflow](https://stackoverflow.com/questions/52449202/correct-way-to-use-done-while-testing-asyc-await-with-mocha)
  - The correct way is to not use `done` with `async..await`. 
  - Mocha supports promises and is able to chain a promise that is returned from `it`, etc. functions.
  - `done` is needed only for testing asynchronous APIs than don't involve promises. Even then, converting to promises often results in cleaner control flow.

```JS
it('Testing insertDocumentWithIndex', async () => {
  var data = await db.insertDocumentWithIndex('inspections', {
    "inspectorId": 1,
    "curStatus": 1,
    "lastUpdatedTS": 1535222623216,
    "entryTS": 1535222623216,
    "venueTypeId": 1,
    "location": [
      45.5891279,
      -45.0446183
    ]
  })
  expect(data.result.n).to.equal(1);
  expect(data.result.ok).to.equal(1);
})
```

- [Describe block with async function behaving weirdly · mochajs/mocha](https://github.com/mochajs/mocha/issues/2975)
  - Mocha's describe blocks do not support (as in waiting for resolution of) returned promises. 

## 0105

- [Import '.json' extension in ES6 Node.js throws an error](https://stackoverflow.com/questions/60205891/import-json-extension-in-es6-node-js-throws-an-error)
- `node --experimental-json-modules ./your-file.js`

```JS
import packageFile from "../../package.json"
assert { type: "json" };

const {
  name,
  version
} = packageFile;

// The dynamic import version looks like this:

const {
  default: {
    name,
    version
  }
} = await import("../../package.json", {
  assert: {
    type: "json"
  }
});
```

- [ShopifyQL Notebooks · Shopify Help Center](https://help.shopify.com/en/manual/reports-and-analytics/shopifyql-notebooks)
  - ShopifyQL Notebooks is an app that enables you to query, explore, and visualize your business’ data.

## 0104

- Each time you're introducing a Boolean field in a Database schema, use a timestamp instead. Future You will thank you. 

```JS
isPublished = true;
if (isPublished) console.log(';; true');

isPublished = new Date();
if (isPublished) console.log(';; true');
```
