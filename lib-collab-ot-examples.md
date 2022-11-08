---
title: lib-collab-ot-examples
tags: [collaboration, examples, ot]
created: 2022-10-02T20:50:54.901Z
modified: 2022-10-02T20:51:30.444Z
---

# lib-collab-ot-examples

# guide

- [am-editor 协同编辑配置](https://editor.aomao.com/zh-CN/config/ot)
  - 编辑器基于 sharedb 与 json0 协议交互协作操作数据
  - 客户端（编辑器）通过 WebSocket 与服务端建立长连接通信，编辑器每次的 dom 结构变更都将转换为json0格式操作命令（ops）发送到服务端并修改服务端数据后再分发给各个客户端
  - sharedb 会把每次客户端与服务端的操作数据保存为日志，并且在每次操作后都会把最新生成的文档数据保留下来。这些操作都在 ot-server 中进行
# popular
- https://github.com/Starcounter-Jack/JSON-Patch
  - Update JSON documents using delta patches.
  - JSON-Patch (RFC6902) is a standard format that allows you to update a JSON document by sending the changes rather than the whole document. 
  - JSON Patch plays well with the HTTP PATCH verb (method) and REST style programming.
  - Lean and mean Javascript implementation of the JSON-Patch standard (RFC 6902).

- https://github.com/Palindrom/Palindrom
  - Library for two-way data binding between local and remote JSON models. 
  - It uses JSON-Patch for data updates and Operational Transformation for versioning and data consistency. 
  - It operates via HTTP or WebSocket or both.

- sharedb /5.4kStar/MIT/202210/js
  - https://github.com/share/sharedb
  - ShareDB is a realtime database backend based on Operational Transformation (OT) of JSON documents. 
  - It is the realtime backend for the DerbyJS web application framework.
  - https://github.com/derbyjs/derby
    - MVC framework making it easy to write realtime, collaborative applications that run in both Node.js and browsers

- https://github.com/Progyan1997/Operational-Transformation
  - http://operational-transformation.github.io/
  - A collection of Algorithms to Synchronise changes across multiple clients using Operational Transformation
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
  - Embedded string editing, using the old text0 OT type as a subtype
  - limitations
    - doesn't support moves between object keys
    - doesn't support moving child values from one object to another
    - Set if null (object insert with first writer wins semantics)
    - Efficient list insert-of-many-items

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
