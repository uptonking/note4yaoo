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
# tailwind-ui
- https://github.com/htmlstreamofficial/preline /2kStar/MIT/202306/js
  - https://preline.co/examples.html
  - prebuilt UI components based on the utility-first Tailwind CSS
  - table示例元素丰富、色彩丰富、操作丰富
  - sidebar可多级
  - modal按钮位置多变，分隔线很少
  - 分隔线用的不多
  - [Application AI Prompt](https://preline.co/examples/application-ai-prompt.html)
  - [Fork from Flowbite. Shouldn't it be mentioned?](https://github.com/htmlstreamofficial/preline/issues/1)
    - I've taken a good look at Preline and I must say that as one of the founders of Flowbite I have found a whole lot of similarities
    - Of course the code is not exactly the same, but the whole concept of Preline seems VERY similar to Flowbite.
  - [Show HN: Preline UI – Open-Source Tailwind CSS Components | Hacker News_202207](https://news.ycombinator.com/item?id=31989062)
    - It looks good from a quick overview, but a look in the code base makes me question if I'd be able to use it in a React project
    - The dropdown component binds click/mousemove/keydown event handlers on the document element, but there's no method to remove such handlers. 
  - https://github.com/SynapseTech/preline-react /ts
    - Preline UI bindings for React
    - Preline already supports react, so why this?It does support react, but not very nicely.
  - https://github.com/rioarray/kumonos-ui /ts
    - Using Tailwind as CSS framework. Big thanks to Preline

- https://github.com/themesberg/flowbite /4.9kStar/MIT/202306/ts/组件超丰富
  - https://flowbite.com/blocks/
  - UI components based on the utility-first Tailwind CSS framework featuring dark mode support, a Figma design system, templates, and more.
  - 很多付费解锁，但可参考效果
  - 字体较大
  - All of the elements are built using the utility classes from Tailwind CSS and vanilla JavaScript with support for TypeScript.
  - Flowbite also offers an API for using the components programmatically with vanillajs
  - https://github.com/themesberg/flowbite-react /1.2kStar/MIT
    - https://www.flowbite-react.com/
    - Official React components built for Flowbite and Tailwind CSS
  - flowbite-repos
    - https://github.com/themesberg/flowbite-icons /MIT
    - https://github.com/themesberg/flowbite-react-admin-dashboard /MIT
      - admin dashboard interface built with Flowbite, React, and Tailwind CSS
      - react-sortablejs for Kanban-style boards found on Kanban page
    - https://github.com/themesberg/flowbite-admin-dashboard
      - https://flowbite-admin-dashboard.vercel.app/
      - admin dashboard template built with Tailwind CSS and Flowbite
    - https://github.com/themesberg/tailwind-landing-page
      - https://themesberg.github.io/tailwind-landing-page/
      - responsive landing page built with Tailwind CSS and Flowbite Blocks
    - https://github.com/themesberg/flowbite-typography
    - https://github.com/themesberg/tailwind-datatables
      - forked from https://github.com/DataTables/DataTablesSrc /jquery
    - https://github.com/themesberg/flowbite-vue
    - https://github.com/themesberg/flowbite-angular
- https://github.com/OMikkel/tailwind-datepicker-react
  - https://omikkel.github.io/tailwind-datepicker-react/
  - A tailwindcss/flowbite datepicker component built as a react component with types
  - Date logic from https://github.com/mymth/vanillajs-datepicker /js
- https://github.com/saiteja-madha/flowbite-admin-dashboard-nodejs
  - a fork of the original Flowbite Admin Dashboard repository. 
  - This fork is used to create a NodeJS version of the dashboard using Express and EJS as the templating engine.
- https://github.com/PrakasRavichandran/flowbite
  - https://flowbitereact.netlify.app/
  - Official React components built for Flowbite and Tailwind CSS

- https://github.com/MarsX-dev/floatui /2kStar/202306/js/非常简洁/已被收购
  - https://floatui.com/components
  - https://floatui.com/demo
  - responsive UI components and templates for React and Vue (soon) with Tailwind CSS.
  - 提供了components、templates、demo
  - sidebar元素丰富
  - table过于简单
  - card设计很烂

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
# popular
- https://github.com/xiaoluoboding/tailwind-pre-processor /202101/inactive
  - https://tailwind-pre-processor.vercel.app/
  - An implementation of tailwindcss using less/stylus/Sass/SCSS.

- https://github.com/nado1001/style-dictionary-tailwindcss-transformer
  - This is a plugin to generate the config of Tailwind CSS using Style Dictionary
  - Create an object for each theme, assuming that various customizations will be made in the configuration file.
  - [Tailwind format · amzn/style-dictionary](https://github.com/amzn/style-dictionary/issues/843)

- https://github.com/zvizvi/freewindcss /scss
  - https://codesandbox.io/s/freewindcss-pfq17e
  - Use Tailwind's set values and units in pure CSS variables

- https://github.com/fouita/tailwind-editor
  - https://editor-tw.fouita.com/
  - notion like tailwindcss editor built with svelte

- https://github.com/itaditya/tw-universal-tokens
  - https://tw-tokens.netlify.app/
  - Use Tailwind tokens as CSS variables, SASS map, SASS variables, ES module, JSON & Common JS module.
# style-dictionary
- https://github.com/StefanKandlbinder/styledictionarytailwindbridge /202212/ts
  - https://stylewind.netlify.app/
  - A Design System based on Style Dictionary Tokens, converted into TailwindCSS Objects, which are then imported into the tailwind.config.js.

- [RFC: What would you like to see in Style Dictionary 4.0? · amzn/style-dictionary](https://github.com/amzn/style-dictionary/issues/643)
  - Support for the W3C Design Token spec, specifically the `$value`
# tailwind-pure-css
- https://github.com/swlkr/totallycss
  - Like tailwind but with css variables.

- https://github.com/swkeever/tailwind-scss
  - Compiles Tailwind CSS default configuration into SASS variables.

- https://github.com/rahmanda/tailwindscss /201905/inactive
  - SCSS version of Tailwind CSS for people who don't use modern module bundler.
# more-tailwind
- https://github.com/zendeskgarden/tailwindcss
  - A Tailwind CSS plugin for generating CSS based on the Garden theme object.

- https://github.com/ernestoruperez/eo_design-tokens
  - This repository contains the files with the configuration of the Design Tokens for TailwindCSS and DaisyUI that can be used with Tokens Studio for Figma (Figma Tokens).
