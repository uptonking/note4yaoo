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
# office
- https://github.com/ONLYOFFICE/DocumentServer
  - Starting from version 6.0, Document Server is distributed under a new name - ONLYOFFICE Docs.
  - https://github.com/ONLYOFFICE/CommunityServer /c#/apache2
    - open source office suite with business productivity tools: document and project management, CRM, mail aggregator.
  - https://github.com/ONLYOFFICE/sdkjs /AGPLv3/js
    - https://github.com/ONLYOFFICE/document-editor-react-samples
    - https://github.com/ONLYOFFICE/document-editor-react
    - JavaScript SDK which is a part of ONLYOFFICE Document Server and ONLYOFFICE Desktop Editors. 
    - Contains API for all the included components client-side interaction.
  - https://github.com/ONLYOFFICE/server
    - backend server software layer which is the part of ONLYOFFICE Document Server and ONLYOFFICE Desktop Editors and is the base for all other components.
  - https://github.com/ONLYOFFICE/core /cpp
    - Server core components which are a part of ONLYOFFICE Document Server
  - https://github.com/ONLYOFFICE/sdkjs
    - Contains API for all the included components client-side interaction.

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

- https://github.com/LibreOffice/core /GPLv3/java
  - [LibreOffice Online](https://www.libreoffice.org/download/libreoffice-online/)
    - LibreOffice Online is a server service built from the main LibreOffice project code, which provides display and collaborative visual editing of a range of document types in a web browser. 
  - [LibreOffice for Android and iOS](https://www.libreoffice.org/download/android-and-ios/)
    - doesn’t currently offer an Android or iOS version of LibreOffice, there is a LibreOffice-based product in app stores from Collabora

- https://github.com/CollaboraOnline/online /MPLv2/LibreOffice
  - https://www.collaboraoffice.com/
  - Collabora Online is a collaborative online office suite based on LibreOffice
  - This is also the source for the Collabora Office apps for iOS and Android.
  - Collaborative editing features
  - [Collabora Office: The enterprise-ready edition of LibreOffice](https://news.ycombinator.com/item?id=26614654)
# office-like
- https://github.com/mnt-ltd/moredoc /go
  - moredoc，魔豆文库，基于golang开发的类似百度文库的开源文库系统，dochub文库的重构版本。

- https://github.com/j-berman/hush-docs
  - https://hushdocs.com/
  - offline-first, private Google Docs alternative.
  - using IndexedDB/Dexie.js
  - Docs stay in sync using CRDTs (Automerge)
  - 依赖userbase-js
  - https://github.com/smallbets/userbase
    - Userbase is the easiest way to add user accounts and user data persistence to your static site.
    - All Userbase features are accessible through a very simple JavaScript SDK, directly from the browser. No backend necessary.
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
# more-office
