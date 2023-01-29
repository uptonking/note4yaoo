---
title: pm-pattern-local-first
tags: [local-first, pattern, pm]
created: 2021-08-22T08:05:15.252Z
modified: 2021-08-22T08:05:39.413Z
---

# pm-pattern-local-first

# guide

- 浏览器存储层原理
  - 业务代码appCode > indexeddb > leveldb/sqlite > os-fs
  - 业务代码appCode > sqlite-opfs > os-fs

- 对indexeddb/外部存储的取舍
  - 对于基础库，应该以内存数据模型为主，因为idb读写要慢得多
  - 对于应用层，可对indexeddb的数据模型进行可扩展的设计，方便迁移到其他数据库如sqlite

- 用户自己选择数据存储位置的缺点
  - 第一次拉取数据耗时较长
  - 不能使用服务端集群搜索，只能在本地搜索

- 放弃使用浏览器扩展的形式来实现离线
  - indexeddb的访问存在same-origin的限制，不应该维护两套数据
  - pwa支持离线使用，使用webview打包也简单

- 本地文件格式的设计
  - 移动端对本地格式不敏感，所以考虑优先sqlite，但文本或开放格式方便使用第三方同步
  - 完全自定义，类似pdf、xls、doc、dwg
  - 多层级文件夹，类似git
  - 被封装的多层级，类似epub、odt
  - sqlite
  - 可以结合多种方案，将适合用户读写的数据以纯文本格式暴露，不合适读写的数据放在其他格式甚至数据库

- 如何同步修改

- why local
  - 平台封号
  - 百度网盘替换部分视频为8秒短视频
  - 百度网盘后期限速，就算开了超级会员仍然可能因为带宽流量消耗过多而被系统限制
  - 腾讯起诉DD373交易平台，庭审时腾讯代表称「账号主人不可转卖自己的手机游戏账号」

- ref
  - [local-first tech](https://jaredforsyth.com/posts/)
  - [Local-first data migrations](https://blog.gfor.rest/blog/lofi-migrations)

# [Local-first software__201910](https://www.inkandswitch.com/local-first.html)
- Cloud apps like Google Docs and Trello are popular because they enable real-time collaboration with colleagues, and they make it easy for us to access our work ~~from all of our devices~~ anytime anywhere. 
  - However, by centralizing data storage on servers, cloud apps also take away ownership and agency from users. 
  - If a service shuts down, the software stops functioning, and data created with that software is lost.
- In this article we propose “local-first software”: a set of principles for software that enables both collaboration and ownership for users. 
  - Local-first ideals include the ability to work offline and collaborate across multiple devices, while also improving the security, privacy, long-term preservation, and user control of data.
- We survey existing approaches to data storage and sharing, ranging from email attachments to web apps to Firebase-backed mobile apps, and we examine the trade-offs of each. 
  - We look at Conflict-free Replicated Data Types (CRDTs): data structures that are multi-user from the ground up while also being fundamentally local and private. 
  - CRDTs have the potential to be a foundational technology for realizing local-first software.

- Motivation: collaboration and ownership

## Seven ideals for local-first software

- Fast; No spinners: your work at your fingertips
- Offline-able; The network is optional
- Longevity; The Long Now(accessing the data for a long time in the future)
- User control; You retain ultimate ownership and control
- Privacy; Security and privacy by default

- Collaborative; Seamless collaboration with your colleagues
- Multi devices; Your work is not trapped on one device

## Existing data storage and sharing models

- How application architecture affects user experience
  - Files and email attachments
  - Web apps: Google Docs, Trello, Figma
  - Dropbox, Google Drive, Box, OneDrive, etc.
  - Git and GitHub
- Developer infrastructure for building apps
  - Web app (thin client)
  - Mobile app with local storage (thick client)
  - Backend-as-a-Service: Firebase, CloudKit, Realm
  - CouchDB

## Towards a better future

- CRDTs as a foundational technology
- Ink & Switch prototypes
  - Trello clone
  - Collaborative drawing
  - Media canvas
  - Findings

- Ink & Switch has developed an open-source, JavaScript CRDT implementation called `Automerge`. 
  - It is based on our earlier research on JSON CRDTs. 
  - We have then combined Automerge with the Dat networking stack to form Hypermerge. 
  - We do not claim that these libraries fully realize local-first ideals — more work is still required.
- However, based on our experience with them, we believe that CRDTs have the potential to be a foundation for a new generation of software. 
  - Just as packet switching was an enabling technology for the Internet and the web, or as capacitive touchscreens were an enabling technology for smartphones, so we think **CRDTs may be the foundation for collaborative software that gives users full ownership of their data**.

- We built three prototypes
- Trellis
  - https://github.com/automerge/trellis
  - Trello clone/sample app for Automerge persistence library
  - take a look at PushPin, a much more complete & robust implementation of this approach to software development.
- pixelpusher
  - https://github.com/automerge/pixelpusher
  - bringing a Figma-like real-time experience to Javier Valencia’s Pixel Art to CSS.
- PushPin
  - https://github.com/automerge/pushpin
  - a mixed media canvas workspace similar to Miro or Milanote.
  - A local-first collaborative corkboard app. 

- Our goal in developing the three prototypes Trellis, PixelPusher and PushPin was to evaluate the technology viability, user experience, and developer experience of local-first software and CRDTs. 
  - CRDT technology works.
  - The user experience with offline work is splendid.
  - Developer experience is viable when combined with Functional Reactive Programming (FRP).
    - The FRP model of React fits well with CRDTs. 
    - A data layer based on CRDTs means the user’s document is simultaneously getting updates from the local user (e.g. as they type into a text document) but also from the network (as other users and other devices make changes to the document).
  - Conflicts are not as significant a problem as we feared.
  - Visualizing document history is important.
  - URLs are a good mechanism for sharing.
  - CRDTs accumulate a large change history, which creates performance problems.
    - Performance and memory/disk usage quickly became a problem because CRDTs store all history, including character-by-character text edits. 
    - These pile up, but can’t easily be truncated because it’s impossible to know when someone might reconnect to your shared document after six months away and need to merge changes from that point forward.
    - We continue to optimize Automerge, but this is a major area of ongoing work.
  - Network communication remains an unsolved problem.
  - Cloud servers still have their place for discovery, backup, and burst compute.

- Then some strategies for improving each area:
- Fast. 
  - Aggressive caching and downloading resources ahead of time can be a way to prevent the user from seeing spinners when they open your app or a document they previously had open. 
  - Trust the local cache by default instead of making the user wait for a network fetch.
- Offline. 
  - In the web world, Progressive Web Apps offer features like Service Workers and app manifests that can help. 
  - In the mobile world, be aware of WebKit frames and other network-dependent components. 
  - Test your app by turning off your WiFi, or using traffic shapers such as the Chrome Dev Tools network condition simulator or the iOS network link conditioner.
- Longevity. 
  - Make sure your software can easily export to flattened, standard formats like JSON or PDF. 
  - For example: 
    - mass export such as Google Takeout; 
    - continuous backup into stable file formats such as in GoodNotes; 
    - and JSON download of documents such as in Trello.
- User control. 
  - Can users easily back up, duplicate, or delete some or all of their documents within your application? 
  - Often this involves re-implementing all the basic filesystem operations, as Google Docs has done with Google Drive.
- Privacy. 
  - Cloud apps are fundamentally non-private, with employees of the company and governments able to peek at user data at any time. 
  - But for mobile or desktop applications, try to make clear to users when the data is stored only on their device versus being transmitted to a backend.

- Collaboration. 
  - Besides CRDTs, the more established technology for real-time collaboration is Operational Transformation (OT), as implemented e.g. in ShareDB.
- Multi-device. 
  - Syncing infrastructure like Firebase and iCloud make multi-device support relatively painless, although they do introduce longevity and privacy concerns. 
  - Self-hosted infrastructure like Realm Object Server provides an alternative trade-off.

- If you are an entrepreneur interested in building developer infrastructure, all of the above suggests an interesting market opportunity: “Firebase for CRDTs.”
  - Such a startup would need to offer a great developer experience and a local persistence library (something like SQLite or Realm). 
  - It would need to be available for mobile platforms (iOS, Android), native desktop (Windows, Mac, Linux), and web technologies (Electron, Progressive Web Apps).
  - User control, privacy, multi-device support, and collaboration would all be baked in. 
  - Application developers could focus on building their app, knowing that the easiest implementation path would also given them top marks on the local-first scorecard. 

## Conclusions

- In the pursuit of better tools we moved many applications to the cloud. 
  - Cloud software is in many regards superior to “old-fashioned” software
  - it offers collaborative, always-up-to-date applications, accessible from anywhere
- However, in the cloud, ownership of data is vested(合法的归属于) in the servers, not the users, and so we became borrowers of our own data. 
  - The documents created in cloud apps are destined to disappear when the creators of those services cease to maintain them. 
  - Cloud services defy(不可能；反抗) long-term preservation. 
  - No Wayback Machine can restore a sunsetted web application. 
  - The Internet Archive cannot preserve your Google Docs.
- But more work is needed to realize the local-first approach in practice.
  - Application developers can take incremental steps, such as improving offline support and making better use of on-device storage. 
  - Researchers can continue improving the algorithms, programming models, and user interfaces for local-first software. 
  - Entrepreneurs can develop foundational technologies such as CRDTs and peer-to-peer networking into mature products able to power the next generation of applications.
# [SQLite As An Application File Format](https://www.sqlite.org/appfileformat.html)
- An SQLite database file with a defined schema often makes an excellent application file format. 
  - Here are a dozen reasons why this is so:
  - Simplified Application Development
  - Single-File Documents
  - High-Level Query Language
  - Accessible Content
  - Cross-Platform
  - Atomic Transactions
  - Incremental And Continuous Updates
  - Easily Extensible
  - Performance
  - Concurrent Use By Multiple Processes
  - Multiple Programming Languages
  - Better Applications

- An "application file format" is the file format used to persist application state to disk or to exchange information between programs. 
  - There are thousands of application file formats in use today, like doc/xls/pdf/dwg/epub/git/...
- We make a distinction between a "file format" and an "application format". 
  - A file format is used to store a single object. 
    - So, for example, a GIF or JPEG file stores a single image
  - An EPUB file, in contrast, stores both text and images (as contained XHTML and GIF/JPEG files) and so it is considered an "application format". 
  - The boundary between a file format and an application format is fuzzy. 
  - This article is about "application formats".
  - For this article, let us say that a file format stores a single object and an application format stores many different objects and their relationships to one another.

- Most application formats fit into one of these three categories:
- Fully Custom Formats. 大多单文件、大多二进制、读写需要专用软件
  - Custom formats are specifically designed for a single application. 
  - DOC, XLS, DWG, PDF, and PPT are examples of custom formats. 
  - Custom formats are usually contained within a single file, for ease of transport. 
  - They are also usually binary, though the DWG format is a notable exception.
  - Custom file formats require specialized application code to read and write and are not normally accessible from commonly available tools such as unix command-line programs and text editors.
  - In other words, custom formats are usually "opaque blobs". 
  - To access the content of a custom application file format, one needs a tool specifically engineered to read and/or write that format.
- Pile-of-Files Formats. 通常多级文件夹、部分可读写、移动或引用不便
  - A pile-of-files format essentially uses the filesystem as a key/value database, storing small chunks of information into separate files. 
  - Git is a prime example of this, though the phenomenon occurs frequently in one-off and bespoke applications. 
  - This gives the advantage of making the content more accessible to common utility programs such as text editors or "awk" or "grep". 
  - But even if many of the files in a pile-of-files format are easily readable, there are usually some files that have their own custom format (example: Git "Packfiles") and are hence "opaque blobs" that are not readable or writable without specialized tools. 
  - It is also much less convenient to move
  - Finally, a pile-of-files format breaks the "document metaphor": there is no one file that a user can point to that is "the document".
- Wrapped Pile-of-Files Formats. 
  - Some applications use a Pile-of-Files that is then encapsulated into some kind of single-file container, usually a ZIP archive. 
  - EPUB, ODT, and ODP are examples of this approach.
  - OpenOffice documents (ODT and ODP) are also ZIP archives containing XML and images that represent their content as well as "catalog" files that show the interrelationships between the component parts.
  - A wrapped pile-of-files format is a compromise between a full custom file format and a pure pile-of-files format. 
  - A wrapped pile-of-files format is not an opaque blob in the same sense as a custom format, since the component parts can still be accessed using any common ZIP archiver, but the format is not quite as accessible as a pure pile-of-files format because one does still need the ZIP archiver
  - As with custom file formats, and unlike pure pile-of-file formats, a wrapped pile-of-files format is not as easy to edit, since usually the entire file must be rewritten in order to change any component part.

- The purpose of this document is to argue **in favor of a fourth new category of application file format: An SQLite database file**.

- Any application state that can be recorded in a pile-of-files can also be recorded in an SQLite database with a simple key/value schema 
  - CREATE TABLE files(filename TEXT PRIMARY KEY, content BLOB); 
  - it has the advantage of being able to **update individual "files" without rewriting the entire document**.
- An SQLite database can have dozens or hundreds or thousands of different tables, with dozens or hundreds or thousands of fields per table
  - An SQLite database is a more versatile container than key/value filesystem or a ZIP archive. 
- The power of an SQLite database could, in theory, be achieved using a custom file format. 
  - But any custom file format that is as expressive as a relational database would likely require an enormous design specification and many tens or hundreds of thousands of lines of code to implement. 
  - And the end result would be an "opaque blob" that is inaccessible without specialized tools.

- SQLite database as an application file format has compelling advantages
- Simplified Application Development
- Single-File Documents
  - An SQLite database is contained in a single file, which is easily copied or moved or attached. 
  - SQLite does not have any file naming requirements and so the application can use any custom file suffix that it wants to help identify the file as "belonging" to the application.
- High-Level Query Language
- Accessible Content
  - Information held in an SQLite database file is accessible using commonly available open-source command-line tools 
  - It is true that command-line tools such as text editors or "grep" or "awk" are not useful on an SQLite database, 
  - but the SQL query language is a much more powerful and convenient way for examining the content
  - An SQLite database is a well-defined and well-documented file format that is in widespread use
  - The longevity of SQLite database files is particularly important to bespoke(定制的) applications, since it allows the document content to be accessed far in the future
  - Data lives longer than code.
- Cross-Platform
- Atomic Transactions
  - Writes to an SQLite database are atomic.
  - They either happen completely or not at all, even during system crashes or power failures. 
  - So there is no danger of corrupting a document just because the power happened to go out at the same instant that a change was being written to disk.
  - SQLite is transactional, meaning that multiple changes can be grouped together such that either all or none of them occur, and so that the changes can be rolled back if a problem is found prior to commit. 
  - This allows an application to make a change incrementally, then run various sanity and consistency checks on the resulting data prior to committing the changes to disk. 
- Incremental And Continuous Updates
- Easily Extensible
- Performance
  - In addition to being faster for raw read and writes, SQLite can often dramatically improves start-up times because instead of having to read and parse the entire document into memory, the application can do queries to extract only the information needed for the initial screen.
  - As the application progresses, it only needs to load as much material as is needed to draw the next screen
  - This helps keep the memory footprint of the application under control.
  - A pile-of-files format can be read incrementally just like SQLite. 
  - But many developers are surprised to learn that SQLite can read and write smaller BLOBs (less than about 100KB in size) from its database faster than those same blobs can be read or written as separate files from the filesystem.
  - There is overhead associated with operating a relational database engine, however one should not assume that direct file I/O is faster than SQLite database I/O, as often it is not.
  - In either case, if performance problems do arise in an SQLite application those problems can often be resolved by adding one or two `CREATE INDEX` statements to the schema or perhaps running `ANALYZE` one time and without having to touch a single line of application code. 
- Concurrent Use By Multiple Processes
  - SQLite automatically coordinates concurrent access to the same document from multiple threads and/or processes. 
  - Two or more applications can connect and read from the same document at the same time. 
  - SQLite automatically ensures that the low-level format of the document is uncorrupted. 
  - Accomplishing the same with a custom or pile-of-files format, in contrast, requires extensive support in the application. 
  - And the application logic needed to support concurrency is a notorious bug-magnet.
- Multiple Programming Languages
- Better Applications

- Conclusion
  - in many cases, SQLite is a far better choice than either a custom file format, a pile-of-files, or a wrapped pile-of-files. 
  - SQLite is a high-level, stable, reliable, cross-platform, widely-deployed, extensible, performant, accessible, concurrent file format. 
  - It deserves your consideration as the standard file format on your next application design.
# [Riffle: Building data-centric apps with a reactive relational database__202203](https://riffle.systems/essays/prelude/)
- We’re exploring a new way to manage data in apps by storing all app state—including the state of the UI—in a single reactive database. 
  - Instead of imperatively fetching data from the database, the user writes reactive queries that update with fresh results whenever their dependencies change.
- As an initial prototype, we have built a reactive layer around SQLite that populates data in a React app, and used it to build a music library app.
- Even in our limited prototype, we’ve found thinking of apps as queries to be a powerful frame, opening up new approaches to debugging, persistence, and cross-app interoperability.
  - Together, our ideas and experiments suggest that we could take this frame even further. 
  - We sketch a vision for thinking of every layer of an app, from the event log to the pixels on the screen, as pieces of a single large query.
  - Furthermore, we believe that the key components for building such a system already exist, in tools developed for incremental view maintenance and fine-grained provenance tracking.

## Introduction

- Consider a music player app like iTunes. The core user interface is simple: it manages a music collection and displays a variety of custom views organized by various properties like the album, artist, or genre. 
- In data-centric apps, much of the complexity of building and modifying the app comes from managing and propagating state
- We’ve found that state management tends to be a colossal pain. 
  - In a traditional desktop app, state is usually split between app’s main memory and external stores like filesystems and embedded databases, which are cumbersome to coordinate. 
  - In a web app, the situation is even worse: the app developer has to thread the state through from the backend database to the frontend and back. 
  - A “simple” web app might use a relational database queried via SQL, an ORM on a backend server, a REST API used via HTTP requests, and objects in a rich client-side application, further manipulated in Javascript
  - The need to work across all these layers results in tremendous complexity. Adding a new feature to an app often requires writing code in many languages at many layers.
  - To optimize performance, developers must carefully design caching and indexing strategies at every level.

- We think one promising pattern is a local-first architecture where all data is stored locally on the client, available to be freely edited at any time, and synchronized across clients whenever a network is available
  - This architecture allows rich, low-latency access to application state, which could unlock totally new patterns for managing state. 
  - If an app developer could rely on a sufficiently powerful local state management layer, then their UI code could just read and write local data, without worrying about synchronizing data, sending API requests, caching, or other chores of app development.
- what might such a powerful state management layer look like? 
  - It turns out that researchers and engineers have worked for decades on systems that specialize in managing state: databases! 
  - We think that many of the technical challenges in client-side application development can be solved by ideas originating in the databases community. 
  - As a simple example, frontend programmers commonly build data structures tailored to looking up by a particular attribute; databases solve precisely the same problem with indexes, which offer more powerful and automated solutions. 
- In the Riffle project, our goal is to apply ideas from local-first software and databases research to radically simplify app development.
  - In this essay, we start by proposing some design principles for achieving this simplification. 
  - We think that a relational model, fast reactivity, and unified approach that treats all state the same way form a potent trio, which we call the reactive relational model. 
  - We’ve also built a concrete prototype implementing this idea using SQLite and React, and have used the prototype to build some apps that we can actually use.

## Principles

- Declarative queries clarify application structure
- In a local-first application, all the queries can instead happen directly within the client. 
  - This raises the question: how should those queries be constructed? 
  - We suspect that a good answer for many applications is to use a relational query model directly in the client UI.
  - Anyone who has worked with a relational database is familiar with the convenience of using declarative queries to express complex reshaping operations on data. 
  - Declarative queries express intent more concisely than imperative code, and allow a query planner to design an efficient execution strategy independently of the app developer's work.
- This is an uncontroversial stance in backend web development where SQL is commonplace. 
  - It’s also a typical approach in desktop and mobile development—many complex apps use SQLite as an embedded datastore, including Adobe Lightroom, Apple Photos, Google Chrome, and Facebook Messenger.
- However, we’ve observed that the primary use of database queries is to manage peristence: that is, storing and retrieving data from disk. 
- We imagine a more expansive role for the relational database, where even data that would normally be kept in an in-memory data structure would be logically maintained “in the database”. 
  - In this sense, our approach is reminiscent of tools like Datascript and LINQ which expose a query interface over in-memory data structures. 
  - **There’s also a similarity to end-user focused tools like Airtable**: Airtable users express data dependencies in a spreadsheet-like formula language that operates primarily on tables rather than scalar data.

## Fast reactive queries provide a clean mental model

- A reactive system tracks dependencies between data and automatically keeps downstream data updated, so that the developer doesn’t need to manually propagate change. 
  - Frameworks like React, Svelte, and Solid have popularized this style in web UI development, and end-users have built complex reactive programs in spreadsheets for decades.
- However, database queries are often not included in the core reactive loop.
  - When a query to a backend database requires an expensive network request, it’s impractical to keep a query constantly updated in real-time; 
  - instead, database reads and writes are modeled as side effects which must interact with the reactive system. 
  - Many applications only pull new data when the user makes an explicit request like reloading a page; 
  - keeping data updated in realtime usually requires a manual approach to sending diffs between a server and client. 
  - This limits the scope of reactivity: the UI is guaranteed to show the latest local state, but not the latest state of the overall system.
- In a local-first architecture where queries are much cheaper to run, we can take a different approach. The developer can register reactive queries, where the system guarantees that they will be updated in response to changing data.
  - Reactive queries can also depend on each other, and the system will decide on an efficient execution order and ensure data remains updated. 
  - The UI is guaranteed accurately reflect the database's contents, without the developer needing to manage side effects.

- When queries happen locally, they are fast enough to run in the core reactive loop. 
  - In the span of a single frame (16ms on a 60Hz display, or even 8ms on modern 120Hz display), we have enough time to ① write a new track to the database, ② re-run the queries that change because of that new track, and ③ propagate those updates to the UI. From the point of view of the developer and user, there was no intermediate invalid state.
- Low latency is a critical property for reactive systems.
- The database community has spent considerable effort making it fast to execute relational queries; 
  - many SQLite queries complete in well under one millisecond. 
  - Furthermore, there has been substantial work on incrementally maintaining relational queries (e.g., Materialize, Noria, SQLive, and Differential Datalog) which can make small updates to queries much faster than re-running from scratch.

## Managing all state in one system provides greater flexibility

- With a fast database close at hand, this split doesn’t need to exist. What if we instead combined both “UI state” and “app state” into a single state management system? This unified approach would help with managing a reactive query system—if queries need to react to UI state, then the database needs to somehow be aware of that UI state. Such a system could also present a unified system model to a developer, e.g. allow them to view the entire state of a UI in a debugger.

## Prototype system: SQLite + React

- We built an initial prototype of Riffle: a state manager for web browser apps. 
  - For this prototype, our goal was to rapidly explore the experience of building with local data, so we reduced scope by building a local-only prototype which doesn’t do any multi-device sync. 
  - Syncing a SQLite database across devices is a problem others have solved (e.g., James Long’s CRDT-based approach in Actual Budget) so we’re confident it can be done. 
- Our prototype is implemented as a reactive layer over the SQLite embedded relational database. The reactive layer runs in the UI thread, and sends queries to a SQLite database running locally on-device. For rendering, we use React, which interacts with Riffle via custom hooks.
- To run apps in the browser, we run the SQLite database in a web worker and persist data to IndexedDB, using SQL.js and absurd-sql. 
  - We also have a desktop app version based on Tauri (an Electron competitor that uses native webviews instead of bundling Chromium); 
  - in that architecture we run the frontend UI in a webview and run SQLite in a native process, persisting to the device filesystem.
- A first reactive query
  - We can do this declaratively, specifying the tables to join separately from any particular join strategy.
  - Once we’ve written this query, we’ve already done most of the work for showing this particular UI. We can simply extract the results and use a JSX template in a React component to render the data

- Reacting to UI state in the database
- The current sort property and direction represents a new piece of state that needs to be managed in our application.
  - A typical React solution might be to introduce some local component state with the useState hook. 
  - But the idiomatic Riffle solution is to **avoid React state, and instead to store the UI state in the database**.
- Our prototype has a mechanism for storing local state associated with UI components. 
  - **Each type of component gets a relational table, with a schema that defines the local state for that component**. 
  - Each row of the table is associated with a specific instance of the component, identified by a unique ID called the component key.

- Building a more complex app has revealed several challenges. 
  - One issue has been integrating Riffle’s reactive queries with React’s own reactivity in a way that doesn’t create confusion for a developer. 
  - Another challenge has been maintaining low latency even as the app grows in complexity. 
  - Finally, there are many details which matter greatly for day-to-day developer experience, including API design, TypeScript type inference for query results, and schema/migration management.

## Findings

- Structured queries make it easier to understand an app
- Data-centric design encourages interoperability
  - When using the desktop version of our app, the database is stored in a SQLite file on disk which can be opened in a generic SQL tool like TablePlus. 
  - This is helpful for debugging, because we can inspect any app or UI state. 
  - But we can also go even further: we can modify the UI state of the app! 
- Users and developers benefit from unified state
  - We were frequently (and unexpectedly) delighted by the persistent-by-default UI state. 
  - In most apps, closing a window is a destructive operation, but we found ourselves delighted to restart the app and find ourselves looking at the same playlist that we were looking at before
- restarting the app didn’t work as well when the buggy UI state persisted between runs. 
  - We often found ourselves digging through the database to delete the offending rows.
  - in this model, we can decouple restarting the app from resetting the state. Since the system is entirely reactive, we could reset the UI state completely without closing the app.

- SQL is a mediocre language for UI development
- A few key pain points for us were:
  - Standard SQL doesn’t support nesting
  - SQL syntax is verbose and non-uniform. 
  - SQL’s scalar expression language is weird and limited.
  - QL doesn't have good tools for metaprogramming and changing the shape of a query at runtime

- Performance is a challenge with existing tools
- The application developer can model the data conceptually, and it is up to the database to find an efficient way to implement the read and write access patterns of the application. 
- On the bright side, the core database itself has been mostly fast
  - Even running in the browser using WebAssembly, SQLite is fast enough that most queries with a few joins over a few tens of thousands of rows complete in less than a millisecond. 
  - We've had some limited exceptions, which we've worked around for now by creating materialized views which are recomputed outside of the main synchronous reactive loop.
- However, outside of the database proper, we’ve encountered challenges in making a reactive query system that integrates well with existing frontend web development tools in a performant way.
- One challenge has been inter-process communication. 
  - When the reactive graph is running in the UI thread and the SQLite database is on a web worker or native process, each query results in an asynchronous call that has to serialize and deserialize data. 
  - When trying to run dozens of fast queries within a single animation frame, we’ve found that this overhead can become a major source of latency. 
  - One solution we’re exploring is to synchronously run SQLite in the UI thread, and to asynchronously mirror changes to a persistent database.
- Another challenge has been integrating with React. 
  - In an ideal world, a write would result in Riffle fully atomically updating the query graph in a single pass, and minimally updating all the relevant templates. 
  - However, to preserve idiomatic React patterns (like passing component dependencies using props), we've found that it sometimes takes a few passes to respond to an update—a write occurs, Riffle queries update, React renders the UI tree and passes down new props, Riffle queries are updated with new parameters, then React renders the tree again, and so on. 
  - We're still finding the best patterns to integrate with React in a fast and unsurprising way.

## Migrations are a challenge

- In our experience, migrations are a consistent pain when working with SQL databases. 
- However, our prototype created entirely new levels of pain because of the frequency with which our schema changed.
- Our prototype stores all state, including ephemeral UI state that would normally live exclusively in the main object graph, in the database, so any change to the layout of that ephemeral state forced a migration
  - In most cases, we chose to simply delete the relevant tables and recreate them while in development, which essentially recreates the traditional workflow with ephemeral state.

- Of course, Riffle is not the first system to struggle with migrations; indeed, one of us has already done extensive work on migrations for local-first software

## Towards a more radical approach

- In this section, we describe a more radical approach to spreading reactive relational queries further up and down the stack. These ideas are more speculative and we haven’t yet substantiated them with concrete implementations

- View templates as queries
  - So far, in our prototype, we’ve delegated rendering to React. The database’s responsibility ends at updating derived data views; React is responsible for rendering those into view templates and applying updates to the DOM
- What if we removed React (or any other rendering library) from the stack, and used reactive relational queries to directly render view templates?
  - It’s difficult to imagine doing this in a language like SQL, but with a different relational language and a careful approach to templating, it’s plausible. Jamie Brandon has explored this direction in his work on Relational UI.

- CRDTs as queries
- There’s yet another part of the stack that we’ve mostly ignored in this essay. 
  - In many collaborative apps, we need to turn events representing user actions into some base state that’s seen by all users. 
  - One common approach to this step is to use Conflict-Free Replicated Data Types (CRDTs), which ensure that all users see the same state even if their events got applied in different orders
  - Typically, CRDTs are developed for maintaining specific kinds of data structures, by reasoning very carefully about commutativity properties. 
  - However, there’s an elegant idea of representing CRDTs in a more general way: as a declarative, relational query that turns a set of events into a final state—as seen in Martin Kleppmann’s implementation of a text CRDT using Datalog. 

- What might compressing the stack into a query get us?
- If the UI can be expressed in a way that is friendly to one of these automated incremental maintenance, perhaps as a declarative view of the data, we might be able to express user interfaces in a declarative, build-from-scratch way but obtain the performance benefits of incremental updates. Other efforts in this space, like the Incremental and inc-dom libraries, have shown considerable success in these directions.

- Where we’re going
  - we see the outline of an approach where user interfaces are expressed as queries, those queries are executed by a fast, performant incremental maintenance system, 
# ref
- [Optimistic, Offline-First Apps__202001](https://www.swyx.io/svelte-amplify-datastore/)
