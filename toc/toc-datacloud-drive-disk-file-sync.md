---
title: toc-datacloud-drive-disk-file-sync
tags: [cloud-drive, data, data-sync, synchronization, toc]
created: 2022-09-10T02:24:13.285Z
modified: 2022-09-10T02:26:52.062Z
---

# toc-datacloud-drive-disk-file-sync

# guide

- 需要同步的场景
  - app设置项，如vscode设置，pwa列表
  - app内容，如笔记内容
  - 浏览器标签页部分设置和布局，或扩展列表
  - 同步方式，对大数据或小数据都可以放在云盘，需要自己读取解析

- 云同步提供商
  - 网盘：百度OAuth2.0, 腾讯文档/微云，onedrive
  - 云服务商：七牛
  - 非主流存储：github仓库、gitee

- 其他云存储
  - 国外：dropbox clone

- free-cloud-database
  - PlanetScale: mysql
  - supabase: postgresql

- https://github.com/syncthing/syncthing
  - Syncthing is a continuous file synchronization program. 
  - It synchronizes files between two or more computers. 
# 国外云存储
- icloud 需付费成为apple-developer
  - [iOS独立开发-基于iCloud构建用户体系](https://zhuanlan.zhihu.com/p/392378738)

- firebase
# 国内云存储
- [七牛云开发者 免费额度](https://developer.qiniu.com/af/kb/1574/free-credit-information)
  - 对象存储
  - 标准存储免费空间	0-10 GB
  - 标准存储数据读取	无上限

- 百度网盘
  - [百度网盘开放平台 技术文档](https://pan.baidu.com/union/doc/mksg0s9l4)
- 百度API商城
  - https://apis.baidu.com/
  - 在百度云控制台API网关发布的API可以直接在百度API商城售卖，不过你得先作为服务商入驻——作为API的提供者，还是要有一定资质的，不然没法监管，平台承担不起这个风险。

- 腾讯文档
  - [腾讯文档开放平台](https://support.qq.com/products/331111)
  - 目前支持API接入和小程序接入
  - 腾讯文档面向开发者提供限时免费的 API 服务。在限免期间，开发者可以免费使用指定次数的 API 调用，只需轻量级开发即可接入腾讯核心能力。

- 微信小程序
  - 认证服务费300元，如果不需要使用微信支付等需要认证才能实现的功能，此项可以不认证
  - [微信小程序怎么收费](https://zhuanlan.zhihu.com/p/379636354)
    - 腾讯提供了展示前端，每年要300，需要自己开发维护

- 腾讯微云
  - [腾讯微云开放平台TWOA](https://open.weiyun.com/)
  - api
    - [RESTFUL API接口文档](https://open.weiyun.com/api/twoa_restful_api.html)
    - Android版本SDK
    - IOS平台SDK
    - Windows平台SDK

- [飞书文档api](https://open.feishu.cn/document/ukTMukTMukTM/uUDN04SN0QjL1QDN/docs-overview)
  - 云文档是飞书在线文档、电子表格、多维表格、知识库、云空间等产品的统称。你可以调用云文档的相关接口
  - 多维表格的数据容器，一个多维表格中至少有一个数据表，也可能有多个数据表。每个数据表都有唯一标识 table_id。
  - [飞书开放平台 应用商店 计费方式](https://open.feishu.cn/document/uMzNwEjLzcDMx4yM3ATM/ucDN3QjL3QzN04yN0cDN)

- 坚果云
  - 用于授权第三方应用利用 WebDAV 协议访问团队的文件
# cloud-drive-alternatives
- https://github.com/alist-org/alist
  - 一个支持多存储的文件列表程序，基于 go-Gin 和 Solidjs。
  - 支持 国内外主流网盘

- firefiles /133Star/GPLv3/202207/ts/inactive
  - https://github.com/faisalsayed10/firefiles
  - https://firefiles.vercel.app/
  - https://firefiles.vercel.app/docs/self-host
  - 后端可选firebase、aws-s3、mysql
  - 依赖chakra-ui、swr、prisma
  - Firefiles is an open‑source alternative to Dropbox which lets you setup a cloud drive with the backend of your choice 
  - A modern file-system interface for your storage buckets.
  - A MySQL database. (We recommend using Railway or PlanetScale)

- myDrive /2.8kStar/GPLv3/202012/js+ts
  - https://github.com/subnub/myDrive
  - https://mydrive-storage.com/
  - MyDrive is an Open Source cloud file storage server (Similar To Google Drive). 
  - 前端js，依赖react-redux
  - 后端ts，依赖express、mongoose
  - MyDrive uses mongoDB to store file/folder metadata, and supports multiple databases to store the file chunks, such as Amazon S3, the Filesystem, or just MongoDB. 
  - https://github.com/vitstef/myDrive

- ezshare /324Star/MIT/202207/js/inactive
  - https://github.com/mifi/ezshare
  - A simple file server that lets you easily share many big files like photos and videos with friends (or between your devices) over a local network without requiring an internet connection.
  - If you don't want to install Node.js, you can download a zipped executable of ezshare
  - It starts an HTTP server that lists all files and directories in the directory
  - Then anyone can then connect to the server and download files or automatically generated ZIP of whole directories (kind of like Google Drive.) 
  - The client can also upload files to the server via their browser, and clipboard card be shared both ways. A QR code is generated for convenience.

- internxt-drive-web /78Star/AGPLv3/202212/ts
  - https://github.com/internxt/drive-web
  - https://internxt.com/drive
  - 类似dropbox
  - 依赖reduxjs/toolkit、idb、react-dnd
  - at Internxt, we've created a suite of services truly focused on you. Switch to Internxt Drive, Photos, Send
  - https://github.com/internxt/drive-server-wip
    - WIP: New version of Drive Server based in NestJS
    - based on NestJS and implements DDD (Domain Driven Design). 
    - Our implementation has these layers: Use cases; Persistence; Domain; Controllers
  - https://github.com/internxt/drive-server
    - 依赖express实现，旧版
    - Database setup (MariaDB)
  - https://github.com/internxt/drive-mobile
    - Current react-native-reanimated fails with Android using RN 0.64

- https://github.com/frappe/drive /python/vue
  - easy to use, document sharing and management solution
  - 依赖werkzeug
  - Upload and store files across multiple platforms.
  - Preview files such as images, videos, PDFs, etc.
# cloud-drive-sync
- https://github.com/reruin/sharelist
  - ShareList 是一个易用的网盘工具，支持快速挂载 GoogleDrive、OneDrive

- https://github.com/harrisoff/onedrive
  - https://github.com/beetcb/sosf
  - 基于 OneDrive API 的图床

- https://github.com/spencerwooo/onedrive-vercel-index
  - https://drive.swo.moe/
  - Showcase, share, preview, and download files inside your OneDrive with onedrive-vercel-index

- https://github.com/golf1052/code-sync
  - Sync VSCode extensions using your favorite file synchronization service

- https://github.com/OneDrive/onedrive-texteditor-js
  - sample application provides a simple markdown (text) editor experience for files stored in OneDrive.
# google-drive
- https://github.com/ErickWendel/semana-javascript-expert05
  - JS Expert 5.0 Week classes - Google Drive Clone
  - This is the starting code to start our journey.
  - https://github.com/CJBiohacker/semana-javascript-expert05

- https://github.com/liberodark/ODrive /202005/js/inactive
  - This is a GUI client for Google Drive on linux

- https://github.com/penge/my-notes
  - Chrome extension for simple and fast note-taking
  - Back up notes to Google Drive
  - Drag and drop image with automatic image upload to Google Drive
  - Works offline

- gdocwiki /81Star/MIT/202205/ts
  - https://github.com/pingcap/gdocwiki
  - A wiki based on Google Doc/Drive.
  - Gdocwiki combines a folder tree view in a sidebar (equivalent to drive.google.com) with a document viewer in the main panel (equivalent to docs.google.com, etc).
  - This is not an official PingCAP product.

- https://github.com/misterfresh/react-drive-cms /202204/js
  - http://misterfresh.github.io/react-drive-cms/
  - Publish articles directly from Google Drive to your blog with React JS
  - A dynamic site, but no backend to manage, no database, no server, no hosting & no maintenance (almost)
  - ReactDrive CMS was started in October 2015. 
  - It uses Github Pages to host static assets, and uses React to generate the HTML on the client.

- wikiGDrive /7Star/ISC/202211/ts/vue
  - https://github.com/mieweb/wikiGDrive
  - WikiGDrive is a node app that uses the Google Drive API to transform Google Docs and Drawings into markdown.
  - Reads all the files from a Google "Shared Drive"

- https://github.com/terence410/ts-google-drive /202110/ts
  - Manage Google Drive easily. Support create folders, upload files, download files, searching, etc.. 
  - The library is build with Google Drive API v3.
- https://github.com/HuasoFoundries/node-google-drive /201910/js
  - Library to operate with Google Drive API v3 from Node.js, using system user tokens or personal keys

- https://github.com/0x5eba/Storage /202008/js
  - Google Drive and Keep clone in a few lines of code.
  - Storage is a safe place that let you store, share and access your files completely anonymously while keeping them secure.
  - Developed with MERN (MongoDB, Express, ReactJS, Node.js) stack.
  - No account needed

- https://github.com/kael-shipman/libgwiki /201804/js
  - A simple single-page app that turns any google drive folder into a traversable wiki
  - Takes a parent folder and provides basic, hierarchical navigation for children and descendents; 
  - Renders docs via HTML export; 

- https://github.com/dash-anurag/dash-drive
  - A google drive clone having features like authentication, folder creation and more.
  - 依赖firebase
- https://github.com/Mironshoh1603/Google-drive-clone
  - React App and Redux
  - 依赖firebase
- https://github.com/RichProsper/RDrive /js
  - RDrive is a Google Drive Mini Clone. 
  - RDrive was built using Reactjs, Firebase and Sass.
  - It allows users to save their folders and files. 

- https://github.com/trnwrckd/drive-clone-ui
  - https://relaxed-kheer-00772d.netlify.app/
  - Tried cloning parts of Google Drive

- https://github.com/stravo1/obsidian-grive-sync
  - sync notes across devices in Obsidian via Google Drive

## google-drive-api-usage

- https://github.com/TeemuKoivisto/google-oauth-drive-example
  - Shows how to use Google OAuth with Google Drive

- https://github.com/theoephraim/node-google-spreadsheet
  - Google Sheets API (v4) wrapper for Node.js
# known-drive-dropbox
- https://github.com/feup-infolab/dendro /202006/js/inactive
  - "Open-source Dropbox" with added description features. 
  - It is a data storage and description platform designed to help researchers and other users to describe their data files, built on Linked Open Data and ontologies. 
  - Users can use Dendro to publish data to CKAN, Zenodo, DSpace or EUDAT's B2Share and others.

- https://github.com/eltonlazzarin/dropbox-fake-app
  - RocketBox - A Full Stack Project App
  - react native

- takenote /2.8kStar/MIT/202108/ts/数据可选local或github
  - https://github.com/taniarascia/takenote
  - https://takenote.dev/app
  - 依赖react-beautiful-dnd、react-router、@reduxjs/toolkit、redux-saga、react-markdown、axios、codemirror、express、jszip
  - A free, open-source notes app for the web
  - The notes are persisted temporarily in local storage, but you can download all notes in markdown format as a zip.
  - Hidden within the code is an alternate version that contain a Node/Express server and integration with GitHub.
# filesystem-utils
- https://github.com/jvilk/BrowserFS /202001/ts/inactive
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
  - 支持 memory/localStorage/indexeddb/dropbox/Emscripten file systems
# aws-s3
- Zenko CloudServer /1.5kStar/apache2/202302/js
  - https://github.com/scality/cloudserver
  - https://www.zenko.io/cloudserver
  - CloudServer (formerly S3 Server) is an open-source Amazon S3-compatible object storage server 
  - CloudServer provides a single AWS S3 API interface to access multiple backend data storage both on-premise or public in the cloud.
  - 支持的存储backend: file, in-memory, multiple
  - [Getting Started](https://s3-server.readthedocs.io/en/latest/GETTING_STARTED.html)
  - [Add S3 SELECT functionality · Issue](https://github.com/scality/cloudserver/issues/3247)
    - Current behavior: Entire file must be pulled back to process one column
    - [Amazon S3 Select supports only the SELECT SQL command.](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-glacier-select-sql-reference-select.html)
  - CloudServer is useful for Developers, either to run as part of a continuos integration test environment to emulate the AWS S3 service locally or as an abstraction layer
# local-network
- https://github.com/localsend/localsend /dart
  - https://localsend.org/
  - An open source cross-platform alternative to AirDrop

- https://github.com/LANDrop/LANDrop /cpp
  - https://landrop.app/
  - Drop any files to any devices on your LAN.
# more-drive
- https://github.com/FazioNico/dDrive
  - An alternative storage solution to Google Drive
  - open-source and fully decentralized that is built on top of the InterPlanetary File System (IPFS)

- https://github.com/storj/storj /202212/go
  - Storj is an S3-compatible platform and suite of decentralized applications that allows you to store data in a secure and decentralized manner. 
  - Your files are encrypted, broken into little pieces and stored in a global decentralized network of computers. 

- https://github.com/enochbayode/google-drive-web-app
  - Storage web app like Google drive
  - 无前端

- https://github.com/obraia/FreeDrive
  - Google Drive e construído em React + NodeJS

- https://github.com/Arunjoseph3007/github-clone-frontend
  - A Github alternative built using NextJS and Django
