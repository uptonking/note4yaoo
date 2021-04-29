---
title: toc-lib-list-tree
tags: [lib, toc, tree]
created: '2020-07-12T18:55:54.993Z'
modified: '2020-07-12T19:00:27.345Z'
---

# toc-lib-list-tree

# tree

- react-treeview /MIT/1kStar/201706
  - https://github.com/chenglou/react-treeview
  - https://cdn.rawgit.com/chenglou/react-treeview/aa72ed8b9e0b31fabc09e2f8bd4084947d48bb09/demos/index.html
  - Easy, light, flexible tree view made with React.
- react-vtree /MIT/113Star/202004
  - https://github.com/Lodin/react-vtree
  - https://lodin.github.io/react-vtree/
  - React component for efficiently rendering large tree structures
  - based on react-window
- cp-react-tree-table /MIT/41Star/202005
  - https://github.com/constantin-p/cp-react-tree-table
  - https://constantin-p.github.io/cp-react-tree-table/
  - A fast, efficient tree table component for ReactJS
- react-simple-tree-menu /MIT/62Star/202006
  - https://github.com/iannbing/react-simple-tree-menu
  - https://iannbing.github.io/react-simple-tree-menu/
  - A simple React tree menu component
- react-state-tree /MIT/94Star/202001
  - https://github.com/suchipi/react-state-tree
  - Drop-in replacement for useState that persists your state into a redux-like state tree
- react-ui-tree /MIT/693Star/201811
  - https://github.com/swiftcarrot/react-ui-tree
  - https://swiftcarrot.github.io/react-ui-tree/
  - React tree component with drag & drop
  - based on js-tree
- react-sortable-tree /MIT/3.3kStar/202005
  - https://github.com/frontend-collective/react-sortable-tree
  - https://frontend-collective.github.io/react-sortable-tree/
  - Drag-and-drop sortable component for nested data and hierarchies
  - based on react-virtualized, react-dnd, react-dnd-html5-backend
- rc-tree /MIT/689Star/202006
  - https://github.com/react-component/tree
  - http://react-component.github.io/tree/
  - Tree component based on rc-virtual-list, rc-animate
- react-treebeard /MIT/1.5kStar/201909
  - https://github.com/storybookjs/react-treebeard
  - http://storybookjs.github.io/react-treebeard/
  - Tree Component. Data-Driven, Fast, Efficient and Customisable.
  - based on velocity-animate

- https://github.com/clauderic/dnd-kit
  - http://dndkit.com/
  - http://examples.dndkit.com
  - extensible drag & drop toolkit for React.
  - https://github.com/clauderic/dnd-kit/tree/master/stories/3%20-%20Examples/Tree
    - https://5fc05e08a4a65d0021ae0bf2-vrdufzklrj.chromatic.com/?path=/story/examples-tree-sortable--basic-setup
    - https://twitter.com/clauderic_d/status/1375623307060510731
      - I recently built a sortable tree example with @dndkit .
      - Collapsible subtrees, removable items, unlimited nesting, dynamic placeholder, keyboard support and zero external dependencies.

# file-folder-directory-scan-watch

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
  - On most other platforms, the fs.watch-based implementation is the default, which avoids polling and keeps CPU usage down. 
- https://github.com/webpack/watchpack
  - 不依赖chokidar，依赖graceful-fs，由webpack开发
  - watchpack high level API doesn't map directly to watchers. 
  - Instead a three level architecture ensures that for each directory only a single watcher exists.
- https://github.com/Qard/onchange
  - 依赖chokidar
  - Use glob patterns to watch file sets and run a command when anything is added, changed or deleted.

- https://github.com/mihneadb/node-directory-tree
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

# misc

- https://github.com/aximario/json-tree
  - 把扁平化的数据转换成树形结构的JSON，把树形JSON扁平化
- https://github.com/daniel-hauser/react-organizational-chart
  - Simple react hierarchy tree - any React children accepted for nodes
- https://github.com/bkrem/react-d3-tree
- https://github.com/mar10/fancytree
