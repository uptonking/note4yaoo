---
title: tool-ux-design-prototyping
tags: [design, prototyping, tool, ux]
created: '2021-01-02T12:24:49.293Z'
modified: '2021-01-02T12:26:32.961Z'
---

# tool-ux-design-prototyping

## guide

- 使用设计工具生成design system的优点
  - 不用写代码，拖拽设计即可完成
  - 方便测试与分享
- 使用设计工具生成design system的缺点
  - 没有统一标准，经常面临选择问题
  - 有的插件只生成一个大tokens文件，有的可按自己分类生成多个
  - 用什么属性名，用什么属性值类型，该支持哪些类别的属性
  - 结论是**不推荐**使用拖拽搭建工具生成项目中间要用的配置属性数据
    - 具体业务场景对灵活性要求过高，要修改自动生成的代码太繁琐

## figma

- 使用设计工具的2种思路
  - 以设计工具作为样式数据源 make figma your source of truth
    - [Figma plugin to export design tokens to json in an amazon style dictionary compatible format.](https://github.com/lukasoppermann/design-tokens)
    - 导出设计样式为json，然后再将json转换成平台相关样式文件，如css,xml,js
  - 以react组件作为样式数据源 Use comp as a source for your designs.
    - https://github.com/react-figma/react-figma
      - A React renderer for Figma
      - Compatible with react-native, react-sketchapp, react-primitives API.
    - https://github.com/airbnb/react-sketchapp
      - render React components to Sketch 

## 稿定设计

## more-design-tools

- canva
