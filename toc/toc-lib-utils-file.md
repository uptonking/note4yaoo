---
title: toc-lib-utils-file
tags: [file, filesystem, toc, utils]
created: 2023-04-05T19:34:59.260Z
modified: 2023-04-05T19:35:14.347Z
---

# toc-lib-utils-file

# guide

# popular
- https://github.com/eligrey/FileSaver.js /js
  - An HTML5 saveAs() FileSaver implementation
  - FileSaver.js is the solution to saving files on the client-side, and is perfect for web apps that generates files on the client, 
  - However if the file is coming from the server we recommend you to first try to use `Content-Disposition` attachment response header as it has more cross-browser compatibility.

- https://github.com/jimmywarting/StreamSaver.js /js
  - the solution to saving streams in the web browser. 
  - It is perfect for web apps where there's a need to save large amounts of data on devices with e.g. limited RAM.
  - This is accomplish by emulating how a server would instruct the browser to save a file using some response header + service worker
  - there is this new native way to save files to the HD:
    - https://github.com/whatwg/fs
  - I also built native-file-system-adapter so you can have it in all Browsers, Deno, and NodeJS with different storages
- https://github.com/jimmywarting/native-file-system-adapter /MIT/202407/js
  - This is a file system API that follows the File System Access specification. 
  - Thanks to it we can have a unified way of handling data in all browsers and even in NodeJS & Deno in a more secure way.

- https://github.com/streamich/memfs /apache2/ts
  - JavaScript file system utilities for Node.js and browser.
  - This demo shows how to run isomorphic-git on memfs in-memory file system.
# file-upload
- https://github.com/transloadit/uppy /MIT/202503/ts
  - https://uppy.io/
  - modular JavaScript file uploader that integrates seamlessly with any application
  - Fetch files from local disk, remote URLs, Google Drive, Dropbox, Box, Instagram or snap and record selfies with a camera
  - Preview and edit metadata with a nice interface
  - Upload to the final destination, optionally process/encode
  - Resumable file uploads via the open [tus](https://tus.io/) standard, so large uploads survive network hiccups
  - https://github.com/tus/tus-node-server

- https://github.com/johndatserakis/file-upload-with-preview /ts/框架无关
  - Simple file-upload utility that shows a preview of the uploaded image. 
  - Written in TypeScript. No dependencies.

- https://github.com/pqina/filepond /MIT/202503/js/NoDeps
  - https://pqina.nl/filepond/
  - A flexible JavaScript file upload library that can upload anything you throw at it, optimizes images for faster uploads, and offers a great, accessible, silky smooth user experience.
  - Accepts directories, files, blobs, local URLs, remote URLs and Data URIs.
  - Drop files, select on filesystem, copy and paste files, or add files using the API.
  - Async uploading with AJAX, or encode files as base64 data and send along form post.
  - Image optimization, automatic image resizing, cropping, and fixes EXIF orientation.
  - https://github.com/pqina/react-filepond
    - a handy wrapper component for FilePond
  - https://github.com/wladiston/filepond-server-example
    - FilePond Server example using Express and AWS
  - https://github.com/shahnawaz-pabon/File-Upload-With-Multer
    - Uploading files with Multer in Node

- https://github.com/FineUploader/fine-uploader /201811/js
  - Multiple file upload plugin with image previews, drag and drop, progress bars. 
  - Dependency-free
  - [Fine Uploader is shutting down](https://github.com/FineUploader/fine-uploader/issues/2073)
  - https://github.com/FineUploader/server-examples
    - Server-side examples for the Fine Uploader library
    - Traditional upload examples (upload to your own server): java, nodejs, php, python
    - Fine Uploader S3/Azure examples

- https://github.com/elninotech/uppload /MIT/202308/ts
  - https://uppload.js.org/
  - JavaScript image uploader and editor, no backend required
  - It's highly customizable with 30+ plugins

## file-upload-utils

- https://github.com/shadowings-zy/easy-file-uploader
  - 开箱即用的大文件分片上传库

- https://github.com/beforegolive/resumable-upload-demo
  - 断点续传的demo
  - [web端断点续传的思路和实现 | 上线前夕](https://www.twomeetings.com/2020-06-11-how-to-implement-resumable-upload/)

- https://github.com/HiWayne/large-file-uploader
  - 专为上传功能而优化，file uploader, supporting file segmentation, resume from break point, offline storage...
  - 断点续传，不必重头再来
  - 基于 indexedDB 的文件缓存，离线也能恢复进度
  - 多线程计算，面对大文件处理更快
  - 只提供下载队列的状态数据，你可以自由定制 UI
  - 丰富的配置，你可以限制文件类型、每个切片大小、线程数、请求并发数、是否开启离线缓存等

- https://github.com/diced/zipline /ts
  - A ShareX/file upload server that is easy to use, packed with features, and with an easy setup!
  - Built with Next.js & React
  - Gallery viewer, and multiple file format support
  - File Chunking (for large files)
  - Automatic video thumbnail generation
- https://github.com/TannerReynolds/ShareX-Upload-Server /js
  - Feature full & Stable ShareX and file server in node. Includes images, videos, code, text, markdown rendering, password protected uploads, logging via discord, administration through Discord, url shortening, and a full front end. Use standalone or via reverse proxy

- https://github.com/sailshq/skipper /202109/js
  - Streaming multi-uploads for Sails/Express - supports disk, S3, gridfs, and custom file adapters

- https://github.com/Vinnu1/express-mongodb-storefiles-nogridfs /201902/js
  - App to upload and store files in mongodb without using gridfs.
  - Upload image, audio/video files upto 16 mb.

- https://github.com/ProgerXP/FileDrop /202304/js/NoDeps
  - Self-contained cross-browser pure JavaScript class for Drag & Drop and AJAX (multi) file upload
  - Flexible event system with over 15 callbacks
# opfs/Origin Private File System
- [chromium sqlite3-api-opfs.js](https://www.blick-newwsch.com/?_=%2Fexternal%2Fgithub.com%2Fsqlite%2Fsqlite%2F%2B%2Frefs%2Fheads%2Fopfs-lock-without-xlock%2Fext%2Fwasm%2Fapi%2Fsqlite3-api-opfs.js%23Zn%2F56Y4trIg2C2EYQD%2F9g5ZYfX%2BnMC3zulsbohqB0K9j)
  - This file holds the synchronous half of an sqlite3_vfs
  implementation which proxies, in a synchronous fashion, the
  asynchronous Origin-Private FileSystem (OPFS) APIs using a second
  Worker, implemented in sqlite3-opfs-async-proxy.js.

- https://github.com/hughfenghen/opfs-tools /MIT/202404/ts
  - https://hughfenghen.github.io/opfs-tools-explorer/
  - 在浏览器中运行的简单、高性能、完备的文件系统 API，基于 OPFS 构建
  - [Web文件系统（OPFS 及工具）介绍 | 风痕 · 術&思](https://hughfenghen.github.io/posts/2024/03/14/web-storage-and-opfs/)
  - https://github.com/hughfenghen/opfs-tools-explorer /MIT/202403/ts
    - Manage OPFS assets in your web site, supporting file creation, copying, and moving features, providing a user-friendly interactive experience.
    - 支持创建文件夹、文件，支持编辑文本
    - The basic file operation capabilities are provided by opfs-tools.

- https://github.com/wariasar/opfs
  - https://v22018096896673253.goodsrv.de/opfs/
  - This is just a test for the OPFS feature in Webbrowsers. 

- https://github.com/kevin-daniel-hunt/opfs-sqlite-poc
  - This small project will setup a frontend and backend environment for serving mock data through a websocket from an express server to a webworker on the frontend (React + Vite) which will store the data using sqlite.wasm and OPFS.

- https://github.com/nmeibergen/bare-sqlite-opfs
  - This is a bare minimum package to run Sqlite with OPFS in a worker.

- https://github.com/jvilk/BrowserFS /MIT/202309/ts
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
  - 支持 memory/localStorage/indexeddb/dropbox/Emscripten file systems
  - [File System Access Backend by DustinBrett](https://github.com/jvilk/BrowserFS/pull/321)
    - I won't be using it by default in my project with OPFS instead of IndexedDb because it has other limits such as not allowing the making of `.url` files. 
    - I also wrote a benchmark and found it interesting that OPFS was not faster. But maybe this could be improved in the code I wrote

- https://github.com/tomayac/opfs-explorer
  - OPFS Explorer is a Chrome DevTools extension that allows you to explore the Origin Private File System (OPFS) of a web application.

- https://github.com/qwtel/sqlite-viewer-vscode  /ts
  - https://sqliteviewer.app/
  - easy SQLite viewer for VSCode, inspired by DB Browser for SQLite and Airtable.
  - [Next version of SQLite Viewer, handling 3 million rows, 1 GB sqlite file, in a browser.](https://twitter.com/qwtel/status/1639204056622321664)
    - Memory usage low despite 1GB file, thanks to OPFS and SQLite WASM
  - [Opening large SQLite files is solved in the (unreleased) web version though.](https://twitter.com/qwtel/status/1644319722178248708)
    - The limit is now how much the browser permits to write into the Origin Private File System.
  - I'm surprised the current version of SQLite Viewer keeps getting good reviews in the vsc marketplace. It flat out crashes if you open a large file. I suppose most sqlite files are small.
    - Unfortunately fixing it would be hard. 
    - vsc's own `fs` module doesn't let you read with random offsets, and even if it did, it would require writing a custom VFS and juggling buffers across 2-3 layers of iframes and workers.

- https://github.com/ncisrc/opfs /js
  - A class based connector to the browser Origin Private File System API
# file-parser/generator
- https://github.com/plantain-00/js-split-file
  - A library to split big file to small binary data for nodejs and browsers.

- https://github.com/jimsmart/peanut /202301/go
  - a Go package to write tagged data structs to disk in a variety of formats, simply and without ceremony.
  - Its primary purpose is to provide a single consistent interface for easy, ceremony-free persistence of record-based struct data.
  - Currently supported formats are CSV, TSV, Excel (.xlsx), JSON Lines (JSONL), and SQLite. Additional writers are also provided to assist with testing and debugging. 
  - All writers perform atomic file operations, writing data to a temporary location and moving it to the final output location when Close is called.
# file-server
- https://github.com/vercel/serve /ts
  - serve helps you serve a static site, single page application or just a static file
  - It also provides a neat interface for listing the directory's contents
  - [how to add prefix _202003](https://github.com/vercel/serve/issues/584)
  - [i hope the serve can add proxy feature _201801](https://github.com/vercel/serve/issues/315)
    - To customize serve's behavior, create a `serve.json` file in the public folder 
    - Simply add `redirects` or `rewrites` to your config file, as described in the serve-handler documentation
  - https://github.com/vercel/serve-handler /MIT/202410/js
    - This package represents the core of serve. It can be plugged into any HTTP server and is responsible for routing requests and handling responses.

- https://github.com/http-party/http-server /js
  - a simple zero-configuration command-line http server

- https://github.com/teclone/r-server
  - NodeJS production ready web-server with inbuilt routing-engine, static file server, file upload handler, request body parser, middleware support and lots more

- https://github.com/lwsjs/local-web-server /js
  - A lean, modular web server for rapid full-stack development.
  - Supports HTTP, HTTPS and HTTP2.
  - Running ws without any arguments will host the current directory as a static web site.

- https://github.com/cloudhead/node-static
  - rfc 2616 compliant HTTP static-file server module, with built-in caching.

- https://github.com/jfhbrook/node-ecstatic
  - [ecstatic's Past, Present and Future](https://github.com/jfhbrook/node-ecstatic/issues/259)
  - My initial version was really bad - a 30 line call to readFile

- https://github.com/Arlen22/TiddlyServer
  - A static file server that can also save files and mount TiddlyWiki folders

- https://github.com/dbohdan/caddy-markdown-site
  - Serve Markdown files as HTML pages with CSS using just Caddy

- https://github.com/YousefED/filebridge /ts
  - FileBridge is a simple server to interact with a directory on your local file system.
  - FileBridge exposes filesystem events (provided by Chokidar) over WebSockets.
# file-folder-dir-scan-watch
- 文件编辑浏览的实现思路
  - edit > ~~save(内存或本地)~~ > render
  - 文件逐个处理

- `fs.watch(filename[, options][, listener])`.
  - Watch for changes on `filename`, where `filename` is either a file or a directory.
  - The `listener` callback gets two arguments (eventType, filename). `eventType` is either 'rename' or 'change', and `filename` is the name of the file which triggered the event.
  - The `fs.watch` API is not 100% consistent across platforms, and is unavailable in some situations.
  - If the underlying functionality is not available for some reason, then fs.watch() will not be able to function and may thrown an exception.
  - It is still possible to use `fs.watchFile()`, which uses stat polling, but this method is slower and less reliable.

- `fs.watchFile(filename[, options], listener)`.
  - Watch for changes on `filename`.
  - The callback listener will be called each time the file is accessed.
  - The `listener` gets two arguments the current stat object and the previous stat object(instances of fs. Stat)
  - To be notified when the file was modified, not just accessed, it is necessary to compare `curr.mtime` and `prev.mtime`.
  - `fs.watch()` is more efficient than `fs.watchFile` and fs.unwatchFile

- nodemon
  - is a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.
  - [Don’t use nodemon, there are better ways!](https://codeburst.io/dont-use-nodemon-there-are-better-ways-fc016b50b45e)
    - Solution: don’t restart the server
    - use `chokidar` to watch the files
  - I am generally not a fan of nodemon as a workflow for basically this reason.
    - If I'm in a sandbox usually fine to 'hot load' and run whatever code on save.
    - If I'm in node, I always want manual control over *what* changes run and *when*.
  - In fact I don't even use nodemon on my machine.
    - It always leaves zombie processes running on my machine.
    - I have to kill them manually by looking them up by opened port.

- https://github.com/paulmillr/chokidar
  - file watcher used in MS VSCode.
  - Minimal and efficient cross-platform file watching library
  - On MacOS, chokidar by default uses a native extension exposing the Darwin `FSEvents` API.
  - On most other platforms, the `fs.watch`-based implementation is the default, which avoids polling and keeps CPU usage down.
  - [Watching file over network _201507](https://github.com/paulmillr/chokidar/issues/315)
    - With nfs mounting and `UsePolling: true` it is working.

- https://github.com/facebook/watchman /13.1kStar/MIT/cpp/python/rust
  - https://facebook.github.io/watchman/
  - Watchman exists to watch files and record when they actually change. 
  - It can also trigger actions (such as rebuilding assets) when matching files change.
  - support: Windows and macOS builds, Linux builds on recent Ubuntu and Fedora releases
  - Python, Rust, and JavaScript clients
  - [[Feature Request] Symlink support. Is there any performance/complexity reason for not supporting symlinks? _201505](https://github.com/facebook/watchman/issues/105)
    - Watchman recursively watches files that are contained within a filesystem tree. Symlinks can point to an arbitrary location on the filesystem. Changes to symlink targets that are outside the tree are not observable.
    - Why not simply resolve the symlink and watch its target? Because it isn't simple. Here are a handful of reasons that make this a difficult prospect.
    - 👷🐛202303: The harsh reality is that there is not really a case for symlink support internally (I recently chatted with folks about this), and we probably won't be motivated to implement this.
    - 202303: gajus/turbowatch@v2.0.0 (release) `Turbowatch` made a switch to `chokidar`. However, I kept the API such that we could revert to using Watchman, or maybe even support multiple backends.

- https://github.com/webpack/watchpack
  - 不依赖chokidar，依赖graceful-fs，由webpack开发
  - watchpack high level API doesn't map directly to watchers.
  - Instead a three level architecture ensures that for each directory only a single watcher exists.

- https://github.com/Qard/onchange
  - 依赖chokidar
  - Use glob patterns to watch file sets and run a command when anything is added, changed or deleted.
- https://github.com/fabiospampinato/watcher
  - The file system watcher, with no native dependencies and optional rename detection support.
  - Node's built-in `fs.watch` function is garbage and you never want to use it directly.
    - Recursive watching is not supported under Linux
    - the events provided by fs.watch are completely useless as they tell you nothing about what actually happened in the file system
  - `chokidar` requires a native dependency for efficient recursive watching under macOS
  - It doesn't watch recursively efficiently under Windows

- https://github.com/tapio/live-server
  - 依赖chokidar、colors、connect、event-stream、faye-websocket、htp-auth、morgan、opn、proxy-middleware、send、serve-index
    - 不建议使用，推荐使用依赖livereload-js的node-livereload
  - a little development server with live reload capability.
  - Having the page reload automatically after changes to files can accelerate dev
  - If you don't want/need the live reload, you should probably use something simpler, like python -m SimpleHTTPServer/http.server 8999
  - https://github.com/geelen/jspm-server
    - It's based on @tapio's excellent live-server
- https://github.com/livereload/livereload-js
  - 无依赖
  - 示例依赖watchify，watchify依赖chokidar
  - To use LiveReload, you need a client (this script) in your browser and a server running on your development machine
  - This repository (livereload.js) implements the client side of the protocol.
  - The client connects to a LiveReload server via web sockets and listens for incoming change notifications.
  - It gets change notifications from a LiveReload server and applies them to the browser.
  - If you are developing a LiveReload server, see dist/livereload.js for the latest version built using the sources in this repository.
  - We require LiveReload server vendors to distribute livereload.js as part of their apps or tools.
- https://github.com/napcs/node-livereload
  - Current maintained fork of LiveReload server in Node.js
  - 依赖 chokidar、livereload-js、ws、opts
  - 注意：文件更新消息的发送，使用的是ws协议，需要在浏览器中访问file:///path/to/test.html，而不是http://localhost:35729/test.html

- https://github.com/mihneadb/node-directory-tree
  - http://livereload.com/
  - Creates a JS object representing a directory tree.
  - const dirTree = require("directory-tree"); 
  - const tree = dirTree("/some/path"); 
- https://github.com/euberdeveloper/dree
  - 只依赖yargs
  - A nodejs module which helps you handle a directory tree.
  -  It provides you an object of a directory tree with custom configuration and optional callback method when a file or dir is scanned.
  - const dree = require('dree'); 
  - const tree = dree.scan('./folder', options); 

- https://github.com/jkomyno/pate
  - 依赖glob, yargs, chalk, progress
  - pate is a library that, given a RegExp pattern and a folder path, filters out every nested file in that folder which doesn't match the pattern.
  - Optionally it's possible either to write the list of files that match to a file, to log every single action that's happening internally, or even to filter the files via a glob pattern.

- more-folder-tree
  - https://www.npmtrends.com/directory-tree-vs-fs-readdir-recursive-vs-node-dir-vs-walk-vs-walkdir
  - https://github.com/fshost/node-dir
  - https://github.com/fs-utils/fs-readdir-recursive

- https://github.com/mysticatea/cpx
  - cpx "src/**/*.{html, png, jpg}" dist --watch
  - Whenever the files are changed, copy them.
  - 在原目录的修改和重命名操作会同步到新目录，在新目录操作不影响原目录

- more-copy
  - https://www.npmtrends.com/copy-vs-copyfiles-vs-cp-vs-cpx-vs-ncp-vs-npm-build-tools

- https://github.com/plangrid/react-file-viewer
  - Extendable file viewer for web
  - support jpg, png, gif, pdf, xlsx, docx, csv
- https://github.com/RandomFractals/vscode-data-preview
  - Data Preview is already capable of loading a few 10+MB's large data files with 100+K records & extensive list of supported Data Formats
  - you'll be hard pressed to find on VSCode marketplace in one extension.
  - soon it will include large text & binary data files loading & Apache Arrow data streaming.
# file-utils
- https://github.com/plantain-00/files2text
  - A CLI tool and library to get text structure of files in a folder.

- https://github.com/hyperhyperspace/hyperhyperspace-core /MIT/ts
  - https://www.hyperhyperspace.org/
  - A library to create p2p applications, using the browser as a full peer.
  - An offline-first shared data library for creating p2p apps that work in the browser (and now also NodeJs).
  - HHS uses an immutable typed-objects local storage model. 
    - Objects are both retrieved and cross-referenced using a structural hash of their contents as their id (a form of content-based addressing).
  - Mutability is implemented using CRDTs. Identities and data authentication are cryptographic.
  - Objects and their references form an immutable DAG, a fact that is used for data replication in HHS p2p mesh.
# undo/history
- https://github.com/pomber/git-history /MIT/202303/js/inactive
  - https://githistory.xyz/
  - Quickly browse the history of files in any git repo
  - Go to a file in GitHub (or GitLab, or Bitbucket); Replace github.com with github.githistory.xyz
# file-types
- https://github.com/sindresorhus/file-type /js
  - Detect the file type of a Buffer/Uint8Array/ArrayBuffer
  - file type is detected by checking the magic number of the buffer.
  - This package is for detecting binary-based file formats, not text-based formats like .txt, .csv, .svg, etc.
# archive/encoding/zip/rar
- https://github.com/SheetJS/cfb-editor
  - Archive (ZIP/CFB/MAD) Editor

- https://github.com/cthackers/adm-zip /202212/js
  - A Javascript implementation of zip for nodejs. 
  - Allows user to create or extract zip files both in memory or to/from disk

## formats

- https://github.com/fabiospampinato/siar
  - a simple random-access archive format. 
  - It's similar to Electron's asar (compact, json header, random access) but with: no integrity checks, browser support, tree-shaking, much smaller, zero party dependencies. Fast.
# more

# discuss

- ## 

- ## 

- ## Use `fetch()` to check if a file exists without downloading the entire thing.
- https://twitter.com/wesbos/status/1712485929255051592
- For cases where `HEAD` is not supported (ex. S3 GET signed URL), you can also do a `GET` with the `Range` header and get only the first byte to confirm the file.
  - Would this be the code? `fetch('...', { headers: { Range: 'bytes=0-0' }})` ; 
  - Correct, by doing so you don't need to worry about the server supporting HEAD, very handy
- Wouldn’t that require also to finish the request via .text(), as example, to avoid dangling promises around? 
  - not sure. 是否要手动释放资源

- ## To find out whether a file is UTF-8 text file in browser.
- https://twitter.com/__enix__/status/1681710341372117003
  - This is especially FAST when compared to the common solution that loads the whole file as a BLOB into memory.

```JS
const decoder = new TextDecoderStream()

file.stream().pipeTo(decoder.writable);

const reader = decoder.readable.getReader();

const { done, value } = await reader.read()

// unrecognized bytes will be turned into \ufffd
if (value?.includes('\ufffd')) {
  return false;
}
```
