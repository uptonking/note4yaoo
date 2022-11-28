---
title: lib-db-filesystem-web
tags: [db, filesystem, indexeddb]
created: 2022-11-27T14:19:27.900Z
modified: 2022-11-27T14:20:27.098Z
---

# lib-db-filesystem-web

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
# blogs

## [The File System Access API: simplifying access to local files](https://web.dev/file-system-access/)

- The File System Access API (formerly known as Native File System API and prior to that it was called Writeable Files API) enables developers to build powerful web apps that interact with files on the user's local device, such as IDEs, photo and video editors, text editors, and more.
  - After a user grants a web app access, this API allows them to read or save changes directly to files and folders on the user's device.

- The origin private file system is a storage endpoint that, is private to the origin of the page.
  - While the browser might make it seem that there are files, internally—since this is an origin private file system—the browser might store these "files" in a database or any other data structure. 
  - if you use this API, do not expect to find the created files matched one-to-one somewhere on the hard disk. 
  - You can operate as usual on the origin private file system once you have access to the root `FileSystemDirectoryHandle`.
