---
favorited: true
tags: [components, web]
title: note-ui-components
created: '2019-09-07T13:04:41.983Z'
modified: '2020-04-20T11:43:33.773Z'
---

# note-ui-components

## latest
- 组件开发方向
    - 跨框架开发ui组件库(stencil) https://zhuanlan.zhihu.com/p/41974042

## back-garden-ui-in-action
- logo: green plum
- design-system-tokens
    - text: sans serif(衬线体多用于印刷)
    - color: mineral-ui-color-palette, primary-mediumseagreen-like
    - bezel-less
- interaction
    - hover-color
    - click-ripple
    - loader-flower
- animation
    - rotate
    - unfold
    - point movement
- shape
    - point/polygon-shape-based
    - https://medium.com/google-design/you-need-a-shape-system-8d2aa9016817

## react-dev-in-action
- dev-faq
    - 生成色板后，给各色值定义了类似blue900的名称，各组件如何使用相关颜色
        - 对于不需改变的或很少变化的颜色，直接写，对于用户可控制的颜色放到组件props中
            - 不必像bulma-styled-components那样抽象出所有变量，如边框色、宽度等
- styled-components
    - 多采用styled写法
    - 很少采用css prop写法
- styled-system
    - 可直接用所需的style prop function，也可用大类分组，还可自定义
    - 更多用在底层基础组件，可以不必大量用在上层组件，如w-design 
- theme
    - 推荐使用`@styled-system/css`的css方法，直接写theme.js主题对象中的值
        - 使用 style object，而不是字符串DSL
        - 优点是可以使用consistent的样式值，同时查看更直观，因为不是变量
        - 缺点是引入了css方法的依赖，只支持style object形式的写法
    - 通过props.theme.propName获取样式值，一般很冗长，且查看不直观
        - w-design,looker
    - 自己封装类似themeGet()方法取值，使用方法取值可避免对props.theme的ts类型检查
        - flame
        - https://twitter.com/iamsapegin/status/1136317690149330944
        - themeGet是封装类似style prop function的教程
    - 直接import theme.js然后使用
        - smores-react,everblue-ui
- 组件形式
    - 多采用function component( + hooks)
    - 仍以class组件为主的：zent,rsuite,uiw,typeui   
    - 以单文件的形式创建组件，如flame、cactus、radix
    - 少部分组件库导出组件时，最外层是styled包裹的，如primer、priceline
- 类型写法
    - 不使用react提供的propTypes，使用ts
    - 提取出公共type，如knitui
- 样式写法
    - 大多采用string template literals的写法
    - 很少采用style object的写法: minerva-ui
    - 静态样式可以使用className，若要使用theme中的样式值则用内联的写法更好
    - 尽可能拆分组件而不是分离样式，也可以类似Card.tsx, Card.style.tsx分离复杂样式
        - grommet将样式写在StyledButton，然后Button使用了它，主题样式值冗长
        - w-design,knack-ux,Amsterdam-s-c
- defaultProps默认值的写法  
    - 推荐:直接在函数的参数处指定，如`const C = function(p1='1',p2...){}`   
        - polaris-react,om,kenobi,knitui,smores-react,axiomatic
        - flame,w-design
        - 为避免实参对象每次render都重新创建，可考虑在函数外创建复杂对象再赋值到内部
    - 在组件定义之外指定，如`Button.defaultProps={}`, to be deprecated
        - eact-atomicus，Amsterdam-s-c,cactus,everblue-ui
        - flame，looker,prestyled,priceline,primer,pulse
    - 参数写props，方法体中`const {p1='1',p2=false,...restProps}=props;` 
        - w-design,eui,minerva-ui,xl-vision,knitui,snake-design      
    - ref作为单独的参数，方便forwardRef
        - polaris-react，react-ui-components，snake-design,xl-vision
        - knitui,flame
    - props中**可分离**出去的参数
        - ref, children, className, theme
- 使用Box作为基础组件
    - chakra-ui,falme,w-design,rbx,rebass,axiomatic,marozzo-ui,prestyled
 - 使用Flex组件
    - flame,w-design    
- 组件结构写法
    - 分类采用atom+molecule+organism
        - primer-core-concepts,axiomatic,react-components,pulse
    - 一组参数采用variant属性控制，如type,size，不建议使用variant作为属性名
    - 在render方法中，调用renderComp()来生成子元素
- design-tokens作为单独的库
    - flame-tokens:text,color,spacing,border,shadow,transition
        - 使用了pxToRem
        - baseTheme对象放在token包，variant对象放在component
    - looker：theme.js放在token包
    - mineral-ui
- test
    - flame：Button.test.tsx,Button.stories.tsx,README.md
    - w-design:`__snapshots__`文件夹，所有组件文档放在一起放在单独项目
        - 基于@mdx-js/loader
    - looker:`__snapshots__`文件夹和Button.test.tsx，文档单独项目
        - 基于gatsby和gatsby-plugin-mdx
    - cactus:Button.test.tsx,Button.storybook.tsx,Button.mdx + gatsby
    - snake-design：`__tests__`文件夹，所有组件文档放在一起放在单独项目
        - 基于markdown-it
    - kenobi:tests文件夹，stories文件夹 + docz
- documentation
    - storybook+mdx
        - storybook缺少实时编辑实时显示的功能，可配合使用react-live
        - stories的顺序，顶层目录的顺序，修改不够灵活
    - docz,styleguidist
    - snake-design: 基于markdown-it自定义babel-loader处理md文件的逻辑
    - 基于md的文档里面的组件很难注释掉(现已有非正式标准)，不方便快速切换显示隐藏组件
    - 需求是编写组件文档的mdx后，既可以在storybook里面使用，也可在单独项目使用
        - 同一个mdx，若不修改，很难在sb和单独项目同时渲染正常，import路径有问题
        - 推荐：以sb正常显示csf story为主，若要在单独项目中使用，可通过手动读取代码并修改import路径来调整，考虑到Button.stories.mdx中依赖story组件太多
        - 在单独的项目中使用类似Button.docs.mdx时，可统一修改`import Button from './Button';`的导入路径
        - 文档中代码过多时，可将代码放在单独mdx文件或文件夹中，提高可读性(zent,rbx)
    - 文档要考虑**国际化**，直接使用storybook很难实现多语言，参考ant-design,zent
        - 推荐自己实现文档网站，可控度最高，体验最好，难点包括多语言、多版本
- 将需要的组件或功能是放在单独的folder，还是单独的package，还是单独的project
    - 个人项目开发采用monorepo，多个project需要更多的时间精力
    - 分类不同的组件或功能放在不同folder，如Box，Modal
    - *重要*的组件或功能*可以*放在单独的package，如table，aniamation
    - 需要单独考虑的包括
        - i18n/locale
        - theme
        - css
        - icon
        - animation
        - drag/resize
        - starter template with common necessities like hooks,context,hoc
    - 参考项目：cactus,Amsterdam,vital-ui-kit-react
- 可以用rem作为单位的组件(即与设备宽度相关的)
    - modal
    - pxToRem `16px = 1rem`
- component-ecosystem
    - starter-boilerplate
    - todo-app
    - admin-dashboard
    - doc-site-generator(component-preview)
    - theme-designer(grommet/UI Fabric Theme Designer)
    - ui-designer(grommet/blocks)
    - components-showcase(m-design-components-showcase/flutter_catalog)
- 组件库开发总结
    - 开发组件库的原因
        - 避免重复造轮子和写过多重复代码
        - 自己处理代码与文档的一致性
    - 组件分类
        - primitive元组件：代替html标签元素，如h1,span,flex
        - general/basic基础组件：常用来合成其他组件,如button,input,image
        - 公共组件：各项目通用组件，如modal,toast,toggle
        - 业务组件:一般直接用在业务代码中的较复杂的组件，如抽奖转盘
    - 业务开发
        - 产品经理抽象业务场景和业务逻辑 + 设计师设计ui规范 + 开发者实现交互逻辑
        - 既要有造轮子的能力（个人），也要有不造轮子的觉悟（团队）
        - 最好提供 cjs/esm/umd 等三种形式的模块供不同使用情景使用
    - ref
        - https://jxnblk.com/blog/patterns-for-style-composition-in-react/
- tips
    - 为了tree-shaking和明确语义，只使用named import/export，同时支持default
        - 不使用dynamic import，不方便tree-shaking
        - esm3种import:named,namespace,default
        - esm2种export:named,default
        - commonjs/cjs1种import和export: require, module.exports
        - antd开发了专用babel插件将import转换成多个named import
 
## general 
- Button
    - gradient
- Image
    - 可刮奖擦拭的图片，可做个人头像
    - ImagePlaceholder: 使用unsplash的随机图片作为背景图
- Headline
    - animated

## layout
- Flex
- Box vs Container vs Grid
    - https://spectrum.chat/styled-system/general/whats-in-your-box~6f41c990-f49f-4063-ba64-fcea702014f9
    - https://spectrum.chat/material-ui/help/grid-vs-box-and-now-vs-container~73cef09f-1eb9-4d0f-a3a3-d46c44232524
    
## navigation
- FloatingActionButton
- Sidebar
- Divider
    - 空白样式的组件可代替Spacer空行

## input
- Input
    - 公式输入
    - as form control
- Dropdown/Select
    - 单选
    - 手动关闭
    - 超过10个项目可显示下拉列表滚动条，超过20个项目可显示弹出菜单选择器，超过100个提示不推荐使用
- ComboBox
    - 可输入选择(自动完成)，可选择多个
- Toggle

## display
- Collapse: 默认显示前16个字符串，也可显示单独设置的，点击时展开显示原内容
- Card
- PinnableCard: 类似支付宝首页可固定的菜单
- List
    - collapsible
    - 评分表情包
- Grid
- Tree
- Timeline
- DiffViewer
- Comparator

## feedback
- Popover/Tooltip/弹出气泡
    - 要点
        - 触发方式：点击、鼠标移入、获取焦点的文本框
        - 气泡位置：中间或上下左右，箭头或三角形
        - 弹层显示控制：第几层、覆盖情况、弹层控制、元素操作  
- Modal/Dialog/弹出窗口对话框
- Toast
- Loading
    - flower-loader
- Skeleton
    - bg-image-color
- BulletComment/弹幕

## ui-components-category
- summary
    - 移除other/misc/more的分类，语义模糊
    - 作为单独库实现的组件
        - list
        - tree
        - chart
        - map
    - 类别总数:8
        1. general：常用于创建业务组件的基础组件，如Box、Link
            - primitive：只替代html标签，如H1、Image、Button
        2. foundation：不直接提供ui视图的组件，如Draggable、Resizable
        3. layout：布局组件，如Row、Column
        4. navigation：导航组件，如Menu
        5. input：输入组件
        6. display：展示类组件
        7. feedback：反馈通知信息相关组件
        8. incubator：新组件实验
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
- feedback/反馈组件
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
- misc
    - jumbotron：extend the entire viewport to showcase key content
    - hero component:image preloading fade-in effect, a semi-transparent color overlay 
    - embeddable-widget
    - color-palette
    - lucky-draw/抽奖转盘
    - bullet-comments
    - 图章：如封禁
    - subtle-ui: tab notification
    - link-image:文字链接有时太单调，内容预览可信度更高
- connected/联系第三方应用的组件
    - douban-movie-card
    - github
        - repo-card
        - made-with-love
    - sharing-to-weibo/wx/twitter/datalking
    - unsplash-image-card
- dataset
    - TopN
- entertainment
    - AnimationPlayer: 类似视频播放器，点击播放动画，动画元素主要是图标，播放效果类似视频

