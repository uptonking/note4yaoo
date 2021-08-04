---
title: pm-ux-dashboard-admin
tags: [antd, dashboard, pm, ux]
created: '2021-07-27T09:07:57.334Z'
modified: '2021-07-27T09:09:48.459Z'
---

# pm-ux-dashboard-admin

# guide

- usecase
  - 工作台、分析页、监控页
  - 表单、列表、详情、结果、异常

- tips
  - dashboard for knowledge base, or wiki spaces
  - sass场景模板可参考 vercel/commerce, async-labs/saas
# features
- core
  - theming
  - configurable panel
  - widgets/componnets: easy to drop in reusable components

- optional
  - tree-shaking: only include modules you need
# draft
- auth
- mock
- data viewer
- editor/builder/configurable
- mini app
# products-solutions
- 布局参考
  - black-dashboard右边面板依赖`reactstrap. Dropdown`组件
    - 主题切换基于document.body.classList.add/remove
    - 重度定制bootstrap.css，注意自定义css的顺序
  - xtream-dashboard左边折叠通过`[data-sidebartype='mini-sidebar']`选择器
    - 折叠侧边栏element.classList.add/remove("mini-sidebar")
    - 轻度定制bootstrap.css，只添加vars和组件css
  - airframe-dashboard左边折叠通过显示不同Sidebar Variants组件
    - Sidebar.HideSlim Only for Desktop
    - Sidebar.MobileFluid Only for Mobile
    - 重度定制bootstrap.css
    - 实现过于复杂

## [ant-design-pro](https://pro.ant.design/zh-CN/)

- features
  - 高效快速
  - 模板组件
  - 国际化
  - 预设样式
  - 最佳实践
  - TypeScript

- Ant Design Pro是基于 Ant Design 和 umi 的封装的一整套企业级中后台前端/设计解决方案，致力于在设计规范和基础组件的基础上，提炼出典型模板/业务组件/配套设计资源
  - Ant Design Pro 在力求提供开箱即用的开发体验，为此我们提供完整的脚手架，涉及页面布局、国际化i18n，权限，数据流，mock，网络请求等各个方面。

- [demo-preview](https://preview.pro.ant.design/dashboard/analysis)
  - 仪表板：工作台(动态流)、分析页、监控页
  - 列表页
  - 详情页
  - 表单页
  - 结果页
  - 个人页
  - 通知页、异常页
  - 图形编辑器

- umi插件
  - 权限、统计、antd、initial-state、layout、locale、model、request

- 添加图片，字体和文件
  - 为了加快加载速度，并且减少网络请求，我们会把小于 1000k 的转化为 base64，这一版只对图片有效。

## [vue-element-admin](https://panjiachen.gitee.io/vue-element-admin-site/zh/)

- features
  - 丰富功能
  - 最佳实践
  - 最新技术栈
  - 权限验证
  - 国际化
  - 主题换肤

- 本项目的定位是后台集成方案，不太适合当基础模板来进行二次开发。因为本项目集成了很多你可能用不到的功能，会造成不少的代码冗余。
  - 使用了最新的前端技术栈，内置了 i18 国际化解决方案，动态路由，权限验证，提炼了典型的业务模型，提供了丰富的功能组件，它可以帮助你快速搭建企业级中后台产品原型

- [demo-preview](https://panjiachen.github.io/vue-element-admin/#/dashboard)
  - 组件、图标、图表
  - 创建文章、文章列表
  - excel、pdf

## creative tim dashboards

- pro version
  - mini sidebar
  - more components
  - more plugins
  - more example pages
  - auth/login/signup pages
  - datatables
  - design assets: ps, sketch

### codebase

- code-xp
  - blackdashboard的scss插入到了bootstrap的scss的源码编译流程
  - 顶部AdminNavbar不可固定

- 最核心的界面布局是 AdminLayout
  - 左边Sidebar支持隐藏显示
  - 中间main-panel包括不可固定的AdminNavbar和与当前路由url对应的react组件
  - 右边FixedPlugin可配置样式主题，基于Dropdown实现
- 项目中样式主要使用className设置类名
  - 甚至主要使用reactstrap中的各种带样式的组件，不用自己实现状态管理、交互等逻辑
- dark mode通过在body.classList.add/remove样式类名实现

- 路由及其对应的组件通过类似json的js对象配置

## bootstrapdash dashboards

- pro version
  - dashboard variants
  - theming
  - layouts
  - tables
  - editor
  - maps
  - widgets
  - rtl
  - apps: kanban, todo, tickets, chats, email, calendar, gallery

## wrappixel dashboards

- pro version
  - dashboard variants
  - mini sidebar
  - settings floating panel
  - layouts
  - theming/dark
  - rtl
  - apps

### codebase

- todo
  - 添加折叠和展开左边侧边栏的按钮；
  - 目前监听window.width显示折叠按钮的逻辑有问题
    - 关闭控制台时，折叠过的左边栏不会自动展开

- code-xp
  - 顶部导航条左侧背景色与侧边栏背景色相同，让人误以为导航条在侧边栏，有好有坏
  - 动态样式不依赖classnames，而是通过`data-*`css属性选择器控制，如`[data-sidebartype='mini-sidebar']`选择器
  - 自定义样式都写在.scss文件里面

- 路由及其对应的组件通过类似json的js对象配置

## airframe-react

### codebase

- pros
  - 示例页面很丰富，比较符合文字展示的示例是projects、financial；与outline wiki样式接近
  - 侧边栏支持两级目录
  - 侧边栏内容过多时滚动条也不会显示
  - 整体布局完全自己基于css实现，不依赖reactstrap组件

- todo
  - 路由及其对应的组件手写指定，超过100行配置后显得很凌乱 

- code-xp
  - 左边侧边栏可折叠，侧边栏占据整页高度，导航条在侧边栏右边
  - 顶部导航条固定在顶部
  - 动态样式通过classnames拼接类名实现

- AppLayout指定了dashboard整体布局，从上到下依次是 
  - Navbar
  - Sidebar
  - Content
  - PageConfigConsumer 右侧是可勾选配置项的浮动sidebar
