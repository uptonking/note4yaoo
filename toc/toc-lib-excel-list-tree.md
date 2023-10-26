---
title: toc-lib-excel-list-tree
tags: [file-manager, lib, toc, tree]
created: 2020-07-12T18:55:54.993Z
modified: 2022-08-21T10:02:41.845Z
---

# toc-lib-excel-list-tree

# guide
- tips
  - > see also json/ast; editor-render-only
# flat-tree
- 更推荐用parentId的方式
  - path的优势在于查找更快，且符合直觉易理解
  - 也可以同时维护2套数据结构
- 考虑交换2个同级节点的顺序这个场景
  - 若用parentId作为key，则只要更新同级节点数组顺序
  - 若用path作为key，则要更新所有受影响的子孙节点的key

- flat-data-model的示例
  - frontend/in-memory database，如rxdb/pouchdb
  - 还可以参考indexeddb相关示例，如dexie, react-admin-dexie/localforage

## 基于id+parentId

- https://github.com/naisutech/react-tree /202302/ts/不支持drag
  - https://naisutech.github.io/react-tree/
  - a hierarchical tree component for React in Typescript
  - data should be a flat list of node objects with 
    - required properties: label, id, parentId 
    - optional properties: items
  - files/leaf items should be a flat list of node objects on items property inside a node.
    - 类似，文件夹有items属性，文件没有
  - 👉🏻 Use as an **uncontrolled** component with defaultSelectedNodes and defaultOpenNodes or a completely **controlled** component 
  - Multi-select API! hold your OS's meta key or ctrl key to be able to select/deselect multiple-nodes
  - new context-based state management for better maintainability and handling of business logic
  - [wip: Add drag and drop event API](https://github.com/naisutech/react-tree/issues/6)

- https://github.com/mpkelly/react-tree /202011/ts/inactive
  - https://codesandbox.io/s/fervent-wave-u7psb
  - accessible React Tree component with a sensible API that supports sorting, drag & drop, keyboard navigation and cut/copy/paste while leaving the visual content entirely to the library user.
  - This tree is intended for file systems and the like. 
  - It will be comfortable with thousands of nodes but is **not virtualized** and not intended for use with massive data sets.
  - Support for toggling expand/collapse

## 基于path

- infinite-tree /153Star/MIT/202207/js
  - https://github.com/cheton/infinite-tree
  - https://infinite-tree.js.org/
  - High performance infinite scroll with large data set
  - 💡 Load nodes on demand
  - Customizable renderer to render the tree in any form
  - Native HTML5 drag and drop API
  - 初始化时传入经典tree结构(使用children)，会先flatten，再渲染
  - forks
    - https://github.com/acierto/infinite-tree
  - https://github.com/cheton/react-infinite-tree /201910/js/inactive
    - http://cheton.github.io/react-infinite-tree/
    - The infinite-tree library for React
    - 支持 [Flat Tree Structure](https://github.com/cheton/flattree/blob/master/examples/tree1.js)

- https://github.com/baurine/react-tree-view /201809/ts/inactive
  - https://baurine.github.io/react-tree-view/
  - simple React TreeView component with flat data structure
  - Instead of using nested data structure, for example, each tree view item data has a children property, we use the flat data structure, keep them same as in the database, each child item has a parentKey property points to its parent item data.
  - { key: '0-0-1-0', title: 'title 1-2-0', disableCheckbox: true }

- https://github.com/adyz/react-tree-grid
  - https://codesandbox.io/s/virtual-tree-from-npm-g0h7v
  - 依赖react-virtualized
  - This is a component that controls user interactions and state for you so you can create tree/grid components.

- https://github.com/5achinJani/table-dnd-tree
  - https://5achinjani-table-dnd-tree.netlify.app/
  - Table with dnd, indent and outdent rows with flat data-structure and preserving parent-child relationship.
  - 数据源直接使用indent数值，其实类似path

- https://github.com/uptick/react-keyed-file-browser
  - https://uptick.github.io/react-keyed-file-browser/
  - 依赖 react-dnd、date-fns
  - Folder based file browser given a flat keyed list of objects

## more-flat

- https://github.com/tinyplex/tinybase
  - https://tinybase.org/demos/movie-database/

- react-sortable-tree /MIT/3.3kStar/202005/js/inactive
  - https://github.com/frontend-collective/react-sortable-tree
  - https://frontend-collective.github.io/react-sortable-tree
  - https://github.com/frontend-collective/react-sortable-tree-theme-file-explorer
  - 依赖 react-virtualized, react-dnd, react-dnd-html5-backend
  - Drag-and-drop sortable component for nested data and hierarchies
  - 提供了将flat data转换成tree的工具getTreeFromFlatData/getFlatDataFromTree
  - 不支持显示拖拽指示线
  - 每一行容器都是`position: absolute`，默认 `display: block` 布局
    - 从左到右依次是，折叠按钮+横线 > 父级连接线(竖线+横线，通过::before/::after实现) > nodeContent
# tree-ui
- dnd-kit /3.9kStar/MIT/202201/ts
  - https://github.com/clauderic/dnd-kit
  - http://dndkit.com/
  - http://examples.dndkit.com
  - Zero dependencies and modular: built around built-in React state management and context
  - extensible drag & drop toolkit for React.
    - Built for React: exposes hooks such as useDraggable and useDroppable
  - Supports a wide range of use cases: lists, grids, multiple containers, nested contexts, variable sized items, virtualized lists, 2D Games, and more.
  - tree组件每一项是li，外层没有ul/ol
  - 作者旧轮子 [react-sortable-hoc](https://github.com/clauderic/react-sortable-hoc)
  - 树形组件示例
    - https://github.com/clauderic/dnd-kit/tree/master/stories/3%20-%20Examples/Tree
    - https://5fc05e08a4a65d0021ae0bf2-vrdufzklrj.chromatic.com/?path=/story/examples-tree-sortable--basic-setup
  - https://twitter.com/clauderic_d/status/1375623307060510731
    - I recently built a sortable tree example with @dndkit.
    - Collapsible subtrees, removable items, unlimited nesting, dynamic placeholder, keyboard support and zero external dependencies.
  - forks
    - https://github.com/wix-playground/dnd-kit
    - https://github.com/replayio/dnd-kit

- react-treeview /MIT/1kStar/201706/js/NoDeps
  - https://github.com/chenglou/react-treeview
  - demos: [controlled, uncontrolled](https://cdn.rawgit.com/chenglou/react-treeview/aa72ed8b9e0b31fabc09e2f8bd4084947d48bb09/demos/index.html)
  - 无依赖；可折叠；无样式主题
  - Easy, light, flexible tree view made with React.

- cp-react-tree-table /MIT/41Star/202106/ts/NoDeps
  - https://github.com/constantin-p/cp-react-tree-table
  - https://constantin-p.github.io/cp-react-tree-table/
  - 给出的示例很像data table，可以从外部按钮触发展开、折叠、滚动
  - A fast, efficient tree table component for ReactJS

- react-simple-tree-menu /MIT/62Star/202008/ts
  - https://github.com/iannbing/react-simple-tree-menu
  - https://iannbing.github.io/react-simple-tree-menu/
  - 依赖可忽略；示例stories使用了reactstrap.v8
  - Inspired by Downshift, a simple, data-driven, light-weight React Tree Menu component
  - fully customizable with render props and control props
- react-checkbox-tree /505Star/MIT/202105/js
  - https://github.com/jakezatecky/react-checkbox-tree
  - https://jakezatecky.github.io/react-checkbox-tree/
  - 依赖classnames、lodash、nanoid
  - 非常适合用来实现文件管理器
- react-super-treeview /93Star/MIT/201908/js/ClassComp
  - https://github.com/azizali/react-super-treeview
  - https://azizali.github.io/react-super-treeview/examples/
  - 依赖只有react-transition-group、lodash
  - a React Treeview component which is customizable on every level.
- react-virtualized-sticky-tree
  - https://github.com/marchaos/react-virtualized-sticky-tree
  - https://marchaos.github.io/react-virtualized-sticky-tree/
  - 依赖react-measure
  - 使用场景类似滚动城市列表时能固定省名
  - A React component for efficiently rendering tree like structures with support for `position: sticky`.
  - uses a similar API to react-virtualized.
- react-arborist /1.6kStar/MIT/202207/ts
  - https://github.com/brimdata/react-arborist
  - https://react-arborist.netlify.app/
  - A sortable, virtual, customizable tree component for React.
  - 依赖 react-dnd, react-window

- https://github.com/lukasbach/react-complex-tree /ts/NoDeps
  - https://rct.lukasbach.com/
  - https://rct.lukasbach.com/storybook
  - Unopinionated Accessible Tree Component with Multi-Select and Drag-And-Drop
  - 提供了自动执行的demo

- https://github.com/plantain-00/tree-component
  - https://plantain-00.github.io/tree-component/packages/react/demo/
  - A reactjs and vuejs tree component.
  - drag and drop between different tree
  - composition model(reactjs children and vuejs slot)

- react-ui-tree /MIT/693Star/201811
  - https://github.com/swiftcarrot/react-ui-tree
  - https://swiftcarrot.github.io/react-ui-tree/
  - React tree component with drag & drop
  - 依赖js-tree

- react-treebeard /MIT/1.5kStar/201909/js
  - https://github.com/storybookjs/react-treebeard
  - http://storybookjs.github.io/react-treebeard/
  - Tree Component. Data-Driven, Fast, Efficient and Customisable.
  - 依赖emotion、velocity-animate
- rc-tree /MIT/689Star/202006
  - https://github.com/react-component/tree
  - http://react-component.github.io/tree/
  - Tree component based on rc-virtual-list, rc-animate
  - 基于class component
  - 
- https://github.com/drcmda/react-animated-tree
  - configurable tree view with full support for drop-in animations
  - 依赖react-spring.v5

- react-virtualized-tree
  - https://github.com/diogofcunha/react-virtualized-tree
  - 依赖 react-virtualized
- react-aspen
  - https://github.com/NeekSandhu/react-aspen
  - https://neeksandhu.github.io/react-aspen-demo/
  - performant solution for displaying (dynamic) nested trees in React apps.
  - 依赖aspen-tree-model、react-window
- react-vtree /MIT/113Star/202004
  - https://github.com/Lodin/react-vtree
  - https://lodin.github.io/react-vtree/
  - React component for efficiently rendering large tree structures
  - 依赖react-window

- https://github.com/phb1206/atlaskit-tree-fork
  - A modified version of @atlaskit/tree library.
  - Flexible tree rendering
  - Dynamic tree expansion with lazy loading

- https://github.com/Vigneshbabuvb/tree-implementation
  - https://heuristic-clarke-aa0809.netlify.app/
  - A simple CRUD operation tree implementation using React library

- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.

- https://github.com/jakezatecky/react-checkbox-tree
  - https://jakezatecky.github.io/react-checkbox-tree/
  - a feature-rich React component for a checkbox treeview.

- [Tree views in CSS](https://iamkate.com/code/tree-views/)
  - A tree view (collapsible list) can be created using only html and css, without the need for JavaScript.

- https://github.com/dgreene1/react-accessible-treeview /ts
  - https://dgreene1.github.io/react-accessible-treeview
  - A react component that implements the treeview pattern as described by the WAI-ARIA Authoring Practices.
  - Highly customizable through the use of the render prop and prop getter patterns.
# tree-crud-operations
- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.
  - Limitations
  - It is assumed that you have children of each node in a single array object
  - Self referencing objects at any point in the tree are not supported
  - An id field is required to perform better change detection (using idKey option).

- https://github.com/PerimeterX/flast
  - Provides a flat Abstract Syntax Tree and an Arborist to trim and modify the tree
  - Adds a unique id to each node to simplify tracking and understanding relations between nodes.
  - Arborist - marks nodes for replacement or deletion and applies all changes in a single iteration over the tree.

- https://github.com/iyegoroff/un-flatten-tree /ts
  - converting trees to lists and vice versa. Can be used in browser and Node.

- https://github.com/kwhitley/treeize
  - Converts row data (in JSON/associative array format or flat array format) to object/tree structure based on simple column naming conventions.
- https://github.com/panosoft/untreeize
  - Reverse treeize library - takes hierarchical data produced by treeize and flattens it

- https://github.com/philipstanislaus/performant-array-to-tree
  - Converts an array of items with ids and parent ids to a nested tree in a performant O(n) way.
  - Runs in browsers and Node.js.
- https://github.com/DenQ/list-to-tree
  - Convert list to tree
- https://github.com/thunderrun/flat-to-tree
  - Convert flat array into tree structure. 
  - O(n) time complexity.

- https://github.com/mafintosh/flat-tree /js
  - A series of functions to map a binary tree to a list
- https://github.com/cheton/flattree
  - Convert hierarchical tree structure to flat structure.

- https://github.com/tibdex/tree-to-flat-map
  - converts a tree to a flat map with dot-separated keys.

- freezer /1.3kStar/MIT/201803/js/NoDeps/inactive
  - https://github.com/arqex/freezer
  - A tree data structure that emits events on updates, even if the modification is triggered by one of the leaves, making it easier to think in a reactive way.
  - Immutable trees to make fast comparison among nodes.
  - Eventful nodes to notify updates to other parts of the app.
  - Freezer is inspired by other tree cursor libraries, specifically Cortex, that try to solve an inconvenience of the Flux architecture
    - It creates a new tree every time a modification is required, referencing the non modified nodes from the previous tree.
    - Sharing node references among frozen objects saves memory and boosts the performance of creating new frozens.
  - https://github.com/arqex/react-json-table
    - A simple but flexible table react component to display JSON data.
- https://github.com/mquan/cortex
  - Cortex is an immutable data store for managing deeply nested structure with React
  - uses immutable data, which allows fast comparison in shouldComponentUpdate

- https://github.com/couralex/treem
  - treem converts flat data (like SQL rows) into an object tree.
  - The tree structure is determined by the columns' names.

- https://github.com/filiplipinski/tree-view-rest-api
  - Categories Tree View + CRUD Rest Api

- https://github.com/Pierre-LouisDeu/NoSQL-Folders
  - A CRUD API to manage your documents in a NoSQL folder tree.

- https://github.com/hughsk/flat /js
  - Flatten/unflatten nested Javascript objects
# crdt-tree
- https://github.com/ymlsam/lww-element-dict
  - a LWW key-value store, a conflict-free replicated data type (CRDT) implemented in Typescript/Javascript
  - State-based or operation-base replication
  - Abstraction of clock (e.g. unix timestamp clock or vector clock)
  - Abstraction of data store (e.g. in memory via Map or object literal, cookie, local storage, database, etc.)

- https://github.com/crdteam/causal-tree-ts
  - causal tree replicated data type (RDT) in Typescript.
# tree-data-structure
- ref
  - [LSM-Tree 论文的中文翻译](https://github.com/tangwz/LSM-Tree-CN/blob/main/LSM-Tree-CN.md)

- treemate /54Star/MIT/202208/ts
  - https://github.com/07akioni/treemate
  - https://treemate.vercel.app/guide.html
  - All in one solution for tree structure in component developling.
  - It helps you manipulate tree data structure for user interface. (Can be used in Tree, Select, Dropdown, Table, Menu components and ...)
  - In treemate, a tree is composed of node (optional group node and optional ignored).

- https://github.com/Yomguithereal/baobab /js/inactive
  - JavaScript & TypeScript persistent and optionally immutable data tree with cursors.
  - It is mainly inspired by functional zippers (such as Clojure's ones) and by Om's cursors.
  - It aims at providing a centralized model holding an application's state and can be paired with React easily through mixins, higher order components, wrapper components or decorators
  - you can create cursors to easily access nested data in your tree and listen to changes concerning the part of the tree you selected.
  - Note that the tree, being a persistent data structure, will shift the references of the objects it stores in order to enable immutable comparisons between one version of the state and another
  - Baobab lets you record the successive states of any cursor so you can seamlessly implement undo/redo features.
  - https://github.com/Yomguithereal/baobab-react
    - React integration for Baobab.

- https://github.com/mafintosh/append-tree /js/hypercore/inactive
  - Model a tree structure on top of an append-only log.
  - stores a small index for every entry in the log, meaning no external indexing is required to model the tree. 
  - Also means that you can perform fast lookups on sparsely replicated logs.

- https://github.com/jlxw/static-json-db
  - A NoSQL key-value database stored as a directory tree of small JSON files which can be deployed as part of a static website and queried from client browsers in an efficient manner.
  - Data is stored in JSON files which are branched into smaller JSON files as size tresholds are met.
  - static-json-db can be a lower-cost alternative to traditional databases that do not need to be updated frequently.

- https://github.com/mihneadb/node-directory-tree
  - Creates a JavaScript object representing a directory tree.

- https://github.com/joaonuno/tree-model-js
  - Manipulate and traverse tree-like structures in javascript.

- https://github.com/wshager/frink
  - Standards-based hierarchical data processing library
  - Parse XML into a DOM level 4 compatible, persistent (AKA immutable) virtual tree.
  - Parse JSON into similar, traversable trees, or mix with XML.
  - Generate L3, a lightweight, flat representation of XML or JSON trees (or mixed) for fast storage and retrieval.

- https://github.com/qwertie/btree-typescript
  - fast in-memory B+ tree with a powerful API based on the standard Map.
  - B+ trees are ordered collections of key-value pairs, sorted by key.
  - data structures in JavaScript tend to be slower than the built-in Array and Map data structures in typical cases, because the built-in data structures are mostly implemented in a faster language such as C++
- https://github.com/w8r/splay-tree
  - This tree is based on top-down splaying algorithm by D. Sleator.

- https://github.com/mikolalysenko/functional-red-black-tree /js
  - A fully persistent red-black tree written 100% in JavaScript. Works both in node.js and in the browser
  - 被使用在pg-mem, leveljs-memory
  - Functional (or fully persistent) data structures allow for non-destructive updates.
  - Functional (or fully persistent) data structures allow for non-destructive updates. So if you insert an element into the tree, it returns a new tree with the inserted element rather than destructively updating the existing tree in place. Doing this requires using extra memory
  - this data structure saves some memory by recycling references to previously allocated subtrees. This requires using only O(log(n)) additional memory per update instead of a full O(n) copy.

## lsm

- https://github.com/gutobortolozzo/node-lsm /js/inactive
  - a log-structured-merge-tree, implemented in node.js

- https://github.com/Pr65/minilsm /rust
  - A simple, single threaded LSM tree implementation
- https://github.com/kaimast/lsm-rs /rust
  - Modular, Asynchronous Implementation of a Log-Structured Merge Tree
  - This implementation does not aim to reimplement LevelDB
- https://github.com/WyattJia/Pomegranate /rust/archived
  - tiny skiplist based log-structured merge-tree written in Rust

- https://github.com/tomfran/LSM-Tree /java
  - Log-Structured Merge Tree Java implementation
  - Sorted String Table (SSTable) is a collection of files modelling key-value pairs in sorted order by key. It is used as a persistent storage for the LSM tree.
- https://github.com/ingaleniranjan365/lsmdb /java
  - Implementation of log-structured merge-trees to create a key-value store
  - Implement a generic key-value database in Java that fulfills /element/:id/timestamp/:timestamp

- https://github.com/chrislessard/LSM-Tree /python
  - An implementation of an LSM Tree in Python

- https://github.com/dhanus/lsm-tree /c
  - an implementation of a two-level single-threaded log structure merge (LSM) tree. 
  - The in-memory data structure is a simple array. 
  - The on-disk data structure is also a simple array, which can be sorted using merge sort.

- https://github.com/eileen-code4fun/LSM-Tree /go
  - A simplified Golang implementation for log structured merge tree. 
  - Data is only stored in memory. 
  - Disk files are simulated by in-memory byte arrays.
  - Put and Get are supported. Compaction is also supported. 
- https://github.com/krasun/lsmtree /go
  - a log-structured merge-tree implementation in Go.
  - not goroutine-safe - calling any methods on it from a different goroutine without synchronization is not safe and might lead to data corruption
# tree-like/nested
- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.
  - Limitations
  - It is assumed that you have children of each node in a single array object
  - Self referencing objects at any point in the tree are not supported
  - An id field is required to perform better change detection (using idKey option).

- https://github.com/Voronenko/Storing_TreeView_Structures_WithMongoDB
  - Educational repository demonstrating approaches for storing tree structures with NoSQL database MongoDB
  - using five typical approaches plus one combination of operating with hierarchy data on example of the MongoDB database.

- https://github.com/jlxw/static-json-db
  - A NoSQL key-value database stored as a directory tree of small JSON files which can be deployed as part of a static website and queried from client browsers in an efficient manner. 
  - Data is stored in JSON files which are branched into smaller JSON files as size tresholds are met. 
  - static-json-db can be a lower-cost alternative to traditional databases that do not need to be updated frequently. 

- https://github.com/epochtalk/treedb /js/inactive
  - Database for tree structured data
  - LevelDB backend for hierarchical data.

- https://github.com/ClosureTree/closure_tree /ruby
  - Closure_tree lets your ActiveRecord models act as nodes in a tree data structure
  - Common applications include modeling hierarchical data, like tags, threaded comments, page graphs in CMSes, and tracking user referrals.
# json tree
- https://github.com/measuredco/react-from-json
  - Declare your React component tree in JSON
- https://github.com/aximario/json-tree
  - 把扁平化的数据转换成树形结构的JSON，把树形JSON扁平化

- https://github.com/proshoumma/organigram
  - http://organigram.surge.sh/
  - 依赖redux.v3、react-dnd.v5、react-dropzone
  - A JSON based tree structure with drag and drop functionally to re-arrange the tree.
# accordion
- https://github.com/springload/react-accessible-accordion
  - https://springload.github.io/react-accessible-accordion
  - Accessible Accordion component for React
- https://github.com/glennflanagan/react-collapsible /js
  - React component to wrap content in Collapsible element with trigger to open and close.
  - It's like an accordion, but where any number of sections can be open at the same time.
  - Collapsible can receive any HTML elements or React component as it's children. Collapsible will wrap the contents, as well as generate a trigger element which will control showing and hiding.

- https://github.com/stuartjnelson/badger-accordion
  - An accessible vanilla JS accordion with extensible API
- https://github.com/cferdinandi/houdini
  - A simple, accessible show-and-hide/accordion script.
# lazy-load-tree
- use-tree /6Star/MIT/202207/ts
  - https://github.com/elseu/use-tree
  - useTree is a set of components and hooks that make it ridiculously easy to work with lazy-loaded tree structures like navigation menus or tables of contents.

- react-lazy-tree /12Star/MIT/201808/js
  - https://github.com/ethanselzer/react-lazy-tree
  - https://ethanselzer.github.io/react-lazy-tree
  - Recursively render tree data structures. Render lazily or greedily.
  - 侧边导航栏经典示例，一次仅展开一个第一层

- https://github.com/velovsky/Derived-D3.js-Collapsible-Tree
  - https://rawgit.com/velovsky/Derived-D3.js-Collapsible-Tree/master/src/test.html
  - a D3 tree performing lazy loadings on click
  - 类似思维导图

- https://github.com/legharir/react-lazy-paginated-tree /201808/js
  - https://boweihan.github.io/rlpt-example/
  - 依赖material-ui.v1
# more
- https://github.com/daniel-hauser/react-organizational-chart
  - Simple react hierarchy tree - any React children accepted for nodes
- https://github.com/bkrem/react-d3-tree
- https://github.com/mar10/fancytree
  - http://wwwendt.de/tech/fancytree/demo/
  - a JavaScript tree view/tree grid plugin with support for keyboard, inline editing, filtering, checkboxes, drag'n'drop, and lazy loading.
- https://github.com/vakata/jstree
  - http://jstree.com/
  - jquery tree plugin

- https://github.com/Idered/behavior-tree
  - Manage React state with Behavior Trees
  - JavaScript/TypeScript implementation of Behavior Trees.
  - @btree/core - Framework agnostic behavior trees implementation
  - With Behavior Tree notation all your code will be wrapped with nodes - that allows to visualize how it works.

- https://github.com/imsnif/nmtree
  - Get a (flat) tree representation of the modules in your node_modules folder

- https://github.com/HannesOberreiter/btree_server
  - API Server for b.tree Beekeeping Application. Node.js and Objections.js
  - Written in typescript build with nodejs, express, knex.js and objections.js.
  - https://github.com/HannesOberreiter/btree_database
    - The maria folder will be our local volume for the database
    - The redis folder will be our local volume for the redis database dumps
