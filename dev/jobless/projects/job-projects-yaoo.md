---
title: job-projects-yaoo
tags: [job, projects, yaoo]
created: 2021-09-21T19:45:54.152Z
modified: 2021-09-21T19:47:30.211Z
---

# job-projects-yaoo

# 项目中的难点

## 编辑器协作的设计与实现

- 数据模型
  - 使用tree存储数据，还是使用扁平map存储数据+关系，如何设计更好
- 冲突处理算法 crdt
- 同步流程
  - 两阶段同步减少传输体积

- 难点
  - 减少传输数据的体积

- 多维表格就算使用了数据库，仍然需要设计细粒度的缓存
## 长列表virtualized的实现，参考react-window

## 不同框架的数据通信方法

- 编辑器通知更新react组件，一般是更新props而不是state
  - 在编辑器的NodeView.update获取新数据, React.createPortal(), ReactDOM.render(), unstable
  - 还可以在上面的过程中封装一层，init时保存 {this.dom: elements}，update时将PMNode的新数据作为参数传给注册过的react封装setState的函数

- react组件通知编辑器
  - 直接通过编辑器的dispatch/updateState

- react NodeView如何通知其他NodeView
  - react state --> editor state 钩子更新 portals nodeView --> react state

- 2个问题
  - portal中自定义react组件子树非常多，还可能非常深 (react应用自身就是一颗巨大的vdom树)
  - 通信链路长的问题

## 当一个portal里面存在大量NodeViews，任何一个NodeView的rerender都会触发Portal组件的rerender

- 虽然最终commit阶段只会更新dom变化的部分，但render阶段Portal也存在React.createElement将所有子组件、标签的vdom重新计算一遍的过程

- 思路1: 最简单的，提取高频子组件到单独的portal，如popover、callout，缺点是需要额外添加Provider和PortalRenderer

- 思路2: 使用非受控组件+useRef手动更新dom，这些组件ui展示的数据保存在dom，不受react state/props控制，代码量变大了

- 思路atlaskit： 
  - 借助context传递EventEmitter，这样context的值不变，但EventEmitter中保存的值变化了，同时不会引起Context. Provider的所有子组件更新
  - 首次渲染使用createPortal，更新使用 unstable_renderSubtreeIntoContainer
  - 批量更新，需要更新的ReactNodeView会将自身的更新方法注册到portalProviderApi, 然后每次PortalProvider更新都会在componentDidUpdate里面更新

- once I was able to implement the rendering with React portals, I noticed my approach to be quite unusable when rendering large numbers of nodeviews. 
  - This was mainly due to how the rendering of the portals was done in one big loop that every update caused to re-render. 
- Atlassian solved by using `unstable_renderSubtreeIntoContainer`.

- 渲染的时机选择
  - 独立
  - 同时
  - 之后
# configurable-dashboard 仪表板
- goals
  - 简单易定制的仪表板/管理界面
- tasks
  - 布局
  - 路由配置
  - 登录状态、鉴权状态
- actions
  - bootstrap v4
  - react-router
  - rbac
- results
  - 实现了管理界面
  - 实现了全局数据流
  - 实现了路由鉴权
- 进一步的工作
  - 可复用的组件
  - 依赖升级
# materials-repo 资料库
- goals
  - 为离线优化的文档资料系统
- tasks
  - 网盘文件操作
  - 页面小程序创建
  - 文档浏览导航
  - 文档编辑
- actions
  - 基于仪表板模版实现了类似网盘的文件操作与管理系统
  - 基于动态加载实现了markdown文档转换成小程序
  - 基于prosemirror和rich-markdown-editor实现了文档在线浏览，支持滚动高亮当前编辑目录标题
- results
  - 网盘基本功能已实现
  - 任意文件夹可以资料小程序网站的形式打开
  - 文档浏览体验很方便，类似excel里面切换多张工作表
- 进一步的工作
  - 直接在前端请求网盘中sqlite单文件数据库中保存的数据，因为observable笔记本在推、geojson -> geopackage
  - markdown文档的解析目前很简陋，需要定制的front-matter，针对中文优化空格、字体等
  - 文档编辑需要提高性能
# prospect-garden-design
- goals
  - 可灵活复用的样式和组件
- tasks
  - css, 组件库
- actions
  - 基于style-dictionary实现了design tokens，定义了一系列的json对象，可输出各种格式
- results
  - 基于第三方css实现的设计系统不够标准、规范
- 进一步的工作
  - 不使用虽然的样式值，统一迁移到基于bootstrap的样式值和交互模式
# prosemirror-editor

# 系统设计

- 整理笔记时发现了我起草的 backend #面试流程，感觉还行，欢迎大家点评。
  * 提一个广度的问题判断面试者擅长哪个方面
  * 基础算法，时间空间复杂度
  * 针对特定语言的基础算法结构，数据类型
  * 框架针对性问题
  * IO，多线程
  * DB，缓存，消息队列
  * 测试流程
  * 系统设计

# didact: react-like library
- goals
- tasks
- actions
- results
