---
title: lib-ui-ant-design-dev
tags: [antd, lib]
created: '2020-06-15T10:25:37.356Z'
modified: '2020-12-08T13:22:47.564Z'
---

# lib-ui-ant-design-dev

# pieces

# changelog

- ref
  - [changelog for v4.x](https://ant.design/changelog-cn)
  - [changelog for v3.x](https://github.com/ant-design/ant-design/blob/3.x-stable/CHANGELOG.zh-CN.md)
  - [changelog for v2.x](https://github.com/ant-design/ant-design/blob/2.x-stable/CHANGELOG.zh-CN.md)
  - [changelog for v1.x](https://github.com/ant-design/ant-design/blob/1.x-stable/CHANGELOG.md)
  - [changelog for v0.x](https://github.com/ant-design/ant-design/releases?after=0.10.1)

- 4.0.0-20200228
  - v4依赖的React最低版本要求升级到了React 16.9，提供更多的hooks 
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
- 3.0.0-20171204
  - 全面支持React 16
  - 全新的色彩系统，组件主色由『#108EE9』改为『#1890FF』(『拂晓蓝』)
  - 全新的视觉样式和组件尺寸，基础字体大小由12px增大到14px
  - 新增组件：List, Divider
  - 3.9引入svg图标
- 2.0.0-20160928
  - 开发语言改为TypeScript，官方提供 .d.ts
  - 时间类组件 DatePicker、TimePicker、Calendar 等的底层 使用 moment 替换 gregorian-calendar
  - 新增组件：Mention, AutoComplete
- 1.0.0-20160509
  - 兼容React@15.x
  - 样式支持按需加载
  - 新增组件：Card, Rate, LocaleProvider
- 0.7.0-201500721
  - 第一个公开版本
  - 发布layout、iconfont、button、form、checkbox、radio、switch、slider、input-number、datepicker、select、tabs、steps、breadcrumb、collapse、pagination、modal、message、dropdown、popover、popconfirm、tooltip、progress、table 等组件。

# ref

- https://github.com/huanhunmao/XiLan
  - 类似Ant design的UI组件库（更加的轻量级和便于使用）
- https://github.com/websemantics/ant-strap
  - https://github.com/websemantics/ant-strap
- https://github.com/joshuaturner/ant-design-sass
  - Simple port of Ant Design v3 to Sass
