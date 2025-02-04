---
title: note-react-latest-changelog
tags: [changelog, react]
created: 2020-06-23T05:49:13.941Z
modified: 2020-07-14T11:54:44.711Z
---

# note-react-latest-changelog

# features

- 16.8-hooks
- 16.6-lazy loading with Suspense
- 16.3-new context api
- 16.0-fiber reconciliation
# changelog
- ref
  - https://github.com/facebook/react/blob/master/CHANGELOG.md
  - [React - Versions](https://legacy.reactjs.org/versions/)

## v19

## v18.0.0_20220329

- v18.0.0_20220329
  - ✨ `useId` is a new hook for generating unique IDs on both the client and server, while avoiding hydration mismatches
  - ✨ `startTransition` and `useTransition` let you mark some state updates as not urgent. 
    - Other state updates are considered urgent by default. 
    - React will allow urgent state updates (for example, updating a text input) to interrupt non-urgent state updates
  - ✨ `useSyncExternalStore` is a new hook that allows external stores to support concurrent reads by forcing updates to the store to be synchronous. 
    - It removes the need for `useEffect` when implementing subscriptions to external data sources, and is recommended for any library that integrates with state external to React.
  - `useDeferredValue` lets you defer re-rendering a non-urgent part of the tree. 
    - It is similar to debouncing
    - There is no fixed time delay, so React will attempt the deferred render right after the first render is reflected on the screen. 
  - `useInsertionEffect` is a new hook that allows CSS-in-JS libraries to address performance issues of injecting styles in render. 
    - Unless you’ve already built a CSS-in-JS library we don’t expect you to ever use this
    - This hook will run after the DOM is mutated, but before layout effects read the new layout. 
  - ✨ `createRoot`: New method to create a root to render or unmount. 
    - Use it instead of `ReactDOM.render`. 
    - New features in React 18 don't work without it.
  - `hydrateRoot`: New method to hydrate a server rendered application. 
    - Use it instead of `ReactDOM.hydrate` in conjunction with the new React DOM Server APIs. New features in React 18 don't work without it.
  - ✨ Add selective hydration.
  - ✨ Add the new streaming renderer.
  - 💣 Automatic batching for fewer renders in React 18
    - you can use `ReactDOM.flushSync()` to opt out of batching
  - 💣 React now depends on modern browsers features including `Promise, Symbol, and Object.assign`.
  - No warning about `setState` on unmounted components
  - Improved memory usage: React now cleans up more internal fields on unmount
  - Make `<StrictMode>` re-run effects to check for restorable state
  - Remove unsupported `unstable_changedBits` API.
  - Flush `useEffect` resulting from discrete events like clicks synchronously
  - Use `setImmediate` when available over `MessageChannel`. 
  - Allow suspending outside a Suspense boundary

## v17.0.0_20201020

- v17.0.0_20201020
  - ✨ Add `react/jsx-runtime` and `react/jsx-dev-runtime` for the new JSX transform.
  - Build component stacks from native error frames
  - 💣 Run `useEffect` cleanup functions asynchronously
  - 💣 Delegate events to roots instead of `document`.
  - Clean up all effects before running any next effects
  - Use browser focusin and focusout for onFocus and onBlur
  - Make all Capture events use the browser capture phase.
  - 💣 Remove event pooling
  - Attach all known event listeners when the root mounts
  - 🧪 Concurrent Mode (Experimental)

- [Event Pooling – React](https://legacy.reactjs.org/docs/legacy-event-pooling.html)
  - React 17 removes the “event pooling” optimization from React. 
  - It doesn’t improve performance in modern browsers and confuses even experienced React users
  - With React 16 and earlier, you have to call `e.persist()` to properly use the event, or read the property you need earlier.
  - Note that e.persist() is still available on the React event object, but now it doesn’t do anything.
  - 从 React 17 开始，React DOM 已经将 e.persist() 设为 noop，仅在 React Native 中仍然保留 Event Pool 和 e.persist()

## v16.0.0_20170926

- 16.13.0_20200226
  - In Strict Development Mode, React calls lifecycle methods twice to flush out any possible unwanted side effects. 
    - This release adds that behaviour to shouldComponentUpdate
  - Warnings for some deprecated string refs
  - Deprecate React.createFactory()
- 16.9.0_20190808
  - Performance Measurements with `<React.Profiler>`.
  - Async `act()` for Testing
  - warning for using componentWill Mount/ReceiveProps/Update
  - URLs starting with `javascript:` are a dangerous attack surface because it’s easy to accidentally include unsanitized output in a tag like `<a href>` and create a security hole
  - Before compiling JavaScript classes with Babel became popular, React had support for a “factory” component that returns an object with a render method

- 16.8.0_20190206
  - ✨ Add Hooks

- 16.7.0_20181219
  - 废除componentWillMount，componentWillUpdate，componentWillReceiveProps
  - 关于提早发送数据请求，官方鼓励将数据请求部分的代码放在组件的constructor()中，将现有componentWillMount中的代码迁移至componentDidMount即可
  - new: getSnapshotBeforeUpdate()与componentDidUpdate()一起使用可以取代componentWillUpdate
  - new: getDerivedStateFromProps()与componentDidUpdate()一起使用可以取代componentWillReceiveProps    
  - Clear fields on unmount to avoid memory leaks.  
  - Post to MessageChannel instead of window.   
- 16.6.0-20181023
  - use the **Suspense component to do code-splitting** by wrapping a dynamic import in a call to React.lazy().
  - Add React.memo() as an alternative to PureComponent for functions.
    - PureComponent要依靠class才能使用，而React.memo()可以和functional component一起使用
  - React. StrictMode now warns about legacy context API, findDOMNode.
  - Rename unstable_Placeholder to Suspense, and delayMs to maxDuration.
  - Add contextType as a more ergonomic way to subscribe to context from a class.
- 16.5.0-20180905
  - Add a warning if React.forwardRef render function doesn't take exactly two arguments 
  - Add support for React DevTools Profiler 
  - Minimally support iframes (nested browsing contexts) in selection event handling
- 16.4.0-20180523
  - Add a new experimental React.unstable_Profiler component for measuring performance.
  - Add support for the Pointer Events specification. 
  - Add the ability to specify propTypes on a context provider component.
  - You can now assign propTypes to components returned by React. ForwardRef.
- 16.3.0-20180329
  - **new Context API**：父组件向嵌套内层子组件传递props
  - React.createRef()：在编码中提前声明需要获取 Ref，as an ergonomic alternative to callback refs.
  - React.forwardRef()：let components forward their refs to a child. 用于高阶组件传递ref，使包裹的无状态组件可以接收ref作为第二个参数，并且可以传递下去
  - Add a new getDerivedStateFromProps() lifecycle
  - Add a new getSnapshotBeforeUpdate() lifecycle.
  - Add a new `<React.StrictMode>` wrapper to help prepare apps for async rendering. 
  - StrictMode：用于在开发环境下提醒组件内使用不推荐写法和即将废弃的API，不会被渲染成真实DOM
  - Add support for onLoad and onError events on the `<link>` tag. 
  - Prevent an infinite loop when attempting to render portals with SSR.
  - Improve user timing API messages for profiling.
- 16.2.0-20171128
  - Add Fragment as named export to React: Fragment可以让聚合一个子元素列表，并且不在DOM中增加额外节点。
  - Support experimental Call/Return types in React. Children utilities.
- 16.1.0-20171109
  - Add support for portals in React. Children utilities.
  - Move link in the warning message to avoid redirect.
  - Include the autoFocus attribute into SSR markup.
  - Support string values for the capture attribute.

- 16.0.0_20170926
  - ✨ React Fiber：使得大量的计算可以被拆解分片、异步化
  - Components can now return arrays and strings from render.
  - Improved error handling with introduction of "error boundaries"：`componentDidCatch()`捕获render()时的错误
  - ✨ `ReactDOM.createPortal()`： support for declaratively rendering a subtree into another DOM node. 解决modal不渲染到parent node的问题
  - Streaming mode for server side rendering is enabled with `ReactDOMServer.renderToNodeStream()`.
  - React DOM now allows passing non-standard attributes.
  - `ReactDOM.render()` now return null if called from inside a lifecycle method.
  - Calling `setState` with null no longer triggers an update.
  - Calling `setState` directly in render always causes an update. Regardless, you should not be calling setState from render.
  - setState callback (second argument) now fires immediately after componentDidMount/componentDidUpdate instead of after all components have rendered.
  - When replacing `<A />` with `<B />` , B.componentWillMount now always happens before A.componentWillUnmount.
  - Shallow renderer no longer calls componentDidUpdate() because DOM refs are not available. 
  - The server renderer has been completely rewritten
  - When "unknown" props are passed to DOM components, for valid values, React will now render them in the DOM. 
  - Errors in the render and lifecycle methods now unmount the component tree by default. To prevent this, add error boundaries.
  - 💣 `React.createClass, React.PropTypes, ReactDOM` have been removed from the core package. 

## v15.0.0_20160407

- 15.6.2-20170925
  - Switch from BSD + Patents to MIT license
  - Prevent event handlers from receiving extra argument in development.
  - Add support for controlList attribute to DOM property whitelist 
- 15.6.0-20170613
  - Add support for CSS variables in style attribute
  - Add support for CSS Grid style properties.
- 15.5.0-20170407
  - Added react-dom/test-utils, which exports the React Test Utils.
- 15.4.0-20161116
  - Improved development performance by freezing children instead of copying.
  - The unstable batchedUpdates API now passes the wrapped function's return value through.
- 15.3.0-20160729
  - Add `React.PureComponent`
  - Add xmlns, xmlnsXlink to supported SVG attributes. 
- 15.2.0-20160701
  - Stop validating props at mount time, only validate at element creation. 
  - Add warning for unknown properties on DOM elements. 
- 15.1.0-20160520
  - Add a new warning to communicate that props objects passed to createElement must be plain objects. 
  - Add additional information to the controlled input warning.

- 15.0.0_20160407
  - Initial render now uses `document.createElement` instead of generating HTML. 
  - No more extra `<span>`s. 
    - ReactDOM will now render plain text nodes interspersed with comment nodes that are used for demarcation(界限; 分界, 划分).
  - Rendering `null` now uses comment nodes. 
    - Previously null would render to `<noscript>` elements. 
    - We now use comment nodes. 
  - Functional components can now return `null`.
  - All SVG tags are now fully supported.

## v0.14.0_20151007

- 0.14.0_20151007
  - 💣 Split the main react package into two: react and react-dom
  - Stateless functional components：使用js函数直接定义react组件
  - Refs to DOM components as the DOM node itself.  
    - Note that refs to custom (user-defined) components work exactly as before; 
    - only the built-in DOM components are affected by this change.
  - The props object is now frozen, so mutating props after creating a component element is no longer supported.
  - Plain objects are no longer supported as React children; arrays should be used instead.
  - setProps and replaceProps are now deprecated. 
  - Added React. Children.toArray

- 0.13.0-20150310
  - 💣 Calls to `setState` in life-cycle methods are now always batched and therefore asynchronous.
  - ✨ Support for using ES6 `class`es to build React components
  - ✨ Added new top-level API `React.findDOMNode(component)` as a replacement for `component.getDOMNode()`.
  - The findDOMNode method has moved from react module to the react-dom module.
  - Added a new top-level API React.cloneElement(el, props)
  - New ref style, allowing a callback to be used in place of  string
  - this.setState() can now take a function as the first argument for transactional state updates, 
    - such as this.setState((state, props) => ({count: state.count + 1}));

- 0.12.0_20141028
  - key and ref moved off props object, now accessible on the element directly
  - React is now BSD licensed with accompanying Patents grant
  - Spread operator ({...}) introduced to deprecate this.transferPropsTo
  - Added support for more HTML attributes: acceptCharset, classID, manifest

- 0.11.0-20140717
  - Support rendering to null
  - `React.Children.count` has been added as a helper for counting the number of children
- 0.10.0-20140321
  - Made it possible to server render without React-related markup
- 0.9.0-20140220
  - Added support for SVG tags defs, linearGradient, polygon
  - On input, select, and textarea elements, .getValue() is no longer supported; use .getDOMNode().value instead
- 0.8.0-20131219
  - Support for more dom attributes
- 0.5.0-20131016
  - Support for Selection events., Composition events
  - Support for additional DOM properties, SVG properties
- 0.4.0-20130717
  - Support for more DOM elements and attributes (e.g.,  `<canvas>` )
  - Support for the `key` prop

## v0.x_20130529 /#InitialRelease

- 0.3.0_20130529
  - initial public release
