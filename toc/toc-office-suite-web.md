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

- resources
  - [List of office suites - Wikipedia](https://en.wikipedia.org/wiki/List_of_office_suites)
  - [精读《WOPI协议》 - 掘金](https://juejin.cn/post/7105322391597187103)
    - WOPI是微软基于REST API的协议，定义了一组Http操作，使客户端能够访问和改变服务器存储的文件。
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

- cryptpad /4.3kStar/AGPLv3/202301/js/onlyoffice
  - https://github.com/cryptpad/cryptpad
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

- CollaboraOnline /1kStar/MPLv2/202401/js/cpp/LibreOffice
  - https://github.com/CollaboraOnline/online
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
# office-viewer
- https://github.com/cweijan/vscode-office /MIT/202401/js
  - 让VSCode支持预览PDF, Excel和Word等格式, 并增加markdown所见即所得编辑器
  - 支持预览xlsx, docx, svg, pdf, zip等格式, 后来才增加markdown编辑器
  - 该扩展在vscode内集成Vditor

- https://github.com/501351981/vue-office /MIT/202401/js/vue
  - https://501351981.github.io/vue-office/examples/docs/
  - 支持word(.docx)、excel(.xlsx)、pdf等各类型office文件预览的vue组件集合，提供一站式office文件预览方案
  - 支持vue2和3，也支持React等非Vue框架
  - 依赖docx-preview、pdfjs、exceljs、x-data-spreadsheet
  - [非Vue框架文件预览 | vue-office](https://501351981.github.io/vue-office/examples/docs/guide/js-preview.html)
    - 为了在非Vue的框架中进行Office文件预览，增加了通过js进行预览的方式。

- https://github.com/react-office-viewer/react-office-viewer /MIT/202301/js
  - Temporary support 'pdf, xls, xlsx, docx'.
  - 依赖handsontable, mammoth, xlsx, pdfjs-dist

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

- https://github.com/MartsTech/google-docs-clone /202206/ts
  - Google Docs Clone created with Next. JS, Firebase, Tailwind CSS
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

- https://github.com/docusealco/docuseal /AGPLv3/ts
  - https://www.docuseal.co/
  - Open source DocuSign alternative. Create, fill, and sign digital documents

- https://github.com/PDFTron/pdftron-sign-app /paid/202305/js
  - Sign and request signatures on PDFs, MS Office documents
  - demonstrates building a signing application where users can request signatures on the documents by placing fields, sign documents, review signed documents using PDFTron PDF SDK.
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
