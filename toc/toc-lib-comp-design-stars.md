---
title: toc-lib-comp-design-stars
tags: [design-system]
created: 2020-10-24T18:21:09.519Z
modified: 2021-01-12T18:48:52.713Z
---

# toc-lib-comp-design-stars

# guide

- pick-ui-components
  - headless/unstyled
  - framework-agnostic
  - accessible
  - 还要参考dashboard

- refs
  - https://github.com/SaraVieira/ui-libraries /组件库对比

- css-ui
  - https://ui.shadcn.com/examples /主色黑白灰
  - https://ui.mantine.dev /默认浅灰背景色-组件多
  - https://www.tremor.so/blocks /侧重图表recharts
  - https://flowbite.com/blocks /大部分付费-可参考效果
  - https://daisyui.com/components /无app-ui
  - https://floatui.com/components
  - https://preline.co/examples.html
# components-stars
- https://github.com/argyleink/open-props
  - https://open-props.style/
  - https://stackblitz.com/@argyleink/collections/open-props
  - CSS custom properties to help accelerate adaptive and consistent design.
  - 毛玻璃风格
  - These props come in many flavors: CSS, PostCSS, JSON, or Javascript.
  - [A json source for style dictionary](https://github.com/argyleink/open-props/issues/288)
    - one of the reasons I dont ship Style Dictionary format is because there's **so many props that wouldnt convert to other platforms**. 

- https://github.com/mantinedev/mantine
  - https://mantine.dev/
  - https://ui.mantine.dev/
  - React components library with native dark theme support
  - 134 responsive components built with Mantine
  - 样式依赖emotion，支持sx

- https://github.com/shadcn/ui
  - https://ui.shadcn.com/docs/primitives/dropdown-menu
  - Beautifully designed components built with Radix UI and Tailwind CSS
  - 默认白色主题很有设计感

- https://github.com/skeletonlabs/skeleton /风格glassmorphism
  - https://skeleton.dev/
  - The UI toolkit for Svelte and Tailwind.

- NextUI /8.3kStar/MIT/202211/ts
  - https://github.com/nextui-org/nextui
  - https://nextui.org/
  - React UI library: themeable, fast
  - 依赖stitches-css-in-js、
  - created with React.js and Stitches, based on React Aria and inspired by Vuesax(vue).
  - modal的模糊背景特效很好
  - 大量使用阴影

- radix-ui /6.2kStar/MIT/202210/ts
  - https://github.com/radix-ui/primitives
  - https://www.radix-ui.com/docs/primitives/components/toolbar
  - Unstyled, accessible components for building high‑quality design systems and web apps in React.
  - https://github.com/radix-ui/design-system
    - https://design-system.modulz-deploys.com/
    - 使用纯.css样式文件，未使用自研的stitches
    - Design system maintained and used by WorkOS.
    - Built with Stitches and Radix UI Primitives.
  - https://github.com/radix-ui/icons
    - https://icons.radix-ui.com/
    - A crisp set of 15×15 icons designed by the WorkOS team.

- https://github.com/dracula/dracula-ui
  - https://ui.draculatheme.com/
  - A dark-first collection of UI patterns and components.
# data-centric-components
- guidu /13Star/MIT/202105/ts/react
  - https://github.com/uidu-org/guidu
  - https://uidu.design/
  - Guidu is uidu's design system library
  - 完全复制了atlassian-editor，并将组件替换成了自己的design system
  - 提供了专门的数据类别组件：list, table, data manager, data views, timeline, dashlet, dashboard
  - 依赖styled-components、@amcharts/amcharts4、d3、@cubejs-client/react、react-table、twin.macro
  - These components are Atlassian Design Guidelines(ADG) compliant

- data-catalog-components /5Star/GPLv3/202104/js
  - https://github.com/getdkan/data-catalog-components
  - https://getdkan.github.io/data-catalog-components
  - 依赖bootstrap.v4、reactstrap、react-dnd, react-table.v7
  - 样式普通
  - A set of React components to facilitate the creation of Open Data Catalogs with React.
  - built for dkan(基于php，而ckan基于python)

- https://github.com/Talend/ui /js/ts
  - created to simplify the development of Talend's front-end stack.
  - containers: A component here should never embed HTML or CSS. Only connection to the store and behavior should be done. All the state should be synchronised with redux using react-cmf API.
  - presenters: A set of stateless components. We want to avoid {children} for leaf as much as possible. 
  - react-cmf: a framework to build configurable React App using redux/redux-saga.
# amazing
- Denali Design /Verizon Media
  - /69Star/MIT/202012/scss
  - https://github.com/denali-design/denali-css
  - https://denali.design/
  - Themeable CSS framework of Denali Ui components
  - 官方文档示例做得好，但实际使用一般
  - theming基于scss vars，代码十分清晰，未使用css vars
    - [v1版本的global variables](https://denali.design/docs/1.0.3/guides/global-variables)用的是css vars
    - v2版本统一使用scss vars
  - 支持创建自定义theme
    - 预置的dark theme是通过覆盖sass vars实现
  - It supports theming through custom variables which means the visual appearance of Denali’s components can be easily adapted to fit the visual style of any brand. 
    - Additionally, components are framework independent allowing you to take what you need and leave the rest.
  - [Theme Your App with Denali](https://denali.design/docs/2.1.0/guides/themeable)
    - use a single CSS file to override Denali’s default visual style and create a custom theme for any project
      1. Get Denali CSS.
      2. Duplicate and rename the denali-dark-theme.scss file.
      3. Update global and component overrides to style all necessary components.
      4. Compile the code to a CSS file that will override Denali’s visual style.
    - decide whether to add your CSS styles within a `:root` or any parent container. 
      - A `:root` tag is recommended if you plan on creating a single theme, but a specific class is recommended if you plan on creating multiple themes for a project.
      - This is because multiple themes can be stored in a single file, but they can only be called upon individually if they are wrapped in any parent container with the theme class. 
      - Storing multiple themes in a single file is especially useful if you want to provide multiple variations of the same theme (such as a default, dark, or color accessible) to your end users.
    - Denali offers global overrides and component overrides. 
      - Global overrides override Denali’s default styling of multiple components at once, 
      - while component overrides only override styles specific to that component. 
  - ref
    - repos: css,site,svg,icon-font,ember
    - https://denali.design/docs/2.1.0/guides/themeable
    - https://github.com/denali-design/denali-ember
      - Ember.JS component library for the Denali CSS Framework
