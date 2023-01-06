---
title: page-ui-comp-design
tags: [components, ui]
created: 2020-09-28T16:28:19.740Z
modified: 2021-01-19T10:51:22.355Z
---

# page-ui-comp-design

# [Headless User Interface Components](https://www.merrickchristensen.com/articles/headless-user-interface-components/)

- A headless user interface component is a component that offers maximum visual flexibility by providing no interface.
- Headless user interface components separate the logic & behavior of a component from its visual representation. 
- This pattern works great when the logic of a component is sufficiently complex and decoupled from its visual representation. 
- This headless component happens to be implemented as a render prop, yes! It could just as well be implemented as a higher order component. 
- It could have even been implemented as a View and a Controller. Or a ViewModel and a View. 
- The point here is about separating the "mechanism" of flipping coins and the "interface" to that mechanism.
- Rule of Separation: Separate policy from mechanism; separate interfaces from engines. 
- How long will this component live for? Is it worth deliberately preserving the mechanism aside from the interface? Perhaps to use this mechanism in another project with a different look and feel?
- How frequently is our interface bound to change? Will the same mechanism have multiple interfaces?
- There is an indirection cost paid when you separate "mechanism" and "policy". 
- You need to be sure that the benefits of separation merit the expense of indirection. 

- For a truly exemplar non-trivial headless component, check out a project downshift. In fact, it is downshift that ultimately inspired this post
- In a world where design systems and user interface libraries are headless, your interfaces can have a high-end custom feel and the durability & accessibility of a great open source library. 
- You spend your time implementing the only part that you needed to, the part that is truly unique, the look and feel specific to your application.

# [The Sexiness of Headless UI Components_2019](https://www.joshbritz.co/posts/the-sexiness-of-headless-ui/)

- One of the things I’ve noticed about components is that we developers have a natural tendency of just make them work in the given immediate use case or context. 
- So often we incorporate business logic, layout logic, and other specifics as part of the component’s makeup. 
- Many components are just abstracted into a separate project from where they are being used, but take no advantage of the benefits provided by doing that. 
- One of the biggest reasons for this, in my opinion, is that components are way too tied to the design iteration they represent. They are made to cater for the designs that can be found at the time of them being made, but have no mindfulness of future enhancements.

- Headless UI Components are Components that provide a set of functionalites for a feature without explicitly determining its UI aspect.

``` JS
// not a Headless Component
const Counter: FC = () => {
  const [count, setCount] = useState(0);

  return (
    <div className="counter-wrapper">
       <button onClick={() => setCount(count - 1)}>-</button>
       <span>{count}</span>
       <button onClick={() => setCount(count + 1)}>+</button>
     </div>
  );
}
```

- However, as you can see, each change we want to make to the component’s UI has to be pre-planned and built into the component. It also gets messier with each new state or option you add.
- So what if I want the functionality of the counter (its state, and ability to increment and decrement), but not the UI that is given. 
- In most cases, the solution is to just build a new component that works in the same way as an exsisting component, but render a different UI or, to add another config to the component’s props that switches between the two UIs.
- There is another way. Enter Headless UI Components. Hopefully at this point you can see a use case for a component that provides the functionality you need without caring about it’s UI. 

``` typescript
// Headless Component
interface Arguments {
  count: number;
  increment: (value: number) => void;
  decrement: (value: number) => void;
}

const Counter = (props: { children: (args: Arguments) => JSX.Element }) => {
  const [count, setCount] = useState(0);

  if (!props.children || typeof props.children !== 'function') return null;

  return props.children({
    count,
    increment: (value: number = 1) => setCount(value),
    decrement: (value: number = 1) => setCount(value),
  });
};

<CounterHeadless>
  {({ count, increment, decrement }: any) => {
    return (
      <div className="counter-wrapper">
        <button onClick={() => decrement(count - 1)}>less</button>
        <span>{count}</span>
        <button onClick={() => increment(count + 1)}>more</button>
      </div>
    );
  }}
</CounterHeadless>

<CounterHeadless>
  {({ count, increment }: any) => {
    return (
      <div className="counter-wrapper">
        <h2>{count}</h2>
        <button onClick={() => increment(count + 1)}>+</button>
      </div>
    );
  }}
</CounterHeadless>
```

- With Headless Components, you can easily package common utilities for various components and ship them without even having to think about how much padding this button must have, etc.
- A common use case for components is to have pre-styled and tested design elements that can be dropped into a page without having to worry about their styling. 
- The problem is, headless components don’t let you do that
- Just because you make use of headless components doesn’t mean that you should never build components that have UI. 
- In fact headless components can make this process even easier. 
  - If we take the example of the counter above, we can see that we have created a few different variations of that counter. 
  - Using the headless counter component we built, we can make each of these counters into their own component without having to duplicate functionality accross components.
  - Three components for the price of one. 
  - You can use each one of the above counters as preset components in your app or, 
  - if you need to, you can just use the headless base version and create your own variation.

# ref

- [The Vanilla Javascript Component Pattern](https://dev.to/megazear7/the-vanilla-javascript-component-pattern-37la)
  - https://dev.to/frankdspeed/the-html-component-pattern-hcp-3pkp
- [Moving from Vanilla JavaScript to a Reusable Vue Component](https://css-tricks.com/moving-from-vanilla-javascript-to-a-reusable-vue-component/)
- [React vs. Plain JavaScript](https://www.framer.com/blog/posts/react-vs-vanilla-js/)
- [Wrap a Vanilla JavaScript Package for Use in React](https://www.digitalocean.com/community/tutorials/wrap-a-vanilla-javascript-package-for-use-in-react)
