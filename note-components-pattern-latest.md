---
title: note-components-pattern-latest
tags: [components, latest, pattern]
created: '2020-10-29T12:46:59.023Z'
modified: '2020-10-29T12:52:12.025Z'
---

# note-components-pattern-latest

## latest

- 组件库研发方向及特色
  - 每个大公司都有自己的设计系统与组件库
    - 可参考实现细节:ui渲染、css、状态
    - 既要突出特色与众不同，也要考虑互操作标准化，如theme共享
  - themeable
    - 全局theme及组件级theme
  - near-zero config
    - 提供合理默认值，尽可能减少必需配置项
  - headless ui
    - 只适合简单组件，复杂组件如table实现功能时很可能与layout密切相关
    - opinionated: ui交互或技术选型具有明显的偏向性
  - cross-framework ui
    - foundation(host-agnostic) + adapter(host-interaction)
    - [跨框架开发ui组件库(stencil)](https://zhuanlan.zhihu.com/p/41974042)
    - 用户或二次开发者用起来像framework-agnostic，但原作者可能要维护多个port或bridge
  - reactive/functional ui
    - state-based components
  - tagged template literals
    - 基于模板字符串的视图模板
  - jsx
    - 基于jsx的通用视图，参考jsx-lite/solid/vue
  - hooks pattern

- ui组件构成
  - dom结构(非视觉结构)、样式、属性、行为
- 组件库重点
  - 样式书写与主题切换
  - 状态数据的存储与更新
  - 事件发布与订阅

## ideas

- ComponentPreview
  - 组件的快速预览图，不需要交互事件
  - 可参考SkeletonLoader

- [UI Component Best Practices](https://github.com/chris-pearce/ui-component-best-practices)

### [Old and new ideas in React UI](https://react-ui.dev/core-concepts/ideas)

- Design Tokens
- Modular Scales
- Theme specification
- ThemeProvider in React
- Styles connected to theme
- Element primitive
- Classes, not inline styles
- Component tokens
- Component selectors
- Layouts and marginless components
- Stack with gap
- Responsive syntax
- Components in themes
- Variants
- Extending the library
