---
title: toc-saas-ecommerce-shopping
tags: [ecommerce, sass, shopping, toc]
created: 2022-11-03T17:09:36.468Z
modified: 2023-06-07T14:19:18.719Z
---

# toc-saas-ecommerce-shopping

# guide

- 商店类产品的设计可参考类似ckan的data-portal
# popular

# starter

- https://github.com/hicmtrex/TypeShop-Backend /202212/ts
  - https://github.com/hicmtrex/TypeShop-Frontend
  - https://type-shop.vercel.app/
  - react-bootstrap、Redux Toolkit
  - express、mongodb
  - 不依赖nextjs

- https://github.com/ivan3123708/fullstack-shopping-cart /202101/ts+js
  - MERN stack shopping cart

- https://github.com/dneflas/shop-shoppe /js
  - A MERN stack e-commerce platform, featuring persistent shopping cart, offline capabilities and stripe payment processing

- https://github.com/kt946/awesome-shop-shop-redux
  - An e-commerce MERN application that uses Redux to manage global state. 

- https://github.com/andrewsolonets/Azon-Shop
  - Ecommerce website built with t3-stack (typescript, prisma, trpc, next.js)
  - E-Commerce website with Prisma PlanetScale db, optimistic updates with React Query, rating system, persistent cart, algolia search, categories, in stock indicator, infinite scroll and order tracking
  - Custom db with orders connected to Stripe
# plugins/packages-marketplace
- 可参考
  - realworld示例的list-article架构
  - 包管理器: npm, rust-crate, docker, flathub, appimage, greasy-scripts
  - 插件扩展: vscode-extensions-marketplace, opensumi, chrome-store, jetbrains, Ulauncher
  - marketplace: atlassian, mattermost, airtable, zoho, directus
  - app-store: unhosted/0data, Store.app, Electron
  - 其他: data-portal, strapi-plugins, better-discord, observable-notebook-import
  - 可考虑基于npm发布插件，参考Cerebro-launcher
  - npm的优点，支持各版本的文档分别显示
  - 可考虑类似ckan，但版本管理功能弱
  - 支持迁移deprecate-app到new-app，一键迁移
  - search: made-with, product-hunt

- 收集聚合类
  - ui组件、数据、表格
  - [Botpress Hub: Integrations, Skills, Channels](https://botpress.com/hub)
  - [Discord Servers - Public Server Listing](https://discordservers.com/)
  - [Storybook Component Encyclopedia](https://storybook.js.org/showcase)
    - The Component Encyclopedia is built with Hygraph cms(NonOpen)

- openvsx /1kStar/EPLv2/202312/java/ts/参考前端
  - https://github.com/eclipse/openvsx
  - https://open-vsx.org/
  - https://ecdtools.eclipse.org/adopters/
  - Open VSX is a vendor-neutral open-source alternative to the Visual Studio Marketplace.
  - It provides a server application that manages VS Code extensions in a database, a web application similar to the VS Code Marketplace, and a command-line tool for publishing extensions similar to vsce.
  - 前端依赖mui.v5、markdown-it、react-infinite-scroller
  - 后端依赖spring-boot、ehcache
  - 未实现依赖的依赖dependents
  - https://github.com/EclipseFdn/open-vsx.org
    - This repository contains the source of open-vsx.org, the public instance of Eclipse Open VSX. 
    - Most of the code is maintained in eclipse/openvsx, while here you'll find only adaptations specific to the public instance.

## npm-registry(支持版本历史)

- verdaccio /15.6kStar/MIT/202401/ts
  - https://github.com/verdaccio/verdaccio
  - https://www.verdaccio.org/
  - https://verdaccio.org/dev/plugins-search/
  - Verdaccio is a simple, zero-config-required local private npm registry. 
  - 后端依赖express，采用插件式架构，支持express/fastify
  - 前端依赖redux、mui.v5、rematch、marked、react-markdown、JSONStream
  - 支持显示包的历史版本和各版本信息，和npm前端几乎类似
  - Verdaccio comes out of the box with its own tiny database, and the ability to proxy other registries (eg. npmjs.org), caching the downloaded modules along the way
  - 📡 使用openvsx的前端替换
  - A memory based storage plugin.
  - File system storage plugin for verdaccio
  - AWS S3/minio storage plugin for Verdaccio
  - [Release v6.0.0-beta.1 _202401](https://github.com/verdaccio/verdaccio/releases/tag/v6.0.0-beta.1)
    - node > v16
    - using new plugin loader
    - replace deprecated `request` dependency by `got`.
    - experiment: accept async tarball_url_redirect function
    - refactor auth class 
  - [Show HN: Verdaccio – Open-Source Lightweight private NPM proxy registry | Hacker News _201806](https://news.ycombinator.com/item?id=17215474)
    - Does this use couchdb the way NPM seems to?
    - If you're looking for that, try smart-private-npm.
  - https://www.npmjs.com/package/verdaccio/v/2.7.2
    - verdaccio is a fork of sinopia. It aims to keep backwards compatibility with sinopia, while keeping up with npm changes.
    - No CouchDB here. This application is supposed to work with zero configuration, so filesystem is used as a storage.
  - https://github.com/sgrandner/my-local-npm-registry-with-verdaccio
  - examples-private-registry
    - https://npm.patrocinium.com/
    - https://npm.bsimo.fr/
    - https://npm.claimh.com/
- https://github.com/RightCapitalHQ/verdaccio-package-diff
  - A package diff plugin for Verdaccio
  - This will display the file differences between the two versions.

- https://github.com/cnpm/cnpmweb /202401/ts
  - https://npmmirror.com/
  - A missing UI for custom registry.
  - 支持任意 npm registry
  - 基于 Next.js 纯静态部署
  - cnpmweb 是独立的前端应用，npmmirror 提供一个新的制品库界面，可在 config.js 中定义自定义 registry 地址。
  - https://github.com/cnpm/cnpmcore /500Star/MIT/202401/ts
    - Private NPM Registry for Enterprise
    - Reimplementation based on cnpmjs.org with TypeScript.
    - 本项目的外部服务依赖有：MySQL 数据服务、Redis 缓存服务。
    - 基于 PaaS 基础设置实现各种 adapter 真实适配实现，cnpmcore 会内置一种实现，企业自定义的 cnpmcore 应该自行基于自身的 PaaS 环境实现自己的 infra module。
    - 目前只支持 HTTP 协议的 Controller，代码在 app/port/controller 目录下。 基于类继承的模式来实现
    - 依赖 @eggjs/tegg.v3、elasticsearch、mysql2

- https://github.com/taskforcesh/nandu /AGPLv3/202212/ts/inactive
  - a new open source NPM registry compatible with Npm, Yarn and Pnpm.
  - built from scratch 
  - Compatible with scalable technologies such as S3 and PostreSQL so you can scale your registry to meet your needs.
  - Compatible with scalable technologies such as S3 and PostreSQL so you can scale your registry to meet your needs.
  - Nandu is secured by default, focusing on user, team and organization management, enabling corporate use cases where user access management is important 
  - The registry is both a package metadata store, for which you can use any SQL-based database (including SQLlite), as well as a package store that is based on file storage. 
  - The package store can be anything capable of storing files but currently, we are shipping support for local files as well as S3, but it is quite easy to add other file storage by implementing a simple interface if needed.

- https://github.com/topheman/npm-registry-browser /MIT/202104/js
  - https://topheman.github.io/npm-registry-browser/
  - Browse the npm registry with an SPA made in React, with full dev workflow.
  - 依赖mui.v4、downshift、recompose、react-markdown

- openupm /1.4kStar/BSD/202401/js/参考后端
  - https://github.com/openupm/openupm
  - https://openupm.com/
  - Open Source Unity Package Registry
  - Many UPM packages use NuGet packages as embedded DLLs. This practice can become troublesome when two packages include the same DLL or different versions of one NuGet package. 
  - UnityNuGet is a project that provides a service to bundle NuGet packages into the UPM format
  - https://github.com/openupm/openupm-cli
    - a command-line interface for maintaining UPM registries.
    - 依赖commander、libnpmsearch、pkginfo
    - The command-line tool to maintain the Unity manifest file for 3rd-party upm registries, offering a similar but lighter experience like npm or yarn for Node.js.
    - The tool is designed to work with the OpenUPM registry, but can also work with any upm registries, including the official Unity registry.
    - The command-line tool installs the 3rd-party registry as a scoped registry and maintains the Packages/manifest.json file when adding/removing packages. If the manifest file is modified, the Unity Package Manager will detect the changes and try to resolve the package dependencies.
    - Notice: the command-line tool does not directly install/uninstall package tarballs, at least for now.
  - https://github.com/openupm/verdaccio-storage-proxy /BSD/202210/ts
    - A verdaccio storage proxy to decouple database, search, packument, and tarball accesses.
  - https://github.com/openupm/openupm-next /BSD/202401/ts/vue
    - Codebase for OpenUPM website and services
    - 依赖aws-sdk、fastify、vuepress
    - 软件包搜索在vuepress的markdown和vue组件中实现

- OpenUserJS.org /GPLv3/789Star/202401/js
  - https://github.com/OpenUserJS/OpenUserJS.org
  - https://openuserjs.org/
  - The home of Free and Open Source Software (FOSS) user scripts. 
  - Built using Node.js and other web familiar technologies.
  - 依赖mongodb
  - 无法访问旧版本的脚本
  - [Is there a way to view previous versions of scripts hosted there? | Discussions | OpenUserJS_202307](https://openuserjs.org/discuss/Is_there_a_way_to_view_previous_versions_of_scripts_hosted_there)
    - OUJS is a Presentational Userscript Repository only. So no. 
    - Use GitHub if you want full SCM functionality at this time.
- https://github.com/JasonBarnabe/greasyfork /202401/ruby
  - https://greasyfork.org
  - online repository of user scripts and user styles.

- https://github.com/denosaurs/crux.land /MIT/202205/ts
  - a free registry service meant for hosting small (≤ 20kB) single deno scripts.
  - crux.land runs on deno deploy and requires the deployctl cli for local development.

- https://github.com/Tanuel/baggy /202005/ts/inactive
  - a reverse engineered NPM registry with a modular structure.
  - You can provide your own functionality for storing artifacts and metadata.

- https://github.com/npmx-dev/npmx.dev /1.2kStar/MIT/202602/ts/vue
  - https://npmx.dev/
  - The goal of npmx.dev is to build a fast, modern browser for the npm registry.
  - Compatibility – Replace npmjs.com with xnpmjs.com or npmx.dev in any URL and it just works.
  - Enhanced admin experience – Manage your packages, teams, and organizations from the browser, powered by your local npm CLI.

## marketplace

- https://github.com/joplin/website-plugin-discovery /MIT/202401/ts/mustache
  - https://joplinapp.org/plugins/
  - https://joplinapp.org/help/api/get_started/plugins/
  - The official plugin repository website
  - 依赖codemirror.v6、highlight.js、markdown-it、mustache、webpack
  - 详情页会显示Minimum app version、下载量
  - 搜索没有单独的页面
  - build时会请求`https://github.com/joplin/plugins/blob/master/manifests.json`文件的内容作为所有插件元数据，打包出来的产物是普通spa
  - npm install -g yo generator-joplin
    - The `src/` directory contains a `manifest.json` file, which contains the various information about the plugin
    - You should test your plugin in Development Mode. Doing so means that Joplin will run using a different profile, so you can experiment with the plugin without risking to accidentally change or delete your data.
  - https://github.com/joplin/plugins /202402
    - This is the official Joplin Plugin Repository. 
    - 包含所有plugin的jpl逻辑代码和manifest.json
    - It is updated every 30 minutes on the hour and half-hour.

- https://github.com/all-in-aigc/gpts-works /apache2/202312/ts
  - https://gpts.works/
  - A Third-party GPTs store
  - 依赖nextjs、daisyui、react-lazy-load-image-component、langchain、@vercel/postgres
  - 支持详情页
  - index system is used for searching GPTs with vector.
  - fastapi-python for building index system
  - Vercel Storage Postgres: used for storing data.
  - Zilliz Cloud: used for vector storing and searching

- https://github.com/xx025/carrot /无源码
  - https://cc.ai55.cc/
  - 免费好用的ChatGPT镜像站点

- https://github.com/Ulauncher/ext.ulauncher.io /202211/js
  - https://ext.ulauncher.io/
  - Ulauncher Extensions Website
  - built using JS and React library (with CRA)
  - 数据依赖后端
  - https://github.com/Ulauncher/ext-api.ulauncher.io /python
    - Backend for ext.ulauncher.io
    - This API server is written in Python using bottle, boto3 libraries

- https://github.com/AppImage/appimage.github.io /未实现单独搜索
  - https://appimage.github.io/apps/
  - Given an URL to an AppImage, the GitHub action in this project inspects the AppImage and puts it into a community-maintained catalog

- https://github.com/botpress/botpress /MIT/202401/ts
  - https://botpress.com/
  - The open-source hub to build & deploy GPT/LLM Agents
  - https://botpress.com/hub
    - integrate with hundreds of applications and automate workflows with pre-built templates

- https://github.com/logseq/marketplace /MIT/202401/js
  - A centralized packages manager for Logseq marketplace plugins.
  - How to submit your plugin?
  - Make a Github Pull Request

- https://github.com/deriv-com/quill-icons-park /202404/ts/依赖少
  - https://quill-icons-park.pages.dev/
  - A little park to explore Quill Icons intuitively.
  - 🪟 图标的查看和搜索，无详情页，简洁
  - 依赖react、file-saver、@tanstack/react-query.v5
  - 似乎不依赖服务端

## package-manager

- https://github.com/0dataapp/0data
  - https://0data.app/glance
  - Zero Data App - Own your data, all of it.
  - 未实现详情页

- https://gitlab.com/fdroid/fdroidserver /AGPLv3/202401/python
  - a suite of tools to publish and work with collections of Android apps (APK files) and other kinds of packages
  - It is used to maintain the https://f-droid.org/packages
  - https://gitlab.com/fdroid/fdroiddata
    - Metadata for all the apps of the F-Droid main repository.

- https://gitlab.com/theopenstore/openstore-web /GPLv3/202401/vue
  - https://open-store.io/
  - The official Ubuntu Touch app store
  - https://gitlab.com/theopenstore/openstore-api /GPLv3/202401/ts
    - Api for the OpenStore.
    - 依赖express、mongoose、elasticsearch、node-gettext、passport
  - https://gitlab.com/theopenstore/openstore-app /qml/cpp

- https://github.com/flatpak/flat-manager /MIT/202401/rust/python
  - flat-manager serves and maintains a Flatpak repository. 
  - You point it at an ostree repository and it will allow Flatpak clients to install apps from the repository over HTTP. 
  - it has an HTTP API that lets you upload new builds and manage the repository.
  - The server is written in Rust, so you need to have Rust and Cargo installed. 
  - PostgreSQL is used for the database
  - You also need ostree
  - flat-manager contains a Python-based client that can be used to talk to the server. 

- https://github.com/artifacthub/hub /apache2/go/ts
  - https://artifacthub.io/
  - a web-based application that enables finding, installing, and publishing packages and configurations for CNCF projects.

## showcase(不支持版本历史)/data-portal

- https://github.com/rupali-codes/LinksHub /MIT/202401/ts
  - https://linkshub.dev/
  -  a Hub of Links For Developers By Developers. 
  - 依赖daisyui、nextjs、typewriter-effect
  - 无详情页
  - aims to provide developers with access to a wide range of free resources and tools that they can use in their work.
  - contribute by creating a PULL REQUEST 

- https://github.com/MarsX-dev/devhunt /MIT/202401/ts/Supabase/nextjs
  - https://devhunt.org/
  - A launching platform for dev tools
  - we use GitHub pull requests for listings and user logins for genuine voting.
  - Create a Supabase Project and make sure to save the database password.
  - For a complete list of all available social login methods, consult the Supabase Social Login documentation

- https://github.com/jaywcjlove/tools /MIT/202406/ts
  - https://jaywcjlove.github.io/tools
  - Many many useful Web Online Tools For Web Developers & Programmers
  - 每个icon点进去是独立的工具在线使用页面

- https://github.com/tgnav/tgnav.github.io /GPLv3/202402/js
  - https://tgnav.github.io/
  - Telegram频道导航。收录Telegram上的优质频道
  - 无详情页
  - 基于html实现，未使用npm等包管理器

- https://github.com/xjh22222228/nav /MIT/202310/ts
  - https://nav3.cn/?git
  - 发现导航, 打造最强静态导航网站(支持SEO)
  - 无详情页; 支持子路由
  - 支持sim/side/shortcut/app等多个主题

- https://github.com/WebStackPage/WebStackPage.github.io /MIT/202311/js
  - http://webstack.cc/
  - 静态响应式网址导航网站
  - 无详情页; 单页应用，只有一个url且无其他子路由
  - 本项目前端基于bootstrap前端框架开发，各后台及主题版本由广大网友提供。
  - https://github.com/arleycn/arleybookmarks
    - https://bm.arley.cn/
    - Webstack网址导航 美化版
  - https://github.com/Waynenet/Wayne-Navigation
    - https://nav.kong.pub/
    - Webstack网址导航美化版
- https://github.com/hygd0813/WebStack /202312/js/php
  - https://www.80srz.com/link/
  - Typecho Webstack导航主题 | 魔改
  - 包含详情页，在子路由

- https://github.com/liuyike98/233-nav-page /apache2/202111/js
  - https://liuyike233.gitee.io/vue-web-navigation/
  - 一个对前端小白和懒人友好的开源网址导航源码, 部署简单, 仅需修改json文件就能自定义网站内容
  - 使用vue和jquery制作, 纯前台版本, 无后台, 维护比较方便

- https://github.com/x1ah/gena-template yml
  - https://when.run/nav/
  - gena 导航网站生成模板，零依赖，自动部署
  - 数据使用yml
  - 无详情页; 无子路由
  - 使用github-actions自动部署到github-pages
  - https://github.com/x1ah/gena /202210/go/inactive
    - 导航网站生成器(Start page generator)

- https://github.com/DEKVIW/book-nav /MIT/202604/python
  - https://nav.yilancn.top/
  - [导航站更新图标管理功能 - LINUX DO _202604](https://linux.do/t/topic/1891924)
  - 使用 Flask 构建的、可通过 Docker 轻松部署的个人导航网站项目

- https://github.com/electron/apps /MIT/202310/js/无详情页
  - https://www.electronjs.org/apps
  - A collection of apps built on Electron

- https://github.com/expojs/made-with-react /202001/js/过于简单
  - https://madewithreact.com/
  - a collection of websites and applications using the React or React Native JavaScript library.
  - https://madewithreactjs.com/ /未开源
  - [1655+ React Sites | Best Websites Made With React](https://bestofreact.com/)
  - [Made With React Native](https://madewithreactnative.com/)

- https://github.com/react-native-community/directory /MIT/202401/ts
  - https://reactnative.directory/
  - A searchable and filterable directory of React Native libraries.
  - How do I add a library? Add it at the end of react-native-libraries.json file (we use the order in that file for "Recently added" sort option).
  - 依赖nextjs、react-native-web
  - 只展示包列表，每个包没有单独的详情页

- https://github.com/ant-design/scaffold-market /MIT/202310/js
  - http://scaffold.ant.design/
  - scaffold market for single page application
  - 依赖antd.v3、dva、react-disqus-comments、react

- https://github.com/torch2424/made-with-webassembly /MIT/202212/js
  - https://madewithwebassembly.com/
  - A showcase of awesome production applications, side projects, and use cases made with WebAssembly 

- https://github.com/2KAbhishek/projects /GPLv3/202310/js/无详情页
  - https://2kabhishek.github.io/projects
  - Showcase All Your Projects

- https://github.com/Reinforz/Nishan /MIT/202110/ts
  - https://nishan-docs.netlify.app/
  - An ecosystem of packages for notion written in typescript.
  - 模仿npm

- https://github.com/419Labs/starknet-ecosystem.com /apache2/202401/ts
  - https://www.starknet-ecosystem.com/
  - Starknet Ecosystem Dashboard
  - To update your project you have to do the same thing than for adding. Edit the data/ecosystem.ts file and create a dedicated Pull Request

- https://github.com/jamstack/jamstack.org
  - https://jamstack.org/generators/
  - A List of Static Site Generators for Jamstack Sites
  - 基于eleventy实现

- https://github.com/statichunt/statichunt /MIT/202402/js
  - https://statichunt.com/
  - a free open-source Jamstack directory that lists hundreds of themes, starters, and resources for static sites.
  - 依赖next-mdx-remote、marked、react-infinite-scroll-component

- https://github.com/piotrkulpinski/openalternative /GPLv3/202502/ts
  - https://openalternative.co/
  - A community driven list of open source alternatives to proprietary software and applications.
  - item默认展示为卡片，点击item会进入详情页，支持filter
  - OpenAlternative is currently written in Remix. 

## more-app-store

- https://github.com/pawelmalak/snippet-box /MIT/202110/ts
  - a simple self-hosted app for organizing your code snippets. 
  - It allows you to easily create, edit, browse and manage your snippets in various languages.
  - Sequelize ORM + SQLite
  - for search, multiple filters can be used at once: `card lang:typescript tags:react,editor` is a valid query

- https://github.com/mattermost/mattermost-marketplace /apache2/202312/go
  - https://mattermost.com/marketplace/
  - The stateless HTTP service backing the Mattermost marketplace.
  - It is meant to be queried by the Mattermost server to enable plugin discovery by System Admins.

- https://github.com/pkgxdev/ossapp /apache2/202401/ts/svelte
  - https://pkgx.app/
  - https://pkgx.dev/pkgs/
  - The App Store for Open Source
  - ossapp is a Svelte Electron app
  - ossapp is the graphical app complement to pkgx.
  - Under the hood ossapp installs and manages your packages with pkgx
  - pkgx is a core contributor to the tea protocol

- [useHooks – The React Hooks Library](https://usehooks.com/)

- [Directories](https://directories.so/)
  - The ultimate directory of the best directories on the internet.
# books/reads
- https://github.com/Alamantus/Readlebee /AGPLv3/202104/js/archived
  - https://gitlab.com/Alamantus/Readlebee
  - An attempt at a viable alternative to Goodreads
# more
