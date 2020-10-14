---
title: note-react-rfc-createElement
tags: [react, rfc, roadmap]
created: '2020-07-16T09:54:01.538Z'
modified: '2020-07-17T06:01:14.632Z'
---

# note-react-rfc-createElement

## React createElement changes and surrounding deprecations

- The goal is to bring element creation down to this logic:

``` JS
function jsx(type, props, key) {
  return {
    $$typeof: ReactElementSymbol,
    type,
    key,
    props,
  };
}
```

- This proposal simplifies how `React.createElement` works and ultimately lets us remove the need for forwardRef.
- In the next major version, we would actually move ref/defaultProps resolution to classes. forwardRef would extract it from props, but now we could soft-deprecate forwardRef and instead just recommend pulling it off of props.

- In React 0.12 time frame we did a bunch of small changes to how `key` , `ref` and `defaultProps` works. 
  - Particularly, they get resolved early on in the `React.createElement(...)` call. 
  - This made sense when everything was classes, but since then, we've introduced function components. 
- Element creation is a hot path because it is used a lot but also because it is always recreated in rerenders.
- `React.createElement(...)` was never intended to be the implementation of JSX but was the best we could do with tooling at the time. 
- It has a number of issues:
  - The transform uses `React.createElement` which is a dynamic property look up instead of a constant closed over module scope.
  - We don't know if the passed in props is a user created object that can be mutated so we must always clone it once.
  - `.defaultProps` in element creation doesn't work with `React.lazy` so in that case we also have to check for resolving defaultProps in the render phase too
  - Children are passed as var args and we have to patch them onto props dynamically instead of statically knowning the shape of the props at the callsite.
  - `key` and `ref` gets extracted from JSX props provided so even if we didn't clone, we'd have to delete a prop, which would cause that object to become map-like.
  - The transform relies on a the name React being in scope of JSX. I.e. you have to import the default.

- Pass key separately from props
  - Currently, `key` is passed as part of `props` , but we'll want to special case it in the future so we need to pass it as a separate argument.
- Always pass children as props
  - In createElement, children gets passed as var args. 
  - In the new transform, we'll always just add them to the props object - inline.
  - The reason we pass them as var args is to distinguish static children from dynamic ones in DEV. 
  - We can instead pass a boolean flag or use two different functions to distinguish them.
- avoid clone props
  - `<div {...props} />` can currently be safely optimized to `createElement('div', props)`
  - That's because `createElement()` always clones the passed object. 
  - We want to avoid cloning in the `jsx()` function with the new transform. 
  - Most of the time this won't be observable because the JSX creates a new inline object anyway. 
  - his would be a breaking change, but we could always clone in the call in a minor and then make the breaking change later in a major. 
  - The new semantics would be that the passed in object gets frozen (in DEV).

- ### Deprecate "module pattern" components.

``` JS
// It causes some implementation complexity just by existing.
const Foo = (props) => {
  return {
    onClick() {
      //...
    }
    render() {
      return <div onClick={this.onClick.bind(this)} />;
    }
  }
};
```

- ### Deprecate `defaultProps` on function components.
  - defaultProps is very useful on classes because the props object gets passed to many different methods. Life-cycles, callbacks etc.
  - This makes it hard to use JS default arguments because you'd have to replicate the same defaults in each function.
  - However, in function components there really isn't much need for this pattern since you can just use JS default arguments and all the places where you typically use these values are within the same scope.

- ### Move `defaultProps` resolution to class render time.
  - The upgrade path here, is to just avoid reading from `element.props` or move away from relying on `defaultProps` and passing them in explicitly or resolving them in the class.
  - In the next major, we'd stop resolving defaultProps during element creation and instead, we'd only resolve it right before we pass them into class components.

- ### Deprecate spreading `key` from objects.
  - The problem with this is that we can't statically know if this object is going to pass a `key` or not.
  - So for every set of props, we have to do an expensive dynamic property check to see if there is a key prop in there.
  - To minimize churn and open up a larger discussion about this syntax, we'd instead treat `key` as a keyword in JSX and pass it separately.
  - An unresolved issue is how we distinguish `<div key="Hi" {...props} />` from `<div {...props} key="Hi" />` which currently have different semantics depending on if props has a `key` .
  - In a later major, we'd stop extracting key from props and therefore props is now just passthrough.

- ### Deprecate string refs 
  - We'll remove string refs and that will let us get rid of the `_owner` field from elements.

- ### Move `ref` extraction to class render time and `forwardRef` render time.
  - In a minor, we'll add an enumerable getter in DEV for `props.ref` if a ref is defined on its element. This will warn if you try to access it. 
    - However, in class components, we'll detect this and create a copy of the props before passing it into the class. 
    - The same thing applies to `forwardRef` .
    - We can also special case `cloneElement` .
  - Since you can't pass a `ref` to anything but host, class and forwardRef, it should be fairly unusual that you're spreading `props` that has a `ref` on it.
  - In the next major, we'll start copying the `ref` onto both the `props` and the `element.ref` . 
    - React will now use the `props.ref` as the source of truth for `forwardRef` and classes 
    - and it will still create a shallow copy of props that excludes the ref in these cases. 
    - At the same time, we'll add a getter for element.ref in DEV that warns if you access it. 
  - The upgrade path is now to just access it off props if you need it from the element.
    - 可以尝试使用callback ref代替forwardRef
    - 也可以使用自定义名称，如refInput

- I'm wondering if the jsx constructor should accept `ref` as an argument too.
  - The original plan was to pass `ref` separately too, but now I’m thinking that ref should just be a normal prop in all cases except when it is passed to a class component. 
  - In that case we can strip it off in a shallow clone of the props that excludes it.
  - The original reason for treating `ref` separately was because it's easy to accidentally spread it along (and before that transferPropsTo).
  - If `ref` was part of props, then in this pattern it is easy to forget to avoid passing along the ref. Which is extra bad because refs really should only be attached to one thing at a time.
  - However if you want to attach a ref on a function component you do need to explicitly do something with the ref. like `useImperativeHandle(ref, ...);` _owner`
  - So the reason for special casing ref no longer exists in the Hooks world. 
  - Therefore I think the right call here is to stop special casing it at the element level and instead start special casing it only for classes.

- The plan is to eventually get rid of the need for `forwardRef` altogether by putting it back into `props` .
- Beware forwardRef affects reconciliation: element is always re-created on parent re-rendering.

- ### [value of using React.forwardRef vs custom ref prop](https://stackoverflow.com/questions/58578570/value-of-using-react-forwardref-vs-custom-ref-prop)
- ref常用别名：setRef, nodeRef, innerRef
- [forwardRef to FC](https://www.reddit.com/r/reactjs/comments/dfyclo/with_introduction_of_hooks_do_we_need_to_use/f39w4tv/?context=3)

``` JS
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));
// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;

// =====================================

const FancyButton = ({ innerRef }) => (
<button ref={innerRef} className="FancyButton">
    {props.children}
  </button>
));
const ref = React.createRef();
<FancyButton innerRef={ref}>Click me!</FancyButton>;
```

- If you use React 16.2 or lower, or if you need more flexibility than provided by ref forwarding, you can use this alternative approach and explicitly pass a ref as a differently named prop.
  - compatible with all React versions
  - passing refs as usual props does not cause breaking changes and is the way to go for multiple refs
  - works for class and function components
  - simplifies passing a ref to a nested component several layers deep
- The only advantages of forwardRef coming to my mind are
  - uniform access API for DOM nodes, functional and class components (you mentioned that)
  - ref attribute does not bloat your props API, e.g. if you provide types with TypeScript

 

- ### ref
- [RFC: createElement changes and surrounding deprecations](https://github.com/reactjs/rfcs/pull/107)
  - 大部分在讨论去掉defaultProps的决定，而未讨论去掉forwardRef的决定
- [Hook for forwardRef](https://github.com/facebook/react/issues/15306)
- [Potential performance issues with using forwardRef](https://github.com/facebook/react/issues/13456)
- [React hooks and functional component ref](https://stackoverflow.com/questions/58411779/react-hooks-and-functional-component-ref)
- [An alternative to ReactDOM.findDOMNode](https://github.com/reactjs/react-transition-group/issues/606)
  - ref object as a 2nd argument in render prop
  - [feat: add `nodeRef` alternative instead of internal `findDOMNode` ](https://github.com/reactjs/react-transition-group/pull/559)
