---
title: note-react-alternatives
tags: [alternatives, react]
created: '2020-11-09T13:08:17.281Z'
modified: '2020-11-09T13:10:09.581Z'
---

# note-react-alternatives

## guide

- ### [React vs Preact vs Inferno_202004](https://dev.to/tamb/react-vs-preact-vs-inferno-15go)
- Preact differs from React in a few ways:
  - There is no synthetic event system. 
    - React ships its own (very heavy) Synthetic Event system that offers a host of benefits but comes with a larger size and slower performance. 
    - Preact uses native `addEventListener` so it trusts/uses the DOMs API to a performance and size benefit.
  - Preact doesn't push JSX as it's client-side templating tool. 
    - In fact, the original author of Preact offers his package `htm` as an alternative. 
    - One of the benefits of this is difference is you can use regular old HTML attributes like class instead of className.
  - An added feature in Preact is that its `Component.render({props}, {state});` method signature has state and props as parameters, so you can access them easier within the JSX or htm.
- Pros:
  - Preact is a lot faster and lighter than React. And it aims to be "mostly" compatible with React.
  - To have near 100% compatibility Preact offers an additional package: `preact-compat`
  - Preact is compatible and even encourages using `htm` over JSX so you can unlock regular HTML attributes.
  - Preact is popular. This means that it's gonna have better support, a larger ecosystem and a quicker fixes.
  - It offers its own Server Side Rendering, routing, and other popular add-ons.
- Cons:
  - Hooks are in a separate preact package: `preact/hooks`. (Though some people may see this a pro)
  - Preact only has experimental support for `Lazy` and `Suspense` components.
  - Preact is kind of shoe-horned into a "React clone" category. 
    - A lot of development on the library will be to mimic React and not to innovate in its own way.
  - If you need a React component or package you have to use an additional library. 
    - preact/compat makes your project larger and slower but is the only way to bridge the gap between React-based npm packages and Preact.

- Inferno is different from React in the following ways:
  - It only offers a partial Synthetic Events system. 
    - So only certain events are synthesized. 
    - This is for performance reasons.
  - It is built explicitly for the DOM.
  - It has lifecycle methods on functional components
  - Inferno `setState` is synchronous by default and becomes async when chained (it will batch update for performance)
- Pros:
  - It's lightweight (but not as light as Preact)
  - It really is "insanely fast". 
    - Some of the demonstrations will actually blow you away 
    - and it even offer internal objects for optimization that will really crank up the speed.
  - It doesn't aim to mimic React entirely. 
    - In fact there are some difference (lifecycle methods on functional components) that truly set it apart from React
  - Inferno styles are set with regular old CSS property. 
    - There's no need to write the property as backgroundColor. You can use background-color.
  - It offers its own Server Side Rendering, routing, and other popular add-ons.
- Cons:
  - It has a MUCH smaller community. 
    - Support is slower and ecosystem is a lot smaller. 
    - Expect a longer wait time to get 3rd party libraries and components.
  - There is no `Lazy`, `Suspense`,    `Memo`, or Hooks support. 
    - At the time of writing these features are being considered, but my money is on library remaining small.
  - Since `setState` is synchronous you will experience differences from React. There's no real way around this.
  - If you need a React component or package you have to use an additional library. 
    - inferno/compat makes your project larger and slower but is the only way to bridge the gap between React-based npm packages and Inferno.

- Conclusion
  - The real benefit of React is how easily it can port to React Native and its support. 
  - In terms of performance, only really really heavy DOM manipulation will reveal the gains of Inferno or Preact over React.
  - This last point is spicy: I don't like hooks. 
    - I find them to be a little sloppy(凌乱的) and to introduce less uniform standards. 
    - For this reason I really like Inferno's support for lifecycle methods on functional components.
  - In the end, React is still the top dog. 
    - But Preact is pretty close behind. 
    - The added benefit a larger Preact ecosystem and community makes me prefer Preact over Inferno.  

## pieces
