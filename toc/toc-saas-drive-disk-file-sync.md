---
title: toc-saas-drive-disk-file-sync
tags: [cloud-drive, data-sync, saas, synchronization, toc]
created: 2022-09-10T02:24:13.285Z
modified: 2024-03-31T17:45:16.789Z
---

# toc-saas-drive-disk-file-sync

# guide

- 需要同步的场景
  - app设置项，如vscode设置，pwa列表
  - app内容，如笔记内容
  - 浏览器标签页部分设置和布局，或扩展列表
  - 同步方式，对大数据或小数据都可以放在云盘，需要自己读取解析

- tips
  - 网盘实现: file-manager + storage-provider
  - 开源cms的files/media通常包含网盘的常用功能
  - 若强调文件预览，则更推荐专门的软件
  - 对于视频类的预览，推荐plex
# 云存储
- 云同步提供商
  - 网盘：百度OAuth2.0, 腾讯文档/微云，onedrive
  - 云服务商：七牛
  - open: next-cloud(php), owncloud(php), seafile(clang)
  - 非主流存储：github仓库、gitee

- 其他云存储
  - 国外：dropbox clone
  - 类似cms的media library

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

- myDrive /2.8kStar/GPLv3/202012/前端js+后端ts/inactive
  - https://github.com/subnub/myDrive
  - https://mydrive-storage.com/
  - MyDrive is an Open Source cloud file storage server (Similar To Google Drive). 
  - 依赖express、mongoose、fluent-ffmpeg、react-redux、react-contextmenu
  - 🐛 不支持 webdav
  - MyDrive uses mongoDB to store file/folder metadata, and supports multiple databases to store the file chunks, such as Amazon S3, the Filesystem, or just MongoDB. 
  - [I created an Open Source Google Drive Clone - MyDrive _202006](https://www.reddit.com/r/selfhosted/comments/h8tvtg/i_created_an_open_source_google_drive_clone/)
    - myDrive uses the HTTP protocol to transfer files.
  - 🍴 forks
  - https://github.com/vitstef/myDrive /202204
    - Fixed build
  - https://github.com/CharlesCatYT/charlDrive /202301/format

- https://github.com/0x5eba/Storage /202008/js/MERN
  - Google Drive and Keep clone in a few lines of code.

- firefiles /133Star/AGPLv3/202308/ts/inactive
  - https://github.com/faisalsayed10/firefiles
  - https://firefiles.app/
  - https://firefiles.vercel.app/
  - Firefiles is an open‑source alternative to Dropbox which lets you setup a cloud drive with the backend of your choice 
  - 存储可选firebase、aws-s3、mysql, 🐛 无单独后端服务器
  - 依赖nextjs、chakra-ui、swr、prisma、dexie-react-hooks
  - A modern file-system interface for your storage buckets.
  - A MySQL database. (We recommend using Railway or PlanetScale)
  - AWS S3 support.
  - [Feature: Download entire folder with its contents_202202](https://github.com/faisalsayed10/firefiles/issues/16)
    - Implement downloading an entire folder (.zip) along with its child files and folders.
    - I can't think of a way where this can be done without a server. So this will probably break our policy of "your files stay with you and we don't access it".
    - Will need to research a bit on this about how this can be done without needing to have a server.

- https://github.com/linagora/twake-drive /9Star/AGPLv3/202402/ts
  - open-source alternative to Google Drive
  - 依赖mui.v4、antd、redux、fullcalendar、dnd-kit、draft-js、minimongo、fastify、rxjs、opensearch、amqplib、mongodb
  - rxjs用在event-bus、message-queue

- internxt-drive-web /78Star/AGPLv3/202403/ts
  - https://github.com/internxt/drive-web
  - https://internxt.com/drive
  - 类似dropbox
  - 依赖reduxjs/toolkit、idb、react-dnd、@headlessui/react、xlsx-preview
  - at Internxt, we've created a suite of services truly focused on you. Switch to Internxt Drive, Photos, Send
  - https://github.com/internxt/drive-server-wip
    - WIP: New version of Drive Server based in NestJS
    - based on NestJS and implements DDD (Domain Driven Design). 
    - Our implementation has these layers: Use cases; Persistence; Domain; Controllers
  - https://github.com/internxt/drive-server /AGPLv3/202401/ts/js/旧版服务端
    - 依赖express、sequelize、mariadb、multer
    - Database setup (MariaDB)，似乎支持pg
  - https://github.com/internxt/drive-mobile
    - Current react-native-reanimated fails with Android using RN 0.64
  - https://github.com/internxt/drive-desktop

- https://github.com/frappe/drive /AGPLv3/202401/python/vue
  - easy to use, document sharing and management solution
  - 依赖werkzeug
  - Upload and store files across multiple platforms.
  - Preview files such as images, videos, PDFs, etc.

- https://github.com/filebrowser/filebrowser /apache2/202401/go/js/vue
  - https://filebrowser.org/
  - https://demo.filebrowser.org/
  - filebrowser provides a file managing interface within a specified directory and it can be used to upload, delete, preview, rename and edit your files. 
  - It allows the creation of multiple users and each user can have its own directory.

- https://github.com/pydio/cells /AGPLv3/202402/go/js
  - https://pydio.com/
  - the nextgen file sharing platform for organizations. 
  - It is a full rewrite of the Pydio project using the Go language following a micro-service architecture.
  - https://github.com/pydio/pydio-core /php/archived

- https://github.com/mgilangjanuar/teledrive /GPLv3/202310/ts
  - open source Google Drive/OneDrive/iCloud/Dropbox alternative using Telegram API for the free unlimited cloud storage.

- https://github.com/saleel/nymdrive /202201/js/ipfs/inactive
  - decentralized, E2E encrypted, privacy friendly alternative to Google Drive/Dropbox.
  - Files are encrypted locally and uploaded to server app using Nym mixnet.
  - Server app (service-provider) store the files in IPFS using Textile buckets.
  - Connect multiple devices running NymDrive and keep them in sync.

- https://github.com/akovacs/uploadserver /MIT/202207/rust/inactive
  - simple standalone webserver which you can upload and download files to/from using just a web browser. 
  - By running just one instance of the uploadserver, you can transfer files between devices on your local network without installing anything on them.

- https://github.com/devld/go-drive /MIT/202401/go/ts/vue
  - https://go-drive.top/
  - simple cloud drive mapping web app supports local, FTP/SFTP, S3, OneDrive, WebDAV, Google Drive.
  - 拖拽/粘贴上传，拖拽管理文件
  - 文件打包下载
  - 基于用户/组的权限控制

- https://github.com/haiwen/seafile /AGPLv3/202402/c
  - http://seafile.com/
  - open source cloud storage system with privacy protection and teamwork features. 

- https://github.com/pydio/cells /AGPLv3/202408/go
  - https://pydio.com/
  - Pydio Cells is an open-source, self-hosted Document Sharing and Collaboration platform specifically designed for organizations that need advanced document-sharing and collaboration without security trade-offs or compliance issues.
# cloud-drive-sync
- https://github.com/qiniu/kodo-browser /apache2/202406/ts
  - 为七牛对象存储（Kodo）提供类似 Windows 资源管理器的功能。用户可以很方便的浏览文件，上传下载文件，支持断点续传等。
  - 参考 阿里 OSS Browser 设计
  - 使用开源框架 React + Electron
  - https://github.com/aliyun/oss-browser /apache2/202406/js
    - 提供类似windows资源管理器功能。用户可以很方便的浏览文件，上传下载文件，支持断点续传等。

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
# dropbox
- https://github.com/mickael-kerjean/filestash /AGPLv3/202408/go/js
  - https://www.filestash.app/
  - A Dropbox-like file manager that let you manage your data anywhere it is located: FTP • FTPS • SFTP • WebDAV • Git • S3 • LDAP • Mysql CardDAV • CalDAV • Backblaze B2 • Minio Dropbox • Google Drive
  - Multiple cloud providers and protocols, easily extensible

- https://github.com/psi-4ward/psitransfer /1.4kStar/BSD/202311/js/vue/inactive
  - Simple open source self-hosted file sharing solution.
  - alternative to paid services like Dropbox, WeTransfer.
  - No accounts, no logins
  - Supports many and very big files (Streams ftw)

- https://github.com/feup-infolab/dendro /28Star/202006/js/inactive
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

- https://github.com/elwood-studio/elwood /apache2/202308/ts/inactive
  - open source Dropbox alternative, built for advanced media management. 
  - Lighting fast uploads. Real-time, multi-user collaboration. 
  - Powerful role-based sharing. 
  - Simple one-click distribution.

- https://github.com/Scille/parsec-cloud /BSL/202503/rust/ts/vue
  - https://parsec.cloud/
  - Open source Dropbox-like file sharing with full client encryption
# webdav
- https://github.com/sigoden/dufs /MIT/202402/rust
  - A file server that supports static serving, uploading, searching, accessing control, webdav...
  - Download folder as zip file
  - Upload files and folders (Drag & Drop)
  - Resumable/partial uploads/downloads
# filesystem
- https://github.com/rejetto/hfs /GPLv3/202402/ts
  - HFS is the best way via web to access or share files from your disk.
  - access files from a phone or another computer just using a browser
  - possibly create accounts and limit access to files
  - Share even a single file with our virtual file system, even with a different name, all without touching the real file. Present things the way you want!
  - Watch all activities in real-time.
  - Control bandwidth, decide how much to give.
  - This is a full rewrite of the Delphi version.

- https://github.com/internalfx/sqlgrid /16Star/apache2/201910/js
  - A file storage system for SQL databases inspired by GridFS
  - Revisions - Keeps multiple versions of files.
  - Supports byte ranges to allow for streaming media.
  - Consistent - Sha256 hashes are calculated when the file is written, and verified when read back out.
  - 依赖sequelize.v5、bluebird、lru
  - https://github.com/internalfx/rethinkdb-regrid

- https://github.com/djedi23/mongodb-gridfs-rs /202310/rust
  - An implementation of Mongo GridFS in Rust
  - provides an implementation of Mongo GridFS on the top of mongodb's crate.
  - This implementation only use the async/await version of mongodb.

- https://github.com/fhellwig/mongodb-filesystem /202006/js
  - Implements a basic filesystem using the MongoDB GridFS interface
- https://github.com/oleksiyk/mongofs /201312/js
  - MongoFS is an implementation of MongoDB GridFS that emulates node.js fs module

## fs-utils

- https://github.com/jvilk/BrowserFS /202001/ts/inactive
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
  - 支持 memory/localStorage/indexeddb/dropbox/Emscripten file systems
# s3/minio
- Zenko CloudServer /1.5kStar/apache2/202401/js
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

- https://github.com/deuxfleurs-org/garage /AGPLv3/202401/rust
  - https://git.deuxfleurs.fr/Deuxfleurs/garage
  - https://garagehq.deuxfleurs.fr/
  - self-hosted drop-in replacement for the Amazon S3 object store.
  - Garage is designed for storage clusters composed of nodes running at different physical locations
  - Self-contained: We ship a single dependency-free binary that runs on all Linux distributions
  - https://twitter.com/eatonphil/status/1755942977443074410
    - Internally garage uses only crdt.
    - why not raft/paxos? the leader is a bottleneck for all requests
  - https://twitter.com/bluxte/status/1753823896715886898
    - TIL minio not for geo distribution
  - [Internals | Garage HQ](https://garagehq.deuxfleurs.fr/documentation/design/internals/)
    - CRDT semantics by default keep all tombstones, because they are necessary for reconciliation
    - Garage makes use of Sled's atomic operations (such as compare-and-swap and transactions) to ensure that only tombstones that have been correctly propagated to other nodes are ever deleted from the local entry tree.

- https://github.com/juicedata/juicefs /apache2/202401/go
  - https://juicefs.com/
  - a distributed POSIX file system built on top of Redis and S3.
  - The data, stored via JuiceFS, will be persisted in Object Storage (e.g. Amazon S3), and the corresponding metadata can be persisted in various compatible database engines such as Redis, MySQL, and TiKV based on the scenarios and requirements.
  - Supported Object Storage: s3, minio, Ceph RGW, Redis, Local disk

- https://github.com/s3fs-fuse/s3fs-fuse /GPLv2/202312/cpp
  - FUSE-based file system backed by Amazon S3
  - s3fs allows Linux, macOS, and FreeBSD to mount an S3 bucket via FUSE(Filesystem in Userspace).
  - s3fs makes you operate files and directories in S3 bucket like a local file system.
# file-sharing/local-network
- https://gitlab.com/timvisee/send /MPLv2/202306/js
- https://github.com/timvisee/send
  - https://send.vis.ee/
  - Simple, private file sharing
  - A fork of Mozilla's Firefox Send. Mozilla discontinued Send, this fork is a community effort to keep the project up-to-date and alive.

- https://github.com/kern/filepizza /BSD/202502/ts
  - https://file.pizza/
  - Peer-to-peer file transfers in your browser
  - Works on most mobile browsers, including Mobile Safari.
  - 依赖nextjs、PeerJS for WebRTC、Redis(optional)
  - Using WebRTC, FilePizza eliminates the initial upload step required by other web-based file sharing services. 
    - files are sent directly from your browser to the downloader's browser. They never pass through our servers. 
    - Transfers are now directly from the uploader to the downloader's browser (WebRTC without WebTorrent) with faster handshakes.
    - Uploaders can monitor the progress of the transfer and stop it if they want.
  - Support for uploading multiple files at once, which downloaders receive as a zip file.
  - Streaming downloads with a Service Worker.
  - Out-of-process storage of server state using Redis.

- ezshare /324Star/MIT/202207/js/inactive
  - https://github.com/mifi/ezshare
  - A simple file server that lets you easily share many big files like photos and videos with friends (or between your devices) over a local network without requiring an internet connection.
  - If you don't want to install Node.js, you can download a zipped executable of ezshare
  - It starts an HTTP server that lists all files and directories in the directory
  - Then anyone can then connect to the server and download files or automatically generated ZIP of whole directories (kind of like Google Drive.) 
  - The client can also upload files to the server via their browser, and clipboard card be shared both ways. A QR code is generated for convenience.

- https://github.com/RobinLinus/snapdrop /17.2kStar/GPLv3/202302/js/inactive
  - https://snapdrop.net/
  - local file sharing in your browser. Inspired by Apple's Airdrop.
  - Vanilla HTML5/ES6/CSS3 frontend
  - WebRTC/WebSockets
  - https://github.com/schlagmichdoch/PairDrop /js
    - PairDrop is a sublime alternative to AirDrop that works on all platforms.
    - File Sharing on your local network
    - Fork of Snapdrop.

- https://github.com/localsend/localsend /dart
  - https://localsend.org/
  - An open source cross-platform alternative to AirDrop

- https://github.com/LANDrop/LANDrop /cpp
  - https://landrop.app/
  - Drop any files to any devices on your LAN.

- https://github.com/hyperhyperspace/hyperhyperspace-core /MIT/ts
  - https://www.hyperhyperspace.org/
  - A library to create p2p applications, using the browser as a full peer.
  - An offline-first shared data library for creating p2p apps that work in the browser (and now also NodeJs).
  - HHS uses an immutable typed-objects local storage model. 
    - Objects are both retrieved and cross-referenced using a structural hash of their contents as their id (a form of content-based addressing).
  - Mutability is implemented using CRDTs. Identities and data authentication are cryptographic.
  - Objects and their references form an immutable DAG, a fact that is used for data replication in HHS p2p mesh.

- https://github.com/cypsela/sailplane-web /GPLv3/202206/js
  - https://cypsela.github.io/sailplane-web
  - Collaborative p2p file sharing in the browser
  - https://github.com/cypsela/sailplane-node /202101/js/inactive

- https://github.com/Peergos/Peergos /AGPLv3/202402/java
  - https://peergos.org/
  - A p2p, secure file storage, social network and application protocol

## file-ssh

- https://github.com/vitodeploy/vito /AGPL/202502/php
  - Free and Self-Hosted Server Management Tool
  - https://x.com/saeed_vz/status/1886166663113949238
    - Vscode has a plug in for editing files over ssh as well.
    - Thats what I do usually. But a web interface inside the app sometimes is handy for very quick needs
# files-preview
- https://github.com/musama619/react-files-preview /MIT/202311/ts
  - https://react-files-preview.netlify.app/
  - A file view component for React apps with image editor, and a sleek design powered by Tailwind CSS
  - 偏向图片
# more-drive
- https://github.com/FazioNico/dDrive
  - An alternative storage solution to Google Drive
  - open-source and fully decentralized that is built on top of the InterPlanetary File System (IPFS)
  - The foundation of Peergos is a peer-to-peer encrypted global filesystem with fine-grained access control
  - Peer-to-peer and data layer - IPFS provides the data storage, routing and retrieval.

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
