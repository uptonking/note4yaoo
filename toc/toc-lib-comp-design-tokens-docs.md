---
title: toc-lib-comp-design-tokens-docs
tags: [design-system, design-tokens, docs, toc]
created: 2021-01-05T01:10:28.172Z
modified: 2021-01-11T18:34:20.713Z
---

# toc-lib-comp-design-tokens-docs

# guide

- style guide 文档该设计成单页，还是多页？
  - 前期可设计成单页，快速修改 + 方便查看
    - 单页文档参考theo html format
  - 后期可扩展成多页或SPA，丰富内容

- 设计样式时theming可参考
  - dark, material, bootstrap, flat/metro, monochrome, neumorphism, hand-drawn

- style-guide-docs-tips
  - 不要直接提供复制按钮，因为使用场景非常灵活
  - 提供多种格式的颜色值供复制

# style-docs-template

- tips
  - 不必搜索所有最新样式项目的仓库
    - 深入理解主流css framework的文档实现更好，大多都是多页文档

- primitive /760Star/MIT/202010/scss/NoDeps
  - https://github.com/taniarascia/primitive
  - https://taniarascia.github.io/primitive/
  - https://taniarascia.github.io/primitive/test.html
  - 完全基于sass，提供了基础页面模版
  - 提供了通过改变link的href属性值来切换theming的示例
  - A front-end design toolkit built with Sass for developing responsive web apps.
  - [Skeleton CSS](http://getskeleton.com/), the original inspiration
  - 实现细节
    - 使用了normalize.css和单独的reset.css，scaffolding.scss重置了大多数内置元素的样式
    - 测试页面link标签默认href为空字符串，即默认不加载css，但传入undefined不会变为空
    - 测试页面只有3处使用class设置了样式名，只用了`.small-container`和`.radio`两个类名

- 单页文档示例
  - primitive, pico
  - https://oxal.org/projects/sakura/demo/ (classless)
  - https://ajusa.github.io/lit/docs/lit.html
  - https://jenil.github.io/chota/
  - https://yeun.github.io/open-color/
  - https://nordhealth.com/styleguide/

- 多页文档示例
  - https://github.com/ciucacristi/elementric
    - https://ciucacristi.github.io/elementric/
    - minimal HTML + CSS + JS base front-end framework for simple web site projects.
  - https://newcss.net/usage/elements/ (classless)
  - https://picturepan2.github.io/spectre/utilities/colors.html
  - https://mildrenben.github.io/surface/


# docs-ui

- https://github.com/htmlstreamofficial/docs-ui-kit
  - https://htmlstream.com/preview/docs-ui-kit/index.html
  - /62Star/MIT/201905
  - 依赖jquery、jquery-ui、feather、prismjs
  - 右侧toc无法高亮
  - A beautiful Open Source Bootstrap 4 UI Kit 
  - Perfect for Documentation & Help Desk projects.
- infima /60kStar/MIT/202102/css
  - https://github.com/facebookincubator/infima
  - https://facebookincubator.github.io/infima/
  - A modern styling framework for content-driven websites 
  - It's just CSS, so it works with React, Vue, Angular, anything!
- UI Playbook /507Star/MIT/202010/ts
  - https://github.com/raunofreiberg/ui-playbook
  - https://uiplaybook.dev/
  - document common UI components, their functionality, best practices, accessibility requirements, and examples.
  - 网站设计是页面背景灰色、卡片背景白色

# components-docs-showcase

- [material-components-web](https://material-components.github.io/material-components-web-catalog/#/)
  - 作为所有组件预览的页面，页面白背景卡片白背景，视觉上一般，并且都设计为黑白单色，点开每个组件的页面是彩色
- https://material.io/components?platform=web
  - 页面白背景卡片紫背景，视觉上失败

- [grommet components](https://v2.grommet.io/components)
- 在所有组件预览的页面，展示了所有组件的轮廓，重新设计和简化了所有组件

- [ant-design scaffold 脚手架](https://scaffold.ant.design/#/)
- 页面灰背景卡片白背景，视觉上失败，元素凌乱
- https://ant.design/index-cn
  - 首页的白卡片边框几乎不可见，但感觉边框很尖锐

- [egghead.io](https://egghead.io/)
- 页面灰背景卡片白背景，视觉上很棒，页面灰背景的值修改了透明度
- https://egghead.io/blog
  - 文章页的网格布局没有使用卡片组件，每个格子直接上大图片下文字

- [made with react.js](https://madewithreactjs.com/)
- 页面灰背景卡片白背景，视觉上很棒，卡片很大，每行3个

- [UI Components Handbook](https://www.uiguideline.com/components)
- 组件信息详细，列出了所参考的设计系统

- 页面灰背景卡片白背景
  - https://www.facebook.com/
  - https://chakra-ui.com/
    - 视觉上很棒

- 页面白背景卡片白背景
  - https://next-ozone.vercel.app/
    - hover时卡片会变大，多用对齐的布局，卡片用得很少
  - [bit components](https://bit.dev/components)
    - 视觉上失败，文字太多了
  - https://ionicframework.com/docs/components
    - 网格展示，每行3个卡片，视觉还行
  - https://storybook.js.org/addons
    - 视觉上还行
  - https://vaadin.com/components
    - 页面白背景卡片白背景，视觉一般

- 页面白背景，无卡片边框
  - https://www.magicpattern.design/blog
    - 页面白背景，默认无卡片边框，但hover时显示边框阴影；部分卡片背景为深蓝色
    - 作者展示了很多示例和模版，大多数模板页面是灰背景
    - 设计了很多半圆形扇形的抽象图形
  - https://medium.com/
  - https://substack.com/

- more-ui-components
  - [eva design](https://akveo.github.io/nebular/docs/components/components-overview)
    - 首页只展示各种组件的缩略图图标
    - 灰白背景卡片白背景，视觉很棒
  - https://akveo.github.io/react-native-ui-kitten/
    - 直接展示在手机屏幕上的组件，并且是以动画自动播放的形式
  - https://material-ui.com/discover-more/showcase/
    - 直接展示应用该组件库的网站

# themeable design docs

- looker /gatsby
  - https://components.looker.com/foundations/typography
- mineral ui /react
  - https://mineral-ui.netlify.app/tokens
  - https://mineral-ui.netlify.app/color  /计算了对比度
  - tokens的命名如 `backgroundColor_brandPrimary_hover`
- theme-ui /gatsby
  - https://theme-ui.com/demo
- priceline /next
  - https://priceline.github.io/design-system/palette
- chakra-ui /next
  - https://chakra-ui.com/docs/theming/theme
- flame /storybook
  - https://lightspeed-flame.netlify.app/?path=/story/theme-tokens--colors

# popular docs

- material
  - https://material.io/design/color/the-color-system.html
- fluent
  - https://developer.microsoft.com/en-us/fluentui#/styles/web/typography
- carbon
  - https://www.carbondesignsystem.com/guidelines/color/overview /计算了对比度
- lightning
  - https://www.lightningdesignsystem.com/design-tokens/
    - colors,font,opacity,line height,spacing,radius,sizing
    - time,touch,media query,z-index
  - 命名混乱 $button-color-border-primary, $color-text-tab-label-disabled
- ant-design
  - https://ant.design/docs/spec/colors-cn
- polaris
  - https://polaris-tokens.herokuapp.com/
  - https://polaris.shopify.com/design/colors
  - https://github.com/Shopify/polaris-tokens
- primer-css /gatsby
  - https://primer.style/css/support/variables
- atlassian
  - https://atlassian.design/foundations/color/  /计算了对比度
  - https://atlassian.design/foundations/color/color-palette/
- spectrum
  - https://spectrum.adobe.com/page/design-tokens/
    - color,font,icon,motion,layout
  - https://opensource.adobe.com/spectrum-css/typography.html
- elastic ui
  - https://elastic.github.io/eui/#/utilities/color-palettes
  - https://elastic.github.io/eui/#/guidelines/colors
- patternfly
  - https://www.patternfly.org/v4/guidelines/colors

 

- bootstrap
  - https://getbootstrap.com/docs/5.0/utilities/colors/
  - https://github.com/twbs/bootstrap/tree/main/site
- pico
  - https://github.com/picocss/pico
  - https://picocss.com/
- fluid
  - https://www.engie.design/fluid-design-system/design-tokens/
- infor
  - https://design.infor.com/resources/design-tokens
  - https://github.com/infor-design/design-system/tree/master/design-tokens
- opentable
  - https://opentable.github.io/design-tokens/
  - Colors Typography Grids Spacing Borders Breakpoints Shadows Icons Icons(theme)
- garden
  - https://garden.zendesk.com/design/color
- grommet
  - https://v2.grommet.io/color
- backpack
  - https://backpack.github.io/tokens/spacing
  - https://github.com/Skyscanner/backpack

- gov
  - https://designsystem.digital.gov/design-tokens/
    - color,typesetting,flex,opacity,order,shadow,spacing units,z-index
  - https://design.cms.gov/styles/color/

# css framework docs

- Spectre.css /cssonly
  - https://picturepan2.github.io/spectre/utilities/colors.html
  - https://github.com/picturepan2/spectre/tree/master/docs
- Auro Design System
  - https://auro.alaskaair.com/color/core-digital-palette-usage
  - 开源的是api doc源码，设计网页源码未找到
- bulma /jekyll
  - https://bulma.io/documentation/overview/colors/
- materialize /cssonly
  - https://materializecss.com/color.html
  - https://github.com/Dogfalo/materialize/tree/gh-pages

# design tokens for design system

- https://www.formstack.com/brand
  - Messaging, Attributes, Logos, Colors, Typography, Photography
  - illustration, iconography, shapes
- https://orbit.kiwi/design-tokens/
  - use tokens instead of static values (like HEX codes) for color or sizing units.
- https://kalo.design/foundations/design-tokens/
  - Colors, type scales, spacing units, and transitions 
- https://comet.discoveryeducation.com/visual-language/tokens.html
  - Font, Size, Space, Shadow, Border, Animation, Breakpoints, Themes
- https://design.bitnami.com/category/Design-Tokens/
  - store visual attributes.
- https://protocol.mozilla.org/fundamentals/tokens.html
  - https://github.com/mozilla/protocol-tokens
  - https://github.com/FirefoxUX/design-tokens
- https://rei.github.io/rei-cedar-docs/tokens/all-tokens/
  - https://github.com/rei/rei-cedar-tokens

# docs for design system

- https://www.duetds.com/tokens/
  - color, font, viz, radius, space, size, opacity, z-index, transition
- https://nulogy.design/style/typography/ /react/styled-comp
  - https://nulogy.design/style/spacing/
- Norton Design
  - https://wwnorton.github.io/design-system/docs/foundations/design-tokens
  - https://wwnorton.github.io/design-system/docs/foundations/color
- vue design
  - https://vueds.com/example/#!/Design%20Tokens

- https://styleguide.pivotal.io/modifiers/colors/
- http://mongodb.design/#/ui-design-system/base-styles/colors
- https://seek-oss.github.io/seek-style-guide/typography
- https://seeds.sproutsocial.com/visual/color

# docs for living/ui style guide

- https://github.com/wikimedia/WikimediaUI-Style-Guide
  - https://design.wikimedia.org/style-guide/
  - https://design.wikimedia.org/style-guide/visual-style_colors.html
  - Wikimedia Design Style Guide with user interface focus

 - https://github.com/adjust/design-tokens
   - https://design-tokens.now.sh/
   - show off the new UI design in a centralized and easy-to-consume way

- https://github.com/AljanScholtens/taiga-boilerplate
  - 使用了nunjucks模版
- https://github.com/bjankord/Style-Guide-Boilerplate
  - 大量空白，弱依赖php
- https://github.com/pure-css/pure-site
  - 使用了handlebars，旧版文档

- https://github.com/uswitch/ustyle
  - https://ustyle.guide/
  - uStyle, aptly named, is the styleguide gem for uSwitch. 
  - Include it in your Rails/Sinatra/Anything project as a gem to apply consistent styles according the uSwitch styleguide.
  - uStyle comes with JavaScript implementations of the custom Sass Ruby functions used by Sprockets.


- https://github.com/anges244/evie
  - https://evie.undraw.co/docs
  - 基于ejs

- https://github.com/freeCodeCamp/design-style-guide

- https://github.com/kylelogue/mustard-ui
  - https://kylelogue.github.io/mustard-ui
  - A starter CSS framework that actually looks good.
  - 文档是纯client js，但组件示例用的是codesandbox


- https://qian-dao-zhen-yi.gitbook.io/rspec-style-guide/
  - 使用gitbook创作

- https://github.com/Foveluy/ReStory
  - 依赖antd3、showdown、koa
  - A static site generator with MDX for React documentation.
## 文档单页

- https://github.com/agileleague/thimblecss
  - https://thimblecss.com/
  - A nimble CSS framework built with Flex Box for the modern web
  - 类似pico的文档
- https://github.com/Jaspero/pix
  - https://pix-css.firebaseapp.com/
  - A modern css/scss boilerplate framework. simple and modular
- https://github.com/Ferror/grave
  - https://grave.malcherczyk.com/
- https://github.com/dgrammatiko/naf-css
  - https://dgrammatiko.github.io/naf-css/
  - 样式过于简单，示例很典型
- https://github.com/milligram/milligram
  - https://milligram.io/
- https://github.com/Spiderpig86/Cirrus
  - https://cirrus-ui.netlify.app/
  - 样式非常友好
- https://github.com/kbrsh/wing
  - https://kbrsh.github.io/wing

## 文档多页

- https://github.com/codeforms/Punica-CSS-Framework
  - https://codeforms.github.io/Punica-CSS-Framework/base/colors.html
- https://github.com/pepabo/nachiguro
  - https://pepabo.github.io/nachiguro/color.html
- https://github.com/halibegic/coco-css
  - https://github.com/halibegic/coco-css

# more-docs

- gatsby
  - https://aha.got-it.ai/2.0.1/foundations/colors/
  - https://amar-ui.tunaiku.com/foundations/color-system
  - https://xstyled.dev/docs/colors/
  - https://bumbag.style/palette/

- next
  - https://www.welcome-ui.com/theming/colors
  - https://trendmicro-frontend.github.io/styled-ui/colors

- https://turretcss.com/demo/
  - No Javascript. Just clean, simple, and modern CSS.
  - 支持搜索侧边栏菜单项目
  - 侧边栏菜单是accordion，只能有1个展开

