---
title: web-filesystem-opfs
tags: [filesystem, opfs, web]
created: 2023-01-12T10:26:26.166Z
modified: 2023-01-12T10:26:41.060Z
---

# web-filesystem-opfs

# guide

# opfs-api
- window.showDirectoryPicker()
  - displays a directory picker which allows the user to select a directory
  - This feature is available only in secure contexts (HTTPS), in some or all supporting browsers.
# blogs
- [The origin private file system  |  web.dev](https://web.dev/articles/origin-private-file-system)

- [Origin Private File System (OPFS)](https://github.com/web-platform-tests/interop/issues/172)
  - The OPFS is what powers, among other things, Photoshop on the Web.
  - [Photoshop's journey to the web_202110](https://web.dev/ps-on-the-web/)

- [The origin private file system - Chrome Developers](https://developer.chrome.com/articles/origin-private-file-system/)
  - https://glitch.com/edit/#!/sqlite-wasm-opfs

- [Let installed web applications be file handlers - Chrome Developers](https://developer.chrome.com/en/articles/file-handling/)

- [What is the Databricks File System (DBFS)?](https://docs.databricks.com/en/dbfs/index.html)
  - The Databricks File System (DBFS) is a distributed file system mounted into a Databricks workspace and available on Databricks clusters. 
  - DBFS is an abstraction on top of scalable object storage that maps Unix-like filesystem calls to native cloud storage API calls.
# docs

## [File System Access API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API)

- This API allows interaction with files on a user's local device, or on a user-accessible network file system.
- Core functionality of this API includes reading files, writing or saving files, and access to directory structure.

- Most of the interaction with files and directories is accomplished through handles. 
- The handles represent a file or directory on the user's system. 
  - You can first gain access to them by showing the user a file or directory picker using methods such as `window.showOpenFilePicker()` and `window.showDirectoryPicker()`. 
  - Once this happens successfully, a handle is returned.

- Objects based on FileSystemHandle can also be serialized into an IndexedDB database instance, or transferred via postMessage().

- The origin private file system (OPFS) is a storage endpoint private to the origin of the page, 
  - providing optional access to a special kind of file that is highly optimized for performance, 
  - for example, by offering in-place and exclusive write access to a file's content.

- Storing data in the OPFS is similar to storing data in any other browser-provided storage mechanism that's private to the origin of the page (for example the IndexedDB API).

- 💡 This means that files in the OPFS differ from files selected using a picker in the following ways:
  - Permission prompts are not required to access files in the OPFS.
  - Clearing data for the site deletes the OPFS.
  - The OPFS is subject to browser quota restrictions.

- Files can be manipulated inside the OPFS via a three-step process:
  - navigator.storage.getDirectory() 
  - FileSystemDirectoryHandle.getFileHandle()
  - createSyncAccessHandle()

- `FileSystemSyncAccessHandle` object that can be used to read and write to the file. 
  - This is a high-performance handle for synchronous read/write operations (the other handle types are asynchronous). 
  - The synchronous nature of this class brings performance advantages intended for use in contexts where asynchronous operations come with high overhead (for example, WebAssembly). 
  - Note that it is only usable inside dedicated Web Workers.
- Writes performed using `FileSystemSyncAccessHandle.write()` are in-place, meaning that changes are written to the actual underlying file at the same time as they are written to the writer. 
  - This is not the case with other writing mechanisms available in this API (e.g. `FileSystemFileHandle.createWritable()`), where changes are not committed to disk until the writing stream is closed.

- While browsers typically implement this by persisting the contents of the OPFS to disk somewhere, it is not intended that the contents be easily user-accessible.
  - While the browser might make it seem that there are files, they might be stored in a database or any other data structure. 

- 
- 
- 
- 
- 

# compatibility

## [chrome: SQLite Wasm in the browser backed by the Origin Private File System_202301](https://developer.chrome.com/blog/sqlite-wasm-in-the-browser-backed-by-the-origin-private-file-system/)

- To debug SQLite Wasm's Origin Private File System output, use the OPFS Explorer Chrome extension.

- https://github.com/tomayac/opfs-explorer
  - https://tomayac.github.io/opfs-explorer/

- ### [SQLite Wasm in the browser backed by the Origin Private File System | Hacker News_202301](https://news.ycombinator.com/item?id=34352935)
- what is exactly the use case for this?
  - It's an alternative to using IndexedDB which is a browser provided API.
  - On use cases, you can give your web app offline support by locally caching data in an SQL database and have it be fully queryable.
  - A design pattern that is beginning to emerge is "offline/local first". You design your app to fundamentally work offline, using things such as this, and the server component only works to synchronise clients. It's a bit like the design move to "mobile first" that happed 10 years ago, but going to another level.

- The blog post on absurd-sql notes that it's a hacky solution that would be improved with file system access; it references the old Storage Foundation proposal, which has since evolved into the current File System Access API proposal(s).

## [safari: The File System Access API with Origin Private File System | WebKit_202202](https://webkit.org/blog/12257/the-file-system-access-api-with-origin-private-file-system/)

- the origin private file system — a private storage endpoint to some origin
- It is available in Safari on: macOS 12.2 and above iOS 15.2 and above
- Based on the implementation of different browsers, one entry in the origin private file system does not necessarily map to an entry in the user’s local filesystem — it can be an object stored in some database. 
- 👀 That means a file or directory created via the File System Access API may not be easily retrieved from outside of the browser.
- If your web app needs to interact with files, you should try the new File System Access API. It provides interfaces that are similar to the native file system API, with optimized performance.

## ✨ [Safari now supports File System Access API with private origin | Hacker News_202202](https://news.ycombinator.com/item?id=30394737)

- This is brilliant! Being called a “file system access” api will confuse many people into thinking it’s about traditional file storage for “people” to use, like a file picker/save dialog. 
  - 👉🏻 It’s not, this is about providing a block storage that can be used for other things.
  - The one I am most excited by is for persistent SQLite with proper acid transaction in the browser, not having to load the whole db into memory. 
  - Absurd SQL currently does this by creating a VFS on top of IndexedDB.

- Many new in browser DB engines are going to get built on top of this. Others that I could see happing are:
  - Realm from MongoDB being ported to WASM and use this for storage.
  - If I were Supabase I would be looking to create a “Mini Supabase” for mobile, and make it work in browser too.
  - Couchbase Mobile as an alternative to PouchDB

- This is brilliant! Being called a “file system access” api will confuse many people into thinking it’s about traditional file storage for “people” to use, like a file picker/save dialog. It’s not, this is about providing a block storage that can be used for other things.
  - I don’t see how this is fundamentally any different from IndexedDB: both are asynchronous transactional key-value databases. One is byte-oriented and the other object-oriented, but it looks to me like they’re essentially completely equivalent in what’s possible with them—except insofar(到这种程度) as File System Access may allow you to avoid loading the entire thing into memory. 
  - Implementing SQLite on top of this would require that a commit write the changes, close the file, and then reopen it, since writes are only performed when you close the file. That could perform tolerably or terribly (there’s no way of knowing), but certainly won’t be as good as what you get natively, where you can truly write only part of a file, especially once you get to large databases where it will certainly be drastically slower. If you want performance out of any of these sorts of things, you’re going to need to stop putting everything in one “file” and split it into many, so that you can avoid touching most of them on most writes.
- I’m aware the spec is somewhat a moving target. 
  - The point of this over “abusing” IndexedDB, jlongster who created Absurd SQL had to perform some pretty unholy hacks to get it to work. When porting these db engines to WASM they expect a FS to look and behave like a FS, that’s what this does that IndexedDB doesn’t.
  - Quite true you could build a new SQL/DB engin on top of IndexedDB with a storage architecture designed for it. But that’s not what the existing engines are expecting.
- This FS doesn’t much look like an FS either—certainly it’s way off what SQLite needs. For mutating a file, you get the options write, seek, and truncate, but they don’t do anything until you close the file. It’s essentially equivalent to the write-to-a-temporary-file-and-then-atomic-rename-overwrite pattern.
  - You can implement exactly the same thing on top of an `ArrayBuffer` that you’ll put in an IndexedDB with no fuss—and if you were doing it that way, then you could even decide whether to go for something like a rope for intermediate editing, or mutating the `ArrayBuffer` directly, whereas if you use FSA you have no control over which of the two approaches it might use, or something else altogether.

- For Origin Private File Systems, I would not expect any user agent to map things to the actual file system: there are notable functional problems especially on Windows, and it’s a very significant security hazard(危险；危害), all of which is neatly avoided by putting it all in the likes of a SQLite database.
- First, the functional problems: 
  - file names are going to be a bit of a bother, to the point where if you back it by the actual file system you will require some kind of escaping mechanism, which loses you the exact one-to-one correspondence. 
  - Names are sequences of 16-bit code units, which means they need not be valid Unicode (ugh, I wish new additions to the browser platform would just start rejecting malformed Unicode), which will cause trouble on some platforms and will probably not be looked on favourably on others as having the potential to cause trouble in software not written to cope with that (e.g. on Windows I don’t think I’ve ever encountered a name with an unpaired surrogate, though it’s legal; on Linux, paths that aren’t UTF-8 are decidedly more common, though they still have a habit of breaking things). 
  - It also allows various file names that are forbidden in Windows at large, though in almost all cases you could with difficulty work around that on a per-process basis by throwing it into POSIX mode and/or using fully qualified (\\.\ or \\?\) paths.
- Second, the security hazard: 
  - putting files with arbitrary names and contents on the file system is dangerous for a few reasons. 
  - The simplest is that there’s various buggy software that automatically reads files that get added to the file system, and more than a few times such software has had bugs in parsers that have led to privileged arbitrary code execution. 
  - A key purpose of Origin Private File Systems is that you don’t need to prompt the user for permission, because it’s supposed to be safe. 
  - I have no idea if this sort of vector was ever used back in the days when IE persisted its internet cache directly to files on the disk, but I can easily imagine such a thing happening now, and it could be really bad, given the right bug.

- I didn't notice before that this was supposed to be a safe api usable without permission, that indeed changes things.

- the Origin Private File System is basically just a file system implemented atop a database: it doesn’t provide any new fundamental functionality, but can be shimmed perfectly atop IndexedDB (though performance characteristics will probably differ). 
  - It doesn’t put things in a private folder so that you could open its contents in other locally-installed apps.
  - The only real reasons I can think of straight away for it potentially being useful are (a) if it performs better than IndexedDB, and (b) for simpler API compatibility with something using the dangerous parts of File System Access, which Chromium has implemented but which Firefox and Safari are both utterly rejecting.

- I wonder how symlinks work in this context.
  - Not applicable; Private Origin File Systems are just a key-value store made to look a bit like a file system, and symlinks don’t exist.
  - only Google has implemented that—Mozilla and Apple have strongly rejected it as a currently-unfixable security hazard
