---
title: web-ui-comp-catalog
tags: [components]
favorited: true
created: 2020-08-09T05:13:36.363Z
modified: 2021-04-11T17:38:29.829Z
---

# web-ui-comp-catalog

# guide

# ui-design-choices
- 常用组件比较
  - button, card
  - checkbox, dropdown-list
  - accordion, modal/dialog

# ux-experts-designers

- Angel Uriostegui
  - https://github.com/anguriostegui
  - https://twitter.com/anguriostegui
  - https://angel-seven.vercel.app/
  - https://woonders.vercel.app/
  - https://powerkit.app/
  - https://heros-rouge.vercel.app/
# component-api-design
- awesome-list
  - https://open-ui.org/analysis/component-matrix
  - [Material-UI API Design Approach](https://next.material-ui.com/guides/api/)
  - [react-native Core Components and APIs](https://reactnative.dev/docs/components-and-apis)
    - [react-native-web](https://necolas.github.io/react-native-web/docs/)
    - [react-native-aria](https://geekyants.github.io/react-native-aria/docs/)

- more-comp-libs
  - https://www.npmtrends.com/@material-ui/core-vs-antd-vs-react-bootstrap
  - https://ant.design/components/button-cn/
# general 
- Button
  - gradient
- Image
  - 可刮奖擦拭的图片，可做个人头像
  - ImagePlaceholder: 使用unsplash的随机图片作为背景图
- Headline
  - animated

- Box
  - flexible one-off component that can live outside the design system constraints
# foundation
- 大多数组件通用的非dom元素或操作

- component-theme
- animation
- drag
- resize
- layer
  - 考虑：portal的target容器默认是组件自身或document.body
- typing
  - 文字逐个打出
  - 在文字较多时，自动换行；多到占满容器时，自动缩小
# layout
- Flex
- Box vs Container vs Grid

 

  - https://spectrum.chat/material-ui/help/grid-vs-box-and-now-vs-container~73cef09f-1eb9-4d0f-a3a3-d46c44232524
# navigation
- FloatingActionButton
- ## Sidebar
  - variant: window-manager
    - 可显示或隐藏侧边栏的容器组件
- Divider
  - 空白样式的组件可代替Spacer空行
- NavBar
  - 下滑时显示，上滑时隐藏
# input
- ## InputText
- 公式输入
- as form control

- ## checkbox
- props
- props-discuss
  - checkgroup
    - maxSelectCount
- ref
  - [ `<input type="checkbox">` ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)
    - indeterminate: A Boolean which, if present, indicates that the value of the checkbox is indeterminate rather than true or false

- ## Form
- 难点
  - 布局
  - 双向绑定
  - 错误收集 & 检验显示
  - 编辑流畅
  - 联动
- 参考
  - [alibaba-formily](https://github.com/alibaba/formily)

- ## Dropdown/Select
  - 单选
  - 手动关闭
  - 超过10个项目可显示下拉列表滚动条，超过20个项目可显示弹出菜单选择器，超过100个提示不推荐使用
  - variant: ScalableDropdown
    - 选项少时显示下拉列表，选项多时显示modal
- ComboBox
  - 可输入选择(自动完成)，可选择多个
- Toggle

- ## Search
  - [appbaseio/reactivesearch](https://github.com/appbaseio/reactivesearch)
  - 搜索结果预览，类似豆瓣输入后
# display
- ## Collapse/Accordion
  - 默认显示前N个字符串，也可显示设置内容，点击会切换展开与折叠状态
  - 内容显示为可折叠的card，或者显示为浮动的modal()

- ### html details/summary cons
  - 使用场景
    - 可能只适合用来折叠与展开文字内容
    - 和accordion不一样
    - dev.to用来实现折叠评论
  - 待解决的问题
    - 不支持自定义切换动画
    - 不支持创建链接到details内部元素的url
    - 不直接支持find in page
    - 多层嵌套折叠，内外层元素的通信，如tooltip
    - 各浏览器实现不一样，外观也不一致
  - 不适合将state作为单一数据源的框架，但可实现为受控组件
  - ie都不支持
  - there's no built-in way to animate the transition between open and closed.
  - `<details>` element supports the toggle event
    - It is sent after the state is changed, although if the state changes multiple times before the browser can dispatch the event, the events are coalesced so that only one is sent.
- collapsible text
- collapsible banner

- ## Card

- CodeCard
  - 显示源码的卡片，类似源码截图，左上角有类似macOS的三点菜单
  - examples

- PinnableCard
  - 类似支付宝首页可固定的菜单

- examples-usecases
  - [Every repo, issue, commit, etc will get a generated card like it.](https://twitter.com/JasonEtco/status/1380194813140725761)

- ## tabs
- eg-preview
  - https://gui-challenges.web.app/tabs/dist/
    - 可通过移动水平滚动条来自动切换tab

- ## List
  - collapsible
  - 评分表情包
- ## Grid
- ## Tree
- Timeline
- DiffViewer
- Comparator
# feedback
- ## Modal/Dialog/弹出窗口对话框

- 一般情况，模态框和遮罩总是作为在body下的第一层子节点出现
  - 因为如果很深层次的子孙组件触发模态框，而使得该组件内的模态框组件层级较深
  - 根据z-index的规则，这样的情况很难完成模态框凌驾于页面整体而出现的，遮罩也无法覆盖整个页面
- 支持同时显示多个modal
  - 类似地图上显示多个poi的overlay信息
  - modal下层无mask
  - modal不重叠，若重叠，则先显示的在下层
- modal嵌套
  - 如modal重视form，点击form的field会再弹出modal来选择
- 关闭modal是否应该移除该modal原本挂载的目标节点呢
  - 此处的目标节点是指 `ReactDOM.unstable_renderSubtreeIntoContainer(this, component, containerNode)` 中的 containerNode
  - react-modal (Basic Example) 关闭modal后，目标节点保持、不移除
    - 可以在body元素上动态添加和删除弹窗是否打开的属性
  - react-bootstrap中的modal对目标节点，关闭modal后即移除
- modal状态恢复
  - 如关闭弹窗查找信息，再恢复弹窗继续填写
  - modal变成悬浮按钮fab
- 显示和隐藏的动画
  - 如果根节点删除，动画不好处理。根节点不删除，还是有动画方面的考虑复用根节点也麻烦
  - 隐藏弹窗时，先执行动画，再unmount弹窗组件

- usecase
  - 弹出菜单
  - user guide tour
- modal的位置
  - 一般情况，模态框和遮罩总是作为在body下的第一层子节点出现
  - 因为如果很深层次的子孙组件触发模态框，而使得该组件内的模态框组件层级较深
  - 根据z-index的规则，这样的情况很难完成模态框凌驾于页面整体而出现的，遮罩也无法覆盖整个页面
- 支持同时显示多个modal
  - 类似地图上显示多个poi的overlay信息
  - modal下层无mask
  - modal不重叠，若重叠，则先显示的在下层
- modal的开闭控制，放在props还是state
  - 示例多放在state
  - antd
- modal嵌套后的数据传递
  - 如modal重视form，点击form的field会再弹出modal来选择，点击下层弹层组件，可关闭上一层弹层，点击mask，可关闭所有
  - 弹层组件在react DOM树中的位置跟它们实际的层次以及包含关系是没有必然联系的，如果两个弹层是body下面的两个兄弟节点，但从弹层的使用角度看它们是有层次关系的，并不是并列的
- 弹层的层次关系数据是多叉树的结构
- 关闭modal是否应该移除该modal原本挂载的目标节点呢
  - 此处的目标节点是指 `ReactDOM.unstable_renderSubtreeIntoContainer(this, component, containerNode)` 中的containerNode
  - react-modal(Basic Example)关闭modal后，目标节点保持、不移除
    - 可以在body元素上动态添加和删除弹窗是否打开的属性
  - react-bootstrap中的modal对目标节点，关闭modal后即移除
  - 如果根节点删除，动画不好处理。根节点不删除，还是有动画方面的考虑复用根节点也麻烦
  - 隐藏弹窗时，先执行动画，再unmount弹窗组件
- modal状态恢复
  - 如关闭弹窗查找信息，再恢复弹窗继续填写
- modal变成悬浮按钮fab
  - 显示和隐藏的动画
- ref
  - [有赞：多层嵌套弹层组件](https://juejin.im/post/59a02c38518825244b068486)
    - 嵌套modal的结构
  - [一步一步带你封装基于react的modal组件](https://juejin.im/post/5ba5ab61e51d450e9162c4ae)
    - 进出场动画
  - [React模态框秘密和“轮子”渐进设计](https://zhuanlan.zhihu.com/p/30271961)
    - modal的位置应该放在body下的第一层、传递context到modal
  - [React实现动态调用的弹框组件](https://blog.csdn.net/qq_35757537/article/details/90322144)
    - 直接在组件外调用组件内的自定义方法传入自定义参数，来改变触发组件状态改变的setState
  - http://limoer.cc/2019/12/19/global-component/
    - 在不暴露组件实例对象的前提下，暴露修改组件内部状态的方法， `ReactDOM.render(element, container[, callback])`
    - the preferred solution is to attach a callback ref to the root element.
    - 通过高阶方法，提前在callback ref方法中调用参数方法，并传入可修改state的方法的对象
  - [React造轮系列：对话框组件 - Dialog思路](https://juejin.im/post/5cea293ef265da1bc07e15cc)
    - 通过 `ReactDOM.render` 直接实现 `<button onClick={() => alert('1')}>alert</button>`
    - 在onClick方法内直接关闭modal，通过React.cloneElement传入 `{visible: false}`
    - 还可以在ReactDOM.render完成后，返回一个包含操作modal状态方法的对象
  - [用react做一个跟随组件的 tooltip](https://zhuanlan.zhihu.com/p/143093317)
  - [侧边栏设计](https://zhuanlan.zhihu.com/p/28465951)

- ready-modal
  - chatting-modal
    - 用于在线客服咨询的聊天窗口

- ## sidebar

- usecase
  - dockable
  - 多个sidebar
  - 非边缘的容器上，效果类似sidebar的组件
- 兼容移动浏览器
  - 移动端浏览器，向上滑时会隐藏上面的url地址栏和下面的导航菜单，来增大显示空间
  - When viewing a web page on a smartphone browser, the browser will typically remove the URL and menu bars from the screen when the user scrolls down the page.
  - For some reason react-sidebar breaks this behavior, leaving the browser UI in place even when the page is scrolled.
  - Mobile Chrome's autohide works by listening for scroll events on the body element. 
    - As far as I can see this plugin wraps your whole app in an absolutely positioned div with an `overflow-y: auto`
    - as a result, scroll events never trigger on body and the browser chrome does not get hidden. 
- multi-sidebar: 使用多个sidebar用于导航
  - https://github.com/balloob/react-sidebar/issues/65
  - 多个sidebar的效果也可以考虑用多个window来实现

- ## Popover/Tooltip/弹出气泡
- 要点
  - 触发方式：点击、鼠标移入、获取焦点的文本框
  - 气泡位置：中间或上下左右，箭头或三角形
  - 弹层显示控制：第几层、覆盖情况、弹层控制、元素操作
- ref
  - [popperjs: Why not use pure CSS](https://github.com/popperjs/popper-core)
    - CSS tooltips will not be prevented from overflowing clipping boundaries, such as the viewport. 
      - The tooltip gets partially cut off or overflows if it's near the edge since there is no dynamic positioning logic.
    - CSS tooltips will not flip to a different placement to fit better in view if necessary.
      - Popovers containing interactive HTML are difficult or not possible to create without UX issues using pure CSS. 
      - Popperjs positions any HTML element – no pseudo-elements are used.
    - CSS tooltips cannot follow the mouse cursor or be used as a context menu.
    - CSS tooltips cannot be easily extended to fit any arbitrary use case you may need to adjust for. 
      - Popper is built with extensibility in mind.
  - [Tether](https://github.com/shipshapecode/tether) is a small js lib for defining and managing the position of UI elements 
- FloatingActionButton
- Toast
- Loading
  - flower-loader
  - 类似文字从左到右一次变色的动画，如ktv歌词，如https://vaadin.com/components

- ## Skeleton 骨架屏
  - bg-image-color
  - [一种自动化生成骨架屏的方案](https://github.com/Jocs/jocs.github.io/issues/22)
- BulletComment/弹幕

- ## alert/callout
# experimental
- table-of-contents
  - 内容显示为可折叠的card，或者显示为浮动的modal()
# ui-components-catalog
- 组件类别summary
  - 作为单独库实现的组件
    - list
    - tree
    - chart
    - map
    - editor
  - 组件类别数:8
    1. general：常作为创建业务组件的基础组件，如Box、Link
      - primitive：只替代html标签，如H1、Image、Button
    2. foundation：不直接提供ui视图的组件
      - Draggable
      - Resizable
      - animation
      - layer
    3. layout：布局类组件
      - 如Row、Column
    4. navigation：导航类组件
      - 如Menu
    5. input：数据输入类组件，表单组件
    6. display：展示类组件
    7. feedback：反馈通知信息类组件
    8. experimental：实验新组件，也为experimental,addon,extension
- general/通用组件
  - button
  - icon
  - label
- layout/布局组件
  - container
  - box
  - grid
  - grid-list
  - column
  - row
  - divider
- navigation/导航组件
  - affix/固钉：将页面元素钉在可视范围
  - breadcrumb
  - dropdown
  - menu
  - pagination
  - pagehelper
  - steps
  - floating-action-menu
  - page-header
  - drawer/sidebar
  - anchor
  - back-top
- input/数据输入组件
  - auto-complete
  - checkbox
  - cascader
  - color-picker
  - date-picker
  - input-number
  - input
  - search
  - mentions
  - rate
  - radio
  - toggle/switch
  - slider
  - select
  - tree-select
  - transfer 穿梭窗：A列表窗口的项目加入B列表窗口
  - time-picker
  - uploader
  - form 表单
- display/数据展示组件
  - Link 文字链接
  - avatar
  - badge
  - comment
  - collapse
  - carousel
  - card
  - calendar
  - chip
  - list
  - tree
  - timeline
  - tag
  - tabs
  - table
  - image
  - infinite-scroll
- feedback/反馈通知组件
  - alert
  - loading
  - modal
  - message
  - notification
  - progress-bar/circle
  - spinner
  - skeleton
  - dialog
  - popover
  - toast
  - tooltip
  - snackbar
  - captcha
  - countdown
  - qrcode
- experimental/incubator
  - jumbotron
    - extend the entire viewport to showcase key content
  - hero component:image preloading fade-in effect, a semi-transparent color overlay 
  - embeddable-widget
  - url-viewer: card形式、tab形式，类似无标题栏的浏览器
  - color-palette
  - lucky-draw/抽奖转盘
  - bullet-comments
  - 图章：如封禁
  - subtle-ui: tab notification
  - link-image: 文字链接有时太单调，内容预览可信度更高
  - CodeCard
  - AnimationPlayer
    - 类似视频播放器，点击播放动画，动画元素主要是图标，播放效果类似视频
- integrated/connected/联系第三方应用的组件
  - douban-movie-card
  - github
    - repo-card
    - made-with-love
  - sharing-to-weibo/wx/twitter/datalking
  - unsplash-image-card
- data-oriented
  - TopN
  - AlphabeticalMenu
    - 类似win10开始菜单的首字母排序
