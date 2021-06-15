---
title: page-ui-comp-react-design
tags: [blog, components, react]
created: '1970-01-01T00:00:00.000Z'
modified: '2021-01-19T10:51:34.462Z'
---

# page-ui-comp-react-design

# [Don't overabstract your components](https://kirjai.com/component-abstraction/)
- At some point you are tasked with adding a new component. 
  - That is first step in a process known as component API design.

- Component as a layer of abstraction
- When you are creating a new component - you are, generally, aiming to abstract something away. 
- Whatever you are abstracting ends up being the component's functionality. What it does and the reason why it exists.
- As with any abstraction - you are trying to strike a balance. 
  - A balance between providing some functionality, and the ability to configure said functionality. 
  - That balance is also the reason why you want to keep your abstractions as small as possible. 
- The more functionality you are trying to fit into a single layer of abstraction - the more functionality you might have to make configurable. 
  - Something that becomes harder to do the more functionality the abstraction has.

- Children prop
  - In my opinion, the `children` prop is underutilized in a lot of React components.
- Basic select implementation
- Composable select implementation
- Shifting responsibility
  - some responsibility has been shifted to the consumer. 
  - Generally, that is a good thing, but only to an extent. 
  - What you want to avoid is having an incomplete abstraction - leaving it up to the consumer to "finish".

- Communication between components
  - One of the ways is using the React Context API.

- Trade-offs
  - More opportunity for misconfiguration
  - Results in more typing
  - Lack of type safety

- Conclusion
- My advice is to approach component API design from the perspective of the consumer first. 
  - Using that as a starting point for iterating over the API. 
  - Having said that, the first API design that comes to your mind might not be the right one. 
  - How do you know? Take inspiration from existing component libraries, like Reach UI, Material UI, React Bootstrap, Ant Design to name a few.
  - There is a lot of overlap in problems a lot of us are solving, after all.

- Finally, if I find myself rendering components and elements from a configuration object - I take a step back. 
  - I re-evaluate whether the problem I am solving could be solved in a more composable and open way.
# [Writing Type-Safe Polymorphic React Components (Without Crashing TypeScript)_201908](https://blog.andrewbran.ch/polymorphic-react-components/)
- When designing a React component for reusability, you often need to be able to pass different DOM attributes to the component’s container in different situations.
- Let’s say you’re building a `<Button />`. 
  - At first, you just need to allow a custom `className` to be merged in, 
  - but later, you need to support a wide range of attributes and event handlers that aren’t related to the component itself, 
  - but rather the context in which it’s used
    - say, `aria-describedby` when composed with a `Tooltip` component, 
    - or `tabIndex` and `onKeyDown` when contained in a component that manages focus with arrow keys.
- It’s impossible for Button to predict and to handle every special context where it might be used, 
  - so there’s a reasonable argument for allowing arbitrary extra props to be passed to Button, 
  - and letting it pass extra ones it doesn’t understand through.

```typescript
interface ButtonProps extends React.ButtonHTMLAttributes < HTMLButtonElement > {
  color ? : ColorName;
  icon ? : IconName;
}

function Button({ color, icon, className, children, ...props }: ButtonProps) {
  return (
    <button
      {...props}
      className={getClassName(color, className)}
    >
      <FlexContainer>
        {icon && <Icon name={icon} />}
        <div>{children}</div>
      </FlexContainer>
    </button>
  );
}
```

- The Button component you made only renders as an `HTMLButtonElement`.
  - how do we use Button as a react-router Link?
  - If we weren’t concerned about type safety, we could write this pretty easily in plain JavaScript
  - But, how do we type this correctly?
- `ref` isn’t the only problem; it’s just the first problem. The rest of the problems are every event handler prop
- **An alternative approach**
- let’s refresh on what we’re actually trying to accomplish. 
- Our Button component should:
  - be able to accept arbitrary props like onKeyDown and aria-describedby
  - be able to render as a button, an a with an href prop, or a Link with a to prop
  - ensure that the root element has all the props it requires, and none that it doesn’t support
  - not crash TypeScript or bring your favorite code editor to a screeching halt
- It turns out that we can accomplish all of these with a render prop. 
- There’s a small cost to an API design like this.
  - On one hand, this provides the ultimate degree of customizability
  - But on the other hand, you probably wanted to merge those classes 99% of the time
