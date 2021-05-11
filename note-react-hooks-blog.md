---
title: note-react-hooks-blog
tags: [blog, hooks, react]
created: '2020-12-29T14:16:59.370Z'
modified: '2020-12-29T14:18:03.808Z'
---

# note-react-hooks-blog

# guide

# [DejaVu: Caching versus Memoization](https://dev.to/thekashey/dejavu-caching-versus-memoization-298n)

- Devs had a great conversation about the future concurrent rendering
- The main problem was “tearing” - different time slices coexistence in one render(output). 
  - Some component might see the New State, while others might still see the Old. 
  - You, as a User, will see both.
- There was no such thing as the "past" with Class based components - there was the only one `this`, and nothing else. And `this` always represents the "present".
- With hooks, well...
  - When you are do onClick - it sees variables from the local -functional scope. From the "past" scope - only refs represents the present.
  - When you are declare effect there is no "past" - only the present. As a result, you don't know when some effect might trigger. "Past" and "Present" dependencies would be compared inside React.
  - When you are run effect - it's already one time tick in the past. Something might have already been changed, but not for effect - it is frozen in time.
  - When you are running multiple effects - they might affect each other, causing cascade and repetitive updates. Until they all are not finished - there is no past and there is no present - it's mixed, as long as every hook works by its own.
- In RxJS world it's called glitches - temporary inconsistencies emitted by Observables - and they are not considered as a problem.
  - Glitches in React are also more about features than bugs. 
  - However, they are at least a big performance problem.
- As a conclusion
  1. useState state is derived from props, only during the first render
  - useMemo other values are derived from state and props
  - useEffect some variations of props and state are reflected back to the state.
  - ANY useEffect might cause glitches.
  1. React is a subject for glitches
  2. Use Class Components to handle complex state situations.
  3. Use external state (like Redux)
  4. Be aware of the problem
  5. And it might be not a problem at all.
- state management is, and always will be a very complicated beast

# [Conditional React Hooks](https://www.benmvp.com/blog/conditional-react-hooks/)

- Hooks enable us to use state and other React features without writing a class. 
- We can’t call Hooks inside of conditionals, loops, or nested functions 
  - in order to ensure that Hooks are called in the same order each time a component renders. 
  - The order is important for how React associates Hook calls with components. 
  - So if we conditionally render a hook, for instance, the order of the Hooks could change between renders of a component, completely messing up the Hooks system.
- How to conditionally call a React Hook while still calling Hooks at the top level？

``` JS
// use useClickAway Hook to hide an overlay when the user clicks outside of its container.
const Overlay = ({ show, children, onClose }) => {
  // not render if not shown
  if (!show) {
    return null
  }
  // early return is a sneaky conditional. 
  // breaking the rules of hooks!
  const rootRef = useRef(null)
  useClickAway(rootRef, () => {
    console.log('clicked outside')
    onClose()
  })
  return (
    <div ref={rootRef}>
      {children}
      <CloseButton onClick={onClose} />
    </div>
  )
}
```

- **Call but ignore**
- With this workaround, we always call the Hook, but we do nothing with it.

``` JS
const Overlay = ({ show, children, onClose }) => {
  const rootRef = useRef(null)
  // `useClickAway` from react-use is always called, 
  // but we only use the callback when `show` is `true`
  useClickAway(rootRef, () => {
    if (show) {
      console.log('clicked outside')
      onClose()
    }
  })
  // early return moves to after Hook calls
  if (!show) {
    return null
  }
  return (
    <div ref={rootRef}>
      {children}
      <CloseButton onClick={onClose} />
    </div>
  )
}
```

- This works, and is usually the simplest approach, but it **can be wasteful**. 
  - Creating a bunch of refs with `useRef` is likely not that big of a deal, but calling `useClickAway` unnecessarily is more so. 
  - The implementation of `useClickAway` adds `mousedown` and `touchstart` events to the `document`, which now are getting added whether or not the `Overlay` is being shown.
- The “call but ignore” approach **doesn’t always work** either. 

``` JS
const Example = ({ team }) => {
  // we do not want it to set the page title when the value is null or undefined
  if (team.name !== null && team.name !== undefined) {
    useTitle(team.name)
  }
  return (
    <section>
      <h1>{team.name}</h1>
      { ... }
    </section>
  )
}
```

- there’s no clear way to use the “call but ignore” approach, because there’s nothing to ignore. 
  - We’d have to implement our own `useTitle` Hook in order to get it to ignore null and undefined values.
- **Renderless component wrapper**
- When the “call but ignore” workaround doesn’t work, we can use the “renderless” component wrapper workaround.
- We wrap our Hook with a component interface and then conditionally render the component. 
  - This requires more work, but on the flip side it always should work.

``` JS
// wrap your hook in a renderless component
const ClickAway = ({ ref, onClickAway }) => {
  useClickAway(ref, onClickAway)
  return null
}
const Overlay = ({ show, children, onClose }) => {
  const rootRef = useRef(null)
  if (!show) {
    return null
  }
  return (
    <div ref={rootRef}>
      <ClickAway
        ref={rootRef}
        onClickAway={() => {
          console.log('clicked outside')
          onClose()
        }}
      />
      {children}
      <CloseButton onClick={onClose} />
    </div>
  )
}
```

- Now, instead of trying to conditionally call the `useClickAway` Hook, we’re conditionally rendering the `<ClickAway>` component, and there is no rule against that. 
  - since `ClickAway` is being conditionally rendered within `Overlay`,  `useClickAway` is indirectly conditionally called!
  - `ClickAway` component’s props match the arguments that the `useClickAway` Hook accepts.

``` JS
const PageTitle = ({ title }) => {
  useTitle(title)
  return null
}
const Example = ({ team }) => {
  return (
    <section>
      {team.name && <PageTitle title={team.name} />}
      <h1>{team.name}</h1>
      { ... }
    </section>
  )
}
```

- Both the `useClickAway` and `useTitle` Hooks don’t return any data so their “renderless” component wrappers have rather simple interfaces. 
  - However, if you have a Hook that returns data AND you still want to conditionally render it, your component wrapper will still be “renderless, ” but in a slightly different way.
  - to display a “back to top” button if the user has scrolled down the page enough

``` JS
const WindowScroll = ({ children }) => {
  const { x, y } = useWindowScroll()
  return <>{children({ x, y })}</>
}
const Page = ({ showBackToTop }) => {
  return (
    <div>
      {showBackToTop && (
        <WindowScroll>
          {(pos) => {
            const shouldShow = pos.y > 250
            return (
              <button className={shouldShow ? 'sticky' : 'hidden'}>
                Back to top
              </button>
            )
          }}
        </WindowScroll>
      )}
      <main>
        {...}
      </main>
    </div>
)
}
```

- If the Hook you wanna conditionally render returns data, your component wrapper needs a render prop
- Instead of returning `null` to be “renderless”, it renders the UI returned by the children render prop. 
  - In this example, that UI is the “back to top” button. 
  - But the entire `<WindowScroll>` component is conditionally rendered based on the `showBackToTop` prop. 
- discussion
- I think you can use a `useEffect` to conditionally call them without breaking the rules
  - The easiest way around this is to put the conditional in the `useEffect` . 
  - For custom hooks that’d be mean passing a bool argument like `useTitle(myTitle, shouldChangeTitle)`

  - This also helps to wrap the arguments logics within the hook, so render fn doesn't need to do argument validations. 

    - Hooks will run every time, but what they do depends on the arguments.

- Why not just pass an extra argument to hook to tell the hook to not do anything when it runs?
- Hooks can be called or used conditionally mostly by passing a method as 2nd argument. 
  - For example `useMyHook("value", ()=>{doSomethingWithValue})`

  - this way you don't have to directly hack through "rendering".
