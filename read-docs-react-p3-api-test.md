---
tags: [api, docs, react]
title: read-docs-react-p3-api-test
created: '2020-06-23T07:30:37.293Z'
modified: '2020-06-23T07:37:09.944Z'
---

# read-docs-react-p3-api-test


### 4. api

#### React API

- React.Component
- React.PureComponent
- React.memo
- React.Fragment

- createElement()
- createFactory()      

- cloneElement()
- isValidElement()
- React.Children

- React.createRef
- React.forwardRef

- Suspense
	- Suspense lets components “wait” for something before rendering. 
		- Today, Suspense only supports one use case: loading components dynamically with React.lazy. 
		- In the future, it will support other use cases like data fetching.
	- React.lazy
	- React.Suspense

#### React.Component

- The Component Lifecycle
	- Mounting：methods are called in the following order when an instance of a component is being created and inserted into the DOM
		- constructor()
		- static getDerivedStateFromProps()
		- render()
		- componentDidMount()
	- Updating：methods are called in the following order when a component is being re-rendered
		- static getDerivedStateFromProps()
		- shouldComponentUpdate()
		- render()
		- getSnapshotBeforeUpdate()
		- componentDidUpdate()
	- Unmounting： method is called when a component is being removed from the DOM
		- componentWillUnmount()
	- Error Handling：methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.
		- static getDerivedStateFromError()
		- componentDidCatch()
- Other APIs
	- setState()
	- forceUpdate()
- Class Properties
	- defaultProps
	- displayName
- Instance Properties
	- props
	- state

#### ReactDOM

- `ReactDOM.render(element, container[, callback])`
	- Render a React element into the DOM in the supplied container and return a reference to the component (or returns null for stateless components).
	- If the React element was previously rendered into container, this will perform an update on it 
	  and only mutate the DOM as necessary to reflect the latest React element.
        -  If the optional callback is provided, it will be executed after the component is rendered or updated.
        - ReactDOM.render() does not modify the container node (only modifies the children of the container)
        - ReactDOM.render() currently returns a reference to the root ReactComponent instance. 
        	- 不推荐直接使用返回值的引用，因为后期版本的React可能会异步渲染组件
        	- 如果要使用组件实例的引用，推荐使用 callback ref
	- Using ReactDOM.render() to hydrate a server-rendered container is deprecated and will be removed in React 17. Use hydrate() instead.
- `ReactDOM.hydrate(element, container[, callback])`
	- Same as render(), but is used to hydrate a container whose HTML contents were rendered by ReactDOMServer. 
	- React will attempt to attach event listeners to the existing markup.
	- React expects that the rendered content is identical between the server and the client. It can patch up differences in text content
	- If you intentionally need to render something different on the server and the client, you can do a two-pass rendering. 
- `ReactDOM.unmountComponentAtNode(container)`
	- Remove a mounted React component from the DOM and clean up its event handlers and state. 
	- If no component was mounted in the container, calling this function does nothing. 
	- Returns true if a component was unmounted and false if there was no component to unmount.
- `ReactDOM.findDOMNode(component)`
	- findDOMNode is an escape hatch used to access the underlying DOM node. 
	- In most cases, use of this escape hatch is discouraged because it pierces the component abstraction. 
	- It has been deprecated in StrictMode.
	- If ` component` has been mounted into the DOM, this returns the corresponding native browser DOM element. 
	- This method is useful for reading values out of the DOM,
		- such as form field values and performing DOM measurements. 
	- In most cases, you can attach a ref to the DOM node and avoid using findDOMNode at all.
	- When a component renders to null or false, findDOMNode returns null. 
	- When a component renders to a string, findDOMNode returns a text DOM node containing that value. 
	- As of React 16, a component may return a fragment with multiple children, in which case findDOMNode will return the DOM node corresponding to the first non-empty child.
	- findDOMNode only works on mounted components (that is, components that have been placed in the DOM).
	- If you try to call this on a component that has not been mounted yet (like calling findDOMNode() in render() on a component that has yet to be created) an exception will be thrown.
	- findDOMNode cannot be used on function components.
- `ReactDOM.createPortal(child, container)`
	- Portals provide a way to render children into a DOM node that exists outside the hierarchy of the DOM component.

#### ReactDOMServer

- ReactDOMServer enables you to render components to static markup.
	- Typically, it's used on a Node server:
- The following methods can be used in both the server and browser environments
	- renderToString()
	- renderToStaticMarkup()
- The following methods depend on a package (stream) that is only available on the server, and won't work in the browser.
	- renderToNodeStream()
	- renderToStaticNodeStream()
- `ReactDOMServer.renderToString(element)`
	- Render a React element to its initial HTML. 
	- Return an HTML string. 
- `ReactDOMServer.renderToStaticMarkup(element)`
	- Similar to renderToString, except this doesn't create extra DOM attributes that React uses internally, such as `data-reactroot.`
	- If you plan to use React on the client to make the markup interactive, do not use this method. Instead, use renderToString on the server and ReactDOM.hydrate() on the client.
- `ReactDOMServer.renderToNodeStream(element)`
	- Render a React element to its initial HTML. 
	- Return a Readable stream that outputs an HTML string. 
	- The HTML output by this stream is exactly equal to what `ReactDOMServer.renderToString` would return.
- `ReactDOMServer.renderToStaticNodeStream(element)`
	- Similar to renderToNodeStream, except this doesn’t create extra DOM attributes that React uses internally

#### DOM Elements

- React implements a browser-independent DOM system for performance and cross-browser compatibility. 
- In React, all DOM properties and attributes (including event handlers) should be camelCased.
	- The exception is aria-* and data-* attributes, which should be lowercased. For example, you can keep aria-label as aria-label.
- There are a number of attributes that work differently between React and HTML:
	- input-checkbox/radio: checked, defaultChecked
	- className
	- dangerouslySetInnerHTML
		- 不推荐使用，很容易暴露用户，收到xss攻击
		-  React's replacement for using innerHTML in the browser DOM
		- 示例
		```
		function MyComponent() {
		  return <div dangerouslySetInnerHTML={ {__html: 'First &middot; Second'} } />;
		}
		```
	- htmlFor
	- onChange
		- whenever a form field is changed, this event is fired.
		-  React relies on this event to handle user input in real time.
	- selected
		- selected attribute is supported by `<option>` components.
	- style
		- 不推荐直接使用style属性，推荐使用className
		- 一般用来实现动态样式
		- React 会自动为某些内联样式的数字属性值附加一个 “px” 后缀
	- suppressContentEditableWarning
	- suppressHydrationWarning
	- value
		- `<input>` 和 `<textarea>` 组件支持 value 属性，一般用于受控组件
		- `defaultValue` is the uncontrolled equivalent, which sets the value of the component when it is first mounted.
- As of React 16, any standard or custom DOM attributes are fully supported.
- Similarly, all SVG attributes are fully supported:

#### SyntheticEvent

- Your event handlers will be passed instances of SyntheticEvent, a cross-browser wrapper around the browser's native event. 
	- It has the same interface as the browser's native event, including stopPropagation() and preventDefault(), except the events work identically across all browsers.
- If you find that you need the underlying browser event for some reason, simply use the nativeEvent attribute to get it.
- 从v0.14起，从事件处理程序return false将不再停止事件冒泡，应该根据需要手动 e.stopPropagation() 或 e.preventDefault() 
- SyntheticEvent is pooled.
	- This means that the SyntheticEvent object will be reused and all properties will be nullified after the event callback has been invoked.
	-  you cannot access the event in an asynchronous way.
		- If you want to access the event properties in an asynchronous way, you should call event.persist() on the event
- React normalizes events so that they have consistent properties across different browsers.
- Supported Events
	- Clipboard Events
	- Composition Events
	- Keyboard Events
	- Focus Events
	- Form Events
	- Mouse Events
	- Pointer Events
		- As defined in the W3 spec, pointer events extend Mouse Events 
	- Selection Events
	- Touch Events
	- UI Events
	- Wheel Events
	- Media Events
	- Image Events
	- Animation Events
	- Transition Events
	- Other Events

#### Test Utilities

- `import ReactTestUtils from 'react-dom/test-utils';`
- jest是Facebook发布的js测试工具
- enzyme是Airbnb发布的react测试工具
- Shallow Rendering
	- Shallow rendering lets you render a component "one level deep" and assert facts about what its render method returns, 
	  without worrying about the behavior of child components, which are not instantiated or rendered. 
        - This does not require a DOM.  
- Simulate an event dispatch on a DOM node with optional eventData event data.
- renderIntoDocument()
	- Render a React element into a detached DOM node in the document. This function requires a DOM.
- mockComponent()
	- We recommend using shallow rendering or jest.mock() instead.
- isElement()
- isElementOfType()
- isDOMComponent()
- isCompositeComponent()
	- Returns true if instance is a user-defined component, such as a class or a function.
- findAllInRenderedTree()
- findRenderedDOMComponentWithClass()
- findRenderedDOMComponentWithTag()
- findRenderedComponentWithType()

#### Shallow Renderer

- 组件
```
function MyComponent() {
  return (
    <div>
      <span className="heading">Title</span>
      <Subcomponent foo="bar" />
    </div>
  );
}
```

- 测试    

```
import ShallowRenderer from 'react-test-renderer/shallow';

// in your test:
const renderer = new ShallowRenderer();
renderer.render(<MyComponent />);
const result = renderer.getRenderOutput();

expect(result.type).toBe('div');
expect(result.props.children).toEqual([
  <span className="heading">Title</span>,
  <Subcomponent foo="bar" />
]);
```
- Shallow testing currently has some limitations, namely not supporting refs.
- We also recommend checking out Enzyme’s Shallow Rendering API. 
	- It provides a nicer higher-level API over the same functionality.
- `shallowRenderer.render()`
	- similar to ReactDOM.render() but it doesn't require DOM and only renders a single level deep.
- `shallowRenderer.getRenderOutput()`
	- get the shallowly rendered output.

#### Test Renderer

- `import TestRenderer from 'react-test-renderer';`
- This package provides a React renderer that can be used to render React components to pure JavaScript objects,
	- without depending on the DOM or a native mobile environment.
-  this package makes it easy to grab a snapshot of the platform view hierarchy (similar to a DOM tree) rendered by a React DOM or React Native component 
	- without using a browser or jsdom.

#### JavaScript Environment Requirements

- React 16 depends on the collection types Map and Set.
- React also depends on requestAnimationFrame (even in test environments).

#### Glossary of React Terms

- Single-page Application
	- 所有的交互行为不会导致页面重新加载
- js compiler
	- babel
- bundler
	- Bundlers take JavaScript and CSS code written as separate modules (often hundreds of them), and combine them together into a few files better optimized for the browsers. 
	- Some bundlers commonly used in React applications include Webpack and Browserify.
- Package Managers
	- npm
	- yarn
- jsx
- React Elements
	-  An element describes what you want to see on the screen. 
	- React elements are immutable.
	- Typically, elements are not used directly, but get returned from components.
- React Components
	- React components are small, reusable pieces of code that return a React element to be rendered to the page.
	-  if a part of your UI is used several times (Button, Panel, Avatar), or is complex enough on its own (App, FeedStory, Comment), it is a good candidate to be a reusable component.
- props
	- readonly
	- props are inputs to a React component. They are data passed down from a parent component to a child component.
	- props.children is available on every component. It contains the content between the opening and closing tags of a component. 
- state
	- to change state, you must call this.setState()
	- A component needs state when some data associated with it changes over time.
	- Only components defined as classes can have state.
- The most important difference between state and props is that 
	- props are passed from a parent component, but state is managed by the component itself.
- Controlled vs. Uncontrolled Components
	- An input form element whose value is controlled by React is called a controlled component. 
	- An uncontrolled component works like form elements do outside of React. 
- key
	- A `key` is a special string attribute you need to include when creating arrays of elements. 
	- Keys help React identify which items have changed, are added, or are removed.
- ref
	- ref is an attribute that you can attach to any component.
	- 不要过度使用 Refs。如果你发现自己经常在应用程序中使用refs来“搞事情”，请考虑使用状态提升。
- Reconciliation
	- When a component's props or state change, 
	  React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. 
	  When they are not equal, React will update the DOM.
	  This process is called “reconciliation”.
  
