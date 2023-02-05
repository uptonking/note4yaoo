---
title: lib-ui-css-themes-api-design
tags: [api-design, css, themes]
created: 2021-03-21T18:23:49.826Z
modified: 2023-01-09T15:45:27.018Z
---

# lib-ui-css-themes-api-design

# css-fwk-codebase

- css-coding-tips
  - css-reset依赖全局级css vars，经常将两者放在一个文件或挨着@import
  - css vars的polyfill有些只支持全局级变量，要考虑支持IE浏览器
  - css-framework-global-config
    - theme, size, lang(标准html属性), dir/ltr/rtl(标准html属性)
    - 同时支持多种配置方式，优先级: 自定义配置类名 > 标准属性值 > 框架默认值
  - 主流design system的类名都包含前缀，如mdc-/slds-/pf-/spectrum-
    - 无前缀的有bootstrap、carbon、infima
  - 如何去掉design tokens中的prefix
    - 若写在样式源码中，export的对象就变得复杂，但可通过js生成来简化
    - 建议使用一个默认prefix，生成样式文件后，通过hook action修改生成的文件来去掉；或使用自定义transformer

- css变量名和类名都采用小写和短横，如halfmoon，infima
  - spectrum变量小写，类名大写
  - patternfly变量大写，类名小写

- style-docs
  - 组件示例中多个组件的间隔的实现
    - primitive: ml=mr=0，在一个元素闭合标签和下一个元素开始标签间手动添加空格或换行
    - halfmoon: docs: mr=2
    - pico: docs: mr=1/4, mb=1

- 组件variant的样式规则使用`css属性名: css变量值`(语义更明确，推荐)
  - pico，halfmoon, infima, cutestrap, chipolette, aqua
  - 样式规则全部采用css属性名，标准统一且语义明确方便查找
- 组件variant的样式规则使用`css变量名: 新的css变量的值`(修改更灵活)
  - patternfly, infima, cutestrap
  - 若在类似hover/primary这类样式中全写css变量名，早晚有一两个会出现循环引用的error，或者一两个不常用的css属性名未提前定义为变量，如outline/text-decoration，这时仍需要书写css属性名，会产生不一致的视觉效果

# css-fwk-tokens

- pgd/css
  - reset: modern-normalize.css1
  - font: 16, 18, 20
  - 行高: 24, 27, 20

- bootstrap v5.0.0-beta1(202012)
  - reset: normalize.css8，进行了定制，移除无关浏览器，添加新样式
  - breakpoints: 576, 768, 992, 1200, 1400
    - max-width: 540, 720, 960, 1140, 1320
  - font: 16
  - 行高: 24
  - 字体始终是16px，没有随着屏幕宽度变大变小
  - ref
    - github的font-size始终是14px，没有变大变小

- halfmoon v1.1.1(202103, develop branch)
  - reset: normalize.css8
  - font: 14, 16.8, 19.6
    - html-font-size: 0.625(10)， 0.75(12)， 0.875(14)
    - body-font-size: 始终为1.4rem
  - 行高: 21, 25.2, 29.4
  - 未提供组件级css vars，但全局级css变量名称规则很容易提取出各组件的变量
    - 因为没有组件级变量，切换主题时，直接修改属性color的值为另一个变量即可
    - 全局级变量统一放在:root中，组件中样式规则用的css属性名和css变量值
      - background-color: var(--lm-button-primary-bg-color-hover);
  - 单位几乎都用rem，1rem = 10px，因为1600px以上的屏幕会自动放大
  - **所有组件的所有样式值几乎都是css vars**，非常灵活
  - the containers, grid system and the flex utilities found in Halfmoon CSS are almost direct copies of the ones found in Bootstrap
  - Transparency(rgba) is used more commonly in dark mode, because everything needs to blend together to look good.

- primitive ui v1.5.3(202004)
  - reset: normalize.css8, scaffolding.scss

- pico.css v1.2.1(202011)
  - reset: normalize.css8, sanitize.css12, sectioning.scss
  - breakpoints: 576, 768, 992, 1200
    - max-width: 510, 700, 920, 1130
  - font: 16, 17, 18, 19, 20
  - 行高: 24, 25.5, 27, 28.5, 30
  - 未提供组件级css vars，样式变量全是global
  - 组件中的css vars没有使用fallback回退值

- bulma
  - font: 16, 18
  - 行高: 24, 27

- spectrum
  - font: 22, 18
  - 行高: 33, 27
  - 用[postcss-remapvars](https://www.npmjs.com/package/postcss-remapvars)自动生成各组件各套size对应的css vars变量名
  - 提供了组件级css vars，组件级变量也是全局级，分为`--spectrum-global/button/...`.
    - 组件中样式规则用的css属性名和css变量值
  - 切换theme通过在html标签添加多个class实现，包括scale, color, ltr-direction等，示例的中html元素的class超级多，其中包括serif字体

- patternfly
  - [Patternfly 4 Guidelines](https://pf4.patternfly.org/guidelines/)
  - 组件级的变量未提供fallback回退值
    - 组件中样式规则用的css变量名和css变量值，前提条件是每种variant的前面需要写一遍color: var(--pf-c-button--m-secondary--Color);
  - dark mode只有button和card勉强能用，其他组件如banner的dark模式部分已开始但未实现
  - `.pf-t-dark`下的变量，命名清晰
    - 全局变量
      - --pf-global--primary-color--100
    - 各组件的变量，具体使用的是`.pf-t-dark .pf-c-button`
      - --pf-c-button--m-primary--Color，--pf-c-card--BackgroundColor
  - PatternFly is made out of isolated and modular structures that fall into 2 categories: Layouts, Components
  - Layouts are the containers that allow for organizing and grouping its immediate children on the page
    - A layout never imposes padding or element styles on its children.
  - Components are modular and independent structures concerned with how a thing looks.
    - The component itself never has widths, floats or margins.
  - classnames
    - create an extension to an element with BEM modifiers if it’s a change of color or scale. 
      - If the change generates a new entity, then create a new component.
    - PatternFly is made up of isolated components that don't allow dependencies. 
      - Therefore, the use of helpers or utility classes is discouraged.
