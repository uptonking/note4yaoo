---
title: web-filesystem-opfs-community
tags: [community, opfs]
created: 2023-01-13T10:47:22.203Z
modified: 2023-01-13T10:47:36.755Z
---

# web-filesystem-opfs-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Do you know what persistence is like in Chrome? 
- https://twitter.com/tomayac/status/1613605318407094275
  - Say my website dumps 1 GB of data in an OPFS SQLite database. Does that get persisted similar to IndexedDB? Like will it get evicted(驱逐，赶出) due to low disk space, or deleted if the user clears their browser cache?
- When it hits your origin, _all_ quota-managed storage mechanisms get purged. The way if it hits your origin gets decided is by looking at all quota-managed storage mechanisms of all origins and then purging by LRU.
  - Quota-managed storage mechanisms are: cache storage, IDB, service worker, media license, OPFS, Web SQL (the last is of course soon history).
- The library uses the OPFS, the origin private file system, and requires a web worker context.

- ## "Browsers will not serve Wasm files from file:// URLs" and that a web server is required, along with setting 2 response headers. 
- https://groups.google.com/a/chromium.org/g/chromium-extensions/c/WsxV-5CqAko
  - What about inside a Chrome extension? Can extensions create a SQLite database using SQLite wasm and OPFS?
- Files in Chrome extensions like https://localhost (not file://), it is a secure context.
  - Why does it need the "Cross-Origin-Opener-Policy" and "Cross-Origin-Embedder-Policy" HTTP headers? Because it is the security requirements of SharedArrayBuffer.
  - Furthermore, Chrome extension does support these two HTTP headers. 
  - 👉🏻 In summary, SQLite Wasm with SharedArrayBuffer works in Chrome extension.
- Service worker and web worker are different. You can read their introductory article. Here, createSyncAccessHandle is a sync IO method, so it only works in web worker by design. 
  - You can create a web worker in extension pages, e.g. the popup page or any web pages in your extension.
  - Content scripts are out of extension origin. You should only use sqlite in your extension origin.
  - You can't create web worker in service worker at present. Some extension developers propose that web workers can be created in service worker.

- https://github.com/randyl/sqlite3-wasm-demo-extension
  - [SQLite Wasm in the browser backed by the Origin Private File System - Chrome Developers](https://developer.chrome.com/blog/sqlite-wasm-in-the-browser-backed-by-the-origin-private-file-system/)

- As mentioned earlier, there's a missing API in service workers which means the OPFS SQLite implementation doesn't work at the moment.
