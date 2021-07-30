---
title: toc-lib-editor-builder-dashboard-popular
tags: [dashboard, ui, ux]
created: '2021-07-25T10:47:32.961Z'
modified: '2021-07-25T10:48:21.307Z'
---

# toc-lib-editor-builder-dashboard-popular

# guide

- dashboard baseline
  - AdminLTE, ant-design-pro, coreui-admin
  - ct-material-dashboard

- open dashboards vendors
  - 大厂的dashboard一般会提供多种框架实现的版本，但有些较新的也会只提供一个版本
  - creativetimofficial的仓库要比bootstrapdash多很多，更容易长期维护
  - https://www.creative-tim.com/
    - https://github.com/creativetimofficial
    - material, argon, black, now-ui
    - 第三方依赖都较少；大多基于reactstrap.v8
    - 更新较频繁，很多repos都长期维护
    - free repos多，但页面功能较少
    - 示例大多左边没有，右边有
  - https://www.bootstrapdash.com/
    - https://github.com/BootstrapDash
    - Star Admin 2, Purple Admin
    - 第三方依赖都很多；大多基于react-bootstrap.v1
    - 样式符合最新流行风格
    - free repos不太多；更新不太频繁
    - 示例大多左边有，右边有
  - https://www.wrappixel.com/
    - https://github.com/wrappixel
    - flexy, xtreme, ample, matrix
    - 第三方依赖都较少；大多基于reactstrap.v8，少部分基于material-ui.v4、bootstrap
    - 样式一般；更新不太频繁
    - 示例大多左边有，右边没有
  - https://themesberg.com/
    - https://github.com/themesberg
    - volt(react-bootstrap)
  - https://codedthemes.com/
    - https://github.com/codedthemes
    - berry(material-ui), datta-able(react-bootstrap)
  - https://flatlogic.com
    - https://github.com/flatlogic
    - 第三方依赖有点多；大多依赖reactstrap.v8
    - 示例大多左边没有，右边没有
    - 样式都很一般
  - https://startbootstrap.com/
    - https://github.com/StartBootstrap
    - SB Admin
  - https://themeforest.net/
  - https://keenthemes.com/
    - https://github.com/KeenthemesHub /无repos
  - https://github.com/puikinsh
    - 大多基于bootstrap，没有提供react版
  - https://github.com/uifort
    - 开源了多个主题，但作者弃更了
    - 依赖redux

- dashboards examples
  - [Bootstrap Themes](https://themes.getbootstrap.com/shop/?orderby=popularity)
  - https://www.admin-dashboards.com/
    - https://github.com/admin-dashboards
    - 只是自愿提交展示
  - https://appseed.us/app-generator
    - https://github.com/app-generator
# popular dashboards
- Volt Bootstrap 5 Dashboard
  - [free](https://demo.themesberg.com/volt/pages/dashboard/dashboard.html)
    - 左边不可折叠，右边有浮动面板
  - [pro($69)](https://demo.themesberg.com/volt-pro/pages/dashboard/dashboard.html)
    - 左边可折叠，右边没有浮动面板
  - https://github.com/themesberg/volt-react-dashboard
    - https://demo.themesberg.com/volt-react-dashboard/#/dashboard/overview
    - /372Star/MIT/202102/js
    - 依赖bootstrap.v5、@themesberg/react-bootstrap.v1.4、react-router、chartist、react-live、simplebar(scrollbar) 
    - /主题白色；dashboard + components + pages
    - Volt React is an extension of the popular react-bootstrap library and it is based on Bootstrap 5.
  - https://github.com/themesberg/volt-bootstrap-5-dashboard
    - /2.1kStar/MIT/202107/scss
    - 依赖bootstrap.v5、popperjs、chartist、simplebar、sweetalert2

- CoreUI Free Bootstrap Admin /10.5kStar/MIT/202012/pug
  - CoreUI offers 6 versions: Bootstrap, Angular, Laravel, React.js, Vue.js, and Vue.js + Laravel.
  - https://github.com/coreui/coreui-free-bootstrap-admin-template
    - [free](https://coreui.io/demo/free/)
    - [pro](https://coreui.io/demo/)
    - free bootstrap admin template
    - 左边可折叠，右边没有
  - https://github.com/coreui/coreui
    - https://coreui.io/docs/getting-started/theming/
    - 依赖perfect-scrollbar, @popperjs/core，免费版未提供其他theme
    - UI Kit built on top of Bootstrap 5 and plain JavaScript without any additional libraries like jQuery
    - CoreUI is the fastest way to build modern dashboard
    - Several of our components need the use of JavaScript to function. Specifically, they need our JavaScript plugins and Popper.js
- CoreUI Free React Admin /3.1kStar/MIT/202012/js
  - https://github.com/coreui/coreui-free-react-admin-template
    - [free](https://coreui.io/react/demo/free/)
    - [pro](https://coreui.io/react/demo/)
    - 左边侧边栏能折叠到只显示图标，右边可切换显示浮动设置面板
    - 但源码还未完全实现两侧功能
    - 依赖redux、chart.js；redux易去除
    - React admin template based on Bootstrap 5
  - https://github.com/coreui/coreui-react
    - 依赖coreui css,react-router-dom,perfect-scrollbar,@popperjs/core、Tippy.js,classnames
    - 用react hooks重写实现组件，只复用css
    - CoreUI for React.js replaces and extends the Bootstrap javascript. 
    - Components have been built from scratch as true React hook components, without jQuery and unneeded dependencies.
# BootstrapDash dashboards 
- 缺点
  - 左边侧边栏不能fixed，滚动过长时会消失
  - 第三方依赖过多，但这是复杂应用都会出现的问题
- 优点
  - 样式非常友好
  - 打包购买才$59，性价比爆炸

- react版dashboard开源的不多
  - [Purple-React 左可右浮动面板仅展示](https://www.bootstrapdash.com/demo/purple-react-free/template/demo_1/preview/dashboard)
  - [StarAdmin-Free-React-Admin-Template 左可右没有](https://www.bootstrapdash.com/demo/star-admin-free/react/template/demo_1/preview/dashboard)
    - https://github.com/BootstrapDash/StarAdmin-Free-React-Admin-Template
  - [corona-react-free-admin-template 左可右没有；dark](https://www.bootstrapdash.com/demo/corona-react-free/template/demo_1/preview/dashboard)
    - https://github.com/BootstrapDash/corona-react-free-admin-template
  - [connect-plus-react-free-admin-template 左可右没有；样式普通](https://bootstrapdash.com/demo/connect-plus-react-free/template/demo_1/preview/dashboard)
    - https://github.com/BootstrapDash/connect-plus-react-free-admin-template
  - [Stellar-React-Free-Admin-Template 左可右没有；样式普通](https://www.bootstrapdash.com/demo/stellar-react-free/template/demo_1/preview/dashboard)
    - https://github.com/BootstrapDash/Stellar-React-Free-Admin-Template
  - [Azia-Admin-React 非标准dashboard，类似nytimes](https://www.bootstrapdash.com/demo/azia-react-free/template/preview/dashboard)
    - https://github.com/BootstrapDash/Azia-Admin-React

- Purple Admin
  - [free](https://www.bootstrapdash.com/demo/purple-react-free/template/demo_1/preview/dashboard)
  - [pro($25)](https://www.bootstrapdash.com/demo/purple/react/template/demo_1/preview/dashboard)
  - https://github.com/BootstrapDash/Purple-React
    - 依赖react-bootstrap、bootstrap.v4、bosket(tree)、react-treebeard、canvasjs(charts)、i18next、react-ace、react-beautiful-dnd、react-c3js、react-chartjs-2、react-dnd、react-images、react-quill、react-router、react-simple-maps、react-simplemde-editor、react-table.v6、react-trello
    - 左边可折叠，右边有浮动面板但只展示
    - React.js version of popular admin template Purple Admin.
  - https://github.com/BootstrapDash/PurpleAdmin-Free-Admin-Template
    - https://www.bootstrapdash.com/demo/purple-admin-free/#
    - 右侧浮动面板未实现

- 左边可折叠，右边有浮动面板可设置颜色
  - 样式符合最新流行风格
  - 未实现react版本
- https://github.com/BootstrapDash/skydash-free-bootstrap-admin-template
  - https://bootstrapdash.com/demo/skydash-free/template/
  - 依赖jquery、quill、chart.js...
  - 样式非常友好，右边有浮动面板但只展示
- https://github.com/BootstrapDash/star-admin2-free-admin-template
  - https://www.bootstrapdash.com/demo/star-admin2-free/template/
  - 右边有浮动面板，能设置颜色
  - 主题深蓝较正式
- https://github.com/BootstrapDash/PlusAdmin-Free-Bootstrap-Admin-Template
  - https://www.bootstrapdash.com/demo/plus-free/template/demo_1/index.html
  - 右边有浮动面板，能设置颜色
- https://github.com/BootstrapDash/futureui-free-admin-bootstrap-template
  - https://www.bootstrapdash.com/demo/futureui-free/template/
  - 右边有浮动面板，能设置颜色

- 右边没有浮动面板
- https://github.com/BootstrapDash/MajesticAdmin-Free-Bootstrap-Admin-Template
  - https://www.bootstrapdash.com/demo/majestic-free/template/index.html
- https://github.com/BootstrapDash/Kapella-Free-Bootstrap-Admin-Template
  - https://www.bootstrapdash.com/demo/kapella-free/template/index.html
  - 全宽仪表板页面，没有左边和右边；样式友好
- https://github.com/BootstrapDash/SpicaAdmin-Free-Bootstrap-Admin-Template
  - https://www.bootstrapdash.com/demo/spica-free/template/index.html
- https://github.com/BootstrapDash/RoyalUI-Free-Bootstrap-Admin-Template
  - https://www.bootstrapdash.com/demo/royalui-free/template/index.html
  - 卡片直角
# WrapPixel dashboards
- Flexy
- https://github.com/wrappixel/flexy-react-lite
  - [free](https://www.wrappixel.com/demos/free-admin-templates/flexy-react-dashboard-lite/main/#/dashboards/dashboard1)
  - https://github.com/wrappixel/flexy-bootstrap-lite
  - 依赖material-ui.v5, emotion, apexcharts
  - 样式符合最新流行风格，超级友好
  - 左边不可折叠，右边没有

- Xtreme
- https://github.com/wrappixel/xtreme-react-lite
  - [free](https://wrappixel.com/demos/free-admin-templates/xtreme-reactadmin-lite/main/#/dashboard)
  - [pro](https://www.wrappixel.com/demos/react-admin-templates/xtreme-react-admin/main/dashboards/classic)
  - 依赖reactstrap.v8、history、chart.js
  - 提供了bootstrap版、react版、angular版
  - 左边可折叠，右边没有；样式还行
  - 左边侧边栏fixed
- https://github.com/wrappixel/xtreme-admin-lite
  - https://www.wrappixel.com/demos/free-admin-templates/xtreme-admin-lite/xtreme-html/ltr/
  - 左边可折叠，右边没有

- Ample
- https://github.com/wrappixel/ample-react-lite
  - https://wrappixel.com/demos/admin-templates/ampleadmin/ample-admin-lite/dashboard.html
  - 左边可折叠，右边没有；和xtreme类似
  - 左边侧边栏不能fixed

- Matrix
- https://github.com/wrappixel/matrix-admin-bt5
  - 左边可折叠；纯色块metro风格，样式普通

- more-dashboards
- https://github.com/wrappixel/materialpro-react-lite
  - https://wrappixel.com/demos/free-admin-templates/materialpro-reactadmin-lite/main/#/starter/starter
# creative tim dashboards
- tips
  - free版几乎都是 左边不可折叠，右边有浮动面板
  - pro 版几乎都是 左边可折叠，右边有浮动面板

- argon-dashboard
  - 生态最为丰富，还提供了next、nuxt等实现
  - 样式符合最新流行风格
  - [free](https://demos.creative-tim.com/argon-dashboard/examples/dashboard.html)
    - 左边不可折叠，右边没有浮动面板
  - [pro](https://demos.creative-tim.com/argon-dashboard-pro/pages/dashboards/dashboard.html)
    - 左边可折叠，右边没有
  - [free argon-design-system](https://demos.creative-tim.com/argon-design-system/)
    - design system based on Bootstrap 4.

- soft-ui-dashboard
  - 基于bootstrap5，暂时没有实现react版本
  - 样式符合最新流行风格，大量运用卡片，按钮有点浮雕凸起的效果
  - [free](https://demos.creative-tim.com/soft-ui-dashboard/pages/dashboard.html)
  - [pro](https://demos.creative-tim.com/soft-ui-dashboard-pro/pages/dashboards/default.html)
    - 实现不完美，折叠到图标的侧边栏因为部分文字过多就显示了水平滚动条
  - https://github.com/creativetimofficial/soft-ui-dashboard
    - Bootstrap 5 Dashboard
  - https://github.com/creativetimofficial/soft-ui-design-system
    - https://demos.creative-tim.com/soft-ui-design-system/index.html
    - Bootstrap 5 design system
  - https://github.com/creativetimofficial/soft-ui-react-native
    - app template built over React Native and Expo
  - paid
    - https://github.com/creativetimofficial/ct-soft-ui-design-system-pro
    - https://github.com/creativetimofficial/ct-soft-ui-dashboard-pro

- black-dashboard
  - [free](https://demos.creative-tim.com/black-dashboard/examples/dashboard.html)
  - [pro](https://demos.creative-tim.com/marketplace/black-dashboard-pro/examples/dashboard.html)

- now-ui-dashboard  
  - [free](https://demos.creative-tim.com/now-ui-dashboard/examples/dashboard.html)
  - [pro](https://demos.creative-tim.com/now-ui-dashboard-pro/examples/dashboard.html)

- light-bootstrap-dashboard
  - [free](https://demos.creative-tim.com/light-bootstrap-dashboard/examples/dashboard.html)
  - [pro](https://demos.creative-tim.com/light-bootstrap-dashboard-pro/examples/dashboard.html)

- material-dashboard
  - [free](https://demos.creative-tim.com/material-dashboard/examples/dashboard.html)
  - [pro](https://demos.creative-tim.com/material-dashboard-pro/examples/dashboard.html)

- paper-dashboard
  - 基于bootstrap3
  - [free](https://demos.creative-tim.com/bs3/paper-dashboard/dashboard.html)
  - [pro](https://demos.creative-tim.com/paper-dashboard-pro/examples/dashboard/overview.html)

- paper-dashboard-2
  - [free](https://demos.creative-tim.com/paper-dashboard/examples/dashboard.html)
  - [pro](https://demos.creative-tim.com/paper-dashboard-2-pro/examples/dashboard.html)

- vue-white-dashboard
  - [free](https://demos.creative-tim.com/vue-white-dashboard/#/dashboard)
  - [pro](https://demos.creative-tim.com/vue-white-dashboard-pro/#/dashboard)
