---
title: lib-ui-spectrum-codebase
tags: [adobe-spectrum, codebase]
created: 2021-04-12T16:38:36.775Z
modified: 2021-04-12T18:06:54.456Z
---

# lib-ui-spectrum-codebase

# guide

# react-spectrum
- useComp hook的参数一般都是3个：props、state、domRef

- useComp(options) hook传入的参数会作为内部各个函数的默认值，最后返回的对象也会包含这些默认值属性及新的属性，如事件处理函数

## Accordion

- 主要状态的管理基于 useTreeState
- useAccordion使用了 useSelectableList 来处理按键和鼠标选择事件
  - allowsTabNavigation: true
- useAccordionItem使用了useSelectItem来处理item相关事件
  - 主要是将mouse相关事件处理函数都变为调用onSelect方法
# react-aria

## Collection相关

- useSelectableCollection
  - 处理按键相关事件onKeyDown：4个方向键 + Home/End/PageDown/PageUp/Escape/Tab
  - 处理焦点或选择相关事件onFocus/onBlur/onMouseDown

- useSelectableItem
  - 利用selectionManager处理onSelect事件
  - 条用onPress(/Start)会调用onSelect方法

- useSelectableList
  - 使用了 useSelectableCollection
  - 注意单独处理virtualized的情况

## interaction相关

- useHover返回的hoverProps会在鼠标进入元素触发一次，鼠标离开元素也会触发一次
# react-stately
- CollectionBase类型的属性children和items的区别
  - children是必需属性而非可选，可用于静态或动态数据集合
  - items是可选属性，用来实现 dynamic collections

- CollectionBuilder
  - 对象是不变的(用作工具)，build()是入口
  - iterable(){}工具方法会返回一个`可迭代的对象`，执行`迭代器指针对象`的next()，则会返回cache中的item，并更新cache
  - `*iterateCollection()`会创建所有数据对应的Node对象的集合
  - `*getFullNode()`会创建一项数据对应的Node对象
  - 先处理 React.isValidElement === true，将react元素转换，其中type值由Item函数变为item字符串，还添加了aria-label, childNodes等属性
  - 再处理 React.isValidElement === false，返回完整节点对象

- PartialNode由Node没有的属性
  - element、renderer
- Node有PartialNode没有的属性
  - level、parentKey, prevKey, nextKey

- Item
  - Item会创建，一项数据对应的较为详细的节点信息，主要包括节点类型、子节点类型
  - Item组件函数始终`return null`，该组件的状态不由react管理
  - Item的子元素可以是Item，描述树形结构
  - *getCollectionNode(){}返回的是PartialNode类型的迭代器指针对象
  - *childNodes(){}会陆续返回所以子节点数据，注意生成器函数是延迟计算的，具体表现在ui上一般是在点击父节点后才会计算子节点的数据，一种惰性计算的感觉

- Section组件函数始终`return null`，所有内容和Item几乎相同
  - 会返回子项目数据对应的PartialNode

- useCollection
  - 创建集合数据对应的不可变的节点集合 new CollectionBuilder(props, context)
  - 根据节点集合创建对应结构的Collection对象

- useControlledState对于非受控组件，状态值应该如何变化???
  - hook自身就是封装了useState的功能，返回[value, setValue]
  - [useControlledState value param should be optional ?](https://github.com/adobe/react-spectrum/issues/1859) 

- TreeCollection/ListCollection
  - 内部实现几乎相同
  - 提供符合Collection接口的API
  - 两者都基于递归创建树形结构，基于class实现
    - list递归因为支持section分组
    - tree递归因为支持expandedKeys和section分组

- useTreeState
  - 将Item中的children转换成Collection对象
  - 返回值对象的属性包括 collection，expandedKeys, disabledKeys, toggleKey(), selectionManager

- useListState
  - 支持在useCollection创建Collection对象之前，先过滤数据
  - 和useTreeState很相似

- Selection
  - `class Selection extends Set<Key>`
  -  A Selection is a special `Set` containing Keys, which also has an anchor and current selected key for use when range selecting.

- SelectionManager
  - An interface for reading and updating multiple selection state.
  - select方法支持single/multiple
  - setFocused方法 `this.state.setFocused(isFocused); `
  - setFocusedKey方法 `this.state.setFocusedKey(key, childFocusStrategy); `
  - setSelectedKeys方法 `this.state.setSelectedKeys(selection); `
  - selectAll方法 `this.state.setSelectedKeys('all'); `

- useMultipleSelectionState
  - selectionMode 默认值为 'none'
  - 返回对象的属性包括...
    - setFocused
    - setFocusedKey
    - setSelectedKeys
  - 使用者
    - useListState, useTreeState, useSelectState
    - 不建议使用，可以使用更高层的SelectionManager

## Collection

- The `Collection` interface provides a generic representation for many types of collections. 
  - The collection is read only (immutable), and sequential (ordered). 
  - Each item has a unique key that identifies it, which can be used to access items. 
  - It's like a combination of an array and a map: you can iterate over items in a well defined order, and also access items by key.

- The `Collection` interface can be implemented in many ways. 
  - For example, you could write a class to expose the required methods and properties for an underlying data structure like an array or Map.
- React Spectrum implements a JSX-based API for defining collections. 
  - This is implemented by the `useCollection` hook. 
  - `useCollection` iterates over the JSX tree, and recursively builds a collection of `Node` objects. 
  - Each node includes the value of the item it represents, along with some metadata about its place in the collection.
  - These nodes are then wrapped in a class that implements the Collection interface, and exposes the nodes. 
  - State management hooks like `useListState` and `useTreeState` handle building the collection and exposing the necessary interface to components.
- When implementing collection components using react-aria hooks like `useListBox`, and `useSelect`, you'll iterate over these nodes to render the data in the collection.

- useListState
  - Provides state management for list-like components. 
  - Handles building a collection of items from props, and manages multiple selection state.
  - See the docs for `useListBox` in react-aria for an example of `useListState`.

- useSingleSelectListState
  - Provides state management for list-like components with single selection.
  - Handles building a collection of items from props, and manages selection state.
  - [Add useSingleSelectListState](https://github.com/adobe/react-spectrum/pull/802)
    - This hook handles mapping the props for components supporting single selection to the internal state which is stored as a set of one key. 
    - `onSelectionChange` is now always fired, regardless of whether the key actually changed. This was to ensure that the picker closes when selecting the same item

- useTreeState
  - Provides state management for tree-like components. 
  - Handles building a collection of items from props, item expanded state, and manages multiple selection state.
    - See the docs for `useMenu` in react-aria for an example of `useTreeState`.

- useAsyncList
  - Manages state for an immutable async loaded list data structure, and provides convenience methods to update the data over time.
  - `useAsyncList` extends on `useListData`, adding support for async loading, pagination, sorting, and filtering. 
  - It manages loading and error states, supports abortable requests, and works with any data fetching library or the built-in browser `fetch` API.

- useListData
  - Manages state for an immutable list data structure, and provides convenience methods to update the data over time.
  - React requires all data structures passed as props to be immutable. 
  - This enables them to be diffed correctly to determine what has changed since the last render. 
  - This can be challenging to accomplish from scratch in a performant way in JavaScript.
  - `useListData` stores selection state for the list, based on unique item keys.

- useTreeData
  - useTreeData helps manage an immutable tree data structure, with helper methods to update the data in an efficient way. 
  - Since the data is stored in React state, calling these methods to update the data automatically causes the component to re-render accordingly.
  - `useTreeData` stores selection state for the tree, based on unique item keys.

## Selection

- Many collection components support selecting items by clicking or tapping them, or by using the keyboard. 
  - This page discusses how to handle selection events, how to control selection programmatically, and the data structures used to represent a selection.
- Selection is handled by the `onSelectionChange` event, which is supported on most collection components. 
  - Controlled behavior is supported by the `selectedKeys` prop, and uncontrolled behavior is supported by the `defaultSelectedKeys` prop. 
  - These props are passed to the top-level collection component, and accept a set of unique item keys that are selected. 
  - This allows marking items as selected by their key even before they are loaded, which can be useful when you know what items should be selected on initial render, before data loading has completed.
- Selection is represented by a `Set` object. 
  - You can also pass any iterable collection (e.g. an array) to the selectedKeys and defaultSelectedKeys props, 
  - but the `onSelectionChange` event will always pass back a `Set`.
- When data in a collection changes, the selection state may need to be updated accordingly. 
  - For example, if a selected item is deleted, it should be removed from the set of selected keys. 
  - You can do this yourself, but the `useListData` and `useTreeData` hooks can handle this automatically.
- selectedKeys and defaultSelectedKeys can also be set to `all` to programmatically select all items.
  - This represents all items in the collection, whether currently loaded or not. 
  - The application must adjust its handling of bulk actions in this case to apply to the entire collection rather than only the keys available to it locally.

- SelectionManager
  - provides a generic interface for reading and updating selection and focus state based on a Collection
  - Focus is represented by a single item key.
  - A SelectionManager wraps the state returned by useMultipleSelectionState

- useMultipleSelectionState
  - manages selection state for many components. 
  - Oftentimes, you won't need to use this hook directly, since it's included in hooks like useListState, and useSelectState. 

## stately-more-apis

- useSelectState
  - Handles building a collection of items from props, handles the open state for the popup menu, and manages multiple selection state.

## coding-style

- 函数内大多数局部变量都是let块级可再赋值的变量，特别是props参数
  - https://github.com/adobe/react-spectrum/pull/93
  - Creating a new variable is a recipe for bugs in this case. I'd immediately forget to use the new variable not named props and keep using props later in the code, not realizing that it isn't actually all of the props. Already did this several times.
# state

# docs
- 几乎所有文档都在mdx文件中，部分文档从组件源码的注释中提取
  - 各种文件以及特殊的import形式，参考.parcelrc配置
