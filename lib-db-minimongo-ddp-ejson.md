---
title: lib-db-minimongo-ddp-ejson
tags: [ddp, ejson, meteor, minimongo]
created: 2022-12-04T16:32:43.249Z
modified: 2022-12-04T16:33:23.817Z
---

# lib-db-minimongo-ddp-ejson

# guide

- minimongo/meteor 的replication协议参考 [Distributed Data Protocol (DDP)](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)

- ddp/ejson的参考实现: 官方包提取、gongo、第三方ddp
# meteor-ddp-ejson

## [EJSON, Meteor's JSON extension](https://docs.meteor.com/api/ejson.html)

- EJSON is an extension of JSON to support more types. 
  - Date (JavaScript Date)
  - Binary (JavaScript Uint8Array or the result of EJSON.newBinary)
  - Special numbers (JavaScript NaN, Infinity, and -Infinity)
  - Regular expressions (JavaScript RegExp)
  - User-defined types (see EJSON.addType. For example, Mongo. ObjectID is implemented this way.)
- All EJSON serializations are also valid JSON

## [meteor ddp intro](https://github.com/meteor/meteor/tree/devel/packages/ddp)

- DDP (Distributed Data Protocol) is the stateful websocket protocol that Meteor uses to communicate between the client and the server.
- ddp supports the standard DDP transport, stringified EJSON over websockets. 
  - It also supports a second transport, EJSON over HTTP long polling. 
  - It will automatically fall back to this transport if websockets are not available. 
  - It uses the sockjs library for long polling.

## ddp-more

- [Meteor-DDP翻译](https://cnodejs.org/topic/51b030d9555d34c678e5fb2e)
# meteor
- meteor
  - a whole framework with its own package manager, database management and replication protocol.
  - hard to integrate it with other modern JavaScript frameworks like angular, vue.js or svelte
  - Meteor uses MongoDB in the backend and can replicate with a Minimongo database in the frontend
  - to make a meteor app offline first capable. There are some projects that might do this, but all are unmaintained.

- [Meteor的工作原理及优势与不足](https://cloud.tencent.com/developer/article/1643568)
  - 优势：易学、偏向客户端、实时响应、生态
  - 不足：nodejs单线程不适合计算密集型、约束少、NoSQL、非静态、首次加载时间长
# discuss

- ## [How efficient is Meteor's DDP at syncing very large collections? - Stack Overflow](https://stackoverflow.com/questions/18734507/how-efficient-is-meteors-ddp-at-syncing-very-large-collections)
- After some empirical experience with this, I have to conclude that the answer is "not very efficient". 


- [benchmarking - How efficient can Meteor be while sharing a huge collection among many clients? - Stack Overflow](https://stackoverflow.com/questions/13113256/how-efficient-can-meteor-be-while-sharing-a-huge-collection-among-many-clients/21835534#21835534)
