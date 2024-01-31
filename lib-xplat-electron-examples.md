---
title: lib-xplat-electron-examples
tags: [client-desktop, electron, examples, toc]
created: 2021-01-16T20:49:44.833Z
modified: 2024-01-31T19:13:11.286Z
---

# lib-xplat-electron-examples

# guide
- tips
  - 不建议基于electron实现自定义浏览器，要考虑支持各浏览器自带的扩展商店，可在自己的应用层实现
  - ? electron-for-android/ios vs apps

- resources
  - https://github.com/sindresorhus/awesome-electron
# popular
- https://github.com/Elanis/web-to-desktop-framework-comparison
  - 🆚️ Web to Desktop framework comparison
  - an objective comparison of multiple framework that grant us to "transform" our web app to desktop application formats.
  - Electron, NW. JS, Tauri, NodeGui(Qt6), Neutralino, Wails, Flutter

- https://github.com/electron/fiddle /MIT/202401/ts
  - https://electronjs.org/fiddle
  - The easiest way to get started with Electron
  - Try Electron without installing any dependencies: Fiddle includes everything you'll need to explore the platform. 

- https://github.com/electron/apps /MIT/202310/js/无详情页
  - https://www.electronjs.org/apps
  - A collection of apps built on Electron

- https://github.com/jupyterlab/jupyterlab-desktop /BSD/202401/ts
  - JupyterLab desktop application, based on Electron.
  - Sessions represent local project launches and connections to existing JupyterLab servers. Each JupyterLab UI window in the app is associated with a separate session and sessions can be restored with the same configuration later on.
  - Each launch of JupyterLab in a different working directory is a separate project and projects can have their own configuration such as Python environment and UI layout.

- https://github.com/gristlabs/grist-electron /apache2/202311/ts
  - Desktop Grist, packaged with Electron
  - It does not need the internet, and will work fine when offline

- kikko /75Star/MIT/202401/ts
  - https://github.com/kikko-land/kikko
  - https://kikko-doc.netlify.app/
  - Powerful SQLite adapter for web, mobile and desktop. Build reactive UI on top of it
  - It brings transaction support, middlewares for queries, and SQLite adapters for the most popular platforms.

- https://github.com/Icon-Shelf/icon-shelf /MIT/202311/ts
  - https://icon-shelf.github.io/
  - SVG icon manager for developers.
  - Link the icons folder of your project to Icon Shelf and see all your icons in an easily previewable manner. 
  - File-based (adding, deleting, modifying icons in app get reflected in file-system as well.)

- https://github.com/sprout2000/leafview /MIT/202401/ts
  - Minimalist image viewer based on Leaflet.js and Electron.
  - Browse the images in a folder
  - 示例不是地图

- https://github.com/wulkano/Kap /MIT/202210/ts
  - open-source screen recorder built with web technology

- https://github.com/xushengfeng/eSearch /GPLv3/202401/ts
  - https://esearch-app.netlify.app/
  - eSearch 是Information-portal的:electron: 重写版(顺便加了亿些功能)
  - 主要是想在 Linux 上(win 和 mac 上也能用)实现锤子大爆炸或小米传送门这样的屏幕搜索功能，当然也是一款方便的截屏软件。
  - 截屏 离线OCR 搜索翻译 以图搜图 贴图 录屏 滚动截屏 
  - 本地 OCR 由`PaddleOCR`的模型提供支持。

- https://github.com/027xiguapi/pear-rec /apache2/202401/ts
  - https://027xiguapi.github.io/pear-rec/
  - 跨平台的截图、录屏、录音、录像软件
  - react + electron + vite + viewerjs + plyr + aplayer + react-screenshots.
  - 支持网页版、pc版

- https://github.com/likaia/js-screen-shot /MIT/202401/ts
  - https://www.kaisir.cn/js-screen-shot/
  - web端自定义截屏插件(原生JS版)
  - 支持electron环境下使用插件

- https://github.com/rubickCenter/rubick /MIT/202312/ts
  - https://rubickcenter.github.io/docs
  - Open-source plugin-based desktop efficiency toolbox. 
  - 基于 electron 的开源工具箱，自由集成丰富插件。
  - 支持基于 webdav 的多端数据同步，支持内网部署。
  - rubick 插件全部托管在 npm 仓库，rubick 插件的安装、使用、删除就是 npm 包的安装、使用、删除

- https://github.com/httptoolkit/httptoolkit-desktop /AGPLv3/202401/ts
  - https://httptoolkit.com/
  - Electron wrapper to build and distribute HTTP Toolkit for the desktop
  - the desktop build setup for HTTP Toolkit, a cross-platform & open-source HTTP(S) debugging proxy, analyzer & client.
  - HTTP Toolkit consists of two runtime parts: a UI, written as a single-page web application, and a server, written as a node.js CLI application.
  - built using Electron Builder.
  - This isn't the only way to run HTTP Toolkit! It's the most convenient option for most users, but it's also completely possible to run the server as a standalone tool and open the UI (hosted at https://app.httptoolkit.tech) in any browser you'd like.

- codex /195Star/CC-BY-NC-4.0/202401/ts/electron
  - https://github.com/jcv8000/Codex
  - https://codexnotes.com/
  - 依赖 prosemirror、katex、bootstrap4、jquery、highlight.js
  - A free note-taking software for programmers and Computer Science students
- https://github.com/1943time/bluestone /AGPLv3/202401/ts
  - https://www.bluemd.me/
  - 青石是一个开源的所见即所得Markdown编辑器
  - markdown的table元素也不利于书写，双栏模式并不利于聚焦，所以开发了青石编辑器。他以富文本的方式结合markdown的编辑习惯来帮助你日常记录，并以标准的markdown格式保存
  - Using shiki as a code shader to make code highlights more fine-grained
  - 依赖mobx-react-lite、remark-gfm

- https://github.com/picturama/picturama /MIT/202203/ts/inactive
  - Digital image organizer powered by the web
  - don't upload your personal photos to cloud 
  - Read various photo formats: JPG, PNG, TIF, WebP, HEIC / HEIF
  - Read raw formats of a whole bunch of cameras (only on Mac and Linux, see Issue #25)
  - Tags/Favorites

- https://github.com/low-teck/vault
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.
  - https://github.com/codegiik/electron-react-nedb-boilerplate

- https://github.com/wavebox/waveboxapp
  - https://wavebox.io/
  - Browser for Work
  - Wavebox gives you customizable toolbars, sleeping tabs, cookie containers and multiple profile
  - Wavebox 10, a complete fork of Chromium launched in 2019, but if you're looking for the Electron based Wavebox Classic, there's an archive of the code here

- https://github.com/samuelmaddock/electron-browser-shell /ts
  - A minimal, tabbed web browser with support for Chrome extensions—built on Electron.
  - 🍴 forks
  - https://github.com/fvulich/electron-chrome-extensions

- https://github.com/Electron-Store/electron-app-store /inactive
  - A Cross-Platform App Store for Electron.js Apps

- https://github.com/opensumi/ide-electron /MIT/202401/ts
  - https://opensumi.com/
  - OpenSumi Electron Version
# examples-starter
- https://github.com/electron-react-boilerplate/electron-react-boilerplate /MIT/202309/ts
  - https://electron-react-boilerplate.js.org/
  - Electron React Boilerplate uses Electron, React, React Router, Webpack and React Fast Refresh.
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

- https://github.com/garrylachman/ElectroCRUD /MIT/202306/ts
  - http://garrylachman.github.io/ElectroCRUD/
  - Database CRUD Application Built on Electron | MySQL, Postgres, SQLite
  - 依赖chakra-ui.v2、@saas-ui/react、@reduxjs/toolkit、knex

- https://github.com/cawa-93/vite-electron-builder /MIT/202401/ts
  - a template for secure electron applications. Written following the latest safety requirements
  - Under the hood is Vite and electron-builder for packaging.
  - TypeScript + Vue/React/Angular/Svelte/Vanilla

- https://github.com/alex8088/electron-vite /MIT/202401/ts
  - https://electron-vite.org/
  - 新一代 Electron 开发构建工具，支持源代码保护
  - 编译为 V8 字节码以保护源代码。
  - 依赖esbuild
  - 支持electron-builder和forge
  - [默认创建的工程编译出exe 后启动比较慢，对比 elctron-forge](https://github.com/alex8088/electron-vite/issues/181)
    - 编译后即是electron可运行的cjs标准文件和electron-forge无异。

- https://github.com/electron-vite/electron-vite-react /MIT/202401/ts
  - https://electron-vite.github.io/
  - Electron + Vite + React + Sass boilerplate.
  - https://github.com/diego3g/electron-typescript-react

- https://github.com/ccorcos/electron-architecture /4Star/CC0-1/202108/ts
  - This project is a boilerplate electron app with a thoughtfully designed architecture
  - Main and renderer processes manage state using a Redux-like state machine.
  - Electron BrowserWindows are controlled declaratively through the application state.
  - Electron IPC uses a Proxy enabling "Rename Symbol" and "Find All References" in VSCode.
  - https://github.com/ccorcos/electron-boilerplate /202012/ts
    - uses TypeScript and demonstrates using a preload script to interact with the native APIs.

  - https://github.com/codegiik/electron-react-nedb-boilerplate
- https://github.com/sprout2000/electron-react-ts
  - An Electron boilerplate with hot reloading for React and TypeScript.
- https://github.com/fantasticit/electron-react-boilerplate
  - 各窗口均采用 React 开发，也可根据需要更改为其他框架
  - 支持多窗口：修改 erb.config.js 中 windows 配置
  - 支持 Touchbar、Tray、Dock
  - 支持更新
- https://github.com/Devtography/electron-react-typescript-webpack-boilerplate
  - Ready to use Electron project template with React, Webpack and TypeScript seamlessly integrated
  - electron-builder for app packaging, with basic build config for Windows macOS included.
- https://github.com/codesbiome/electron-react-webpack-typescript-2022
  - Electron React Webpack Typescript Boilerplate with Custom Window and Titlebar Menus.

- https://github.com/garrylachman/ElectroCRUD
  - ElectroCRUD is Open Source Database CRUD (Create, Read, Update, Delete) Software. No Code Needed

- https://github.com/ArcherGu/fast-vite-nestjs-electron
  - build vite + electron + nestjs projects. Build with Doubleshot, crazy fast!
  - https://github.com/Doubleshotjs/doubleshot
    - A split node backend and electron main process.
    - integrating the nodejs backend framework with electron to build a desktop application. 

- https://github.com/frankhale/electron-with-express /MIT/202310/ts
  - A simple project demonstrating how to spawn an Express app from Electron as well as providing server logs directly in the Electron app.

- https://github.com/jlongster/electron-with-server-example /202001/js
  - An example Electron app with a backend server all wired up via IPC
# examples
- https://github.com/zonetti/zonote /202105/inactive
  - Cross-platform desktop note-taking app. 
  - Sticky notes with Markdown and Tabs. All in one .txt file.

- https://github.com/danobot/notorious /GPLv3/202102/ts/友好
  - https://danobot.github.io/notorious-landing
  - Offline-first note taking application for desktop and the web
  - 依赖redux-pouchdb、blueprintjs、material-ui.v4、antd.v3、codemirror.v5、flexsearch、turndown
  - Notorious backend is a CouchDB database and an optional web interface for accessing Notorious through a web browser.

- https://github.com/pkolchanov/tablesapp
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

- https://github.com/d2-projects/folder-explorer /MIT/202011/js/vue/inactive
  - 扫描目录，分析文件结构和统计信息，给任意文件添加备注，导出带注释的树形文本和其它多种数据格式，大大方便书写技术文档。

- https://github.com/WhiteMinds/LiveAutoRecord /LGPLv3/202401/ts/vue
  - 基于 Electron 的多平台直播自动录制软件
  - 普通用户可以直接使用客户端版本来自动录制需要回顾的直播与弹幕
  - 开发者可以基于插件系统来扩展可用的直播平台，或基于 @autorecord/manager 包和已实现的直播平台插件来做一款新的软件

## file-manager

- https://github.com/SuboptimalEng/orbital /MIT/202110/ts
  - desktop app that allows you to search, filter, and preview video files on your computer - like YouTube for your local file system.

- https://github.com/caorushizi/oss-client /202401/ts
  - 七牛云文件仿百度网盘文件夹管理，上传下载，删除。
# utils
- https://github.com/nativefier/nativefier /MIT/202309/ts/archived
  - a command-line tool to easily create a “desktop app” for any web site with minimal fuss. 
  - Apps are wrapped by Electron
  - [Nativefier is unmaintained _202309](https://github.com/nativefier/nativefier/issues/1577)
    - Nativefier was built a couple of years ago before the ability to create shortcuts for websites in Chrome, or similarly on Firefox. 
    - Users who want to build and use their own website wrappers should strongly prefer these options as they are protected from security vulnerabilities by the browser's self updating mechanism.

- https://github.com/alexiusacademia/electron-db
  - let you simplify database creation and operation on a json file.

- https://github.com/sindresorhus/electron-store /MIT/202305/js
  - Simple data persistence for your Electron app or module
  - Save and load user preferences, app state, cache, etc
  - Electron doesn't have a built-in way to persist user settings and other data. This module handles that for you
  - The data is saved in a JSON file named config.json in `app.getPath('userData')`.
  - You can use this module directly in both the main and renderer process

- https://github.com/sentialx/electron-extensions /GPLv3/202007/ts/inactive
  - allow you to use Chrome extensions APIs with Electron.
  - https://github.com/getstation/electron-chrome-extension /inactive

- https://github.com/ArekSredzki/electron-release-server /MIT/202310/js
  - self-hosted release server for electron applications, compatible with auto-updater.
  - A node web server which serves & manages releases of your Electron App, and is fully compatible with Squirrel Auto-updater (which is built into Electron).

- https://github.com/weolar/miniblink49 /201911/cpp
  - 一个小巧、轻量的浏览器内核，用来取代wke和libcef
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
