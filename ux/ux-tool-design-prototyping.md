---
title: ux-tool-design-prototyping
tags: [design, prototyping, tool, ux]
created: '2021-01-02T12:24:49.293Z'
modified: '2021-04-08T09:20:43.467Z'
---

# ux-tool-design-prototyping

# guide

- 使用设计工具生成design system的优点
  - 不用写代码，拖拽设计即可完成
  - 方便测试与分享

- 使用设计工具生成design system的缺点
  - 没有统一标准，经常面临选择问题
  - 有的插件只生成一个大tokens文件，有的可按自己分类生成多个
  - 用什么属性名，用什么属性值类型，该支持哪些类别的属性
  - 结论是**不推荐**使用拖拽搭建工具生成项目中间要用的配置属性数据
    - 具体业务场景对灵活性要求过高，要修改自动生成的代码太繁琐

- 常用设计工具 design-tools
  - Figma /tokens-repos-42
    - https://github.com/six7/figma-tokens
      - a Figma Plugin allowing you to integrate Tokens into your Figma designs.
    - It gives you reusable tokens that can be used for a whole range of design options, from border radii or spacer units to semantic color and typography styles. 
    - It allows you to change tokens and see these changes applied to the whole document or its styles.
    - https://github.com/lukasoppermann/design-tokens
      - Design Tokens plugin for figma allows you to export design tokens into a json format that can be used with the Amazon style dictionary 
    - https://github.com/mikaelvesavuori/figmagic
      - Generate design tokens, export graphics, and extract design token-driven React components from your Figma documents.
  - Adobe XD
    - https://github.com/AdobeXD/design-system-package-dsp
  - Sketch /tokens-repos-28
    - https://github.com/design-meets-development/design-tokens-plugin
      - A Sketch plugin that exports Design Tokens to JSON format. 
      - You can export colors, typography, icons and utilis
  - Canva
  - 稿定设计
  - [Modulz](https://www.modulz.app/)
    - The user interface design tool
  - ref
    - [google trends comparison](https://trends.google.com/trends/explore?date=today%205-y&geo=US&q=%2Fg%2F11f65940xs,%2Fg%2F11cmy5dpl7,%2Fg%2F11c3xbl03p)

# figma

- 使用设计工具的2种思路
  - 以设计工具作为样式数据源 make figma your source of truth
    - 要做到与设计工具无关，可考虑导出通用格式文件如json
    - 导出设计样式为json，然后再将json转换成平台相关样式文件，如css,xml,js
    - [Figma plugin to export design tokens to json in an amazon style dictionary compatible format.](https://github.com/lukasoppermann/design-tokens)
  - 以react组件作为样式数据源 use comp as a source for your designs
    - https://github.com/react-figma/react-figma
      - A React renderer for Figma
      - Compatible with react-native, react-sketchapp, react-primitives API.
    - https://github.com/airbnb/react-sketchapp
      - render React components to Sketch 

- Figma.Cool official website 2020
  - https://github.com/yancymin/Figma.Cool-2020
  - https://www.figma.cool/
# 稿定设计

# more-design-tools

# tokens

- https://github.com/preciousforever/data-populator
  - A plugin for Sketch and Adobe XD to populate your design mockups with meaningful data. Goodbye Lorem Ipsum. Hello JSON.
