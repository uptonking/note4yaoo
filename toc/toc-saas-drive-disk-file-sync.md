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
# 国外云存储
- icloud 需付费成为apple-developer
  - [iOS独立开发-基于iCloud构建用户体系](https://zhuanlan.zhihu.com/p/392378738)

- firebase
# 国内云存储
- [白嫖中国科技云 20G 存储，并接入 Obsidian 实现同步  ](https://linux.do/t/topic/1505165)
  - 提供了一个 免费的 20G 存储（兼容 S3）。

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
- https://github.com/suitenumerique/drive /77Star/MIT/202509/python/ts
  - A collaborative file sharing and document management platform that scales. 
  - Built with Django and React.
  - [已合并@202509 (back) create wopi application ](https://github.com/suitenumerique/drive/pull/2)

- https://github.com/opencloud-eu/opencloud /2.1kStar/apache2/202509/go
  - https://opencloud.eu/
  - This the main repository of the OpenCloud server. It contains the golang codebase for the backend services.
  - 🛢️ The OpenCloud backend does not use a database. It stores all data in the filesystem. By default, the root directory of the backend is `$HOME/.opencloud/`.
  - Architecture: Built with a microservices approach
  - The OpenCloud backend authenticates users via OpenID Connect using either an external IdP like Keycloak or the embedded LibreGraph Connect identity provider.
  - 📱 支持 web/win/mac/linux/android/ios
  - 📡 尝试自定义客户端
  - https://github.com/opencloud-eu/web /112Star/AGPL/202507/ts/vue
    - Web UI for OpenCloud built with Vue.js and TypeScript
    - Files: Upload, download, search and manage files 
    - Versioning: Saved the wrong version? We have the time machine you were looking for! Easily go back in time and restore older versions of your files.
    - Share: Allow fine-grained access to files and whole folders directly with other users on your OpenCloud.
    - Create links and share them with anyone in the world - optional password-protection available.
    - Write: Edit your documents with the editor of your choice like Collabora, ONLYOFFICE or Microsoft Word and more.
    - Extensible: OpenCloud Web is built as a platform that can be extended in the most developer friendly way.
    - extension-sdk: Provides utilities for developing and integrating custom extensions
    - runtime: Central place of (user) authentication, provisioning of the user interface layout, client side storage, routing, theming, dependencies and (sub)application handling
  - https://github.com/opencloud-eu/web-extensions
    - A collection of officially supported apps and extensions for OpenCloud Web
    - web-app-draw-io
    - web-app-json-viewer
    - web-app-importer
    - web-app-unzip
  - https://github.com/opencloud-eu/desktop /GPL/cpp
  - https://github.com/opencloud-eu/android /GPL/kotlin
  - https://github.com/opencloud-eu/ios /GPL/swift
  - [Support any S3 provider instead of just Minio _202507](https://github.com/orgs/opencloud-eu/discussions/1149)
    - This is a misunderstanding. Every S3 compatible Storage should work.
  - [[Feature] External S3 storage additionally mounting and encryption _202505](https://github.com/opencloud-eu/opencloud/issues/875)
    - Is it currently possible to mount an additional s3 bucket (to the existing primary) for data storage into opencloud? 
    - OpenCloud can be set up with the so called DecomposedS3 storage driver, which uses S3 as storage for the binary blobs, in addition to a little bit of Posix storage for the metadata storage, that references to the S3.
    - I think it should be possible to also encrypt the S3 buckets, independently from OpenCloud, as a feature of the storage
    - OpenCloud however does not yet support client side S3 encryption.

- https://github.com/DrizzleTime/Foxel /1kStar/MIT/202602/python/ts
  - https://foxel.cc/
  - https://demo.foxel.cc/
  - extensible private cloud storage solution for individuals and teams, featuring AI-powered semantic search.
  - Unified File Management: Centralize management of files distributed across different storage backends.
  - extensible adapter pattern to easily integrate various storage types:
    - Local, S3-compatible, WebDAV, SFTP, FTP
    - Google Drive, OneDrive, Dropbox, Quark
    - Telegram, AList, Foxel-to-Foxel
  - Semantic Search: configurable embedding providers and vector databases (Milvus, Qdrant).
  - Preview images, videos, PDFs, Office documents, text, and code files directly in the browser — no downloads required.
  - full-featured Role-Based Access Control (RBAC) system to secure your data
  - Generate public or password-protected share links with configurable expiration dates
  - a manifest-based plugin architecture: Load React frontend components and custom backend routes at runtime, without modifying the core codebase.
  - Run asynchronous background tasks — file indexing, data backups, scheduled jobs — without impacting the main application.
  - agent with built-in tools for VFS operations, web fetching, and file processing — bringing intelligent automation directly into your cloud storage.
  - Backend	Python 3.14+, FastAPI, Tortoise ORM, SQLite
  - Frontend	React 19, TypeScript, Vite, Ant Design
  - Vector DB	Milvus Lite / Server, Qdrant
  - [「开源自荐」Foxel V2 不仅是网盘，更是你的 AI 文件操作系统（支持插件/RBAC/多存储） _202602](https://linux.do/t/topic/1589655)
    - 如果说 v1 是 “好用的文件管理器”，那么 v2 则是 “可扩展的 AI 文件操作系统” 。在保留了美观界面的同时，补齐了权限管理、插件系统和 AI Agent 能力。
    - 参考并致敬了 AList 的设计，现在支持挂载更多主流存储云盘
  - [[开源] Foxel 转型成智能文件管理系统啦 _202508](https://linux.do/t/topic/915704)
    - 当时选用 .NET 开发，后续发现很多感兴趣的开发者并不熟悉 .NET 技术栈，这次我用 Python 对整个项目进行了重构，不仅从原来的 “图片管理” 升级为全类型文件管理

- https://github.com/owncloud/ocis /1.8kStar/apache2/202510/go
  - https://doc.owncloud.com/ocis/next/
  - ownCloud Infinite Scale (oCIS) is the new file sync & share platform that will be the foundation of your data management platform.
  - [Provide login option for Basic Auth and SSO at the same time _202508](https://github.com/owncloud/ocis/issues/11601)
    - this will be hard to implement as requested. When having an external IDP configured, oCIS uses that as source of truth for the authentication. That means that ocis itself does not store any password information internally, hence it can't authenticate basic auth requests. I do not think it is a good idea to duplicate this password information. 
    - A better solution to this problem is in my opinion to allow multiple IDPs. This would give the user the opportunity to choose its identity provider on login. These IDPs would be independent from each other, means each one will have their own password.
  - [OIDC can't be set up for the hardcoded clients · Issue · owncloud/ocis](https://github.com/owncloud/ocis/issues/9389)
    - The OIDC implementation that ownCloud uses is fundamentally broken: the clients are not authenticating in a way that anyone considers rational, and which is incompatible with many identity providers. ownCloud's response here is nothing short of absolutely wild, from suggesting small home users pay an enterprise subscription to rationalizing the why it's not broken "because of the history".
  - https://github.com/owncloud/web /516Star/AGPL/202510/ts/vue
    - https://owncloud.dev/clients/web/
    - Next generation frontend for ownCloud Infinite Scale

- https://github.com/gtsteffaniak/filebrowser /3.3kStar/apache2/202509/go/ts/vue
  - FileBrowser Quantum is a massive fork of the file browser 
  - Add and configure multiple sources
  - Login support for OIDC, password + 2FA, and proxy
  - Directory-level access control that can be scoped to user or group.
  - Developer API support: create long-lived API Tokens
  - 依赖go-cmp、image、jwt
  - Simplified configuration via `config.yaml` config file.
  - 🔍 Ultra-efficient indexing and real-time updates
  - 🆚 readme最后提供了产品对比图
  - Notable features that this fork does not have (removed):
    - jobs are not supported yet.
    - shell commands are completely removed and will not be returned.
    - [Command Execution - File Browser](https://filebrowser.org/command-execution.html)
      - Within File Browser you can toggle the shell (< > icon at the top right) and this will open a shell command window at the bottom of the screen. 
  - [add s3 compatibility _202407](https://github.com/gtsteffaniak/filebrowser/issues/140)
    - We are working on adding s3 compatibility, on this branch. Right now, it is on a early stage but functional, we have tried so far with Minio and Backblaze B2 and all basic funcionality is there
  - 📡 roadmap
    - electron-app
  - https://github.com/Softwaredam/filebrowser-chart
    - For anyone interested in a chart to deploy it on Kubernetes
  - [High memory usage _202506](https://github.com/gtsteffaniak/filebrowser/issues/747)
    - With an 80TB source, indexing takes 12–24h (interestingly, full sync seems faster), which is fine. However, after running the program for several days, memory usage grows to unreasonable levels. For the 80TB source, RAM usage reached 50GB+. I haven't tested this rigorously, but it seems memory usage increases with each indexing and doesn't drop, just keeps growing with subsequent indexing runs.
    - There is one "memory leak" I am aware of, if a folder is delete/renamed or moved, that directory info will stay in memory until restart. Is this possibly what's happening? Do you move large directories often?
    - The other situation I know increases ram is when you search, but that should clear after a while on its own with garbage collection.
    - 202506: A lot of good changes in 0.7.10 regarding excluded files/folders. 
    - 202511: I have created an experimental release that utilizes sqlite to improve memory performance, would love to get feedback
  - [v1.0.0 stable release update _202509](https://github.com/gtsteffaniak/filebrowser/discussions/1293)
    - introduction of SQLite database: 
    - Initially, this will be primarily for job status information.
    - eventually, this could enable RAM-free indexing and replace the existing simple (but very fast) database.
  - [Database - SQLite  _202510](https://github.com/gtsteffaniak/filebrowser/discussions/1471)
    - I was hoping the index was already in a SQLite db so I could see if I could use the unique IDs assigned to a path as a universal id for image sharing (even if path changes) but looks like the SQLite Db is currenty not the full index and just for the job processing 
    - 202511: check out this experimental build which uses SQLite for indexing. The benefit is reduced memory usage, but it is a bit slower and more io heavy. But seems like a decent compromise.
  - [Beta/v1.1.2 _20251129](https://github.com/gtsteffaniak/filebrowser/pull/1679)
  - [bbolt/boltdb alternative _202507](https://github.com/gtsteffaniak/filebrowser/issues/1026)
  - [Feature Request – filebrowser-quantum-sync _202512](https://github.com/gtsteffaniak/filebrowser/issues/1767)
    - https://github.com/cryinkfly/filebrowser-quantum-sync /apache2/go
    - The filebrowser-quantum-sync tool is designed to work with FileBrowser Quantum 🔄. It reads the BoltDB database and automatically extracts usernames and hashed passwords, generating a users file compatible with htpasswd
    - This is perfect for multi-container setups 🛠️ (e.g., FileBrowser Quantum + Radicale), ensuring centralized and consistent authentication without duplicating user management. Centralizes authentication across containers
    - PS: Bolt DB will soon be deprecated and this will need refactoring
  - [allow tagging files for search _202407](https://github.com/gtsteffaniak/filebrowser/issues/143)

- https://github.com/filebrowser/filebrowser /31.1kStar/apache2/202509/go/ts/vue
  - https://filebrowser.org/
  - https://demo.filebrowser.org/
  - filebrowser provides a file managing interface within a specified directory and it can be used to upload, delete, preview, rename and edit your files. 
  - It allows the creation of multiple users and each user can have its own directory.
  - User Management, Easy Login System
  - File Editing
  - 不支持OIDC, 相关pr都关闭了
  - [S3 support _202009](https://github.com/filebrowser/filebrowser/issues/1077)
    - 👷202010: cloud storage support is out of the scope of this project. As @fdefilippo mentioned you can mound your s3 bucket using fuse.
    - A work-around I've found when trying to get S3 to act as the storage back-end for Filebrowser, at least when deploying Filebrowser as a container, is to mount the Filebrowser storage folder to an NFS share interface tying back to S3.
  - [add minio as file storage  _202202](https://github.com/filebrowser/filebrowser/issues/1809)
    - Filebrowser uses spf13/afero as a filesystem abstraction layer. 
    - S3 support can be added after adding it to the afero package.
  - [What's the database format of filemanager.db? _201906](https://github.com/filebrowser/filebrowser/issues/779)
    - it is BoltDB. We use bbolt fork since the original was archived. It has the same API and some improvements.
  - https://github.com/spf13/afero /6.4kStar/apache2/202508/go
    - The Universal Filesystem Abstraction for Go
  - [[Feature Request] File Tags ](https://github.com/filebrowser/filebrowser/issues/3351)

- https://github.com/xiaobaidadada/filecat /77Star/apache2/202601/ts
  - https://filecat.xiaobaidadada.fun/
  - 一个基于 Web 的文件服务器、服务器管理工具。集成了文件管理、超大日志查看、远程终端访问、系统进程监控，以及包括 VPN、SSH、RDP、HTTP、TCP 等多种网络代理功能。
  - 用于管理服务器上的文件，但是不是用于云盘访问(未来没有开发计划)，支持文件的各种编辑操作预览。
  - 支持windows、linux、mac。
    - 目前 不支持直接在 macOS 系统上运行。 由于部分子功能由 C 语言实现，尚未跨平台，无法确保在 macOS 上的构建与运行。 不过你仍然可以使用 Docker 容器方式在 macOS 上体验所有功能。
    - 部分依赖为 C++ 原生模块，已预构建发布至 GitHub（支持 Node.js 16、18、20、22）
  - [FileCat-Docs-技术介绍](https://filecat.xiaobaidadada.fun/#/zh-CN/%E6%8A%80%E6%9C%AF/%E6%8A%80%E6%9C%AF%E4%BB%8B%E7%BB%8D.md)
    - 基于node.js ，使用TypeScript，http 功能使用 routing-controllers 与 express，长连接是websocket，
    - 前端采用react框架，样式采用filebrowser的，前端样式基本是复制的filebrowser的。全局状态管理使用了 recoil
    - 后端工作量有点小大的几个功能是，虚拟网络vpn，workflow自动化构建，虚拟终端 pty-shell ，大日志文件日志，这些功能都是本项目自己原创设计实现的，还有个rdp 原创桌面控制，是采用了其它项目的源码， 我给直接复制过来改了一下，node.js 的rdp代理好像目前只有MeshCentral实现了可以远程访问的。
    - 传输编码做了两个版本的实现，proto和socket.io的socket.io-parser。
    - 数据库使用多个json文件，连sqlite都没有使用，因为没有必要，本项目能产生数据的地方极少，json文件是足够的
    - 前后端都使用 webpack打包。
  - 本项目是对filebrowser的功能增强，使用和filebrowser一样的ui，以服务器文件管理为基础添加一些服务器控制功能
  - 文件管理: 支持断点分块上传、多个根目录、代码\图片编辑、编辑器模式、白板绘图...
  - 终端：相比filebrowser使用了xterm.js，并且采用了虚拟shell完美实现命令的权限过滤，避免用户执行类似 rm -r / 的危险命令
  - CI/CD自动化构建：内置了一个模仿github workflow 语法实现的自动化构建功能，作用于以.act结尾的文件
  - ssh代理: 可以管理多个linux服务器，作用和winscp类似，让终端和文件管理更方便。除此之外还支持http代理，rdp远程桌面(windows)等代理
  - https://github.com/Ylianst/MeshCentral /apache2/202601/js
    - https://meshcentral.com/
    - A complete web-based remote monitoring and management web site. Once setup you can install agents and perform remote desktop session to devices on the local network or over the Internet.

- https://github.com/OpenListTeam/OpenList /15.5kStar/AGPL/202509/go
  - A new AList Fork to Anti Trust Crisis
  - https://github.com/OpenListTeam/OpenList-Frontend /MIT/202509/ts/solidjs
    - The front-end of OpenList, powered by SolidJS
- https://github.com/alist-org/alist /MIT > AGPL/go
  - 一个支持多存储的文件列表程序，基于 go-Gin 和 Solidjs。
  - 支持 国内外主流网盘
  - SolidJS + Hope UI，已经停止维护
  - https://github.com/AlistGo/alist-web

- https://github.com/drivebase/drivebase /MIT/202510/ts/inactive
  - https://drivebase.github.io/
  - self-hosted cloud file manager designed to unify file storage across multiple cloud providers into one seamless interface.
  - ⚠️ This project is currently being migrated to Golang and getting a dashboard redesign with many other changes.
  - Multi-Cloud Integration (Google Drive, Dropbox, etc.)
  - File Routing Rules for Automated Uploads

- myDrive /2.8kStar/GPLv3/202012/前端js+后端ts/ ~~inactive~~ 
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

- https://github.com/linagora/twake-drive /9Star/AGPLv3/202505/ts/inactive
  - open-source alternative to Google Drive
  - 依赖mui.v4、antd、redux、fullcalendar、dnd-kit、draft-js、minimongo、fastify、rxjs、opensearch、amqplib、mongodb
  - rxjs用在event-bus、message-queue
  - https://github.com/linagora/linshare /旧版

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
  - Preview files such as images, videos, PDFs, etc

- https://github.com/chibisafe/chibisafe /2.4kStar/MIT/202507/ts/inactive
  - https://chibisafe.app/
  - Chibisafe is a file uploader service written in typescript
  - It accepts files, photos, documents, anything you imagine and gives you back a shareable link for you to send to others.
  - You can run it in public mode, user accounts mode or invite-only mode.
  - The service also comes with a dashboard where you can edit almost every configuration of the instance directly from the UI without having to touch environment or configuration files manually. 
  - S3 Storage Support
  - File management and file tagging
  - Snippets/Gists creation with direct links to share
  - User management and quotas
  - Built-in URL shortener
  - Easily extensible

- https://github.com/pydio/cells /2kStar/AGPLv3/202509/go/js
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

- https://github.com/haiwen/seafile /13.6kStar/AGPLv3 > GPLv2/202402/c
  - http://seafile.com/
  - open source cloud storage system with privacy protection and teamwork features. 

- https://github.com/DioCrafts/OxiCloud /1.8kStar/MIT/202506/rust/js
  - A lightweight, Rust-powered alternative to NextCloud
  - Lightweight: Minimal resource requirements compared to PHP-based alternatives
  - Simple Setup: Get running with minimal configuration
  - Responsive UI: Clean, fast interface that works well on both desktop and mobile
  - Optimized Binary: Uses Link Time Optimization (LTO) for maximum performance
  - PostgreSQL 13+ database, 512MB RAM minimum (1GB+ recommended)
  - I built OxiCloud because I wanted a simpler, faster file storage solution than existing options. After struggling with NextCloud's performance on my home server, I decided to create something that prioritizes speed and simplicity while still being robust enough for daily use.

- https://github.com/cloudreve/cloudreve /25.4kStar/GPL/202510/go
  - https://cloudreve.org/
  - Self-hosted file management and sharing system, supports multiple storage providers
  - Support storing files into Local, Remote node, OneDrive, S3 compatible API, Qiniu, Aliyun OSS, Tencent COS, Upyun.
  - Compress/Extract files, download files in batch.
  - WebDAV support covering all storage providers.
  - Multi-users with multi-groups.
# cloud-drive-sync
- https://github.com/syncthing/syncthing /75.9kStar/MPL/202509/go
  - https://syncthing.net/
  - Syncthing is a continuous file synchronization program. 
  - It synchronizes files between two or more computers. 
  - Safe From Data Loss: We take every reasonable precaution to avoid corrupting the user's files.

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
- https://github.com/mickael-kerjean/filestash /12.6kStar/AGPLv3/202509/go/js
  - https://www.filestash.app/
  - A Dropbox-like file manager that let you manage your data anywhere it is located: FTP • FTPS • SFTP • WebDAV • Git • S3 • LDAP • Mysql CardDAV • CalDAV • Backblaze B2 • Minio Dropbox • Google Drive
  - Multiple cloud providers and protocols, easily extensible
  - Extensible / Customisable / Hackable via a rich ecosystem of plugins
  - Shared Links which you can mount locally as network drives

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
# webdav
- https://github.com/cs3org/reva /197Star/apache2/202510/go
  - https://reva.link/
  - WebDAV/gRPC/HTTP high performance server to link high level clients to storage backends
  - Reva is an interoperability platform consisting of several daemons written in Go. 
  - It acts as bridge between high-level clients (mobile, web, desktop) and the underlying storage (CephFS, EOS, local filesytems). 
  - It also exports a high-performance gRPC API, codenamed CS3 APIs, to easily integrate with other systems. 
  - Reva is meant to be a high performant and customizable HTTP and gRPC server.
  - [Decide on HTTP chunked-data transfer protocol _201910](https://github.com/cs3org/reva/issues/290)
    - Compare different chunking data transfer protocols and chose the one that everyone should implement.
    - The protocol needs to allow to upload by chunks of data (files are split into small chunks) and resumable, if the transfer is cut, the client should be able to discover what are the missing chunks to be uploaded.
    - tus.io and ownCloud rely solely on HTTP headers while the rest rely on some encoded payload.
    - @butonic prefers relying only on headers and I also share the same opinion.
    - I think `tus` is a great approach. IMHO tus and ownCloud Chunking NG share the same basic ideas, which is cool, but tus is way further on the way to become a real standard: It has many supporters, people who verified it's concepts and wrote code and put it in production. That alone makes it the top candidate
    - the decision is that we use tus.
  - https://github.com/tus/tusd
    - Reference server implementation in Go of tus: the open protocol for resumable file uploads
  - 🍴 forks
  - https://github.com/opencloud-eu/reva

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
# fs-filesync
- https://github.com/rclone/rclone /55.1kStar/MIT/202601/go
  - https://rclone.org/
  - "rsync for cloud storage" - Google Drive, S3, Dropbox, Backblaze B2, One Drive, Swift, Hubic, Wasabi, Google Cloud Storage, Azure Blob, Azure Files, Yandex Files
  - https://github.com/RsyncProject/rsync /4.1kStar/GPL/202601/c
    - https://rsync.samba.org/
    - open source utility that provides fast incremental file transfer. 
    - It also has useful features for backup and restore operations among many other use cases.

- https://github.com/fccview/scatola-magica /LGPL/202512/ts
  - A simple, self-hosted file storage/transfer app.
  - a privacy first, lightweight alternative to overcomplicated, bloated file storage solutions, to transfer, manage, encrypt/decrypt your personal files and folders. 
  - It's built with Next.js 14, is easy to deploy, and keeps all your data on your own server.
  - It features optional PGP encryption for stored items and optional AES-256-GCM encryption for file transfer.
  - [[beta] Scatola Magica - Self hosted file sharing system : r/selfhosted _202511](https://www.reddit.com/r/selfhosted/comments/1p8b80o/beta_scatola_magica_self_hosted_file_sharing/)

- https://github.com/datopian/giftless /157Star/MIT/202507/python
  - https://giftless.datopian.com/
  - Giftless is a Python implementation of a Git LFS Server. 
  - It is designed with flexibility in mind, to allow pluggable storage backends, transfer methods and authentication methods.
  - Giftless supports the basic Git LFS transfer mode with the following storage backends:
    - Local storage
    - Amazon S3 Storage
    - Google Cloud Storage
    - Azure Blob Storage with direct-to-cloud or streamed transfers
  - In addition, Giftless implements a custom transfer mode called multipart-basic, which is designed to take advantage of many vendors' multipart upload capabilities. It requires a specialized Git LFS client to use, and is currently not supported by standard Git LFS.
  - https://github.com/datopian/giftless-client
# fs-utils
- https://github.com/jvilk/BrowserFS /202001/ts/inactive
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
  - 支持 memory/localStorage/indexeddb/dropbox/Emscripten file systems
# file-sharing/local-network
- https://gitlab.com/timvisee/send /5.6kStar/MPLv2/202507/js/inactive
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

- https://github.com/ZhangShengFan/FastFile /MIT/202603/js/单文件
  - http://file.091224.xyz/
  - 基于 Cloudflare Workers 的文件快传工具，支持口令保护、二维码分享、在线预览。
  - 基于 Cloudflare Workers + KV 的轻量级文件快速分享工具
  - 无需服务器 · 无需数据库 · 一键部署 · 全球加速
  - 可设置提取口令，防止文件被陌生人下载
  - 自定义有效期	10分钟 ~ 3天，过期自动删除
  - 管理后台	支持多 Worker 接口调度，统一管理配额
  - API 接口	提供标准 REST API，方便第三方集成
  - [开源了！基于CF的文件快传工具 _202603](https://linux.do/t/topic/1674057)

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
# files-protocols
- https://github.com/xetdata/nfsserve /685Star/BSD/202409/rust
  - This is an incomplete but very functional implementation of an NFSv3 server in Rust.
  - I wanted to implement a user-mode file-system mount that is truly cross-platform. What is a protocol that pretty much every OS supports? NFS.
  - Portmapper is a very old mechanism which is rarely used anymore. We do not strictly need to implement this protocol as this is pretty much unused these days (NFSv4 does not use the portmapper for instance).
  - [XetHub | NFS > FUSE: Why We Built our own NFS Server in Rust _202309](https://xethub.com/blog/nfs-fuse-why-we-built-nfs-server-rust)
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
