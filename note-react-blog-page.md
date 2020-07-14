---
title: note-react-blog-page
tags: [blog, dev, react]
created: '2020-06-29T08:43:56.344Z'
modified: '2020-07-14T11:51:59.253Z'
---

# note-react-blog-page

## When to useMemo and useCallback

- ref
  - [When to useMemo and useCallback](https://kentcdodds.com/blog/usememo-and-usecallback)
  - [【译】什么时候使用useMemo和useCallback](https://jancat.github.io/post/2019/translation-usememo-and-usecallback/)
  - [React, Inline Functions, and Performance](https://reacttraining.com/blog/react-inline-functions-and-performance/)
- The point is this:
  - Performance optimizations are not free. 
  - They ALWAYS come with a cost but do NOT always come with a benefit to offset that cost.
  - Therefore, optimize responsibly.
- So when should I useMemo and useCallback?
- There are specific reasons both of these hooks are built into React:
  - Referential equality
  - Computationally expensive calculations

``` JS
function Foo({ bar, baz }) {
  const options = { bar, baz }
  React.useEffect(() => {
    buzz(options)
  }, [options]) // we want this to re-run if bar or baz change
  return <div>foobar</div>
}

function Blub() {
  return <Foo bar="bar value" baz={3} />
}
```

- The reason this is problematic is because `useEffect` is going to do a referential equality check on options between every render, 
  - and thanks to the way JavaScript works, `options` will be new every time 
  - so when React tests, whether `options` changed between renders, it'll always evaluate to `true` , 
  - meaning the `useEffect` callback will be called after every render rather than only when `bar` and `baz` change.

``` JS
function Foo({ bar, baz }) {
  React.useEffect(() => {
    const options = { bar, baz }
    buzz(options)
  }, [bar, baz]) // we want this to re-run if bar or baz change
  return <div>foobar</div>
}
```

- But there's one situation when this isn't a practical solution: If `bar` or `baz` are (non-primitive) objects/arrays/functions/etc

``` JS
function Foo({ bar, baz }) {
  React.useEffect(() => {
    const options = { bar, baz }
    buzz(options)
  }, [bar, baz])
  return <div>foobar</div>
}

function Blub() {
  const bar = React.useCallback(() => {}, [])
  const baz = React.useMemo(() => [1, 2, 3], [])
  return <Foo bar={bar} baz={baz} />
}
```

- This is precisely the reason why `useCallback` and `useMemo` exist. So here's how you'd fix that (all together now)
- Note that this same thing applies for the dependencies array passed to `useEffect` , `useLayoutEffect` , `useCallback` , and `useMemo` .

``` typescript
function CountButton({onClick, count}) {
  return <button onClick={onClick}>{count}</button>
}

function DualCounter() {
  const [count1, setCount1] = React.useState(0)
  const increment1 = () => setCount1(c => c + 1)
  const [count2, setCount2] = React.useState(0)
  const increment2 = () => setCount2(c => c + 1)
  return (
    <>
      <CountButton count={count1} onClick={increment1} />
      <CountButton count={count2} onClick={increment2} />
    </>
  )
}
```

- Every time you click on either of those buttons, the `DualCounter` 's state changes and therefore re-renders which in turn will re-render both of the CountButtons.
  - However, the only one that actually needs to re-render is the one that was clicked right? 
  - So if you click the first one, the second one gets re-rendered, but nothing changes.
  - We call this an "unnecessary re-render."
- MOST OF THE TIME YOU SHOULD NOT BOTHER OPTIMIZING UNNECESSARY RERENDERS. 
  - React is VERY fast 
  - and there are so many things I can think of for you to do with your time that would be better than optimizing things like this. 
- However, there are situations when rendering can take a substantial amount of time (think highly interactive Graphs/Charts/Animations/etc.).

``` typescript
const CountButton = React.memo(function CountButton({onClick, count}) {
  return <button onClick={onClick}>{count}</button>
})

function DualCounter() {
  const [count1, setCount1] = React.useState(0)
  const increment1 = React.useCallback(() => setCount1(c => c + 1), [])
  const [count2, setCount2] = React.useState(0)
  const increment2 = React.useCallback(() => setCount2(c => c + 1), [])
  return (
    <>
      <CountButton count={count1} onClick={increment1} />
      <CountButton count={count2} onClick={increment2} />
    </>
  )
}
```

- Now we can avoid the so-called "unnecessary re-renders" of CountButton.
  - I would like to re-iterate that I strongly advise against using React.memo (or it's friends PureComponent and shouldComponentUpdate) without measuring 
  - because those optimizations come with a cost 
  - and you need to make sure you know what that cost will be as well as the associated benefit 
  - so you can determine whether it will actually be helpful (and not harmful) in your case, 
  - and as we observe above it can be tricky to get right all the time so you may not be reaping any benefits at all anyway.
- This is the other reason that `useMemo` is a built-in hook for React (note that this one does not apply to `useCallback` ).
  - React stores previous values given the inputs and will return the previous value given the same previous inputs. 
  - That's memoization at work.
  - This is useful for computationally expensive calculations
- I'd just like to wrap this up by saying that every abstraction (and performance optimization) comes at a cost. 
- Apply the AHA Programming principle and wait until the abstraction/optimization is screaming at you before applying it and you'll save yourself from incurring the costs without reaping the benefit.
- Specifically the cost for `useCallback` and `useMemo` are that you make the code more complex for your co-workers, 
  - you could make a mistake in the dependencies array, and you're potentially making performance worse by invoking the built-in hooks and preventing dependencies and memoized values from being garbage collected. 
  - Those are all fine costs to incur if you get the performance benefits necessary, but it's best to measure first.

``` JS
class FavoriteNumbers extends React.Component {
  render() {
    return (
      <ul>
        {this.props.favoriteNumbers.map(number => (
          // TADA! 
          // This is a function defined in the render method!
          // Hooks did not introduce this concept.
          // We've been doing this all along.
          <li key={number}>{number}</li>
        ))}
      </ul>
    )
  }
}
```

## You Probably Don't Need Derived State

- ref
  - https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
  - [你可能不需要Derived State](https://zhuanlan.zhihu.com/p/38090110)

- To recap, when designing a component, it is important to decide whether its data will be controlled or uncontrolled.
  - The terms “controlled” and “uncontrolled” usually refer to form inputs, but they can also describe where any component’s data lives. 
  - Data passed in as props can be thought of as **controlled** (because the parent component controls that data). 
  - Data that exists only in internal state can be thought of as **uncontrolled** (because the parent can’t directly change it).
  - Instead of trying to “mirror” a prop value in state, make the component controlled, and consolidate the two diverging values in the state of some parent component. This makes the data flow more explicit and predictable.
  - For uncontrolled components, if you’re trying to reset state when a particular prop (usually an ID) changes, you have a few options:
    - Recommendation: To reset all internal state, use the `key` attribute.
    - Alternative 1: Reset uncontrolled component with an ID prop
      - To reset only certain state fields, watch for changes in a special property (e.g. props.userID).
    - Alternative 2: Reset uncontrolled component with an instance method
      - consider fall back to an imperative instance method using refs.
- bugs
  - If our component’s parent rerenders, anything we’ve typed into the `<input>` will be lost!
  - In practice, components usually accept multiple props; 
    - another prop changing would still cause a rerender and improper reset. 
    - Function and object props are also often created inline, making it hard to implement a shouldComponentUpdate that reliably returns true only when a material change has happened.
    - As a result, shouldComponentUpdate is best used as a performance optimization, not to ensure correctness of derived state
    - It is a bad idea to unconditionally copy props to state.
    - When navigating between details for two accounts with the same email, the input would fail to reset. This is because the prop value passed to the component would be the same for both accounts! 
- When a `key` prop changes, React will create a new component instance rather than update the current one.
  - Keys are usually used for dynamic lists but are also useful here. 
  - Sometimes it might make more sense to put a key on the whole form instead. Every time the key changes, all components within the form will be recreated with a freshly initialized state.
  - While this may sound slow, the performance difference is usually insignificant. Using a key can even be faster if the components have heavy logic that runs on updates since diffing gets bypassed for that subtree.

## react component vs element vs instance

- ref
  - [React Components, Elements, and Instances](https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html)
- An element is a plain object describing a component instance or DOM node and its desired properties. 
  - It contains only information about the component type (for example, a Button), its properties (for example, its color), and any child elements inside it.
  - It is a way to tell React what you want to see on the screen. 
  - You can’t call any methods on the element.
  - It’s just an immutable description object with two fields: `type: (string | ReactClass)` and `props: Object`
  - An element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components.
  - Elements can contain other elements in their props. 
  - Creating a React element is cheap. 
  - Once an element is created, it is never mutated.
- A React component takes props as an input, and returns an element tree as the output.
  - A component can be declared in several different ways. class/func
  - props flows one way in React: from parents to children.
- An instance is what you refer to as `this` in the component class you write. 
  - It is useful for storing local state and reacting to the lifecycle events.
  - Only components declared as classes have instances, and you never create them directly: React does that for you
  - While mechanisms for a parent component instance to access a child component instance exist, they are only used for imperative actions (such as setting focus on a field), and should generally be avoided.
  - React takes care of creating an instance for every class component, so you can write components in an object-oriented way with methods and local state, but other than that, instances are not very important in the React’s programming model and are managed by React itself.
  - Function components don’t have instances at all.

## A Complete Guide to useEffect

- ref
  - [A Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
- Question: How do I replicate `componentDidMount` with `useEffect` ?
- Question: How do I correctly fetch data inside `useEffect` ? What is `[]` ?
- Question: Do I need to specify functions as effect dependencies or not?
- Question: Why do I sometimes get an infinite refetching loop?
- Question: Why do I sometimes get an old state or prop value inside my effect?
- Each Render Has Its Own Props and State
- Each Render Has Its Own Event Handlers
- Each Render Has Its Own Effects
- Each Render Has Its Own… Everything
  - We know now that effects run after every render, are conceptually a part of the component output, and “see” the props and state from that particular render.
  - Closures are great when the values you close over never change. That makes them easy to think about because you’re essentially referring to constants.
  - And as we discussed, props and state never change within a particular render.
