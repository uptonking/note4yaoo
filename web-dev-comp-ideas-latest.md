---
title: web-dev-comp-ideas-latest
tags: [components, frontend, latest, web]
created: '2020-10-29T12:46:59.023Z'
modified: '2020-12-27T20:29:55.568Z'
---

# web-dev-comp-ideas-latest

# latest

- 组件库研发方向及特色
  - 每个大公司都有自己的设计系统与组件库
    - 可参考实现细节:ui组件结构、css、状态
    - 既要突出特色与众不同，也要考虑互操作标准化，如theme共享
  - **framework agnostic**
    - architected to be adaptable to major web frameworks
    - foundation(host-agnostic) + adapter(host-interaction) architecture
    - [跨框架开发ui组件库(stencil)](https://zhuanlan.zhihu.com/p/41974042)
    - 开发者用户可在不同框架的项目中使用组件，因为原作者维护了多个port/bridge
      - 最理想的状态是
  - **themeable**
    - follow the [Theme Specification](https://system-ui.com/theme/)
    - 全局theme，组件级theme
    - dark mode
    - 基于css vars实现theming，因为修改外层css无法影响shadow dom内的样式
    - 单独提供theme object using css in js，方便复用
      - 可提供一套css，再另外提供一套css in js的theme object
      - js工具方便计算css样式值，还能使用array-based values
      - css的复用性和灵活性不如js，可以用js生成css
    - css vars和css in js实现theming都很方便
    - constraint-based design
      - better consistency with constraint-based design
      - themeable主要预定义颜色，constraint约束几乎所有属性名和属性值
      - 直接从theme中取值，不必花费过多精力选择数值大小、名称，节省时间精力
      - 使用一套设计约束，能更好地保持视觉和交互的一致性
      - allow the flexibility to write one-off styles
        - 一般通过className或style属性实现
      - 基于css-in-js的形式，更容易实现约束和theming
        - 组件只暴露必要接口，接口属性名统一，要依赖css in js才方便实现
        - 只用css vars不方便实现组件级的带约束的api接口
  - **playful**
    - pluggable extensions
      - loading skeleton
      - collapsible card/panel/window
      - ui shell
      - configurable
      - highlight code
    - interactive animations
    - 此处的features都是nice-to-have，非必需
  - headless ui
    - 只适合简单组件，复杂组件如table实现功能时很可能与layout密切相关
    - opinionated: ui交互或技术选型具有明显的偏向性
  - block-style component
    - 方便实现 collapsible content
  - interactive animation
    - anchor based flowing animation 
      - 基于某起点开始的变形动画，多是流动线型
      - 多是flow down的模式，坚持竖直滚动，取消水平滚动，水平滚动用下拉/分页
    - auto animation by default 
      - 首次渲染完成后，组件的某部分会自动开始动起来
      - 如文字从0开始增加
      - 如输入框的边框开始闪烁
    - 组件的动画不是必需项
  - ui shell
    - 开箱即用的dashboard模版
    - 单个小组件的示例
    - 支持 ui shell theming
  - near-zero config
    - 提供合理默认值，尽可能减少必需配置项
  - reactive/functional ui
    - state-based components
  - tagged template literals
    - 基于模板字符串的视图模板
  - jsx
    - 基于jsx的通用视图，参考jsx-lite/solid/vue
    - jsx-lite compiles jsx to React, Vue, Angular, Svelte, Solid, web components, vanillajs
  - hooks pattern
    - plugin system
  - 其他特色参考点
    - openapi spec
    - 兼容性，高仿现有系统的设计、优点、api
    - responsive & mobile first
  - experimental
    - 基于css vars实现constraint-based design

- ui组件构成
  - dom结构(非视觉结构)、样式、属性、行为

- 组件库重点
  - 样式书写与主题切换
  - 状态数据的存储与更新
  - 事件发布与订阅

# ideas

- ComponentPreview
  - 组件的快速预览图，不需要交互事件
  - 可参考SkeletonLoader

- [UI Component Best Practices](https://github.com/chris-pearce/ui-component-best-practices)

## [Old and new ideas in React UI](https://react-ui.dev/core-concepts/ideas)

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

# discuss
