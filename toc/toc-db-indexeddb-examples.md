---
title: toc-db-indexeddb-examples
tags: [examples, indexeddb]
created: 2022-06-03T22:06:28.976Z
modified: 2022-06-03T22:06:47.464Z
---

# toc-db-indexeddb-examples

# guide

- 放弃使用浏览器扩展的形式来实现离线
  - indexeddb的访问存在same-origin的限制，不应该维护两套数据
  - pwa支持离线使用，使用webview打包也简单
# popular
- https://github.com/HiWayne/large-file-uploader
  - 专为上传功能而优化，file uploader, supporting file segmentation, resume from break point, offline storage...
  - 断点续传，不必重头再来
  - 基于 indexedDB 的文件缓存，离线也能恢复进度
  - 多线程计算，面对大文件处理更快
  - 只提供下载队列的状态数据，你可以自由定制 UI
  - 丰富的配置，你可以限制文件类型、每个切片大小、线程数、请求并发数、是否开启离线缓存等

- https://github.com/DeepBlueCLtd/RCO /ts/纯前端
  - https://deepbluecltd.github.io/RCO/
  - Secure asset register
  - 依赖ra-data-local-forage、mitt、react-admin.v4、mui5
  - indexeddb保存扁平化数据

- https://github.com/rpecuch/text-editor /js
  - The purpose of this project was to build a single-page application that meets Progressive Web Application criteria. 
  - 后端只依赖express
  - 前端依赖codemirror5、idb、workbox

- https://github.com/mWater/offline-leaflet-map
  - Offline maps in Leaflet using IndexedDb to store tiles
- https://github.com/yagajs/indexed-db-tile-cache /inactive
  - Spatial tile cache that saves its data into the IndexedDB of your browser

- https://github.com/nareshbhusal/roadmap
  - A kanban board, project and idea management app built with React and IndexedDB.
  - 依赖TailwindCSS、Chakra-ui、dexie、dnd-kit
- https://github.com/eyalzh/simple-kanban
  - A lightweight offline kanban board
  - Completely offline (IndexedDB backend)
  - JSON import/export
- https://github.com/roottool/skeban
  - Skeban is an open source Electron based kanban app. It is written in TypeScript and uses React.

- https://github.com/kevinbgreene/indeksd
  - A DSL for defining IndexedDB schemas.
  - Generate a type-safe IndexedDB client from a simple schema file.
  - https://github.com/kevinbgreene/indeksd-example
    - Example app for using indeksd IndexedDB code generation
# crud-api
- https://github.com/simplifyjs/indexeddb-crud
  - Comparison between native IndexedDB API and using IDB library in operating CRUD workaround

- https://github.com/chenstarx/GoDB.js
  - indexedDB with Intuitive API, CRUD with one line of code.

- https://github.com/ismaelcallerojas/CRUD-indexeddb
  - CRUD con la api indexed db 单文件使用示例
# react-vue
- https://github.com/assuncaocharles/react-indexed-db
  - wraps IndexedDB database in an Declarative way. 
  - It exposes very simple promises API to enable the usage of IndexedDB 

- https://github.com/bernabe9/redux-react-session
  - Simple Session API storage for Redux and React

- https://github.com/hc-oss/use-indexeddb
  - hook w/ promises for easy IndexedDB access in React

- https://github.com/eldomagan/vuex-orm-localforage
  - VuexORMLocalforage is a plugin for the amazing VuexORM that let you sync your Vuex Store with an IndexedDB database using LocalForage.
# browser-extension
- getsetfetch-extension /202108/ts/inactive
  - https://github.com/get-set-fetch/extension
  - https://getsetfetch.org/extension/getting-started.html
  - open source web scraper available as a cross-browser (chrome, firefox, edge) extension with csv and zip export capabilities.
  - parses pages and stores relevant data in the builtin browser database (IndexedDB)
  - Binary data (images, pdf files, …) can be exported as zip archives. Text based data can be exported as csv files.

- https://github.com/MVMS1994/idb-utils
  - A chrome extension to import/export indexed db.

- https://github.com/darx/IndexedDBEdit
  - Devtools panel for changing IndexedDB key values
  - 基于svelte+js
# apps
- https://github.com/alexeagleson/template-indexeddb
  - A simple template for getting started with IndexedDB
  - IndexedDB is known to be quite fast on inserting reasonably large quantities of data on a single transaction, but can slow down significantly when these inserts/updates are made across multiple transactions.
  - ensure you are developing your application to batch data modifications into as few transactions as possible.

- https://github.com/wizexplorer/excel-clone /202210/js
  - An excel clone using HTML-CSS-JavaScript. Change properties of different cells. 
  - Capable of applying formulas, copying/cutting/pasting multiple cells. 

- graph /7Star/MIT/202210/ts
  - https://github.com/graphcentral/graph
  - https://graphcentral.github.io/graph
  - Performant graph visualization on the web with WebGL + Webworkers + IndexedDB
  - You can visualize Notion pages on force layout graph using this library

- https://github.com/crossjs/cofe
  - No-Code System
  - core依赖unist-builder

- https://github.com/AlisherKonratbaev/Shop
  - https://shop-ruddy.vercel.app/index.html
  - An example of an electronic store with the functionality of authorizing registration, adding, deleting, changing products, placing orders from the basket. 
  - Implemented patterns as "Singleton", "Observer". 
  - The data is stored in indexedDB.

- https://github.com/BaseMax/MyPhonebook
  - https://basemax.github.io/MyPhonebook/src/
  - show how to use IndexedDB internal browser database with dexie
  - MyPhonebook is a web-based phone book page with ability to add contacts and search betweens with internal browser database supporting (IndexedDB full cache), styled powered by TailwindCSS.

- https://github.com/SimonPe25/Apple-Note
  - React v18.0, React Router v6, React Context, react Hooks, Ant Design, Sass, BEM, IndexedDB, Markdown
- https://github.com/familyfriendlymikey/JILU
  - free note taking app for psychopaths hosted on Github Pages which directly addresses the problem of realtime organization by combining folder pathing, search, and highly optimized workflows
  - entirely local to your device: No server, no remote database, no accounts, no tracking

- https://github.com/periodo/periodo-client
  - https://client.perio.do/
  - A Web browser application for browsing and editing PeriodO data.
  - Because browsers do not support IndexedDB for pages served from local file systems, during development, you will need to run a process that will serve the root directory over HTTP.

- https://github.com/brookslybrand/react-indexeddb-example
  - Example of using the Indexed API to persist changes to a simple form in React with dexie.js

- https://github.com/pamelac21/Budget-Tracker
  - NoSQL - MongoDB - A budget tracker with offline functionality
- https://github.com/avaarm/Budget-Tracker
  - Budget Tracker is a progressive web application that allows the user to add and subtract funds online and offline.
- https://github.com/jorgeabrahan/budgtcalc
  - (Responsive) (CRUD) (IndexedDB) budget calculator developed using vanilla JS and storing data on IndexedDB

- https://github.com/googlecodelabs/workbox-indexeddb /202012/js/inactive
  - use IndexedDB and Workbox to create a fully offline-capable, data-driven app. 
  - You'll also use Background Sync to sync your app with the server even when your web app is closed.
  - Follow the Google Codelabs instructions.
# more-indexeddb
- https://github.com/yued-fe/yux-storage
  - yux-storage 是一个基于 HTML5 IndexedDB 封装的 Web 本地数据离线存储库。

- https://github.com/Jeremy664K/crud-drag-drop
  - App that contains the indexedDB API and Drag-And-Drop API.

- https://github.com/BinaryBitBytes/JustAnotherTextEditor
  - A progressive web application that utilizes IndexedDB API to log text in a database

- https://github.com/coderbennett/text-editor
  - https://joeys-text-editor.herokuapp.com/
  - This is a single-page text editor which stores data to an IndexedDB database. 
  - This application features multiple data persistence techniques in case one of the options aren't supported by the browser. 
  - This application also functions offline when installed.
- https://github.com/siennameow/text-editor
  - https://dreamcatcher-texteditor.herokuapp.com/
    - created as a simple text editor app that can function both online and offline

- https://github.com/corskaya/browser-storages-app
  - An app to manage data in IndexedDB, Cookies, Local and Session Storages

- https://github.com/web2solutions/voodux
  - VooduX - "with bateries included" agnostic scalable "M" layer for React, Vue, ExtJS, DHTMLX

- https://github.com/6fa/AccountBook
  - 一个用原生js+webpack+indexedDB写的记账本应用

- https://github.com/alufers/hn-offline
  - An offline-first client for hackernews that even fetches the article contents for reading on the go.

- https://github.com/HondryTravis/TinyDB
  - easy to use multi-table indexedDB lib

- https://github.com/Hacker233/IndexedDB
  - 前端本地存储数据库IndexedDB完整教程，仅文字

- https://github.com/Banana021s/music-player
  - a nice theme music playeryum with indexedDB

- https://github.com/gotpop/gotpop
  - A component based portfolio application build with React, Redux and CSS Grid layout.
