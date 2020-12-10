---
title: note-web-dev-topics
tags: [dev, web]
created: '2020-11-01T09:48:26.955Z'
modified: '2020-12-08T14:40:01.285Z'
---

# note-web-dev-topics

## 难点

- scrolling滚动时的样式
  - 不同浏览器的滚动条样式不一致
  - 难以实现sticky，滚动的是body还是div
  - 移动端地址栏显示与隐藏
- tree-shaking
  - 各工具库的编译方式不同，webpack各版本支持程度不同
  - webpack v4不支持，v5支持
- component-to-image
  - repng
- 中文字体体积大的问题
  - 静态网页可通过腾讯开源的font-spider删除字体库中未使用的字符数据
  - 动态中文web字体暂无解决方案
- css模块化方案选择的问题
  - 暂无统一标准的解决方案，可以参考ant-design等大型项目的选择，直接使用css或scss
  - 要考虑将依赖的第三方组件的样式如何集成到现有项目
  - 要考虑与具体框架结合，方便实现国际化RTL、语言和样式主题切换
  - 考虑在特殊情况下如何覆盖组件的样式

## 前端基础框架开发

- 视图渲染 view render
  - MVC/MVVM
  - VDOM结构
  - DOM更新及操作
  - 生命周期
- 状态管理 state
  - 拆分合并, 子树更新
- 路由管理 router
- 中间件
- 网络请求
- ui组件库
- 同构
- ssr：
  - 核心优势：首屏加载更快、seo友好
  - next.js、razzle
  - 其他：beidou、react-server

- [2020年的React Hooks生态](https://juejin.im/post/6861055676652158990)
  - router: react-router, hookrouter
  - state: redux, mobx, unstated-next, recoil, use-immer, dva
  - components: antd, sunflower
  - hooks封装: react-use, ahooks, huse, react-adaptive-hooks
  - css-in-js: emotion, useTheme
  - i18n: react-intl, react-i18next
  - animation: react-spring
  - request: swr, react-query
