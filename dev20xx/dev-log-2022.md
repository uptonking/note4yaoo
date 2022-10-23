---
title: dev-log-2022
tags: [dev-log, dev-xp, stage-2022]
created: 2022-05-24T17:56:50.063Z
modified: 2022-10-21T21:06:47.860Z
---

# dev-log-2022

# dev-xp

# dev-07-job-leave-edit20211025-20220720

## more-tasks

- dev-to-draft
  - inline-toolbar
    - [x] 添加link输入框或小挂件输入框中一输入文字就抛出异常
    - [ ] 在工具条点击下拉菜单按钮时，视觉上始终显示蓝色选区
    - [x] 菜单项包括inline-menu要显示鼠标提示，内容包括快捷键
    - [x] 在通过键盘创建选区时未显示工具条
    - [x] 在codeblock和挂件也会触发，不合预期
    - 在inline-menu上或在下拉菜单上移动鼠标时应禁止冒泡，不触发left-menu的mousemove事件，也不应更新left-menu位置
  - comment
    - [ ] 评论在slate的mark无法删除的问题，只能设为false
    - [ ] comment和link样式叠加的edge-cases
    - [x] active comment的交互效果：高亮 + 自动调出评论侧边栏
    - [x] 评论部分区域重叠时显示加深颜色
  - page
    - [ ] 优化page-tree新建page的逻辑
    - [x] 创建新页面体验优化，光标聚焦到标题，下面显示类似notion的开始创作提示
  - slate
    - previous_selection永不为空的设计是否合理
  - more-editor-issues
    - [ ] 用户id和用户在哪里查询和缓存

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

- [新产品设计稿figma](https://www.figma.com/file/7pyx5gMz6CN0qSRADmScQ7/AFFINE?node-id=0%3A1)

## 0719

- dev-to
  - 导航条响应式隐藏元素

- css设置了margin，就不要设置 width 为 100%
  - border-box的width不包括margin，width: 100% + margin 总宽度会超出父容器

## 0718

- dev-to
  - [x] slate左中右对齐未持久化

- 删除逻辑在退格按键和各种菜单按钮都存在，逻辑经常重复

- slate编辑器文本样式能持久化但对齐不能持久化的原因
  - 文本样式属性加在TextNode，children变化后会触发持久化逻辑
  - 对齐属性加在文本的父节点之上，改变对齐方式后，自身变化但children不会变化，所以未触发持久化逻辑

## 0715

- dev-xp 👀
  - 注意传入事件处理函数的写法 onClick={handleClick} , 默认event对象会做为第一个实参传入handleClick方法 
  - 更推荐这样写 onClick={()=> handleClick(myArgs) }

## 0714

- 设计稿还原问题
  - 导航栏高度是多少？  80 + 下边距96
  - page的上面是否要预留一个图标的高度？ 
    - 这个高度以后可能用来单独放一个page图标或emoji
    - 对于大的空白间距，不要无脑 margin

## 0713

- nx build时一直抛出 property 'cursor' does not exist on type 'cssproperties' 的异常
  - 异常信息提示的位置行数是错误的，不要过于依赖
  - 解决方法是，手动找到该文件中使用 cursor 的位置，将cursor值类型由 `CSSProperties['cursor']` 改为联合类型 `'grab' | 'pointer'`

## 0712

- 确定布局包的结构
  - layout-header
  - layout-left
  - layout-right
  - 讨论后决定，先将布局相关的放在一个包，等代码变多或变复杂后再拆成子包，不要过早优化

## 0711

- 评论pr合并前
  - inline-menu入口使用featureFlag
  - 块级评论去掉入口
  - 添加评论插件去掉

- 评论功能难点
  - 创建块级评论
  - 高亮的评论数据保存在slate中和comment-block中，什么场景应该删除高亮mark？
    - 复制页面？
    - 分享页面？
  - 白板中的评论选中状态与高亮
    - 将评论高亮功能放在slate-text-leaf层更容易实现支持多编辑器实例
  - 评论卡片用户名和头像不符合设计
  - 评论回复框复的ui用添加评论的回复框
  - 评论卡片与编辑器内位置水平对齐

- ❓ 如何在侧边栏解决评论时删除对应编辑器的高亮文本
  - 先找blockId，再找带有高亮mark的textNode
  - 第一步拿到slate-text的blockId没有直接方法，思路1-遍历page-block所有block来找，思路2-修改service的createComment方法，把评论关联的slate-text blockId 也存进去
  - 👀 要考虑跨区评论的场景

- 上周总结
  - 在添加评论后，高亮编辑器内文本，且支持评论部分重叠
  - 选中编辑器内已评论的文本，动画突出当前被评论卡片 
  - 评论设计稿更新后，更新ui
  - 修复了在tag-app或其他外部输入框输入文字slate抛出异常的问题
  - 对顶部导航条进行小改动，实现了简单侧边栏显示评论

- 每个block是async的问题
  - remove + append  ?==  move ❓
  - 在低性能电脑上，先删除后就刷新了，会导致闪烁

- 先基础编辑，再卡片、group

## 0708

- 文本折叠效果参考
  - coda
  - things
  - height

## 0707

- 在白板里面，如何拿到当前编辑器的selection
  - 理想方案是先直接改数据，再通过数据更新通知视图更新
  - 临时方案是先拿到editor对象，再通过editor对象拿到slate-selection

- 当光标处于编辑器内高亮评论文本时，高亮文本的颜色会加深，这个状态最好不要保存到mark，因为这是临时状态，不需要持久化
  - 持久化后也可能是feature
  - ❓ 颜色加深条件使用点击事件最直接，使用collapse的selection也能做

## 0706

- 更新依赖后，webpack热加载会一直recompiling
  - 可能是style9生成的css导致的

- slate-bugs-通过增加条件减少触发搜索的逻辑

```JS
Uncaught( in promise) TypeError: Cannot destructure property 'selectionEnd' of 'this.getSelectionStartAndEnd(...)'
as it is undefined
```

## 0705

- xp-异常处理
  - 在hook层，一般暴露crud方法，不处理异常而是直接抛出error
  - 在视图组件层，处理输入异常，提示给用户的反馈

- 方案参考
  - 飞书的评论引文最多显示1行
  - 飞书的评论引文最多显示3行

- ❓ editor是否需要自己的状态，还是以indexeddb作为唯一数据源？

- 编辑器重构设计讨论

- editor-core
  - selection
  - cursor
  - keyboard
  - scroll
  - drag-drop
  - widget
    - 松耦合的插件plugin和强耦合的widget

- blockdb管理数据model
  - viewController并不管理数据

- 本地或远程数据源通过adapter

- jwt封装了对block操作的抽象
  - block实例
  - 检索
  - block响应式更新
  - undo/redo
  - snapshots

- 异步接口转同步可以在editor-core内实现

- command层只约定参数类型
  - 设计得越来越像redux的action
  - command只负责传参

```shell
# 编辑器与数据源交互的逻辑流程
👉 blockdb/jwt 非

👉 command-manager / action / 原子操作 

^(command做为通信协议)  v(onUpdate)

👉 editor-core

```

- 去掉AsyncBlock的原因
  - 异步写起来麻烦
  - 除了indexeddb的缓存，前端又缓存了一次数据

## 0704

- 👉 方案参考：编辑器选中评论部分时，加深高亮评论颜色和其他交互
  - notion会高亮侧边对应的评论卡片的背景色
  - 飞书会高亮侧边对应的评论卡片的顶部

- 协同功能需要权限系统作为前提
  - 协同、分享、评论常一起考虑

## 0701

- 评论功能排期
  - resolve和恢复
  - 评论操作菜单，如编辑、删除

- 👉 方案参考：在已评论文字中选择部分文字进行评论
  - 飞书默认显示第一条；不会高亮内部文字评论
  - notion默认按时间排序，默认显示第一条，然后会高亮内部部分文字和；会高亮内部和外部文字的评论

- slate-toolbar： We use onMouseDown and not onClick which would have made the editor lose focus and selection to become null

- 维基共享的图一般无版权问题
  - splash图也ok

- 要讨论在一些框架层面的事情，我这几天做评论的时候，看到的一些问题，你们可以参考看一下，不一定正确
  - 感觉现在的Service 层更像是实体接入层，没有service逻辑在
  - Block 创建者有对应字段，但没有存储信息；Service 层是否应该存储用户状态；即便有状态，是否需要统一管理
  - 同步异步数据的隔离
  - getBlockDatabase 多次读取时，会创建多次（这个我看已经修改过了）；缓存内容，没有考虑账号切换
  - 数据驱动；editor是否只注册一个观察者就可以；感觉没有必要像现在这样，在editor管理更新，是否可以移动到service层
  - Workspace 上挂着pages、二进制文件，这样的话，Observe 更新通知是否过于简陋，不知道更新了哪些内容，现在更新频率过高
# dev-06

## 0630

- 评论实现方案比较
  - notion评论默认黄色背景通过style属性添加
    - hover或聚焦时深黄色通过添加带有 `!important`的classname实现
  - 飞书评论默认黄色下划线通过className添加
    - hover时无样式变化
    - 聚焦时深黄色通过添加带有 `!important`的classname实现

- 请问一下大家，history一般是对编辑器里的内容的记录，但是对某一条句子添加了一条评论，然后再ctrl+z之后，评论也会相应删除，这种是怎么做到的呢？**评论也设计在了编辑器的数据模型之内吗**？
  - 评论跟样式一样，是一个属性
  - setNodes 和 unSetNodes 就添加和撤销了
  - 只是渲染的时候，评论的内容是单独保存的
  - node 属性只存 id 属性，类似于 comment_xxx: true, comment_yyy: true 这种

## 0629

- 同步一下Group Filter/Sorter的节奏，目前有两种方式：
  - 第一种：内存过滤（针对当前已经展示的数据进行过滤，不和db交互）；
  - 第二种：db搜索，需要数据库支持；
  - 考虑到稳定性及当前的节奏（Filter/Sorter以灰度存在，告诉用户有这个能力，并且会持续雕琢），当前采用第一种方式

```shell
# 我的分支是 feat1
git co field
git fetch origin field:field # 同步 field 到远端最新
go co feat1
git rebase field # 将当前分支基于 field 进行 rebase

# 👉 不用切换分支
git fetch origin field:field
git rebase field

```

- rebase改为merge的案例
  - 原代码删除后，找不到对应的人和commit记录了
  - 线上事故后，找不到对应的负责人了
- 自己的分支b1想用没合并的pr分支b2怎么办，备注主分支是main
  - 先rebase到b2，然后rebase到main时会自动跳过b2的commit

- rebase一般用来处理小改动，对于大改动，rebase后要处理的冲突特别多
  - git rebase --abort

- 排查webpack一直热更新的问题花了很多时间，搜索也没人碰到过
  - [webpack-dev-server] App updated. Recompiling...
  - 其他同事没碰到的原因是只pull了最新代码，但没有执行 pnpm i
  - 解决方式是将代码回退，找到没问题的版本，原因大致是monorepo其他地方修改了配置
    - 其他同事也是这么解决的

## 0628

- 现在 getComments 的返回值是一系列type-comments的block，quote放在单独的block，评论内容content也放在单独block，我在前端需要做很多异步查询才能组装出需要的数据结构Comment[]，这部分逻辑放在前端做好，还是service层做好？
  - 放在service层的好处是异步获取的数据量少，方便实现虚拟滚动动态请求，暂时没什么问题，你这边不用操作

- 评论输入框拿到的数据结构是 `{ value: Array<{ text: string; bold?: boolean }> }` ，而不是text，方便切换到

- event的dataTransfer是保护模式？可能拿不到

- html input可以设置min-width属性
  - There is size="20" set on `<input>` type text, search, tel, url, email, and password ... by default, which is approximately of 100px width, although it can vary in a different browser and operating system.

## 0627

- dev-to
  - styled中属性值如何选择子元素
  - [x] 评论数据如何自动更新的 ?
    - 类似PageTree的observe
  - [x] 评论列表不能回复中间某一个人
    - 点击中间部分评论内容时，直接聚焦到回复框，并且自动在回复框最前面添加@对应用户

- 评论卡片宽度 w-322 + ml-22 + mr-26 = 370
  - Hug是什么单位，在figma里面代表依据内容确定宽度

## 0624

- 普通业务组件如何通过点击编辑器中元素唤起？
  - 在普通业务组件内注册 onSelectionChange
  - 普通业务组件先通过全局state拿到对应editor对象

- 飞书云文档评论，一共有 3 种类型，分别是：全文评论、正文内容划词评论和表情回复评论
  - 在文档级别可以添加点赞表情

- 解决评论：点击评论右上角的 对勾 按钮，该评论将被解决并隐藏 。
- ​删除评论： 只有评论者可删除、编辑自己的评论，协作者可以把评论标为解决（隐藏）。
- 查看历史评论
  - 已解决的评论可重新打开，已删除的评论不可恢复
  - 将鼠标悬浮在页面右上角的 ... 按钮上，点击 历史评论，你可以在列表中查看原评论位置、评论人、评论内容和评论被归档的原因：“原文被删除”或“某人已解决此评论”。

- 评论操作
  - 编辑
  - 删除
  - 翻译
  - 复制评论处链接，类似锚点
  - 导航：上一个、下一个
  - 回复：文字、富文本、表情

- 私有属性和方法
  - 目标：在视觉上区分，在编译执行安全性层次上区分，然后放心删除
  - vscode的私有变量和方法是 _前下划线
    - https://github.com/microsoft/vscode/blob/main/src/vs/editor/common/model/textModelSearch.ts
  - 后下划线_ 也有人用
  - rust社区 流行_中下划线
  - 安全性应该通过单元测试、集成测试保证

## 0623

- [Git branch command behaves like 'less'](https://stackoverflow.com/questions/48341920)
  - git config --global pager.branch false

## 0622

- ux-悬浮工具条
  - 通过键盘选中连续文字支持触发悬浮工具条

## 0621

- 评论实现讨论
  - google-docs会在内存保存评论位置

- 评论prd-impl-talking
  - 评论暂时只不支持对齐
    - 评论位置暂时只根据block，不细分到文本所在行
  - 评论暂时只能@自己
  - 锚点暂不考虑

- dev-style-talking
  - 样式方案用css-in-js如styled更容易长期维护
    - 可以放心删除未使用的纯样式组件
    - 方便跳转样式定义
  - 考虑vanilla-extract

## 0620

- 块编辑器开始支持跨区选择，后面禁用此功能改为只支持单行选择的原因
  - 跨区选择时，会将各子块的contenteditable改为false，此时选中的内容无法响应键盘事件

## 0619

- inline-toolbar
  - 点击一级按钮如加粗斜体时，只触发click事件，不会触发编辑器onBlur
  - 点击按钮打开dropdown时，先触发工具条click事件，再触发slate-text组件的onBlur事件

## 0617

- notion的工具条添加link会出现弹窗
  - 👀 同时link对应的文字选区会变大一点，蓝色选区视觉上不会消失
  - link弹窗出现时的底层文字的蓝色选区并不是通过leaf实现
    - 而是通过 renderLinkFakeSelection 添加的全局纯背景div
    - div的长宽和位置通过window.getSelection().getRangeAt(0).getClientRects()确定

- ❓ 保存上次选区的逻辑放在应用层react组件内？还是编辑器框架层？
  - 放在应用层方便测试，但每个失焦事件都需要处理
  - 放在编辑器框架层如 onBlur, onFocus，可以自动保存选区

- 光标丢失问题的排查定位
  - 二分法注释plugin，定位到导致问题的plugin，然后单步调试可能的问题代码块
  - 并不是slate内部debounce导致，debounce会触发事件，throttle才可能导致丢失中间事件

## 0616

- 文本中添加前景色背景色的实现方式
  - 通过给span添加style对象实现
    - ckeditor
    - slate-plate
    - atlaskit
      - style添加的是css var颜色定义

- slate设置文本对齐的方式示例在官方示例rich-text，自己却在其他地方找了很久，浪费时间

- [Apply block level formatting (like text alignment) on node](https://github.com/ianstormtaylor/slate/issues/3569)

- 传说中的block editor鼻祖quip，notion抄的对象

## 0615

- slate如何获取selection所在block
  - [how to get the current Localtion in the editor, where the user is placing it's cursor at](https://github.com/ianstormtaylor/slate/issues/3485)
  - editor.selection

- 段落左中右对齐的实现方式
  - 通过给p元素添加style对象实现
    - slate-plate
    - ckeditor 
    - TinyMCE
  - 通过给p元素添加className实现
    - atlaskit
    - quill

- slate设置对齐方式的参考
  - https://news.ycombinator.com/item?id=14127632

- [How to change property of SlateJS node element onChange?](https://stackoverflow.com/questions/71152875)
  - Transforms.setNodes( editor, { id: '123', }, { at: [0] }, )

## 0614

- [Get union type from indexed object values](https://stackoverflow.com/questions/50044023)

```TypeScript
const X = {
 a: 'A',
 b: 'B'
 // mark properties as readonly, otherwise string type inferred 
} as const

type XValues = typeof X[keyof typeof X]
// "A" | "B

```

## 0613

- 插件需求
  - 插件间通信，功能待实现，但会增加复杂度 
  - 添加挂件的插件，会影响block的内容和样式；
    - 外部插件修改了block，设计不合理，插件影响范围太大；
    - 可考虑放到renderBlock组件内，方便读写数据，而不用plugin方式实现
  - 插件创建的元素如left-menu六个点，有时显示，有时隐藏
    - 可能是插件的实现机制存在瑕疵，插件卸载再重载时，react组件的事件未绑定，热加载也可能有影响

- 👉 结论是，暂时不考虑插件间通信，而是将添加link的弹窗做到inline-toolbar组件内
  - notion打断点的方法，找到目标元素的位置，如输入框input的`Paste link or search pages`，然后在目标位置打断点跟踪
  - 还可以打dom元素属性变更的断点

- 同步难点
  - 将indexeddb的数据存储转换为mongodb-like结构
  - 如何同步 mongodb-like 的结构，是否用 crdt，还是 http
  - 是否需要中心化服务器
  - 不必过于纠结crdt的集成或三方库，关注于官方同步示例，如block-editor/y-indexeddb/dexie-sync

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

- search
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
  - [x] 使用command方式迁移text bold/italic

- 鼠标事件顺序
  - mousedown -> mouseup -> click
  - 鼠标先点击input，再点击button，触发的事件顺序
    - mousedown ->  onblur(input) -> mouseup -> click
  - 注意
    - ❓ 在mouseup回调中可以拿到selection取位置，但click回调中selection就变为空了

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
# dev-05

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
# dev-04

## 0429

- todo
  - subPage悬停菜单消失了
  - 基于slate编辑器实现添加和清除富文本格式

- 废弃 getWorkspaceConfig，自定义数据的读写统一用 get/setDecoration

- 搜索的初步实现
  - 搜索根据索引实现，而不是直接搜索源数据
  - 元数据更新时，搜索结果是即时反馈的
  - page内容更新时，搜索结果要等待一段时间

- 在代码实现时，有疑问的、做决策花了很多时间的，要文档记录、然后讨论

- pageEditorBlock.getChildren 获取所有直接block
- workspaceDBBlock.getChildren ?

- redo/undo分2类
  - 文字加减
  - 异步：上传文件、删除文件

- ctrl+a 全选是否要选上标题
  - notion选上
  - 飞书第二次ctrl+a才会选上标题

- 检查所有block的backspace、enter按键后的光标位置
  - 特别是todo list

- 从block查找其他block都通过搜索来实现

- 富文本相关文字创作完全依赖slate实现

- divider在回删时，保留分割线且删除到上个block，参考notion

## 0428

- 在架构上分离 dbBlock、businessBlock、editorBlock
  - dbBlock是block在存储层的存储结构和实现
  - businessBlock是block在业务层的较为通用的数据结构，通过dbBlock计算或转换得到
  - editorBlock是block在具体编辑器业务层的数据结构，是编辑器直接存取的业务数据

- 将数据转换和计算放到组件层，还是放在service层？
  - 一个判断方法是，其他地方需不需要用原始数据？转换后的数据？
  - 切换到react-native后，service需不需要改动？改动大不大？

## 0427

- block-editor插件重构
  - 修改 defaultValue
  - 修改 get properties/fields
  - 新增 PageModel PluginModel
  - 💡 将db操作重构为传统CRUD应用的service层

## 0426

- dev-to-daily-notes
  - 点击每个日期时，显示当天的自动生成的统计page。只读？
  - 显示什么内容？
    - todo list 列表
    - 文档创建修改记录

- debug在特定版本浏览器才会出现的问题
  - 首先在同一台电脑上多试几个浏览器，如果只在一个浏览器出现问题，在其余浏览器是正常的，则说明是浏览器的问题，而不是代码的问题
  - 在问题浏览器上debug时，发现问题是y-websocket的监听4个事件只处理了2个漏了2个导致的，但单步debug调试能锁定问题的位置和异常值

## 0425

- dev-to-calendar-heatmap
  - 🤔 用户昨天只新建了一篇文章A，日历上显示最浅的颜色，今天把文章A删除了，要不要更新日历颜色
    - 每次登录系统根据db数据动态计算，所以删除page后，颜色就变浅或消失了

- databse需求讨论及数据结构
  - notion中2个database跨表格拖动行时，对非文本列，根据列定义名称匹配
    - 若将tableA的tags列拖到tableB的tags列，若OptionA在tableB中也存在，则显示，若不存在，则OptionA对应的列显示为空
  - 要考虑支持列名的国际化
    - 列名不能是字符串，要考虑方便用户添加翻译配置，使用对象
    - 交互实现可以用2个输入框
  - 省略的效果就是折叠展开，不支持部分折叠展开

- 🤔 列定义、tags的动态修改放在page级别，还是workspace级别？
  - 参考现有产品的设计
  - 一个page的tags/column变动了，其他page也要变？
  - tags跟随page?
  - 💡 讨论阶段性结论
    - 在跨group层级拖动block时，会先合并列字段，始终都是增量合并的方式，若存在同名列，则新建列col(1)
    - 根据col名称合并

- 目前db搜索所有content
  - 要优化对元数据的搜索

- 对无序列表，一行是block
  - 切换成看板视图，子任务显示进度
  - 切换成列表视图，子任务在单元格？缩进子列表？

- 用户选中任意元素的组成 block-group
  - 隐式创建group的规则取舍太多
  - 可以先实现显式手动创建group，在体验中继续优化逻辑

- 默认一个page所有内容都在一个group

- local-first要考虑用户断网的场景

- 有对手比没有对手好。接下来我们的每一步都有honourable的对手：
  - block transform ——》干死notion和monday，asana
  - page transform ——》 干死miro和mural
  - 版本控制 ——》干死almanac
  - blockdb加密协作，selfhost ——》干死skiff和anytype
  - 网页发布时编辑器套壳editor ——》干死super和simple.ink
  - automation，流程自动化 ——》干死google docs和uipath

## 0422

- daily-note初步实现
  - 查询某一天的所有pages，基于search api实现
  - 搜索基于tag实现
  - 前端blockdb的搜索实现，直接用sql，还是自定义dsl
    - 倾向于类似mongodb的查询dsl，完善类型，查询简单

- daily-notes的数据源包括本地数据库和服务端数据2部分
  - 本地直接读取
  - 🤔 服务端数据可以直接请求数据、可以先从数据库请求然后前端从本地数据库

- 登录时需要fetch recent workspaces，因为有多设备同步的问题
  - 若用户先在设备A使用了spaceA，然后在设备B使用了spaceB，当再次登录设备A时应该进入spaceA

- PageTree小结
  - 标题支持点击和拖拽事件
  - 支持保存和恢复折叠展开状态

- dnd-kit-onClick 失效的问题
  - https://github.com/clauderic/dnd-kit/issues/296
  - useSensor(PointerSensor, { activationConstraint: { distance: 10, }, }); 

- pm-features
  - block transform: notion/monday/asana
  - page transform: miro/mural
  - version control: almanac
  - self-host with encryption: anytype/skiff
  - publish editor: super/simple.ink
  - automation: uipath/google docs

### oneOnOne-terry-google-docs-产品矩阵

- 2005年收购 wirtely(doc)、xl2web(sheet)、DocVerse(collab)、QuickOffice(mobile)
- 2015年google工程师回国，本地化、替换docker，发布一起写
- 2017年快手收购一起写
- google-docs控制台调试，save?id
- 快手，?sid=
- doc核心 
  - 排版gui
  - 数据交换协作协议
- google办公套件
  - drive
  - document
  - sheet
  - ppt
  - form
  - cloud file
- 产品一体化的研发趋势
  - 黑盒卡片，集成im、figma
  - 编辑器能力插件组合，学术版、设计版，类似vscode扩展包、ckeditor打包了四五种

- 壁垒
  - gui架构
  - 排版器
  - sheet比doc更复杂

## 0421

- 登录时，PageTree显示untitled

- PageTree 数据结构和更新分析
  - 更新标题名称时，异步通知再重新读取标题
  - 更新标题顺序层级时，先更新缓存，再异步保存

## 0420

- PageTree现有组件的问题
  - 所有内层叶节点默认展开，而不是记住折叠状态

## 0419

- dev-to
  - [x] 修改获取初始workspace的流程，优先使用本地找不到，可以不从api获取

- 大日历暂停

- 先实现文章数据保存和恢复

- 重构编辑器的load-save
  - .get()
  - .set()
  - 去掉 .getContent()

## 0418

- discussion
  - 小日历接入实际创作数据时，日历颜色根据什么指标确定？创建、修改文件数量？
    - 日历颜色分3级，分级指标如何确定？ 3/6/9？
  - daily-notes数据具体包含哪些数据？ pin+todo-task+activities/comments
    - 每天的daily-notes文档是动态计算生成的？还是把前一天的算好了存起来？若预先存储长期会占用空间？
  - 顶部导航条什么时候显示7天日期？因为默认显示2个视图切换按钮
  - 左侧日历热力图切换弹窗大日历？全页的大日历还存在吗？

- dev-to
  - 重写PageTree正在进行中

- google-calendar的格式已成为协同类产品的基建
  - 功能参考
  - 导入导出日程

- 编辑器的数据与无状态react组件分离
  - `<ReactComp blockId={dbBlockId} />` 抽离出react组件
  - 让看板组件、日历组件能够在editor里面用，也能单独使用

- 白板和editor集成的额外信息
  - 白板shape的位置信息
  - shape所属group

## 0415

- dev-to
  - 前端项目请求api通过proxy代理到线上服务端
  - PageTree组件重写
  - 后端登录流程熟悉

- @nrwl/web:dev-server 的配置项不包含proxy, packages\web\src\executors\dev-server\schema.json
  - 但其他文档有个单独的页面介绍了配置方法，proxyConfig
  - 对照webpack-dev-server的文档，发现沿用了其配置
  - nx的代理配置不在options页面，而在单独的配置教程页面，要先搜索，再提问讨论

- 多个useEffect尽量不要依赖执行顺序
  - 有时候，deps依赖项过多，effects就会比预期的先执行，结果常是显示旧数据

## 0414

- dev-to
  - 本地配置代理，直接使用后端在线服务
  - 🤔 本地是否要实现免登录

- daily-notes/calendar-view
  - 作为文档的入口，比文档更高一级

- workspace、page 的content可以用来放metadata
  - 普通block的content用来放内容

## 0413

- 工作小结
  - 因为在线api服务无法跨域访问，就在本地跑通了登录、获取workspace列表的逻辑
  - 对接blockdb相关
    - 去掉找不到workspace的404页面，默认workspace为space前缀_userId
    - 用户登录后，默认打开上次访问的文件，逻辑没跑通
    - 刷新页面恢复用户和页面相关数据，需要继续完善
  - PageTree获取blockdb数据源失败了，因为api改变了
    - PageTree的更新方式有2种，会采用哪一种
  - 登录相关细节优化
    - 登录后显示google头像、退出登录
    - 顶部导航条切换白板视图和页面视图已经work

- dev-to
  - workspace flavor类型的block用来干嘛的
    - workspace与page是如何关联的
  - page flavor类型的block应该是类似以前的doc
    - 如何设置title、author、lastUpdate、create
  - 迁移到新db后更新目录树的数据源

- 若没有workspace，则新创建默认workspace

- block flavor  
  - workspace, page, text, title, comments, tag, reference, video, audio, image

- blockdb结构
  - workspace、page、block
  - page.insertChildren(block1); 

- 实现数据存储和操作时，要考虑 编辑器多实例的问题

- [wsl安装mongodb教程](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)

- caddy类似 nginx

## 0412

- 浏览器滚动条宽度
  - The default scrollbar width can range anywhere from 12px to 17px. 
  - Webkit browsers also have the ability for the user to configure scrollbar widths. 
  - Webkit browsers, such as Chrome can have custom scrollbars that can have any size scrollbar.

## 0411

- 数据请求的问题
  - api函数放在哪里
  - 有没有比拆分更好的方式

- 💡 发现将 useUser 和 useSpaces 合并为一个hook后能够减少请求次数，同时降低复杂度，流程更清晰

- dev-to
  - 推进产品上aws

- 白板的激光笔设计，笔迹3S后自动消失

## 0408

- dev-to 完善本地数据库操作和文档树操作的逻辑
  - 文档树的拖拽按钮被挡住了，重构为拖拽标题改变顺序
  - 实现左侧面板滚动条

- linear
  - 最常用的单位是issue
  - 看板常用于浏览数据，而不是修改数据
- height
  - 完全任务的动效，提升体验
- cron
  - 专注于日历，日/周/月

## 0407

- 研发方案讨论
  - 全局共享dbClient的方式，共享editor对象的方式
  - documentdb vs blockdb，该用哪一个
  - 全局状态管理

- 协作的粒度是block
  - block层级 workspace-page, page, sub-page
  - PageTree优先级很高

- 文档树旧bug
  - 拖到最下面时，会弹到最上面

- 产品
  - workspace 数据
  - login
  - daily notes

- 左侧面板需求讨论
  - 面板内容如PageTree页面树太高时、太宽时如何显示和交互？
    - 太高时，是否显示滚动条
      - notion一直会显示定制滚动条
    - 太宽时，总是显示一行？
  - 页面树每行
    - 在鼠标悬浮时，应该显示哪些内容
    - 拖拽的部分是标题文字，还是尾部手柄

- PageTree 组件需求分析
  - 每行内容为👉🏻️ 折叠按钮 + 文档图标 + 标题 + 悬浮操作菜单
  - 折叠展开
  - 拖拽移动实现改编顺序和层级
  - 拖拽时显示位置提示条
  - 每行末尾为悬浮操作菜单

- doc-db执行db.set时异常 insert a new version before save
  - 不能用 doc.addVersion('')
  - 应该用 doc.addVersion(' ')

- react-router
  - useNavigate() may be used only in the context of a `<Router>` component. 
  - I think duplicated react-router-dom is the problem. Removing react-router-dom can be the solution

## 0406

- 日历问题
  - 选择年份后，星期那一行会被挡住，经排查是flex-column的弹性项目height不生效的问题

- 还原设计稿时，注意卡片div2的margin是32px的代码实现方式， div1 > div2 > div3
  - div2的margin为16，div2的内容div3如span的margin也为16

## 0404

- dev-to
  - calendar-heatmap细节调整到完全还原设计稿
  - 迁移旧项目文档树组件到新产品，并mock数据
  - 完全理解dnd-kit的原理，设计实现多维表格的拖拽列宽度
    - drag和layer的工作以前都做过，但没系统地总结
  - 重新实现calendar-heatmap组件

## 0402

- 当div定义宽度和实际宽度不同时，排查方向应该是作为flex容器内项目的grow或shrink比例生效了
  - 若要去掉自动放大缩小，flex可取值 auto (1 1 auto) 和 none (0 0 auto)

- 注意图标按钮写法
  - `<IconButton><SvgIcon /></IconButton>` 如果只把svg设为visibility： hidden，那么外层IconButton的hover仍然会存在，不符合预期交互

## 0401

- 顶部导航条的元素依次是
- HeaderStart
  - logo图片
  - 侧边菜单图标
  - 版本记录图标 + 版本文字
  - 文章标题，可选emoji
- HeaderMiddle
  - 文章页
    - 视图切换按钮：文章视图、白板视图
- HeaderEnd
  - 用户下拉菜单
  - 打开文章面板

- `升级到pro版`的元素的定位是fixed ？
# dev-03

## 0331

- 日历热力图沟通
  - 不显示当天
  - 颜色分3级

- style9的样式keys只支持 at-rules or pseudo selectors
- material v5正在将部分组件迁移到付费plan
  - 已迁移 data-grid、tree-view、date-picker
  - 迁移中 charts、sparkline、gauge

## 0330

- 为什么要自定义calendar组件 / mui-组件DatePicker的问题
  - [x] 需要参考现有组件实现i18n
  - [x] 自定义样式更灵活，如日期背景色、日期背景形状、日期小红点
    - mui v5的日期选择器内层组件会丢失className，变通方案是使用普通css selector
    - 自定义切换年月图标、星期与月份文字
    - 定制日期选择的方块大小、方便与头部星期几对齐，同时控制高度增加时不会显示竖直滚动条
  - 定制功能更方便，如鼠标悬浮提示
    - 定制选择年份的面板的内容，定制打开年份选择器时显示的初始年份(StaticDatePicker)
  - eg: Customized day rendering 👉 StaticDatePicker 没有弹出层
    - renderDay属性类型是function
  - eg: Dynamic data 👉 DatePicker
    - renderLoading属性显示日期空白占位符
    - 切换月份时更新highlightedDays
    - renderDay属性值函数返回的是封装过PickersDay的组件
  - eg: Sub-components 👉 CalendarPicker, MonthPicker, YearPicker
    - rendered without a wrapper or outer logic (masked input, date values parsing and validation, etc.).
    - 没有renderDay属性

- StaticDatePicker 源码结构
  - Picker
    - CalendarPicker
      - YearPicker
      - MonthPicker
      - PickersCalendar 选择日期

- PickersCalendar 源码结构
  - PickersCalendarWeek
    - PickersDay
      - children

## 0329

- 两个daily notes
  - 左侧calendar，日历热力图
  - 上侧全屏calendar，交互细节还要设计和修改

- cloverapp的daily notes文档是自动创建的
  - subscription events
  - overdue tasks

- dev-xp
  - 用户可编辑/不可编辑，作为系统内置的filter实现
  - 本地数据库是否都要支持pin、第三方导入的？
    - 实现时讨论，本地pin预缓存然后合并云端数据源

- [TS2322: Type 'Timeout' is not assignable to type 'number'](https://stackoverflow.com/questions/55550096)
  - You could try with using `window.setTimeout` instead of just `setTimeout`, this way the typescript one will be explicitly used
  - `let timeoutId: null | ReturnType<typeof setTimeout> = null` 显式声明
    - timeoutId = setTimeout(fn, 1000)

- 遇事不决，先按 F12 > Application/应用程序 > 存储/Storage > 清除站点数据 Clear site data

## 0328

- fix类型后，出现编辑器持续重复渲染，且无法正常工作的问题
  - 排查原因，先稳定复现bug

- 新编辑器抽象层次
- app 
  - useDatabase => `<BlockEditor db={database} />` 传递数据库操作实例
- block-editor
  - 定义block-editor的vdom结构，以及初始化editor对象
  - EditorRoot, div, RenderBlock
  - createDefaultEditor -- createStandaloneEditor

## 0327

- 浏览器中人工合成（synthetic）的事件派发（dispatch）是同步执行的，包括执行click()和dispatchEvent()这两种方式。
  - Unlike "native"(dom) events, which are fired by the browser and invoke event handlers asynchronously via the event loop, dispatchEvent() invokes event handlers synchronously

```JS
console.log('本轮任务');

new Promise((resolve, reject) => {
  resolve(3)
}).then(() => {
  console.log('本轮微任务');
});

// 💡️ 通过click方式触发的事件是同步执行的，只有浏览器自己触发的事件才是放在一个 macrotask 里执行的。
document.body.addEventListener('click', () => { console.log('click-synchronously'); })
document.body.click()

// 本轮任务
// click-synchronously
// 本轮微任务
```

## 0326

- block-editor新编辑器类型补充
  - 难以补充类型的use case，主要是深层路径属性的取值
    -  const element = editor?.children?.[path[0]]?.children?.[path[1]];

## 0325

- ts noImplicitAny的解决方法
  - // @ts-ignore

- Property 'current' does not exist on type 'ForwardedRef
  - [React fordwardRef with typescript](https://stackoverflow.com/questions/69503174)
  - `type ForwardedRef<T> = ((instance: T | null) => void) | MutableRefObject<T | null> | null;` 类型定义
  - Therefore attempting to just access .current, without doing some type checking, won't work because functions do not have such a property.

```jsx
// This should work:

const ProfileMenu = forwardRef<HTMLInputElement, PropsDummy>((props, forwardedRef) => {
  if (forwardedRef != null && typeof forwardedRef !== 'function') {
    console.log(forwardedRef.current);
  }
  
  return (
    <div className="App" ref={forwardedRef}>
      <h1>Hello there</h1>
    </div>
  );
});
```

## 0324

- nx
  - nx build myapp --skip-nx-cache

- 使用nx编译修改源码后，nx在cli编译仍然报错
  - src/lib/Text/Text.tsx(459, 25): semantic error TS7030: Not all code paths return a value.
  - 原因是，nx在命令行报错针对的是转译后的代码；
  - 要修改源码错误，应该以ide提示的problems/error的行数位置为准

- typescript playground可以打印出类型变量定义的结果，使用 `// ^?` 然后鼠标停在问号后就可以显示类型定义的结果
  - 如果不能显示，可以刷新页面，之后就能显示
  - [打印类型的示例](https://www.typescriptlang.org/play?pretty=true#code/C4TwDgpgBAqgdgSwPZwPIDMAqBXMAbCAZygF4BYAKCmqgB8oBtAIgAUE4BrJgGilYEM4wABYQATkwC6lGnUZMASkn4ATHnwXY4ccVJk16zNh37qmAYWHY9FSqEhRUAIwBWEAMbAAYmKQBbHHwiAB5AgmIIAA9gCDgVYgZCYDF2AHNeJJS4VMkAPlIoAG99agYw6HYocuJ+YnKGAAZJSQAuKtwCBgBGaQoAXygAMiK+yjtwaAUibDxgAuc3Tx9-auD4ZDQsDqJcygB6PdkAPQB+MYp7aEwJroKpwhm5+gByTLTngG59w5pToA)

## 0323

- pnpm: fast, disk space efficient package manager
- features
  - fast
  - efficient
  - support monorepos
  - strict access to pkg with non-flat node_modules

- nx: build system with first class monorepo support and powerful integrations.
- features
  - Best-in-Class Support for Monorepos
  - Integrated Development Experience
  - Rich Plugin Ecosystem

- ckeditor顶部工具条的dropdown被页面顶部导航栏挡住的原因
  - 编辑器的父容器使用了自定义滚动条，外层div-overflow：hidden，内层div-overflow：scroll
  - 临时的解决办法：外层 overflow：auto，内层div-overflow：auto，但此时编辑器无法滚动了
  - 💡排查元素被部分挡住的问题，思路是查找position-absolute的元素、overflow-hidden的元素

- 替换ckeditor图标的2种方法
  - 1. 编译器替换：new webpack. NormalModuleReplacementPlugin
  - 2. 运行期替换：自定义插件 localizedBoldPlugin 
    - boldButton.icon = getIcon( 'bold', locale.language );
    - 适合做国际化图标合文字
    - https://github.com/ckeditor/ckeditor5/issues/1613
  - NormalModuleReplacementPlugin site:github.com/ckeditor/ckeditor5
  - 在com-editor项目替换ckeditor图标完成后，在前端项目却仍显示ckeditor图标的解决办法
    - 在com-frontend项目重复替换图标的逻辑

```SCSS
// 修改cke工具条文字
& .ck.ck-toolbar__items .ck-heading-dropdown {
    & .ck-button_with-text .ck-button__label{
      color: #133b75;
    }
}
```

## 0322

- milestone 交付jnu-editor编辑器
  - not-yet
    - 将bibtex插入编辑器的逻辑实现有问题，如何只在光标点击editor内容后才执行插入bibtex的command，否则就会出现现在的问题，鼠标若不再editor中点击一下就不执行该逻辑

### 多维表格和看板-pending

- 工作记录在20211220之前
- my-agenda
  - [x] 点击任务卡片时，应该出现弹窗
  - [x] checklist/子任务
  - [x] 创建文档
  - [x] 添加日程：开始时间、结束时间
  - [x] @负责人成员或用户
  - [x] 看板卡片右上角的删除、更多图标应该悬浮时才出现
  - [x] 鼠标在卡片上方时，形状应该是pointer，而不是拖拽的grab
  - [ ] 卡片弹窗应该自动保存内容，而不是显示保存和放弃修改按钮
  - 卡片上文档列表展开时，底部头像会被快速挤到卡片之外，然后快速还原
  - 卡片上需要动作菜单列表，对话框需要弹出搜索列表、选择列表、日期面板
  - 子任务暂时不能修改，只能先删除再添加，需要一个列表
  - 将卡片拖动到最右边`添加分组`的空列时，应该支持自动新建卡片
  - 标签、子任务添加按钮出现时，旁边应该还有取消按钮
  - 对于看板上的日程，近期日程除了日期数字外，还可以显示类似下周日这样的文本
  - 看板任务与编辑器打通
    - 全局task检索和展示
    - 打通 看板任务、文档侧边栏的任务
    - 在文档中的不能修改checkbox，打开弹窗才能修改
    - 子任务转换成任务卡片
  - 看板设计其他参考
    - 看板必填项
    - 企业倾向于自动发邮件
      - 倾向于低代码完成自动化流程
- 多维表格实现计划
  - [x] 工具条 + 表格
  - [x] 切换普通表格视图、分组表格视图
  - [ ] 分组表格的测试数据修改为trello格式，也会作为看板数据源
  - [x] 切换表格视图、看板视图
    - 如果要做得像notion，不妨做得更像一点，样式改成适合编辑器的卡片和看板样式
  - [x] 实现表格视图下特殊字段的显示，如子任务、参考文档、标签
  - [ ] 全局菜单 字段配置
  - [ ] 表格拖拽改变列宽度
  - 表格顶部的工具条和标题栏都应该支持sticky到页面顶部
  - 表格数据导出
  - 编辑一行、单元格
  - 子任务转换成任务卡片，任务卡片转换成子任务
  - 样式调整
    - 表格整体左边框和上边框缺失
  - 去掉依赖
  - 复制表格自身到下方的动画
- 多维表格计划待定
  - 支持添加任意自定义字段
  - 支持设置字段类型，内置常用数据类型
  - 过滤筛选支持组合条件，如多个条件求交集
  - 更多搜索方式，如日期范围
  - 可设置显示 表格左边和上边的索引列、索引行
- 多维表格实现问题
  - 🤔️ 多个视图来回切换时，如何保存每个视图的状态
    - 表格的每个ui状态都可以由tableOptions确定
  - 要不要区分普通表格和分组表格
    - 分组表格不适合 合并单元格
- 多维表格实现说明
  - 分组
    - 暂时只支持离散变量，不支持连续型数值
    - 破坏了useExpandAll的sticky header
  - 竞品参考
    - 飞书和notion的多为表格都是现在在编辑器页面中，未考虑分页的情况
- 🤔️ 看板组件和表格组件切换视图的状态设计问题
  - 除非要明确使用缓存，否则每个视图的数据都应该动态计算出来，这样能减少内存消耗和及时同步更新
    - 在顶层定义更新一行数据的方法，传下去
    - 每个视图层可以进一步封装顶层数据更新方法，然后更新自己的ui时更新顶层数据和配置
  - 工具栏的状态应该放在每个视图层，工具栏的dom可以放在顶层
    - 每个视图可显示不同的过滤条件
  - ✅️ 都存在自己的内部状态，将顶层存储数据和更新方法都传到2个组件
    - 数据更新方法被调用后，所有视图被刷新
  - ❌️ 以表格内部状态作为基础，将表格组件的数据和更新方法传到看板组件
    - 表格更新时，数据源更新，看板会更新；看板更新时，表格也会更新
    - 如果只创建看板视图，那没必要定义表格数据的更新方法
  - 如果增加其他视图，比如甘特图呢？
    - 定义一份配置数据，传下去作为初始state
- 表格 not-yet
  - 表格末尾为什么会渲染一个英文分号

### products-old-dev-log

- 重构题头部分
  - [x] 更换emoji picker
  - ~~字段列表分类型重构~~
- 编辑器
  - blockquote插件中的换行，每次刷新页面后，中间的空行会加一个
    - 空文档无此问题，复制示范文档会出现此问题
  - 图片按回车不能换行
  - [x] 编辑器工具条第一个查找替换图标是烂图标，左上部分都是黑色
- 文章页
  - [x] 去掉水平滚动条
  - [x] 使用CustomScrollbar后，最好去掉浏览器默认的竖直滚动条
- 文章左侧标题目录toc
  - [x] 点击无法跳转
  - [x] 收起折叠按钮会被文章中的图片挡住
- 侧边栏部分
  - 已注册的用户是不可删除的，是否应该不显示删除按钮
  - 参考文献
    - 连续按两次插入bibtex后，会出现2个编辑器
    - [x] 有时点击插入bibtex的图标会无反应
      - 首次添加bibtex时，新添加的bibtex entry会带有onClick点击事件
- hard
  - 粘贴第三方文章如知乎专栏复制的文章时，侧边栏和导航栏字体会缩小到无法辨认
    - 光标移动到待创建双链的文字的位置时，文字会突然缩小

### products-old-not-yet

- my-agenda
  - workspace 文档列表
    - sticky header
    - 删除文档后，只在列表删除了，文档数据库中仍然存在
  - 全局路由守卫的时机错误
    - ~~**应该在路由跳转前重定向，而不是在路由跳转后再次跳转**~~
      - 在跳转前显示loading可以解决此问题
    - 登录后无法访问登录页，需要实现退出登录的逻辑
- 任务看板
  - features
    - 切换 列表视图、看板视图、时间线(甘特图)视图
    - 从看板创建文档
    - checkbox
- 看板 to-do
  - [x] 负责人列表不能多选
  - [ ] 截止日期不能清除
  - 看板、表格的数据考虑全局，暴露出去给其他组件访问
- workspace如何设计
  - 本地仓库、云端仓库
  - 我的仓库、公共仓库
  - 是否可参考github仓库？
- 文档核心功能
  - 双链展示
  - 分支文档
  - 工作空间内搜索
- ux交互设计
  - 落地页/未登录时的宣传页
  - 个人主页/首页
  - 工作空间页
  - 国内环境不适合对接github，可考虑百度网盘
- 新首页设计与工作计划
  - [x] 首页使用~~类似workspace的设计~~，快捷菜单跳转到workspace
  - [x] 布局改为左侧边栏
  - [x] 文档列表只显示创建的文件，最近操作的文档要跳转到单独页面
  - [ ] 文档列表：pin置顶一个日期
- 编辑器工作计划
  - ~~左侧目录显示参考文献锚点~~
  - ~~编辑器首页顶部显示图片~~
  - 日期时间的处理
    - 可参考日历组件的实现方案
  - 流程图bug
    - ~~复制粘贴后，就变成图片，无法编辑代码了~~
- 检查图片的接入方式
  - toolbar打开文件选择器
  - 拖拽本地图片到编辑器光标位置
  - ctrl+v粘贴图片到编辑器
- 图片上传的问题
  - ~~将 同步执行的createObjectURL 改为 异步执行的 `FileReader.readAsArrayBuffer` + `new Blob([arrayBuffer], { type: "mime/type" })`~~
  - 上传已经以前已经上传过的图片时，是否保存了2份数据，存在冗余
  - 首次渲染图片时，由于blobUrl失效了，控制台会报错
    - blob:http://127.0.0.1:4001/223c5400-55e2-4ac7-b936-574b47cd0201 net::ERR_FILE_NOT_FOUND
  - 考虑直接将数据库中docId存储到编辑器图片model
- 如何在自定义插件中使用官方image-plugin的功能和UI
  - 类似插入buttonView一样插入imageView
  - 需要继承官方plugin暴露的各个class，然后添加自定义逻辑，再glue一个新的入口类
- 是否需要更新图片标题的显示逻辑
  - 若不存在，则默认不显示；选中图片时，可输入标题
  - 若存在，则始终显示；选中图片时，可输入修改标题
  - 图片下方标题默认居中对齐
- 要不要实现自定义image-plugin
  - 双击图片时，会在蒙版层中放大图片，全屏显示图片
  - 图片裁剪图标
  - 系统操作菜单，如收藏、下载、删除当前图片
  - 替换当前图片
  - 自定义图片标题的显示和更新逻辑
  - 如何插入inline图片，插入图片后，先缩小，再拖放到一行内
- 图片工具条的设计
  - notion 鼠标悬浮时自动显示工具条
    - 图片处于选中状态时，图片和caption上方会出现蓝色蒙版
    - 工具条在图片之内
  - 飞书 鼠标悬浮时图片会显示蓝色边框，图片上方会显示工具条
    - 图片处于选中状态时，蓝色边框会变成深蓝色，此时鼠标悬浮到其他图片上方时不会显示工具条只是边框变蓝
    - 工具条在图片外，且无三角形指示位置关系
  - ckeditor 鼠标悬浮时会显示边框
    - 图片处于选中状态时，会显示工具条
    - 工具条在图片外，且有三角形指示位置关系
- boxEditing, boxUI 的ui部分为什么总是toolbar界面相关的内容
  - 插入元素的位置，通常放在command
- later
  - 就算postcss-loader/style-loader版本与官方文档一致，也可能会出现demo样式异常的问题
  - 测试连续调用自定义hook时useRef的current的值的变化

## 0321

- editor自动保存失败
  - 复现方法
    - 在toe-editor仓库不能复现，说明问题出在前端应用层
    - 当光标闪烁时，如光标在标题处刚修改完闪烁时，立刻刷新页面，就能复现
  - 原因排查
    - yjs的set不是原子操作，先删除，再添加；当删除后，文档数据库gc发生，文档内容就变为空了的，之后执行的添加操作就成了添加undefined，内容变成空

```
  Uncaught (in promise) TypeError: Cannot read properties of null (reading 'forEach')
    at Bs (index.js:9:66961)
    at Fs (index.js:9:67618)
    at index.js:9:83227
    at ps (index.js:9:57845)
    at yn.insert (index.js:9:83194)
    at yn._integrate (index.js:9:82305)
    at Bn.integrate (index.js:9:91244)
    at Fn.integrate (index.js:9:94802)
    at qs (index.js:9:68815)
    at index.js:9:71751
```

- react-table virtualized之后要检查功能
  - scroll to index
  - search/filter
  - row selection
  - 示例参考
    - https://codesandbox.io/s/cubs-react-virtualized-resizable-sortable-filterable-table-x77iw
      - 支持 virtualized、global filter、row selection

## 0320

- js处理私有属性的方法
  - ❌️ 名称以 _ 开头
    - python、dart也有此习惯
    - ide提示时很清晰
    - microsoft/google都不推荐这种方式
  - ✅️ 将私有属性或方法的声明全放在最前面或最后面
  - ✅️ es6新提案支持class的属性名或方法名以#开头代表私有
  - ❓️ 使用Symbol类型的值作为私有属性名
    - 使用反射api可以获取到Symbol值

- prosemirror offline / local-first

## 0318

- 新品ui交互设计
  - block工具条、多维表格工具条
  - 将多维表格转换成todo-list，多维表格多余字段可折叠展开
  - 无序列表、有序列表，实现为可拖动的树
  - 每个block可外挂插件能力，缩进、可折叠、设置人、设置时间

## 0317

- 交付测试问题
  - bibtex文中引用问题
  - 登录后取出空白文档
  - 现在正在有人编辑的前端实现

- css选择器选择style属性的方法
  - div[style*="display:block"]

## 0316

- bibtex列表需要虚拟化
  - 去掉竖直滚动条
  - 避免每次添加bibtex后刷新数据，列表重渲染后会跳转到顶部的问题
  - 跳转到第一条就很简单

- Shouldn't it be when useRef.current changes, the stuff in useEffect gets run?
  - Short answer, no.
  - react组件rerender的原因：
    - prop变化
    - state变化
    - parent rerender

```JS
export default function App() {
  const myRef = useRef(1);
  useEffect(() => {
    // ⚠ myRef.current变化后，effect不会执行
    console.log("myRef current changed"); // this only gets triggered when the component mounts
  }, [myRef.current]);
  return (
    <div className="App">
      <button
        onClick={() => {
          myRef.current = myRef.current + 1;
          console.log("myRef.current", myRef.current);
        }}
      >
        change ref
      </button>
    </div>
  );
}
```

## 0314

- dev-plan
  - bibtex支持更多类型
  - 有时插入bibtex不会触发文末参考文献的更新
  - bibtex refList 可以添加同名文件，然后控制台会打印异常信息
  - 点击标题名跳转路由后，文末参考文献消失了，为什么
  - undo-redo 未处理恢复和删除参考文献、双链的情况，文末参考文献也应该同步更新
  - [ ] 双链从文中删除时，却没有从尾部删除
  - [ ] 默认字体修改为衬线体
  - [ ] 修复字体突然变小的问题
  - [ ] 定制标题样式
  - [x] ~~编辑器中普通双链文章也无法点击跳转了~~，url也变化，但需要手动刷新浏览器

- 需求讨论
  - 其他人有权限删除我的文档
  - 更新bibtex的流程，推荐先删除再添加，如一个book bibtex，开始没有chapter，后面添加了chapter，那系统会认为是2条文献，对于title/booktitle/chapter字段的增删默认认为是2条

- 不能稳定复现的bug
  - 文档树一直显示转圈加载中

```bibtex
@inbook{CitekeyInbook,
  author    = "Lisa A. Urry and Michael L. Cain and Steven A. Wasserman and Peter V. Minorsky and Jane B. Reece",
  title     = "Photosynthesis",
  booktitle = "Campbell Biology",
  year      = "2016",
  publisher = "Pearson",
  address   = "New York, NY",
  pages     = "187--221"
}

@phdthesis{CitekeyPhdthesis,
    address = { Stanford, CA },
    author = { Rempel, Robert Charles },
    month = { 06 },
    school = { Stanford University },
    title = { Relaxation effects for coupled nuclear spins }
}

@inbook{test,
  author={Grandstrand, O.},
  year= 2004, 
  chapter={Innovation and Intellectual Property Rights}, 
  editor = {J. Fagerberg and D. C. Mowery and R. R. Nelson}, 
  title= {Oxford Handbook of Innovation}, 
  publisher= {Oxford University Press},
  address= {Oxford}, 
}

```

- continue和break支持在各种for循环中使用
  - By loops I mean for, for...in, for...of, while and do...while, not forEach, which is actually a function defined on the Array prototype.
  - forEach中要用return

## 0311

- 🤔 debug为什么删除bibtex失效的问题
  - 原因出现在useEffect里面注册db更新的监听器时，每次add后，马上就remove了
  - 解决方法是只在组件卸载时移除监听器
  - 如何定位此问题
    - a. 用浏览器的debug工具，发现useEffect的cleanup函数被执行多次
    - b. 打印注册监听器和移除监听器的log，观察数量不对应
  - The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), the previous effect is cleaned up before executing the next effect.

## 0310

- bibtex列表和文末文献列表都应该使用ErrorBoundary拦截局部错误，避免整个页面坏掉
  - 也可以完善解析容错的逻辑

```bibtex
@article{CitekeyArticle,
  author   = "P. J. Cohen",
  title    = "The independence of the continuum hypothesis",
  journal  = "Proceedings of the National Academy of Sciences",
  year     = 1963,
  volume   = "50",
  number   = "6",
  pages    = "1143--1148",
}

@book{CitekeyBook,
  author    = "Leonard Susskind and George Hrabovsky",
  title     = "Classical mechanics: the theoretical minimum",
  publisher = "Penguin Random House",
  address   = "New York, NY",
  year      = 2014
}

@booklet{CitekeyBooklet,
  title        = "Canoe tours in {S}weden",
  author       = "Maria Swetla", 
  howpublished = "Distributed at the Stockholm Tourist Office",
  month        = jul,
  year         = 2015
}

@inbook{CitekeyInbook,
  author    = "Lisa A. Urry and Michael L. Cain and Steven A. Wasserman and Peter V. Minorsky and Jane B. Reece",
  title     = "Photosynthesis",
  booktitle = "Campbell Biology",
  year      = "2016",
  publisher = "Pearson",
  address   = "New York, NY",
  pages     = "187--221"
}

@manual{CitekeyManual,
  title        = "{R}: A Language and Environment for Statistical Computing",
  author       = "{R Core Team}",
  organization = "R Foundation for Statistical Computing",
  address      = "Vienna, Austria",
  year         = 2018
}

@unpublished{CitekeyUnpublished,
  author = "Mohinder Suresh",
  title  = "Evolution: a revised theory",
  year   = 2006
}

@proceedings{CitekeyProceedings,
  editor    = "Susan Stepney and Sergey Verlan",
  title     = "Proceedings of the 17th International Conference on Computation and Natural Computation, Fontainebleau, France",
  series    = "Lecture Notes in Computer Science",
  volume    = "10867",
  publisher = "Springer",
  address   = "Cham, Switzerland",
  year      = 2018
}

@inproceedings{CitekeyInproceedings,
  author    = "Holleis, Paul and Wagner, Matthias and Koolwaaij, Johan",
  title     = "Studying mobile context-aware social services in the wild",
  booktitle = "Proc. of the 6th Nordic Conf. on Human-Computer Interaction",
  series    = "NordiCHI",
  year      = 2010,
  pages     = "207--216",
  publisher = "ACM",
  address   = "New York, NY"
}

@incollection{CitekeyIncollection,
  author    = "Shapiro, Howard M.",
  editor    = "Hawley, Teresa S. and Hawley, Robert G.",
  title     = "Flow Cytometry: The Glass Is Half Full",
  booktitle = "Flow Cytometry Protocols",
  year      = 2018,
  publisher = "Springer",
  address   = "New York, NY",
  pages     = "1--10"
}

@mastersthesis{CitekeyMastersthesis,
  author  = "Jian Tang",
  title   = "Spin structure of the nucleon in the asymptotic limit",
  school  = "Massachusetts Institute of Technology",
  year    = 1996,
  address = "Cambridge, MA",
  month   = sep
}

@phdthesis{CitekeyPhdthesis,
  author  = "Rempel, Robert Charles",
  title   = "Relaxation Effects for Coupled Nuclear Spins",
  school  = "Stanford University",
  address = "Stanford, CA",
  year    = 1956,
  month   = jun
}

@techreport{CitekeyTechreport,
  title       = "{W}asatch {S}olar {P}roject Final Report",
  author      = "Bennett, Vicki and Bowman, Kate and Wright, Sarah",
  institution = "Salt Lake City Corporation",
  address     = "Salt Lake City, UT",
  number      = "DOE-SLC-6903-1",
  year        = 2018,
  month       = sep
}

@misc{CitekeyMisc,
  title        = "Pluto: The 'Other' Red Planet",
  author       = "{NASA}",
  howpublished = "\url{https://www.nasa.gov/nh/pluto-the-other-red-planet}",
  year         = 2015,
  note         = "Accessed: 2018-12-06"
}

```

## 0309

- 异步保存编辑器数据到本地数据库，导致新数据被旧数据覆盖的问题
  - 先解决新数据一定要覆盖旧数据的问题，用闭包
  - react组件useEffect如何书写节流防抖，应该包装请求方法，而不是包装setState
    - [React use debounce with setState](https://stackoverflow.com/questions/60789246)
      - 示例将防抖过的请求方法声明在了react组件之外，算是一个普通的js方法
      - [debounce in useEffect](https://stackoverflow.com/questions/61785903)
      - [React Hooks 搞定 Race Condition](https://segmentfault.com/a/1190000019893237)

```JS
 useEffect(() => {
   const saveContent = async () => {
     console.log(';; save编辑器数据-闭包 ', content);
     const title =
       new DOMParser().parseFromString(content, 'text/html').querySelector('h1')?.innerText || 'No Title';
     await docInstance.save(content, { metadata: { title } });
     console.log(';; save完成后编辑器数据 ', await docInstance.getDecodedContent());
   };
   if (content !== undefined) {
     saveContent();
   }
 }, [content, docInstance]);
```

```JS
const saveContent2 = useCallback(
  throttle(async (text) => {
    console.log(';; save编辑器数据-闭包 ', content);

    const title =
      new DOMParser().parseFromString(text, 'text/html').querySelector('h1')?.innerText || 'No Title';
    await docInstance.save(text, { metadata: { title } });
  }, 2000),
  [docInstance]
);

useEffect(() => {
  if (content !== undefined) {
    saveContent2(content);
  }
}, [content, docInstance, saveContent2]);
```

## 0307

- VM827:1 Uncaught TypeError: oo is not iterable at anonymous:1:21
  - for (const [k, v] of oo) { console.log(k, v)}
  - 应该使用 for-in

## 0306

- dev-plan
  - [x] 从侧边栏插入bibtex到编辑器时，应用层必须执行 addRef，因为编辑器的command也没有
  - [x] 文末参考文献按作者、年份排序
  - [x] 解决数据请求切换到listener模式后编辑器rerender过多的问题
    - 解决办法 debounce
  - [x] bibtex未显示页码
- 🤔️ 排查添加bibtex需要点击2次的问题 和 文末参考文献无法显示的问题
  - console.log打印出来的是引用，其实打印时刻是3，后面变成了4
  - 👉🏻️ 问题出在数据库层

```JS
// ⚠️️ 获取一篇文章的ref需要传递额外的参数 resolve: 1
(await editor.db.get('1e98d1b3-35d9-47e3-94c0-f7f78d7a0ac7', { resolve: 1 })).getRefsByType('binary')
```

## 0305

- 排查图片无法显示的问题，依次检查渲染层、数据库层
  - 发现编辑器初始化的数据丢失了图片信息
  - 此bug有时不会复现
  - 在frontend项目也能复现出编辑器初始数据图片model缺少源数据id信息

```JS
const docContent = await doc.getDecodedContent();
console.log(`editor取回的数据1`, docContent);
```

## 0304

- dev-plan
  - [x] 完善所有文档列表
    - [ ] 快速查看我的文档
    - [ ] 当前编辑的文章，应该高亮显示？ 不许删除？
    - [ ] 在文档列表点击当前文档时，应当不跳转路由
    - [x] 重构更多操作按钮组
    - [x] 新建文档操作应该传入类似bibtex的数据
      - 新建文档传入bibtex数据后，侧边栏bibtex初始化时search type reference却搜索出来了
    - [x] 文档树和文件列表数据同步
      - 通过双链创建的新文章能立即显示在文档列表，但通过新建按钮创建的文档不会立即显示在文档列表，需要先输入标题
  - [x] 从侧边栏bibtex列表中删除项目
  - [x] 添加bibtex后，未实时取到数据，应该在应用层，还是在数据库层实现？
    - 问题出在数据库层
  - [x] fix 默认显示文末参考文献
  - [x] 通过新建文档按钮创建的新文档没有出现在左侧目录树
  - 待讨论
    - bibtex是归属到workspace，还是归属到文章？
      - 暂时整个workspace共享
    - 新建的空文档(无标题文档、无内容文档)是否要保存？

## 0303

- bibtex与文献的设计
  - 侧边栏的bibtex是数据源
    - 删除后所有地方会消失
  - 文末参考文献完全自动生成，不可编辑
  - 文中引用
    - 只能通过侧边栏插入
    - 能通过键盘退格键删除
- 分享文章的功能
- 清空本地数据库的方法，方便测试
  - editor.db.inspector().clear()
- 文档数据库修改操作丢失的问题
  - ⚠ 当editor在操作currentDoc对象时，若在其他react业务组件中也要操作当前文档，必须使用全局共享的currentDoc对象，不能用db.get(id)得到的对象，否则某处的修改会丢失

## 0302

- 文档数据库问题测试
  - ⚠ 碰到数据库显示有延迟/需要刷新才更新的问题，一定要先检查调用函数时是不是少写了await

```JS
await editor.db.get('article')
// 创建文章后，一定要set，否则下面get返回的是一篇新文档
await editor.db.get(id)
```

## 0301

- 开会小结
  - 新的基座工程项目
    - 路由管控
    - 接入子项目
    - 在test站点能上线
    - 登录保留authing
  - block editor 后端可以很简单
    - 单个拉取
    - 批量拉取
    - version解决同步冲突的问题，但yjs也可以解决冲突问题
  - 客户端如何拉取数据
    - 一批一批
    - 同步数据库
  - yjs的二进制数据包含了历史记录，但二进制默认不可识别，服务器实现搜索需要额外功能
  - 设计block数据表
  - 数据同步放在编辑器层，还是数据库层？ 编辑器变了，通知数据库？还是数据库变了，通知编辑器？
    - yjs提供了合并编辑器多个操作的方法
    - 光标的同步更适合通过yjs
- bug定位，通过vscode-git-graph
  - refactor: docActionsMenu state
    - 无法分页
  - fix table types
    - 无法正常运行
  - chore: remove unused code
    - 可正常分页
    - 65b141e7fcabd98511e73f49aced5d714d044812
- 测试新建文章时文件列表不实时更新的原因
  - 前端读取文件列表是异步，当文件列表在服务端生成也是异步时，可能会出现前端新建文档后，马上打开文档列表时，服务端还没更新索引，前端的列表总是少一项的情况

```JS
await dbClient.getByDocumentType('article').then(docs => Array.from(docs.values()).filter(doc => !doc.metadata?.ttl))
```

- forEach中不能写await的解决办法
  - https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop
  - await y.forEach(async (x) => {
    - await Promise.all(y.map(async (x) => {
# dev-02

## 0228

- dev-plan
  - [x] 添加bibtex去重，根据标题
  - [x] 所有文档列表

## 0225

- 路由部分重构思路
  - 使用isLoading和user对象来判断，而不是userStatus

## 0224

- dev-plan
  - [x] 登录后打开的最近一篇文档，所有人都是相同的
  - [x] 恢复插入数学公式的按钮
  - [x] 用户设置项保存到本地数据库
- 紧急bug
  - bibtex无法添加
  - 协作编辑时，第2个人的输入无法同步到第1个人
  - 打开链接文档会卡顿，打开目录树会卡顿
  - ~~分享功能~~
- 需要修改图标的大小
  - m
    - 上极限
    - 下极限
    - 所有三角函数，如 余弦
  - l
    - 所有矩阵，如 多行对齐等式
- [How to change font-size to a SVG?](https://stackoverflow.com/questions/64914200)
  - You can not change the font size or font width because SVG is not a font. It is Scalable Vector Graphics. 
  - If you would have some text in your SVG, then you could do something with the font from the text element.
  - The trick is to assign with and height the em unit

## 0223

- bugs整理
  - 切换文章相关 (bugs自己消失了)
    - createImgDataRefConverterPlugin() 创建的图片插件有问题，每次切换文章会抛出异常
      - plugincollection-plugin-name-conflict {"pluginName":"ImgDataRefConverterPlugin"}
    - 点击新建文档按钮时，控制台抛出异常  (reading 'model') at Pr._save
  - 创建新文章时，目录树组件更新有问题
  - [x] 登录用户没有workspace时弹窗提醒

## 0222

- 站点测试
  - 重新登录后，编辑器无法显示
- 路由验证的场景
  - 没spaceId就进不去编辑器页面
    - 首次登录时
    - 刷新页面时
  - 退出登录时
    - `location.reload()` method reloads the current URL, like the Refresh button.
    - `location.assign(url)` method causes the window to load and display the document at the URL specified.
- location.href property vs. location.assign() 
  - it may be true that `location.href = url;` is faster than `location.assign(url)`, although it may depend on the JavaScript engine implementation
  - Calling a function should be slightly slower than accessing the property, but in terms of memory there should not be a big difference in my humble opinion.

## 0221

- dev-plan
  - [x] alert-block plugin upcast
  - 设置项保存到本地数据库
  - [x] 高亮块 或 窄宽度的段落
  - ~~通用的文档列表弹窗~~
- ckeditor的默认图标文件导出位置
  - packages/ckeditor5-core/src/index.js

## 0220

- 高亮块功能设计
  - 可调整宽度
  - 可设置背景色
  - 支持编辑高亮块内容
  - 不支持
    - 不支持嵌套高亮块
    - 不支持 > 快捷键
- 高亮块api设计
  - width 0.5, 0.75, 1
  - backgroundColor none, gray, rgby
  - showBorder
- 高亮块ui交互设计
  - 参考 ckeditor blockquote/link/codeblock
  - 配置项放在balloon toolbar
- documentdb接入yjs前的版本是 1.0.32

## 0218

- [How to align horizontal icon and text in MUI](https://stackoverflow.com/questions/51940157)
- [How to keep showing the 'popover' on hovering on the anchorEl and 'popover' as well?](https://stackoverflow.com/questions/54705254)
  - 要点在设置 pointerEvents

## 0217

- 列表项上显示悬浮卡片是不是一种优雅的交互体验？
  - 可采用类似wolai的单独的侧边悬浮卡片
- 为什么编辑器中插入的bibtex文献，点击后跳转的url显示的id变了
  - 原因是默认创建的文档类型是 binary，而不是 article
  - (await editor.db.get('d65338ed-8651-4dc8-91e2-60649e5711db')).type
  - 等待以后修复双链的链接文档

## 0216

- 样式picker almanac侧边栏
  - 主文字 #2E4155，灰色文字 #757C8A
  - font-family: "Microsoft YaHei"
- magic-css-heading-title
  - 为什么文末参考文献 h1-References 的高度为71
    - margin-block-start/end 的效果就是 margin-top/bottom
- 登录后，没有从 /docs 跳转到 /docs/docId 的原因是
  - 后端获取workspace的请求失败了
  - url前面多了一个空格，见npm run dev后webpack-dev-server的异常信息

```bibtex
@misc{piece, author={J Strother Moore}, title={``{M}y'' Best Ideas.\\ \url{https://www.cs.utexas.edu/users/moore/best-ideas/structure-sharing/text-editing.html}}}
@article{Ota1981,
        author = {Terukazu Ota, Yoshihisa Asano and Jun-ichi Okawa},
        title = {Teattachment length and transition of the separated flow over blunt flat plates},
        journal = {Bulletin of the JSME},
        volume = {24},
        No = {192-7},
        year = {June 1981},
        pages = {941--947},
        }
@article{myers1986ano,
    title={An {O(ND)} difference algorithm and its variations},
    author={Myers, Eugene W},
    journal={Algorithmica},
    volume={1},
    number={1-4},
    pages={251--266},
    year={1986},
    publisher={Springer},
    url = {http://web.archive.org/web/20080207010024/http://www.808multimedia.com/winnt/kernel.htm}
}
@article{grishchenko_2010, title={Deep hypertext with embedded revision control implemented in regular expressions}, DOI={10.1145/1832772.1832777}, journal={Proceedings of the 6th International Symposium on Wikis and Open Collaboration - WikiSym 10}, author={Grishchenko, Victor}, year={2010}}
@article{CitekeyArticle,
  author   = "P. J. Cohen",
  title    = "The independence of the continuum hypothesis",
  journal  = "Proceedings of the National Academy of Sciences",
  year     = 1963,
  volume   = "50",
  number   = "6",
  pages    = "1143--1148",
}
```

- 文字省略号的一种实现方式

```CSS
.text-ellipsis {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 60%;
}
```

## 0215

- 编辑器设置选项分类 功能设计
  - 编辑器样式
    - 字体、大小、宽度
    - toc目录样式
    - 折叠图片、列表
  - 编辑器功能特性
    - fork/创建副本、分支
    - 历史版本
    - 拼写检查
    - 离线
    - 图片编辑器
    - 查找替换
    - 文档信息统计
  - 导入、导出
    - 导出/下载
  - 分享、权限
    - 只读、可编辑
    - 分享链接、二维码、微信
    - 分享管理
  - 产品功能特性
    - 收藏
    - 分享
    - 删除
    - 保存为模板
    - 回收站
    - 集成到slack
    - 文档更新提醒
    - 关闭评论
    - 翻译
    - 举报

## 0213

- 让dom中id为`#id001`的元素滚动到页面顶端的方法 (如toc点击跳转)
  - `$('#fixed-tabs').scrollIntoView({ block: 'start', behavior: 'smooth' })`

## 0211

- bug修复
  - [ ] 修改store中的doc对象为docId
    - 等到闫东先实现请求文章id再实现此工作
  - 修改编辑器中代码字体 monospace  ->  'Courier New', monospace
  - 讨论
    - 要不要做退出登录
    - 要不要暂停修复编辑器bugs，开始实现分享功能
- react-router
  - 应该将PublicRoutes和PrivateRoutes分开，这样在public路由页面就不会发出用户数据请求

```JS
(await (await editor.db.getNamedDocument('global')).getDecodedContent()).getMap('recent-docs').get('lastDocument')
await (await editor.db.getNamedDocument('global')).getDecodedContent()
temp1.getMap('recent-docs').get('lastDocument')
temp1.getMap('recent-docs')
temp1.getMap('recent-docs').get('d')
temp1.getMap('recent-docs').set('d', 'id')
temp3.set('d', 'id')
temp3.get('d')
```

## 0210

- [First item from a Map on JavaScript ES2015](https://stackoverflow.com/questions/32373301)
  - console.log(m.entries().next().value); 
- 早期在 useUser(){} hook声明中放useEffect请求数据的缺陷
  - react创建虚拟dom树时，所有执行了useUser() 的组件都会触发http请求
  - 解决方案1: 拆分成2个hook
    - 抽象出一个单独的 useInitUser(){} hook，只执行请求初始化操作；
      - 在顶层组件(通常是Router组件)中获取到user对象后才渲染其他组件
      - 其他组件直接从useUser()中取user对象，而useUser中没有请求操作
- 测试添加bibtex的示例

```js
await editor.db.setReference({
  entry: 'article',
  author: 'Grishchenko, Victor',
  year: '2010',
  title: 'Deep hypertext with embedded revision control',
  journal: 'proceedings of the 6th International Symposium on Open Collaboration',
});
await editor.db.search({ tag: 'type:reference' });
```

- bug修复
  - [x] 移除文章页水平滚动条
  - [x] 去掉container 100vw 100vh
  - [x] 修复添加bibtex后刷新页面却显示为空的问题
- [Microsoft 提供的等宽 TrueType 字体](https://support.microsoft.com/zh-cn/topic/microsoft-%E6%8F%90%E4%BE%9B%E7%9A%84%E7%AD%89%E5%AE%BD-truetype-%E5%AD%97%E4%BD%93-93aa7a47-2149-be09-31a9-c22df598c952)
  - Microsoft 隨附的唯一 monospaced TrueType 字型是「宋體」（隨附于 Windows 3.1）和黑體（包含在 TrueType 字型套件中）。 Windows 3.1 隨附的所有其他 TrueType 字型，以及 TrueType 字型套件都是成比例字型。
  - Microsoft 附带的唯一等宽 TrueType 字体是 Microsoft 3.1 附带的 "宋体" 和 "宋体"，它包含在 TrueType 字体包中。 Windows 3.1 和 TrueType 字体包中包含的所有其他 TrueType 字体都是成比例字体。
  - The only monospaced TrueType fonts shipped by Microsoft are Courier New, which shipped with Windows 3.1, and Lucida Sans Typewriter, which was included in the TrueType Font Pack. All other TrueType fonts included with Windows 3.1 and the TrueType Font Pack are proportional fonts.

## 0209

- 设置调试逻辑
  - localstorage.debug = 'DocumentDB:*'
- [React.js with Factory Pattern ? Building Complex UI With Ease](https://dev.to/shadid12/react-js-with-factory-pattern-building-complex-ui-with-ease-1ojf)
  - 示例用的switch-case获取指定类型的组件，这些组件被memo过
- [React Hooks Factories](https://dev.to/pietmichal/react-hooks-factories-48bi)

```JS
// Alternatively, without classes
function getUser(name: string): User {
  return { name }
}
const user = getUser("Bob") // { name: "Bob" }
// Factory function that returns a new function that uses Hooks API.
function createHook(initialValue: string) {
  return function useHook() {
    return React.useState(initialValue)
  }
}
```

- [Conditionally render react components in cleaner way](https://dev.to/ms_yogii/conditionally-render-react-components-in-cleaner-way-1ik5)
  - 提出了enum 和 switch-case 2种方法并讨论，可以是Component或ReactElement(自带实参props)
  - enum-pros
    - 简单直观，直接从预定义对象中取组件
    - {roleSettings(username)[userRole]} 所有子组件都有username参数
    - {createElement(RoleSettings[userRole], { username })}
  - enum-cons
    - ~~对每个组件不方便传入定制参数~~
    - A downside of enum solution is all the component will be compiled even it doesn't need to rendered，但可解决
  - switch-case-pros
    - 选择组件自身也是一个组件，all in react
    - memo后方便优化性能
    - 扩展case方便
  - switch-case-cons
    - The long term cost of the switch/case in this scenario is higher. 
      - When you're wrapping different components inside a single component (which is the case for this component), is better to share props across them because they will be used in the same places, so ideally they should receive the same props
  - 不要直接写组件，可以先定义一个组件变量

## 0208

- react实现conditional rendering的3种模式
  - [Which is the react way of complex conditional rendering?](https://stackoverflow.com/questions/50901604)
  - 👍 `{ this.state.err ? <Err /> : <Main /> }` 数据驱动视图
  - 👎 `<div className="App"> {this.state.comp} </div>` state中不要存comp
    - `<div className="App"> {comp} </div>` 将comp提取成变量更好

## 0207

- 编辑器刷新时非常卡
  - 需要清理storage
  - 不能稳定复现
# dev-01

## 0126

- 下一步的工作计划
  - 重构文章页题头列表组件
  - 重构文章页的复杂组件

## 0125

- 🤔 通过双链创建新文档时，为什么在代码中可以打印出 `newDoc.getMetadata('metadata')` 的属性键值对，但在控制台打印出来却为空
  - 确定了问题出在文档数据库层
  - 原因是在执行 dbClient.set(newDoc) 后，其他地方触发执行了 dbClient.set(oldDoc)，很难排查
- 文档页工作需求
  - [x] 从本地数据库中读取文章参考文献列表
  - [x] fix types
  - [ ] 实现更多的参考文献样式 bibtex styles
- 检查parser是否具有isValid的方法
- 补充ts类型

## 0124

- latex的参考文献处理要考虑文中引用和文末条目
  - 文末条目默认是所有作者全部列出，且不使用作者缩写
- bibtex style的难点
  - 多个作者的分隔符可能是逗号，也可能不是逗号，and是人名还是分隔符

## 0121

- [ ] 封装bibtex的转换方法，默认转换方风格为plain

## 0120

- https://github.com/enric1994/bibtexonline
  - Convert your BibTeX bibliographies into text on the fly
  - 但字体用的是无衬线体，十分圆润
- https://github.com/bertobox/CSS-for-APA-Style-references
- [Citation Style Language vs. biblatex (vs. possibly other "citing-systems"?)](https://tex.stackexchange.com/questions/434946)
  - biblatex basically is a reimplementation and reinvention of the BibTeX way of creating bibliographies that had been with the TeX world since the late 1980ies
    - With BibTeX the `.bst` files written in their own reverse Polish notation language determine the output of the bibliography. 
    - BibTeX compiles all the information from the `.bib` file and outputs it to the `.bbl` in the expected format, LaTeX then simply imports the `.bbl` and typesets its contents. 
  - With biblatex on the other hand the formatting is done on the LaTeX side. 
  - CSL is an XML-based language for citation and bibliography styles. 
    - It aims to be a universal language that can be used by all kinds of reference managers and word processors. 
  - biblatex is basically LaTeX-only and CSL is supposed to be a universal standard.
- [Overleaf Bibtex bibliography styles](https://www.overleaf.com/learn/latex/Bibtex_bibliography_styles)
- 当title字段中间存在"\url"时会提示错误，原因是\会被理解为转义字符
  - 变通方法是将\url改为\\url
  - [\u in JavaScript String.raw`template literal`](https://stackoverflow.com/questions/39310685)
    - replacing the line with `\u005Cusepackage{indentfirst}`, or even just `\x5Cusepackage{indentfirst}`.
      - `5C` corresponds with `\`.
    - Another option might be using the dollar sign and curly braces notation for expressions. `${'\\'}usepackage{indentfirst}`
- [overleaf中关于引用website的处理](https://www.overleaf.com/learn/latex/Bibliography_management_with_bibtex)
  - `@misc` is for whatever doesn’t quite fit any other entry type. 
  - not all bibliography styles support the `url` field: plain doesn’t, but IEEEtran does. All styles support `note`. 
  - It can be especially useful for web pages—by writing `note = \url{http://...}` or `url = {http://...}`
- A simple way of doing it in BibTeX is with a `@misc` entry
  - If you are using BibLaTeX there is an `@online` entry type
- [Generate BibTeX entry from URL](https://www.reddit.com/r/LaTeX/comments/q85jo1/generate_bibtex_entry_from_url/)
  - https://karlosos.github.io/url_to_bibtex/

```bibtex
@misc{WinNT,
  title = {{MS Windows NT} Kernel Description},
  howpublished = {\url{http://web.archive.org/web/20080207010024/http://www.808multimedia.com/winnt/kernel.htm}},
  note = {Accessed: 2010-09-30}
}
@online{WinNT,
  author = {MultiMedia LLC},
  title = {{MS Windows NT} Kernel Description},
  year = 1999,
  url = {http://web.archive.org/web/20080207010024/http://www.808multimedia.com/winnt/kernel.htm},
  urldate = {2010-09-30}
}
@MISC{Anu:2013,
author = {Aggarwal, Anupama},
title = {This is how you cite a website in latex},
month = may,
year = {2013},
howpublished={\url{http://precog.iiitd.edu.in/people/anupama}}
}
\usepackage{url}
```

## 0119

- BibTexBook的类型需要添加title，editions改为edition
- BibTexMisc类型需要添加url
- 每个参考文献的元数据类型是否都要添加 `doi` 字段
  - 还有url字段
- 暂未实现，当一篇文章有多个作者时需要缩写，是在从数据库读取bibTex时实现，还是在渲染时实现
- 暂未实现，bibTex的tag值中可能含有`{}`包裹的变量，需要在读取元数据字段时解析，还是就设计为不支持
- [TS 3.1 - 高级类型总结](https://www.cnblogs.com/qq3279338858/p/14206569.html)

## 0118

- 参考文献的显示流程
  - 解析获取文章元数据的各个字段
  - 判断文章类型，选择最合适的文献显示组件
  - 参考文献组件根据文章元数据，渲染到dom
- [APA style Reference List: Basic Rules](https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/reference_list_basic_rules.html)
  - [Reference List: Articles in Periodicals](https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/reference_list_articles_in_periodicals.html)
  - [Reference List: Books](https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/reference_list_books.html)
- [How to Cite in APA Format (7th edition) | Guide & Generator](https://www.scribbr.com/category/apa-style/)
  - components of a reference entry
  - 1. author
    - 一作，多个作者，合作者，通讯作者，联合@
  - 2. date
    - 年、年月日、未发布、未知日期
  - 3. title
    - 文章网页用普通文字、书籍用斜体、未知来源用方括号
  - 4. source
    - 期刊、出版社、网站、地址
  - prefix
    - doi
    - Use the prefix field in situations like see also or i.e..
- [How to Create an APA Style Appendix | Format & Examples](https://www.scribbr.com/apa-style/appendices/)
  - 附录可以放图片、表格、伪代码、名词解释

## 0117

- 参考文献暂不支持手动输入
- latex入门
  - [LaTeX入门指南|新手速进](https://www.zhihu.com/zvideo/1421078748670566400)
- [在arXiv下载论文的LaTeX源码](https://www.jianshu.com/p/b8baca4bfc20)
  - 找到一篇arXiv论文的版面，点击Download中的Other formats；
  - 点击Source目录下的：Download source；
  - 改名为：.zip， .tar.gz等的尾缀，然后解压缩此文件；
  - 打开tex主文件，编译成PDF；
- 闫东沟通
  - workspace的操作接口写了哪些
  - 向workspace中添加手机号或邮箱时，该用户登录后会自动拥有workspace的权限
- 搜索ui的设计
  - cmd+k调出位置固定的弹窗，类似docusaurus、notion
    - 弹窗空间较多，可显示详细条目及信息
  - 下拉菜单，类似github
    - 可切换全局搜索、仓库内搜索、org内搜索
- [flexsearch](https://github.com/nextapps-de/flexsearch)
  - Next-Generation full text search library for Browser and Node.js
  - fastest and most memory-flexible full-text search library with zero dependencies.
  - `Document` is multi-field index which can store complex JSON documents (could also exist of worker indexes).
- https://github.com/timc1/kbar
  - https://kbar.vercel.app/
  - Command+k interfaces are used to create a web experience where any type of action users would be able to do via clicking can be done through a command menu.
  - With macOS's Spotlight and Linear's command+k experience in mind, kbar aims to be a simple abstraction to add a fast and extensible command+k menu to your site.

## 0112

- 完善/docs
  - [x] 图片保存到本地数据库 迁移到 toe-frontend
  - [ ] 文档内搜索
- 实现/user
  - 最近文档列表
  - 搜索用户数据
- 实现/workspace
  - 输入关键字搜索出匹配文档名或内容的文档
  - [ ] 选中一篇文档后，所有行的复选框都应该显示
  - 全局header

## 0111

- 实现所有文档列表组件时，要考虑在以后实现回收站文档列表时方便复用
  - 不支持文件夹的设计，大大简化了文件列表的实现难度
- 实现列表一行的悬浮菜单花费了大量时间
  - 原因是查看mui的Popover文档示例时，看漏了一行触发条件
    - const open = Boolean(anchorEl);
    - const id = open ? 'simple-popover' : undefined;

## 0109

- 登录后无法访问登录页，需要实现退出登录的逻辑
- react custom hook函数不需要有返回值
  - useEffect可以有返回值，也可以没有
- [useFetch: Building custom hooks in React to fetch Data](https://dev.to/shaedrizwan/building-custom-hooks-in-react-to-fetch-data-4ig6)
- [How to extract React component logic into a custom Hook](https://www.benmvp.com/blog/how-to-extract-react-component-logic-custom-hook/)
  - Most of the time I write the “messy” logic in the component first and then extract it into a custom Hook. 
  - But sometimes I am able to “see in the future” and build the custom Hook first and “magically” have the data ready in the component.
- [what is the difference between using useEffect inside a custom hook and a component](https://stackoverflow.com/questions/62329615)
  - The `useEffect` function inside custom hook will only run when you use it inside a functional component and invoke it. 
  - Also note that the behavior of `useEffect` will remain exactly the same as if it were written inside the functional component itself

## 0108

- 路由未解决的问题
  - 刷新页面能保持原页面状态的问题，路由是不变的
  - 示例MentorLabs给出的解决方案是，在 if (!isAuthenticated) 前有一个前置判断  if ( status === 'pending'){ show loading } 
    - 首次请求用户数据pending时，会显示加载组件；
    - 注意当用户数据请求完成后，isUserAuthenticated会变成true，下一个if也不会执行了
- 注意更新user状态的顺序，前面会先执行，错误顺序会匹配执行错误的if分支
  - 先 setUserInfo(userInfo); 
  - 后 setUserStatus('resolved'); 
- [React batch updates for multiple setState() calls inside useEffect hook](https://stackoverflow.com/questions/56885037)
  - on next major release (probably v17) React will batch everywhere by default.

## 0107

- routing难点
  - 登录用户刷新页面时，会闪过明显的登录窗口
    - 可以使用useNavigate()在合适的时机命令式执行跳转，而不是使用`<Navigate>`声明式每次都会跳转
- 刷新页面保持用户登录状态的方法
  - https://github.com/adarshaacharya/MentorLabs/blob/main/client/src/App.tsx

## 0106

- 区分3种路由
  - RoutePrivate 未登录不可访问，登录后才可访问
  - RouteUnauthorizedOnly 未登录可访问，登录后不可访问，会自动跳转到指定路由
  - 默认public 未登录可访问，登录后可访问

## 0104

- 图片保存本地数据库仍然存在的问题
  - 不显示dataReference属性的原因，在上传图片addRef后，不能  await dbClient.set(articleDbDoc); 
  - Failed to execute 'createObjectURL' on 'URL': Overload resolution failed
    - 不能稳定复现
- 🤔 复现调试图片刷新时，突然编辑器不见了
  - 🔈 变通的方案是在wsl的linux下复现bug，竟然能顺利执行，没有bug
  - 注意wsl的4001端口会被windows的4001端口屏蔽掉，要检查端口是否相同
    - ⚠ 开发环境必须以linux为主，在windows vscode中打开linux下的源码
  - TypeError: Cannot read properties of null (reading 'getAttribute')
  - at IconView._updateXMLContent (iconview.js:100)
  - https://github.com/ckeditor/ckeditor5/issues/10927
    - Most probably, the file-loader handles CKEditor 5 icons. You need to exclude CKEditor 5 assets from this loader. But it's hard to say more as we don't see the full webpack config.
  - Cannot read property 'getAttribute' of null in react
    - it seems there's something wrong with your webpack configuration
