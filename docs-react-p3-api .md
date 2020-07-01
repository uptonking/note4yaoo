---
tags: [api, docs, react]
title: docs-react-p3-api
created: '2020-06-23T07:30:37.293Z'
modified: '2020-06-30T05:13:55.088Z'
---

# docs-react-p3-api

## API for React Component Class Definition

- React lets you define components as classes or functions. 
- Components defined as classes currently provide more features
- The only method you must define in a `React.Component` subclass is called `render()` . 
- We strongly **recommend against creating your own base component classes**. 
  - In React components, code reuse is primarily achieved through composition rather than inheritance.
- The Component Lifecycle
	- Mounting
		- constructor()
		- static getDerivedStateFromProps()
		- render()
		- componentDidMount()
	- Updating
		- static getDerivedStateFromProps()
		- shouldComponentUpdate()
		- render()
		- getSnapshotBeforeUpdate()
		- componentDidUpdate()
	- Unmounting
		- componentWillUnmount()
	- Error Handling
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

- `render(): ReactNode`
- When called, it should examine `this.props` and `this.state` and return one of the following types
  - React elements. 
    - Typically created via JSX. 
    - For example, `<div />` and `<MyComponent />` are React elements that instruct React to render a DOM node
  - Arrays and fragments. 
    - Let you return multiple elements from render
  - Portals. 
    - Let you render children into a different DOM subtree
  - String and numbers.
    - These are rendered as text nodes in the DOM
  - Booleans or null. 
    - Render nothing. 
    - Mostly exists to support return `test && <Child />` pattern
- `render()` function should be pure, meaning that it does not modify component state, it returns the same result each time it’s invoked, and it does not directly interact with the browser.
- If you need to interact with the browser, perform your work in `componentDidMount()` or the other lifecycle methods instead.
- Keeping render() pure makes components easier to think about

- `constructor(props: Readonly<P>);`
- It is called before it is mounted.
- If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your React component.
- You should not call `setState()` in the `constructor()` . 
  - Instead, if your component needs to use local state, assign the initial state to this.state directly in the constructor
- Constructor is the only place where you should assign `this.state` directly. 
  - In all other methods, you need to use `this.setState()` instead.
- Avoid introducing any side-effects or subscriptions in the constructor. 
  - For those use cases, use `componentDidMount()` instead.
- Avoid copying props into state
  - updates to the color prop won’t be reflected in the state
  - Only use this pattern if you intentionally want to ignore prop updates. In that case, it makes sense to rename the prop to be called initialColor or defaultColor

- `componentDidMount?(): void`
- It is invoked immediately after a component is mounted (inserted into the tree). 
  - reading `clientHeight` from within componentDidMount should force the browser to do a *sync* layout (not great but sometimes necessary) and return a valid clientHeight.
- Initialization that requires DOM nodes should go here. 
- If you need to load data from a remote endpoint, this is a good place to instantiate the network request.
- This method is a good place to set up any subscriptions. 
  - If you do that, don’t forget to unsubscribe in `componentWillUnmount()` .
- You **may call `setState()` immediately in `componentDidMount()` **. 
  - It will trigger an extra rendering, but it will happen before the browser updates the screen. 
  - This guarantees that even though the `render()` will be called twice in this case, the user won’t see the intermediate state.
  - Use this pattern with caution because it often causes performance issues. 
  - In most cases, you should be able to assign the initial state in the constructor() instead. 
  - It can, however, be necessary for cases like modals and tooltips, when you need to measure a DOM node before rendering something that depends on its size or position.

- `ccomponentDidUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>, snapshot?: SS): void`
- It is invoked immediately after updating occurs.
- Use this as an opportunity to operate on the DOM when the component has been updated. 
- This is also a good place to do network requests as long as you compare the current props to previous props (e.g. a network request may not be necessary if the props have not changed).
- You **may call `setState()` immediately in `componentDidUpdate()` ** but note that it must be wrapped in a condition like in the example above, or you’ll cause an infinite loop.
  - It would also cause an extra re-rendering which, while not visible to the user, can affect the component performance. 
  - If you’re trying to “mirror” some state to a prop coming from above, consider using the prop directly instead.
- If your component implements the `getSnapshotBeforeUpdate()` lifecycle (which is rare), the value it returns will be passed as a third “snapshot” parameter to `componentDidUpdate()` . Otherwise this parameter will be undefined.

- `componentWillUnmount?(): void`
- It is invoked immediately before a component is unmounted and destroyed. 
- Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in `componentDidMount()` .
- You **should not call `setState()` in `componentWillUnmount()` ** because the component will never be re-rendered. 
- Once a component instance is unmounted, it will never be mounted again.

- `shouldComponentUpdate?(nextProps: Readonly<P>, nextState: Readonly<S>, nextContext: any): boolean`
- It is invoked before rendering when new props or state are being received. 
- Defaults to `true` . 
- The default behavior is to re-render on every state change, and in the vast majority of cases you should rely on the default behavior.
- This method only exists as a performance optimization
- Consider using the built-in `PureComponent` instead of writing shouldComponentUpdate() by hand.
- If you are confident you want to write it by hand, you may compare this.props with nextProps and this.state with nextState and return `false` to tell React the update can be skipped. 
- Note that returning false does not prevent child components from re-rendering when their state changes.
- We do not recommend doing deep equality checks or using `JSON.stringify()` in `shouldComponentUpdate()` . 
  - It is very inefficient and will harm performance.
- Currently, if shouldComponentUpdate() returns false, then componentWillUpdate(), render(), and componentDidUpdate() will not be invoked. 
- In the future React may treat shouldComponentUpdate() as a hint rather than a strict directive, and returning false may still result in a re-rendering of the component.

- `static getDerivedStateFromProps(nextProps, prevState)`
- It is invoked right **before calling the render method**, both on the initial mount and on subsequent updates. 
  - Its presence prevents any of the deprecated lifecycle methods from being invoked
- It should **return an object to update the state**, or null to update nothing.
- Returns an update to a component's state based on its new props and old state.
- This method exists for rare use cases where the state depends on changes in props over time.
- If you need to perform a side effect (for example, data fetching or an animation) in response to a change in props, use `componentDidUpdate` lifecycle instead.
- If you want to re-compute some data only when a prop changes, use a memoization helper instead.
- If you want to “reset” some state when a prop changes, consider either making a component fully controlled or fully uncontrolled with a `key` instead.
- This method doesn’t have access to the component instance. 
  - If you’d like, you can reuse some code between getDerivedStateFromProps() and the other class methods by extracting pure functions of the component props and state outside the class definition.
- Note that this method is fired on every render, regardless of the cause. 
  - This is in contrast to componentWillReceiveProps, which only fires when the parent causes a re-render and not as a result of a local setState.
- getDerivedStateFromProps exists for only one purpose.
  - It enables a component to update its internal state as the result of changes in props. 
- 执行时机
  - Firstly in version of React 16.3, getDerivedStateFromProps() just was invoked when updating props
  - But since version of React 16.4, getDerivedStateFromProps() is invoked when updating props and updating state (regardless of the reason for re-rendering).
  - getDerivedStateFromProps() is invoked before render() method under that conditions;
    - Initial mount
    - Every state and prop updating
    - forceUpdate
    - It's called any time a parent component rerenders, regardless of whether the props are “different” from before. 
  - 如果setState和getDerivedStateFromProps同时存在，则getDerivedStateFromProps的参数中prevState是setState后的值，可自行创建ControlledInput组件测试，所以可以在这个方法中拦截强行修改state
- ref
  - repeat https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
  - https://tech.youzan.com/getderivedstatefromprops/
  - http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

- `getSnapshotBeforeUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>): SS | null`
- It is invoked right before the most recently rendered output is committed to e.g. the DOM. 
- It enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed. 
- Any value returned by this lifecycle will be passed as a parameter to `componentDidUpdate()` .
  - A snapshot value (or null) should be returned.
- It may occur in UIs like a chat thread that need to handle scroll position in a special way

- `static getDerivedStateFromError(error)`
- It is invoked after an error has been thrown by a descendant component. 
- It receives the error that was thrown as a parameter and should return a value to update state
- `getDerivedStateFromError()` is called during the “render” phase, so side-effects are not permitted.
- For those use cases, use componentDidCatch() instead.

- `componentDidCatch(error, info)`
- It is invoked after an error has been thrown by a descendant component.
- It receives two parameters:
  - error - The error that was thrown.
  - info - An object with a `componentStack` key containing information about which component threw the error.
- `componentDidCatch()` is called during the “commit” phase, so side-effects are permitted. 
- It should be used for things like logging errors
- In the event of an error, you can render a fallback UI with `getDerivedStateFromError()`
- `componentWillMount()`
- It is invoked just before mounting occurs. 
- It is called before `render()` , therefore calling `setState()` synchronously in this method will not trigger an extra rendering. 
- Generally, we recommend using the `constructor()` instead for initializing state.
- Avoid introducing any side-effects or subscriptions in this method.
  -  For those use cases, use `componentDidMount()` instead.

- `componentWillReceiveProps(nextProps)`
- It is invoked before a mounted component receives new props. 
- If you need to update the state in response to prop changes (for example, to reset it), you may compare this.props and nextProps and perform state transitions using `this.setState()` in this method.
- Note that if a parent component causes your component to re-render, this method will be called even if props have not changed. 
- Make sure to compare the current and next values if you only want to handle changes.
- React only calls this method if some of component’s props may update. Calling this.setState() generally doesn’t trigger this method.

- `componentWillUpdate(nextProps, nextState)`
- It is invoked just before rendering when new props or state are being received. 
- Use this as an opportunity to perform preparation before an update occurs. 
- Note that you cannot call this.setState() here; nor should you do anything else (e.g. dispatch a Redux action) that would trigger an update to a React component before UNSAFE_componentWillUpdate() returns
- Typically, this method can be replaced by `componentDidUpdate()` . 
- If you were reading from the DOM in this method (e.g. to save a scroll position), you can move that logic to `getSnapshotBeforeUpdate()` .

- `setState(updaterFunc, [callback])`
  - updaterFunc: `(state, props) => stateChange`
- `setState()` enqueues changes to the component state and tells React that this component and its children need to be re-rendered with the updated state. 
- This is the primary method you use to update the user interface in response to event handlers and server responses.
- React may delay it, and then update several components in a single pass. React does not guarantee that the state changes are applied immediately.
- This makes reading `this.state` right after calling `setState()` a potential pitfall. 
  - Instead, use `componentDidUpdate` or a setState callback ( `setState(updater, callback)` ), either of which are guaranteed to fire after the update has been applied. 
- If you need to set the state based on the previous state, use the updater argument
- **setState() will always lead to a re-render** unless shouldComponentUpdate() returns `false` .
- `this.state` should not be directly mutated. Instead, changes should be represented by building a new object based on the input from state and props.
- Both state and props received by the updater function are guaranteed to be up-to-date. 
  - The return value of the updater is shallowly merged with state.
- You may optionally pass an object as the first argument to setState() instead of a function
  - This performs a shallow merge of the arg object into the new state
- The optional second parameter callback function that will be executed once setState is completed and the component is re-rendered. 
  - Generally we recommend using `componentDidUpdate()` for such logic instead.
- `setState()` is asynchronous, and multiple calls during the same cycle may be batched together.
- Subsequent calls will override values from previous calls in the same cycle, so the quantity will only be incremented once.
- If the next state depends on the current state, we recommend using the updater function form

``` js
this.setState((state) => {
  return { quantity: state.quantity + 1 };
});
```

- `component.forceUpdate(callback)`
- By default, when your component’s state or props change, your component will re-render. 
- If your render() method depends on some other data, you can tell React that the component needs re-rendering by calling forceUpdate()
- Calling forceUpdate() will cause render() to be called on the component, skipping shouldComponentUpdate(). 
  - This will trigger the normal lifecycle methods for child components, including the shouldComponentUpdate() method of each child. 
  - React will still only update the DOM if the markup changes.
- Normally you should try to avoid all uses of forceUpdate() and only read from this.props and this.state in render().

- `MyComponent.defaultProps={}`
- set the default props for the class.

- `MyComponent.displayName='strName'`
- used in debugging messages. 
- Usually, you don’t need to set it explicitly because it’s inferred from the name of the function or class that defines the component. 
- You might want to set it explicitly if you want to display a different name for debugging purposes or when you create a higher-order component

- `props`
- `this.props` contains the props that were defined by the caller of this component. 
- `this.props.children` is a special prop, typically defined by the child tags in the JSX expression rather than in the tag itself.

- `state`
- `this.state` contains data specific to this component that may change over time. 
- The state is user-defined, and it should be a plain JavaScript object.
- If some value isn’t used for rendering or data flow (for example, a timer ID), you don’t have to put it in the state. 
  - Such values can be defined as fields on the component instance.
- Never mutate this.state directly, as calling setState() afterwards may replace the mutation you made. 
- Treat this.state as if it were immutable.

## React Top-Level API

- Components
  - React. Component
  - React. PureComponent
  - React.memo
  - React. Fragment
- Creating React Elements
  - createElement()
  - createFactory()      
- Transforming Elements
  - cloneElement()
  - isValidElement()
  - React. Children
- Refs
  - React.createRef
  - React.forwardRef
- Suspense
  - React.lazy
  - React. Suspense
- Hooks
  - useState
  - useEffect
  - useContext
  - useReducer
  - useCallback
  - useMemo
  - useRef
  - useImperativeHandle
  - useLayoutEffect
  - useDebugValue

- `React.PureComponent`
- `React.Component` doesn’t implement `shouldComponentUpdate()` , but `React.PureComponent` implements it with a shallow prop and state comparison.
  - src `!shallowEqual(oldProps,newProps) || !shallowEqual(oldState,newState) `
  - Performs equality by iterating through keys on an object
    - If you mean individual properties, afaik they're compared using `Object.is` algorithm (which is slightly different from `===` because it also handles NaN).
    - Returns false when any key has values which are not strictly equal between the arguments.
    - Returns true when the values of all keys are strictly equal.
  - https://github.com/facebook/react/issues/13468
  - shallowCompare is a legacy add-on. Use React.memo or React. PureComponent instead.
- `React.PureComponent` ’s `shouldComponentUpdate()` skips prop updates for the whole component subtree. Make sure all the children components are also “pure”.
- Using a render prop can negate the advantage that comes from using React. PureComponent if you create the function inside a render method.
- You can't use PureComponent and specify shouldComponentUpdate at the same time. 
- If your component utilizes a render prop, you can't do a shallow comparison, you would always need to re-render since the function reference isn't guaranteed to change on each render.
- If you use render props, make sure shouldComponentUpdate() in your components always respects children (like PureComponent does). Otherwise you can end up with very confusing issues
- Having each of your components check to see if props or state have changed, even if it is a shallow check, takes up some computation time. Don't overuse it.

``` js
class App extends React.PureComponent {
  state = {
    ele: { a: '1' }
  }
  // click event triggers render every time.
  // 因为setState每次都会通过Object.assign合并属性成一个新对象
  trigger = () => {
    console.log('click')
    this.setState({ ele: { a: '1' } })
  }
  render() {
    console.log('render')
    return (
      <div onClick={this.trigger}>click here to trigger setState</div>
    );
  }
}
```

- `React.memo`
- React.memo is a higher order component. 
- It’s similar to `React.PureComponent` but for function components instead of classes.
- React.memo **only checks for prop changes**. 
  - If your function component wrapped in React.memo has a `useState` or `useContext` Hook in its implementation, it will still rerender when state or context change.
- By default it will only shallowly compare complex objects in the props object. 
- If you want control over the comparison, you can also provide a custom comparison function as the second argument.
  - return true if props are equal, false if not equal
- This method only exists as a performance optimization. Do not rely on it to “prevent” a render, as this can lead to bugs.

- `React.createElement(type,[props],[...children])`
- Code written with JSX will be converted to use React.createElement().

- `React.cloneElement(element,[props],[...children])`
- Clone and return a new React element using element as the starting point. 
- The resulting element will have the original element’s props with the new props merged in shallowly. 
- New children will replace existing children. 
- `key` and `ref` from the original element will be preserved.
- almost equivalent to `<element.type {...element.props} {...props}>{children}</element.type>`
- `React.createFactory(type)`
- This helper is considered legacy
- We encourage you to either use JSX or use `React.createElement()` directly instead.

- `React.isValidElement(object)`
- Verifies the object is a React element.

- `React.Children`
- `React.Children.map(children, function[(thisArg)])`
  - If children is a `Fragment` , it will be treated as a single child and not traversed.
- `React.Children.forEach(children, function[(thisArg)])`
- `React.Children.count(children)`
- `React.Children.only(children)`
  - React. Children.only() does not accept the return value of React. Children.map() because it is an array rather than a React element.
- `React.Children.toArray(children)`
  - Returns the `children` opaque data structure as a flat array with keys assigned to each child. 
  - Useful if you want to manipulate collections of children in your render methods
  - especially if you want to reorder or slice `this.props.children` before passing it down
  - React. Children.toArray() changes keys to preserve the semantics of nested arrays when flattening lists of children. 
  - That is, toArray prefixes each key in the returned array so that each element’s key is scoped to the input array containing it.

- `React.Fragment`
- return multiple elements in a render() method without creating an additional DOM element

- `React.createRef`
- creates a ref that can be attached to React elements via the `ref` attribute

- `React.forwardRef`
- creates a React component that forwards the ref attribute it receives to another component below in the tree
- Forwarding refs to DOM components
- Forwarding refs in higher-order-components
- accepts a rendering function as an argument. 
  - React will call this function with props and ref as two arguments. 
  - This function should return a React node.

- `const MyComponent = React.lazy(() => import('./MyComponent'));`
- define a component that is loaded dynamically. 
- This helps reduce the bundle size to delay loading components that aren’t used during the initial render.
- use it for code splitting 
- Rendering lazy components requires that there’s a `<React.Suspense>` component higher in the rendering tree
- Using React.lazy with dynamic import requires Promises to be available in the JS environment. 

- `React.Suspense`
- specify the loading indicator in case some components in the tree below it are not yet ready to render. 
- Today, lazy loading components is **the only use case** supported by `<React.Suspense>`
- The best practice is to place `<Suspense>` where you want to see a loading indicator, but to use lazy() wherever you want to do code splitting.
- While this is not supported today, in the future we plan to let `Suspense` handle more scenarios such as data fetching.

## ReactDOM

- The `react-dom` package provides DOM-specific methods that can be used at the top level of your app and as an escape hatch to get outside of the React model if you need to. 
- Most of your components should not need to use this module
  - render()
  - hydrate()
  - unmountComponentAtNode()
  - findDOMNode()
  - createPortal()

- `ReactDOM.render(element, container[, callback])`
- Render a React element into the DOM in the supplied `container` and return a reference to the component (or returns null for stateless components).
- If the React element was previously rendered into container, this will perform an update on it 

  and only mutate the DOM as necessary to reflect the latest React element.

- If the optional callback is provided, it will be executed after the component is rendered or updated.
- It controls the contents of the container node you pass in. 
  - Any existing DOM elements inside are replaced when first called. 
  - Later calls use React’s DOM diffing algorithm for efficient updates
- It does not modify the container node (only modifies the children of the container).
- It currently returns a reference to the root ReactComponent instance. 
  - However, using this return value should be avoided because future versions of React may render components asynchronously in some cases. If y
  - ou need a reference to the root ReactComponent instance, the preferred solution is to attach a callback ref to the root element.
- Using ReactDOM.render() to hydrate a server-rendered container is deprecated and will be removed in React 17. Use hydrate() instead

- `ReactDOM.hydrate(element, container[, callback])`
- Same as `ReactDOM.render()` , but is used to hydrate a container whose HTML contents were rendered by ReactDOMServer. 
- React will attempt to attach event listeners to the existing markup.
- React expects that the rendered content is identical between the server and the client.
- It can patch up differences in text content, but you should treat mismatches as bugs and fix them
- If a single element’s attribute or text content is unavoidably different between the server and the client (for example, a timestamp), you may silence the warning by adding suppressHydrationWarning={true} to the element. 
  - It only works one level deep, and is intended to be an escape hatch.
  - Don’t overuse it. 
- If you intentionally need to render something different on the server and the client, you can do a two-pass rendering. 
  - this approach will make your components slower because they have to render twice, so use it with caution

- `ReactDOM.unmountComponentAtNode(container)`
- Remove a mounted React component from the DOM and clean up its event handlers and state. 
- If no component was mounted in the container, calling this function does nothing. 
- Returns `true` if a component was unmounted and `false` if there was no component to unmount.

- `ReactDOM.findDOMNode(component)`
- It is an escape hatch used to access the underlying DOM node. 
- In most cases, use of this escape hatch is discouraged because it pierces the component abstraction. 
- It has been deprecated in StrictMode.
- If component has been mounted into the DOM, this returns the corresponding native browser DOM element. 
- This method is useful for reading values out of the DOM, such as form field values and performing DOM measurements. 
- In most cases, you can **attach a `ref` to the DOM node and avoid using `findDOMNode` at all**.
- When a component renders to null or false, findDOMNode returns null. 
- When a component renders to a string, findDOMNode returns a text DOM node containing that value. 
- As of React 16, a component may return a `Fragment` with multiple children, in which case findDOMNode will return the DOM node corresponding to the first non-empty child.
- findDOMNode only works on mounted components (that is, components that have been placed in the DOM).
- If you try to call this on a component that has not been mounted yet (like calling `findDOMNode()` in `render()` on a component that has yet to be created), an exception will be thrown.
- findDOMNode cannot be used on function components.

- `ReactDOM.createPortal(child, container)`
- Portals provide a way to render children into a DOM node that exists outside the hierarchy of the DOM component.

## ReactDOMServer

- ReactDOMServer enables you to render components to static markup.
	- Typically, it's used on a Node server
- The following methods can be used in both the server and browser environments
	- renderToString()
	- renderToStaticMarkup()
- The following methods depend on a package ( `stream` ) that is only available on the server
	- renderToNodeStream()
	- renderToStaticNodeStream()

- `ReactDOMServer.renderToString(element)`
- Render a React element to its initial HTML. 
- Return an HTML string. 
- You can use this method to generate HTML on the server and send the markup down on the initial request for faster page loads and to allow search engines to crawl your pages for SEO purposes.
- If you call ReactDOM.hydrate() on a node that already has this server-rendered markup, React will preserve it and only attach event handlers, allowing you to have a very performant first-load experience.

- `ReactDOMServer.renderToStaticMarkup(element)`
- Similar to `renderToString` , except this doesn't create extra DOM attributes that React uses internally, such as `data-reactroot.`
- This is useful if you want to use React as a simple static page generator, as stripping away the extra attributes can save some bytes.  
- If you plan to use React on the client to make the markup interactive, do not use this method. 
- Instead, use renderToString on the server and ReactDOM.hydrate() on the client.

- `ReactDOMServer.renderToNodeStream(element)`
- Render a React element to its initial HTML. 
- Return a Readable stream that outputs an HTML string. 
- The HTML output by this stream is exactly equal to what `ReactDOMServer.renderToString` would return.
- Server-only. This API is not available in the browser.
- The stream returned from this method will return a byte stream encoded in utf-8. 
  - If you need a stream in another encoding, take a look at a project like iconv-lite, which provides transform streams for transcoding text.

- `ReactDOMServer.renderToStaticNodeStream(element)`
- Similar to `renderToNodeStream` , except this doesn’t create extra DOM attributes that React uses internally

## DOM Elements

- React implements a browser-independent DOM system for performance and cross-browser compatibility. 
- In React, all DOM properties and attributes (including event handlers) should be camelCased.
	- The exception is `aria-*` and `data-*` attributes, which should be lowercased.
  - For example, you can keep `aria-label` as `aria-label` .
- There are a number of attributes that work differently between React and HTML
- checked
  - The checked attribute is supported by `<input>` components of type `checkbox` or `radio` . 
  - You can use it to set whether the component is checked. 
  - This is useful for building controlled components. 
  - `defaultChecked` is the uncontrolled equivalent, which sets whether the component is checked when it is first mounted.
- className
- dangerouslySetInnerHTML
  - It is React’s replacement for using `innerHTML` in the browser DOM. 

``` js
  function MyComponent() {
    return <div dangerouslySetInnerHTML={ {__html: 'First &middot; Second'} } />;
  }
```

- htmlFor
- onChange
  - whenever a form field is changed, this event is fired.
  - We intentionally do not use the existing browser behavior because onChange is a misnomer for its behavior and React relies on this event to handle user input in real time.
- selected
  - `selected` attribute is supported by `<option>` components.
- style
  - using the `style` attribute as the primary means of styling elements is generally not recommended.
  - style is most often used in React applications to add dynamically-computed styles at render time.
  - styles are not autoprefixed. 
  - React will automatically append a “px” suffix to certain numeric inline style properties
- suppressContentEditableWarning
  - This attribute suppresses that warning. 
- suppressHydrationWarning
  - React will not warn you about mismatches in the attributes and the content of that element.
- value
  - `value` attribute is supported by `<input>` and `<textarea>` components. 
  - You can use it to set the value of the component.
  - This is useful for building controlled components. 
  - `defaultValue` is the uncontrolled equivalent, which sets the value of the component when it is first mounted.
- As of React 16, any standard or custom DOM attributes are fully supported.
- Similarly, all SVG attributes are fully supported
- You may also use custom attributes as long as they’re fully lowercase.

## SyntheticEvent

- Your event handlers will be passed instances of `SyntheticEvent` , a cross-browser wrapper around the browser's native event. 
- It has the same interface as the browser's native event, including stopPropagation() and preventDefault(), except the **events work identically across all browsers**.
- If you find that you need the underlying browser event for some reason, simply use the `nativeEvent` attribute to get it.
- Every `SyntheticEvent` object has the following attributes
  - type string 
  - target DOMEventTarget 
  - currentTarget DOMEventTarget 
  - nativeEvent DOMEvent 
  - eventPhase number 
  - timeStamp number 
  - bubbles boolean 
  - cancelable boolean 
  - defaultPrevented boolean 
  - isTrusted boolean 
  - preventDefault() void 
  - isDefaultPrevented() boolean 
  - stopPropagation() void 
  - isPropagationStopped() boolean 
  - persist() void 
- As of React v0.14, returning `false` from an event handler will no longer stop event propagation. 
  - Instead, `e.stopPropagation()` or `e.preventDefault()` should be triggered manually
- `SyntheticEvent` is pooled.
	- This means that the `SyntheticEvent` object will be reused 
  - and all properties will be nullified after the event callback has been invoked.
	- you cannot access the event in an asynchronous way.(like in setTimeout)
  - This is for performance reasons. As such, you cannot access the event in an asynchronous way
- If you want to access the event properties in an asynchronous way, you should call `event.persist()` on the event, which will remove the synthetic event from the pool and allow references to the event to be retained by user code.
- React normalizes events so that they have consistent properties across different browsers.
- The event handlers below are triggered by an event in the bubbling phase. 
  - To register an event handler for the capture phase, append Capture to the event name; 
  - for example, instead of using `onClick` , you would use `onClickCapture` to handle the click event in the capture phase
- Supported Events
	- Clipboard Events
	- Composition Events
	- Keyboard Events
	- Focus Events
	- Form Events
  - Generic Events
	- Mouse Events
	- Pointer Events
	- Selection Events
	- Touch Events
	- UI Events
	- Wheel Events
	- Media Events
	- Image Events
	- Animation Events
	- Transition Events
	- Other Events

## Test Utilities

- `import ReactTestUtils from 'react-dom/test-utils';`
- At Facebook we use Jest for painless JavaScript testing.
- https://jestjs.io/docs/en/tutorial-react
- https://enzymejs.github.io/enzyme/
- Shallow Rendering
	- Shallow rendering lets you render a component "one level deep" and assert facts about what its render method returns, without worrying about the behavior of child components, which are not instantiated or rendered. 
  - This does not require a DOM.  
- Simulate an event dispatch on a DOM node with optional eventData event data.
- renderIntoDocument()
	- Render a React element into a detached DOM node in the document. This function requires a DOM.
- mockComponent() (legacy API)
	- We recommend using shallow rendering or `jest.mock()` instead.
- isElement()
- isElementOfType()
- isDOMComponent()
- isCompositeComponent()
	- Returns true if instance is a user-defined component, such as a class or a function.
- findAllInRenderedTree()
- findRenderedDOMComponentWithClass()
- findRenderedDOMComponentWithTag()
- findRenderedComponentWithType()

- Shallow Renderer Test Example
- 组件

``` js
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

``` js
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

## Test Renderer

- `import TestRenderer from 'react-test-renderer';`
- This package provides a React renderer that can be used to render React components to pure JavaScript objects, without depending on the DOM or a native mobile environment.
- This package makes it easy to grab a snapshot of the platform view hierarchy (similar to a DOM tree) rendered by a React DOM or React Native component without using a browser or jsdom
- You can use Jest’s snapshot testing feature to automatically save a copy of the JSON tree to a file and check in your tests that it hasn’t changed
- example

``` js
function MyComponent() {
  return (
    <div>
      <SubComponent foo="bar" />
      <p className="my">Hello</p>
    </div>
  )
}

function SubComponent() {
  return (
    <p className="sub">Sub</p>
  );
}

const testRenderer = TestRenderer.create(<MyComponent />);
const testInstance = testRenderer.root;

expect(testInstance.findByType(SubComponent).props.foo).toBe('bar');
expect(testInstance.findByProps({ className: "sub" }).children).toEqual(['Sub']);
```

- `TestRenderer.create(element, options);`
- Returns a TestRenderer instance
- Create a TestRenderer instance with the passed React element. 
- It doesn’t use the real DOM, but it still fully renders the component tree into memory so you can make assertions about it. 
- You can pass `createNodeMock` function to `TestRenderer.create` as the option, which allows for custom mock refs. 
- `createNodeMock` accepts the current element and should return a mock ref object. 
- This is useful when you test a component that relies on refs.

- `testRenderer.toJSON()`
- Return an object representing the rendered tree. 
- This tree only contains the platform-specific nodes like `<div>` or `<View>` and their props, but doesn’t contain any user-written components. 
- This is handy for snapshot testing.

- `testRenderer.root`
- Returns the root “test instance” object that is useful for making assertions about specific nodes in the tree.
- You can use it to find other “test instances” deeper below.

- `testInstance.findByType(type)`
- Find a single descendant test instance with the provided `type` . 
- If there is not exactly one test instance with the provided type, it will throw an error.

- `testInstance.findByProps(props)`
- Find a single descendant test instance with the provided `props` . 
- If there is not exactly one test instance with the provided props, it will throw an error.

- `testInstance.type`
- The component type corresponding to this test instance. 
- For example, a `<Button />` component has a type of `Button` .

## JavaScript Environment Requirements

- React 16 depends on the collection types `Map` and `Set` .
- React also depends on `requestAnimationFrame` (even in test environments).

## Glossary of React Terms

- Single-page Application
  - Any interactions with the page or subsequent pages do not require a round trip to the server which means the page is not reloaded
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
	- An element describes what you want to see on the screen. 
	- React elements are immutable.
	- Typically, elements are not used directly, but get returned from components.
- React Components
	- React components are small, reusable pieces of code that return a React element to be rendered to the page.
  - Components can return other components, arrays, strings and numbers.
	- If a part of your UI is used several times (Button, Panel, Avatar), or is complex enough on its own (App, FeedStory, Comment), it is a good candidate to be a reusable component.
  - Component names should also always start with a capital letter
- props
	- props are inputs to a React component. 
  - They are data passed down from a parent component to a child component.
	- props are readonly. They should not be modified in any way
- props.children 
  - `props.children` is available on every component. 
  - It contains the content between the opening and closing tags of a component. 
  - For components defined as classes, use `this.props.children`
- state
	- A component needs `state` when some data associated with it changes over time.
	- The most important difference between state and props is that `props` are passed from a parent component, but `state` is managed by the component itself. 
  - A component cannot change its props, but it can change its state.
  - For each particular piece of changing data, there should be just one component that “owns” it in its state. 
  - Don’t try to synchronize states of two different components. 
  - Instead, lift it up to their closest shared ancestor, and pass it down as props to both of them.
- Lifecycle methods 
  - are custom functionality that gets executed during the different phases of a component.
- Controlled vs. Uncontrolled Components
  - React has two different approaches to dealing with form inputs.
	- An input form element whose value is controlled by React is called a controlled component. 
	- An uncontrolled component works like form elements do outside of React. 
- key
	- A `key` is a special string attribute you need to include when creating arrays of elements. 
	- Keys help React identify which items have changed, are added, or are removed.
  - It is important that keys have a “stable identity” across re-renders so that React can determine when items are added, removed, or re-ordered. 
- ref
	- React supports a special attribute that you can attach to any component. 
	- Use refs sparingly. 
  - If you find yourself often using refs to “make things happen” in your app, consider getting more familiar with top-down data flow.
- Reconciliation
	- When a component's props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. 
	- When they are not equal, React will update the DOM.
	- This process is called “reconciliation”.

  
