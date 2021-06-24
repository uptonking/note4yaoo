---
title: ux-design-system-features
tags: [design-system, pm]
created: '2020-12-27T09:13:57.265Z'
modified: '2021-01-01T20:08:42.719Z'
---

# ux-design-system-features

# guide

- design effects trending
  - neumorphism 类似材质浮雕设计
  - origami 类似折纸展开折叠的动画
# popular

## Material Design

- Principles
  - Material is the metaphor
    - inspired by the physical world and its textures
    - Material surfaces reimagine the mediums of paper and ink.
  - Bold, graphic, intentional
    - guided by print design methods — typography, grids, space, scale, color, and imagery — to create hierarchy, meaning,
  - Motion provides meaning
    - Motion focuses attention and maintains continuity through subtle feedback and transitions

## Carbon Design System

- Guiding principles
  - open
  - inclusive
    - designed and built to be accessible to all, regardless of ability or situation.
  - modular and flexible
    - modularity ensures maximum flexibility in execution. 
    - Its components are designed to work seamlessly with each other
  - puts the user first
    - Using rigorous research into users’ needs and desires
  - consistency
    - Based on the IBM Design Language, every element and component of Carbon was designed from the ground up to work elegantly together to ensure consistent, cohesive user experiences.

## Salesforce Lightning Design System

- Flexible
  - Start building immediately, without worrying about detailed specs. 
- Scalable
  - Manage design at scale, with a living design system that evolves as needs change.
- Efficient
  - SLDS saves time and energy, freeing designers and developers to focus on larger issues of usability 
  - Standardized, reusable components support collaboration and provide a consistent look and user experience
- Accessible
  - All SLDS components include ARIA markup and guidelines
- Living
  - Our UX team rolls out new UI updates with every release
- Platform Agnostic
  - Use the SLDS CSS framework with any tech stack

## Spectrum

- Rational
  - Spectrum is based on real-world situations. 
  - Every component, pattern, and principle is informed by research and thoughtful testing.
- Human
  - It's deeply committed to a high standard of accessibility, honesty, and respect for user attention.
- Focused
  - Spectrum strives to deliver what’s needed, when it’s needed. 
  - No unnecessary decoration or irrelevant content.

## Elastic UI

- Design goals
  - accessible to everyone
  - themable
  - flexible and composable
    - Configurable enough to meet the needs of a wide array of contexts while maintaining brand and low-level consistency.
  - responsive
  - well documented and tested
  - playful
    - Simple and consistent use of animation brings life

## Ant design

- 自然
  - 界面设计中最重要的视觉要素，包括布局、色彩、插画、图标等，应充分汲取自然界规律
  - 让人机交互行为更自然
- 确定性
  - 为设计者提供足够精简的设计规则、组件、模式等
  - 一致的外观和交互，保持面向用户的熟悉感，能提升易学性
- 意义感
  - 结果的意义：明确目标，即时反馈
  - 过程的意义：让当下的工作既不过于简单，亦不过于复杂
- 生长性
  - 提升功能、价值的可发现性。
  - 用发展的眼光做设计，充分考虑人、机两端的共同生长。
# Element
- 一致性 Consistency
- 反馈 Feedback
- 效率 Efficiency
- 可控 Controllability

## Polaris

- Shopify experience values
  - CONSIDERATE
  - EMPOWERING
  - CRAFTED
  - EFFICIENT
  - FAMILIAR
  - TRUSTWORTHY
- Polaris is changing
  - Refreshed visual styles
  - Future-friendliness
    - design tokens and new infrastructure let us iterate easily across experiences.
  - Purposeful brand presence
  - Familiarity across experiences

## Base Design

- Extensibility
  - Through the Overrides API and configurable Themes, Base Web provides you with an extreme level of customization. 
- Accessibility
  - components are built with accessibility being a first-class citizen.
- Performance 
  - Styletron is the CSS-in-JS engine powering Base Web

## OpenUI5

- Enterprise-Grade
  - follows open standards and includes powerful development concepts
- Responsive on All Devices
  - UI5 apps and controls run on smartphones, tablets and desktop browsers.
- Free and Open Source

## PatternFly

- Make it flexible.
  - Our components can be arranged in any number of ways, 
  - and our CSS variable system can be used for all kinds of customization.
- Make it accessible.
- Make it consistent.
  - Our clear guidelines and tools help streamline communication so that all teams can create unified applications and interfaces.
- Make it scalable.
  - Our components are designed for enterprise IT applications used in businesses of all sizes.
- Make it open.

## Theme UI

- Ergonomic
  - Best-in-class developer ergonomics let you style your application quickly and consistently based on your theme
- Themeable
  - Quickly and easily reference values from your theme throughout your entire application, on any component
- Constraint-based
  - Use color, typography, and layout scales rooted in constraint-based design principles

## Chakra UI 

- Themeable
  - Customize any part of our components to match your design needs.
- Light and Dark UI
  - Optimized for multiple color modes. Use light or dark, your choice.
- Composable
  - Designed with composition in mind. Compose new components with ease.
- Accessible
  - Chakra UI strictly follows WAI-ARIA standards for all components.
# more design system
- Semantic UI
  - Concise HTML
    - Classes use syntax from natural languages like noun/modifier relationships, word order, and plurality to link concepts intuitively.
    - Get the same benefits as BEM or SMACSS, but without the tedium.
  - Intuitive Javascript
    - Semantic uses simple phrases called behaviors that trigger functionality.
  - Simplified Debugging
    - Performance logging lets you track down bottlenecks without digging through stack traces.
- Rock's Design System
  - Simplicity
    - Strive to keep the component API fairly simple and show real world scenarios of using the component.
  - Composition
    - Break down components into smaller parts with minimal props to keep complexity low, and compose them together. 
    - This will ensure that the styles and functionality are flexible and extensible.
  - Dark Mode
    - Make components dark mode compatible. 
    - Use our ColorModeProvider component and useColorMode hook to handle styling.
  - Accessibility
    - When creating a component, keep accessibility top of mind. 
    - This includes keyboard navigation, focus management, color contrast, voice over, and the correct aria-* attributes.
  - Style Props
    - All component styles can be overridden or extended via style props to reduce the use of css prop or styled(). 
    - Compose new components from Box.
  - Naming Props
    - We all know naming is the hardest thing in this industry. 
    - Generally, ensure a prop name is indicative of what it does. 
    - Boolean props should be named using auxiliary verbs such as does, has, is and should. 
    - For example, Button uses isDisabled, isLoading, etc.
- Layui
  - 返璞归真
    - 追寻于原生态的书写指令，试图以最简单的方式诠释高效
  - 双面体验
    - 开发简易，功能丰盈
  - 星辰大海
    - 如果眼下还是一团零星之火
