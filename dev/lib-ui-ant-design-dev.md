---
title: lib-ui-ant-design-dev
tags: [antd, lib]
created: '2020-06-15T10:25:37.356Z'
modified: '2020-12-08T13:22:47.564Z'
---

# lib-ui-ant-design-dev

# pieces

# changelog-ant-design

## [v4.0.0__20200228](https://ant.design/changelog-cn)

- v4依赖的React最低版本要求是React 16.9，提供更多的hooks
- 设计规范升级：将基础圆角由4px调整为2px
- 暗色主题
- 部分组件提供了一种新的无边框样式
- 引入了svg图标，支持tree shaking，打包体积更小
- 组件重写：Form, Table, DatePicker、 TimePicker 与 Calendar
- 性能优化
- 由于存在动画效果，自定义虚拟滚动并不方便
- 使用更符合React的动画
- 使用Less3.x
- 停止支持IE9/10，继续支持IE11

## [v3.0.0__20171204](https://github.com/ant-design/ant-design/blob/3.x-stable/CHANGELOG.zh-CN.md)

- 全面支持React 16
- 全新的色彩系统，组件主色由『#108EE9』改为『#1890FF』(『拂晓蓝』)
- 全新的视觉样式和组件尺寸，基础字体大小由12px增大到14px
- 新增组件：List, Divider
- 3.9引入svg图标

## [v2.0.0__20160928](https://github.com/ant-design/ant-design/blob/2.x-stable/CHANGELOG.zh-CN.md)

- 开发语言改为TypeScript，官方提供 .d.ts
- 时间类组件 DatePicker、TimePicker、Calendar 等的底层 使用 moment 替换 gregorian-calendar
- 新增组件：Mention, AutoComplete

## [v1.0.0__20160509](https://github.com/ant-design/ant-design/blob/1.x-stable/CHANGELOG.md)

- 兼容React@15.x
- 样式支持按需加载
- 新增组件：Card, Rate, LocaleProvider

## [v0.7.0__201500721](https://github.com/ant-design/ant-design/releases?after=0.10.1)

- 第一个公开版本
- 发布layout、iconfont、button、form、checkbox、radio、switch、slider、input-number、datepicker、select、tabs、steps、breadcrumb、collapse、pagination、modal、message、dropdown、popover、popconfirm、tooltip、progress、table 等组件。
# changelog-ant-design-pro

## [v5.0.0__202107](https://github.com/ant-design/ant-design-pro/issues/8656)

- 两年间前端的生态也发生了一些变化，Low-Code 大行其道，Bundleless 也随着 Snowpack，Vite 的发布越来越火热，前端在国际化，权限，数据流和布局方面已经有了最佳实践。 
- Ant Design Pro致力于提升中后台的开发体验，在这些领域我们也提出了自己的解决方案。

- 最佳实践
  - 通过一系列umi插件提供了一套中后台最佳实践
  - Pro内置了以下的插件 antd-ui、权限管理、初始化数据、layout、i18n、model数据流、网络请求
  - 这些插件都支持快速关闭
  - 在V5中提供了一个轻量的数据流方案 plugin-model，redux样板代码多
  - 可以从 umi 中导出 react-intl 的所有 API
- 模板组件
  - 早在 Pro 的第一个版本我们就提供了一系列的区块来帮助用户开发页面，在 2.0 中我们还提供了 umi ui 来管理区块。
  - 但是在实际的使用中我们发现区块上手成本高，耦合太强。并没有取得很好的反响
  - 在 2.0 中我们增加了 ProLayout 在社区得到了很好的反馈
  - ProComponents 就是我们对于 CRUD 的抽象。
- 编译提速
  - umi 也提供了 Bundleless 方案 mfsu。
- 项目集成组件
  - 内置了dumi的项目集成模式，在登录之后看到业务组件文档的菜单。
- OpenAPI
  -  V5支持使用 OpenAPI 3.0.1 的接口描述文档，这份文档可以用 Swagger 来生成

## [v4__201905](https://juejin.cn/post/6844903857244340231)

- 带来了 TypeScript，Layout 组件，区块等新特性，并且逐渐抽离 Pro 的组件到 Ant Design 中
- TypeScript
  - 无论脚手架还是区块全部用 TypeScript 重构
- Layout
  - Pro 的 Layout 自动生成菜单，自动生成面包屑。
  - 它只与 antd 耦合
- 组件
  - Pro 中提供了一系列的组件。在 v4 中，我们将他们删除，他们将会逐步的沉淀到 Ant Design 中去
- 区块 （Block）
  - Layout 和 Pages ，所有的界面都是这两部分组成的。
  - 我们将 Layout 组件化来提供开发效率，而区块就是我们对 Pages 提效的解决方案
  - 每个区块都是一个页面 ，它可以带着自己的状态，本地化，甚至是 mock 数据和 server。
  - 如果你需要 Pro 中的页面，你可以通过区块快速下载并添加
- Ant Design Pro 4.0 兼容了 2.0 的所有特性，从 2.0 升级到 4.0 不需要要做任何改动
  - 在 Ant Design Pro 4.0 中，我们将 Layout 抽离成了单独的组件。你可以选择将其替换成最新的组件。

## [v2__201809](https://juejin.cn/post/6844903668660043783)

- 全新的页面
  - 引入四个新的界面：分步对话框、输入对话框、个人中心、个人设置
- 新布局和主题
- 脚手架切换到 umi
  - umi 以路由为基础的，支持类 next.js 的约定式路由
  - 支持路由级的按需加载
- 国际化最佳实践
  - 基于 umi-plugin-locale 的国际化最佳实践

## [v1__201801](https://v1.pro.ant.design/docs/changelog-cn)

- 图表底层升级 BizCharts
- 采用全新的菜单及路由配置，同时支持指定菜单项/面包屑隐藏
- 新增 Authorized 组件，增加权限管理模块
- 升级 Roadhog@2，支持可配置化的代码分割（默认关闭）

- v0.1.10__201710
  - Ant Design Pro 的第一个版本。
  - 一个React技术栈的脚手架。
  - 7个标准化场景，22个页面模板。
  - 14个精品组件。
  - 开发、调试、模拟数据、部署的一整套流程以及配套文案。
# ref
- https://github.com/taejs/ant-design-vanilla
  - Pure HTML/CSS/JavaScript Implementation, originating from Ant Design.
- https://github.com/huanhunmao/XiLan
  - 类似Ant design的UI组件库（更加的轻量级和便于使用）
- https://github.com/websemantics/ant-strap /201609
  - An elegant CSS Framework built after Ant Design using Bootstrap 4.
- https://github.com/joshuat/ant-design-sass
  - Simple port of Ant Design v3 to Sass
