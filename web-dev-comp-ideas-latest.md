---
title: web-dev-comp-ideas-latest
tags: [components, frontend, latest, web]
created: '2020-10-29T12:46:59.023Z'
modified: '2020-12-27T20:29:55.568Z'
---

# web-dev-comp-ideas-latest

# latest

- ## 组件库研发方向及特色
- 每个大公司都有自己的设计系统与组件库
  - 可参考实现细节:ui组件结构、css写法、状态管理、事件处理
  - 既要突出特色亮点，也要考虑互操作标准化，如theme共享
- **framework agnostic**
  - architected to be adaptable to major web frameworks
  - foundation(host-agnostic) + adapter(host-interaction) architecture
  - [跨框架开发ui组件库(stencil)](https://zhuanlan.zhihu.com/p/41974042)
  - 开发者用户可在不同框架的项目中使用组件，因为原作者维护了多个port/bridge
    - 最理想的状态是类似jsx-lite能够自动编译到各种框架的组件形式
- **themeable**
  - follow the [Theme Specification](https://system-ui.com/theme/)
  - 两级theme变量：全局级，组件级
  - dark mode
  - 基于css vars实现theming，因为修改外层css无法影响shadow dom内的样式
  - 单独提供theme object using css in js，方便复用
    - 可提供一套css，再另外提供一套css in js的theme object
    - js工具方便计算css样式值，还能使用array-based values
    - css的复用性和灵活性不如js，可以用js生成普通css或原子类css
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
  - 都是nice-to-have，非必需
  - configurable-knobs
  - pluggable extensions
    - loading skeleton
    - collapsible card/panel/window
    - ui shell
    - highlight code
  - interactive animations
  - lab-features
- headless ui(不推荐)
  - 只适合简单组件，复杂组件如table实现功能时很可能与layout紧密相关
  - opinionated: ui交互或技术选型具有明显的偏向性
  - 使用headless ui时，组件配置项容易多到爆炸，如downshift
- configurable-knobs
  - convention over configuration
    - 所有组件的所有props都有合适的默认值，这样能更快的开始测试
    - 尽量实现不需要 required props
  - 所有组件共有的部分公共api
  - borderless
    - 部分组件提供无边框的版本，如modal
  - dark mode形式的组件
  - export default component screenshot image, not source code
    - 参考use-screenshot-hook，每个组件内置截图功能，截图时组件会动画变小
  - disable mode形式的组件，组件变灰色，常作为背景
  - scalable，如下拉列表列表选项变多时会变modal
  - more-config-options
    - scroll-to-position
- block-style component
  - 方便实现 collapsible content/card
  - 可缩放组件/scalable component，类似获取焦点时会自动放大的效果
  - try
    - 使用collapsible而不是modal，来引导用户聚焦，而不是打断流程
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
  - 开箱即用的dashboard模版，参考ibm carbon
  - 单个小组件的示例
  - 支持 ui shell theming
- near-zero config
  - 提供合理默认值，尽可能减少必需配置项
- reactive/functional ui
  - state-based components
- tagged template literals
  - 基于模板字符串的视图
- jsx
  - 基于jsx的通用视图，参考jsx-lite/solid/vue
  - jsx-lite compiles jsx to React, Vue, Angular, Svelte, Solid, web components, vanillajs
- hooks pattern
  - plugin system
- experimental
  - 基于css vars实现constraint-based design
- 其他特色参考点
  - openapi spec
  - 兼容性，高仿现有系统的设计、优点、api
  - responsive & mobile first
  - 组件实现采用的是单文件形式的组件，方便编辑，如flame、cactus、radix

- 组件ui构成
  - dom结构(非视觉结构)、样式、属性、行为

- 组件库重点
  - 样式书写与主题切换
  - 状态数据的存储与更新
  - 事件发布与订阅

# ideas

- ComponentPreview
  - 组件的快速预览图，不需要交互事件
  - 可参考SkeletonLoader

# discuss

- ## [Old and new ideas in React UI](https://react-ui.dev/core-concepts/ideas)
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

- ## [Layout-isolated components](https://visly.app/blogposts/layout-isolated-components)
- The move to component-based development has enabled a large number of really incredible improvements to tools and the front-end ecosystem as a whole. 
- Remember when we were building our apps as a set of screens and pages instead of thinking in components?
- The component model has changed this entirely - now, we think of pages as a composition of reusable components.
- This modular approach to UI is vital to us at Visly since it's what enables our product to work with any app right away. 
  - In the pre-component era, we would have probably required you to build your whole app inside of Visly from scratch.
- Essentially, we want to avoid any properties on the root element of a component that affect, or are affected by, elements outside of the bounds of that component.
- I would discourage properties like `margin`, because they act on elements outside of the component's scope; 
  - the same goes for properties like `align-self`, as it will stretch the width or height of the component depending on the flex-direction of its parent. 
  - In contrast, properties like `padding` are fine, as they are confined to the scope of the component. 
  - Basically, if a property depends on, or impacts, other components outside of its scope, I would discourage using it.
- Layout-isolated component
  - A component that is unaffected by the parent it is placed within, and does not itself affect the size and position of its siblings.
  - Something I think worth reiterating is that this only applies to the root element of a reusable component. 
- What properties make a component break layout isolation?
  - Any property which affects, or is affected by, elements outside a component scope are not layout isolated properties 
  - and should be avoided on the root layer of your component. 
- **align-self**
- **Flex properties**
  - Just like with `align-self`, the solution is to move flex out of the component 
  - and into a prop that can be controlled by the wrapping component.
- **Percentages**
- **Margins**
- **Tab index**
- **Absolute positioning**
  - This one is not as bad as the others, as it typically doesn't break anything; 
  - it may just make your component unusable in certain situations
  - Like all the previous examples, you can fix this by passing these styles in from above! 
- In conclusion
  - Build your components to be reusable; you never know where you'll end up needing them.
  - Add a `style` prop to your components so that layout responsibility is shifted to the parent.
  - Update your global CSS and disable default flex shrink `{ flex-shrink: 0; }`.
  - Use `<Spacer/> `components or stack spacing instead of margin to make code easer to move around.
- The idea for this post came out of a twitter discussion with Max Stoiber who shares a lot of my thoughts on this 
  - you should check out his thoughts on `margin`.

# ref

- [UI Component Best Practices](https://github.com/chris-pearce/ui-component-best-practices)
