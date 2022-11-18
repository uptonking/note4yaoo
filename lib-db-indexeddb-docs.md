---
title: lib-db-indexeddb-docs
tags: [docs, indexeddb]
created: 2022-06-13T02:57:15.478Z
modified: 2022-06-13T02:57:31.829Z
---

# lib-db-indexeddb-docs

# guide

# docs

## [Using IndexedDB - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)

- The object store persistently holds records, which are key-value pairs. 
  - Records within an object store are sorted according to the keys in an ascending order.

- IndexedDB storage in browsers' privacy modes only lasts in-memory until the incognito session is closed 
  - (Private Browsing mode for Firefox and Incognito mode for Chrome, but in Firefox this is not implemented yet as of May 2021 so you can't use IndexedDB in Firefox Private Browsing at all).

- A key can be one of the following types: string, date, float, a binary blob, and array. For arrays, the key can range from an empty value to infinity. And you can include an array within an array.

- a `success` event (that is, a DOM event whose `type` property is set to "success") is fired with `request` as its `target`.
  - 这么设计是为了方便链式调用，而不用定义request中间变量
  - Since the DOM event has the request as its target you can use the event to get to the result property.

- You can also create indices on any object store, provided the object store holds objects, not primitives.

- To change the "schema" or structure of the database—which involves creating or deleting object stores or indexes—the transaction must be in `versionchange` mode. 
  - This transaction is opened by calling the `IDBFactory.open` method with a `version` specified.

- transaction lifetime
  - As long as there are pending requests the transaction remains active.
- the default behavior of an error is to abort the transaction in which it occurred. 

- There is a performance cost associated with looking at the value property of a cursor, because the object is created lazily. 
  - When you use getAll() for example, the browser must create all the objects at once. 
  - If you're just interested in looking at each of the keys, for instance, it is much more efficient to use a cursor than to use getAll(). 

- A normal cursor maps the index property to the object in the object store. 
  - A key cursor maps the index property to the key used to store the object in the object store

- When you call open() with a greater version than the actual version of the database, all other open databases must explicitly acknowledge the request before you can start making changes to the database (an onblocked event is fired until they are closed or reloaded). 

- Since the user can exit the browser at any time, this means that you cannot rely upon any particular transaction to complete, and on older browsers, you don't even get told when they don't complete.  
  - you should combine the clear and the write into a single transaction.
  - you should never tie database transactions to unload events. because they are asynchronous they will be aborted before they can execute.
  - In fact, there is no way to guarantee that IndexedDB transactions will complete, even with normal browser shutdown.
