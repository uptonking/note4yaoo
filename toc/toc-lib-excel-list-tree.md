---
title: toc-lib-excel-list-tree
tags: [file-manager, lib, toc, tree]
created: 2020-07-12T18:55:54.993Z
modified: 2022-08-21T10:02:41.845Z
---

# toc-lib-excel-list-tree

# guide

# flat-tree
- 更推荐用parentId的方式
  - path的优势在于查找更快，且符合直觉易理解
  - 也可以同时维护2套数据结构
- 考虑交换2个同级节点的顺序这个场景
  - 若用parentId作为key，则只要更新同级节点数组
  - 若用path作为key，则要更新所有受影响的子孙节点的key

## 基于id+parentId

- https://github.com/naisutech/react-tree /202302/ts
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

- https://github.com/mpkelly/react-tree /202011/ts/inactive
  - https://codesandbox.io/s/fervent-wave-u7psb
  - accessible React Tree component with a sensible API that supports sorting, drag & drop, keyboard navigation and cut/copy/paste while leaving the visual content entirely to the library user.
  - This tree is intended for file systems and the like. 
  - It will be comfortable with thousands of nodes but is **not virtualized** and not intended for use with massive data sets.
  - Support for toggling expand/collapse

## 基于path

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
  - { key: '0-0-1-0', title: 'title 1-2-0', disableCheckbox: true }, 

- https://github.com/adyz/react-tree-grid
  - https://codesandbox.io/s/virtual-tree-from-npm-g0h7v
  - 依赖react-virtualized
  - This is a component that controls user interactions and state for you so you can create tree/grid components.

- https://github.com/5achinJani/table-dnd-tree
  - https://5achinjani-table-dnd-tree.netlify.app/
  - Table with dnd, indent and outdent rows with flat data-structure and preserving parent-child relationship.
  - 数据源直接使用indent数值，其实类似path

## more-flat

- react-sortable-tree /MIT/3.3kStar/202005/js/inactive
  - https://github.com/frontend-collective/react-sortable-tree
  - 依赖 react-virtualized, react-dnd, react-dnd-html5-backend
  - Drag-and-drop sortable component for nested data and hierarchies
  - 提供了将flat data转换成tree的工具getTreeFromFlatData/getFlatDataFromTree

- https://github.com/adyz/react-tree-grid
  - https://codesandbox.io/s/virtual-tree-from-npm-g0h7v
  - 依赖react-virtualized
  - This is a component that controls user interactions and state for you so you can create tree/grid components.
# tree-ui
- dnd-kit /3.9kStar/MIT/202201/ts
  - https://github.com/clauderic/dnd-kit
  - http://dndkit.com/
  - http://examples.dndkit.com
  - Zero dependencies and modular: built around built-in React state management and context
  - extensible drag & drop toolkit for React.
    - Built for React: exposes hooks such as useDraggable and useDroppable
  - Supports a wide range of use cases: lists, grids, multiple containers, nested contexts, variable sized items, virtualized lists, 2D Games, and more.
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

- https://github.com/plantain-00/tree-component
  - A reactjs and vuejs tree component.
  - drag and drop between different tree
  - composition model(reactjs children and vuejs slot)

- react-sortable-tree /MIT/3.3kStar/202005/js/inactive
  - https://github.com/frontend-collective/react-sortable-tree
  - https://frontend-collective.github.io/react-sortable-tree/
  - https://github.com/frontend-collective/react-sortable-tree-theme-file-explorer
  - 依赖 react-virtualized, react-dnd, react-dnd-html5-backend
  - Drag-and-drop sortable component for nested data and hierarchies
  - 提供了将flat data转换成tree的工具getTreeFromFlatData/getFlatDataFromTree
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

- https://github.com/mafintosh/flat-tree
  - A series of functions to map a binary tree to a list
- https://github.com/cheton/flattree
  - Convert hierarchical tree structure to flat structure.

- https://github.com/tibdex/tree-to-flat-map
  - converts a tree to a flat map with dot-separated keys.

- freezer /1.3kStar/MIT/201803/js/NoDeps
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
# crdt-tree
- https://github.com/ymlsam/lww-element-dict
  - a LWW key-value store, a conflict-free replicated data type (CRDT) implemented in Typescript/Javascript
  - State-based or operation-base replication
  - Abstraction of clock (e.g. unix timestamp clock or vector clock)
  - Abstraction of data store (e.g. in memory via Map or object literal, cookie, local storage, database, etc.)

- https://github.com/crdteam/causal-tree-ts
  - causal tree replicated data type (RDT) in Typescript.
# tree-data-structure
- treemate /54Star/MIT/202208/ts
  - https://github.com/07akioni/treemate
  - https://treemate.vercel.app/guide.html
  - All in one solution for tree structure in component developling.
  - It helps you manipulate tree data structure for user interface. (Can be used in Tree, Select, Dropdown, Table, Menu components and ...)
  - In treemate, a tree is composed of node (optional group node and optional ignored).

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
- https://github.com/glennflanagan/react-collapsible
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
# misc
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
