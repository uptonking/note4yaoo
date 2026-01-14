---
title: lib-xplat-electron-examples
tags: [client-desktop, electron, examples, toc]
created: 2021-01-16T20:49:44.833Z
modified: 2024-01-31T19:13:11.286Z
---

# lib-xplat-electron-examples

# guide

- loved-examples
  - https://github.com/warpdesign/react-explorer
  - https://github.com/koodo-reader/koodo-reader
  - https://github.com/edrlab/thorium-reader
  - https://github.com/sprout2000/leafview
  - https://github.com/yossTheDev/karbonized
  - https://github.com/dutchigor/pluggable-electron

- resources
  - https://github.com/sindresorhus/awesome-electron
# popular
- https://github.com/Elanis/web-to-desktop-framework-comparison
  - 🆚️ This repository has been made to create an objective comparison of multiple frameworks that allow us to "transform" our web apps to desktop applications.
  - Electron, NW. JS, Tauri, NodeGui(Qt6), Neutralino, Wails, Flutter

- https://github.com/electron/fiddle /MIT/202401/ts
  - https://electronjs.org/fiddle
  - The easiest way to get started with Electron
  - Try Electron without installing any dependencies: Fiddle includes everything you'll need to explore the platform. 
  - It also includes examples for every API available in Electron
  - Fiddle is not an IDE – it is however an excellent starting point.

- https://github.com/electron/apps /MIT/202310/js/无详情页
  - https://www.electronjs.org/apps
  - A collection of apps built on Electron

- koodo-reader /21.4kStar/AGPLv3/202503/ts
  - https://github.com/koodo-reader/koodo-reader
  - https://github.com/troyeguo/koodo-reader /renamed
  - https://koodo.960960.xyz/
  - https://web.koodoreader.com/
  - A modern ebook manager and reader with sync and backup capacities for Windows, macOS, Linux and Web
  - 依赖electron-store、fs-extra、howler、react-hot-toast、webdav、marked、jszip、localforage、react-redux
  - Save your data to Dropbox or Webdav
  - Single-column, two-column, or continuous scrolling layouts
  - Add bookmarks, notes, highlights to your books
  - [希望能够有编辑功能_202401](https://github.com/koodo-reader/koodo-reader/issues/1037)
    - 个人认为作为一个阅读器，编辑功能有点冗余，如果需要编辑可以用对应的各种强大产品

- https://github.com/edrlab/thorium-reader /2kStar/BSD/202503/ts/epub
  - https://www.edrlab.org/software/thorium-reader/
  - A cross platform desktop reading app, based on the Readium Desktop toolkit
  - an easy to use EPUB reading application for Windows 10/10S, MacOS and Linux
  - 依赖redux、redux-saga.v1.3、electron、inversify、lunr2、mathjax、radix-ui、pdfjs、r2-streamer-js、react-table7
  - Thorium-reader is composed of 3 parts: 
    - One node.js main process (electron back-end) 
    - One library window (chromium renderer) 
    - One to N reader window(s) (chromium renderer)
    - Each part runs a model-controller and a view for the renderer process.
  - A great care is taken to ensure the accessibility of the application for visual impaired people using NVDA, JAWS or Narrator.
  - No ads. No private data flowing anywhere.
  - [Feature proposal: read PDFs as HTML _202502](https://github.com/edrlab/thorium-reader/discussions/2810)
    - We never intended to have strong PDF support, considering that other reading software already provides a good reading experience.
    - This seems like a format conversion tool (PDF to EPUB) more than a Thorium feature. Thorium could ultimately integrate this tool transparently like we do with DAISY 2.02 and DAISY 3.0 text / text+audio / audio digital talking books.
  - [consider to swap to mupdfjs ?](https://github.com/edrlab/thorium-reader/discussions/2742)
    - PDF.js may be a slower rendering engine, but it is a mature library, with a strong feature set (including text selection + annotations) and a page layout logic that integrates quite well in Thorium.
  - https://github.com/readium/ts-toolkit
  - https://github.com/edrlab/thorium-web /BSD/202512/ts
    - open-source ebook/audiobook/comics Web Reader
    - 与桌面版架构不同

- https://github.com/desktop/desktop /MIT/202502/ts
  - GitHub Desktop is an open-source Electron-based GitHub app. 
  - It is written in TypeScript and uses React.
  - Focus on what matters instead of fighting with Git.
  - Linux is not officially supported; however, you can find installers created for Linux from a fork of GitHub Desktop in the Community Releases section.

- https://github.com/jupyterlab/jupyterlab-desktop /BSD/202401/ts
  - JupyterLab desktop application, based on Electron.
  - Sessions represent local project launches and connections to existing JupyterLab servers. Each JupyterLab UI window in the app is associated with a separate session and sessions can be restored with the same configuration later on.
  - Each launch of JupyterLab in a different working directory is a separate project and projects can have their own configuration such as Python environment and UI layout.

- https://github.com/gristlabs/grist-desktop /apache2/202410/ts
  - Desktop Grist, packaged with Electron
  - It does not need the internet, and will work fine when offline

- kikko /75Star/MIT/202401/ts/inactive
  - https://github.com/kikko-land/kikko
  - https://kikko-doc.netlify.app/
  - Powerful SQLite adapter for web, mobile and desktop. Build reactive UI on top of it
  - It brings transaction support, middlewares for queries, and SQLite adapters for the most popular platforms.

- https://github.com/Icon-Shelf/icon-shelf /MIT/202311/ts/inactive/非web仅pc
  - https://icon-shelf.github.io/
  - SVG icon manager for developers.
  - Link the icons folder of your project to Icon Shelf and see all your icons in an easily previewable manner. 
  - File-based (adding, deleting, modifying icons in app get reflected in file-system as well.)
  - 依赖codemirror6、dexie3、react-query4、dnd-kit

- https://github.com/jgraph/drawio-desktop /apache2/202503/js
  - Official electron build of draw.io
  - drawio-desktop is a diagramming desktop app based on Electron that wraps the core draw.io editor.
  - draw.io Desktop is designed to be completely isolated from the Internet, apart from the update process.
  - draw.io is closed to contributions (unless a maintainer permits it, which is extremely rare).
  - If we were to receive a PR, we'd have to basically throw it away and write it how we want it to be implemented.

- https://github.com/sprout2000/leafview /MIT/202412/ts/提交多
  - Minimalist image viewer based on Leaflet.js and Electron.
  - 示例不是地图，而是普通图片
  - Browse the images in a folder
  - Grid view

- https://github.com/yossTheDev/karbonized /apache2/202312/ts/inactive/pwa+pc
  - Awesome Image Generator for Code Snippets & Mockups
  - Our block-based system allows you to customize and arrange code snippets, text, images, QR codes, and more, giving you the freedom to bring your ideas to life.
  - 依赖vite-plugin-electron、electron-builder、react-daisyui、easy-peasy、prismjs、react-moveable、localforage
  - `win.loadFile('dist/index.html')`; 能正常打开
  - Export Options: Save your designs as SVG, PNG, or JPG files, making it simple to share or use them in other projects.
  - Extension Support: Karbonized offers support for extensions, allowing you to enhance its functionality and extend its capabilities according to your needs.
  - Multi-Platform Compatibility: Access Karbonized as a Progressive Web App (PWA with Offline Support) via any web browser. We also provide downloadable versions for Windows, Linux, and macOS

- https://github.com/wulkano/Kap /18.4kStar/MIT/202210/ts/inactive
  - open-source screen recorder built with web technology

- https://github.com/xushengfeng/eSearch /6.2kStar/GPLv3/202512/ts
  - https://esearch-app.netlify.app/
  - 截屏+OCR+搜索+翻译+贴图+屏幕翻译+以图搜图+滚动截屏+录屏
  - eSearch 是Information-portal的:electron: 重写版(顺便加了亿些功能)
  - 主要是想在 Linux 上(win 和 mac 上也能用)实现锤子大爆炸或小米传送门这样的屏幕搜索功能，当然也是一款方便的截屏软件。
  - 截屏 离线OCR 搜索翻译 以图搜图 贴图 录屏 滚动截屏 
  - 本地 OCR 由`PaddleOCR`的模型提供支持。

- https://github.com/027xiguapi/pear-rec /1.3kStar/apache2/202407/ts/inactive
  - https://027xiguapi.github.io/pear-rec/
  - 跨平台的截图、录屏、录音、录像软件
  - react + electron + vite + viewerjs + plyr + aplayer + react-screenshots.
  - 支持网页版、pc版

- https://github.com/nashaofu/screenshots /414Star/MIT/202502/ts
  - https://nashaofu.github.io/screenshots/
  - 基于electron和react的截图插件，可以快速地实现截图功能，并支持多种截图操作，例如马赛克、文本、画笔、箭头、椭圆和矩形

- https://github.com/likaia/js-screen-shot /MIT/202502/ts
  - https://www.kaisir.cn/js-screen-shot/
  - web端自定义截屏插件(原生JS版)
  - 由于插件采用原生js编写且不依赖任何第三方库，因此它可以在任意一台支持js的设备上运行。
  - 支持electron环境下使用插件

- https://github.com/rubickCenter/rubick /8.2kStar/MIT/202501/ts/vue
  - https://rubickcenter.github.io/docs
  - Open-source plugin-based desktop efficiency toolbox. 
  - 基于 electron 的开源工具箱，自由集成丰富插件。类似系统launcher/spotlight
  - 插件全部托管在 npm 仓库，rubick 插件的安装、使用、删除就是 npm 包的安装、使用、删除
  - 支持基于 webdav 的多端数据同步，支持内网部署。

- https://github.com/httptoolkit/httptoolkit-desktop /AGPLv3/202401/ts/postman-like
  - https://httptoolkit.com/
  - Electron wrapper to build and distribute HTTP Toolkit for the desktop
  - the desktop build setup for HTTP Toolkit, a cross-platform & open-source HTTP(S) debugging proxy, analyzer & client.
  - HTTP Toolkit consists of two runtime parts: a UI, written as a single-page web application, and a server, written as a node.js CLI application.
  - built using Electron Builder.
  - This isn't the only way to run HTTP Toolkit! It's the most convenient option for most users, but it's also completely possible to run the server as a standalone tool and open the UI (hosted at https://app.httptoolkit.tech) in any browser you'd like.

- https://github.com/1943time/bluestone /AGPLv3/202403/ts
  - https://www.bluemd.me/
  - 青石是一个开源的所见即所得Markdown编辑器
  - markdown的table元素也不利于书写，双栏模式并不利于聚焦，所以开发了青石编辑器。
  - 使用了富文本的编辑模式，同时兼容Markdown语法转换与编辑习惯，当使用搜索功能时，Markdown符号不会被搜索。
  - Using shiki as a code shader to make code highlights more fine-grained
  - 依赖mobx-react-lite、remark-gfm

- https://github.com/picturama/picturama /MIT/202203/ts/inactive
  - Digital image organizer powered by the web
  - don't upload your personal photos to cloud 
  - Read various photo formats: JPG, PNG, TIF, WebP, HEIC / HEIF
  - Read raw formats of a whole bunch of cameras (only on Mac and Linux)
  - Tags/Favorites

- https://github.com/low-teck/vault
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.
  - https://github.com/codegiik/electron-react-nedb-boilerplate

- https://github.com/Electron-Store/electron-app-store /MIT/202112/js/vue/inactive
  - A Cross-Platform App Store for Electron.js Apps

- https://github.com/opensumi/ide-electron /MIT/202401/ts
  - https://opensumi.com/
  - OpenSumi Electron Version

- https://github.com/pd4d10/debugtron /MIT/202407/ts
  - Debugtron is an app to debug in-production Electron based app

- https://github.com/kiwix/kiwix-js-pwa /231Star/GPL/202601/js
  - Kiwix JS Offline Browser implemented as a Progressive Web App (PWA), and packaged as Electron, NWJS and UWP apps for Windows and Linux
  - this app is available either as an offline-capable, installable Progressive Web App (PWA), for almost all modern browsers and devices, or else as app packages for various Windows, Linux and macOS
  - For iOS and Android, use the offline PWA.
  - We also have packaged apps of WikiMed by Kiwix (a complete medical encyclopaedia), and Wikivoyage by Kiwix (a complete travel guide) in English -- no extra download needed
# pattern/architecture
- https://github.com/ccorcos/electron-architecture /4Star/CC0-1/202108/ts/inactive
  - This project is a boilerplate electron app with a thoughtfully designed architecture
  - Main and renderer processes manage state using a Redux-like state machine.
  - Electron BrowserWindows are controlled declaratively through the application state.
  - Electron IPC uses a Proxy enabling "Rename Symbol" and "Find All References" in VSCode.
  - https://github.com/ccorcos/electron-boilerplate /202012/ts
    - uses TypeScript and demonstrates using a preload script to interact with the native APIs.

- https://github.com/klarna/electron-redux /MIT/202410/ts
  - Use redux in the main and browser processes in electron
  - Electron-Redux is an Redux Store Enhancer that helps you loosely synchronize the redux stores in multiple electron processes.
  - This library, enables you to register all your Redux stores in the main & renderer process, and enable cross-process action dispatching & loose store synchronization.

- https://github.com/HopefulHeart2020/electron-typescript-react-clean-architecture /202309/ts
  - Boilerplate for projects using Eletron, React and Typescript applying Clean Architecture together with Atomic Design.

- https://github.com/dutchigor/pluggable-electron /MIT/202401/js/inactive
  - A framework to build Electron apps that can be extended by other parties.
  - Pluggable Electron allows an Electron app to include extension points in the code. 
    - Plugin developers can then write extensions - in the form of npm packages - that can be inserted into these extension points.
  - The framework includes the tools necessary to manage the whole life cycle of plugins, for example writing, installing, uninstalling and updating plugins, and creating and triggering extension points.
  - The framework uses inversion of control and dependency inversion principles for this.
  - [Allow dependencies between plugins ](https://github.com/dutchigor/pluggable-electron/issues/13)
    - Pluggable Electron makes it possible for plugins to add their own extension points that can be registered to by other plugins. Whilst this is useful, this can become confusing if a plugin requires that other plugin to be present but it is not.
    - But since Pluggable Electron is based on npm packages, the obvious solution here would be to usilise the dependencies these packages.
  - [How about custom UI plugins? _202110](https://github.com/dutchigor/pluggable-electron/issues/2)
    - Version 0.2.0 has now been released and this supports importing Pluggable Electron into ES modules on the front end. 
  - https://github.com/dutchigor/pluggable-electron-demo
    - Also check out the with-vue branch to see an example with Vite and Vue. 
  - https://github.com/sunkarapk/electron-plugin-manager /MIT/202202/js/inactive
    - Plugin Manager based on NPM for Electron apps

- https://github.com/reZach/secure-electron-template /MIT/202404/js/inactive
  - A current electron app template with the most popular frameworks, designed and built with security in mind
  - https://github.com/reZach/i18next-electron-fs-backend
    - This is an i18next library designed to work with secure-electron-template.
    - The library is a rough copy of i18next-node-fs-backend but using IPC (inter-process-communication) to request a file be read or written from the electron's main process.

- https://github.com/ArcherGu/einf /MIT/202502/ts
  - Einf is a simple electron main process framework, which provides some decorators and automatic dependency injection to help you simplify the main process code.
  - Support dependency injection powered by Typescript decorators.

- https://github.com/web-infra-dev/electron-sprout /MIT/202210/ts/inactive/modernjs
  - A front-end friendly desktop framework based on Electron.
  - electron-runtime: modified from vscode.
  - Unbundled Dev Server: The server implementation is based on the idea and structure of vite and wmr, and is adapted to the Modern.js application.

- https://github.com/dromara/electron-egg /apache2/202502/js/示例超级多
  - A simple, cross platform, enterprise desktop software development framework
  - Architecture: Single - business process / modular / multi - task (process, thread, rendering process), which simplifies the development of large - scale projects.
  - Independent front - end: Theoretically supports any front - end technology, such as Vue, React, HTML, etc.
  - https://github.com/wallace5303/ee-core /ISC/202502/js
    - Powerful electron third party module, offering 100+ API

## client-server(webapp+desktop-app)

- https://github.com/actualbudget/actual /24.2kStar/MIT/202601/ts/js
  - https://actualbudget.org/
  - A local-first personal finance app
  - it has a synchronization element so that all your changes can move between devices 
  - client + server + sync
  - https://github.com/jlongster/electron-with-server-example /202001/js/inactive
    - An example Electron app with a backend server all wired up via IPC
    - This is exactly how my product Actual, a personal finance manager, works and this code is almost 100% copy and pasted from it.
    - By forking a separate Node.js process using `child_process.fork`, the application ensures that heavy tasks do not block the Main process's event loop, which would otherwise freeze the application's window frame and native menus.
    - [How to run Express inside an Electron app](https://gist.github.com/maximilian-lindsey/a446a7ee87838a62099d)

- https://github.com/engPabloMartinez/react-express-electron-boilerplate /202008/ts/inactive
  - A boilerplate to generate an Electron app with a React Front end and an Express BackEnd embedded.

- https://github.com/rohitsoni007/electron-shadcn /MIT/202511/ts/inactive
  - modern Electron application template built with React, TypeScript, Vite, and shadcn/ui components
  - Rolldown Vite 7.1.20 
  - TanStack Router 1.134, 未使用tanstack-start
  - 默认 uses createMemoryHistory()

- https://github.com/Molizanee/electron-react-tailwind /MIT/202510/ts
  - Boilerplate to build Electron.js apps with Bun.js with React.js and modern web tools
  - bun run start:web
  - bun run start:desktop

- https://github.com/saltyshiomix/nextron /MIT/202508/ts/inactive
  - 提供了很多示例
- https://github.com/MaximePremont/boilerplate-nextron-shadcn /MIT/202411/ts/inactive
  - a Nextron ( Next. Js + Electron ) project template in TypeScript with a Next. Js 14 App Router that includes TailwindCSS and the Shadcn/ui component library.
  - This project is also configured so that the application can be built for both web and desktop versions with the same code.

- https://github.com/DarkGuy10/NextJS-Electron-Boilerplate /MIT/202405/ts/inactive
  - boilerplate for building cross-platform apps with Electron at the core and NextJS serving as the frontend. 
  - why not just use Nextron? And the only valid answer is: flexibiliy.

- https://github.com/ASteinheiser/ts-online-game-template /MIT/202601/ts
  - https://ts-game.online/
  - A highly opinionated template for creating real-time, online games using TypeScript
  - Quickly create mmo-style games using React + Phaser for rendering, Colyseus for websockets and Electron for native builds! Also has support for Progressive Web Apps (PWA). Oh, and lots and lots of Vite for builds and testing
# examples-starter
- https://github.com/alex8088/electron-vite /3.9kStar/MIT/202502/ts
  - https://electron-vite.org/
  - 新一代 Electron 开发构建工具，支持源代码保护
  - 编译为 V8 字节码以保护源代码。
  - 依赖esbuild
  - 支持electron-builder和forge
  - [默认创建的工程编译出exe 后启动比较慢，对比 elctron-forge](https://github.com/alex8088/electron-vite/issues/181)
    - 编译后即是electron可运行的cjs标准文件和electron-forge无异。

- https://github.com/electron-react-boilerplate/electron-react-boilerplate /MIT/202309/ts
  - https://electron-react-boilerplate.js.org/
  - Electron React Boilerplate uses Electron, React, React Router, Webpack and React Fast Refresh.
  - Hot Reloading: Make changes to your app and preview the changes without having to refresh your app.
  - Optimization and minification of code with webpack comes out of the box.
  - Why is webpack a good idea for electron? Webpack helps us reduce the amount of calls made to require by bundling all our code (when possible) into single file. Atom is slow primarily because it makes so many require statements.
- https://github.com/electron/electron-quick-start /CCO-1.0/202309/js
  - https://electronjs.org/docs/latest/tutorial/quick-start
  - Clone to try a simple Electron app
  - https://github.com/electron-userland/electron-webpack-quick-start
  - https://github.com/electron/electron-quick-start-typescript
  - https://github.com/Robinfr/electron-react-typescript
  - https://github.com/yhirose/react-typescript-electron-sample-with-create-react-app-and-electron-builder
  - https://github.com/codesbiome/electron-react-webpack-typescript-2024
  - https://github.com/maxstue/vite-reactts-electron-starter
  - https://github.com/caoxiemeihao/electron-vite-boilerplate

- https://github.com/Level/electron-demo /MIT/202206/js/inactive
  - Demo app loading LevelDB into an Electron context.
  - https://github.com/codegiik/electron-react-nedb-boilerplate

- https://github.com/garrylachman/ElectroCRUD /MIT/202306/ts
  - http://garrylachman.github.io/ElectroCRUD/
  - Database CRUD Application Built on Electron | MySQL, Postgres, SQLite
  - 依赖chakra-ui.v2、@saas-ui/react、@reduxjs/toolkit、knex

- https://github.com/cawa-93/vite-electron-builder /MIT/202401/ts
  - a template for secure electron applications. Written following the latest safety requirements
  - Under the hood is Vite and electron-builder for packaging.
  - TypeScript + Vue/React/Angular/Svelte/Vanilla

- https://github.com/electron-vite/electron-vite-react /MIT/202401/ts
  - https://electron-vite.github.io/
  - Electron + Vite + React + Sass boilerplate.
  - https://github.com/diego3g/electron-typescript-react

- https://github.com/sprout2000/electron-react-ts
  - An Electron boilerplate with hot reloading for React and TypeScript.
  - https://github.com/sprout2000/elephicon
    - a GUI wrapper for png2icons, generates Apple ICNS and Microsoft ICO files from PNG files.
- https://github.com/fantasticit/electron-react-boilerplate /202012/ts/inactive
  - 各窗口均采用 React 开发，也可根据需要更改为其他框架
  - 支持多窗口：修改 erb.config.js 中 windows 配置
  - 支持 Touchbar、Tray、Dock
  - 支持更新
- https://github.com/Devtography/electron-react-typescript-webpack-boilerplate
  - Ready to use Electron project template with React, Webpack and TypeScript seamlessly integrated
  - electron-builder for app packaging, with basic build config for Windows macOS included.
- https://github.com/codesbiome/electron-react-webpack-typescript-2022
  - Electron React Webpack Typescript Boilerplate with Custom Window and Titlebar Menus.

- https://github.com/ArcherGu/fast-vite-nestjs-electron
  - build vite + electron + nestjs projects. Build with Doubleshot, crazy fast!
  - https://github.com/Doubleshotjs/doubleshot
    - A split node backend and electron main process.
    - integrating the nodejs backend framework with electron to build a desktop application. 

- https://github.com/frankhale/electron-with-express /MIT/202310/ts
  - A simple project demonstrating how to spawn an Express app from Electron as well as providing server logs directly in the Electron app.

- https://github.com/jlongster/electron-with-server-example /202001/js
  - An example Electron app with a backend server all wired up via IPC

- https://github.com/ShakeefAhmedRakin/electron-react-ts-tailwind-shadcn-fastapi-template /202504/python/ts
  - fully-featured template for building cross-platform desktop apps with modern web and backend technologies
  - FastAPI backend bundled with PyInstaller
  - https://github.com/buzhiy/electron-fastapi-starter /202508/python/ts/vue
    - 基于 Electron + Vue3 + FastAPI 的桌面应用开发模板，支持后端 API 接入与前端界面集成。
  - https://github.com/micwonder/Electron-React-Typescript-boilerplate-with-FastAPI /202310
  - https://github.com/AgnoyZ/electron-fastapi-starter /202511
  - https://github.com/calvin44/Custom-Dashboard /202508/ts
    - a cross-platform desktop application for managing and visualizing data.
# examples
- https://github.com/danobot/notorious /GPLv3/202102/ts/友好
  - https://danobot.github.io/notorious-landing
  - Offline-first note taking application for desktop and the web
  - 依赖redux-pouchdb、blueprintjs、material-ui.v4、antd.v3、codemirror.v5、flexsearch、turndown
  - Notorious backend is a CouchDB database and an optional web interface for accessing Notorious through a web browser.

- https://github.com/pkolchanov/tablesapp /GPL/202209/js/archived
  - Tablesapp is an local-first table design tool.
  - All tables are ready for one-click cloud sharing. Hosted on Google Firebase.

- https://github.com/CatsJuice/electron-hero-window-demo /ts
  - window expansion animation hack with electron
  - 卡片内容变宽和缩窄的渐变动画

- https://github.com/sqlectron/sqlectron-gui /MIT/202202/ts/inactive
  - https://sqlectron.github.io/
  - lightweight SQL client desktop with cross database and platform support.

- https://github.com/netless-io/netless-app /MIT/202312/ts
  - https://netless-io.github.io/netless-app
  - Official Apps for the Agora Interactive Whiteboard.
  - https://github.com/netless-io/flat /MIT/202401/ts
    - https://flat.whiteboard.agora.io/
    - Project flat is the Web, Windows and macOS client of Agora Flat open source classroom.
  - https://github.com/netless-io/flat-server
    - Node.js server for the Agora Flat open source classroom.

- https://github.com/mattermost/desktop /2.2kStar/apache2/202601/ts
  - native desktop application that's built on Electron; it runs on Windows, Mac, and Linux.
  - Originally created as "electron-mattermost" by Yuya Ochiai.
  - Server dropdown for access to multiple servers
  - Deep Linking to open Mattermost links directly in the app
  - Runs in background to reduce number of open windows

- https://github.com/d2-projects/folder-explorer /MIT/202011/js/vue/inactive
  - 扫描目录，分析文件结构和统计信息，给任意文件添加备注，导出带注释的树形文本和其它多种数据格式，大大方便书写技术文档。

- https://github.com/WhiteMinds/LiveAutoRecord /LGPLv3/202401/ts/vue
  - 基于 Electron 的多平台直播自动录制软件
  - 普通用户可以直接使用客户端版本来自动录制需要回顾的直播与弹幕
  - 开发者可以基于插件系统来扩展可用的直播平台，或基于 @autorecord/manager 包和已实现的直播平台插件来做一款新的软件

- https://github.com/paulosabayomi/vscode-clone-with-electron-js-react-js-and-monaco-library 
  - /202410/ts

- https://github.com/1zilc/fishing-funds /GPLv3/202502/ts
  - 基金, 大盘, 股票, 虚拟货币状态栏显示小应用, 基于Electron开发, 支持MacOS, Windows, Linux客户端, 
  - 数据源来自天天基金, 蚂蚁基金, 爱基金, 腾讯证券等

- https://github.com/pure-admin/electron-pure-admin /MIT/202412/ts/vue
  - pure-admin官方electron版本
  - 当然平台还提供 tauri 版本的 https://github.com/pure-admin/tauri-pure-admin

- https://github.com/getstation/electron-process-manager /202410/js
  - This package provides a process manager UI for Electron applications.
  - It opens a window displaying a table of every processes run by the Electron application with information (type, URL for webContents, memory..).
  - Kill a process from the UI
  - Open developer tools for a given process
  - It can be useful to debug performance of an app with several webview.
  - It's inspired from Chrome's task manager.
  - Unfortunately, memory info are no longer available in Electron>=4 (see electron/electron#16179)
  - https://github.com/quantyle/electron-memory-profiler
    - a simple memory profiling and visualization tool written entirely in JavaScript. 
    - The frontend is a ReactJS/Electron desktop app and the backend is a simple NodeJS websocket server.

- https://github.com/oslabs-beta/fflow /MIT/202202/js/inactive
  - an easy-to-use open-source tool for all developers to create their React application.

- https://github.com/chenfan0/fideo-live-record /AGPLv3/202411/ts
  - 一款方便的直播录制软件! 支持tiktok, youtube, twitch, 抖音，虎牙，斗鱼，快手，微博，网易cc，bilibili，花椒, 淘宝, 京东
  - a live recording software based on React, Ffmpeg, Electron, Shadcn, FRP. 

- https://github.com/Gary-zy/dev-env-installer /202601/ts/vue
  - 基于 Electron + Vue 3 + TypeScript 构建的 macOS 桌面应用，旨在帮助开发者一键配置开发环境。
  - [macOS 开发环境一键安装工具，新电脑配环境再也不头疼 ](https://linux.do/t/topic/1407819)

- https://github.com/t8y2/unihub /202601/ts/vue
  - 现代化的跨平台工具集应用，支持强大的插件系统
  - [【开源发布】UniHub - 跨平台桌面工具集，支持插件扩展的效率神器 ](https://linux.do/t/topic/1407769)
    - 支持动态加载和管理插件，开发者可以轻松创建自己的插件
    - 细粒度权限控制 - 插件需要申请权限才能访问系统资源
    - 基于 GitHub Releases 的自动更新机制
  - 目前内置了几个实用插件：
    - JavaScript 格式化器 - 美化和压缩 JS 代码
    - JWT 工具 - 解析和验证 JWT Token

- https://github.com/DDULDDUCK/every-pdf /1kStar/MIT/202601/python
  - all-in-one desktop PDF toolkit to edit, convert, merge, and secure your documents. Built with Electron, Next.js, and Python.
  - PDF Editor (New!): Add text, signatures, images, and checkboxes to complete your documents.
  - Converting PDFs to different formats and converting different formats to PDFs 
  - split, merge, Watermark
  - Framework: Nextron (Next.js + Electron)
  - Backend: Python, FastAPI
  - Build/Deployment: Electron Builder
  - https://github.com/prasadlonare35/pdf-utility-platform /202601/python/js
    - Offline desktop PDF utility app (Electron + FastAPI)

- https://github.com/AntonioMrtz/SpotifyElectron /CC-NC/202511/python/ts
  - open-source music streaming desktop app made with Electron-React frontend and Python-FastAPI-MongoDB backend. 
  - Our goal is to replicate Spotify's core functionalities while incorporating user-requested features—such as the ability to upload personal music.
  - https://github.com/Swapnanilb/Svara
    - feature-rich music player built with React, Python, and Electron that streams music from YouTube 

- https://github.com/ephes/djdesk /MIT/202511/python
  - Django / Electron Tutorial App
  - `npm start` starts Django on an open port, waits for it to respond, and then shows the site in an Electron window.

- https://github.com/7gxycn08/ProtonMailView /apache2/202510/python/js/单文件
  - A lightweight, privacy-friendly ProtonMail desktop client for Windows.
  - Built with Electron, designed for a distraction-free inbox.
  - ProtonMailView wraps ProtonMail’s secure web interface in an Electron shell
  - Electron · Node.js · (Experemental) Python version using Pyside6 QWebEngineView

## notes-apps

- codex /195Star/CC-BY-NC-4.0/202401/ts/electron
  - https://github.com/jcv8000/Codex
  - https://codexnotes.com/
  - 依赖 prosemirror、katex、bootstrap4、jquery、highlight.js
  - A free note-taking software for programmers and Computer Science students

- https://github.com/dominiksta/wournal /LGPL/202408/ts/inactive
  - Simple "digitial paper" for note taking and PDF annotation. Heavily inspired by Xournal.
  - You can freely put your handwriting, text, images and vector graphics on a canvas that is about as easy to use as paper
  - Supports Windows and GNU/Linux. (Android support is planned, MacOS/iOS open to contribution)
  - Save single-page documents as SVG to interoperate with other software.
  - Wournal is a mostly relatively normal electron app, except that it uses `mvui` as a frontend framework
  - https://github.com/dominiksta/mvui /MIT/202408/ts
    - https://dominiksta.github.io/mvui/
    - A Minimalist Frontend Framework Based on Webcomponents

- https://github.com/husseinhareb/Coffee /202401/js
  - Text editor with file management and terminal integration using Electron.

- https://github.com/OpenMarch/OpenMarch /GPL/202502/ts
  - http://openmarch.com/
  - A free and open source drill-writing app built on web frameworks

- https://github.com/zonetti/zonote /MIT/202105/js/inactive
  - Cross-platform desktop note-taking app. 
  - Sticky notes with Markdown and Tabs. All in one .txt file.

## ai/llm-apps 👾

- https://github.com/ArjunDivecha/mlx-finetune-gui /202509/python/ts/inactive
  - A modern desktop application for fine-tuning Large Language Models using Apple's MLX framework on macOS. 
  - Built with Electron, React, TypeScript, and FastAPI.
  - MLX environment already set up at: `/Users/macbook2024/Library/CloudStorage/Dropbox/AAA Backup/A Working/Arjun LLM Writing/local_qwen/.venv`.
  - Training process management with MLX integration
  - Datasets: File picker for JSONL training data

- https://github.com/niiallenii/offline-ai-assistant /MIT/202509/python/html
  - Offline-first AI assistant PoC (Electron + FastAPI). 
  - Offline-first AI assistant starter built with Electron (desktop UI) + FastAPI (local API).
  - Ships with sample business data (invoices) and a working chat flow. 
  - Designed to add local LLM (llama.cpp / Ollama) + RAG securely in later phases.
  - Demo runs fully offline. LLM integration (e.g., Qwen2.5-7B-Instruct GGUF) is planned in Phase 3.
  - Ready for offline LLM (llama.cpp or Ollama) & RAG (Chroma/FAISS)

- https://github.com/dnzcany/resume-ai /MIT/202512/python/ts
  - AI-powered resume evaluation tool that analyzes PDFs/DOCX, scores resumes 0–100, checks ATS compatibility, and provides smart improvement suggestions.
  - Multiple Deployment Options: Web app, Docker, or Desktop App (Electron)

- https://github.com/moshehto/AI-assistant-app /202509/python/js
  - Desktop AI assistant built with Electron and FastAPI, supporting file uploads and local embeddings

- https://github.com/ManojRaga/journal-app /202509/python/js/inactive
  - A desktop journal application built with Electron that features AI-powered chat functionality using RAG

- https://github.com/CurtainShow/ai-labeling-tool /202601/python/js
  - An AI-powered image labeling tool with active learning capabilities, built with FastAPI, React, and Electron.

- https://github.com/con636/PicFinder-AI /MIT/202601/python/ts/vue
  - Search your local images effortlessly with PicFinder AI, a privacy-focused tool using natural language and AI for instant results.
  - No special hardware like a GPU is required.
  - ChromaDB: Used for efficient image storage.
  - https://github.com/Breathinggg/PicFinder-AI

- https://github.com/asifdotpy/open-talent-local-ai /MIT/202601/python/ts
  - https://opentalent-showcase.vercel.app/
  - Offline, desktop-first local AI interview platform (Ollama/Piper, Granite 4; not affiliated with LinkedIn HR company Open Talent).
  - Using Piper (TTS) ensures instant voice responses, eliminating "awkward cloud lag."
  - Built on IBM Granite 4, optimized for coding and business logic, not creative fiction.
  - Ollama Integration: Marketed as "Universal Compatibility"

- https://github.com/ihatecsv/deepseek-ocr-client /713Star/MIT/202512/python/js
  - A real-time Electron-based desktop GUI for DeepSeek-OCR， 暂不支持webui
  - GPU acceleration (CUDA)
  - Flask backend manages the model, Electron frontend for the UI.
  - 识别文本是流式输出
  - 🐛 仅支持image，暂不支持pdf; 不支持批处理
  - 使用针对mac优化的模型 https://huggingface.co/Dogacel/DeepSeek-OCR-Metal-MPS
  - [A quickly put together a GUI for the DeepSeek-OCR model that makes it a bit easier to use : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ocx27p/a_quickly_put_together_a_gui_for_the_deepseekocr/)

- https://github.com/scarletkc/vexor /MIT/202601/python/js/vue
  - a semantic search engine that builds reusable indexes over files and code. 
  - It supports configurable embedding and reranking providers, and exposes the same core through a Python API, a CLI tool, and an optional desktop frontend.
  - Vexor supports both remote API providers (openai, gemini, custom) and a local provider (local):
    - Local provider ignores api_key/base_url and only uses model plus local_cuda (CPU/GPU switch).

- https://github.com/volcengine/MineContext /4.8kStar/apache2/202601/python/ts
  - open-source, proactive context-aware AI partner, dedicated to bringing clarity and efficiency to your work, study and creation.
  - Based on an underlying contextual engineering framework, it actively delivers high-quality information such as insights, daily/weekly summaries, to-do lists, and activity records.
  - After starting the recording, your context will gradually be collected. It will take some time to generate value.
  - frontend is a cross-platform desktop application built with Electron, React, and TypeScript, providing a modular, maintainable, and high-performance foundation for desktop development.
# server

# files

- https://github.com/kbrisso/file-base /MIT/202312/ts/inactive
  - A database for managing your files using Electron and React.
  - You can tag, add notes, organize, categorize, filter, search and quickly find your needed files with an easy-to-use application
  - Filebase does not modify your existing files or directories 
  - uses `PouchDB` to store file and directory structure using a tree type structure, each of these nodes in the tree can have metadata added to it that will be searchable
- https://github.com/tedb-org/tedb-electron-storage /201801/ts
  - Storage driver for Electron, based on one file per collection item.

- https://github.com/warpdesign/react-explorer /MIT/202405/ts/inactive
  - File manager written in TypeScript, React, Blueprint and packaged with Electron
  - Plugin-based: local supported for now, ftp in the works
  - 依赖blueprintjs、electron-window-state、mobx-react、react-dnd、react-virtual
  - Split-view window
  - Tabs support
  - Media File Preview
  - React-Explorer works on any modern Windows, Mac or Linux 64bit computer.

- https://github.com/fiahfy/zephy /MIT/2024501/ts
  - Simple File Browser based on Electron.
  - Image, Text and Video Preview
  - Tree View Display

- https://github.com/msihly/Medior /NALic/202412/ts
  - https://github.com/msihly/Media-Viewer
  - The tag-based local media management system.
  - Electron app for managing media files in a self-contained portable database. 
  - 依赖dnd-kit、mui.v5、@tensorflow/tfjs、trpc、mobx-react-lite、mongoose、mongodb-memory-server、react-window
  - Portable offline database with support for distributed file storages
  - Hierarchical (parent / child) tagging system with aliases and regular expressions
  - Features a hierarchical tagging system with comprehensive search and sorting, automated tag creation / parsing and batch processes, collections / albums, AI face recognition, Stable Diffusion integration, and built-in media viewers.
  - A self-hosted, portable Electron app for indexing and viewing media files featuring hierarchical tags as well as several features inspired by cloud storage providers that are missing from Windows File Explorer and most contemporary alternatives. 
  - It has been refined over several iterations with the primary goal of optimizing performance at scale and the UX of batch workflows.

- https://github.com/suleymanlaarabi/Aurora-Explorer /MIT/202401/ts/inactive
  - powerful file management tool, built with Electron, ReactTS, and ChakraUI

- https://github.com/lzldev/shelf-desktop /GPLv3/202312/ts/inactive
  - Electron app for file organization

- https://github.com/SuboptimalEng/orbital /MIT/202110/ts/inactive
  - desktop app that allows you to search, filter, and preview video files on your computer - like YouTube for your local file system.

- https://github.com/caorushizi/oss-client /202401/ts
  - 七牛云文件仿百度网盘文件夹管理，上传下载，删除。

- https://github.com/sindresorhus/electron-serve /MIT/202401/js
  - Static file serving for Electron apps

- https://github.com/Michael-Vanderford/electron-file-manager /GPLv3/202405/js/inactive
  - Linux File Manager - Built with Electron
  - Audio or Video to Audio conversion - Requires ffmpeg
  - [How to transport to Winodws platform?_202312](https://github.com/Michael-Vanderford/electron-file-manager/issues/4)
    - Sorry, There a currently no plans to support the Windows platform.
  - https://github.com/Michael-Vanderford/string-file-manager

- https://github.com/imyuanx/sharing-GUI /MIT/202310/js/inactive
  - The Sharing GUI is a client that is used to share files across multiple devices (iOS, Android, macOS, Windows, Linux...)
  - Only one client is required, other devices use WEB. (client support macOS, Windows, Linux)
  - Support ngrok, quickly share to the public network
# storage
- https://github.com/oguz-yilmaz/localforage-file-system-adapter /202312/ts/inactive
  - A file system adapter for LocalForage designed specifically for Electron applications, providing simple file-based storage with a familiar LocalForage API.
  - This adapter implements LocalForage's driver interface to store data in the local file system, making it ideal for Electron apps that need persistent storage without SQLite or other database solutions.
  - Simple file-based storage
  - Simple key-value storage only, Basic string-based storage
  - Not suitable for large datasets
  - Lightweight alternative to SQLite
  - No encryption (use Electron's built-in encryption if needed)

- https://github.com/sindresorhus/electron-store /MIT/202305/js
  - Simple data persistence for your Electron app or module
  - Save and load user preferences, app state, cache, etc
  - Electron doesn't have a built-in way to persist user settings and other data. This module handles that for you
  - The data is saved in a JSON file named config.json in `app.getPath('userData')`.
  - You can use this module directly in both the main and renderer process
  - https://github.com/rt2zz/redux-persist
  - https://github.com/ryanwillis/reduxjs-toolkit-persist

- https://github.com/alexiusacademia/electron-db /MIT/202011/js/inactive
  - Electron module that acts as database management and uses flat file database (json file) to store tables.
  - Flat file database solution for electron and other Nodejs apps.
  - The json file is saved on the application folder or you can specify the location for the database to be created

- https://github.com/tndrle/node-sqlite3-wasm /MIT/202502/js
  - WebAssembly port of SQLite3 for Node.js with file system access
  - node-sqlite3-wasm supports persistent storage with direct file access by implementing an SQLite OS Interface or "VFS" that translates SQLite file access to Node.js' file system API.
# utils
- https://github.com/nativefier/nativefier /MIT/202309/ts/archived
  - a command-line tool to easily create a “desktop app” for any web site with minimal fuss. 
  - Apps are wrapped by Electron
  - [Nativefier is unmaintained _202309](https://github.com/nativefier/nativefier/issues/1577)
    - Nativefier was built a couple of years ago before the ability to create shortcuts for websites in Chrome, or similarly on Firefox. 
    - Users who want to build and use their own website wrappers should strongly prefer these options as they are protected from security vulnerabilities by the browser's self updating mechanism.
    - Otherwise, if the use case is to build a bespoke app wrapping a website for distribution, consider using Electron directly which offers much more flexibility.

- https://github.com/flaviodelgrosso/reactronite /MIT/202510/ts
  - modern, feature-rich Electron kit for building cross-platform desktop applications with React and Vite
  - Clean, scalable project structure with separation of concerns
  - Hot Module Replacement (HMR) with Vite for instant feedback
  - Custom Titlebar - Native-looking titlebar with integrated window controls
  - Secure IPC Communication - Safe main-renderer process communication
  - Window State Management - Remembers window size, position, and state

- https://github.com/alex8088/electron-toolkit /MIT/202502/ts
  - Toolkit for Electron

- https://github.com/sindresorhus/electron-dl /MIT/202310/js
  - Simplified file downloads for your Electron app
  - Support for `BrowserWindow` and `BrowserView`.

- https://github.com/spaceagetv/electron-file-download /MIT/202308/ts
  - A simple module to download files via Electron's main process. 
  - Manages the download process and exposes a simple API to listen for events including progress, success, failure, and cancellation. 
  - The module also exposes Electron's DownloadItem methods for pausing, resuming, and canceling the download.

- https://github.com/sindresorhus/electron-util /MIT/202401/ts
  - Useful utilities for Electron apps and modules
  - There are three parts of this package, “shared”, “main”, and “node”. The “shared” part works in both the main or rendered process. The “main” part works only in the main process. The “node” part is for Node.js-only APIs (not Electron).
  - To use features from the “main” part in the renderer process, you will need to set up IPC channels.

- https://github.com/kunalnagar/encrypt0r /MIT/202211/ts
  - App to encrypt and decrypt your files with a passphrase
  - encrypt0r provides a simple drag and drop interface to encrypt/decrypt your files using a password.
  - When running the app on Mac/Windows, you might get an untrusted developer warning. This is because the app is not signed by the developer (aka me). Signing an app requires a Signing Certificate that costs hundreds of dollars per year
- https://github.com/gjtiquia/mini-file-encryptor /202401/ts
  - A secure, offline, minimalistic file encryptor. Built with Electron.
  - Encrypt any folder into a password-protected file.
  - Securely encrypted with AES256, being fully offline reduces the risk of leaking sensitive data to the Internet.
- https://github.com/abhishekY495/File-encryptor /MIT/202311/js
  - An app that Encrypts / Decrypts your files with a password. 
  - Built using Electron and TailwindCSS
  - App works Offline.

- https://github.com/itsKayWat/Exe-Decompiler /202503/python/inactive
  - A powerful GUI tool for decompiling and analyzing Electron-based .exe applications. 
  - Features ASAR extraction, source map analysis, and live modifications with recompilation support. Built for developers and security researchers.

- https://github.com/rhysd/electron-in-page-search /MIT/201906/ts/inactive
  - This package provides Chrome's native in-page search feature to Electron applications.

- https://github.com/sentialx/electron-extensions /GPLv3/202007/ts/inactive
  - allow you to use Chrome extensions APIs with Electron.
  - https://github.com/getstation/electron-chrome-extension /inactive

- https://github.com/ArekSredzki/electron-release-server /MIT/202310/js
  - self-hosted release server for electron applications, compatible with auto-updater.
  - A node web server which serves & manages releases of your Electron App, and is fully compatible with Squirrel Auto-updater (which is built into Electron).

- https://github.com/artiebits/pdf-to-printer /MIT/202303/ts/archived
  - A utility for printing PDFs and images from Node.js and Electron.
  - Available only on Windows.
  - https://github.com/artiebits/unix-print

- https://github.com/weolar/miniblink49 /201911/cpp
  - 一个小巧、轻量的浏览器内核，用来取代wke和libcef

- https://github.com/nathanbuchar/electron-settings /MIT/202404/ts/inactive
  - A simple persistent user settings framework for Electron.

- https://github.com/junhaoliao/iCtrl /MIT/202501/python/js
  - A Simple VNC + SSH Shell + SFTP Client
  - SSH Remote Web Service / Desktop Client (Previously known as UG_Remote)
  - File Manager via SFTP
  - Graphical Remote via VNC
  - Terminal Console via SSH

- https://github.com/ECRomaneli/electron-findbar /MIT/202406/js/inactive
  - Chrome-like findbar for your Electron application
  - The electron-findbar is a BrowserWindow component designed to emulate the Chrome findbar layout, leveraging the webContents.findInPage method to navigate through matches. 
  - Inter-process communication (IPC) is used for interaction between the main and renderer processes.
  - To optimize memory usage, the Findbar window is created only when the findbar is open. The implementation is lightweight, including only essential code.

## utils-file

- https://github.com/sindresorhus/electron-serve /476Star/MIT/202509/js/inactive
  - Static file serving for Electron apps
  - It serves files if they exist, and falls back to `index.html` if not, which means you can use router modules like react-router, vue-router, etc.

## utils-messaging

- https://github.com/linonetwo/electron-ipc-cat /MIT/202307/ts
  - Passing object and type between Electron main process and renderer process simply via preload script.
  - In latest electron, the remote module is deprecated, and you are required to passing data using IPC. 
  - Based on frankwallis/electron-ipc-proxy, and used in TiddlyGit-Desktop.
    - electron-ipc-proxy doesn't work well when we have `contextIsolation: true`, so here we have electron-ipc-cat
  - Only plain objects can be passed between the 2 sides of the proxy, as the data is serialized to JSON, so no functions or prototypes will make it across to the other side.
  - https://github.com/frankwallis/electron-ipc-proxy /MIT/202010/ts
    - Transparent asynchronous electron remoting using IPC.

- https://github.com/daltonmenezes/interprocess /MIT/202308/ts
  - https://daltonmenezes.github.io/interprocess/
  - A scalable and type-safe Electron IPC management tool with enhanced DX
  - Electron IPC is good, but difficult to maintain and scale, either because of the numerous channels you have to remember, or because of the inconsistent API between processes and the absence of inferred types of your channels and handlers.
  - invoke and handle methods in both processes with the same expected behavior

## utils-worker

- https://github.com/bjrmatos/electron-html-to /MIT/202206/js
  - scalable html conversion using electron workers 
  - Custom converters: Converters are functions that run in the electron process

## utils-browser

- https://github.com/samuelmaddock/electron-browser-shell /450Star/GPL+MIT/202503/ts
  - A minimal, tabbed web browser with support for Chrome extensions—built on Electron.
  - 🍴 forks
  - https://github.com/fvulich/electron-chrome-extensions

- https://github.com/wexond/browser-base /PaidLic/ts/最近版本v5.2_202102/archived
  - Wexond Base is a modern web browser, built on top of modern web technologies such as Electron and React, that can also be used as a framework to create a custom web browser
  - wexond: We've also moved to Chromium as Electron just lacked many important browser features._202111
    - https://twitter.com/sentialx/status/1457867597156917251
    - And we had our fork of Electron which tried to import those features from Chromium, but it was just too much to manually implement all of them, at least for me alone.
  - Wexond has been acquired_202211
    - https://twitter.com/sentialx/status/1588103883494227971
  - [forks](https://github.com/wexond/browser-base/forks)
    - https://github.com/Alex313031/promethium /GPL
    - https://github.com/skyebrowser/skye /GPL
    - https://github.com/Nalem14/browser-base

- https://github.com/beakerbrowser/beaker /MIT/202012/js/inactive
  - An experimental peer-to-peer Web browser

- https://github.com/bamidev/browser-window /MIT/202403/rust/cpp
  - A simple, cross-platform, optionally async, optionally threadsafe, electron-like browser window framework for Rust.
  - Just like Electron.js, you can use it to build a GUI with HTML, CSS & JS
  - There are currently three different underlying browser frameworks that can be selected: CEF, WebkitGTK or Edge WebView2. Each framework has their pros and cons, but CEF will be the most feature complete because it has the best cross-platform support 

- https://github.com/minbrowser/min /apache2/202502/js
  - https://minbrowser.org/
  - A fast, minimal browser that protects your privacy
  - Min supports installing userscripts to extend its functionality.

- https://github.com/hulufei/electron-as-browser /MIT/202401/js/inactive
  - A node module to help build browser like windows in electron.
  - Made with BrowserView instead of webview

- https://github.com/tamkeen-tms/electron-window-manager /MIT/202008/js/inactive
  - A NodeJs module for Electron (Atom Shell, previously) that will help you create, control, manage and connect your application windows very easily.
  - Most of the applications created using Electron are one-window applications
  - if you are to build a multi-window Electron application, then you may want to have a look at this package module.

- https://github.com/wavebox/waveboxapp /1.3kStar/MPLv2/202106/js/open2close
  - https://wavebox.io/
  - Browser for Work
  - Wavebox gives you customizable toolbars, sleeping tabs, cookie containers and multiple profile
  - Wavebox 10, a complete **fork of Chromium** launched in 2019, but if you're looking for the Electron based Wavebox Classic, there's an archive of the code here
# tauri
- https://github.com/12joan/ping-ui
  - A simple GUI for the ping command-line utility built using Tauri.
  - Requires ping to be in the PATH and for the output of ping to have the following format
# nwjs
- https://github.com/nwutils/electron-to-nwjs /js
  - This project aims to build an Electron app as a NW.js app.
  - The Electron main file is converted into the NW.js main file using webpack, by replacing the Electron modules with compatibility layers that make them use the NW.js commands instead. 
# more
- https://github.com/mozilla/positron /201703/cpp/archived
  - a experimental, Electron-compatible runtime on top of Gecko

- https://github.com/GoogleChromeLabs/carlo /apache2/201906/js/deprecated
  - Carlo provides Node applications with Google Chrome rendering capabilities, communicates with the locally-installed browser instance using the `Puppeteer` project, and implements a remote call infrastructure for communication between Node and the browser.
  - Carlo prints an error message when Chrome can not be located.
  - The application can be bundled into a single executable using `pkg`.
  - 🆚️ What was the motivation when we already have Electron and NW.js?
    - One of the motivations of this project is to demonstrate how browsers that are installed locally can be used with Node out of the box.
    - Node v8 and Chrome v8 engines are decoupled in Carlo
