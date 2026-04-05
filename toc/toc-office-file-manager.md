---
title: toc-office-file-manager
tags: [file, file-manager, filesystem, toc]
created: 2021-08-23T05:24:09.775Z
modified: 2021-08-23T05:27:08.068Z
---

# toc-office-file-manager

# guide

- tips
  - 不要执着于独立的的file组件，在成熟产品如vscode/clouddrive/strapi/CMS/paperless/obsidian中都存在文件管理实现可参考
    - 更适合参考网盘类产品的文件管理逻辑，因为会处理大量文件的场景
    - 可参考filebrowser/nextcloud等产品的desktop实现
    - 还可参考云厂商的实现，如s3/r2
  - 数据源支持local/remote/s3需要可扩展的后端架构，重点参考
  - vscode也提供了local/remote文件管理的思路
  - 不要执着于web/pc多个gui，webview/wrapper封装技术很成熟

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
# file-ui
- https://github.com/jpmorganchase/jupyter-fs /238Star/apache2/202601/python/ts
  - A plugin for JupyterLab that lets you set up and use as many filebrowsers as you like, connected to whatever local and/or remote filesystem-like resources you want.
  - The backend is built on top of `PyFilesystem` and `fsspec`, while the frontend is built on top of `tree-finder`.
  - PyFilesystem
    - osfs: os filesystem. The will open a new view of your local filesystem, with the specified root
    - s3: opens a filesystem pointing to an Amazon S3 bucket
    - smb: opens a filesystem pointing to a Samba share
    - jupyter-fs can open a filebrowser pointing to any of the diverse resources supported by PyFilesystem. Currently, we test only test the S3 and smb/samba backends as part of our CI
  - https://github.com/tree-finder/tree-finder /BSD/202512/ts
    - Versatile tree-viewer/filebrowser widget, built on top of regular-table

- react-sortable-tree /MIT/3.3kStar/202005
  - https://github.com/frontend-collective/react-sortable-tree
  - https://frontend-collective.github.io/react-sortable-tree/
  - https://github.com/frontend-collective/react-sortable-tree-theme-file-explorer
  - 依赖 react-virtualized, react-dnd, react-dnd-html5-backend
  - Drag-and-drop sortable component for nested data and hierarchies

- https://github.com/ln-dev7/square-ui/tree/master/templates-baseui/files /MIT/202601/ts/依赖少
  - https://square-ui-files.vercel.app/
  - Modern file manager with folders, storage overview, file grid/list view, and navigation.
  - 依赖zustand、nextjs、base-ui
  - 删除文件、上传文件未实现

- https://github.com/wx-chevalier/web-file-manager
  - 基于 React & TS 的文件管理器
  - 依赖react-beautiful-dnd、styled-components、formik

- https://github.com/codefreak/react-file-manager
  - 依赖react-dnd
  - react-file-manager contains some generic code for D&D and selection handling. You will need some additional code to make it render something.
  - antd-file-manager contains an implementation based on AntD's `<Table/>` component

- https://github.com/uptick/react-keyed-file-browser /MIT/202305/js/inactive
  - https://uptick.github.io/react-keyed-file-browser/
  - Folder based file browser given a flat keyed list of objects, powered by React.
  - 依赖 react-dnd、date-fns

- https://github.com/TimboKZ/Chonky
  - https://chonky.io/
  - A File Browser component for React.
  - 依赖react-window、react-dnd、styled-components、material-ui.v4、react-jss、reduxjs/toolkit

- https://github.com/svar-widgets/filemanager /MIT/202512/ts/svelte
  - https://svar.dev/svelte/filemanager/
  - Easy-to-use Svelte file manager (file explorer) component
  - Integrate it with any backend, whether you're using local storage, databases, or cloud services.
  - Split view to manage files between different locations

- https://github.com/concord-consortium/cloud-file-manager /MIT/202601/ts
  - The Cloud File Manager is a Javascript library that enables applications to save and load files from various file systems using a simple consistent API.
  - 示例偏向单文件的api操作，无文件管理示例
  - [the following file system providers are supported:](https://github.com/concord-consortium/cloud-file-manager/blob/master/doc/providers.md)
    - Local and remote read-only files
    - Google Drive
    - Browser LocalStorage (used mostly for development/testing)
    - s3-provider
# file-manager-fullstack
- https://github.com/MrWangJustToDo/file-manager
  - 依赖redux-thunk、sqlite3、jquery、codemirror、echarts
  - 个人网盘，支持用户的登录、注册，文件/文件夹的新建、删除，文件的上传、下载、编辑、提交、预览、重命名、复制、回收、搜索
  - 上传后文件保存为服务器本地文件，而不是数据库中，所以搜索不方便
  - https://github.com/MrWangJustToDo/requestModule
    - 可能是后端的简单测试
  - https://github.com/serverwentdown/file-manager /js/inactive
    - A basic node.js file manager

- https://github.com/zeitmaschinen/GalleryFlow /33Star/MIT/202510/python/ts/inactive
  - A modern web application for browsing and managing ComfyUI-generated images with advanced metadata support.
  - Workflow visualization for each image and copy JSON to clipboard
  - Recursively reads all folders, so you never miss an image
  - WebSocket support for real-time updates
  - Direct integration with ComfyUI workflows
  - Frontend: React 18, TypeScript, Material UI
  - Backend: FastAPI, SQLAlchemy, Python 3.10+
  - Other: WebSockets, React Flow, custom theming, responsive design

- https://github.com/kannifarhad/CronusFileManager /MIT/202510/ts/inactive
  - Filemanager with React & Nodejs
  - React, Redux, Material UI, Nodejs, ExpressJs
  - 提供了前端和后端实现
  - virtual scroll loading to address performance issues when dealing with large folders containing more than 500 files.
  - Zip/unzip
  - Fully Image editor - Integrated TOAST UI Image Editor

- https://github.com/xiaobaidadada/filecat /77Star/apache2/202601/ts
  - 一个基于 Web 的文件服务器、服务器管理工具。集成了文件管理、超大日志查看、远程终端访问、系统进程监控，以及包括 VPN、SSH、RDP、HTTP、TCP 等多种网络代理功能。支持windows、linux、mac。
  - 本项目是对filebrowser的功能增强，使用和filebrowser一样的ui，以服务器文件管理为基础添加一些服务器控制功能
  - 文件管理: 支持断点分块上传、多个根目录、代码\图片编辑、编辑器模式、白板绘图...
  - 终端：相比filebrowser使用了xterm.js，并且采用了虚拟shell完美实现命令的权限过滤，避免用户执行类似 rm -r / 的危险命令
  - CI/CD自动化构建：内置了一个模仿github workflow 语法实现的自动化构建功能，作用于以.act结尾的文件
  - ssh代理: 可以管理多个linux服务器，作用和winscp类似，让终端和文件管理更方便。除此之外还支持http代理，rdp远程桌面(windows)等代理
  - [FileCat-Docs-技术介绍](https://filecat.xiaobaidadada.fun/#/zh-CN/%E6%8A%80%E6%9C%AF/%E6%8A%80%E6%9C%AF%E4%BB%8B%E7%BB%8D.md)
    - 前端采用react框架，样式采用filebrowser的，前端样式基本是复制的filebrowser的。全局状态管理使用了 recoil
    - 后端工作量有点小大的几个功能是，虚拟网络vpn，workflow自动化构建，虚拟终端 pty-shell ，大日志文件日志，这些功能都是本项目自己原创设计实现的，还有个rdp 原创桌面控制，是采用了其它项目的源码， 我给直接复制过来改了一下，node.js 的rdp代理好像目前只有MeshCentral实现了可以远程访问的。

- https://github.com/dhanyn10/multiple-file-manager /202510/ts/inactive
  - A desktop application built with Electron, Vite, React, and TypeScript, designed to simplify bulk file operations. 
  - This application provides an intuitive interface to rename, delete, and manage multiple files at once based on various patterns and criteria.
  - 似乎没有文件树，需要在url直接输入路径，只适合用来批量操作

- https://github.com/OpusCapita/filemanager /567Star/apache2/202310/java/js/inactive
  - React based FileManager for browser ( + FS REST API for Node.js and Express)
  - supports connectors to different file storages like google drive, node server
  - 前端依赖react-virtualized、react-sortable-hoc、react-dnd

- https://github.com/joni2back/react-filemanager /201901/js/inactive
  - https://joni2back.github.io/react-filemanager/
  - 依赖redux、material-ui.v4
  - Hello ex angular-filemanager user, this is the new version in React and Redux with backends for Local Files and FTP.
  - https://github.com/joni2back/filemanager-connector-node
    - a local file connector API in NodeJS

- https://github.com/GamEditor/Node.js-FileManager
  - This is a simple file manager for download and upload files on the server by categories.

- https://github.com/maykbrito/vanilla-ui-clone-dropbox-home /202008/js
  - https://github.com/rocketseat-content/youtube-clone-dropbox-menu
  - https://cranky-einstein-aff725.netlify.app/
  - 模仿dropbox的首页，简洁大方

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

- https://github.com/psolom/RichFilemanager  /archived
  - http://fm.devale.pro/
  - Rich Filemanager is an open-source file manager
  - Filemanager is designed to interact with a number of programming languages via connectors. 
  - The actual connectors are: PHP, Java, ASHX, ASP, NodeJs & Python 3 Flask.

- https://github.com/dailykit/react-file-manager
  - A file manager built in ReactJs
  - 依赖apollo

- https://github.com/datahuborg/datahub /archived
  - https://datahub.csail.mit.edu/
  - experimental hosted platform (GitHub-like) for organizing, managing, sharing, collaborating, and making sense of data.

- https://github.com/magentaLi/CloudDrive
  - 基于javaweb的仿照百度网盘做的小型云盘系统

- https://github.com/mickael-kerjean/filestash /AGPLv3/202408/go/js
  - https://www.filestash.app/
  - A Dropbox-like file manager that let you manage your data anywhere it is located: FTP • FTPS • SFTP • WebDAV • Git • S3 • LDAP • Mysql CardDAV • CalDAV • Backblaze B2 • Minio Dropbox • Google Drive
  - Multiple cloud providers and protocols, easily extensible

- https://github.com/reactfilemanager/core
  - https://github.com/reactfilemanager/php-server
# file-pc/electron/tauri
- https://github.com/Saifullah-dev/react-file-manager /134Star/MIT/202601/python/js/依赖少/仅web
  - React.js package for seamless file manager integration, offering a user-friendly interface for viewing, uploading, and deleting files with full UI and backend support.
  - It provides a user-friendly interface for managing files and folders, including viewing, uploading, and deleting, with full UI and backend integration.
  - Navigation: Use the breadcrumb trail and sidebar navigation pane for quick directory traversal.
  - Toolbar & Context Menu
  - Drag-and-Drop: Move selected files and folders by dragging them to the desired directory
  - 后端依赖express、mongoose
  - 前端依赖react-collapsed
  - The `backend/fastapi_backend.py` is an alternative backend implementation using Python/FastAPI instead of Node.js/Express. It provides the same file management functionality but:
    - 💡 可参考来替换数据源
    - Uses the local filesystem directly (no MongoDB required)
    - os.walk() filesystem scan: Slower for large directories, No metadata persistence
    - Harder to add features

- https://github.com/warpdesign/react-explorer /279Star/MIT/202506/ts/inactive
  - File manager written in TypeScript, React, Blueprint and packaged with Electron
  - Split-view window
  - Media File Preview
  - WSL integration (Windows)
  - React-Explorer is fully localized using .json files. Right now, English and French are available.
  - React-Explorer has been written so that it can easily be extended using plugins
  - 🔌 Plugin-based filesystem support
    - ~~Plugin-based: local supported for now, ftp in the works~~ 
    - React-Explorer has been written so that it can easily be extended using plugins. As a starting point you may use the `FsGeneric` skeleton.
    - 🛢️ it's highly feasible to create an S3/MinIO plugin
    - Clean `FsApi` interface with ~20 methods to implement
    - Stream-based operations align perfectly with S3 SDK capabilities
  - 依赖blueprintjs、electron-window-state、mobx-react、react-dnd、react-virtual
  - 🧭 this file manager does support running in a browser with a web UI, but with important limitations. It's designed primarily for E2E testing, not production use.
    - The codebase includes a web build configuration that stubs Electron APIs and runs in the browser. However:
    - Uses in-memory filesystem (memfs) - no real file operations
    - Electron APIs are mocked/stubbed
    - Specifically built for Cypress testing
  - it does not support web UI.
    - Uses Node.js fs module directly for all file operations
    - Has file operations running in the renderer process with `nodeIntegration: true`.
    - Has no web backend or HTTP API layer
    - Plugin architecture already exists - can add new `FsWeb` plugin
    - All file operations must be reimplemented as HTTP APIs. Need to build entire backend server from scratch
    - Real-time file watching needs WebSocket implementation
  - 📡 roadmap
    - migrate mobx to tanstack-store

- https://github.com/Scriptol/Advanced-Explorer /CC/202512/js
  - https://www.scriptol.com/scripts/advanced-explorer.php
  - A file manager and text editor built in JavaScript and HTML 5, Ace editor and Node.js library. Requires Electron for the rendering engine.
  - From Java to JavaScript: This is actually the successor of the Advanced Explorer file management software I have written in Java in 1999. This version written entirely in JavaScript in 2012 keeps the essential features of the Java program and includes a more advanced text editor based on ACE for the backend, with a custom interface.

- https://github.com/brettz9/filebrowser-electron /MIT/202512/js
  - This aims to be a cross-platform and enhanced substitute for the desktop file browser.
  - ONLY VERY MINIMALLY FUNCTIONAL
  - Undo/Redo: Maintains up to 50 operations in the undo history
  - Sticky Notes

- https://github.com/27px/Remote-File-Manager /MIT/202110/ts/inactive
  - GUI File Manager, access both local and ssh files, X-OS (Built on electron), Tested for Windows and Ubuntu
  - 支持web/pc
  - [I developed a File Manager (Local and SSH) using Node.js, Electron.js, Angular (No Bootstrap / jQuery / templates are used, It is custom CSS) Packed as Desktop application using Electron.js _202107](https://www.reddit.com/r/node/comments/okqdrh/hi_i_developed_a_file_manager_local_and_ssh_using/)

- https://github.com/Cocycles/electron-storage /201703/js/inactive
  - Simply save/load json files to/from file system in electron applications
- https://github.com/yan-foto/electron-reload /201908
  - the simplest way to load contents of all active BrowserWindows within electron when the source files are changed.

- https://github.com/vasylhoban/electron-file-manager
  - File manager created on Electron/React/Redux (Windows, in future cross-browser)
- https://github.com/matthew-matvei/freeman /GPLv3/201903/archived
  - extensible, cross-platform file manager for power users
- https://github.com/k-water/electron-filesystem /201807/vue
  - 基于vue-electron的文件管理器
- https://github.com/hawkeye64/electron-quasar-file-explorer /202010
  - A Simple File Explorer using Vue/Quasar/Electron
- https://github.com/timotius02/electron-file-explorer /201506
  - File Explorer built using Electron, React, and Flux
- https://github.com/mperitz/react-filetree-electron /201707/js
  - A react component that renders an expandable/collapsible filetree in an electron app
- https://github.com/mflorence99/el-file /201907/ts/inactive
  - Electron-based File Manager
- https://github.com/marceloaugusto80/electron-react-typescript-boilerplate /202010
  - Boilerplate for electron + file system + react + react-hot-loader + typescript
- https://github.com/vasylhoban/electron-file-manager /201802
  - File manager created on Electron/React/Redux
- https://github.com/pmuellr/AnyViewer /201609
  - desktop file viewer built on Electron

 

- https://github.com/gerhardberger/electron-pdf-window /201709
  - view PDF files in electron browser windows
- https://github.com/fraserxu/electron-pdf /202010/js
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
- https://github.com/danobot/notorious /31Star/GPLv3/202102/inactive
  - Offline-first note taking and knowledge management application 
- https://github.com/Merlin04/multipad
  - Notepad for the future - a swiss army knife file editor/viewer.

## tauri

- https://github.com/kimlimjustin/xplorer /5.4kStar/apache2/202202/ts/rust/tauri/inactive
  - customizable, modern and cross-platform File Explorer.
  - a modern file explorer built from ground-up to be fully customizable to fit 2022's need. Besides, Xplorer is a cross-platform application powered by the web that is being wrapped using Tauri 
  - 不支持
    - Remote file (OneDrive, Google Drive, etc.)
    - Web application.

- https://github.com/jeanlyn/mpfm /MIT/202512/rust/ts/Tauri
  - A multi-protocol file storage manager client (S3/FTP/...) that support MacOS/Windows/Linux
  - cross-platform multi-protocol file manager based on Apache OpenDAL™, providing both command-line interface and graphical interface.
  - Multi-Protocol Support: Support for local filesystem, S3-compatible storage, FTP and other protocols
  - Complete File Operations: Support for file/directory listing, upload, download, delete, create, and more

- https://github.com/Coordinate-Cat/Flanker /GPLv3/202407/ts
  - New Age File Explorer
# git-file-tree
- https://github.com/ovity/octotree
  - 旧版v3依赖jquery、jstree
  - Octotree is a proprietary software. 
  - This repository contains the old source code of a very limited version of Octotree.

- https://github.com/EnixCoda/Gitako
  - 依赖 nprogress、react-window
  - File tree extension for GitHub on Chrome & Firefox & Edge

- https://github.com/brumm/tako /MIT/202306/js/inactive
  - 依赖react-query、styled-components、rehype-dom-parse、zustand
  - Tako replaces the default Github repository file list with an expandable file tree and file preview
  - Get it on the Chrome Webstore
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
# filesystem-utils
- https://github.com/flystorage/flystorage /202312/ts
  - a file storage abstraction for NodeJS and TypeScript
  - Provide an async/await based API, promises all the way.
  - Abstract over file permissions using "visibility".
  - It's a generalised solution and will not implement feature only specific to one particular storage implementation.
  - Implemented: local-file-system, AWS S3 (using the V3 SDK)

- https://github.com/use-strict/file-system-access
  - File System Access API implementation (ponyfill) with pluggable storage adapters via IndexedDB, Cache API, in-memory etc.

- https://github.com/libfuse/libfuse
  - The reference implementation of the Linux FUSE (Filesystem in Userspace) interface
- https://github.com/presslabs/gitfs /python
  - gitfs is a FUSE file system that fully integrates with git. 
  - You can mount a remote repository's branch locally, and any subsequent changes made to the files will be automatically committed to the remote.

- https://github.com/sxyazi/yazi
  - yazi，一个新的终端文件管理器，使用 Rust 开发，基于 async I/O
  - 目标是同时兼顾性能、功能，核心部分完全 Rust 实现，减少外部依赖以避免性能瓶颈和体验劣化。
  - 要不要看看 #OpenDAL，顺手支持一把更多存储服务？
    - OpenDAL 是一个 rust lib，提供了各种存储服务的访问能力。没有直接提供这些功能，不过本质上就是一堆 seek & read 操作，是可以实现的

- https://github.com/codecyou/FileManager /202308/python
  - 文件管理/文件去重/文件备份/文件同步/查找相似图片/查找相似视频/本地以图搜图/比对文本文件内容/拷贝目录结构/视频合并/视频裁剪/找出损坏的视频/提取音频/音频格式转换/批量重命名/搜索文件/文本编码转换/CRLF与LF转换
  - 所有操作都有日志，方便追溯和还原。涉及程序配置内容修改的操作会有权限验证。
  - 所有的文件删除、文件更新操作进行防呆保护，最大限度保证数据安全
# zip-files
- https://github.com/gildas-lormeau/zip-manager /MIT/202511/js/inactive
  - https://gildas-lormeau.github.io/zip-manager/
  - a PWA using the filesystem API in zip.js.
  - It is based on React and built with Vite.
# web-storage
- https://github.com/razaanstha/s3kit /202512/ts
  - https://s3kit.vercel.app/
  - A secure, server-driven, framework-agnostic S3 file manager with a React UI.
  - Plug‑and‑play package with FileManager UI for frontend for server‑side connection for S3 storage configuration with permissioned actions and picker/viewer/manager modes.
  - core: S3 operations (virtual folders, pagination, presigned uploads, previews)
  - adapters/*: framework adapters (Express, Next.js, Fetch/Remix)

- https://github.com/jamwt/convex-fs /apache2/202512/ts
  - Virtual filesystem for Convex, backed by Bunny.net Edge Storage & CDN
  - ConvexFS is a Convex component that provides filesystem-like operations for managing files in your Convex application.
  - Instead of dealing with raw blob storage, you work with familiar concepts like paths, files, and directories—while getting the performance benefits of a global CDN.
  - Path-based file management — Organize files with familiar filesystem paths
  - https://x.com/jamwt/status/2006151504823005471
    - i was also working on similar thing since a while but with fully s3 compliant mainly focussed for FE while handling the credentials with authorization from server. 

- https://github.com/ncisrc/cookies-storage
  - It's like localStorage or sessionStorage but with cookies.
# file-viewer
- https://github.com/box/box-content-preview /boxLic/202603/ts
  - https://developer.box.com/docs/box-content-preview
  - JavaScript library for rendering files stored on Box
  - allows developers to easily embed high quality and interactive previews of Box files in desktop and mobile web applications. 
  - Box Content Preview also allows previews of multiple files to be loaded in the same container and exposes arrows to navigate between those files.
  - This library powers Preview in the main Box web application as well as the 'Get Embed Link' Box API endpoint.
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

- https://github.com/spacedriveapp/spacedrive /36.5kStar/AGPLv3/202601/rust/ts
  - https://spacedrive.com/
  - an open source cross-platform file manager, powered by a virtual distributed filesystem (VDFS) written in Rust.
  - Prisma, Rust, React, TypeScript, Tauri
  - Tauri allows us to create a pure Rust native OS webview
  - We also use rspc which allows us to define functions in Rust and call them on the Typescript frontend
  - The core (sdcore) is written in pure Rust.
