---
title: docs-web-mozilla-file-directory
tags: [docs, file, web]
created: 2021-01-14T16:28:19.728Z
modified: 2021-01-15T01:29:18.204Z
---

# docs-web-mozilla-file-directory

# guide

- tips
  - 使用浏览器js操作文件的缺点
    - [filesystem api](https://caniuse.com/filesystem)主要由chrome推动开发，firefox和safari支持度都不好
      - 对api的支持度也不够，如firefox和safari都不支持createWriter
    - 需要用户主动使用`<input>`元素选择文件或文件夹，或拖拽指定文件/文件夹
      - `<input type="file">` webkitdirectory设置只能选择文件夹，但目前未进入标准，除ie外都支持
    - 由于浏览器安全性的限制，每次都需要选择文件路径，无法自动读取路径字符串的目录文件
      - 所以chrome extension扩展操作本地文件大多只作为编辑器和预览器
      - 如果要开发类似ide的应用，要随意读写本地文件，推荐用nodejs的api

# discuss

- ## [Local file access with JavaScript](https://stackoverflow.com/questions/371875/local-file-access-with-javascript)
- If the user selects a file via `<input type="file">`, you can read and process that file using the File API.
- Reading or writing arbitrary files is not allowed by design. It's a violation of the sandbox.

# [Introduction to the File and Directory Entries API](https://developer.mozilla.org/en-US/docs/Web/API/File_and_Directory_Entries_API/Introduction)

- The File and Directory Entries API simulates a local file system that web apps can navigate around. 
  - You can develop apps that can read, write, and create files and directories in a sandboxed, virtual file system.
- It was built on the File Writer API, which, in turn, was built on File API. Each of the APIs adds different functionality.

- The API is a better choice for apps that deal with blobs 
  - The File and Directory Entries API offers client-side storage
  - If you are targeting Chrome for your app and you want to store blobs, the File and Directory Entries API and App Cache are your only choices. 
    - However, AppCache storage isn't locally mutable

- examples of how you can use the File and Directory Entries API
  - When a file or directory is selected for upload, you can copy the file into a local sandbox and upload a chunk at a time.
  - pre-fetches assets in the background
  - The app can write to files in place (for example, overwriting just the ID3/EXIF tags and not the entire file).
  - The app can access partially downloaded files
  - The client downloads attachments and stores them locally.

- Before you start using the File and Directory Entries API, you need to understand a few concepts:
- The File and Directory Entries API is a virtual representation of a file system
  - The API doesn't give you access to the local file system, nor is the sandbox really a section of the file system. 
    - Instead, it is a virtualized file system that looks like a full-fledged file system to the web app. 
    - It does not necessarily have a relationship to the local file system outside the browser. 
  - What this means is that **a web app and a desktop app cannot share the same file at the same time**. 
    - The API does not let your web app reach outside the browser to files that desktop apps can also work on. 
    - You can, however, export a file from a web app to a desktop app. 
    - For example, you can use the File API, create a blob, redirect an iframe to the blob, and invoke the download manager.
- The File and Directory Entries API can use different storage types
  - An application can request temporary or persistent storage. 
  - Temporary storage is easier to get, because the browser just  gives it to you, 
    - but it is limited and can be deleted by the browser when it runs out of space. 
  - Persistent storage, on the other hand, might offer you larger space that can only be deleted by the user, but it requires the user to grant you permission.
  - Use temporary storage for caching and persistent storage for data that you want your app to keep—such as user-generated or unique data.
- Browsers impose storage quota
- The File and Directory Entries API has asynchronous and synchronous versions
  - Both versions of the API offer the same capabilities and features. 
  - In fact, they are almost alike, except for a few differences.
  - The synchronous API can be simpler for some tasks. Its direct, in-order programming model can make code easier to read. 
    - The drawback of synchronous API has to do with its interactions with Web Workers, which has some limitations.
- When using the asynchronous API, always use the error callbacks
- The File and Directory Entries API interacts with other APIs
  - XMLHttpRequest (such as the send() method for file and blob objects)
  - Drag and Drop API
  - Web Workers (for the synchronous version of the File and Directory Entries API)
  - The input element (to programmatically obtain a list of files from the element)
- The File and Directory Entries API is case-sensitive
  - The filesystem API is case-sensitive, and case-preserving. 
- Restrictions
  - The File and Directory Entries API adheres to the same-origin policy
  - The File and Directory Entries API does not let you create and rename executable files
  - The file system is sandboxed
    - Because the file system is sandboxed, a web app cannot access another app's files. 
    - You also cannot read or write files to an arbitrary folder (for example, My Pictures and My Documents) on the user's hard drive.
  - You cannot run your app from `file://`
    - This restriction also applies to many of the file APIs, including BlobBuilder and FileReader.

# [File and Directory Entries API](https://developer.mozilla.org/en-US/docs/Web/API/File_and_Directory_Entries_API)

- Two very similar APIs exist depending on whether you desire asynchronous or synchronous behavior. 
  - The synchronous API is intended to be used inside a Worker and will return the values you desire. 
  - The asynchronous API will not block and functions and the API will not return values; 
    - instead, you will need to supply a callback function to handle the response whenever it arrives.

- The Firefox implementation of the File and Directory Entries API is very limited; 
  - there is no support for creating files. 
    - Content scripts can't create file systems or initiate access to a file system. 
    - There are only two ways to get access to file system entries at this time
      - Only for accessing files which are selected by the user in a file `<input>` element 
      - or when a file or directory is provided to the Web site or app using drag and drop.
  - Firefox does not implement the synchronous API. 
    - Any interfaces with names that end in `Sync` aren't available.
  - Firefox only supports reading from files in the file system. 
    - **You can't write to them**. 
    - In particular, the `FileSystemFileEntry.createWriter()` method, used to create a `FileWriter` to handle writing to a file, is not implemented and will just treturn an error.

- There are two ways to get access to file systems defined in the current specification draft:
  - When handling a `drop` event for drag and drop, you can call `DataTransferItem.webkitGetAsEntry()` to get the `FileSystemEntry` for a dropped item. 
    - If the result isn't `null`, then it's a dropped file or directory, 
    - and you can use file system calls to work with it.
  - The `HTMLInputElement.webkitEntries` property lets you access the `FileSystemFileEntry` objects for the currently selected files, 
    - but only if they are dragged-and-dropped onto the file chooser. 
    - If `HTMLInputElement.webkitdirectory` is true, the `<input>` element is instead a directory picker, 
    - and you get `FileSystemDirectoryEntry` objects for each selected directory.

- The asynchronous API should be used for most operations, 
  - to prevent file system accesses from blocking the entire browser if used on the main thread. 

# [FileSystem](https://developer.mozilla.org/en-US/docs/Web/API/FileSystem)

- FileSystem is used to represent a file system. 
  - These objects can be obtained from the `filesystem` property on any file system entry.
- This interface will not grant you access to the users filesystem. 
  - Instead you will have a "virtual drive" within the browser sandbox. 
  - If you want to gain access to the users filesystem you need to invoke the user by eg. installing a Chrome extension. 

# [LocalFileSystem](https://developer.mozilla.org/en-US/docs/Web/API/LocalFileSystem)

- gives you access to a sandboxed file system.  
  - The methods are implemented by window and worker objects.

# [FileSystemEntry](https://developer.mozilla.org/en-US/docs/Web/API/FileSystemEntry)

- represents a single entry in a file system. 
  - The entry can be a file or a directory
- It includes methods for working with files—including copying, moving, removing, and reading files—as well as information about a file it points to—including the file name and its path from the root to the entry.
- You don't create `FileSystemEntry` objects directly. 
  - Instead, you will receive an object based on this interface through other APIs. 
  - This interface serves as a base class for the `FileSystemFileEntry` and `FileSystemDirectoryEntry` interfaces

# ref

- [Access Local Files using a Google Chrome Extension](https://stackoverflow.com/questions/21912056/access-local-files-using-a-google-chrome-extension)
- [Open local files(file://) using Chrome](https://stackoverflow.com/questions/28724751/open-local-filesfile-using-chrome)
  - The answer is that you can't  and more importantly you shouldn't.
    - Chrome behavior is in fact the right behavior 
    - and it protects you from having malicious users and/or scripts accessing your local resources.
