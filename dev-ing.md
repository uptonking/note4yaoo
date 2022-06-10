---
title: dev-ing
tags: [dev]
created: '2022-05-24T17:52:58.048Z'
modified: '2022-05-24T17:53:08.400Z'
---

# dev-ing

# dev-2022
- 分析核心需求和问题，拆分问题，梳理任务、子任务

## dev-xp

- my-next
  - dev-starter
    - react patterns
    - typescript patterns
    - mvc dev pattern(for app)  ~~in data grid~~
  - readonly-list-grid
    - plain
      - no sort/filter/group
      - no reorder
      - no column width resize
      - custom cell renderer
    - searchable
    - virtualizable
  - crud-list-grid
    - checkbox
    - draggable/reorder list
    - fields menu - filter/groupable
    - inline editing
    - orm integration
  - sortable-filterable-groupable-table

- 产品日历组件
  - headless-date-picker

- 编辑器参考
  - atlassian-editor
    - https://atlaskit.atlassian.com/packages/editor/editor-core
    - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
    - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html

- [新产品设计稿figma](https://www.figma.com/file/7pyx5gMz6CN0qSRADmScQ7/AFFINE?node-id=0%3A1)

```JS
console.log(';; r1-user-spaces ', pathname, user, userSpaces, currentSpaceId);
```

- daily-notes
  - 日历关联的部分
    - 实现大日历
    - 实现大日历与小日历切换的交互
    - 弹窗modal中展示大日历
  - 顶部日期导航条可用
  - daily文章部分由多维表格实现，提前准备好daily数据逻辑

- daily-notes-page-contents，四个部分都是普通文档形式
  - pinned desktop icons
    - 可折叠
  - tasks收集，以多维表格的形式自动生成标签，可切换看板
    - in-progress
    - overdue
    - completed
  - imported info
    - 笔记
    - 代办
  - activities
    - 创建文档
    - 更新文档

- block-editor产品需求讨论
- ✨️ subpage相关
  - 创建subpage
    - 通过斜杠菜单
  - subpage标题同步
    - 在service层对一个page中引用的所有page添加监听器
  - subpage与page-tree同步
    - 🤔️更好的方案
    - 创建subpage时更新db里面tree数据源
- ✨️ backlinks功能讨论
  - 双[[唤起的交互面板
    - 创建backlink时需要能搜索并选择已有page
    - 面板功能和交互设计
  - link和backlink如何区别
    - 🤔️notion似乎没有普通超链接，media细分为 image/video/audio/file/web-bookmark/code
    - notion粘贴普通url后会自动提示创建bookmark或embed，都会展示为卡片
  - page全局backlinks统计
    - notion显示在题头位置
    - 功能上能相互跳转
      - 🤔️ pageA引用pageB，如何从pageB跳转到pageA的引用位置
  - backlink的title会统一动态更新
  - 交互细节
    - 双[[默认唤起双链搜索的交互，但按退格键后可以默认展示双[[文本
    - 在当前文档中可以链接当前文档自身

- dev-to-later-v0429
  - [x] calendar-heatmap sync
  - daily notes pages init
  - calendar-big 进度沟通
  - authing-overseas 变更收集
  - 重构editor
  - 顶部七天周日，是否始终将当天放在第4个居中的位置
  - 顶部七天周日，是否要支持键盘横向滚动，前后滚动7天？10天？
  - 修改默认workspace名称的逻辑，presetWorkspace
  - [] page和page-tree同步正常，page和navbar同步不正常

## dev-ing

- 拖拽逻辑继续
  - 拖拽block到左右上下要放进去，dragend事件
  - 菜单ui实现
  - 拖拽时，没有显示横排布局

- dev-to-draft
  - [ ] 使用command方式迁移text bold/italic

## 0610

- dev-to
  - slate link的悬浮信息弹框应该使用mui的popover实现，而不是使用tooltip
  - [ ] link编辑框的回车事件要正确更新slate model数据
  - [x] 编辑link时要立即隐藏link悬浮框
    - 还存在link文字突然变黑又变白引起的闪烁问题
    - 编辑link链接的modal总input无法检测到ESC按键，但可click-away隐藏modal
  - [x] 在link输入框输入斜杠会意外触发斜杠菜单的keydown计算逻辑
    - 通过在弹出框元素keydown时先将slate-text的selection设为空，然后enter时恢复selection解决，这样输入时就不会触发selection相关事件

- isLinkActive的实现思路
  - Editor.nodes  + n => n.type === 'link'

- anchor元素的href和onClick同时存在时
  - 若onClick中也存在路由跳转，则页面会先跳转onClick的url，再跳转href的url，共跳转2次
  - If your onclick function returns false， the default browser behaviour is cancelled
  - [HTML anchor tag with Javascript onclick event](https://stackoverflow.com/questions/7347786)

- [React link OnClick prevent href](https://stackoverflow.com/questions/54921684)
  - e.stopPropagation(); e.preventDefault(); 
  - e.nativeEvent.stopImmediatePropagation(); 
  - return false; 
  - none of those seem to work.
  - Returning false has been deprecated since React 0.12.

- mui: 当文字很小且很短时，如只有2个字符，hover到文字上鼠标稍微移动一点点tooltip立即就消失了
  - 原因排查定位是由于hover时会触发悬浮挂件面板导致的，下面会显示挂件面板和链接信息面板
  - [Tooltip appears too far from the hovering element](https://github.com/mui/material-ui/issues/27220)
  - This is done on purpose. If the distance was smaller, the tooltip would be covered by the cursor.

## 0609

- block-editor基于多编辑器实例
  - pros
    - 将slate作为主体应用渲染层的一小部分，开发者对数据和定制掌控力更强，方便替换掉slate
  - cons
    - 处理跨block选区需要自己计算选取信息和计算文字偏移量
    - 需要自己实现基础计算：选区、光标、键盘、滚动条

- block-editor基于单编辑器实例
  - pros
    - 更易复用slate的selection、工具方法
  - cons
    - 实现水平分栏可能更复杂

- 普通react table组件和基于slate的table有什么区别？

## 0608

- theme方案选择
  - import theme对象字面量，使用时直接 theme.color.primary.blue500
    - 缺点是编译时就打包进了theme，不支持动态切换主题
    - style9不支持主题切换
  - 通过ThemeProvider的方式传下去
    - 方便动态切换主题

- block-editor在鼠标选择后快捷键失效的问题
  - 因为selectionManager在处理跨block选择时，有一个设置contenteditable为false的逻辑，false后就不接收快捷键
  - notion的处理方式是，在chrome下整个editor顶层套一个额外的contenteditable-div，所以始终可以移动光标；在其他浏览器下不需要套额外的div

- 自动标号，可以手动重新开始标号，可以在中间插入其他元素
  - 不要纠结，忽略非核心问题

- 苹果wwdc发布了官方的白板，官方推广了概念，降低了运营成本
  - logo: better than apple free form

- 飞书发布了block-editor (炫酷的功能，但可能不实用；飞书推广概念降低我们的运营成本)
- 亮点是拖动实现水平并排布局，并排后可调节每栏宽度
  - 分栏默认最多5个，之后不可再次添加分栏
  - 日程可以拖到分栏里面，但多维表格不能拖到

## 0607

- link的实现和难点
  - link作为单独的插件实现，还是放在inline-menu里面实现
    - ❓ 甚至可以放在text组件内部实现，从外部更新slate-text组件
- 👉 还是通过单独的插件实现，插件间的唤起与通信通过单独的eventemitter实现
  - 优点是其他组件也可以唤起link弹出框

- link的需求和设计
  - 添加链接的输入框是否类似notion显示一个简单输入框 ❓
    - notion输入框输入文字可以直接创建page
    - 输入链接，则下面可以将选中文字转换为链接
  - 默认样式，灰字，是否需要下划线 ❓
  - 鼠标悬浮时，光标手型，出现链接悬浮框
    - 当链接为产品内的双链时，样式默认加粗，是否显示为双链图标 ❓
  - 点击悬浮框时编辑链接的交互

- prosemirror的commands设计
  - commands为函数，可以在插件中绑定到快捷键，一般用来暴露给外部

- inline-menu的交互行为，参考notion
  - 出现条件： selection非空
  - 消失条件： selection为空
  - 点击工具条图标：工具条对应按钮变色，编辑器对应内容更新，工具条不消失
  - 点击下拉菜单：下拉菜单消失，工具条不消失，编辑器内容更新

## 0606

- dev-to
  - inline-menu block类型转换： 参考待办列表项实现

- command也许会去掉
  - 各家editor分发修改通过command
  - 我们的block-editor有统一数据源，不需要command

- 如何获取一个js对象的所有key和所有value的union type
  - 思路是 `(typeof x)[keyof typeof x]`

```typescript
const VARIANTS_BY_ID = {
  100: 'diagonal',
  120: 'knight',
  125: 'king',
  200: 'disjointGroups',
  300: 'consecutive',
} as const;

// type Variants = "diagonal" | "knight" | "king" | "disjointGroups" | "consecutive"
type Variants = (typeof VARIANTS_BY_ID)[keyof typeof VARIANTS_BY_ID];

```

- command-menu 代码交流
  - 当对分类菜单有强需求时，如点左边滚动右边，可将数据结构设计为map，而不是数组
  - 向下键需要让元素自动滚到视野之内，原理是 ele.scrollIntoView
    - 为了减少reflow，需要只在Rect位置不足时才执行scrollIntoView
    - 可以每个需要滚到视野内的元素一个id或唯一className，然后得到ele

- discussion-notion-database
- notion的database奇怪的地方蛮多的，但不知道造成这种感觉的主要原因。
- pros：可组合性强
  - 和文档深度结合，使用体验一致
  - 没有使用常见的点击项目弹窗调整表单项而是open as a page，进一步- 加强与文档的不隔离感
- cons：block缩略信息策略较神奇不知道哪些字段会被显示哪些会被隐藏 
  - 缩略信息时展示的信息过少
  - 通知系统比较拉，recent updated term不是很好tracking

- 就拿这个甘特图来看，飞书的界面超级简洁，一眼就可以看见各种状态
  - 后面的排期颜色，notion的太素了，感觉和背景融合在一起
- notion为了支持as page的能力，导致标题部分很乱
- 从使用上，notion切换视图是在上面，并且各种可以自定义各种引用关系，所以新建任务的时候，总会感觉不知道新建在什么位置了
- 而飞书的database更符合直觉，左侧目录区分不同database，可以新建表的形式融合各database
- 功能上来讲，飞书database支持自动化、问卷等各种功能，notion没有
- 从性能优化上讲，长task列表情况下，飞书不会默认隐藏，notion需要自己点开，并且加载的时候会跳
- 文档中嵌入的多维表格是不完整的
  - 但是这就够我们做项目管理用了呀。notion 的各种嵌套能力很强，但是我们用不到呀，甚至用起来会感觉很乱。
- 真的应该看看linear，可以从github直接导入issue和project
- 飞书这种设计相当于创建了一个datasource，文档只是引用了datasource的一部分
  - 然后给这个datasource创建了一个好看的界面，那对用户来说他觉得我需要多用一套东西，心理负担就会高不少了
- it's easy to compare features。飞书和notion都是巨无霸，要是讨论airtable更是巨无霸，因为这些多维表格都是multipurposed。
  - 我觉得notion的心智是显然的。但是飞书也是显然的，飞书和维格都很像airtable，一个从数据出发而不是场景出发的东西，它是更好的excel不是更好的trello或者tower。
  - 两个巨无霸比起来肯定能找出来一堆pro和con，我们应该总从第一性原理出发讲——做什么事情，应该怎么样。
  - 我们现在还不考虑仓储管理啊依赖关系啊关联表啊。我们从最简单的元素开始，就是任务，子任务，时间轴

## 0603

- ubuntu 20.04科学上网
  - sudo apt install shadowsocks-libev -y
  - /usr/bin/ss-local -c /opt/config/shadowsocks.json

- [Linux下刷新DNS缓存（Ubuntu/CentOS）](https://www.cnblogs.com/EasonJim/p/10014517.html)
  - 现在很多Linux发行版都没有内置DNS本地缓存，Linux不像Windows那样可以使用ipconfig /flushdns来刷新，在Linux下无需刷新，因为本身没有缓存；
  - 当然，如果非要缓存刷新，可以安装nscd，然后刷新这个守护进程。
  - apt-get install -y nscd
  - service nscd restart

- sudo systemd-resolve --flush-caches

- 暂时修改 DNS ，修改后立即就可以起作用，但是重启电脑后还需要重新进行修改
  - sudo vim /etc/resolv.conf

- v2ray手动启动命令
  - /usr/bin/v2ray/v2ray -config /etc/v2ray/config.json

## 0602

- se
  - indexeddb
    - local-first client/server architecture
  - notion like  ; block editor

- dev-log
  - [x] inline code 的样式叠加方案，要兼容 code、comment
    - slate的mark可支持加粗、斜体、下划线，使用自定义mark就可以支持comment
  - [x] 主流inline code的样式和交互
    - 常用网站
      - github
      - gitlab
      - bitbucket
      - notion
      - logseq
    - 常用编辑器
      - atlaskit
      - prosemirror
      - ckeditor

- 转换block类型时，block id不能变，要考虑协同的问题
  - 所以不能先删除旧的，再创建新的，因为创建的新block的id变了

- editor-commands的设计
  - 将commands提升到editor的更上层，让commands同时支持文本编辑器、白板的编辑和更新
  - 参考其他编辑器的设计
    - slate-commands，一个接收editor的函数
    - ckeditor-commands，一个class，可以有自己的状态

- left-menu的位置不符合白板的需求
  - 若left-menu定位为fixed，则要修改style为left=0，top=shape-y坐标，menu按钮位置才会勉强符合需求
  - 若left-menu定位为absolute，则要修改style为left=-8, top=0，menu按钮位置才勉强符合需求； 注意此时多行文本是否会自动更新位置
- left-menu位置调整思路
  - 👉🏻️ 白板环境下，计算位置使用新逻辑
  - 👉🏻️ 将left-menu组件渲染逻辑移到render-block组件
  - 同时已解决

- [HTML/Global_attributes/draggable](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/draggable)
  - an enumerated attribute that indicates whether the element can be dragged, either with native browser behavior or the HTML Drag and Drop API.
  - If this attribute is not set, its default value is auto, which means drag behavior is the default browser behavior: only text selections, images, and links can be dragged. 
  - For other elements, the event `ondragstart` must be set for drag and drop to work

- [code和code block设计参考](https://www.notion.so/affineos/code-code-block-7061c2feff1a4962b37cf0d08cba973c)

## 0601

- dev-log
  - [x] 新建page后，光标自动定位在page title 输入区域
  - [x] left-menu的定位问题，要符合白板； 👉 参考晓东实现，fixed -> absolute; 

- 鼠标事件顺序
  - mousedown --> mouseup --> click
  - 鼠标先点击input，再点击button，触发的事件顺序
    - mousedown -->  onblur(input) --> mouseup --> click
  - 注意
    - 在mouseup回调中可以拿到selection取位置，但click回调中selection就变为空了

- 更新text或其他block的流程
  - 理想流程：action  发布_command_  修改blockdb  只通知相关block数据更新  更新blockView
  - 短期变通：action  只通知相关blockView更新  修改blockdb ...

- 工具条设计稿
- inline-menu 悬浮工具条
  - 三级标题、block类型指示按钮、加粗、斜体、删除线、链接、代码块、字体颜色、字体背景色、对齐方式、block类型转换、唤起双链搜索
  - 末尾更多是否一直显示？
- tag-toolbar 挂件工具条
  - 截止日期、人员、任务状态
- group工具条
  - list、kanban、table、add-view

- 如何在多环境的ReactDOM.render()的组件内获取另一个环境内的useParams和导航
  - 对于简单场景，可以直接 location.href ❌ 页面会刷新
  - 对于复杂场景，可以将需要的数据和方法作为参数传到组件
  - 思路尝试，2个环境的react组件都从外部数据源获取和更新数据，而不使用react的state

- [react-router: Support multiple React apps](https://github.com/remix-run/react-router/discussions/8647)
  - 没有解决方案

- [block-menu的动画效果](https://www.figma.com/proto/7pyx5gMz6CN0qSRADmScQ7/AFFINE?node-id=5863%3A2095&scaling=scale-down&page-id=0%3A1&starting-point-node-id=5863%3A2052)

## 0531

- dev-to
  - 斜杠菜单的action，创建sub page
  - 斜杠菜单暂时不支持键盘导航

- 斜杠菜单的设计稿
  - 顶层容器
    - mx: 12
    - mt: 16
  - 左边菜单item
    - 行间距12，my-6
  - 右边菜单item
    - icon行间距 12，文字行间距 16
  - 右边容器
    - ml: 5
    - 右边图标 pl: 22

- `ReactDOM.render(reactElement, container)` 触发react应用执行
  - 需要在普通js环境直接执行

- `ReactDOM.createPortal(child, container)` 触发react元素的render phase
  - 需要在react环境下执行
  - 需要在react组件中 return ReactDOM.createPortal( this.props.children, domNode ); 

- [How to get the caret position in ContentEditable elements with respect to the innerText?](https://stackoverflow.com/questions/68822587)
  - target.addEventListener('keyup', () => {  })
  - get the Selection and Range from the `target` element

- 旧项目双链的弹窗在数量很多时，会出现滚动条

- [Hide scroll bar, but while still being able to scroll](https://stackoverflow.com/questions/16670931)
- 思路1: 让子容器宽度大于父容器，然后子容器右边滚动条被挡住

```css
.container1 {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.container2 {
  box-sizing: border-box;
  /* 让子容器宽度大于父容器，然后子容器右边滚动条被挡住 */
  width: calc(100% + 5px);
  height: 100%;
  overflow-y: scroll;
}
```

- 思路2: 子容器采用绝对定位，right设置负值比父容器更宽而被挡住

```CSS
.container3 {
  box-sizing: border-box;
  position: relative;
  height: 100%;
  width: 100%;
  overflow: hidden;
}

.container4 {
  box-sizing: border-box;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: -5px;
  overflow-y: scroll;
}
```

- [CSS: How to get browser scrollbar width?](https://stackoverflow.com/questions/28360978)
  - Scrollbar widths can vary between browsers and operating systems, and unfortunately CSS does not provide a way to detect those widths: we need to use JavaScript
  - The default scrollbar width can range anywhere from 12px to 17px.

```JS
// This example would usually return: 15px
let scrollbarWidth = (window.innerWidth - document.body.clientWidth) + 'px';
// if your document.body has a max-width: 
const scrollbarWidth = window.innerWidth - document.documentElement.offsetWidth
```

```JS
// Create the div
var scrollDiv = document.createElement("div");
scrollDiv.className = "scrollbar-measure";
document.body.appendChild(scrollDiv);

// Get the scrollbar width
var scrollbarWidth = scrollDiv.offsetWidth - scrollDiv.clientWidth;
console.warn(scrollbarWidth);

// Delete the div
document.body.removeChild(scrollDiv);
```

- [Browser Scrollbar Widths (2018)](https://codepen.io/sambible/post/browser-scrollbar-widths)
  - OSX (Chrome, Safari, Firefox) - 15px
  - Windows XP (IE7, Chrome, Firefox) - 17px
  - Windows 7 (IE10, IE11, Chrome, Firefox) - 17px
  - Windows 8.1 (IE11, Chrome, Firefox) - 17px
  - Windows 10 (IE11, Chrome, Firefox) - 17px
  - Windows 10 (Edge 12/13) - 12px

## 0530

- dev-to
  - inline-toolbar 页面滚动时，工具条没有reposition

    - 暂时可以采用基于滚动条发出的通知来更新弹出层的位置

- 优先实现command-menu、拖拽并排布局的功能
  - 暂停显示按钮初始高亮状态

- 基于eventemitter实现悬浮工具条加粗斜体的问题
  - 实现加粗斜体的action实现容易，但获取选中文本初始高亮状态需要搜集action的结果，比较复杂
  - plugin里面需要添加单独的eventemitter，与editor plugin的hooks设计不符

- 现在SlateText组件对内容的覆盖，是全量覆盖text字段的value
  - 可以在blockdb直接修改text数据，然后blockdb通知SlateText更新

- ？ot默认指令，crdt默认修改

- useSyncExternalStore使用示例，类似redux
  - [React18中的新特性——useSyncExternalStore](https://juejin.cn/post/7056588815170813965)

- 白板要点
  - 里面的编辑器能可用、resize
  - 各种笔
  - 各种形状
  - 白板协作：editor和白板的光标

- 项目开发排期
  - 一个星期一个功能

- figma中点击导航条三角形演示按钮，可以播放设计稿中支持的动画

- dev-to-inline-menu-text-v0518
  - 将page-tree相关的逻辑提取到顶层命名空间，方便复用，如斜杠菜单、全局快捷键

    - 参SelectionManager实现 ❌  在service层封装page-tree数据操作

  - [x] 先实现单例弹窗

    - 获取当前选区及在viewport中的物理位置

  - [x] 实现静态悬浮菜单
  - [x] 实现动态菜单项
  - [x] 自定义菜单项事件
  - [x] 重构Text组件，底层Text不处理业务，只处理编辑器相关逻辑

    - 上层BusinessTextHoc获取数据和操作方法

- 本周3个菜单
  - command menu
  - inline menu: bold/italic
  - block menu

## 0527

- dev-to-inline-toolbar
  - 调整取消高亮的逻辑，部分文本含有mark标记时，应该先加粗，接着点击时才取消加粗
  - 调整工具条位置，不要显示成2行
  - 处理跨选区改变文本样式的情况
  - 编辑器工具条按钮缺少下划线

- SelectionManager是如何实现只通知和更新选中blocks，而不通知未选中blocks
  - emit事件时，传入需要执行方法的blocks ids

- vscode使用本地ts
  - "typescript.tsdk": "node_modules/typescript/lib"
  - 还可以直接升级vscode，里面会带有某个版本的typescript

- debug时发现，subscribe注册的方法总是执行2遍
  - 排查发现是忘了在useEffect里面 return ()=> unsubscribe() 导致

## 0526

- 🔨 在slate-text编辑器外的toolbar组件触发更新slate-text组件
  - 点击toolbar按钮时，在toolbar组件触发 toggle-text-bold事件
  - 在text组件中监听对应事件，然后执行toggleBold方法
  - 若block是文本，则直接toggle高亮button
  - 对于跨段落的选区，在各个text组件分别执行bold方法

- 🔨 如何显示工具条上bold按钮的高亮状态
  - toolbar渲染时，还是选区change后toolbar出现前？，在toolbar组件触发 check-text-bold事件
    - emitter.emitAsync('check-bold',0) .then((results) => { console.log(results);  
  - 在text组件中监听对应事件，然后执行isBold方法，将结果放到resolve参数
  - 👉 等待所有isBold执行完毕
    - 若全为true，则触发 toggle-toolbar-bold事件
    - 若有一个为false，则do nothing

- 复制粘贴的一般处理方式
  - 软件内部json，软件外部富文本？

- 旧代码未实现加粗斜体按钮显示初始高亮状态，不必执着于找参考实现

- eventemitter流行度
  - https://www.npmtrends.com/eventemitter2-vs-eventemitter3-vs-eventemitter4-vs-events
- [React: Event Emitter](https://lolahef.medium.com/react-event-emitter-9a3bb0c719)
- [Event Emitter instead of lifting state up in React](https://medium.com/@krzakmarek88/eventemitter-instead-of-lifting-state-up-f5f105054a5)

- [EventEmitter implementation that allows you to get the listeners' results?](https://stackoverflow.com/questions/19214723)
  - I don't think it should be. Event Emitter should not return callback results. Eventemitters are an alternative to asynchronous function calls, if you use them correctly. You should not try to combine them and complicate stuff.
  - https://github.com/mercmobily/EventEmitterCollector
  - https://github.com/EventEmitter2/EventEmitter2

- [Node.js: how can I return a value from an event listener?](https://stackoverflow.com/questions/42802931)
  - 思路是修改 emitter.emit("sayHello", data); 的data参数
  - 但不清楚具体什么时候data才会变化
  - 在其他地方很难拿到data数据

- [NodeJS EventEmitter: how to wait for all events to finish?](https://stackoverflow.com/questions/71684125)
  - 思路是 extends EventEmitter

## 0525

- dev-to
  - toolbar bold/italic

    - 触发悬浮工具条渲染和更新时，工具条按钮如何显示正确的初始状态，特别是高亮加粗斜体
    - 工具条按钮触发的编辑器操作，如何传入参数

  - toolbar要在鼠标停止拖动后才显示，正在拖动时不应该显示，notion是此行为
  - drag to row layout

- 需求
  - 在其他react组件拿到编辑器数据和触发编辑器修改方法
    - isFormatActive
    - toggleFormat

- 🤔️ 如何在其他react组件触发Text组件更新
  - 👉🏻️ 思路1，命令式手动触发
    - 将slate-text-editor实例放到全局，getNodeById可拿到编辑器实例，就可以触发编辑器方法
  - 👉🏻️ 思路2，pub-sub
    - 在工具条组件，getNodeById可拿到业务block实例，在工具条点击加粗，emit加粗事件，然后通过类似u

- selection选择时要考虑长表格的问题
  - 删除部分行，还是删除整个表格
  - database表格视图经常不显示所有行

- toolbar组件参考
  - 优先参考 atlaskit 编辑器工具条的实现
  - https://github.com/hifromkevin/Reusable-Toolbar
    - Reusable components that can be utilized to create a custom toolbar.
  - https://github.com/CBIConsulting/ProperToolbar
  - https://github.com/lucascassiano/react-minimalist-toolbar

## 0524

- dev-to
  - inline-menu 工具条ui、弹窗定位、selectionchange触发悬浮工具条

- 🐛️ 对于在slate编辑器中双击选中文本时
  - chrome-linux的selectionchange事件，选区类型为range
  - 但 edge-win11的change事件选区类型为caret，所以需要对特殊的浏览器特殊处理如setTimeout，其他的浏览器可以普通处理

- 对于普通页面
  - 浏览器点击任意位置时，selection.type === Caret 
  - 浏览器双击文本选中时，selection.type === Range

- 💡 hack: editor-selection
  - win浏览器双击选中文本时，先触发selection-caret，第2次点击后才会触发 selection-range
  - mac浏览器无此问题
  - 👉🏻️ 黑科技解决思路： 等待一段时间如300ms，可以在setTimeout里面拿到range类型的selection

- Uncaught (in promise) TypeError: this.hide_inline_menu is not a function
  - es6的class实例方法作为callback传递时，要在构造函数中bind

- 解决eslint处理自动生成文件的异常
  - 手动进文件添加 eslint-disable
  - 在eslint-plugin仓库里面手动搜索issues，很可能是远古bug
    - 使用第三方方案的缺点，早晚都会碰到未暴露的方法或不支持的配置项
  - [unable to specify regexp inside json-config](https://github.com/dolsem/eslint-plugin-filename-rules/issues/8)
  - "ignorePath": "libs/components/ui/.eslintignore"

- figma新图标引入
  - 新 file/7pyx5gMz6CN0qSRADmScQ7/AFFINE?node-id=4703%3A635
  - 旧 file/7pyx5gMz6CN0qSRADmScQ7/AFFINE?node-id=665%3A1735

- 悬浮工具条样式
  - height - 50
  - 按钮 - 20x20
  - 按钮 gap - 12

## 0523

- 工具条的视图类型
  - 图标
  - 图标 + 下拉三角图标
  - 分隔竖线

## 0520

- dev-to
  - popover

    - block-left-menu、斜杠菜单、文本悬浮工具条、mention面板、group/ungroup悬浮菜单

  - base states
  - 图标资源

- 讨论block-popover实现方式的问题
  - 现在block-popover触发条件是onMouseEnter，交互友好吗？ 
    - 之后会修改触发条件
  - 是否用这种实现方式，每个block都有自己的弹窗，每个block都有自己的悬浮工具条吗？
    - plugin机制是否要废弃，现在没人用，我感觉用react的方式我更顺手
    - block的挂件工具条使用很频繁，且弹窗内容会转换为文内显示，支持2种形态，所以放在block是合理的
  - 弹窗组件的内容是否要根据block类型动态变化
    - 如对text-block有加粗斜体没有下载按钮，对list-block有切换类型
    - 暂时不考虑太复杂的

- inline悬浮工具条存在的问题
  - 当菜单项过长时，未实现在工具条末尾添加更多图标来隐藏菜单项
  - 工具条上每个图标都可以添加悬浮tooltip添加操作说明
  - 工具条组件要支持下拉分组
  - selection变化时更新inlineMenu的位置

- 悬浮工具条
  - 第1个按钮，只修改标题级别
  - 第2个按钮，只修改list类型，编号、无需、待办
  - turn-into按钮，修改block类型
    - 场景1，默认会拆分block
    - 场景2，是具体目标类型而定，如变为图片标题

- TypeScript 3.9 给出了一个替代 // @ts-ignore 注释的方案：// @ts-expect-error。
  - 从字面上我们不难理解为什么后者是更优的选择：
  - 显示声明了会报错的原因，而不只是一味的规避检查；
  - 向前兼容，未来如果 TypeScript 支持某语法导致不再报错，TypeScript 会主动提示删除注释，这会让代码变得更加简洁；

## 0519

- page初始渲染时，title是如何渲染的
  - PageView渲染的不是title，而是普通Text组件，但传入了标题样式名

- KeyboardEvent.metaKey
  - On Macintosh keyboards, this is the ⌘ Command key
  - 对windows，若按过windows键，则metaKey为true

- 弹层应该实现为plugin，因为不处理编辑器核心的输入、渲染逻辑

- block-left-menu、斜杠菜单、文本悬浮工具条、mention面板、group/ungroup悬浮菜单，可以有一个统一的唤起隐藏逻辑，根据所在block类型和数据动态渲染菜单项。

- Editor层主要关注于编辑器核心能力的提供，例如编辑、选区、各种block的管理和控制，可以认为Editor是一个编辑器内核的sdk，类似于操作系统shell层；
  - plugin是对Editor的能力增强，例如弹出菜单、下拉菜单、筛选过滤查找、导入导出等交互，这些交互形式不是编辑器内核关注的内容；
  - plugin和Editor的交互，通过Editor层对外接口进行沟通，通过Editor的各种hook完成对plugin的回调

- 可能的风险，现在大家都还没有使用plugin，我可能会根据需求增加plugin的api和方法的参数

- undo/redo不仅回滚输入内容，还要回滚光标

## 0518

- 浮动工具条 FloatingToolbarPlugin
  - 在plugin构造函数中注册ON_ENTER显示隐藏浮动工具条的方法
  - 触发条件
    - 在自定义block的useEffect中，onSelectionChange/输入变化时
  - 在TextBlock或CodeBlock中触发 editor.getHooks().onEnter/onKeydown/onBeforeInput

- dev-to-topic-selection
  - 向selectionManager中setSelection
  - 从selectionManager中getSelection
  - 下拉小弹窗、悬浮工具条，都需要从selection中 getBoundingClientRect

    - 获取一个range的text

- dev-to-topic-inline-menus
  - 👉 如何注册菜单项，斜杠commandMenuItems、inlineMenuItems

    - ✔ 不需要在全局注册菜单项，每个block自己传入自己支持的菜单项及事件
    - ckeditor采用的是初始化编辑器器传入toolbarConfig属性
    - slate示例给的是创建一个自定义Menu组件

  - 👉 如何实现动态菜单项

    - ✔ 根据block type和block自身传入的配置

  - 👉 与设计沟通文本悬浮工具条设计图
  - 👉 悬浮工具条及下拉框是放在全局单例，还是和每个Text组件写在一起

    - ✔ 放在全局，方便在不同block间复用

  - 💡 commandMenu和inlineMenu的实现放在哪里更好

    - 可以放在封装的TextView组件
      - 优点是方便直接获取SlateEditor的selection数据和其他属性方法
      - 容易获取editor command
      - 触发条件 输入斜杠或选中
    - 可以放在BlockEditor的plugin
      - 优点是非TextView组件也能唤起斜杠菜单
      - 缺点是针对工具条的不同操作，不同的按钮事件需要传入额外的不同的编辑器相关的参数
      - 触发条件是 showCommandMenu

- 关于编辑器中选中文字或其他元素才会出现的悬浮工具条的命名
  - slate: hovering-toolbar 🤔 并不是hover就会出现的
  - ckeditor/slate-plate: balloon-toolbar
  - prosemirror: tooltip
  - medium-editor: inline/block-toolbar

- 😋️ pm: innos
  - innos的编辑器可以将block拖入拖出card/group
  - 可以将block拖到行内并列，并且保留样式背景色
  - innos的设计强调卡片自适应变宽，占满一行
  - innos的缺点，容器元素过多，心智成本高

- block可以嵌套block
  - group不要嵌套group

- 拖动时应该默认带上子集一起拖动，因为子集数量可能很多超出屏幕
  - 另一种设计是，按住其他键如shift可以只拖动父级单行
  - shift可能白板也能用

- 回退删除键的逻辑要讨论
  - a. 直接跳过分隔线，直接在上一个block末尾删除文本
  - b. 先focus分隔线，再删除分隔线

## 0517

- slate
  - mention输完@后，如何弹出下拉框
    - 整体架构为 `<Slate><Editable></Editable><Portal></Portal></Slate>`，注意只有在@x用户输入x非空时才渲染下拉框
    - 下拉框出现的条件@后用户输入文字非空，且搜索结果非空
    - 下拉框portal定位样式 position: 'absolute', 动态修改style.left/top
  - mention下拉列表中选中文字后，如何插入编辑器
    - 在Editable组件的onKeyDown事件中，检测到enter按键时插入文字到编辑器
    - Transforms.insertNodes(editor, mentionNode);
    - 上下键可以在下拉列表切换当前选择高亮项

- slate的selection和block-editor的selection有什么关系
  - 如何存取slate编辑器的selection

- 将block级的onMouseMove事件注册到root根节点的onMouseMove，然后在block级事件内判断位置只在block内才执行逻辑

- 主要改动是createView返回react组件 -> 直接使用View组件 。
  - 原来RenderBlock中是直接调用createView方法，这样会导致 react 的 hook 会报错，因为react会将这个函数理解为普通函数调用，hook会合并到RenderBlock的hook stack中。如果组件重渲染会报错（warning级别，不会影响build，因为createView调用位置保持一致，且在最后面)
  - 写法明明就是 FunctionComponent，但是多加了一层，完全没必要。所以直接改为FC了

## 0516

- dev-to
  - command-menu
  - inline-menu
  - sub-page实现设计方案文档

- 紧密联系功能
  - backlinks
  - slash command menu
  - link page

- 公司集体断网的原因
  - maximum number of concurrent DNS queries reached.(max: 150)

- 备份带斜杠菜单的编辑器-bak20220506
  - commit-id b9d74bacb33198d073afb2b2331d1210ce476dc7
  - [旧架构的使用示例](https://github.com/toeverything/Ligo-Virgo/blob/b9d74bacb33198d073afb2b2331d1210ce476dc7/libs/components/heading/src/block.tsx)

### oneOnOne-terry-表格研发体验

- google docs dom转canvas的原因
  - 最开始是基于dom实现滚动
  - 每次滚动一行高度，不够平滑
  - 虚拟滚动append缓冲行执行会卡顿
  - 合并单元格基于colspan

- 友商都在用spreadjs
  - 石墨文档 handsontable -> spreadjs
  - 腾讯文档 spreadjs

- spreadjs基于canvas实现，且逻辑分层非常好
  - spreadjs的模型是比较通用的，**数据模型层特别重要**
  - spreadjs下性能并不是很优秀
  - spreadjs不支持协同
- 只保留spreadjs的渲染视图层，模型换成google-docs的数据层
  - 行数量、每行的列、单元格输入内容、单元格文本格式/条件格式、单元格样式、单元格评论
  - row[], cell[]
  - 合并单元格保存在全局
- 全局属性
  - 行冻结、列冻结
  - 全局边框色

- canvas的性能一定能够更好吗
  - canvas像素级绘制，dom依赖浏览器渲染
  - canvas也能实现虚拟滚动，还能实现双缓存画布
    - 利用双画布复用canvas内存对象
    - dom的虚拟渲染未考虑，文字斜体；canvas直接复用2d的位置信息
  - canvas的性能瓶颈，一行的高度取决于所有行中单元格所有文本的高度，word-segment分词算法，优化了排版算法
  - canvas的兼容性在移动端更好

- canvas上线后还会出现移动端黑屏的问题
  - 部分移动端由于gpu的问题，导致渲染
  - 页面canvas特别多，会出现粉屏

- 要优化性能
  - 一都会增加链路，使用简化的指令，传递指令
  - 更现代的基础设置，不存对象数组，直接存数组，如用protobuff

- 实现表格
  - 稳健的架构
    - 渲染可支持svg/canvas
    - 离线需要优秀的模型设计 数据库模型、编辑器模型、视图层模型
    - 协作需要指令，用户操作 -> taco -> 取缓存 -> 缓存中没有就刷新

- crdt更新是整体block更新
  - 性能不会比ot更好

- 在效率和功能间取得平衡

## 0513

- dev-to
  - 确定斜杠命令菜单的实现思路
  - 确定获取斜杠锚点dom元素位置的思路
  - 初步实现在焦点行的下一行唤起斜杠命令菜单

- 编辑器基础
  - 光标显示、是否可focus
  - 选区拖拽：当block高度大于屏幕高度时，选区的实现
  - 快捷键
  - 滚动条

- forEach 循环里面不能await，改普通for循环

## 0512

- dev-to
  - [x] authing登录已经接入海外版，目前支持google登录和用户自己注册邮箱登录，不支持注册手机号登录

- 编辑器的几种menu
  - add-menu，如创建添加各种block
  - block-menu，如复制、粘贴、上移、下移
  - slash-command-menu，弹窗内容同add-menu

- 左侧菜单的触发条件 onMouseMove
  - 斜杠菜单的触发条件 用户手动刚刚手动输入/

## 0511

- 创建subpage的两种方式
  - 斜杠菜单 /
  - 双链热键 [[
  - 实现可以参考 menu/hover-toolbar

- [python 字符串转列表出现\ufeff的解决方法](https://www.cnblogs.com/mjiang2017/p/8431977.html)
  - 在Windows下用文本编辑器创建的文本文件，如果选择以UTF-8等Unicode格式保存，会在文件头（第一个字符）加入一个BOM标识。
  - BOM = Byte Order Mark
  - BOM是Unicode规范中推荐的标记字节顺序的方法。比如说对于UTF-16，如果接收者收到的BOM是FEFF，表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little-Endian的。
  - UTF-8不需要BOM来表明字节顺序，但可以用BOM来表明“我是UTF-8编码”。BOM的UTF-8编码是EF BB BF（用UltraEdit打开文本、切换到16进制可以看到）。所以如果接收者收到以EF BB BF开头的字节流，就知道这是UTF-8编码了。
- [Python 读取文件首行多了"\ufeff"字符串](https://blog.csdn.net/chenmozhe22/article/details/89472790)

- 👉🏻️ authing海外迁移
  - 我对接authing的技术支持
  - https://core.authing.cn/api/v2/applications/61961a7b8b90af37e7c422e0/public-config

- authing海外版的2个问题
  - google登录暂时未生效，authing控制后配置后需要等待一段时间，生效前需要每个人重新注册一个帐号
  - 切换到海外版后，后端的/user和/spaces接口请求出现异常，需要后端修改一下请求authing用户的url

## 0510

- dev-log
  - [x] 测试接入authing海外版，需要等authing的人对接修改配置

- services之间的相互调用，考虑用依赖注入实现

- `/usr/bin/env: ‘sh\r’`: No such file or directory
  - 解决方法是，在vscode手动将异常文件编码改为LF

## 0509

- 迁移到包含service层的架构后，顶部导航条获取page标题的时机难以确定
  - 原因1: 导航条NavigationBar是未被route_private包裹的，渲染时机非常早
  - 原因2: 顶导航条通过router的useParams只能获取到workspace_id，不能获取到page_id
  - 就算用魔法强制在page初始化后注册title更新的事件监听器，navbar更新title还是失败

## 0506

- 为方便调试编辑器开发，应该提供一个单独的编辑器页面，不包含获取用户数据等逻辑

## 0505

- 登录流程设计
  - 登录路由守备要支持offline

- page-tree的状态同步
  - 未调完的分支不要commit到主分支，会导致协作者debug很混乱

- 👉🏻️ workspace初始化过程讨论
  - 离线功能支持的程度
    - 是否要离线可登录
    - 是否支持离线切换page、跳转page
  - 初始化workspace实现的细节
  - 创建workspace的ui和交互
  - 删除workspace的ui和交互
- 👉🏻️ 其他task
  - page-tree创建page后ui和state要视觉上立即更新

### oneOnOne-terry-文档基建closure

- google closure 运行时
  - 扩展了js、dom
  - ui库

- google closure compiler 编译器
  - 提高js压缩率
  - 编辑css为atomic css
  - 从compiler迁移到webpack，体积增大了，但便于协作开发
  - closure-templates 支持模板，类似handlebar/pug

- goog.disposable.prototype.disposeInternal 在基类实现dispose方法

- dev-to-login-issues
  - 🤔 workspaceName为用户名带来的问题

      - 邮箱名冲突的问题，如a@qq.com/a@163.com
          - 暂时解决命名冲突的问题，用户名_邮箱的方式，a_qq
      - useBlockDatabase传入的workspaceName，取回来的id是一致的吗

  - 🤔 上次的workspaceId/workspaceName存放在哪里，怎么获取？

      - 计划存放在localStorage
      - 先向服务端请求最近workspace列表，若为空，则使用localStorage中保存的
      - 如果存放在database中，则需要修改现在的初始化逻辑，在useInitEditor之前先初始化database

  - 🤔 有没有必要在每次登录或刷新页面时，从服务器请求用户的所有workspaceId列表？

      - 我认为有必要，在新浏览器登录时可恢复上次workspace，而不是在本地新建workspace
      - 若离线，则自动创建新的workspace，id为 用户名_创建日期

  - 🤔 若用户上午在设备A登录workspaceA，下午在设备B登录workspaceB(先自动登录A然后手动切换到workspaceB)，晚上离线/在线时，在设备A打开自动进入哪个workspace？

      - ? 若离线， workspaceId默认先用本地的，然后比较远程同步得到的id和访问时间
