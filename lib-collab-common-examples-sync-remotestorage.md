---
title: lib-collab-common-examples-sync-remotestorage
tags: [data-sync, examples, indexeddb, remotestorage, synchronization, toc]
created: 2022-11-25T17:19:25.386Z
modified: 2023-01-18T17:04:25.234Z
---

# lib-collab-common-examples-sync-remotestorage

# guide

- rs protocol defines a simple key/value store for apps to save and retrieve data
  - 提供的同步方式偏向于类似文件系统，如google-drive/dropbox
  - 不偏向关系数据库

- 参考sqlite+http-range的部分下载示例(sql.js-httpvfs)

- [remoteStorage Protocol: defines a simple key/value store for apps to save and retrieve data](https://remotestorage.io/protocol/)
- [remoteStorage Apps](https://remotestorage.io/apps/)
# blogs
- [Local-first database: remoteStorage.js | Jared Forsyth.com_202005](https://jaredforsyth.com/posts/local-first-database-remotestorage/)
  - Conflicts are not automatically handled – they must be dealt with (or not) by the client using bespoke conflict merging code. 
  - If two clients change the same document, whichever client syncs to the server first wins, and the second one gets an “conflict event” when it tries to sync. A particularly clever client imeplementation could use a `json-crdt` to encode the data, and thereby automatically handle merge conflicts without developer or user intervention 🤔 but I haven’t seen anyone try that yet.
  - remoteStorage occupies an interesting place in my mind. On the one hand, it’s an 8 year old project that still receives active maintenance, which is a pretty big achievement in and of itself. On the other hand, its simplicity means that it’s lacking a lot of features that people have come to expect from modern web applications. Overall, given that it’s still actively being developed, it could very well gain some of those features and become a strong solution for building modern local-first apps in the future.
# popular
- remotestorage.js /2.2kStar/MIT/202311/ts
  - https://github.com/remotestorage/remotestorage.js
  - https://remotestoragejs.readthedocs.io/
  - https://remotestorage.io/
  - a JavaScript library for storing user data locally in the browser, as well as connecting to remoteStorage servers and syncing data across devices and applications.
  - It is also capable of connecting and syncing data with a person's Dropbox or Google Drive account (optional).
  - The first prototype of rs.js was written in November 2010. The library is well-tested and actively maintained.

- https://github.com/FrigadeHQ/remote-storage /186Star/MIT/202401/ts
  - https://remote.storage/
  - a simple library that combines the localStorage API with a remote server to persist data across browsers and devices.
  - Simple API (same as localStorage)
  - Open source server and client
  - How is remoteStorage different from localStorage?
    - localStorage is a browser API that allows you to store data in the browser. The data is stored locally on the user's device and is not shared across devices or browsers. 
    - remoteStorage is a library that combines the localStorage API with a remote server to persist data across browsers and devices.

- https://github.com/remotestorage/myfavoritedrinks
  - https://myfavoritedrinks.remotestorage.io/
  - Example of a simple remoteStorage-enabled app using a custom data module

- https://github.com/DougReeder/notes-together /202210/js
  - https://notestogether.hominidsoftware.com/
  - A web app for taking notes (or copied snippets of text or pictures) and recalling them by context: any words in them, or the date.
  - Data is backed-up and synced with other devices using the remoteStorage protocol, so you control where your data is stored.

- https://github.com/silexlabs/unifile /202101/js/采用文件api
  - http://projects.silexlabs.org/unifile/
  - Unified access to cloud storage services through a simple web API.
  - Unifile use an API similar to the native `fs` module but with Bluebird Promises instead of callbacks.
  - Most of the service in Unifile uses OAuth 2 to connect the user into the service. This means Unifile doesn't have the user credential at any time.
  - 依赖bluebird
  - Currently supported services
    - FTP
    - SFTP
    - Dropbox
    - GitHub: use git as a cloud with repository and branches as folder
    - RemoteStorage
    - WebDAV
    - Local filesystem (might be useful to copy from your drive to your cloud)

- https://github.com/sonnyp/remoteStorage
  - Playing around with remoteStorage, eventually releasing a lightweight library

- https://github.com/anita-app/anita /ts/暂不支持同步
  - https://anita-app.com/
  - Anita is a private, no-server, powerful and fully customizable data management solution
  - Your data is stored on your computer in a JSON file and/or on a remote database of your choice: flexible, open & no lock-in. Stay independent from servers that will go away, sooner or later.
  - full support for CRUD operations on data stored
  - locally in the browser's IndexedDB (with Dexie.js)
  - locally in a JSON or SQLite file in the device FS 
# server
- https://github.com/remotestorage/armadietto
  - a RemoteStorage server written for Node.js.
  - armadietto supports pluggable storage backends, and comes with a file system implementation out of the box (redis storage backend is on the way in feature/redis branch):

- https://github.com/overhide/lucchetto
  - Client side JavaScript helper utilities for working with remotestorage/armadietto servers' token metadata -- servers extended with the pay2my.app extension and others.
- https://github.com/overhide/armadietto
  - Lucchetto is an extended Armadietto to allow authentication, authorization, and in-app-purchases through the open source https://pay2my.app ecosystem.
# examples
- https://github.com/kolism/obsidian-sync-remotestorage
  - Sync obsidian to/from a remotestorage server. 
  - Optionally enable public facing documents and images

- https://github.com/ssisk/mercato
  - Mercato is an app platform (similar to an app store) 
  - Mercato runs your apps inside of a privacy sandbox, where the apps cannot communicate to anywhere on the internet. 
  - The tradeoff is that Mercato can't run some types of apps that require data to be sent over the internet. 

- https://github.com/raucao/sharesome
  - share files quickly from your own remote storage account.
  - 依赖ember

- https://github.com/vcuculo/ghost /201504/js
  - Experimental web app using WebRTC and remoteStorage.js
# more
- https://github.com/0dataapp/0datawrap
  - Unified JavaScript API for Fission + remoteStorage.

- https://github.com/raucao/rs-backup
  - This program allows you to backup your data from a remoteStorage account to a local hard drive and restore it to the same or another account or server.

- https://github.com/relet/python-remotestorage
  - An implementation of remotestorage for Python, using a git backend.
