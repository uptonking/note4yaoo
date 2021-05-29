---
title: toc-lib-comp-design-stars
tags: [design-system]
created: '2020-10-24T18:21:09.519Z'
modified: '2021-01-12T18:48:52.713Z'
---

# toc-lib-comp-design-stars

# data-centric-components

- guidu /13Star/MIT/202105/ts/react
  - https://github.com/uidu-org/guidu
  - https://uidu.design/
  - Guidu is uidu's design system library
  - 提供了专门的数据类别组件：list, table, data manager, data views, timeline, dashlet, dashboard
  - 依赖styled-components、@amcharts/amcharts4、d3、@cubejs-client/react、react-table、twin.macro
  - These components are Atlassian Design Guidelines(ADG) compliant

- data-catalog-components /5Star/GPLv3/202104/js
  - https://github.com/getdkan/data-catalog-components
  - https://getdkan.github.io/data-catalog-components
  - A set of React components to facilitate the creation of Open Data Catalogs with React.
  - built for dkan(基于php，而ckan基于python)
# amazing
- Denali Design /Verizon Media
  - /69Star/MIT/202012/scss
  - https://github.com/denali-design/denali-css
  - https://denali.design/
  - Themeable CSS framework of Denali Ui components
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
