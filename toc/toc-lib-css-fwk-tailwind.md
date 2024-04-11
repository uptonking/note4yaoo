---
title: toc-lib-css-fwk-tailwind
tags: [css-framework, css-vars, tailwindcss]
created: 2023-02-26T18:24:02.955Z
modified: 2023-02-26T18:25:01.328Z
---

# toc-lib-css-fwk-tailwind

# guide

- tips
  - 重点组件: card, table, form

- ui-references
  - https://floatui.com/components
  - https://preline.co/examples.html
  - https://flowbite.com/blocks/
  - https://tailwindui.com/components /很多分隔线
  - https://merakiui.com/components

- dashboard-demos
  - flowbite-admin、windster
  - react-admin、material
  - tremor

- tailwind-css-classes
  - [Tailwind CSS Cheat Sheet - Flowbite](https://flowbite.com/tools/tailwind-cheat-sheet/)
# preline
- design-tokens-from-figma 从figma中找token太慢了，直接在demo中找
  - brand-color用的blue-600
  - 文章内容的颜色 gray-800 #1f2937
  - 暗色内容的颜色
    - demo中是gray-600 #4b5563
    - 设计稿中是slate-600 #475569
  - 默认border是gray-200 #e5e7eb
  - input中提交按钮背景色默认blue-500
  - palette
    - Fuchsia: 50-#fdf4ff 100-#fae8ff 500-#d946ef 600-#c026d3 700-#a21caf 800-#86198f 900-#701a75

- https://github.com/htmlstreamofficial/preline /3.4kStar/MIT/202401/ts
  - https://preline.co/examples.html
  - prebuilt UI components based on the utility-first Tailwind CSS
  - 分隔线用的不多
  - table示例元素丰富、色彩丰富、操作丰富
  - sidebar可多级
  - modal按钮位置多变，分隔线很少
  - icon直接用的svg+path，不方便复用
  - dark mode暂不支持
  - [Application AI Prompt](https://preline.co/examples/application-ai-prompt.html)
  - [Application Form Layouts](https://preline.co/examples/application-form-layouts.html)
  - [Application Layouts](https://preline.co/examples/layouts-application.html)
  - [Blog Articles](https://preline.co/examples/blog-articles.html)
  - [Fork from Flowbite. Shouldn't it be mentioned? _202206](https://github.com/htmlstreamofficial/preline/issues/1)
    - I've taken a good look at Preline and I must say that as one of the founders of Flowbite I have found a whole lot of similarities
    - Of course the code is not exactly the same, but the whole concept of Preline seems VERY similar to Flowbite.
  - [Show HN: Preline UI – Open-Source Tailwind CSS Components | Hacker News_202207](https://news.ycombinator.com/item?id=31989062)
    - It looks good from a quick overview, but a look in the code base makes me question if I'd be able to use it in a React project
    - The dropdown component binds click/mousemove/keydown event handlers on the document element, but there's no method to remove such handlers. 
  - Is Preline UI Figma Free?
    - Yes, it's free for both commercial and personal use.

- https://github.com/SynapseTech/preline-react /ts
  - Preline UI bindings for React
  - Preline already supports react, so why this? It does support react, but not very nicely.

- https://github.com/rioarray/kumonos-ui /ts
  - Using Tailwind as CSS framework. Big thanks to Preline

- https://github.com/kodkafa/reform
  - React Hook Form + Yup + Tailwind
  - Tailwind is optional. And you can use Preline UI too.

- https://github.com/matteopolak/preline-svelte
  - A Svelte implementation of the Preline component library

- https://github.com/kyooowe/PineUI /ts/mern
  - https://home-two-ebon.vercel.app/
  - Boilerplate using TurboRepo, Vite, React, and Express. Provides a fast and efficient setup for building modern web apps.
  - 前端依赖react-popper、preline、zustand、tanstack-query.v4、formik、framer-motion、jsonwebtoken、recharts
  - 后端依赖express、mongoose
# flowbite
- https://github.com/themesberg/flowbite /4.9kStar/MIT/202306/ts/组件超丰富
  - https://flowbite.com/blocks/
  - https://flowbite.com/application-ui/demo/
  - UI components based on the utility-first Tailwind CSS framework featuring dark mode support, a Figma design system, templates, and more.
  - 字体较大，图标线条粗、颜色深
  - 很多付费解锁，但可参考效果
  - All of the elements are built using the utility classes from Tailwind CSS and vanilla JavaScript with support for TypeScript.
  - Flowbite also offers an API for using the components programmatically with vanillajs
  - The preferred way to use the interactive UI components from Flowbite is via the `data-*` attributes interface which allows us to add functionality via the HTML element attributes and most of the examples on our documentation applies this strategy.
  - [Sidenav - Flowbite](https://flowbite.com/blocks/application/sidenav/)
  - [Blog Templates - Flowbite](https://flowbite.com/blocks/publisher/blog-templates/)
  - [Update Forms (CRUD) - Flowbite](https://flowbite.com/blocks/application/crud-update-forms/)

- https://github.com/themesberg/flowbite-react /1.2kStar/MIT
  - https://www.flowbite-react.com/
  - Official React components built for Flowbite and Tailwind CSS

- https://github.com/themesberg/flowbite-icons /MIT
  - https://flowbite.com/icons/
  - 可调整粗细

- https://github.com/themesberg/flowbite-admin-dashboard /js
  - https://flowbite-admin-dashboard.vercel.app/
  - admin dashboard template built with Tailwind CSS and Flowbite
- https://github.com/themesberg/flowbite-react-admin-dashboard /MIT/ts
  - admin dashboard interface built with Flowbite, React, and Tailwind CSS
  - 依赖react-sortablejs(kanban)、apexcharts
- https://github.com/themesberg/tailwind-dashboard-windster /绿色系/白色主题
  - https://demo.themesberg.com/windster/
  - https://demo.themesberg.com/windster-pro/kanban/
  - admin dashboard interface built on top of Tailwind CSS and Flowbite
- https://github.com/mo3id/dashboard
  - https://dashboard-mo3id.vercel.app/
  - 简化版

- https://github.com/themesberg/tailwind-landing-page
  - https://themesberg.github.io/tailwind-landing-page/
  - responsive landing page built with Tailwind CSS and Flowbite Blocks
  - https://github.com/asx-dev/flowbite-clone
    - Flowbite website clone using Tailwind CSS components.

- https://github.com/themesberg/flowbite-typography
- https://github.com/themesberg/tailwind-datatables
  - forked from https://github.com/DataTables/DataTablesSrc /jquery

- flowbite-creator-repos
  - https://github.com/themesberg/flowbite-vue
  - https://github.com/themesberg/flowbite-angular

- https://github.com/OMikkel/tailwind-datepicker-react
  - https://omikkel.github.io/tailwind-datepicker-react/
  - A tailwindcss/flowbite datepicker component built as a react component with types
  - Date logic from https://github.com/mymth/vanillajs-datepicker /js

- https://github.com/saiteja-madha/flowbite-admin-dashboard-nodejs
  - a fork of the original Flowbite Admin Dashboard repository. 
  - This fork is used to create a NodeJS version of the dashboard using Express and EJS as the templating engine.
  - https://github.com/themesberg/flowbite-express
    - EJS/PUG/HBS

- https://github.com/PrakasRavichandran/flowbite
  - https://flowbitereact.netlify.app/
  - Official React components built for Flowbite and Tailwind CSS

- https://github.com/PreetiToppo/Kanban-Board /js/完成度高
  - https://kanban-board-blond-nine.vercel.app/
  - Kanban board web application built with React and styled using Tailwind CSS
  - 依赖flowbite-react、framer-motion、react-beautiful-dnd
  - https://github.com/VishalBhuse/KanBan /与上面一样
    - https://kan-ban.vercel.app/

- https://github.com/AliBagheri2079/Dashboard-ReactTS-Tailwind-ReactSuite-Emotion-Vite
  - Dashboard template/boilerplate built with React/TS (Vite), ReactSuite

- https://github.com/Somanyu/tailwind-flowbite-template /js
  - ReactJS application that demonstrates a suggested project structure

- https://github.com/MiroslavPetrik/form-atoms-field
  - https://miroslavpetrik.github.io/form-atoms-field/
  - Declarative & headless form fields build on top of jotai & form-atoms
  - https://github.com/jaredLunde/form-atoms
    - Atomic form primitives for Jotai
  - https://github.com/MiroslavPetrik/form-atoms-flowbite
    - Next-generation atomic form fields for Flowbite React
  - https://github.com/MiroslavPetrik/form-atoms-chakra-ui

- https://github.com/odu-emse/emse-UI
  - https://emse-ui.pages.dev/
  - The component library to be used in the Async Portal at EMSE

- https://github.com/JessicaaSun/istademy-ui /js
  - https://istademy-ui.vercel.app/
  - 落地页、体验好、粉色系

- https://github.com/abrahamemamani/file-manager /ts/白色系/简洁
  - https://file-manager-lilac.vercel.app/
  - 不支持列表视图

- https://github.com/atefkbenothman/strava-ui
  - a web app that enhances your strava experience by providing a user-friendly interface for viewing your activity data, stats, and local segments.
  - next.js, tailwind, mapbox, redis, flowbite, chart.js

- https://github.com/MehediHasanNabil/research-ecommerce-project /js
  - https://e-commerce-88f93.web.app/
  - Research ecommerce project using MERN stack

- more-flowbite
  - https://github.com/AndreasKarz/ReactStarterTemplate
  - https://github.com/rival-politics/rival-politics-core-ui
# tailwind-ui
- refs
  - [Tailwind Toolbox - Free Starter Templates](https://www.tailwindtoolbox.com/starter-templates)

- https://github.com/MarsX-dev/floatui /2kStar/202306/js/非常简洁/已被收购
  - https://floatui.com/components
  - https://floatui.com/demo
  - responsive UI components and templates for React and Vue (soon) with Tailwind CSS.
  - 提供了components、templates、demo
  - sidebar元素丰富
  - table过于简单
  - card设计很烂
  - demos-落地页
    - [Blinder 白色简洁](https://blinder-nine.vercel.app/)
    - [IO Academy 黑色简洁](https://ioacademy.vercel.app/)
    - [Mailgo 黑色glassmorphism](https://mailgo-rho.vercel.app/)
    - [Starboard 白色普通](https://starboard-one.vercel.app/)
    - [Split 白色普通](https://split-xi.vercel.app/)

- https://github.com/merakiui/merakiui /2kStar/202212/css/inactive
  - https://merakiui.com/components
  - Tailwind CSS components that support RTL languages & fully responsive based on Flexbox & CSS Grid with elegant Dark Mode

- https://github.com/TailGrids/tailwind-ui-components /588Star/202301/css
  - https://tailgrids.com/components
  - 500+ free & premium Tailwind CSS UI components

- https://github.com/Siumauricio/rippleui /620Star/202305
  - https://ripple-ui.com/
  - modern and beautiful Tailwind CSS components.

- https://github.com/sailboatui/sailboatui /760Star/202302
  - https://sailboatui.com/
  - modern UI component library for Tailwind CSS

- https://github.com/saadeghi/daisyui
  - https://daisyui.com/components/
  - The most popular, free and open-source Tailwind CSS component library

- https://shuffle.dev/
  - Shuffle gives you 8, 000+ fully responsive UI components 

- https://github.com/konstaui/konsta
  - https://konstaui.com/
  - Mobile UI components made with Tailwind CSS
  - All Konsta UI components come with pixel perfect native-like iOS and Material Design themes
  - Konsta UI mostly designed to be used with "parent" frameworks like Ionic or Framework7.
# tailwind-dashboard
- https://github.com/cruip/tailwind-dashboard-template /js
  - https://cruip.com/
  - free admin dashboard template built on top of Tailwind CSS and fully coded in React

- https://github.com/horizon-ui/horizon-ui-chakra /js/白色主题
  - https://horizon-ui.com/horizon-ui-chakra/
  - https://horizon-ui.com/chakra-pro/
  - Admin Template for Chakra UI & React

- https://github.com/devias-io/material-kit-react
  - https://material-kit-react.devias.io/
  - https://material-kit-pro-react.devias.io/dashboard
  - 白色主题

- https://github.com/TailAdmin/tailadmin-free-tailwind-dashboard-template
  - https://tailadmin.com/
  - free Tailwind CSS admin template that is perfect for creating data-rich backends, powerful web applications and dashboard-admin projects.
# tailwind-tokens
- https://github.com/xiaoluoboding/tailwind-pre-processor /202101/inactive
  - https://github.com/xiaoluoboding/tailwind-pre-processor/blob/master/assets/styles/sass/config.scss
  - https://tailwind-pre-processor.vercel.app/
  - An implementation of tailwindcss using less/stylus/Sass/SCSS.

- https://github.com/zvizvi/freewindcss /scss
  - https://codesandbox.io/s/freewindcss-pfq17e
  - Use Tailwind's set values and units in pure CSS variables

- [Default config for Tailwind CSS in Figma Tokens format(.json)](https://gist.github.com/yuheiy/e1fc01fc0a4816924d1959221fdba46c)
- [Tailwind CSS default colors in Palettte.app's JSON format](https://gist.github.com/michaelroper/1bbe2232fc49eddac672803e0c4ba813)

- https://github.com/itaditya/tw-universal-tokens /202101/js/inactive/输出了json
  - https://tw-tokens.netlify.app/
  - Use Tailwind tokens as CSS variables, SASS map, SASS variables, ES module, JSON & Common JS module.
  - 依赖style-dictionary.v2, tailwindcss.v2

- https://github.com/ajmalafif/tailwind-to-style-dictionary
  - pull Tailwind's full default config and transform them into a format that Figma Tokens can consume.

- https://github.com/nado1001/style-dictionary-tailwindcss-transformer
  - This is a plugin to generate the config of Tailwind CSS using Style Dictionary
  - Create an object for each theme, assuming that various customizations will be made in the configuration file.
  - [Tailwind format · amzn/style-dictionary](https://github.com/amzn/style-dictionary/issues/843)

- https://github.com/fouita/tailwind-editor
  - https://editor-tw.fouita.com/
  - notion like tailwindcss editor built with svelte

- https://github.com/StefanKandlbinder/styledictionarytailwindbridge /202212/ts
  - https://stylewind.netlify.app/
  - A Design System based on Style Dictionary Tokens, converted into TailwindCSS Objects, which are then imported into the tailwind.config.js.

- [RFC: What would you like to see in Style Dictionary 4.0? · amzn/style-dictionary](https://github.com/amzn/style-dictionary/issues/643)
  - Support for the W3C Design Token spec, specifically the `$value`
- [Using Style Dictionary to transform Tailwind config into SCSS variables, CSS custom properties, and JavaScript via design tokens - DEV Community](https://dev.to/philw_/using-style-dictionary-to-transform-tailwind-config-into-scss-variables-css-custom-properties-and-javascript-via-design-tokens-24h5)
  - https://github.com/ajmalafif/tailwind-to-style-dictionary
- [Any wait to generate a full JSON of tailwind?](https://www.reddit.com/r/tailwindcss/comments/usnnw7/any_wait_to_generate_a_full_json_of_tailwind/)
  - I didn't know about that `npx tailwindcss init -full` generates a 955 line file.
  - [Syncing Design Tokens with Tailwind CSS theme - DEV Community](https://dev.to/ainatenhi/syncing-design-tokens-with-tailwind-css-theme-4d4d)

- https://github.com/tokens-studio/plugin-example-tailwindcss
  - This example illustrates how you can transform your tokens stored on Figma Tokens (with GitHub sync enabled) to be automatically transformed with token-transformer and Style Dictionary to a TailwindCSS environment with multiple themes.
  - https://github.com/tokens-studio/figma-plugin
    - Official repository of the plugin 'Tokens Studio for Figma' (Figma Tokens)
    - Token Transformer: Converts tokens from Tokens Studio for Figma to something **Style Dictionary** can read, removing any math operations or aliases, only resulting in raw values. 

- https://github.com/dobromir-hristov/tailwindcss-export-config /js
  - Export Tailwindcss config options to SASS, SCSS, LESS, and Stylus variables.
# tailwind-pure-css
- https://github.com/swlkr/totallycss
  - Like tailwind but with css variables.

- https://github.com/swkeever/tailwind-scss /202110/js/inactive
  - Compiles Tailwind CSS default configuration into SASS variables.

- https://github.com/rahmanda/tailwindscss /201905/inactive
  - SCSS version of Tailwind CSS for people who don't use modern module bundler.
# more-tailwind
- https://github.com/zendeskgarden/tailwindcss
  - A Tailwind CSS plugin for generating CSS based on the Garden theme object.

- https://github.com/ernestoruperez/eo_design-tokens
  - This repository contains the files with the configuration of the Design Tokens for TailwindCSS and DaisyUI that can be used with Tokens Studio for Figma (Figma Tokens).
