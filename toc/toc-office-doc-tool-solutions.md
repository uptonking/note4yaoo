---
title: toc-office-doc-tool-solutions
tags: [documentation, solutions, toc, tool]
created: 2020-10-13T09:15:27.625Z
modified: 2021-07-21T18:07:43.056Z
---

# toc-office-doc-tool-solutions

# guide

- 要在功能丰富和轻量方便间折中，过重的编辑器就偏向于在线ide了
- write with markdown
- render to html

- ref
  - [top documentation-tool](https://github.com/topics/documentation-tool?o=desc&s=stars)
  - [Unminify JS, CSS, HTML，支持大文件](https://www.unminify2.com/)
# markdown-based docs
- https://github.com/docsifyjs/docsify
  - /15.3kStar/MIT/202010/js
  - 依赖marked、prismjs
  - A magical documentation site generator.
  - No statically built html files, Support SSR, Support embedded files
    - there is literally no build step
    - unlike many static generators no HTML static site is created... update the Markdown and the site immediately shows those changes.
  - Useful plugin API, Smart full-text search plugin
  - Docsify is way way easier, probably because all the “build” stuff is happening via the javascript in realtime. 
  - https://github.com/jhildenbiddle/docsify-themeable
    - simple theme system for docsify.js
  - used-by
    - https://shoelace.style/
    - https://imdone.io/docs/

- https://github.com/callstack/component-docs /120Star/MIT/202011/ts
  - Simple documentation for your React components.
  - `pages (required)`: An array of items or a function returning an array of items to show as pages
  - component-docs is used for [react-native-paper](https://callstack.github.io/react-native-paper/)
  - 左侧目录支持折叠和多级目录
  - 没有实现当前页的toc
  - features
    - minimal configuration
    - fully static, deployable on GitHub pages
    - both server + client routing
    - hot reload
    - supports tsx/jsx/md/mdx
    - Support including markdown from a file reference in markdown files

- https://github.com/facebook/docusaurus
  - /19.5kStar/MIT/202010
  - 不依赖nextjs
  - 使用webpack+babel打包
  - Docusaurus 1 used to be a pure documentation site generator. 
  - In Docusaurus 2, we rebuilt it from the ground up, allowing for more customizability 
    - but preserved the best parts of Docusaurus 1 - easy to get started, versioned docs, and i18n
    - While our main focus will still be helping you get your documentations right and well, 
    - it is possible to build any kind of website using Docusaurus 2 as it is just a React application. 
    - Docusaurus can now be used to build any website, not just documentation websites.
  - Gatsby does many things well and is suitable for building many types of websites. 
    - GraphQL is also pretty core to Gatsby
  - Docusaurus tries to do one thing super well - be the best tool for writing and publishing content.
  - In comparison with statically generated HTML and interactivity added using `<script />` tags, Docusaurus sites are React apps. 
  - ref
    - https://github.com/ThinkBucket/docsite

- https://github.com/shuding/nextra
  - 依赖next、nextra-core、react
  - powerful and flexible site generation framework with everything you love from Next.js.
  - Any change to example/docs will be re-rendered instantly.
  - Nextra first collects all your Markdown files and configurations from the pages directory, and then generates the “page map information” of your entire site, to render things such as the navigation bar and sidebar 
    - By default, the page map contains all .md and .mdx filenames and the directory structure, sorted alphabetically.
    - You can have an `_meta.json` file in each directory, and it will be used to override the default configuration of each page

- NextBook /168Star/MIT/202206/js/inactive
  - https://github.com/amiroff/NextBook
  - https://next-book.vercel.app/
  - 依赖 next11、next-mdx-remote、react、remark、tailwindcss
  - 若屏幕很窄，官方文档会显示水平滚动条，此时滚动会有严重的漂移感
  - easy way to build technical books or documentation with markdown or MDX

- https://github.com/honkit/honkit /2.7kStar/apache2/202308/ts/gitbook
  - building beautiful books using Markdown - Fork of GitBook(legacy)
  - honkit is a command line tool (and Node.js lib) for building beautiful books using GitHub/Git and Markdown (or AsciiDoc).
  - 依赖immutable3.8、nunjucks、chokidar、commander、i18n-t、htmlparser2
  - GitBook is only free for open-source and non-profit teams.

- https://github.com/ryanlelek/Raneto /202208/js
  - https://docs.raneto.com/
  - Markdown powered Knowledgebase Wiki for Node.js
  - 比较典型的问答型知识库
  - Raneto is a "flat file" CMS, meaning no database problems, no MySQL queries, nothing.
  - Full-text search powered by Lunr

- https://github.com/metalsmith/metalsmith /7.8kStar/MIT/202304/js/代码量少
  - https://metalsmith.io/docs/getting-started
  - simple, pluggable static site generator.
  - all of the logic is handled by plugins. You simply chain them together.

- https://github.com/chrisdiana/cms.js /3kStar/MIT/202103/js/NoDeps/inactive
  - CMS.js is a fully Client-side, JavaScript Markdown Site generator in the spirit of Jekyll that uses plain ol' HTML, CSS and JavaScript to generate your website. 
  - CMS.js is like a file-based CMS. It takes your content, renders Markdown and delivers a complete website in Single-Page App
  - CMS.js supports two website modes, Github and Server. 
  - [Server Mode](https://github.com/chrisdiana/cms.js/wiki/Server-Mode)
    - In Server mode, CMS.js takes advantage of the Server's Directory Indexing feature. 
    - By allowing indexes, CMS.js sends an AJAX call to your specified folders and looks for Markdown or HTML files

- https://github.com/plantain-00/simple-doc
  - A Server-less and Build-less markdown document application.
  - 默认显示README.md

- https://github.com/wechatsync/Wechatsync
  - 一键同步文章到多个内容平台，支持今日头条、WordPress、知乎、简书、掘金
# doc-solution-catalog
- helpkb /8Star/MIT/202208/js
  - https://github.com/mrvautin/helpkb
  - https://docs.helpkb.org/
  - https://openkb.markmoffat.com/
  - 后端依赖 express、sequelize、gray-matter
  - 前端依赖 nextjs、react-bootstrap、react-markdown、sharp处理图片
  - helpkb is an open-source Next.js knowledge base or FAQ which is super fast, easy to use and quick to develop.
  - You need a Database for your data. You can use either postgres (recommended), mysql2, mariadb, sqlite3 or mssql.

- https://github.com/mrvautin/squido /js
  - https://squido.markmoffat.com/
  - A dead-simple no-code static HTML website generator
  - With Jamstack, the entire website is prebuilt into highly optimized static pages and assets during the build process.
  - Use Handlebars, EJS or Pug template engines.
  - Posts or Pages are written in Markdown format which is easy to learn and faster to write.
  - Standard website essentials: SEO, Sitemap, Social sharing friendly, Works on desktop and mobile (responsive)

- https://github.com/codex-team/codex.docs /apache2/202212/ts/inactive
  - https://docs.codex.so/
  - a free docs application. It's based on Editor.js ecosystem
  - Docs nesting — create any structure you need
  - Misprints reports to the Telegram / Slack

- https://github.com/ccontrols/component-controls
  - https://component-controls.com/
  - A next-generation tool to create blazing-fast documentation sites.
  - Using MDX or javascript to author documentation files
  - 依赖theme-ui
  - 左侧目录，右侧可高亮书签toc
- https://github.com/josemarluedke/docfy
  - https://docfy.dev/docs/getting-started/
  - Docfy is a modular JavaScript tool to help build documentation sites. 
  - Its core has all the essential features to help you create a full-featured docs app while writing all your content in Markdown.
  - core依赖remark-gfm
  - 给的示例基于ember
- https://github.com/YvesCoding/rcpress
  - /160Star/MIT/202008
  - 基于react、Ant Design的静态文档生成器
  - 配置，代码模仿自VuePress
  - 依赖@hot-loader/react-dom、@loadable/babel-plugin、prism-react-renderer

- https://github.com/palantir/documentalist
  - /125Star/Apache2/202010
  - 依赖kss(a documentation syntax for CSS)、marked、typedoc
  - A sort-of-static site generator optimized for living documentation of software projects.
  - Documentalism is a two-step process: Get the data, Render the data.
  - compiler is an extensible solution to step 1: get all your data in one place, in a consistent format. 
- https://github.com/styleguidist/react-styleguidist
  - /9.2kStar/MIT/202009
  - Isolated React component development environment with a living style guide
- https://github.com/interactivethings/catalog
  - /1.4kStar/BSD/202010/js
  - 依赖react-router、marked、prismjs
  - create beautiful living and fully interactive style guides using Markdown and React components.
  - 使用代码块里的预定义结构来渲染table，将会list形式的文字渲染成table
- https://github.com/Redocly/redoc
  - /11.7kStar/MIT/202012/ts
  - OpenAPI/Swagger-generated API Reference Documentation
- https://github.com/benjycui/bisheng
  - /2.5kStar/MIT/202012/js/react
  - 依赖mark-twain、react-router、webpack、prismjs
  - transform Markdown(and other static files with transformers) into static websites and blogs using React.

- https://github.com/zmister2016/MrDoc
  - http://mrdoc.zmister.com/project-20/
  - MrDoc是基于Python开发的在线文档系统，适合作为个人和小型团队的私有云文档、云笔记和知识管理工具
  - 后端：Python + Django
  - 前端：LayUI + JQuery

- https://github.com/huangwei9527/Ink-wash-docs /511Star/apache2/202010/js/vue2
  - 基于egg+vue开发的在线文档管理平台，支持markdown文档， excel文档
  - 工作台|文档列表、文档编辑预览（支持：md， excel，html产品原型托管）、协作编辑、访问权限设置
  - 依赖vditor、x-data-spreadsheet、vue2、vuex3、element-ui2、egg2

- https://github.com/jxnblk/mdx-deck
  - /9.6kStar/MIT/202004
  - 依赖gatsby
  - React MDX-based presentation decks
- https://github.com/doczjs/docz
  - /19.4kStar/MIT/202005
  - 依赖gatsby、marksy、@mdx-js/react
  - quickly create live-reloading, seo-friendly, production-ready documentation sites with MDX and customize the look, feel and behavior by leveraging GatsbyJS and Gatsby theme shadowing.
- https://github.com/gatsbyjs/gatsby
  - /47.4kStar/MIT/202010
  - Gatsby is a free and open source framework based on React that helps developers build blazing fast websites and apps
  - GraphQL is also pretty core to Gatsby, although you don't necessarily need GraphQL to build a Gatsby site
- https://github.com/react-cosmos/react-cosmos
  - /6.5kStar/MIT/202010/ts
  - An isolated component environment
  - Simple, detail-oriented and battle-tested
  - React Cosmos is not a style guide generator
- https://github.com/sourcejs/Source
  - /inactive
  - Living Style Guides Engine and Maintenance Environment for Front-end Components.
  - Today, the ideas SourceJS surfaced are evolving in other open source projects, like styleguidist and storybook.

- Storybook /40kStar/MIT/201908/ts
  - https://github.com/storybookjs/storybook
  - https://storybook.js.org/
  - UI component dev & test: React, Vue, Angular, Web Components & more
  - 定位很尴尬，做测试有更专业的jest，做文档不够灵活，适合边开发边预览
- https://github.com/fwouts/previewjs
  - Preview.js lets you preview React, Preact, Solid, Svelte, Vue components and Storybook stories instantly in your IDE (or in your browser via the CLI).
- vitro /248Star/ISC/202103/ts
  - https://github.com/remorses/vitro
  - https://vitro.vercel.app/
  - Vitro is a storybook alternative that builds 20x faster
  - It is built on top of esbuild (thanks to bundless)
  - Build and showcase your react components in isolation
  - Differences with storybook
    - No addons, if you want more features open a pull request here
    - Many features inherited from next.js like Incremental compilation
- storycruise /6Star/MIT/202101/ts
  - https://github.com/itaditya/storycruise
  - https://storycruise.vercel.app/stories/button
  - An experiment to render stories (from Storybook) with Snowpack.
  - Storybook is a great tool but it takes ages to load.
  - Snowpack opens pretty fast.
  - What if it could read Component Story Format and show them on a page like Storybook?
- https://github.com/kekingcn/kkFileView
  - https://kkfileview.keking.cn/
  - 使用spring boot打造文件文档在线预览项目解决方案，
  - 支持doc、docx、ppt、pptx、xls、xlsx、zip、rar、mp4，mp3
  - 以及众多类文本如txt、html、xml、java、properties、sql、js、md、json、conf、ini、vue、php、py、bat、gitignore等文件在线预览

- https://github.com/frictionlessdata/livemark
  - https://livemark.frictionlessdata.io/
  - 基于python jinja实现，table、chart完全自己实现
  - Livemark is a static page generator that extends Markdown with interactive charts, tables, and more.
  - Livemark process your document using the Jinja templating language. 
  - Inside templates, you can use Frictionless Framework as a frictionless variable to work with tabular data. 
  - It's a high-level preprocessing so you can combine Logic with other syntax, such as Table or Chart
# more-doc-solutions
- VuePress

- https://github.com/phenomic/phenomic
  - DEPRECATED. Please use Next.js instead.
- https://github.com/egoist/docute /js/vue/inactive
  - Leveraging the power of Markdown and Vue.
  - No build process, website is generated on the fly.

- https://github.com/mkdocs/mkdocs /17.3kStar/BSD/202311/python/ts
  - https://www.mkdocs.org/
  - Project documentation with Markdown built with python
  - static site generator that's geared towards building project documentation
  - 依赖Jinja2、Markdown、pathspec
  - Documentation source files are written in Markdown, and configured with a single YAML configuration file. 
  - Use Plugins and Markdown Extensions to enhance MkDocs.
  - https://github.com/squidfunk/mkdocs-material
    - Write your documentation in Markdown and create a professional static site for your Open Source or commercial project in minutes – searchable, customizable, more than 50 languages, for all devices.

- https://github.com/star7th/showdoc
  - https://www.showdoc.com.cn/
  - https://www.showdoc.com.cn/demo/10
  - 适合IT团队的在线API文档、技术文档工具
  - 依赖PHP
- https://github.com/remorses/dokz
  - https://dokz.site/
  - /283Star/ISC/202010/ts
  - 依赖@chakra-ui/core、@emotion/core、prism-react-renderer
  - Effortless documentation with Next.js and MDX
  - File based routing
- hosting-docs
- https://zeroheight.com/
  - Create beautiful living styleguides and document all your design system resources in one place
- https://github.com/jashkenas/docco
  - http://ashkenas.com/docco/
  - Docco is a quick-and-dirty, hundred-line-long, literate-programming-style documentation generator in Literate CoffeeScript.
  - It produces an HTML document that displays your comments intermingled with your code. 
- https://github.com/mindoc-org/mindoc
  - Golang实现的基于beego框架的接口在线文档管理系统
- https://github.com/TruthHun/BookStack
  - 基于MinDoc，使用Beego开发的在线文档管理系统，功能类似Gitbook和看云
- https://github.com/phachon/mm-wiki
  - 企业知识分享与团队协同软件
  - 依赖go
- https://github.com/mylxsw/wizard
  - 开源的文档管理工具，支持Markdown/Swagger/Table类型的文档。
  - 依赖php
# examples
- ## docusaurus-examples
- https://github.com/ThinkBucket/docsite
  - https://thinkbucket.cn/
  - 只依赖react、@docusaurus/core.v2
  - 典型的文档风格，左侧目录，右侧书签toc

- ## storybook-examples
- https://github.com/webapp-suite/elements-react
  - 在右侧添加了toc
# more-repos
- https://github.com/front10/landing-page-book
  - Fully customizable landing-page components written in React.
  - 依赖gatsby、bootstrap、codemirror
- https://github.com/CoreyMakes/react-landing-page
  - a set of highly-composable React components for building advanced landing pages. 
  - built using Rebass, a library of UI primitives.
  - https://github.com/Hermanya/react-landing-page
    - On one hand, there is no need to couple your app to your landing page. 
    - If your app is using react, it does not mean your landing page should. If anything, react is slowing down your landing page.
- https://github.com/TeselaGen/teselagen-react-components
  - 代码块背景透明，显得很随意
- https://github.com/mbrn/libzy
  - a boilerplate that makes documentation faster. It uses material-ui UI components.

- https://github.com/Foveluy/ReStory
  - 依赖antd3、showdown、koa
  - A static site generator with MDX for React documentation.
- https://github.com/MuYunyun/create-react-doc
  - http://muyunyun.cn/create-react-doc/README
  - 依赖 react-markdown、@mdx-js/react.v1.6、prism-react-renderer
  - 建站理念: 文件即站点 (Files as a Site)。
  - 性能: 通过预渲染、懒加载大幅提升站点加载速度。
  - 基于 mdx: 支持在markdown中书写React组件、数学公式等
  - crd是一个使用React的markdown文档站点生成工具
- https://github.com/framer/monobase
  - https://elegant-clarke-8778e0.netlify.app/
  - 依赖webpack.v4、react-remarkable、express、@mdx-js/loader；不依赖framer-motion
  - Monobase let's you build sites in a component based way, allowing you to isolate and re-use every part of your website. 
# ref
- [Storybook vs Styleguidist_201805](https://www.chromatic.com/blog/storybook-vs-styleguidist/)
- [What’s the difference between Styleguidist and Storybook?](https://react-styleguidist.js.org/docs/cookbook/#are-there-any-other-projects-like-this)
  - For me, the biggest distinction is how you describe component variations.
    - With Storybook you write stories in JavaScript files
    - with Styleguidist you write examples in Markdown files
  - Another important distinction is that Storybook shows only one variation of one component at a time 
    - but Styleguidist can show all variations of all components, all variations of a single component or one variation. 
  - It’s easier to create a style guide with Styleguidist 
    - but Storybook has more tools to develop components
- [Alternatives to storybook/styleguidist?](https://www.reddit.com/r/reactjs/comments/80lkz0/alternatives_to_storybookstyleguidist/)
