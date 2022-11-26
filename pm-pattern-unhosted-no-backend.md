---
title: pm-pattern-unhosted-no-backend
tags: [backend, local-first, unhosted]
created: 2022-11-25T18:11:21.442Z
modified: 2022-11-25T18:11:56.985Z
---

# pm-pattern-unhosted-no-backend

# guide

- [noBackend Solutions](https://nobackend.org/solutions.html)
- [Zero Data App](https://0data.app/)
# solutions

# products

- [logseq: Remote Storage and Sync - Feature Requests - Logseq](https://discuss.logseq.com/t/remote-storage-and-sync/932)
# remoteStorage-docs
- In order to get informed about users connecting their storage, data being transferred, the library going into offline mode, errors being thrown, and other such things, you can listen to the events emitted by the `RemoteStorage` instance, as well as `BaseClient` instances.
  - connected
  - network-offline/online

- rs.js has optional support for syncing data with Dropbox and Google Drive instead of a RemoteStorage server.
  - There are a few drawbacks, mostly sync performance and the lack of a permission model. 

- One of the unique features of rs.js is that users are not required to have their storage connected in order to use the app; you can require connecting storage if it fits your use case.
- The recommended way is to use the private and public BaseClient instances, which are available in so-called data modules.

## api

- A `BaseClient` instance is the main endpoint you will use for interacting with a connected storage: listing, reading, creating, updating and deleting documents, as well as handling incoming changes.

- A `BaseClient` deals with three types of data: folders, objects and files:
  - `getListing` returns a mapping of all items within a folder.
  - `getObject` and `storeObject` operate on JSON objects. Each object has a type.
  - `getFile` and `storeFile` operates on files. Each file has a MIME type.
    - A file is raw data, as opposed to a JSON object 
    - return: Raw data of the document (either a string or an ArrayBuffer)
  - `getAll` returns all objects or files for the given folder path.
  - `remove` operates on either objects or files (but not folders; folders  are created and removed implicitly).

- Conflict Resolution
  - Conflicts are resolved by calling storeObject() or storeFile() on the device where the conflict surfaced.
  - Other devices are not aware of the conflict.
  - If there is an algorithm to merge the differences between local and remote versions of the data, conflicts may be automatically resolved.

## Data modules

- A core idea of the remoteStorage protocol is that the same data can be used by multiple apps.
- A data module is just a JavaScript object containing a module name and a builder function.
- Data types can be defined using the `declareType()` method. 
  - It expects a name (which you can later use with storeObject()), as well as a JSON Schema object defining the actual structure and formatting of your data.
- The recommended way for publishing data modules is as npm packages.

## protocol

- remoteStorage is the first open protocol to enable truly unhosted web apps.
  - That means users are in full control of their precious data and where it is stored

- The remoteStorage protocol is a creative combination of existing protocols and standards (mainly HTTP, CORS, Webfinger, OAuth 2). 
  - It aims to re-use existing technologies as much as possible, adding just a small layer of standardization on top to facilitate its usage for per-user storage with simple permissions and offline-capable data sync.

- Discovery: WebFinger
  - In order for apps to know where to ask permission and later actually sync user data, users give them a user address, basically like with E-Mail or Jabber/XMPP. 
  - With that address, apps retrieve storage information for the username on that domain/host.

- Authorization: OAuth 2.0
  - User data is scoped by so-called categories, which are essentially base directories, for which you can give apps read-only or read/write permission. 
  - Apps will use OAuth scopes to ask for access to one or more categories.
  - If you allow access, the app will retrieve a bearer token, with which it can read and write to your storage, until you revoke that access on your server.

- Data Storage & Sync: HTTP REST
  - remoteStorage defines a simple key/value store for apps to save and retrieve data. 
  - The basic operations are GET/PUT/DELETE requests for specific files/documents.
- the only special feature aside from plain HTTP – there are directory listings, formatted as JSON-LD. 
  - They contain both the content type and size, as well as ETags, which can be used to implement sync mechanisms. 
  - The files and listings themselves also carry ETag headers for sync/caching and conditional requests.

- https://github.com/remotestorage/spec
  - [remoteStorage Protocol Specification](https://datatracker.ietf.org/doc/html/draft-dejong-remotestorage)
  - Each six months (max 185 days), the output is checked using idnits, submitted to the IETF as an Internet Draft
# more
