---
title: lib-db-indexeddb-blog
tags: [blog, indexeddb]
created: 2022-06-13T02:56:54.717Z
modified: 2022-06-13T02:57:07.648Z
---

# lib-db-indexeddb-blog

# guide

# [The pain and anguish of using IndexedDB: problems, bugs and oddities](https://gist.github.com/pesterhazy/4de96193af89a6dd5ce682ce2adff49a)
- This gist lists challenges you run into when building offline-first applications based on IndexedDB, including open-source libraries like Firebase, pouchdb and AWS amplify 

- State deleted after 7 days of inactivity (Safari)
  - After 7 days of inactivity, Safari deletes all browser storage, including cookies, localstorage, websql and indexeddb. Other browsers don't do this.
  - The feature, called Intelligent Tracking Prevention (ITP), is meant to prevent advertisers from abusing indexeddb as a way to track users.

- Is IndexedDB ACID compliant?
  - IndexedDB does not provide transaction isolation. As far as I know, concurrent transactions (in multiple tabs or even in a single tab) are never rolled back because they touch the same object stores. The only exception, as far as I can tell, is exceptions thrown when a primary key constraint is violated. This can be used to achieve some level of transaction isolation. However, the guarantees are nowhere near as extensive as those provided by SQL databases.

- No locking primitives (Safari, Firefox)
  - The Web Platform lacks a standardized way - or any proper way, really - to lock a resource across multiple tabs of the same browser. Multiple tabs of an app using IndexedDB will invariably write to the same IndexedDb database. Without cross-tab locking, database corruption is hard to avoid.

- Private Browsing Mode (Firefox)
  - Firefox is the only major browser without support for IndexedDB in Private Browsing mode. 
  - Because there is no API to tell if Private Browsing is active, the only workaround is to try to open a test database and to regard the API as unavailable if this fails.

- Web SQL - the database that could have been
  - Before IndexedDB there was Web SQL, a thin wrapper around the legendary SQLite embedded database. Web SQL is more powerful (a proper superset of IndexedDB) and arguably better designed than IndexedDB.
  - Mozilla objected to the Web SQL interface as having no alternative implementation available. 
  - Ironically, IndexedDB is internally implemented based on SQLite in Firefox (Chrome uses the simpler LevelDB instead).

- [Notion's page load and navigation times just got faster_202104](https://www.notion.so/blog/faster-page-load-navigation)
  - We decided to migrate our desktop apps to SQLite because it's a hardened storage solution that's shown marked performance improvements on our mobile applications for the past year.
  - Before SQLite, we relied on IndexedDB for client-side storage. 
  - But we encountered storage quotas, a number of bugs, and performance concerns on Windows machines in particular, which meant IndexedDB wouldn’t scale with Notion’s growing user base.

- Bugs, bugs, bugs (Safari)
  - The Webkit team keeps shipping critical storage-related bugs into production, again and again
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
