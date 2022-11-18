---
title: lib-db-indexeddb-blog
tags: [blog, indexeddb]
created: 2022-06-13T02:56:54.717Z
modified: 2022-06-13T02:57:07.648Z
---

# lib-db-indexeddb-blog

# guide

# [Best Practices for Using IndexedDB_201706](https://web.dev/indexeddb-best-practices/)

> Learn best practices for syncing application state between IndexedDB and (in-memory) popular state management libraries.

- When a user first loads a website or application, there's often a fair amount of work involved in constructing the initial application state that's used to render the UI.
  - For example, sometimes the app needs to authenticate the user client-side and then make several API requests before it has all the data it needs to display on the page.
- Storing the application state in IndexedDB can be a great way to speed up the load time for repeat visits. 
  - The app can then sync up with any API services in the background and update the UI with new data lazily, employing a stale-while- revalidate strategy.
- Another good use for IndexedDB is to store user-generated content, either as a temporary store before it is uploaded to the server or as a client-side cache of remote data - or, of course, both.

- Keeping your app predictable
- A lot of the complexities around IndexedDB stem from the fact that there are so many factors you (the developer) have no control over.
- Not everything can be stored in IndexedDB on all platforms
  - If you are storing large, user-generated files such as images or videos, then you may try to store them as `File` or `Blob` objects. 
    - This will work on some platforms but fail on others. 
    - Safari on iOS, in particular, cannot store Blobs in IndexedDB.
    - Storing ArrayBuffers in IndexedDB is very well supported.
    - a Blob has a MIME type while an ArrayBuffer does not. You will need to store the type alongside the buffer in order to do the conversion correctly.
- Writing to storage may fail 
  - Errors when writing to IndexedDB can happen for a variety of reasons, and in some cases these reasons are outside of your control as a developer.
  - For example, some browsers currently don't allow writing to IndexedDB when in private browsing mode.
  - There's also the possibility that a user is on a device that's almost out of disk space, and the browser will restrict you from storing anything at all.
  - This also means it's generally a good idea to keep application state in memory (in addition to storing it), so the UI doesn't break when running in private browsing mode or when storage space isn't available 
- Stored data may have been modified or deleted by the user
  - Unlike server-side databases where you can restrict unauthorized access, client-side databases are accessible to browser extensions and developer tools, and they can be cleared by the user.
- Stored data may be out of date 
  - IndexedDB has built-in support for schema versions and upgrading via its `IDBOpenDBRequest.onupgradeneeded()`
  - you still need to write your upgrade code in such a way that it can handle the user coming from a previous version (including a version with a bug).
  - Unit tests can be very helpful here

- Keeping your app performant
  - As a general rule, reads and writes to IndexedDB should not be larger than required for the data being accessed.
  - While IndexedDB makes is possible to store large, nested objects as a single record, this practice should be avoided. 
    - 👀 The reason is because when IndexedDB stores an object, it must first create a structured clone of that object, and the structured cloning process happens on the main thread. 
    - The larger the object, the longer the blocking time will be.
  - while simply storing the entire state tree as a single record in IndexedDB may be tempting and convenient, doing this after every change (even if throttled/debounced) will result in unnecessary blocking of the main thread, it will increase the likelihood of write errors, and in some cases it will even cause the browser tab to crash or become unresponsive.
  - 👉🏻 Instead of storing the entire state tree in a single record, you should break it up into individual records and only update the records that actually change.
    - In cases where it's not feasible to break up a state object and just write the minimal change-set, breaking up the data into sub-trees and only writing those is still preferable to always writing the entire state tree. 
  - The same is true if you store large items like images, music, or video in IndexedDB.
- Lastly, you should always be measuring the performance impact of the code you write.
# rxdb

## [Alternatives for realtime offline-first JavaScript applications](https://rxdb.info/alternatives.html)

- this page contains all known alternatives to RxDB

- RxDB supports using Dexie.js as RxStorage which enhances IndexedDB with RxDB features like MongoDB-like queries etc

## more rxdb

- https://news.ycombinator.com/from?site=rxdb.info
# more
- [local-first tech](https://jaredforsyth.com/posts/)
