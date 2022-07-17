---
title: web-fwk-storage
tags: [storage, web]
created: 2021-04-12T11:44:40.115Z
modified: 2021-07-28T20:22:58.032Z
---

# web-fwk-storage

# guide

# blogs

## [High performance storage for your app: the Storage Foundation API__202106](https://web.dev/storage-foundation/)

- The Storage Foundation API resembles a basic file system, with direct access to stored data through buffers and offsets. 
- The Storage Foundation API is a new fast and unopinionated storage API that unlocks new and much-requested use cases for the web, such as implementing performant databases and gracefully managing large temporary files.
- The Storage Foundation API is designed to resemble a very basic file system so it gives developers flexibility by providing generic, simple, and performant primitives on which they can build higher-level components. 

- The web platform offers a number of storage options for developers, each of which is built with specific use-cases in mind.
- Some of these options clearly do not overlap with this proposal as they **only allow very small amounts of data** to be stored, like `cookie`s, or the Web Storage API consisting of the `sessionStorage` and the `localStorage` mechanisms.
- Other options are already **deprecated** for various reasons like the File and Directory Entries API or WebSQL.
- The File System Access API has a similar API surface, but its use is to interface with the client's file system and provide access to data that may be outside of the origin's or even the browser's ownership. 
  - This different focus comes with stricter security considerations and higher performance costs.
- The IndexedDB API can be used as a backend for some of the Storage Foundation API's use-cases. 
  - For example, Emscripten includes IDBFS, an IndexedDB-based persistent file system. 
  - However, since IndexedDB is fundamentally a key-value store, it comes with significant **performance limitations**. 
  - Furthermore, directly accessing subsections of a file is even more difficult and slower under IndexedDB.
- Finally, the CacheStorage interface is widely supported and is tuned for storing large-sized data such as web application resources, but the values are immutable.

- The Storage Foundation API is an attempt at closing all the gaps of the previous storage options by allowing for the performant storage of mutable large files defined within the origin of the application.
- Suggested use cases for the Storage Foundation API
  - Productivity or creativity apps that operate on large amounts of video, audio, or image data. Such apps can offload segments to disk instead of holding them in memory.
  - Apps that rely on a persistent file system accessible from Wasm and that need more performance than what IDBFS can guarantee.
- What is the Storage Foundation API?
  - File system calls, which provide basic functionality to interact with files and file paths.
  - File handles, which provide read and write access to an existing file.

## [Storage for the web__202004](https://web.dev/storage-for-the-web/)

- Here's **a general recommendation for storing** resources:
  - For the network resources necessary to load your app and file-based content, use the **Cache Storage API** (part of service workers).
  - For other data, use **IndexedDB** (with a promises wrapper).

- IndexedDB and the Cache Storage API are supported in every modern browser. 
  - They're both asynchronous, and will not block the main thread. 
  - They're accessible from the `window` object, web workers, and service workers, making it easy to use them anywhere in your code.
- SessionStorage is tab specific, and scoped to the lifetime of the tab. 
  - It may be useful for storing small amounts of session specific information, for example an IndexedDB key. 
  - It should be used with caution because it is synchronous and will block the main thread. 
  - It is limited to about 5MB and can contain only strings. 
  - Because it is tab specific, it is not accessible from web workers or service workers.
- LocalStorage should be avoided because it is synchronous and will block the main thread. 
  - It is limited to about 5MB and can contain only strings. 
  - LocalStorage is not accessible from web workers or service workers.
- Cookies have their uses, but should not be used for storage. 
  - Cookies are sent with every HTTP request, so storing anything more than a small amount of data will significantly increase the size of every web request. 
  - They are synchronous, and are not accessible from web workers. 
  - Like LocalStorage and SessionStorage, cookies are limited to only strings.
- The File System API and FileWriter API provide methods for reading and writing files to a sandboxed file system. 
  - While it is asynchronous, it is not recommended because it is only available in Chromium-based browsers.
- The File System Access API was designed to make it easy for users to read and edit files on their local file system. 
  - The user must grant permission before a page can read or write to any local file, and permissions are not persisted across sessions.
- WebSQL should not be used, and existing usage should be migrated to IndexedDB. 
  - Support has been removed from almost all major browsers. 
  - The W3C stopped maintaining the Web SQL spec in 2010, with no plans to further updates planned.
- Application Cache should not be used, and existing usage should be migrated to service workers and the Cache API. 
  - It has been deprecated and support will be removed from browsers in the future.

- How much can I store?
- Chrome allows the browser to use up to 80% of total disk space
  - You can use the StorageManager API to determine the maximum quota available.
- Internet Explorer 10 and later can store up to 250MB and will prompt the user when more than 10MB has been used.
- Firefox allows the browser to use up to 50% of free disk space
  - You can use the StorageManager API to determine how much space is still available.
- Safari (both desktop and mobile) appears to allow about 1GB. 
  - When the limit is reached, Safari will prompt the user, increasing the limit in 200MB increments. 
- In the past, if a site exceeded a certain threshold of data stored, the browser would prompt the user to grant permission to use more data.
  - Today, most modern browsers will not prompt the user, and will allow a site to use up to its allotted quota. 
# ref
