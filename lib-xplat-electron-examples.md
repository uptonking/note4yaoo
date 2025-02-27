---
title: lib-xplat-electron-examples
tags: [client-desktop, electron, examples, toc]
created: 2021-01-16T20:49:44.833Z
modified: 2024-01-31T19:13:11.286Z
---

# lib-xplat-electron-examples

# guide
- tips
  - ~~不建议基于electron实现自定义浏览器，要考虑支持各浏览器自带的扩展商店，可在自己的应用层实现~~
  - ? electron-for-android/ios vs apps
  - web+pc: vscode, jupyter, (rstudio)

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
  - It also includes examples for every API available in Electron
  - Fiddle is not an IDE – it is however an excellent starting point.

- https://github.com/electron/apps /MIT/202310/js/无详情页
  - https://www.electronjs.org/apps
  - A collection of apps built on Electron

- https://github.com/desktop/desktop /MIT/202502/ts
  - GitHub Desktop is an open-source Electron-based GitHub app. 
  - It is written in TypeScript and uses React.
  - Focus on what matters instead of fighting with Git.
  - Linux is not officially supported; however, you can find installers created for Linux from a fork of GitHub Desktop in the Community Releases section.

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

- https://github.com/Icon-Shelf/icon-shelf /MIT/202311/ts/inactive
  - https://icon-shelf.github.io/
  - SVG icon manager for developers.
  - Link the icons folder of your project to Icon Shelf and see all your icons in an easily previewable manner. 
  - File-based (adding, deleting, modifying icons in app get reflected in file-system as well.)
  - 依赖codemirror、dexie、react-query

- https://github.com/sprout2000/leafview /MIT/202401/ts
  - Minimalist image viewer based on Leaflet.js and Electron.
  - Browse the images in a folder
  - 示例不是地图

- https://github.com/wulkano/Kap /MIT/202210/ts/inactive
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
- https://github.com/nashaofu/screenshots /MIT/202311/ts
  - https://nashaofu.github.io/screenshots/
  - 基于electron和react的截图插件，可以快速地实现截图功能，并支持多种截图操作，例如马赛克、文本、画笔、箭头、椭圆和矩形

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
  - Read raw formats of a whole bunch of cameras (only on Mac and Linux, see Issue #25)
  - Tags/Favorites

- https://github.com/low-teck/vault
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.
  - https://github.com/codegiik/electron-react-nedb-boilerplate

- https://github.com/wavebox/waveboxapp /1.3kStar/MPLv2/202106/js/open2close
  - https://wavebox.io/
  - Browser for Work
  - Wavebox gives you customizable toolbars, sleeping tabs, cookie containers and multiple profile
  - Wavebox 10, a complete **fork of Chromium** launched in 2019, but if you're looking for the Electron based Wavebox Classic, there's an archive of the code here

- https://github.com/samuelmaddock/electron-browser-shell /ts
  - A minimal, tabbed web browser with support for Chrome extensions—built on Electron.
  - 🍴 forks
  - https://github.com/fvulich/electron-chrome-extensions

- https://github.com/Electron-Store/electron-app-store /MIT/202112/js/vue/inactive
  - A Cross-Platform App Store for Electron.js Apps

- https://github.com/opensumi/ide-electron /MIT/202401/ts
  - https://opensumi.com/
  - OpenSumi Electron Version

- https://github.com/pd4d10/debugtron /MIT/202407/ts
  - Debugtron is an app to debug in-production Electron based app. It is also built with Electron.
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
  - https://github.com/codegiik/electron-react-nedb-boilerplate

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

- https://github.com/paulosabayomi/vscode-clone-with-electron-js-react-js-and-monaco-library 
  - /202410/ts
# server

# files

- https://github.com/kbrisso/file-base /MIT/202309/js/ts
  - A database for managing your files using Electron and React.
  - You can tag, add notes, organize, categorize, filter, search and quickly find your needed files with an easy-to-use application
  - Filebase does not modify your existing files or directories 
  - uses `PouchDB` to store file and directory structure using a tree type structure, each of these nodes in the tree can have metadata added to it that will be searchable

- https://github.com/warpdesign/react-explorer /MIT/202303/ts/inactive
  - File manager written in TypeScript, React, Blueprint and packaged with Electron
  - Split-view window
  - Plugin-based: local supported for now, ftp in the works
  - 依赖blueprintjs、electron-window-state、mobx-react、react-dnd、react-virtual

- https://github.com/fiahfy/zephy /MIT/202401/ts
  - Simple File Browser based on Electron.
  - Image, Text and Video Preview
  - Tree View Display

- https://github.com/suleymanlaarabi/Aurora-Explorer /MIT/202401/ts
  - powerful file management tool, built with Electron, ReactTS, and ChakraUI

- https://github.com/lzldev/shelf-desktop /GPLv3/202312/ts
  - Electron app for file organization

- https://github.com/SuboptimalEng/orbital /MIT/202110/ts
  - desktop app that allows you to search, filter, and preview video files on your computer - like YouTube for your local file system.

- https://github.com/caorushizi/oss-client /202401/ts
  - 七牛云文件仿百度网盘文件夹管理，上传下载，删除。

- https://github.com/msihly/Media-Viewer /202402/ts
  - Electron app for managing media files in a self-contained portable database. 
  - 依赖dnd-kit、mui.v5、@tensorflow/tfjs、trpc、mobx-react-lite、mongoose、mongodb-memory-server、react-window
  - Features a hierarchical tagging system with comprehensive search and sorting, automated tag creation / parsing and batch processes, collections / albums, AI face recognition, Stable Diffusion integration, and built-in media viewers.
  - A self-hosted, portable Electron app for indexing and viewing media files featuring hierarchical tags as well as several features inspired by cloud storage providers that are missing from Windows File Explorer and most contemporary alternatives. 
  - It has been refined over several iterations with the primary goal of optimizing performance at scale and the UX of batch workflows.

- https://github.com/sindresorhus/electron-serve /MIT/202401/js
  - Static file serving for Electron apps

- https://github.com/Michael-Vanderford/electron-file-manager /GPLv3/202401/js
  - Linux File Manager - Built with Electron
  - Audio or Video to Audio conversion - Requires ffmpeg
  - [How to transport to Winodws platform?_202312](https://github.com/Michael-Vanderford/electron-file-manager/issues/4)
    - Sorry, There a currently no plans to support the Windows platform.
  - https://github.com/Michael-Vanderford/string-file-manager
# notes
- https://github.com/husseinhareb/Coffee /202401/js
  - Text editor with file management and terminal integration using Electron.
# storage
- https://github.com/sindresorhus/electron-store /MIT/202305/js
  - Simple data persistence for your Electron app or module
  - Save and load user preferences, app state, cache, etc
  - Electron doesn't have a built-in way to persist user settings and other data. This module handles that for you
  - The data is saved in a JSON file named config.json in `app.getPath('userData')`.
  - You can use this module directly in both the main and renderer process

- https://github.com/alexiusacademia/electron-db /MIT/202011/js/inactive
  - Electron module that acts as database management and uses flat file database (json file) to store tables.
  - Flat file database solution for electron and other Nodejs apps.
  - The json file is saved on the application folder or you can specify the location for the database to be created
# utils
- https://github.com/nativefier/nativefier /MIT/202309/ts/archived
  - a command-line tool to easily create a “desktop app” for any web site with minimal fuss. 
  - Apps are wrapped by Electron
  - [Nativefier is unmaintained _202309](https://github.com/nativefier/nativefier/issues/1577)
    - Nativefier was built a couple of years ago before the ability to create shortcuts for websites in Chrome, or similarly on Firefox. 
    - Users who want to build and use their own website wrappers should strongly prefer these options as they are protected from security vulnerabilities by the browser's self updating mechanism.

- https://github.com/sindresorhus/electron-dl /MIT/202310/js
  - Simplified file downloads for your Electron app
  - Support for `BrowserWindow` and `BrowserView`.

- https://github.com/spaceagetv/electron-file-download /MIT/202308/ts
  - A simple module to download files via Electron's main process. 
  - Manages the download process and exposes a simple API to listen for events including progress, success, failure, and cancellation. 
  - The module also exposes Electron's DownloadItem methods for pausing, resuming, and canceling the download.

- https://github.com/daltonmenezes/interprocess /MIT/202308/ts
  - https://daltonmenezes.github.io/interprocess/
  - A scalable and type-safe Electron IPC management tool with enhanced DX
  - Electron IPC is good, but difficult to maintain and scale, either because of the numerous channels you have to remember, or because of the inconsistent API between processes and the absence of inferred types of your channels and handlers.
  - invoke and handle methods in both processes with the same expected behavior

- https://github.com/sindresorhus/electron-util /MIT/202401/ts
  - Useful utilities for Electron apps and modules
  - There are three parts of this package, “shared”, “main”, and “node”. The “shared” part works in both the main or rendered process. The “main” part works only in the main process. The “node” part is for Node.js-only APIs (not Electron).
  - To use features from the “main” part in the renderer process, you will need to set up IPC channels.

- https://github.com/alex8088/electron-toolkit /MIT/202401/ts
  - Toolkit for Electron

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

## utils-messaging

- https://github.com/linonetwo/electron-ipc-cat /MIT/202307/ts
  - Passing object and type between Electron main process and renderer process simply via preload script.
  - In latest electron, the remote module is deprecated, and you are required to passing data using IPC. 
  - Based on frankwallis/electron-ipc-proxy, and used in TiddlyGit-Desktop.
    - electron-ipc-proxy doesn't work well when we have `contextIsolation: true`, so here we have electron-ipc-cat
  - Only plain objects can be passed between the 2 sides of the proxy, as the data is serialized to JSON, so no functions or prototypes will make it across to the other side.
  - https://github.com/frankwallis/electron-ipc-proxy /MIT/202010/ts
    - Transparent asynchronous electron remoting using IPC.
# pattern/architecture
- https://github.com/ccorcos/electron-architecture /4Star/CC0-1/202108/ts/inactive
  - This project is a boilerplate electron app with a thoughtfully designed architecture
  - Main and renderer processes manage state using a Redux-like state machine.
  - Electron BrowserWindows are controlled declaratively through the application state.
  - Electron IPC uses a Proxy enabling "Rename Symbol" and "Find All References" in VSCode.
  - https://github.com/ccorcos/electron-boilerplate /202012/ts
    - uses TypeScript and demonstrates using a preload script to interact with the native APIs.

- https://github.com/HopefulHeart2020/electron-typescript-react-clean-architecture /202309/ts
  - Boilerplate for projects using Eletron, React and Typescript applying Clean Architecture together with Atomic Design.

- https://github.com/dutchigor/pluggable-electron /MIT/202210/js/inactive
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


- https://github.com/reZach/secure-electron-template /MIT/202404/js
  - A current electron app template with the most popular frameworks, designed and built with security in mind

- https://github.com/ArcherGu/einf /MIT/202502/ts
  - Einf is a simple electron main process framework, which provides some decorators and automatic dependency injection to help you simplify the main process code.
  - Support dependency injection powered by Typescript decorators.

- https://github.com/web-infra-dev/electron-sprout /MIT/202210/ts/inactive/modernjs
  - A front-end friendly desktop framework based on Electron.
  - electron-runtime: modified from vscode.
  - Unbundled Dev Server: The server implementation is based on the idea and structure of vite and wmr, and is adapted to the Modern.js application.

- https://github.com/dromara/electron-egg /apache2/202502/js
  - A simple, cross platform, enterprise desktop software development framework
  - Architecture: Single - business process / modular / multi - task (process, thread, rendering process), which simplifies the development of large - scale projects.
  - Independent front - end: Theoretically supports any front - end technology, such as Vue, React, HTML, etc.
  - https://github.com/wallace5303/ee-core /ISC/202502/js
    - Powerful electron third party module, offering 100+ API
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
