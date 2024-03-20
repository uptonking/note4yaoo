---
title: lib-collab-ot-examples
tags: [collaboration, examples, ot]
created: 2022-10-02T20:50:54.901Z
modified: 2022-10-02T20:51:30.444Z
---

# lib-collab-ot-examples

# guide

- ot-tips
  - 经典的冲突处理算法，需要central server处理冲突
  - 可不参考冲突处理的逻辑，只参考op的存储和同步

- [am-editor 协同编辑配置](https://editor.aomao.com/zh-CN/config/ot)
  - 编辑器基于 sharedb 与 json0 协议交互协作操作数据
  - 客户端（编辑器）通过 WebSocket 与服务端建立长连接通信，编辑器每次的 dom 结构变更都将转换为json0格式操作命令（ops）发送到服务端并修改服务端数据后再分发给各个客户端
  - sharedb 会把每次客户端与服务端的操作数据保存为日志，并且在每次操作后都会把最新生成的文档数据保留下来。这些操作都在 ot-server 中进行
# popular
- https://github.com/typewriter-editor/json-patch
  - Immutable JSON Patch implementation based on RFC 6902 which adds operational transformation (OT) and last-writer-wins (LWW) support for syncing between client and server. 
  - Does not support the full OT algorithm because `copy` and `move` operations cannot be transformed correctly in all cases, so operations must always be applied in correct order. 
    - This means a central server is required to determine order.
  - 👉🏻 json-patch provides a utility that will help sync an object field-by-field using the Last-Writer-Wins (LWW) algorithm. 
    - This sync method is not as robust as operational transformation, but it only stores a little data in addition to the object and is much simpler
    - It does not handle adding/removing array items, though entire arrays can be set. 
    - It should work great for documents that don't need merging text like Figma

- https://github.com/Palindrom/Palindrom
  - Library for two-way data binding between local and remote JSON models. 
  - It uses JSON-Patch for data updates and Operational Transformation for versioning and data consistency. 
  - It operates via HTTP or WebSocket or both.

- https://github.com/ygs-code/ot-system
  - https://github.com/ygs-code/ot-system-server
    - 服务端用了 node koa，webpack， graphql， mysql，redis.
    - graphql有他的一定优势，就是减少了前后联调对接沟通，对于过滤一些非法请求，也可以说是提高了一些安全性问题，因为http请求他需要先经过graphql验证通过之后才会做业务查询。
  - https://github.com/ygs-code/ot-system-client
    - c 端客户端 我是用我自己写的一个 React Ssr框架写的
    - 系统需要支持SSR和CSR我其他微服务不好实现，所以选择了webpack 构建微服务。当然比较麻烦的是路由同构，我并没有使用react官方推选的路由库，而是我自己实现了一个react 路由
    - 基于了@rematch/core 和redux和react-redux，封装了一下
  - https://github.com/ygs-code/ot-system-admin
    - B端后台管理系统大体的构架目录和使用的技术基本和客户端一样
    - 只不过 admin 使用的是antd ui，而c端使用的是谷歌的ui。
  - 开源ot协同系统是由 姚观寿 业余时间打造的一个开源项目
  - 企业级别文档服务，socket实时通信，增量局部文档改动等功能，支持大数据，高并发，集群等部署
  - 该项目可拓展性高，具留有redis 和 mysql相关拓展接口。
  - https://github.com/ygs-code/operational-transformation
    - 算法源码分析
  - https://github.com/ygs-code/sharedb-textarea-example
    - ShareDB with textarea 源码分析

- https://github.com/Webstrates/Webstrates /apache2/202210/js/inactive
  - 💡✨ a research prototype enabling collaborative editing of websites through DOM manipulations.
  - With Webstrates, webpages become collaboratively editable in real-time. 
  - Changes to the Document Object Model (DOM) of a page persist and are synchronised to all connected clients of the same page using Operational Transformation through ShareDB.
  - https://github.com/Webstrates/Codestrates-v2 /apache2/202402/js
    - Codestrates builds on Webstrates. 
    - A web-page served from a Webstrates server is called a webstrate, and is a web-page where changes to the document object model (DOM) are persisted to the server and synchronized with other clients of the same page.

- https://github.com/Progyan1997/Operational-Transformation
  - http://operational-transformation.github.io/
  - A collection of Algorithms to Synchronise changes across multiple clients using Operational Transformation

- https://github.com/3mcd/p2p-edit /js/201606/inactive
  - collaborative text editor powered by WebRTC and OT
  - Local operations to the document are reconciled by remote clients by use of a data structure called text-tp2.
  - https://github.com/ottypes/text-tp2
    - an implementation of OT for text which implements transform property 2 through the use of tombstones.
    - this data structure can be used in peer-to-peer situations

- https://github.com/ryankaplan/pattern-based-ot /201601/ts
  - A server/client for the Pattern-Based Operational Transform algorithm
# sharedb
- sharedb /5.9kStar/MIT/202402/js/代码少
  - https://github.com/share/sharedb
  - ShareDB is a realtime database backend based on Operational Transformation (OT) of JSON documents. 
  - It is the realtime backend for the DerbyJS web application framework.
  - 依赖json0
  - [Remove JSON0 Dependency for Client](https://github.com/share/sharedb/issues/548)
  - [List of User/Supporters](https://github.com/share/sharedb/issues/182)
  - https://github.com/derbyjs/derby
    - MVC framework making it easy to write realtime, collaborative applications that run in both Node.js and browsers
  - https://github.com/vizhub-core/sharedb-client-browser
    - A distribution of the ShareDB client suitable for use in Vite, Rollup and other build tools that do not have built-in support for CommonJS

- https://github.com/derbyjs/racer /1.2kStar/MIT/202306/js/inactive
  - Realtime model synchronization engine for Node.js
  - By leveraging ShareDB, multiple users can interact with the same data in realtime via Operational Transformation
  - ShareDB also supports PubSub across multiple servers for horizontal scaling. 
  - different clients can be subscribed to different overlapping sets of data

- https://github.com/startupjs/startupjs /MIT/202403/js
  - https://startupjs-ui.dev.dmapper.co/
  - Universal React Native + Web framework with isomorphic collaborative DB and observables.
  - 前端依赖react-native-web
  - 后端依赖express、mongoose、sharedb
  - Collaborative Database: MongoDB which runs behind ShareDB and a client-server observable ORM
  - Observer pattern: When you subscribe to a channel, you are being added to the list of subscribers who then will be notified about new
  - react-native-web for the Web-frontend
  - React Native for the Native-frontend (iOS, Android, etc.)
  - Model based on `Racer` with an ability to create custom ORM methods.
  - Redis for the pub/sub (required by ShareDB) and locking functionality.

  
- https://github.com/goodow/realtime-store /201503/java
  - Google Docs–style collaboration via the use of operational transforms
  - Credits: sharedb for implementation and documents of database api.

- https://github.com/stanographer/u-backend /202008/js/inactive
  - CMS for real-time captioning and transcriptions
  - allows real-time captioners to share their transcription feed to remote participants or to send their feed of live-produced text to any device with an Internet connection.

- https://github.com/source-academy/sharedb-ace-backend /apache2/202212/js/单文件/inactive
  - Backend of collaborative editor (ShareDB, Koa)
  - https://github.com/source-academy/sharedb-ace /202008/js
    - Sharedb-ace provides two-way bindings between ShareDB and Ace Editor.

## sharedb-examples

- https://github.com/ahemaid/OntoEditor /MIT/202312/js
  - Online Collaborative Ontology Editor, built on Distributed Version Control Systems. 
  - It aims to support collaborative ontology development across different RDF serialization formats: Turtle, JSON-LD, and RDF/XML.
  - 依赖codemirror5、ot-text、sharedb-mongo、websocket-json-stream

- https://github.com/with-labs/popspace /GPLv2/202311/ts/inactive
  - open source virtual canvas platform for chatting, collaborating, and playing.
  - rich-text editor example based on Quill and ShareDB

- https://github.com/LSX-s-Software/PaperPilotApp /MIT/202312/swift
  - 基于 SwiftUI 的多平台多人协作文献管理软件
  - 实时同步富文本笔记、论文批注
  - 在 Mac、iPad、Apple Vision Pro 等设备上查看文献
  - 100% 原生，不含任何网页、JavaScript 等代码
# ot-rewrite
- https://github.com/Operational-Transformation/ot.js /js
  - http://operational-transformation.github.io/
  - Visualization of OT with a central server
  - Requires CodeMirror >= 4.0
  - [Operational Transformation in JavaScript](http://operational-transformation.boltdoggy.com/ot-for-javascript.html)
- ref
  - https://github.com/Xing-Chuan/ot.js-demo /202009
    - 服务端只是传递操作的话，不能满足协同编辑的文档一致性，服务端还要保证推送出去的操作正确
  - https://github.com/DonaldY/ot.js-demo /202109
    - [ot.js demo解析，仅服务端](https://juejin.cn/post/7027113667107749918)

- https://github.com/YingshanDeng/SharedPen  /js
  - 包含了otjs源码和针对SharedPen的修改版，转换成了es6 class版
  - 关于扩展 ot.js 支持富文本属性，可以参考文件 TextAction.js 和 TextOperation.js
  - A (web-based) rich-text real-time collaborative editor using CodeMirror and ot.js
  - [SharedPen 之 Operational Transformation](http://objcer.com/2018/03/05/SharePen-Operational-Transformation/)
  - https://github.com/YingshanDeng/ot.js-demo

- https://github.com/srtucker22/text-operation /ts
  - 复用了大部分ot.js的TextOperation类，扩展并支持在operation上添加属性，是否支持富文本❓
  - Classes for Rich Text Operations using Operational Transformation
  - This package is heavily based on firepad's OT operations, which were in turn based on ot.js. 
  - This package is a conversion of their masterful work into Typescript + ES6

- https://github.com/abucraft/operational-transform
  - https://abucraft.github.io/operational-transform/
  - 效果和ot.js相同，但ts重写了，仅前端展示无需服务端

- https://github.com/GarinZ/collaborative-textarea
  - 支持协作编辑的文本框
  - 依赖 reduxjs/toolkit、diff-match-patch
  - 引入了ot.js源码
  - A text area supporting real-time collaborative editing plain text. And display all the online attendees.
  - [如何实现协同编辑 - 理解Operational Transformation](https://garinzhang.com/coding/how-to-implemente-collaborative-editing-understanding-operational-transformation.html)
  - https://github.com/GarinZ/Blog/issues/1

- https://github.com/cricklet/operational-transform-demo /201702
  - https://cricklet.github.io/sites/blue/index.html
  - 包含服务端代码
  - an implementation/demo of collaborative text editing via operational transforms.

- https://github.com/substance/operator /201402
  - Operational Transformation for strings, arrays and objects.

- https://github.com/JoshData/jot
  - This module implements operational transformation (OT) on a JSON data model, written in JavaScript for use either in node.js or browsers.
  - Similar work: ShareDB, ottypes/json0, Apache Wave

- https://github.com/ottypes/text-unicode /ts
  - This OT type can be used to edit plaintext documents, like sourcecode or markdown. 
  - text-unicode counts positions based on the number of unicode codepoints instead of javascript string length (UCS2 2-byte offsets). 
- https://github.com/ottypes/text  /js
  - This OT type can be used to edit plaintext documents, like sourcecode or markdown.
  - This OT type counts characters using UTF16 offsets instead of unicode codepoints. 
  - This is slightly faster in javascript, but its incompatible with ot implementations in other languages. 

- https://github.com/ottypes/json1 /ts
  - JSON1 implements a superset of JSON0's functionality.
  - an operational transformation type for arbitrary JSON trees. It supports concurrently editing arbitrarily complex nested structures.
  - Support for arbitrarily moving objects in the JSON tree. 
  - [ot-json1 <-> JSON Patch (RFC 6902)](https://github.com/ottypes/json1/issues/29)
    - a share of a utility I made to convert between json1 ops and JSON patch ops
    - [ot-json1-patch-utils.js](https://gist.github.com/adorsk/67a27968aeb9cc534057c424ee39e63e)
  - Supports embedded subtypes, like embedding rich text documents using quilljs or something inside your JSON tree
  - can be configured to reject operations which would result in lost data.
  - JSON0 and JSON1 use different embedded string types. 
    - JSON1 uses text-unicode which uses proper unicode offsets. 
    - JSON0 uses the older text type which uses UTF16 pair offsets. 
    - These are normally the same, but notably differ when embedding emoji characters.
  - limitations
    - Your document must only contain pure JSON-stringifyable content. No dates, functions or self-references allowed. Your object should be identical to JSON.parse(JSON.stringify(obj)).
- https://github.com/ottypes/json0 /js
  - The JSON OT type can be used to edit arbitrary JSON documents.
  - JSON0 is an invertable type - which is to say, all operations have an inverse operation which will undo the original op. 
    - As such, all operations which delete content have the content to be deleted inline in the operation.
  - Embedded string editing, using the old `text0` OT type as a subtype
  - [json0 supporting of rfc6902 specification for JSON type?_201410](https://github.com/ottypes/json0/issues/4)
    - json0 type doesn't support moving objects between paths, so its not compatible with json patch.
  - limitations
    - doesn't support moves between object keys
    - doesn't support moving child values from one object to another
    - Set if null (object insert with first writer wins semantics)
    - Efficient list insert-of-many-items
  - uses the list-of-op-components model, where each operation makes a series of individual changes to a document.
    - Joseph now thinks this is a terrible idea because it doesn't scale well to large operations - it has N2 instead of 2N complexity.
    - rewriting this library to instead make each operation be a sparse traversal of the document. 

- https://github.com/vitotafuni/JSOTTEST
  - http://vitotafuni.github.io/jsottest/
  - a simple simulator for Operational Transformation algorithms written in JavaScript.

- https://github.com/yiminghe/ot-engine
  - https://ot-engine-rich-text.herokuapp.com/
  - Operational transformation engine
  - 示例使用quill，不依赖sharedb
  - support presence(cursors)
  - support local undo/redo

- https://github.com/ryneli/ot-crdt-papers
  - intersection of Operational Transformation and Conflict-free Replicated Data Types (CRDT's).
  - Running the prototype collaborative editor，实现简单

- https://github.com/otjs/ot /js
  - A line-based operational transform algorithm
  - https://github.com/otjs/ot-client
  - https://github.com/otjs/ot-server

- https://github.com/tOkeshu/ot.js /js/2013
  - ot.js is a pure JavaScript library to work with operational transformations.

- https://github.com/fitzgen/operational-transformation-example /2013
  - an implementation of a real time collaborative document editor which uses my Operational Transformation library.
  - [Operational Transformation: An Introduction_2011](https://fitzgeraldnick.com/2011/03/26/operational-transformation-an-introduction.html)
  - [Operational Transformation Part 2: Operations](https://fitzgeraldnick.com/2011/04/05/operational-transformation-operations.html)
  - https://github.com/fitzgen/operational-transformation

- https://github.com/gatlin/otis
  - another operational transformation library for JSON values.
  - 依赖robot3，A functional, immutable Finite State Machine library
  - https://github.com/gatlin/cauldron
    - this is a nestjs based operational transform service for arbitrary json data, using my library otis.

- https://github.com/rclarey/simple-ot
  - A simple operational transform library that uses the domain-agnostic GOTO control algorithm.
  - For an example application using this library, see cloudcode
  - https://github.com/rclarey/cloudcode
    - developing and deploying a small Deno backend (see server.ts).

- https://github.com/kizahasi/ot-string
  - Operational Transfomation library for string.

- https://github.com/Jaeyo/Operational-Transformation-Example
  - Operational Transform Example with node.js
  - 直接在控制台测试，无需server

- https://github.com/hanupratap/Operational-Transform
  - Operational Transform algorithm used by google Docs
  - https://github.com/kshitij86/operational_transform

- https://github.com/vaziliybober/operlib
  - An operational transformation library

- https://github.com/BrotherJing/scalable-ot
  - A scalable concurrent collaboration framework based on Operational Transformation (OT).
  - 后端依赖 ot-json0、ot-text、google-protobuf、mongodb、ws、express
  - Clients send operations through API.
  - Operations are pushed into MQ, partitioned by document id.
  - OT server receives operations of same document sequentially and performs conflict solving.
  - Broadcast server sends conflict-free operations to clients.
  - Conflict-free operations are pushed into another MQ(or db stream), trigger a consumer which apply them on document snapshot sequentially.
# ot-examples
- json0前端示例
  - https://codesandbox.io/s/s828w
    - useCollaboration.ts

- https://github.com/josephg/appstate /201407
  - This is a little toy prototype exploring the idea that each client shares a single JSON object with the server. 
  - Both the client and the server can read & edit the session object using OT. 
  - The object has all the data the client needs to know to run the app.

- https://github.com/datavis-tech/json0-presence-demo
  - A demo of plain text presence using json0+ShareDB and html-text-collab-ext.
  - The original application was simplified by Curran Kelleher down to a single textarea with presence

- https://github.com/convergencelabs/html-text-collab-ext
  - A set of utilities that enhances a normal HTML `<textarea>` element with collaborative editing capabilities. 
  - The enhanced `<textarea>` is able to render the cursor and selection of other collaborators.
  - This library has no dependency on Convergence.
  - 只依赖textarea-caret，不依赖其他

- https://github.com/ausnorris/leaderboard
  - json0+sharedb

- https://github.com/jatfret/OT-server
  - https://github.com/jatfret/OT
  - 一个基于 operational transformation 思想的协同编辑应用
# ot-utils
- https://github.com/kbadk/json0-ot-diff
  - Finds differences between two JSON object and generates operational transformation (OT) operations for transforming the first object into the second according to the JSON0 OT Type.

- https://github.com/slevental/operational-transformation /java
  - a reference implementation for OT protocol described introduced in Google Wave and described in their documentation
- https://github.com/Fleischers/OT_example /java
  - simple local console implementation of Operational Transformation
# more-ot
- [I'm looking for a library that would allow me to synchronize text in real-time between multiple users (ala Google Docs).](https://stackoverflow.com/questions/2043165)
