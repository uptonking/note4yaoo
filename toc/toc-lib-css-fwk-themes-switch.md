---
title: toc-lib-css-fwk-themes-switch
tags: [css, css-vars, themes, theming, toc]
created: 2021-01-28T21:12:30.674Z
modified: 2023-02-26T18:26:07.198Z
---

# toc-lib-css-fwk-themes-switch

# guide

- 设计样式theming时可参考
  - dark/darcula, material, apple/ios, bootstrap, flat/metro, monochrome, neumorphism, hand-drawn(papercss)
  - try: glass-ui, web-map-theme, gradient, globs, generative, ink
  - vendor: tailwindui(paid/clone), infima(参考官网文档)
  - 甚至所有的theme主题样式都可以在bootstrap的基础上修改得来
  - 基于粒子/particles的设计，或偏向于某一种dot dash的设计
    - 特别适合表达地理位置，常用在[logo](https://github.com/maplibre/maplibre-gl-js/issues/65)和icon
  - 基于折纸/origami展开折叠的设计

- https://github.com/liangjingkanji/DrakeTyporaTheme
  - 十二种主题风格 - Material Google JetBrains Vue Juejin Purple Ayu Dark

- 实现组件theming的方法(用css vars)
  - patternfly和spectrum都用了全局级变量和组件级变量，并且组件级变量值都由全局级变量值初始化
    - 考虑到设计规则会使组件级变量名唯一，所以组件级变量也是全局级变量，实现新主题就很方便
    - 两者所有组件的样式值几乎都是css变量，灵活性极高，但变量数量太多手写慢
  - 实现组件的不同theme都是(通过添加新类名如.pf-t-dark/.spectrum-dark)修改组件级变量的值
    - patternfly需手动书写在新主题下该组件级变量的值
    - spectrum可以自动生成各套主题对应的组件级变量的新值，也可手写
  - patternfly的优点
    - 切换主题很简单，只需在根部添加一个类 .pf-t-dark
    - 将所有属性值都提取为样式变量，符合思维习惯，手动命名更易理解
  - patternfly的缺点
    - 每新增一个主题，都需要将组件级变量的新值写一遍，没有使用组合，灵活性不足，且工作量大
  - spectrum的优点
    - 不同size和color的主题可组合很灵活，但若组合过多如加上字体、阴影时就容易思维混乱，不如单个主题类清晰
  - spectrum的缺点
    - 组件的类名变得很长
  - 因为组件级变量名不变而值会改变，且组件级变量都由全局级变量初始化，(同时很多中间属性值可能是自动生成的，)这就导致部分全局级变量值与思维相反，(此问题spectrum存在，其他方案也会存在类似问题)
    - patternfly未完整实现暗主题，现有部分很不成熟且少，只是将全局级变量和组件级变量命名为中立名如--pf-c-button--m-primary--Color(代表字颜色)，然后在明主题下值为light-100(蓝底的白色字)，在暗主题下值为dark-100(白底的蓝色字，名称为dark却代表蓝色)
      - 使用的是不同名的全局变量值，在不同主题下值也不同
    - spectrum明主题下gray100最白、gray900最黑，暗主题下gray100最黑、gray900最白
      - 使用的是同名的全局变量值，但在不同主题下具体值不同，极易思维混乱

- 实现themes切换的方法
  - 核心思路
    - `data-theme` 自定义data-属性，然后通过属性选择器设置theme样式变量
      - 若使用的是`data-theme-longName`的形式(名称中含有hyphen一杠)，则读取主题名时要注意会自动camelCase
      - 不方便添加其他可选信息到theme名称
      - 案例
        - pico,cutestrap
    - `class="theme-name--modifier"` 类选择器设置theme样式变量
      - 案例
        - halfmoon,patternfly,spectrum,stackoverflow
  - **通过`body.theme-light/dark`**
    - 当设计多套主题且每套主题有各自的黑白模式时，使用多个类更合适，但多个类也可以加到data-theme属性的元素，此方法思路也可以用到
      - `<html class="is-dark-mode name-of-current-theme">`
      - 甚至可以将主题变量根据多个类名拆分成对应多个部分，提高可读性和复用性
    - 此法还适合自定义主题名称较长的情况，因为BEM命名方式本身就很长

- 实现默认的light theme
  - 直接将light主题的变量全部放到`:root{}`，或者组件级变量的fallback回退值设为light主题变量值
    - 此时每个组件因为有fallback值可独立使用
    - 案例：patternfly
  - 通过`:root:not([data-theme="dark"])`
    - 推荐此方法，流行且清晰
    - 案例：pico
  - 尝试1 `:root:not([data-theme])`
  - 尝试2 `:root:not([class*='theme-dark' i])`
    - 谨慎用此法，伪类+:not属性选择器的特指度 高于 单个类选择器/单个属性选择器

- 实现多主题的方式对比 sass vs css vars
  - 不需要提前编译
  - css vars所有属性都会被inherit，而css属性只会inherit部分
  - css vars支持在css函数中使用

- dark-mode
  - 要测试黑暗模式下系统滚动条的效果，如低版本safari的滚动条未变黑
  - 对chrome，最右侧的滚动条在dark模式下依旧是白色，若页面中间也有白色滚动条，就比较刺眼
  - 对firefox，页面中间的滚动条背景色默认会与周边背景同色，更友好

- ref
  - search: pure css, css only, css framework, css vars
  - https://github.com/topics/css-framework?o=desc&s=updated
  - https://github.com/troxler/awesome-css-frameworks
# ready-themes
- https://github.com/ciucacristi/elementric
  - https://ciucacristi.github.io/elementric/
  - 样式设计基于白底的圆角方形，设计感很强
  - 圆角弧度特殊，整体偏宽
  - 特点
    - 大量白色或浅色纯色背景
    - 大量空白
    - 大量圆角
    - 大量阴影
  - a free front-end package of UI element

- https://github.com/saadeghi/daisyui
  - https://daisyui.com/
  - free and open-source Tailwind CSS component library

- https://tailwindui.com/components/preview
  - crafted components and templates, built by the makers of Tailwind CSS.

- https://github.com/anguriostegui/heros
  - https://heros-rouge.vercel.app/
  - 适合落地页，主内容是带搜索动画的列表
  - 依赖next、formspree-react表单、framer-motion6、swr
  - https://github.com/anguriostegui/portfolio
    - https://portfolio-anyelos.vercel.app/
  - https://github.com/anguriostegui/white-wolf
    - https://white-wolf-murex.vercel.app/

- https://chakra-ui.com/community/showcase
  - https://pro.chakra-ui.com/components
  - https://saas-ui.dev/docs/components/data-display/list
# themes-popular

## material

- https://github.com/beercss/beercss
  - https://www.beercss.com/
  - Build material design interfaces in record time

- https://github.com/material-components/material-components-web
  - 现在的theming功能主要通过sass实现，只有极少数变量可以通过css vars配置
    - 没有直接提供dark theme，但有提供sass实现的示例
    - [roadmap: Add Dark Mode support](https://github.com/material-components/material-components-web/issues/5253)
- materialize /38.3kStar/MIT/202006/scss
  - https://github.com/Dogfalo/materialize
  - https://materializecss.com/
  - 视觉上边框线不明显，大量运用色块
  - 文档多页，基于jade
  - a CSS Framework based on material design
- https://github.com/mildrenben/surface
  - https://mildrenben.github.io/surface/
  - /345Star/MIT/201709/css/inactive/文档多页
  - A Material Design CSS only framework
- https://github.com/maxsite/berry
  - https://maxsite.org/berry
  - A utility-first CSS framework with full support Material Design.
- https://github.com/ManuTheCoder/material-design-pro
  - https://material-design-pro.hostman.site/
  - a responsive front end framework based on Material Design
- https://github.com/finnhvman/matter
  - /870Star/MIT/201907/js
  - Material Design Components in Pure CSS
  - Materializing HTML at just one class per component
  - The purpose of Matter is to provide the most easy-to-use but accurate implementation of Material Design Components.
  - Matter is built with theming in mind
- more-material
  - mui /4.5kStar/MIT/202006
    - https://github.com/muicss/mui 
    - https://www.muicss.com/
    - lightweight CSS framework that follows Google's Material Design guidelines.
    - Small footprint: mui.min.css - 6.6K, mui.min.js - 5.4K

## apple/ios

- https://github.com/Tommy-dotcom/IOS-UI
  - This is free iOS based UI ressources written in SCSS. 
  - It's like Bootstrap but inspired by Apple's design.
- https://github.com/elDrimm/iCss
  - iCSS is a open source CSS component library based on Apple's iOS 11 design.
- https://github.com/deepak-kumbhar/glass-ui-like-mac-big-sur
  - The basic HTML and CSS to design glass UI as like the Apple Big sur os

- https://github.com/konstaui/konsta
  - https://konstaui.com/
  - Mobile UI components made with Tailwind CSS
  - All Konsta UI components come with pixel perfect native-like iOS and Material Design themes
  - Konsta UI mostly designed to be used with "parent" frameworks like Ionic or Framework7.

- https://github.com/hbang/iOS-7-CSS
  - Basic iOS 7 CSS

- https://github.com/codedgar/Puppertino
  - https://codedgar.github.io/Puppertino/
  - A CSS framework based on Human Guidelines from apple
  - Puppertino does not include any responsive system, you must use Bootstrap, Flexbox Grid, Skeleton, or some other responsive Framework along with it.

 

- https://github.com/react-cupertino/react-cupertino
  - https://react-cupertino.github.io/components/accordion
  - React UI Component library inspired by Apple's Design Philosophy
- https://github.com/hennessyevan/human-ui
  - SwiftUI and The Human Design Guidelines for the Web
  - This UI library is built using The Platformtm. 
  - It is made possible by StencilJS, web-components, css modules and other native browser features.

- more-apple-ios
  - https://github.com/sungik-choi/gatsby-starter-apple
    - https://gatsby-starter-apple.netlify.app/
    - 效果就像最新的ios界面，推荐
    - Gatsby blog starter kit with beautiful responsive design
  - https://github.com/rex-taiwan/applescss
    - https://rex-taiwan.github.io/applescss/
    - Sass & Scss Design - Apple Watch Series 5 Web Recreation
  - https://github.com/haneenmahd/apple-colors
  - https://github.com/nursh/Apple-Store-Designs
    - https://nursh.github.io/Apple-Store-Designs/
  - [10 Sleek Apple-Style Code Projects From CodePen](https://1stwebdesigner.com/10-sleek-apple-style-code-projects-codepen/)
  - https://github.com/afeiship/wsui-appify
    - https://afeiship.github.io/wsui-appify/
    - Apple ui tookit for wsui.

## bootstrap

- chipolette /5Star/MIT/202008/css
  - https://github.com/Marcisbee/chipolette
  - http://marcisbee.com/chipolette/
  - 单页文档，但根据多个html通过innerHTML实现，使用了css vars
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - Chipolette is a tiny CSS framework/Starter kit.
  - It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.

## flat/metro

- https://github.com/daniruiz/flat-remix-css /202008/css
  - http://drasite.com/flat-remix-css
  - 视觉上，边框线特别明显，轮廓分明
  - CSS library that provides a set of predesigned elements
  - It follows a modern flat design using a colorful palette
- https://github.com/ajusa/lit /202005/css
  - https://ajusa.github.io/lit
  - 单页文档
  - a ridiculously small responsive css framework.
  - preserve everything Skeleton, Milligram, and other micro frameworks have to offer.
- https://github.com/olton/Metro-UI-CSS
  - https://metroui.org.ua/
  - Build responsive projects on the web in Metro Style
  - https://github.com/TalksLab/metro-bootstrap
    - http://talkslab.github.com/metro-bootstrap
    - Simple bootstrap from Twitter with Metro style.
- https://github.com/codyogden/press-css
  - https://press-css.io/
  - A flat, material, no bullshit, highly extensible CSS button library.
- https://github.com/Tropix126/wincss
  - https://tropix126.github.io/wincss
  - WinCSS is SASS framework which emulates the styles of Fluent Design applications as seen in WinUI 2.4.
- https://github.com/siimple/siimple
  - https://docs.siimple.xyz/examples/index.html
  - The minimal CSS toolkit for flat and clean designs
  - started as a small css framework with basic UI elements.

- https://github.com/designmodo/Flat-UI
  - https://designmodo.github.io/Flat-UI/
  - Flat UI Free - Design Framework (html/css3/less/js)
  - Flat UI is a beautiful theme for Bootstrap. 
    - We have redesigned many of its components to look flat in every pixel.

## monochrome

- https://github.com/asvvvad1/mono-color
  - https://asvvvad1.github.io/mono-color/
  - /57Star/MIT/202008
  - 提供了dark主题demo
  - CSS-only framework built with responsivity, readability, modularity, and a dual-theme in mind.
- https://github.com/kokushin/mono.css
  - https://kokushin.github.io/mono.css/
  - /8Star/MIT/201707/css
  - Minimal design based on black and white.
- https://github.com/cihankoseoglu/shades
  - A Sass/CSS framework for minimalist websites that use black, white and shades of gray as a design choice

- https://github.com/amir2mi/flatifycss
  - Modern flat design framework for the web — inspired by Duolingo design system

## glass ui/mac/blur

- https://github.com/heypoom/glassmorphic-ui
  - https://glassmorphic.netlify.app/
  - Glassmorphic-style UI components for the web.

- https://github.com/harshhhdev/glassmorphicssm
  - https://dev.to/harshhhdev/ui-design-trend-of-2021-4fb7

 

- https://github.com/AKAspanion/ui-glassmorphism
  - https://akaspanion.github.io/ui-glassmorphism/
  - React component library on 'glassmorphism' UI/UX trend.
  - 提供的示例是移动端预览效果，推荐

## neomorphism

- https://github.com/ismail9k/neomorphism
  - https://ismail9k.github.io/neomorphism/
  - UI components library in the new neomorphism design style

## hand-drawn

- https://github.com/papercss/papercss /字体变成手写体
  - https://www.getpapercss.com/
  - /3.2kStar/ISC/202011/scss
  - The Less Formal CSS Framework
- https://github.com/fxaeberhard/handdrawn.css
  - http://fxaeberhard.github.io/handdrawn.css/
  - /61Star/CC0-1.0/201606/css
  - Handdrawn.css lets you prototype your web site with a hand drawn look and feel.

- https://github.com/saurabhdaware/text-to-handwriting
  - https://saurabhdaware.github.io/text-to-handwriting/
  - converts text to an image that looks like handwriting

## particles-tracks

- https://github.com/matteobruni/tsparticles
  - https://particles.js.org/
  - TypeScript library for creating particles. Dependency free

- https://github.com/Wufe/react-particles-js
  - https://rpj.bembi.dev/
  - Particles React component, using tsParticles

- https://github.com/tim-soft/react-particles-webgl
  - https://timellenberger.com/particles
  - A 2D/3D particle library built on React, Three.js and WebGL
  - react-particles-webgl was inspired by the popular particles.js library and built with react-three-fiber to offer smooth 60FPS high-count particle fields in both two and three dimensions.

- https://github.com/kennethcachia/shape-shifter
  - http://www.kennethcachia.com/shape-shifter/
  - A canvas experiment in which a set of particles is used to render different shapes based on the user's input.
  - It supports multiple modes: text, countdown, time and icons.
  - 粒子动画示例的效果amazing

- more-particles
  - https://github.com/chainlito/dot-dashboard
    - https://dot-dashboard.vercel.app/
    - 依赖react, redux-saga, react-chartjs
    - dot-dashboard 一个暗黑系的首页示例
  - https://codepen.io/chrisgannon/pen/vYxmexW
    - 彩色圆形围绕人头轮廓，黑色主题很酷

## gooey/globs 黏成一团、水滴、变形

- https://github.com/luukdv/gooey-react
  - https://gooey-react.netlify.app/
  - The gooey effect for React, used for shape blobbing/metaballs

## origami 折纸艺术

- https://github.com/amandaghassaei/OrigamiSimulator
  - https://origamisimulator.org/
  - 依赖jquery、bootstrap、threejs
  - Realtime WebGL origami simulator

- https://github.com/robbykraft/Origami
  - a Javascript library for modeling, designing, and diagramming origami.
  - https://github.com/robbykraft/Math
    - math for origami. linear algebra, geometry, 2D and 3D, good interoperability with SVG

- https://github.com/xizhonghua/origami
  - http://masc.cs.gmu.edu/origami/folder.html
  - Visualize the folding process.
  - 依赖threejs、jquery

- https://github.com/georgiee/origami
  - https://georgiee.github.io/origami/editor/
  - Origami Building in threejs

- https://github.com/MuTsunTsai/box-pleating-studio
  - https://origami.abstreamace.com/zh/2021/06/02/the-story-of-box-pleating-studio/
  - https://bpstudio.abstreamace.com/
  - 箱形褶单轴基本形中的广义错位毕氏伸展（Generalized Offset Pythagorean Stretches in Box-Pleated Uniaxial Bases）
- ref
  - https://github.com/search?o=desc&q=origami+language%3Ajavascript+language%3Atypescript&s=stars&type=Repositories
  - https://github.com/raphamorim/origami.js
    - https://raphamorim.io/origamijs/
    - Origami began as a project to teach javascript and geometry to children and today has been used to simplify the way we work with canvas

- samples-origami
  - https://x.com/samdape/status/1799843696751325304
# more-themes
- https://github.com/yashdiniz/FRUI
  - Flat & Round User Interface, is a minimalistic and professional UI framework 
