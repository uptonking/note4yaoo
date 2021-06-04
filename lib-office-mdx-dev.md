---
title: lib-office-mdx-dev
tags: [lib, markdown, mdx]
created: '2021-05-27T01:41:58.386Z'
modified: '2021-06-02T16:45:56.858Z'
---

# lib-office-mdx-dev

> easy to read， easy to write， content-centric notebook

# guide
- mdx-features
  - markdown-based simplicity
  - powerful jsx with large ecosystem
  - everything is a component
    - import jsx components and render components
  - customizable: 可通过MDXProvider替换h1、p
  - blazing fast: MDX has no runtime, all compilation occurs during the build stage.

- mdx-cons
  - *控制布局、动态修改更新布局*
    - 不建议提供过多定制样式的能力，不方便迁移
    - 建议后期使用block editor配置布局
  - 服务器接收到mdx文件内容的字符串后，应该如何渲染
    - 使用runtime按需渲染

- goals
  - 易读易写
  - 上传mdx(到数据库的字段)，能够渲染出html(~~应该是ssr吧~~)
  - 能够在渲染的页面编辑mdx
  - 能够在渲染的页面编辑ojs

- is-goal???
  - 导出的使用场景，docx/pptx哪个多一点，office标准的ooxml格式规定了很多属性和配置，在设计实现导出时要参考的
  - 样式丰富的图表、地图很难通过文本表达，通过WYSIWYG能实现，此时编辑器最好是block的，可作为后期目标

- non-goals(难用简单文本实现)
  - 不建议定制各种组件的各种样式细节，样式越多输出的代码就越多，就显得凌乱且难迁移；
    - 提前告知用户，支持保存到本地的文件形式有3种，
    - 一种只包含少量基本样式，但易迁移、可跨平台设备查看
    - 一种包含丰富样式但代码乱，且**以后迁移跨应用可能失败**
    - 一种导出office，支持导出的组件有限、样式有限，平台自定义的组件和样式都不会导出
  - 导出高级组件：图表的代码；嵌入的视频
  - 不要执着于定制自己的mdx的解析器和渲染实现
    - mdx大部分的规则都是兼容markdown的，所以可以考虑扩展markdown流行的工具库，如showdown、json2md(无md依赖)、@moox/markdown-to-json(remark)、@dimerapp/markdown(remark)、md-2-json(marked)、jdown(marked)

- mdx编辑器：3种输入模式(参考vditor)
  - 要支持输出html/json/.md文本
    - 注意html和md有第三方的转换工具，要考虑是转换而来还是直接获取输入的文本
  - (1)输入使用文本编辑器分屏预览SV，不适合做成block editor的形式，输出适合使用.md文本，输出json也容易
  - (2)输入使用所见即所得编辑器WYSIWYG，非常适合做成block style editor，输出适合使用json而不是.md文本
  - (3)输入使用即时渲染IR，在WYSIWYG实时预览的基础上添加输入标志文本的shortcut，能够减少鼠标操作
  - (4)后期可在WYSIWYG的基础上，扩展工具条为block editor的配置工具

- 如何在mdx中支持observable javascript(.ojs)
  - 方法1: 直接将字符串写在js变量中，也有人尝试htm tag模版函数
    - 优点：实现简单，方便测试
    - 缺点：字符串不适合复杂代码的自动补全和高亮
  - 方法2: 扩展code block，添加 meta string
    - 优点：书写简单；直接支持语法高亮，执行时仍然是获取并解析字符串
    - 优点2: 普通markdown渲染器能正常渲染代码块
    - 缺点：需要实现自动补全提示等
  - 方法3: 基于react-live，(~~无法~~)提供ojs专门的文本编辑器，执行时仍然是获取并解析字符串
    - 优点：充分利用react-live的预览功能，上面预览，下面代码，与observablehq的体验最接近
    - 缺点：不容易书写；复杂度高、链路长，修改ojs需要执行ojs编译器、rect-live计算、mdx热加载
    - 缺点2: react-live编辑的是react组件，无法直接支持编辑字符串
      - 只能再一次实现类似ojs编译器的转换器，将输入的字符串通过反射封装成函数，自动调用此函数返回输入的字符串ojs
      - 可在后期实现第(4)种编辑器时实现

- tips
  - mdx的解析，参考remark-parse, mdxc
  - mdx的渲染基于 mdx/jsx字符串 -> react组件 -> dom
  - load
    - build time
    - runtime

- ref
  - wikipedia的书写设计
  - [@mdx-js/loader vs @mdx-js/mdx vs @mdx-js/react vs xdm](https://www.npmtrends.com/@mdx-js/loader-vs-@mdx-js/mdx-vs-@mdx-js/react-vs-xdm)
  - @mdx-js/mdx和xdm都依赖 remark-parse、remark-rehype的unified生态，还依赖 vfile、estree-walker
# faq-not-yet

## remark vs markdown-it

- ### [Consider remark for markdown in svelte](https://github.com/pngwn/MDsveX/issues/20)
- The decision to use markdown-it was relatively arbitrary when I put this together initially
  - the performance was okay and there are a decent array of plugins.
  - I've found it pretty annoying over time, however, and have been investigating alternatives.
- marked is the obvious candidate due to its focus on performance
  - but there don't seem to be as many plugins
- remark was my initial preference but I assumed (without any testing whatsoever) that it would be quite a bit slower due to the fact it builds an AST
  - there are a huge array of plugins available and having access to an AST gives a huge amount of flexibility when it is needed.
  - remark will almost definitely have higher memory consumption than a simple lexer/parser with no intermediary AST 
  - but this seems to be a trade-off that people are willing to make. 
  - There is precedent here as MDX uses Remark and no-one seems to mind much, although what is palatable to one community is not necessarily so for another.

## 如何在.mdx文件中动态导入npm仓库中的js库？

- 若只是动态获取和解析mdx，则参考官方提供的@mdx-js/runtime

- 若通过传统的`<script>`，导入的依赖其实会在浏览器中变成全局依赖，挂再到浏览器的`window`上
- 在.mdx文件中书写`import { useTable } from 'react-table'`时，会由webpack处理
- 若在mdx中import没有预先打包进bundle的库，会提示`Component Checkbox was not imported, exported, or provided by MDXProvider as global scope`
  - 需要预先提供到 MDXProvider
  - 或者修改runtime，动态添加新的库

- ### 尝试解决此问题的参考方案
- observable-notebook支持d3.require和import(url)
- https://github.com/hashicorp/next-mdx-remote
  - 支持获取远程mdx文本内容和动态数据
  - The file content must be local.
  - You are bound to filesystem-based routing. 
  - You will end up running into performance issues. 
  - You will be limited in the ways you are able to structure relational data.
- https://github.com/kentcdodds/mdx-bundler
  - 支持获取远程mdx文本内容
  - The problem: You have a string of MDX and various TS/JS files that it uses and you want to get a bundled version of these files to eval in the browser.
  - next-mdx-remote is not a bundler, it's just a compiler. 
  - mdx-bundler is an MDX compiler and bundler.
  - Webpack/rollup/etc also require that all your MDX files are on the local filesystem to work.
  - mdx-bundler can definitely be used at build-time, but it's more powerfully used as a runtime bundler.
  - You might decide to go with a built-time approach (for Gatsby/CRA), but as mentioned, the true power of mdx-bundler comes in the form of on-demand bundling. 
  - So it's best suited for SSR frameworks like Remix/Next.

## [MDX performance](https://github.com/mdx-js/mdx/issues/1152)

- Numerous babel parse and transformation steps
  - Imports and exports
  - Shortcode generation
  - mdxType

- Returning a compiled string that inevitably needs to be transpiled
# ref
- [Markdown 解析原理详解和 Markdown AST 描述](https://ld246.com/article/1587637426085)
  - [Lute 实现后记](https://ld246.com/article/1567062979327)
