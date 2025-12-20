---
title: toc-office-suite-web
tags: [office-suite, toc]
created: 2023-03-09T13:46:52.602Z
modified: 2023-03-09T13:47:07.317Z
---

# toc-office-suite-web

# guide

- office-online
  - [Zoho Writer](https://www.zoho.com/writer/)

- https://github.com/tycrek/degoogle
  - https://tycrek.github.io/degoogle/
  - alternatives to Google products

- resources
  - [List of office suites - Wikipedia](https://en.wikipedia.org/wiki/List_of_office_suites)
  - [精读《WOPI协议》 - 掘金](https://juejin.cn/post/7105322391597187103)
    - WOPI是微软基于REST API的协议，定义了一组Http操作，使客户端能够访问和改变服务器存储的文件。
# office-popular
- https://github.com/dream-num/univer /11.9kStar/apache2/202512/ts
  - https://univer.ai/
  - An Isomorphic Full-Stack Framework for Creating and Editing Spreadsheets Across Web and Server.
  - Univer is designed to support spreadsheets, documents and presentation.
  - Univer is isomorphic. It can run both on browsers and Node.js (in the future, mobile devices as well), with the same API.
  - Univer is easily embeddable, allowing seamless integration into your applications
  - highly extensible, thanks to its plug-in architecture 
  - Univer is a highly integrated system. Documents, spreadsheets and slides can interoperate with each others and even rendered on the same canvas

- onlyoffice-sdkjs /190Star/AGPLv3/202302/js
  - https://github.com/ONLYOFFICE/sdkjs
  - https://personal.onlyoffice.com/
  - https://api.onlyoffice.com/docbuilder/spreadsheetapi
  - 💡 word/excel/ppt都基于canvas实现
  - Contains API for all the included components client-side interaction.
  - 通过TypedArray，将表格数据以二进制格式存储，通过字段压缩+共享字符串表来优化内存空间
  - [精读onlyoffice在线表格存储设计](https://juejin.cn/post/7202252704978386999)
  - repos
    - https://github.com/ONLYOFFICE/document-editor-react-samples
      - 示例依赖server api，本地无法运行
    - https://github.com/ONLYOFFICE/document-editor-react
      - 示例依赖server api，本地无法运行
  - https://github.com/phpk/godoos
    - 一款高效的内网办公操作系统，内含word/excel/ppt/pdf/聊天/白板/思维导图等多个办公系统工具
    - 支持配置onlyOffice地址，onlyOffice编辑word/ppt/excel文件
- https://github.com/ibisheng/onlyoffice-ibisheng /AGPLv3/201911/js
  - 毕升文档在线文件服务部分在编辑和预览Office时集成了onlyOffice。我们在集成onlyOffice主要是使用了sdkjs部分代码
  - 抛弃了only Office的原来的UI，整体UI重新设计实现
  - 抛弃了原来only Office开源部分的服务器实现，使用golang 和node js重新了实现Office在线编辑时的服务器逻辑
  - 文件的底层存储也抛弃了原来only Office的方案，按照毕升文档在线文件服务的设计，全部采用s3 api的存储。 本地部署时可以使用minio来实现s3服务
  - 与开源版的only office相比，毕升文档在线Office部分主要增加了文件加水印预览以及文件的版本对比功能
- https://github.com/ONLYOFFICE/DocumentServer
  - Starting from version 6.0, Document Server is distributed under a new name - ONLYOFFICE Docs.
  - https://github.com/ONLYOFFICE/CommunityServer /c#/apache2
    - open source office suite with business productivity tools: document and project management, CRM, mail aggregator.
  - https://github.com/ONLYOFFICE/server
    - backend server software layer which is the part of ONLYOFFICE Document Server and ONLYOFFICE Desktop Editors and is the base for all other components.
  - https://github.com/ONLYOFFICE/core /cpp
    - Server core components which are a part of ONLYOFFICE Document Server

- https://github.com/ranuts/document /1.6kStar/AGPL/202512/js
  - https://ranuts.github.io/document/
  - A local web-based document editor based on `OnlyOffice`, allowing you to edit documents directly in your browser without server-side processing
  - All document processing happens locally in your browser, with no uploads to any server
  - Multi-Format Support: Supports DOCX, XLSX, PPTX, CSV, and many other document formats
  - OnlyOffice SDK: Provides powerful document editing capabilities
  - WebAssembly: Implements document format conversion through `x2t-wasm`.
  - https://github.com/sweetwisdom/onlyoffice-web-local /AGPL/202507/ts/inactive
    - https://sweetwisdom.github.io/onlyoffice-web-local/
    - A purely local project based on OnlyOffice, supporting local opening and editing of Office documents.

- cryptpad /4.3kStar/AGPLv3/202406/js/onlyoffice
  - https://github.com/cryptpad/cryptpad
  - https://github.com/xwiki-labs/cryptpad
  - https://cryptpad.org/
  - CryptPad is a collaboration suite that is end-to-end-encrypted and open-source.
  - 依赖 onlyoffice、netflux-websocket
  - It is built to enable collaboration, synchronizing changes to documents in real time. 
  - Because all data is encrypted, the service and its administrators have no way of seeing the content being edited and stored.
  - [Rich Text — CryptPad 5.6.0 documentation](https://docs.cryptpad.org/en/user_guide/apps/richtext.html)
  - The Rich Text application in CryptPad is an integration of `CKEditor`.
  - The Code/Markdown application in CryptPad is an integration of `CodeMirror`.
  - The Slides application in CryptPad is an integration of `CodeMirror`. CryptPad slides are written in Markdown
  - The Kanban application in CryptPad is based on `JKanban`.
  - The Diagram application in CryptPad is an integration of `Draw.io`.
  - The Whiteboard application in CryptPad is based on `FabricJs`.
  - [What is the relationship between CryptPad and OnlyOffice?](https://docs.cryptpad.org/en/FAQ.html#faq-oointegration)
    - The CryptPad Spreadsheet application is an integration of `OnlyOffice Spreadsheets`.
    - However, this only concerns the client-side code, CryptPad does not make use of the OnlyOffice Document Server.
    - CryptPad's encrypted collaboration, used for spreadsheets and other applications, is completely different from the encryption system used in parts of upstream OnlyOffice.
  - [CryptPad: Collaboration suite end-to-end encrypted and open-source | Hacker News](https://news.ycombinator.com/item?id=29921947)
  - https://github.com/xwiki-labs/office-converters
    - an example of a browser-based document converter using Web Assembly. 
  - https://github.com/xwiki-labs/netflux-spec2

- CollaboraOnline /1kStar/MPLv2/202401/cpp/js/ts/LibreOffice
  - https://github.com/CollaboraOnline/online
  - https://www.collaboraoffice.com/
  - https://www.collaboraonline.com/
  - Collabora Online is a collaborative online office suite based on LibreOffice
  - This is also the source for the Collabora Office apps for iOS and Android.
  - Collaborative editing features
  - [Collabora Office: The enterprise-ready edition of LibreOffice](https://news.ycombinator.com/item?id=26614654)
  - [Based on LibreOffice - Collabora Online and Collabora Office](https://www.collaboraonline.com/based-on-libreoffice/)
    - Our flagship products, Collabora Online and Collabora Office, are 100% Open Source

- https://github.com/LibreOffice/core /3.5kStar/MPLv2/202512/cpp/java
  - [LibreOffice Online](https://www.libreoffice.org/download/libreoffice-online/)
    - LibreOffice Online is a server service built from the main LibreOffice project code, which provides display and collaborative visual editing of a range of document types in a web browser. 
  - [LibreOffice for Android and iOS](https://www.libreoffice.org/download/android-and-ios/)
    - doesn’t currently offer an Android or iOS version of LibreOffice, there is a LibreOffice-based product in app stores from Collabora
  - [LibreOffice Licensing Blurb](https://github.com/LibreOffice/core/tree/master/readlicense_oo)
    - `MPL_SUBSET`: If the variable is defined, then GPL and LGPL license text will not be included, because none of the built-in code need it.

- https://github.com/ProtonMail/WebClients /5.1kStar/GPLv3/202512/ts
  - This project is a monorepo hosting the Proton web clients. It includes the web applications, their dependencies & shared modules as well as all tooling surrounding development of the web clients
  - 依赖lexical实现富文本编辑
  - https://github.com/ProtonMail/WebClients/blob/main/applications/docs-editor/src/app/Containers/Spreadsheet/Spreadsheet.tsx
    - 依赖 @rowsncolumns/toolkit 实现 excel

- https://github.com/zserge/awfice /3.3kStar/MIT/202108/html
  - the world smallest office suite
  - a word processor, a spreadsheet, a drawing app and a presentation maker
  - packaged as data URLs, so you can use them right away, without downloading or installing
  - but they can't store their state, so whatever you type there would be lost on page refresh

- https://gitee.com/wfeng0/mpoe /apache2/202402/js/vue
  - 多人协同编辑器开发 MPOE（Multi person online edit）
  - node采用较强的模块化思想，每个单独的模块都会独立导出 index.js ，因此，node有很多的 index.js，注意区分; 
  - 使用Yjs、Quill、LuckySheet 等技术实现的markdown、txt、excel 等文件的多人在线协同编辑，支持以 websocket、webRTC、组合API等形式实现通信
  - [Luckysheet 实现excel多人在线协同编辑 - 掘金](https://juejin.cn/post/7298170736480485376)
  - [Yjs + Quill 实现文档多人协同编辑器开发（基础+实战） - 掘金 _202309](https://juejin.cn/post/7273432426772070457)
# office-like
- https://github.com/mnt-ltd/moredoc /go
  - moredoc，魔豆文库，基于golang开发的类似百度文库的开源文库系统，dochub文库的重构版本。

- https://github.com/j-berman/hush-docs /MIT/202102/js
  - https://hushdocs.com/
  - offline-first, private Google Docs alternative.
  - using IndexedDB/Dexie.js
  - Docs stay in sync using CRDTs (Automerge)
  - 依赖userbase-js、automerge.v0.14、dexie.v3、jquery、quill、workbox
  - https://github.com/smallbets/userbase /js
    - Userbase is the easiest way to add user accounts and user data persistence to your static site.
    - All Userbase features are accessible through a very simple **JavaScript SDK**, directly from the browser. No backend necessary. 类似Authing
    - 100% open source, MIT licensed. You can host it yourself 
# office-inactive
- https://github.com/Darth-Ness/Ink /202210/js/实现简单
  - https://darth-ness.github.io/Ink/
  - The online, static word processor.

- https://github.com/evergreenx/Wordium-Docs /202310/js
  - https://wordium-docs.vercel.app/
  - a word processor application that provides for input, editing, formatting, and output of text, with some additional features.

- https://github.com/airbornio/airborn /AGPLv3/202105/js
  - https://www.airborn.io/
  - Airborn is a service that lets you create and store documents in the browser using Open Web Apps.
  - used a service worker to guarantee that code loaded into the browser came from the latest GitHub commit.
  - https://github.com/airbornio/airborn-server
  - https://github.com/airbornio/firetext
    - A web-based word processor. 

- https://github.com/Graphite-Docs/graphite /201908/js
  - Encrypted, secure, user-owned productivity suite
  - 依赖slate.v0.47、handsontable.v7
# office-viewer
- https://github.com/cweijan/vscode-office /MIT/202412/js
  - 让VSCode支持预览PDF, Excel和Word等格式, 并增加markdown所见即所得编辑器
  - 支持预览xlsx, docx, svg, pdf, zip等格式, 后来才增加markdown编辑器
  - 依赖docxjs、sheetjs、vditor(md)、pdfjs
  - [Please support PPT/PPTX files _202211](https://github.com/cweijan/vscode-office/issues/166)
    - I have done research on this, but due to the complexity of ppt/pptx, it is impossible to display it in js.

- https://github.com/501351981/vue-office /MIT/202401/js/vue/react
  - https://501351981.github.io/vue-office/examples/docs/
  - 支持word(.docx)、excel(.xlsx)、pdf等各类型office文件预览的vue组件集合，提供一站式office文件预览方案
  - 支持vue2和3，也支持React等非Vue框架
  - 依赖docx-preview、pdfjs、exceljs、x-data-spreadsheet
  - [非Vue框架文件预览 | vue-office](https://501351981.github.io/vue-office/examples/docs/guide/js-preview.html)
    - 为了在非Vue的框架中进行Office文件预览，增加了通过js进行预览的方式。

- https://github.com/zhuye1993/file-view /202203/js/vue/inactive
  - https://zhuye1993.github.io/file-view/dist/index.html
  - [前端实现word、excel、pdf、ppt、mp4、图片、文本等文件的预览 - 掘金 _202203](https://juejin.cn/post/7071598747519549454)
- https://github.com/zgsgs/vitest-starter-plus /202307/ts/vue/inactive
  - Vue 3 + TypeScript + Vite + Vitest + wsm + UnoCSS
  - 依赖vue3、pinia、naive-ui、handsontable.v12、nuxt、@vueuse/nuxt、unocss

- https://github.com/Jarrettluo/all-docs /MIT/202401/js/vue
  - https://jiaruiblog.com/all-docs-page/
  - "All Docs" is a tool that enables online previewing, storage, and sharing of documents such as Word, Excel, PowerPoint, PDF, and images 
  - It supports full-text search for all document information. 
  - 开发了一个用于存储ppt、word、png等文档的，支持私有部属的知识库的检索。
  - 后端技术：SpringBoot + MongoDB + ES
  - https://github.com/Jarrettluo/all-docs-vue
    - 前端技术：Vue + axios

- https://github.com/react-office-viewer/react-office-viewer /MIT/202301/js
  - Temporary support 'pdf, xls, xlsx, docx'.
  - 依赖handsontable.v12, mammoth, xlsx, pdfjs-dist

- https://github.com/kekingcn/kkFileView /9.4kStar/apache2/202312/java
  - https://kkview.cn/
  - 文件文档在线预览解决方案，基本支持主流办公文档的在线预览，如doc, docx, xls, xlsx, ppt, pptx, pdf, txt, zip, rar, 图片, 视频, 音频等等
  - 使用spring boot开发，预览服务搭建部署非常简便
  - 支持普通http/https文件下载url、http/https文件下载流url、ftp下载url等多种预览源
  - 提供Docker镜像发行包，方便在容器环境部署
  - 抽象预览服务接口，方便二次开发，非常方便添加其他类型文件预览支持
  - https://github.com/gaoxingzaq/kkFileView
    - 修改版
- https://github.com/YiJiuSmile/kkFileViewOfficeEdit /201903/java/inactive
  - 文件在线预览及OFFICE(word, excel, ppt)的在线编辑
  - 对kkFileView进行了二次开发，整合了openOffice进来，项目体积更大了！但使用和配置更简单，只需要配置redis即可

- https://github.com/sismics/docs /2.2kStar/GPLv2/202409/java/js/inactive
  - https://teedy.io/
  - open source, lightweight document management system for individuals and businesses.
  - Support image, PDF, ODT, DOCX, PPTX files
  - Video file support
  - Tested to one million documents

- https://github.com/webodf/ViewerJS /agpl/201504/js/inactive
  - https://viewerjs.org/
  - the easiest way to use presentations, spreadsheets, PDF's and other documents on your website or blog without any external dependencies
  - WebODF makes it easy to add Open Document Format (ODF) support to your website and to your mobile or desktop applications. 
  - mozilla pdf.js explores building a faithful and efficient Portable Document Format (PDF) renderer without native code assistance.
- https://github.com/webodf/WebODF /agpl/202002/js/inactive
  - https://webodf.org/
  - WebODF is a JavaScript library that makes it easy to add Open Document Format (ODF) support to your website
  - It uses HTML and CSS to display ODF documents.
  - compiled by using the Closure Compiler.
# google-docs-like
- https://github.com/RivaanRanawat/flutter-google-docs-clone /202209/flutter/cpp
  - Responsive Google Docs Clone Tutorial Source Code developed using Flutter & Nodejs.
  - A completely Responsive Instagram App- Works on Android, iOS & Web!
  - https://github.com/funwithflutter/google-docs-clone-flutter

- https://github.com/benawad/mini-google-docs-clone /201905/ts
  - react, 编辑器无依赖
  - [Mini Google Docs Clone in React](https://www.youtube.com/playlist?list=PLN3n1USn4xllb05dQVmRbVtGP2aM4seVq)

- https://github.com/WebDevSimplified/google-docs-clone /ISC/202104/js
  - 最简单的示例，几乎单文件
  - 依赖quill, react、mongoose、socket.io

- https://github.com/NickMandylas/noogle-docs /202106/ts
  - Google Docs clone built with Typescript, inspired by Web Dev Simplified
  - Front-end: Built with ReactJS (utilising Create React App). The TextEditor used is QuillJS.
  - Back-end: Fastify (with Fastify-WebSockets), PostgreSQL and Redis.

- https://github.com/noahskorner/google-docs-clone /202203/ts
  - Google Docs Clone built in React/Typescript/Express/Postgres.
  - 依赖express、sequelize、socket.io、draft-js

- https://github.com/MartsTech/google-docs-clone /202206/ts
  - Google Docs Clone created with Next. JS, Firebase, Tailwind CSS

- https://github.com/tanwarAalok/google-sheet-clone /202309/js
  - https://google-sheet-clone.netlify.app/
  - A google sheets clone developed using Vanilla Javascript
  - more
  - https://github.com/Prakhar-FF13/GoogleSheetClone /202307
  - https://github.com/Yashkanekar/excel-vanilla-js
  - https://github.com/Raj-Stark/Google-Sheet-2.0
  - https://github.com/noobCode-69/ExcelClone
  - https://github.com/PrinceAttri/sheets-clone

- https://github.com/sujitIwale/sharesheet /202208/js/inactive
  - https://sharesheet.netlify.app/landing
  - Upload and Edit Csv File ( Spreadsheet Clone )

- https://github.com/xem/sheet /public/201710/html/js
  - https://xem.github.io/sheet/
  - A 188b/253b spreadsheet app in HTML/JS
  - supports any value: texts, numbers, floats, and formulae. Ex: "=A1+8"
  - cells update in cascade, circular reference protection
  - localStorage persistence
  - [Tinysheet | Hacker News_202110](https://news.ycombinator.com/item?id=28967514)

- https://github.com/kishanrajput23/The-Excel-Clone /202207/js/inactive
  - https://kishanrajput23.github.io/The-Excel-Clone/
  - a web application clone of Excel, created using HTML, CSS and Javscript entirely.
  - User have access of 100 rows and 26 columns to work on.
  - https://github.com/Ayush2966/Excel-Huh /202305/js
  - https://github.com/IslamShg/excel /202109/js
  - https://github.com/amanksdotdev/excel-clone /202307/js
# EtherCalc/SocialCalc 📈
- https://github.com/otetard/ownpad /AGPLv3/202401/js
  - a Nextcloud application that allows to create and open Etherpad and Ethercalc documents.
  - This application requires to have access to an instance of Etherpad and/or Ethercalc to work properly.
  - Note that the documents are only stored with your Etherpad/Ethercalc service provider; no copy is kept on Nextcloud

- ethercalc /2.9kStar/Artistic/202012/js/inactive
  - https://github.com/audreyt/ethercalc
  - https://ethercalc.net/
  - EtherCalc is a web spreadsheet
  - Node.js port of Multi-user SocialCalc
  - 依赖socialcalc、livescript、xlsx、csv-parse、zappajs(node-fwk)、redis、jquery-ui、jszip
  - Your data is saved on the web, and people can edit the same document at the same time. 
  - [EtherCalc: Open-source web spreadsheet | Hacker News_201408](https://news.ycombinator.com/item?id=8129281)
  - [how to start?](https://github.com/audreyt/ethercalc/issues/524)
  - [redis and persistent data](https://github.com/audreyt/ethercalc/issues/556)
    - Ethercalc loads the entire sheet into memory - and as far as I know it stays in memory until the server side of ethercalc is stopped.
    - Every individual change to the sheet is sent to the server and the server sends it to redis. 
    - Also, from time to time the entire sheet is recalculated on the server and sent to redis.
    - You want a "backup" and "restore" of redis. 
  - [MySQL instead of Redis](https://github.com/audreyt/ethercalc/issues/5)
    - currently we only use Redis. 
  - [Where are my files](https://github.com/audreyt/ethercalc/issues/587)
    - It seems that exporting to CSV/ODS/Excel/HTML is not lossless (export to CSV and HTML will lose formulas; export to ODS/Excel seems to lose colors).
  - 🍴 forks
  - https://github.com/Tuanshu/ethercalc /202312/仅修改测试
    - post to ethercalc ok
  - https://github.com/davidbwaikato/cbh-ethercalc /202111/js
    - Cell Block HTML fork of Ethercal to support rich HTML representation along with text analysis in a spreadsheet
  - https://github.com/feryandi/EtherCalc-Data-Collection /201708
    - 支持mysql, forked from v0.20161220.1
  - https://github.com/doc22940/ethercalc.tools /201911

- https://github.com/eddyparkinson/cellmaster /201611/js
  - forked from ethercalc
  - https://news.ycombinator.com/item?id=19022357
    - It is hard to makes formulas fast enough with JS.
    - The main speed problems with ethercalc are loading the data from the server and calculating the formulas. I did strip down the code to remove these problems to make web apps work.

- https://github.com/ethersheet-collective/EtherSheet /BSD/201704/js
  - Online spreadsheet collaboration in real time using node.js. 
  - Similar to etherpad-lite but its a spreadsheet
  - Ethersheet is only supported on GNU/Linux and MySQL as of right now. It's possible that it will work on Windows or with PostgreSQL or some other database, but we haven't tested 
  - [Ethersheet – An open-source collaborative spreadsheet | Hacker News_201410](https://news.ycombinator.com/item?id=8450234)
    - Like ethercalc, you can use any URL, even non-secret ones
    - It doesn't support drag to enter ranges in formulas
    - Arrow keys don't move the selection
  - 🍴 forks
  - https://github.com/Stackato-Apps/EtherSheet /201604/js
- https://github.com/luigser/Ethersheet2 /201907/js
  - collaborative, realtime open source spreadsheet

- https://github.com/DanBricklin/socialcalc /Artistic/201007/js
  - SocialCalc for Socialtext
  - Dan Bricklin co-authored VisiCalc, the first spreadsheet program for the masses.
  - 🍴 forks
  - https://github.com/marcelklehr/socialcalc /201808/js
    - in-browser spreadsheet editor with support for real-time collaboration
    - 🎯 This version is based on the version used in EtherCalc.
  - https://github.com/seballot/socialcalc /201906/js
    - Adds nunjucks template engine
    - Adds style button directly in editor toolbox
    - Handle editor resize
  - https://github.com/audreyt/socialcalc /201109/js
    - Multiplayer SocialCalc with WebSocket, ethercalc的前期
  - https://github.com/Lynnmn/socialcalc /201903/js
    - 可以进行通用编辑电子表格, 但不与excel互通
    - 可以读取远程文件列表, 载入远程文件
    - 可以保存文件到本地, 从本地载入文件
  - https://github.com/seballot/socialcalc /201906/js
    - Fix cell width when merged cell

- https://github.com/marcelklehr/ot-socialcalc /201611/js
  - Operational transformation for socialcalc commands (shareJS compatible)
  - This is a shareJS-compatible OT type. It defines Operations that relate to socialcalc's spreadsheet commands and can be serialized, applied on a socialcalc snapshot and, of course, transformed against each other.

## examples-ethercalc

- https://github.com/sallakarppinen/ethercalc-client /201804/js
  - simple API client for Ethercalc collaborative spreadsheets.

- https://github.com/hivejs/hive-editor-spreadsheet-socialcalc /201605/js
  - This is an editor package bringing Ethercalc's SocialCalc to hive.js.
  - https://github.com/hivejs/hive /GPLv3/201608/js
    - https://github.com/hivejs/hive-core /GPLv2
    - http://hivejs.org/
    - Hive.js is a real-time collaboration platform. 
    - It supports multiple document types and editors, features unopinionated authentication and authorization
  - https://github.com/hivejs/hive-editor-text-codemirror
  - https://github.com/hivejs/hive-editor-html-ckeditor
  - https://github.com/hivejs/hive-editor-text-textarea
  - https://github.com/hivejs/hive-editor-richtext-quill
  - https://github.com/hivejs/hive-plugin-presence

- https://github.com/SheetJS/js-harb /201712/js
  - Plaintext spreadsheet (DIF / CSV / TSV / DBF / SocialCalc) parser
  - this has been merged into js-xlsx
  - 🍴 forks
  - https://github.com/quilt-js/js-harb
    - forked from tokyootakumode/js-harb
  - https://github.com/tokyootakumode/js-harb
    - Designed to provide support for j. Pure-JS cleanroom implementation.

- https://github.com/cestastanford/grandtour /apache2/202401/js
  - [The Grand Tour Project](https://grandtour.stanford.edu/)
  - This is the codebase for the Grand Tour Explorer web project.
  - 依赖angular.v7、angular-ui、ckeditor.v4、d3.v3、ejs、mongoose、mongoose

- https://github.com/selvan/calc-engine /201704/js
  - Virtual calc/excel engine that runs in mobile (React native), web browser(Javascript) and server (Nodejs)
  - 示例代码没找到
  - https://github.com/selvan/wordprocessor-engine /201702/js
    - Virtual wordprocessor engine 
  - https://github.com/selvan/calendar-engine /201807/js
    - Create custom calendars
# utils
- https://github.com/OfficeDev/script-lab /MIT/202311/ts
  - https://script-lab.azureedge.net/
  - Create, run and share your code directly from Office
  - Experiment with the Office JavaScript API without ever leaving Excel, Outlook, Word, or PowerPoint
# office-solutions
- https://github.com/documenso/documenso /AGPLv3/ts
  - https://documenso.com/
  - Signing documents digitally is fast, easy and should be best practice for every document signed worldwide. 
  - This is technically quite easy today, but it also introduces a new party to every signature: The signing tool providers. 
  - Documenso aims to be the world's most trusted document signing tool. 

- https://github.com/docusealco/docuseal /AGPLv3/202402/ts
  - https://www.docuseal.co/
  - Open source DocuSign alternative. Create, fill, and sign digital documents

- https://github.com/PDFTron/pdftron-sign-app /paid/202305/js
  - Sign and request signatures on PDFs, MS Office documents
  - demonstrates building a signing application where users can request signatures on the documents by placing fields, sign documents, review signed documents using PDFTron PDF SDK.

- https://github.com/RKQF-JVS/jvs-knowledge-ui /apache2/202207/java/js/vue/inactive
  - https://gitee.com/software-minister/jvs-knowledge-ui
  - http://knowledge.bctools.cn/
  - 无忧·企业文档=企业级知识库+在线编辑工具集+企业搜索引擎+内容展示平台
  - 【企业级在线文档】，解决企业内部文档编辑、知识沉淀、知识协同等痛点。
  - 项目主要采用Java开发，基础框架采用JVS（spring cloud+Vue）。
  - 支持私有化部署场景。
  - [开源版和商业版有什么区别？ ](https://gitee.com/software-minister/jvs-knowledge-ui/issues/I839LC)
    - 无回答

- https://github.com/phpk/godoos /AGPL/202502/go
  - https://gitee.com/godoos/godoos
  - https://godoos.com/
  - 一款高效的内网办公操作系统，内含word/excel/ppt/pdf/聊天/白板/思维导图等多个办公系统工具，支持AI创作/知识库和原生文件存储。
  - 内网聊天: 无需注册流程，只需在同一内网，即可自动发现并列出所有可用的聊天对象
  - 客户端为开源版，用户所有数据存储到服务端
  - 服务端支持windows/linux和docker安装，安装端支持web端
  - 无需联网使用，全开源
  - 支持多平台，Windows、Linux、MacOS
  - 允许企业/个人单独使用，但需保留版权信息, 如用于商业活动或二次开发后发售，请购买相关版权

- https://gitee.com/umodoc/editor /MIT/202503/ts
  - https://editor.umodoc.com/cn/docs
  - Umo Editor 是一个基于 Vue3 适合于国人使用的本土化开源文档编辑器。
# protocol/sync/WOPI
- https://github.com/mikeebowen/node-wopi-server /MIT/202310/ts
  - A WOPI Server written with Node.js
  - This is a sample implementation of the WOPI Protocol written with in TypeScript with Node.js.
  - This is not a complete implementation, but is meant to be a example
  - This server can be validated with the WOPI Validator Core or will work as a live WOPI Server if the computer running the WOPI Server is part of an active directory domain with a server running Office Online Server.

- https://github.com/coatsy/wopi-node /MIT/201706/ts
  - Sample WOPI Host implementation in node.js
  - This repository contains an application that integrates with Office Online for viewing/editing Office documents.

- https://github.com/cs3org/wopiserver /apache2/202401/python
  - vendor-neutral application gateway compatible with the WOPI specifications
  - This service is part of the ScienceMesh Interoperability Platform (IOP) and implements a vendor-neutral application gateway compatible with the Web-application Open Platform Interface (WOPI) specifications.
  - It enables ScienceMesh EFSS storages to integrate Office Online platforms including Microsoft Office Online and Collabora Online.
# more-office
- [常见附件预览：图片、视频、音频、文本、pdf、office...](https://rapidsu.cn/articles/2745)
