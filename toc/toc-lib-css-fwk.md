---
title: toc-lib-css-fwk
tags: [css, lib, toc]
created: 2020-10-22T12:57:49.045Z
modified: 2021-01-28T21:14:14.667Z
---

# toc-lib-css-fwk

# guide
- tips
  - 偏css的视图层缺少a11y
  - 经典的ui组件: react-bootstrap，可参考实现a11y

- css-ui
  - https://ui.shadcn.com/examples/music /主色黑白灰
  - https://flowbite.com/blocks /部分付费-但可参考效果/低配版是preline
  - https://www.tremor.so/blocks /侧重图表recharts
  - https://ui.mantine.dev /默认浅灰背景色加线框分隔-组件多
  - https://daisyui.com/components /无app-ui

- ux-designer
  - https://dribbble.com/timelessco
  - https://twitter.com/anguriostegui
# popular
- https://github.com/argyleink/open-props
  - https://open-props.style/
  - CSS custom properties to help accelerate adaptive and consistent design.
  - 毛玻璃风格
  - These props come in many flavors: CSS, PostCSS, JSON, or Javascript.

- https://github.com/saadeghi/daisyui
  - https://daisyui.com/
  - free and open-source Tailwind CSS component library

- cirrus /1.1kStar/MIT/202302/scss
  - https://github.com/Spiderpig86/Cirrus
  - https://www.cirrus-ui.com/
  - 文档单页，文档样式非常友好
  - css vars和scss vars混用
  - 特点是简洁干净，多圆角阴影
  - A fully responsive CSS framework with beautiful controls and simplistic structure. 
  - Cirrus is designed to be adaptable to existing themes or when starting fresh.
  - The only component that requires the use of jQuery is the Header component for toggling the dropdown menu on mobile.
  - https://github.com/Cirrus-UI/Cirrus-Start
- https://github.com/jango707/CMS-protfolio
  - https://jangsportfolio.netlify.app/
- cirrus-examples
  - https://github.com/carah-tychewicz/weather-app

- https://github.com/conedevelopment/sprucecss
  - https://sprucecss.com/
  - modern CSS framework, design system built on Sass
  - It comes with dark-mode support. It uses CSS custom properties
  - 大多是业务组件，样式干净，很有设计感，有一点点bootstrap的味道
  - Spruce UI 未开源，但示例组件提供了scss，doesn’t have its public repository
  - We made a controversial decision with Spruce to leave a classical grid system out.
  - [v2_202305:  config() function supports sass and css vars](https://github.com/conedevelopment/sprucecss/releases/tag/v2.0.0)

- https://github.com/codyhouse/codyframe /v4
  - https://github.com/CodyHouse/codyhouse-framework /v3
  - https://codyhouse.co/
  - CodyHouse UI is a library of HTML, CSS, and JavaScript components that make it easy to create accessible websites quickly 
  - The components are available in 3 versions: 
    - Using the CodyFrame components
    - Using the Tailwind components
    - Using the 'framework-free' components
  - 大多数组件都是pro-only，Templates全付费
  - 提供了ui组件的在线编辑器示例
  - 文档和示例做得很好
    - https://codyhouse.co/ds/globals/colors
  - 使用了css vars

- spectre /10.3kStar/MIT/202007
  - https://github.com/picturepan2/spectre
  - https://picturepan2.github.io/spectre/
  - 文档多页，文档基于pug实现
  - a responsive CSS framework based on flexbox
  - Designed and built by Yan Zhu(Microsoft MVP)
  - 特点是方形，多用边框
  - 未使用css vars
- https://github.com/angular-package/spectre.css
  - https://spectre.angular-package.dev/
  - 提供了filter、timeline等扩展

- https://github.com/zvizvi/freewindcss /202205/scss/inactive
  - https://codesandbox.io/s/freewindcss-pfq17e
  - Use Tailwind's set values and units in pure CSS variables

- tremor /6.2kStar/apache/202202/ts
  - https://github.com/tremorlabs/tremor
  - https://www.tremor.so/
  - https://demo.tremor.so/
  - a low-level, opinionated UI component library to build dashboards.
  - [tremor • changelog](https://www.tremor.so/changelog)
    - v2_202303 exposure of className, and full switch to Tailwind CSS
  - 依赖recharts2、tippyjs、date-fns，未使用任何组件库
  - 图表默认动画

- bootstrap /143kStar/MIT/202007
  - https://github.com/twbs/bootstrap
  - https://getbootstrap.com/
  - The most popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.

- bulma /40.5kStar/MIT/202007
  - https://github.com/jgthms/bulma
  - https://bulma.io/
  - Modern CSS framework based on Flexbox
  - https://github.com/jgthms/bulma/tree/css-variables-with-fallback
    - I've been working on this CSS Variables + HSL version of Bulma.
      - The idea is to provide each value as a separate variable, so you can tweak the H, S or L independently. 
      - That way you can theme a whole page dynamically.
    - The main issue is that it requires close to 100 CSS Variables to be applied to `:root`. 
      - While this is done automatically, it might be considered noisy and verbose. 
      - It is however the most flexible approach for theming a CSS framework.

- skeleton /18kStar/MIT/201412/css
  - https://github.com/dhg/Skeleton
    - http://www.getskeleton.com/
    - A Dead Simple, Responsive Boilerplate
  - https://github.com/atomicpages/skeleton-sass
    - https://atomicpages.github.io/skeleton-sass/
    - Skeleton Sass is a highly modular version of Skeleton CSS
    - 提供了themes
  - https://github.com/WhatsNewSaes/Skeleton-Sass
    - Sass Version of Skeleton (2.0.4)
  - more-skeleton
    - https://github.com/amdelamar/osseous
      - A project based off of Skeleton and other popular libraries.
      - a small CSS framework that only includes some (bony) elements

- primer-css /9.7kStar/MIT/202010/scss
  - https://github.com/primer/css
  - https://primer.style/css
  - The CSS implementation of GitHub's Primer Design System
- pure-css /BSD/21kStar/202007/Yahoo
  - https://github.com/pure-css/pure
  - http://purecss.io/
  - A set of small, responsive CSS modules
- https://github.com/andrearufo/nova.css
  - https://andrearufo.github.io/nova.c ss/
  - 文档单页，样式友好，白底绿字
  - minimalistic CSS framework for your webpages.
  - Made in pure SCSS and compiled with Gulp.
# css-framework-ui
- milligram /8.8kStar/MIT/202006
  - https://github.com/milligram/milligram
  - https://milligram.io/
  - /9.2kStar/MIT/202006/css
  - 文档单页，文档也支持多页，基于pug实现
  - A minimalist CSS framework.
- vanilla-framework /438Star/LGPLv3/202009/scss/ubuntu
  - https://github.com/canonical-web-and-design/vanilla-framework
  - https://vanillaframework.io/
  - a simple extensible CSS framework, built using Sass
- Skin /111Star/MIT/202010/less/ebay
  - https://github.com/eBay/skin
  - https://ebay.github.io/skin/
  - Pure CSS framework designed & developed by eBay for e-commerce marketplace.
  - Skin follows the BEM methodology of "Block, Element and Modifier" to ensure our HTML class name and structure is human readable and understandable.

- https://github.com/sky-uk/toolkit
  - http://www.sky.com/toolkit
  - Sky's CSS Toolkit
  - https://github.com/sky-uk/toolkit-react
- https://github.com/OfficeDev/office-ui-fabric-core
  - Fabric is a responsive, mobile-first collection of styles and tools designed to make it quick and simple for you to create web experiences using the Office Design Language.

- https://github.com/5t3ph/smolcss
  - https://smolcss.dev/
  - Minimal snippets for modern CSS layouts and components
  - The goal of SmolCSS is to provide solutions to everyday scenarios and give you just enough info about the included modern CSS properties.
    - responsive grids with both flex and CSS grid
    - centering
    - custom list styles
    - image gallery
 

- https://github.com/Borderliner/Meshki
  - https://borderliner.github.io/Meshki/
  - Meshki: A Black-Colored, Responsive Boilerplate for UI Development

- https://github.com/OrbitCSS/orbitcss
  - https://orbitcss.com/examples/
  - a modern CSS framework based on Flexbox.
  - 方形设计，多边框
  - 模版很多
# classless
- MVP.css /4.2kStar/MIT/202209/css/单文件
  - https://github.com/andybrewer/mvp
  - https://andybrewer.github.io/mvp/
  - https://andybrewer.github.io/mvp/mvp.html
  - Minimalist classless CSS stylesheet for HTML elements

- water.css /5.7kStar/MIT/202010/css/classless
  - https://github.com/kognise/water.css
  - https://watercss.kognise.dev/
  - theming基于css vars实现，文档单页比较简单
  - I commonly make quick demo pages or websites with simple content. 
    - For these, I don't want to spend time styling them but don't like the ugliness of the default styles.
  - Water.css is a CSS framework that doesn't require any classes.

- https://github.com/turretcss/turretcss
  - A Responsive Front-end Framework for Accessible and Semantic Websites with default HTML elements

- new.css /3.2kStar/MIT/202009/css
  - https://github.com/xz/new.css
  - https://newcss.net/demo/
  - theming基于css vars实现，文档单页很标准
  - A classless CSS framework to write modern site using only HTML.

- sakura /2.9kStar/MIT/202012/scss
  - https://github.com/oxalorg/sakura
  - https://oxal.org/projects/sakura/demo/
  - theming基于scss vars实现，提供了dark、ink、vader、earthy等多个主题
  - 文档单页很标准
  - a minimal classless css framework/theme

- https://github.com/yegor256/tacit
  - http://yegor256.github.io/tacit/
  - No classes, no layouts. Just design plain and simple web pages compliant with HTML5
  - Tacit's goal is to be super simple and always with the same look-and-feel.
  - Here are some frameworks built on top of Tacit: kacit, Bahunya
- https://github.com/kevquirk/simple.css
  - a classless CSS template that allows you to make a good looking website really quickly.
# more-css-framework
- https://github.com/asmcss/assembler
  - https://asmcss.com/
  - 自己实现了类似tailwind

- https://github.com/sitetent/tentcss
  - Includes only the essentials to make camp.
  - not currently receiving updates.
- https://github.com/AliBahaari/Jikan
  - https://alibahaari.github.io/Jikan/
  - CSS framework for better, faster and more beautiful UIs.

- https://github.com/ffoodd/a11y.css
  - This CSS file intends to warn developers about possible risks and mistakes that exist in HTML code. 

- https://github.com/propjockey/augmented-ui
  - http://augmented-ui.com/
  - Cyberpunk-inspired web UI made easy
  - css only
