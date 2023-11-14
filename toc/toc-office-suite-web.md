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
# office-popular
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
- https://github.com/ibisheng/onlyoffice-ibisheng /201911/js
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

- cryptpad /4.3kStar/AGPLv3/202301/js
  - https://github.com/xwiki-labs/cryptpad
  - https://cryptpad.org/
  - CryptPad is a collaboration suite that is end-to-end-encrypted and open-source.
  - 依赖 onlyoffice、netflux-websocket
  - It is built to enable collaboration, synchronizing changes to documents in real time. 
  - Because all data is encrypted, the service and its administrators have no way of seeing the content being edited and stored.
  - https://github.com/xwiki-labs/netflux-spec2
  - The Rich Text application in CryptPad is an integration of `CKEditor`.
  - The Code/Markdown application in CryptPad is an integration of `CodeMirror`.
  - The Slides application in CryptPad is an integration of `CodeMirror`.
  - The Kanban application in CryptPad is based on `JKanban`.
  - The Whiteboard application in CryptPad is based on `FabricJs`.
  - [What is the relationship between CryptPad and OnlyOffice?](https://docs.cryptpad.org/en/FAQ.html#faq-oointegration)
    - The CryptPad Spreadsheet application is an integration of `OnlyOffice Spreadsheets`.
    - However, this only concerns the client-side code, CryptPad does not make use of the OnlyOffice Document Server.
    - CryptPad's encrypted collaboration, used for spreadsheets and other applications, is completely different from the encryption system used in parts of upstream OnlyOffice.
  - [CryptPad: Collaboration suite end-to-end encrypted and open-source | Hacker News](https://news.ycombinator.com/item?id=29921947)
  - https://github.com/xwiki-labs/office-converters
    - an example of a browser-based document converter using Web Assembly. 

- https://github.com/LibreOffice/core /GPLv3/cpp/java
  - [LibreOffice Online](https://www.libreoffice.org/download/libreoffice-online/)
    - LibreOffice Online is a server service built from the main LibreOffice project code, which provides display and collaborative visual editing of a range of document types in a web browser. 
  - [LibreOffice for Android and iOS](https://www.libreoffice.org/download/android-and-ios/)
    - doesn’t currently offer an Android or iOS version of LibreOffice, there is a LibreOffice-based product in app stores from Collabora

- https://github.com/CollaboraOnline/online /1kStar/MPLv2/LibreOffice
  - https://www.collaboraoffice.com/
  - Collabora Online is a collaborative online office suite based on LibreOffice
  - This is also the source for the Collabora Office apps for iOS and Android.
  - Collaborative editing features
  - [Collabora Office: The enterprise-ready edition of LibreOffice](https://news.ycombinator.com/item?id=26614654)

- https://github.com/zserge/awfice /3.3kStar/MIT/202108/html
  - the world smallest office suite
  - a word processor, a spreadsheet, a drawing app and a presentation maker
  - packaged as data URLs, so you can use them right away, without downloading or installing
  - but they can't store their state, so whatever you type there would be lost on page refresh
# office-like
- https://github.com/mnt-ltd/moredoc /go
  - moredoc，魔豆文库，基于golang开发的类似百度文库的开源文库系统，dochub文库的重构版本。

- https://github.com/j-berman/hush-docs
  - https://hushdocs.com/
  - offline-first, private Google Docs alternative.
  - using IndexedDB/Dexie.js
  - Docs stay in sync using CRDTs (Automerge)
  - 依赖userbase-js
  - https://github.com/smallbets/userbase /js
    - Userbase is the easiest way to add user accounts and user data persistence to your static site.
    - All Userbase features are accessible through a very simple **JavaScript SDK**, directly from the browser. No backend necessary. 类似Authing
    - 100% open source, MIT licensed. You can host it yourself 
# office-inactive
- https://github.com/airbornio/airborn /AGPLv3/202105/js
  - https://www.airborn.io/
  - Airborn is a service that lets you create and store documents in the browser using Open Web Apps.
  - used a service worker to guarantee that code loaded into the browser came from the latest GitHub commit.
  - https://github.com/airbornio/airborn-server
  - https://github.com/airbornio/firetext
    - A web-based word processor. 

- https://github.com/Graphite-Docs/graphite /js
  - Encrypted, secure, user-owned productivity suite
# office-viewer
- https://github.com/webodf/ViewerJS /agpl/js/inactive
  - https://viewerjs.org/
  - the easiest way to use presentations, spreadsheets, PDF's and other documents on your website or blog without any external dependencies
  - WebODF makes it easy to add Open Document Format (ODF) support to your website and to your mobile or desktop applications. 
  - mozilla pdf.js explores building a faithful and efficient Portable Document Format (PDF) renderer without native code assistance.
- https://github.com/webodf/WebODF /agpl/202002/js/inactive
  - https://webodf.org/
  - WebODF is a JavaScript library that makes it easy to add Open Document Format (ODF) support to your website
  - It uses HTML and CSS to display ODF documents.
  - compiled by using the Closure Compiler.
# more-office
