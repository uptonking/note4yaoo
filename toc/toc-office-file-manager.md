---
title: toc-office-file-manager
tags: [file, file-manager, filesystem, toc]
created: 2021-08-23T05:24:09.775Z
modified: 2021-08-23T05:27:08.068Z
---

# toc-office-file-manager

# guide
- 文件管理器的url路径设计
  - github示例 支持多个branch、tag
    - note4yaoo/blob/main/attachment/tech/node架构图.png
    - url支持完整文件名，包括中文
  - dropbox示例
    - /home/Blockstack%20Branding/BlockstackFile
    - url与文件名和存放路径相对应，支持中文路径
  - 百度网盘示例 路径包含在querystring中
    - /index?category=all&path=%2Fopt%2F系统相关
    - 路径中的特殊字符使用了url编码，如%2F表示斜杠/
  - google-drive示例  内层文件夹url扁平化
    - /folders/uuid-folder?resourcekey=uuid-key
    - 所有文件夹，不管嵌套层级，支持直接通过唯一id访问，url都是随机数字
  - onedrive示例  内层文件夹url扁平化
    - /?id=uuid-folder&cid=AE0F511DC7381EDB
# react-file
- react-sortable-tree /MIT/3.3kStar/202005
  - https://github.com/frontend-collective/react-sortable-tree
  - https://frontend-collective.github.io/react-sortable-tree/
  - https://github.com/frontend-collective/react-sortable-tree-theme-file-explorer
  - 依赖 react-virtualized, react-dnd, react-dnd-html5-backend
  - Drag-and-drop sortable component for nested data and hierarchies

- https://github.com/wx-chevalier/web-file-manager
  - 基于 React & TS 的文件管理器
  - 依赖react-beautiful-dnd、styled-components、formik

- https://github.com/codefreak/react-file-manager
  - 依赖react-dnd
  - react-file-manager contains some generic code for D&D and selection handling. You will need some additional code to make it render something.
  - antd-file-manager contains an implementation based on AntD's `<Table/>` component

- https://github.com/uptick/react-keyed-file-browser
  - https://uptick.github.io/react-keyed-file-browser/
  - 依赖 react-dnd、date-fns
  - Folder based file browser given a flat keyed list of objects

- https://github.com/TimboKZ/Chonky
  - https://chonky.io/
  - A File Browser component for React.
  - 依赖react-window、react-dnd、styled-components、material-ui.v4、react-jss、reduxjs/toolkit

- https://github.com/reactfilemanager/core
  - https://github.com/reactfilemanager/php-server
# file-manager-web
- https://github.com/MrWangJustToDo/file-manager
  - 依赖redux-thunk、sqlite3、jquery、codemirror、echarts
  - 个人网盘，支持用户的登录、注册，文件/文件夹的新建、删除，文件的上传、下载、编辑、提交、预览、重命名、复制、回收、搜索
  - 上传后文件保存为服务器本地文件，而不是数据库中，所以搜索不方便
  - https://github.com/MrWangJustToDo/requestModule
    - 可能是后端的简单测试

- https://github.com/GamEditor/Node.js-FileManager
  - This is a simple file manager for download and upload files on the server by categories.

- https://github.com/rocketseat-content/youtube-clone-dropbox-menu
  - https://github.com/maykbrito/vanilla-ui-clone-dropbox-home
  - 模仿dropbox的首页，简洁大方
  - https://cranky-einstein-aff725.netlify.app/

- https://github.com/emkis/dropbox-clone /202011/js
  - an easy way to store, share and access files from anywhere
  - 依赖后端

- https://github.com/tompdriscoll/DroppyBoy
  - https://droppyboy.herokuapp.com/#/
  - A Dropbox clone
  - 后端：nodejs+PostgreSQL
  - 前端：react+redux
  - 实现了登录认证、上传文件到aws s3

- https://github.com/dhruska/node-dropbox
  - a simple Dropbox clone built in Node.js.

- https://github.com/leoronne/dropbox-homepage-ui-clone
  - https://dropbox.ui-clone.ronne.dev/
  - 首页放了很多截图

- https://github.com/OpusCapita/filemanager
  - React based FileManager for browser ( + FS REST API for Node.js and Express)
  - supports connectors to different file storages like google drive, node server
  - 前端依赖react-virtualized、react-sortable-hoc、react-dnd

- https://github.com/kannifarhad/CronusFileManager
  - Filemanager with React & Nodejs
  - React, Redux, Material UI, Nodejs, ExpressJs
  - 提供了前端和后端实现

- https://github.com/psolom/RichFilemanager  /archived
  - http://fm.devale.pro/
  - Rich Filemanager is an open-source file manager
  - Filemanager is designed to interact with a number of programming languages via connectors. 
  - The actual connectors are: PHP, Java, ASHX, ASP, NodeJs & Python 3 Flask.

- https://github.com/joni2back/react-filemanager
  - https://joni2back.github.io/react-filemanager/
  - 依赖redux、material-ui.v4
  - Hello ex angular-filemanager user, this is the new version in React and Redux with backends for Local Files and FTP.
  - https://github.com/joni2back/filemanager-connector-node
    - a local file connector API in NodeJS

- https://github.com/dailykit/react-file-manager
  - A file manager built in ReactJs
  - 依赖apollo

- https://github.com/datahuborg/datahub /archived
  - https://datahub.csail.mit.edu/
  - experimental hosted platform (GitHub-like) for organizing, managing, sharing, collaborating, and making sense of data.

- https://github.com/magentaLi/CloudDrive
  - 基于javaweb的仿照百度网盘做的小型云盘系统

- https://github.com/mickael-kerjean/filestash
  - A Dropbox-like file manager that let you manage your data anywhere it is located: FTP • FTPS • SFTP • WebDAV • Git • S3 • LDAP • Mysql CardDAV • CalDAV • Backblaze B2 • Minio Dropbox • Google Drive
# git-file-tree
- https://github.com/ovity/octotree
  - 旧版v3依赖jquery、jstree
  - Octotree is a proprietary software. 
  - This repository contains the old source code of a very limited version of Octotree.

- https://github.com/EnixCoda/Gitako
  - 依赖 nprogress、react-window
  - File tree extension for GitHub on Chrome & Firefox & Edge

- https://github.com/brumm/tako
  - 依赖react-query、styled-components、rehype-dom-parse、zustand
  - Tako replaces the default Github repository file list with an expandable file tree and file preview
- https://github.com/ineo6/git-master
  - 依赖jquery、jquery-ui、jstree
  - Git file tree (GitHub && GitLab && Gitee && Gitea && Gogs)
  - Show GitHub repo size and file download support
- https://github.com/FrankFan/gitlab-tree
  - 依赖jquery、jstree
  - Chrome extension to display Gitlab code in tree format.
- https://github.com/jawil/GayHub
  - 依赖monaco-editor、pjax、wolfy-eventemitter
  - 文件目录树、toc

- https://github.com/kaushiknishchay/better-git-viewer
  - http://nkaushik.in/better-git-viewer/
  - react based git repo viewer with file tree for better navigation.
  - 依赖 isomorphic-git、@isomorphic-git/lightning-fs、material-ui

- https://github.com/jpwilliams/gitree
  - Print a directory tree that shows Git status and ignores files dictated by .gitignore.
  - 命令行工具
# file-electron
- https://github.com/warpdesign/react-explorer
  - File manager written in TypeScript, React, Blueprint and packaged with Electron
  - Split-view window
  - Plugin-based: local supported for now, ftp in the works

- https://github.com/Cocycles/electron-storage /201703
  - Simply save/load json files to/from file system in electron applications
- https://github.com/yan-foto/electron-reload /201908
  - the simplest way to load contents of all active BrowserWindows within electron when the source files are changed.
- https://github.com/sindresorhus/electron-serve
  - Static file serving for Electron apps

- https://github.com/vasylhoban/electron-file-manager
  - File manager created on Electron/React/Redux (Windows, in future cross-browser)
- https://github.com/warpdesign/react-explorer /202011
  - File manager written in TypeScript, React, Blueprint and packaged with Electron
- https://github.com/matthew-matvei/freeman /201903
  - extensible, cross-platform file manager for power users
- https://github.com/k-water/electron-filesystem /201807/vue
  - 基于vue-electron的文件管理器
- https://github.com/hawkeye64/electron-quasar-file-explorer /202010
  - A Simple File Explorer using Vue/Quasar/Electron
- https://github.com/timotius02/electron-file-explorer /201506
  - File Explorer built using Electron, React, and Flux
- https://github.com/mperitz/react-filetree-electron /201707
  - A react component that renders an expandable/collapsible filetree in an electron app
- https://github.com/mflorence99/el-file /201907
  - Electron-based File Manager
- https://github.com/marceloaugusto80/electron-react-typescript-boilerplate /202010
  - Boilerplate for electron + file system + react + react-hot-loader + typescript
- https://github.com/vasylhoban/electron-file-manager /201802
  - File manager created on Electron/React/Redux
- https://github.com/pmuellr/AnyViewer /201609
  - desktop file viewer built on Electron

 

- https://github.com/gerhardberger/electron-pdf-window /201709
  - view PDF files in electron browser windows
- https://github.com/fraserxu/electron-pdf /202010
  - A command line tool to generate PDF from URL, HTML or Markdown files with electron.
- https://github.com/artiebits/pdf-to-printer /202101
  - Print PDF files from Node.js and Electron.
- https://github.com/btargac/excel-parser-processor /202012
  - It can download files from URL(s) in a column of Excel files. 
  - If a new filename is provided at column B it will rename the file before saving. 

- https://github.com/steventhanna/proton /201706
  - quickly preview and edit Markdown files using Electron.
- https://github.com/jersou/markdown-explorer /202009
  - view and edit markdown documentation of a file tree
- https://github.com/danobot/notorious /202012/GPLv3/31Star
  - Offline-first note taking and knowledge management application 
- https://github.com/Merlin04/multipad
  - Notepad for the future - a swiss army knife file editor/viewer.
# filesystem-utils
- https://github.com/use-strict/file-system-access
  - File System Access API implementation (ponyfill) with pluggable storage adapters via IndexedDB, Cache API, in-memory etc.

- https://github.com/libfuse/libfuse
  - The reference implementation of the Linux FUSE (Filesystem in Userspace) interface
- https://github.com/presslabs/gitfs
  - gitfs is a FUSE file system that fully integrates with git. 
  - You can mount a remote repository's branch locally, and any subsequent changes made to the files will be automatically committed to the remote.
  - 但vscode不是直接集成git了吗
# opfs/Origin Private File System
- [chromium sqlite3-api-opfs.js](https://www.blick-newwsch.com/?_=%2Fexternal%2Fgithub.com%2Fsqlite%2Fsqlite%2F%2B%2Frefs%2Fheads%2Fopfs-lock-without-xlock%2Fext%2Fwasm%2Fapi%2Fsqlite3-api-opfs.js%23Zn%2F56Y4trIg2C2EYQD%2F9g5ZYfX%2BnMC3zulsbohqB0K9j)
  - This file holds the synchronous half of an sqlite3_vfs
  implementation which proxies, in a synchronous fashion, the
  asynchronous Origin-Private FileSystem (OPFS) APIs using a second
  Worker, implemented in sqlite3-opfs-async-proxy.js.

- https://github.com/wariasar/opfs
  - https://v22018096896673253.goodsrv.de/opfs/
  - This is just a test for the OPFS feature in Webbrowsers. 

- https://github.com/kevin-daniel-hunt/opfs-sqlite-poc
  - This small project will setup a frontend and backend environment for serving mock data through a websocket from an express server to a webworker on the frontend (React + Vite) which will store the data using sqlite.wasm and OPFS.

- https://github.com/nmeibergen/bare-sqlite-opfs
  - This is a bare minimum package to run Sqlite with OPFS in a worker.

- https://github.com/jvilk/BrowserFS /202001/ts
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
  - 支持 memory/localStorage/indexeddb/dropbox/Emscripten file systems
  - [File System Access Backend by DustinBrett](https://github.com/jvilk/BrowserFS/pull/321)
    - I won't be using it by default in my project with OPFS instead of IndexedDb because it has other limits such as not allowing the making of `.url` files. 
    - I also wrote a benchmark and found it interesting that OPFS was not faster. But maybe this could be improved in the code I wrote

- https://github.com/tomayac/opfs-explorer
  - OPFS Explorer is a Chrome DevTools extension that allows you to explore the Origin Private File System (OPFS) of a web application.

- https://github.com/qwtel/sqlite-viewer-vscode  /ts
  - https://sqliteviewer.app/
  - easy SQLite viewer for VSCode, inspired by DB Browser for SQLite and Airtable.
  - [Next version of SQLite Viewer, handling 3 million rows, 1 GB sqlite file, in a browser.](https://twitter.com/qwtel/status/1639204056622321664)
    - Memory usage low despite 1GB file, thanks to OPFS and SQLite WASM
  - [Opening large SQLite files is solved in the (unreleased) web version though.](https://twitter.com/qwtel/status/1644319722178248708)
    - The limit is now how much the browser permits to write into the Origin Private File System.
  - I'm surprised the current version of SQLite Viewer keeps getting good reviews in the vsc marketplace. It flat out crashes if you open a large file. I suppose most sqlite files are small.
    - Unfortunately fixing it would be hard. 
    - vsc's own `fs` module doesn't let you read with random offsets, and even if it did, it would require writing a custom VFS and juggling buffers across 2-3 layers of iframes and workers.

- https://github.com/ncisrc/opfs /js
  - A class based connector to the browser Origin Private File System API
# web-storage
- https://github.com/ncisrc/cookies-storage
  - It's like localStorage or sessionStorage but with cookies.
# more-files-manager
- https://github.com/imshubhamsingh/file-system-react
  - 依赖redux、styled-components、formik
  - File System UI in Web using react
  - 样式友好，但功能简单；没有提供列表视图，只有平铺视图

- https://github.com/xlzy520/nestdisk-be
  - https://github.com/xlzy520/netdisk
  - 网盘项目后端，Koa、mysql，功能：登录注册，加密，hash计算，文件分享，用户、文件管理。
  - 网盘前端基于vue2、vuex、element-ui
- more-基于node实现的网盘
  - https://github.com/nijiayu0914/file_exchange_frontend
  

- https://github.com/huangshaomo/nodejs-express-mysql-bootstrap
  - 一个基于NodeJS Express Bootstrap Mysql 个人博客系统，
  - 前台包括文章展示，登录注册，评论、网盘系统等。
  - 后台包括用户，登录，角色，系统管理等
- https://github.com/270520006/zspdisk
  - 仿百度网盘的一个项目，用到了layui+ssm+shiro
- https://github.com/KingJin-web/kingcloud
  - 基于Hadoop的网盘，spring-boot-data-jpa+vue+layui
- more-基于java-spring实现的网盘
  - https://github.com/DongyangHu/smile-disk
  - https://github.com/asusAaron/XDrive
  - https://github.com/zayvion/Floda-Drive
  - https://github.com/Antony998/cloud
  - https://github.com/heart14/heart-cloud
  - https://github.com/WEIQ311/code-pan

- https://github.com/Studio-42/elFinder
  - 样式陈旧但经典
  - file manager for web, written in JavaScript using jQuery and jQuery UI

- https://github.com/caorushizi/oss-client
  - 七牛云文件仿百度网盘文件夹管理，上传下载，删除。七牛云存储，七牛云图床。桌面应用程序 windows mac
- https://github.com/chenhb23/lanzouyun-disk
  - 蓝奏云网盘、客户端，界面美观。支持登录、大文件批量断点上传 / 下载、URL 解析，使用 electron 构建
