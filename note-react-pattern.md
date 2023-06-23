---
title: note-react-pattern
tags: [pattern, react]
created: 2021-05-11T14:35:46.252Z
modified: 2021-05-11T14:36:13.256Z
---

# note-react-pattern

# guide

- resources
  - [Hooks Pattern](https://www.patterns.dev/posts/hooks-pattern)
  - [JavaScript Patterns Workshop | JavaScript Patterns](https://javascriptpatterns.vercel.app/patterns)
# conditional rendering: switch-case vs map
- [Which is the react way of complex conditional rendering?](https://stackoverflow.com/questions/50901604)
  - 👍 `{ this.state.err ? <Err /> : <Main /> }` 数据驱动视图
  - 👎 `<div className="App"> {this.state.comp} </div>` state中不要存comp
    - `<div className="App"> {comp} </div>` 将comp提取成变量更好
- 不要直接写组件，可以先定义一个组件变量

- [React conditional rendering: 9 methods with examples - LogRocket Blog](https://blog.logrocket.com/react-conditional-rendering-9-methods/)

## [Conditionally render react components in cleaner way](https://dev.to/hey_yogini/conditionally-render-react-components-in-cleaner-way-1ik5)

- 提出了 enum 和 switch-case 2种方法并讨论，可以是Component或ReactElement(自带实参props)

- enum-pros
  - 简单直观，直接从预定义对象中取组件
  - {roleSettings(username)[userRole]} 所有子组件都有username参数
  - {createElement(RoleSettings[userRole], { username })}

- enum-cons
  - ~~对每个组件不方便传入定制参数~~
  - A downside of enum solution is all the component will be compiled even it doesn't need to rendered，但可解决

- switch-case-pros
  - 选择组件自身也是一个组件，all in react
  - memo后方便优化性能
  - 扩展case方便

- switch-case-cons
  - The long term cost of the switch/case in this scenario is higher. 
  - When you're wrapping different components inside a single component, is better to share props across them because they will be used in the same places, so ideally they should receive the same props

## [Use Dynamic Property Maps over Switch Case Statements | Sean C Davis](https://www.seancdavis.com/posts/use-dynamic-property-maps-over-switch-case-statements/)

- 还可以考虑typescript的支持
- 考虑定制逻辑的粒度，函数可以方便设置默认值参数、方法，map需要额外封装

- Don’t Use If Statements
  - It doesn’t scale. Once you add support for a third theme, it starts to become unwieldy(笨拙的；不灵巧的).
  - Often these scenarios will require more logic than a simple string to return. It can become easy to get lost in which part of the if statement you’re in when the logic gets longer (though there are ways of avoiding that).

- Don’t Use Switch Case Statements
  - I do not like switch-case statements. I’ve rarely found a good use for them. 
  - You can already see that it’s messier than the if statement. It doesn’t really scale much better than the if statement either.

- Try Dynamic Property Maps
  - My favorite pattern to use in these scenarios is a dynamic property map. 
  - It works by defining a property and using square brackets to get/set
  - It scales perfectly. Need to support a new mapping? Just add a new key-value pair.
  - No need for a function. Everything is defined statically and accessed directly

- I just go to the map every time. My code is consistent 

- Accounting for Default Values
  - Because this isn’t a function and just an object, we have to define default values differently.
  - `buttonClassMap[theme || "dark"];`

- Accounting For Bad Values
  - `buttonClassMap[Object.keys(buttonClassMap).includes(theme) ? theme : "dark"];`

- Using with Functions/Logic
  - You’re not limited to return simple values here, either. You could even return a function.

```JS
const funcMap = {
  a: (arg) => console.log(arg),
  b: (arg) => console.log(arg),
};

funcMap["a"]("HELLO!"); // Logs "Hello!" to the console
```

## [Use an object instead of a switch - DEV Community](https://dev.to/ubmit/use-an-object-instead-of-a-switch-1e55)

- tl; dr: whenever we notice that the switch is doing nothing more than mapping keys to values, we should use an object instead
  - the usage of an object makes this code less complex and also more readable, since it's less verbose than the switch statement

- use `keyof typeof` keywords to pull the object keys directly from the object, so you don't need to explicitly define the keys

- Even if it isn’t just mapping, you can also use methods in object to perform more logic per case.
  - This method has way more uses than mapping keys to values tho. 
  - We could make the object keys functions for infinite possibilities (if it is needed)

- I think I tend to see your use-cases here, but apperately this might have been a bad choice for replacing it with a map methodology.
  - Switch-Case are generally understood even by all kind of software engineers (while loose object referencing is not that common in many languages)
  - the switch could be refactored to make it less complex

- A switch statement is more performant. Are you sure about that?
  - SpiderMonkey (FireFox) seems to be consistently favouring object property lookup (not surprising as that is a core mechanism in JavaScript that needs to be performant).
  - However somewhere around size > 1000 things get less predictable with V8 (Chromium). Perhaps putting getObjectSwitch on the hot code path may give it the full Turbofan treatment at some point in time.

## [Replace Conditional With Map Refactoring](https://blog.rstankov.com/replace-conditional-with-map-refactoring/)

- This is one of my favorite refactorings. It helps to group logic, making code easier to read and extend.

- replace if-else/switch-case with map
- for redux, I always prefer to use a utility like redux-create-reducer, to remove the noise from here and handle things like default case.

## [Simplifying Code with Maps In JavaScript and React | ClarityDev blog](https://claritydev.net/blog/simplifying-code-with-maps-in-javascript)

- Using a `Map` in this scenario is more advantageous than using an `Object`, as it simplifies the code, maintains the **order** of the tabs, and allows us to leverage the direct iteration and other benefits that Map provides.

## [React Conditional Rendering With Type Safety and Exhaustive Checking - Lloyd Atkinson](https://www.lloydatkinson.net/posts/2022/react-conditional-rendering-with-type-safety-and-exhaustive-checking/)

- While switch in the context of React is an improvement, unfortunately, a switch statement is not exhaustive like pattern matching in a functional language. 
  - This means it’s easy to forget to update a switch.
  - This pattern isn’t specific to just React. I considered demonstrating the pattern for multiple frameworks including Vue but decided against it.

- There is an alternative approach that leads to more readable code while also adding extra type safety.

- To begin with, I created a union type that contains all possible states
  - The union isn’t an absolute necessity for this general pattern, but it’s how I can enforce type-safety and exhaustive pattern matching.
  - The best approach for a type-safe object is the `Record` utility type.
- The next step is to apply the same pattern to the conditional rendering of elements or components. 
- TypeScript will ensure all states are included, and the correct type is returned. The pattern significantly improves code readability and maintainability.
- A traditional `switch` will not tell you if you’ve forgotten to include a state, but this pattern will.

```typescript

type MovieType = 'love'|'action';

const LoveComp = ()=><h1>love</h1>;
const ActionComp = ()=><h1>action</h1>;

const ConditionalMovie = ({type})=>{
  
  const icon:Record<MovieType, ReactNode>={
    love: <LoveComp />,
    action: <ActionComp />,
  }
  
  return (
    <div>
    {icon[type]}
    </div>
  )
  
}
```

# hooks factory

## [React Hooks Factories - DEV Community](https://dev.to/pietmichal/react-hooks-factories-48bi)

- It will be a custom hook wrapping useState but it will set a default value provided at the time of creation.
- Sharing state across hooks to create context without Context API
  - this hook provides a shared state without having to wrap an app with a Context Provider.

- I love this technique, but how did you handle the **race condition** that can occur when using the useSharedState hook? 
  - useEffect is asynchronous, so when the component is first mounted there is a moment of time between when useState is called and when the component registers itself to listen for changes in useEffect. 
  - During this moment of time, another component could change the state value, but the new component would be unaware because it is still waiting to register.
  - I ask because I have implemented a factory very similar to the approach you have described and am currently running into this issue.
  - I could setState from within useEffect (with a useRef to avoid infinite looping); however, that seems a bit hacky. Thoughts?
- It sounds to me that your abstraction breaks the single responsibility principle. Maybe your hook also has to include the asynchronous logic so it can flag that it is loading and prevent child components from setting the state?
# [React wrapper hell was a mistake](https://twitter.com/aralroca/status/1644068034716356628)
- but why is this bad ?i mean it is so easy to compose this way

- Thanks that React use JSX this children hell is possible to fix with JS
  - Function composition in XML Syntax.
  - do not mistake your lack of experience for an issue with React

```jsx
const nestChild = (Child, Parent) => <Parent> <Child /></Parent>;

const ComposedComp = [Provider1, Provider2].reduce(nestChild, App)

// <Provider2>
//   <Provider1>
//     <App />
//   </Provider1>
// </Provider2>

```

- [Avoiding deep nested tree of React Context Providers](https://alexkorep.com/react/react-many-context-providers-tree/)
  - I have released an NPM package for that: react-array-to-tree

```JSX
const buildProviderTree = (providers) => {
  if (providers.length === 1) {
    return providers[0];
  }
  const A = providers.shift();
  const B = providers.shift();
  return buildProviderTree([
    ({ children }) => (
      <A>
        <B>
          {children}
        </B>
      </A>
    ),
    ...providers,
  ]);
};

const Providers = buildProviderTree([
  ThemeContext.Provider,
  UserContext.Provider,
  SomeOtherContext.Provider,
  YetAnotherContext.Provider,
  OneMoreContext.Provider,
  AndSoForthContext.Provider,
]);

const AppWithProviders = () => (
  <Providers>
    <App/>
  </Providers>
);

```

- [Simple example to create global providers easily in the application](https://gist.github.com/nicolasmelo1/82e00970c1dce080bda349e3f0697152#file-globals-tsx)
  - 思路与上面类似

- I don't think the complexity here is React, Vue looks like pretty much the same im my own experience
  - If your Vue code looks like this, you are doing something terribly wrong. Abstract controllers (not "Controller") should be handled at the router level via guards. You could arguably make this spaghetti code with other frameworks as well, so your point is useless
  - You can use a global state management library like Pinia 

- That's why imo angular got it right with services and directives

- This seems more like a problem with leaning on the provider pattern (one manifestation of which is React Context) to manage state. There are better patterns for this stuff out there.

- Don't blame the library/framework for the developer mistakes
  - or the developer was a mistake?

- In the past, these would have been spaghetti code in invisible globals. 
  - Now, you're just seeing a lot of them in a visible and maintainable hierarchy.

- They are differences between react and vue, the image show us how react inject global properties and functionalities using providers components at the root, with vue just can use provide/inject.

- JSX was the mistake. Gets people thinking in markup and not like the functions these things are. You don't need to nest them at all! They can be put through a pipe and all live at the same indent.
  - const Providers = pipe(ProviderA, ProviderB, etc)

- Abusing context is the mistake. Something like Zustand is the solution

- I disagree. This shows how the contextual setup for entire app is concentrated at one place. It helps to make app level decisions with more clarity and quickly. And I’m sure this pattern would emerge in any framework trying to do separation of concerns.

- Well, have you tried flutter yet? 😈 There is actually an autogenerated comment there, otherwise you would be totally completely and hopelessly lost between 20-100 „), “, „); “, „}, “ & „}; “…
  - flutter采用函数，闭合括号无法区分指向范围，
  - react采用xml，闭合标签方便区分范围
# [4 Common Patterns You Can Easily Focus On In Your React Code Reviews](https://www.chakshunyu.com/blog/4-common-patterns-you-can-easily-focus-on-in-your-react-code-reviews/)
- Prop Drilling
- A common (anti-)pattern to solve this issue is to pass the value from the parent component all the way to the child component that needs it. 
-  While this works, it means that all the components in between also have to accept that prop.
- If you’re constantly going between files and being navigated all over the place while trying to understand the code, then it’s very likely that you’re dealing with an occurrence of prop drilling. 
- Based on the scenario, solutions include but aren’t limited to using the composition pattern, React context, or compound components.

- Multiple Boolean States
- A common example is a component that fetches some data and needs to handle the logic for retrieving that data. 
  - This almost always goes together with one variable to track whether the data is done loading and one variable to track whether the data request has failed. 
  - In certain scenarios, it’s also relevant to track whether the data request has already been initialized.
- During reviews, this pattern comes to light more quickly.
  -  It’s indicated by multiple numbers of boolean states that are part of the same data flow or the logic flow. 
  -  This is paired with a lot of combined null checking to verify them individually before they can be used in any meaningful way.
- The most straightforward way to solving this problem is changing the implementation of the states to use a different data structure. 
  - Instead of several boolean variables, use one enumeration variable. 
  - Combining this with TypeScript will remove any unreachable state from having to be handled during development.

- Component, Hook, And Props Naming
- The most common mistake regarding naming components, hooks, and props that I’ve experienced is sacrificing clarity for length. 
- Shorter names are easier to read and result in less code but aren’t always more clear. 
- Therefore, it never hurts to include more information in the names, like elaborating on the context in which it should be used, what type it is, what it expects and returns, and more.

- God Component(does too much job)
- In React development, the equivalent would be a component that either receives a lot of data, is responsible for a lot of logic, renders most of the UI, or a combination of these. 
- When reviewing React code, these symptoms become significantly more apparent due to the lack of IDE support in the browser. You’re forced to read through the code in a different way than you’re used to, which makes you focus on different aspects. 
# [Building highly customizable React components_201810](https://ankit-m.github.io/blog/building-highly-customizable-react-components/)
- Building a React web application, for the most part, is writing components which combine to form your user interface.
- No matter how strict the design guidelines are, you cannot expect the same type of button to be used everywhere. There will be some changes required based on the context.
- Customizability allows them to be modified, both visually and functionally, to fit in various use cases. 
- This article outlines certain ways to make your React component highly customizable. 
- Throughout this guide, I will use a Dropdown component to illustrate examples.
- Note: **You do not need to build all your components to be so customizable**. Components which you know will not be used anywhere else, can be simple.

## Define boundaries

- First of all, you should to determine the expectation from your component.
  - usecase, input, output, side effects, deps, NOT

## Simple use case first approach

- Always try to make the component easy to start off with — minimum or no input from the consumer.
  - This makes it easy for consumers who are prototyping or evaluating your component for further use. It is also very helpful for beginners to start off.
  - Ensure that the installation process is straightforward and standard. 
  - You should NOT expect the consumer to make exceptions or add polyfills to use your component.

```JS
const options = [{ id: 1, label: 'opt 1' }, { id: 2, label: 'opt 2' }];

<Dropdown options={options} onClick={e => console.log(e)} />
```

## Basic customization

- Consumers will expect you to support simple changes to your component out of the box.
- To find out these basic customization options, I find it easy to think of changes in two broad categories
- Functionality changes 
  - These affect the way your component behaves. 
  - You may not need to support functionality changes for simple components, but it might make sense for complex components
  - Use your black box representation to identify the functionality changes needed.
  - For each functionality change, identify if it is the responsibility of the component to implement or that of the consumer.
- Style changes
  - These affect the way your component looks.
  - You cannot make any assumptions about the styles and give the consumer maximum freedom to change it.
  - Simple props: Support optional props like size, align, disabled which will allow consumers to make quick adjustments.
  - CSS classes: If your code is styled purely using classes, consumers can simply override the class rules.
  - Avoid `!important` and multiple combinators in your CSS. It is very difficult to override something like `.dropdown > .option > button > span`.

## Renderers and (Container)Components

- The goal is to make it very easy for consumers to adapt the component for their use case. 
- In most cases, these changes are UI changes — changing the appearance, adding different styles, etc. 
- In order to achieve this, I split the building blocks into renderers and components.
- Renderer only cares about how the component looks and other items which need to be displayed. 
  - This has all the CSS classes attached and accepts the bare minimum props required for display. 
  - If a user wants to use their custom component, they can simply pass the custom renderer as a prop.
- Component handles the business logic for the particular block — event handlers, refs, roles, etc. 
  - These are just containers and do not have any styles. 
  - This abstracts away the working logic from rendering and consumers can simply swap out renderers without affecting the functionality. 
  - Advanced consumers, who want complete control, can replace this component and handle everything themselves.
- This splitting allows for quicker changes and promotes modular code, improving the testability of your code.

```JS
function TriggerRenderer(props) {
  return (
    <button className="trigger-renderer" disabled={props.disabled}>
      {props.label}
    </button>
  );
}

function TriggerContainer(props) {
  const Renderer = props.renderer || TriggerRenderer;

  return (
    <div ref={props.triggerRef} role="button" onClick={props.onClick}>
      <Renderer disabled={props.disabled} label={props.label} />
    </div>
  );
}

/**
 * Consumer of the component can swap out either the renderer or the component
 */
function Trigger(props) {
  const Container = props.triggerComponent || TriggerContainer;

  return <Container {...props} renderer={props.triggerRenderer} />;
}
```

- Some might not prefer this splitting as it might create extra HTML tags. 
  - If that worries you so much, then you can simply allow to replace the entire component.

## Custom props

- You should allow the consumer to pass in custom props for these HTML elements. 
- This can be useful for someone who wants to add additional event handlers or tags like aria which you might not have included out of the box.

```JS
function Trigger(props) {
  return (
    <div
      onClick={props.onClick}
      {…props.customTriggerProps}
    >
      Text
    </div>
  );
}
```

## Lightweight

- A few strategies to keep your output bundle size low
- Minify and/or uglify the production output file.
- Make sure that all parent requirements like React and ReactDOM are listed in peerDependencies in your package.json file.
- If your component has a lot of variants/sub-components, allow for partial imports — `import subComp from package/subComp`
- Keep the number of third-party libraries you depend on to a minimum.

## Improving

- Accessibility
  - Your component should be usable by keyboard. 
  - For people who use screen readers, it is crucial that your component add additional information for them to use. This includes using alt, role, aria and other attributes. 

- Resist non-standard js syntax
  - Transpiling will increase your bundle size 

- Enforcing certain usage
- Component design: 
  - Let's take the dropdown example. You can choose to pass `options` as an array of objects or as children

```typescript

// Method 1
const options = [{id: 1, label: 'opt 1'}, {id:2, label:'opt 2'}];

<Dropdown options={options} onClick={e => console.log(e)} />

// Method 2
<Dropdown>
  <Option id='1'>opt 1</Option>
  <Option id='2'>opt 2</Option>
</Dropdown>

// Anti-pattern usage which might break your component
<Dropdown>
  <div class='section-1'>
    <Option id='1'>opt 1</Option>
    <Option id='2'>opt 2</Option>
  </div>
  <div class='section 2'>
    <Option id='1'>opt 1</Option>
    <Option id='2'>opt 2</Option>
  </div>
</Dropdown>
```

- Method 2 might create a false expectation for the consumer that they can pass anything and the component might break. 
- You should be able to determine the best way to use your component and enforce that by the way you design your component.

- typecheck the props your component accepts and prevent basic mistakes made by consumers.
- Documentation: This is one the easiest way to convey information to consumers. It is crucial to highlight what is the purpose component along with usage examples.
- Test cases provide a good reference point to consumers for what and what not to do.

- Overall, I have tried to highlight a few ways to build customizable components in React. 
  - However, how much customization to offer depends on the use case and problem you are trying to solve. 
  - You should evaluate and pick what makes sense for you.

## discussion

- [Victory Custom Components](https://formidable.com/open-source/victory/guides/custom-components/)
- Every element that a Victory component renders may be altered or completely replaced. 
- Most components expose dataComponent, labelComponent, groupComponent, and containerComponent props. 
- The primitive components that Victory components render by default are simple, stateless components with a consistent set of props whenever possible. 
- These primitive components are exported for users to alter, wrap, extend and reference when creating custom components.

- [Chakra as prop and Custom component](https://chakra-ui.com/guides/as-prop)
- By default, all Chakra components work with the `as` prop. 
- There might be some cases where you need to create smaller components with pre-defined styles, and need the `as` prop to work as well.

## [Pass react component as props](https://stackoverflow.com/questions/39652686)

- Using `this.props.children` is the idiomatic way to pass instantiated components to a react component

```JSX
const Label = props => <span>{props.children}</span>
const Tab = props => <div>{props.children}</div>
const Page = () => <Tab><Label>Foo</Label></Tab>
```

- When you pass a component as a parameter directly, you pass it uninstantiated and instantiate it by retrieving it from the props. 
  - This is an idiomatic way of passing down Component classes which will then be instantiated by the components down the tree (e.g. if a component uses custom styles on a tag, but it wants to let the consumer choose whether that tag is a `div` or `span`)

```JS
const Label = props => <span>{props.children}</span>
const Button = props => {
  const Inner = props.inner; // Note: variable name _must_ start with a capital letter 
  return <button><Inner>Foo</Inner></button>
}
const Page = () => <Button inner={Label}/>
```

- If what you want to do is to pass a `children`-like parameter as a prop, you can do that with a new prop name

```JS
const Label = props => <span>{props.content}</span>
const Tab = props => <div>{props.content}</div>
const Page = () => <Tab content={<Label content='Foo' />} />
```

- After all, properties in React are just regular JavaScript object properties and can hold any value - be it a string, function or a complex object.

- you can just pass a component as a prop. 
- I think this is cleaner sometimes as you might want to pass several components and have them render in different places. 
- if child has a prop. how do I access that in the parent. 
  - the basic idea is to turn the question around. Ie, create the variable in the parent and pass it down to the child as a prop. 
  - If you want the child to change the variable then you need to create a function to do this in the parent and also pass that down as another prop.

```typescript
const Parent = () => { 
  return (
    <Child  componentToPassDown={<SomeComp />}  />
  )
}

const Child = ({ componentToPassDown }) => { 
  return (
    <>
     {componentToPassDown}  
    </>
  )
}
```

- [How to replace a component with another one upon event (button click) in react js](https://stackoverflow.com/questions/50552046)
- Now i am returning: `{this.state.components[0]}`
  - when button is clicked, do `this.setState({components:[<EditForm />]})` to update all
  - It works but i was wondering is storing Component and JSX inside state a good idea/ professional practice?
- I would hold in state just a Boolean for showing the edit form or the display and toggle this on button click.

## [Customizing React components using a components provider](https://medium.com/trabe/customizing-react-components-using-a-components-provider-42cdb78acd24)

- When we talk about component customization, we usually think of style theming: changing the way a component looks by adjusting its style properties, based on some global values (the theme).
- however, I’ll be talking about a different level of customization.
  - When you develop a UI library, some of the more complex components are created using other basic components (think a ConfirmationDialog using a Button). 
  - Sometimes letting the user change the style of the basic components deeply nested inside the more complex one is cumbersome; 
- You can use React’s `Context` functionality to create a provider of components for your library.
  - This provider will act as a registry, where you associate each basic component with its implementation. 
  - You can then get those basic components from the registry, and use them to build the rest of the components. 
  - That way, you can change the look & feel or the behavior of a basic component, even when it is deeply nested inside other components.

```JS
import React, { createContext, useContext } from "react";

/* These are the components we'll provide as defaults */
import Button from "./components/button";
import Icon from "./components/icon";

const defaultComponents = {
  button: Button,
  icon: Icon,
};

/* The context itself */
const ComponentsContext = createContext(defaultComponents);

/* The provider lets you change the provided components */
const ComponentsProvider = ({ children, components = defaultComponents }) => (
  <ComponentsContext.Provider value={components}>{children}</ComponentsContext.Provider>
);

/* A custom hook to get access to the provided components */
export const useComponents = () => useContext(ComponentsContext);

/* The components provider itself */
export default ComponentsProvider;
```

- You can use the provider in your app or complex component

```JS
import React from "react";
import { render } from "react-dom";
import ComponentsProvider, { useComponents } from "./components-provider.jsx";

/* A sample page */
const Page = () => {
  /* We get the components from the provider */
  const { button: Button, icon: Icon } = useComponents();

  return (
    <p>
      This is a sample page with
      <Button onClick={() => alert("click")}>a button</Button>
      and an icon
      <Icon name="plane" />
    </p>
  );
};

/* No need to provide anything if you just want the defaults */
const App = () => <Page />;

render(<App />, document.getElementById("app"));

/* You can provide new components,but you had to provide all the components every time */
const App = () => {
    return (
      <ComponentsProvider
      components={{
        button: props => <button className="custom" {...props} />,
      icon: props => <span>{props.name === "plane" ? "🛩" : "🤷‍♀️"}</span>,
    }
  } >
  <Page /> <
  /ComponentsProvider>
);
};

//  let the user override just some of the default components
/* We accept some components and merge them with the default ones */
const ComponentsProvider = ({ children, components = {} }) => (
  <ComponentsContext.Provider value={{ ...defaultComponents, ...components }}>
    {children}
  </ComponentsContext.Provider>
);
```

- Meta-provided components
  - You can provide components that in turn use other provided components to render themselves. 
  - We’re creating a cyclic dependency here (`components-provider.jsx` depends on `button.jsx` to provide the default `Button` implementation, which in turn depends on `components-provider.jsx` to get the `Icon` implementation), but thanks to the way exports work in ES, the module system has no problem resolving the dependencies at build time.

```JS
import React from "react";
import { useComponents } from "../components-provider.jsx";

const Button = ({ children, iconName, ...rest }) => {
  const { icon: Icon } = useComponents();

  return (
    <button {...rest}>
      <Icon name={iconName} /> {children}
    </button>
  );
};

export default Button;
```

## [material-ui Composition](https://material-ui.com/guides/composition/)

- In order to provide the maximum flexibility and performance, we need a way to know the nature of the child elements a component receives. 
  - To solve this problem we tag some of the components with a `muiName` static property when needed.
- Material-UI allows you to change the root element that will be rendered via a prop called `component`.
- The custom component will be rendered by Material-UI like this:
  - return React.createElement(props.component, props)
- This pattern is very powerful and allows for great flexibility, as well as a way to interoperate with other libraries, such as your favorite routing or forms library. 
  - But it also comes with a small caveat!
  - Using an inline function as an argument for the component prop may result in unexpected unmounting, since a new component is passed every time React renders.

```JS
import { Link } from 'react-router-dom';

function ListItemLink(props) {
  const { icon, primary, to } = props;

  // a new component is passed every time React renders
  const CustomLink = props => <Link to={to} {...props} />;

  return (
    <li>
      <ListItem button component={CustomLink}>
        <ListItemIcon>{icon}</ListItemIcon>
        <ListItemText primary={primary} />
      </ListItem>
    </li>
  );
}
```

- The solution is simple: avoid inline functions and pass a static component to the `component` prop instead

```JS
import { Link } from 'react-router-dom';

function ListItemLink(props) {
  const { icon, primary, to } = props;

  // ref stays the same when rerendering
  const CustomLink = React.useMemo(
    () =>
    React.forwardRef((linkProps, ref) => (
      <Link ref={ref} to={to} {...linkProps} />
    )),
    [to],
  );

  // You can also take advantage of the prop forwarding to simplify the code
  // <ListItem button component={Link} to="/">
  return (
    <li>
      <ListItem button component={CustomLink}>
        <ListItemIcon>{icon}</ListItemIcon>
        <ListItemText primary={primary} />
      </ListItem>
    </li>
  );
}
```

# [React Architecture: The React Provider Pattern](https://mortenbarklund.com/blog/react-architecture-provider-pattern/)
- Going from the above to what I consider to be the React Provider Pattern is merely an act of reorganising all the parts into a more organised structure.
- `folder/context.js` – the file defining the context variable used by the structure
  - `const UserContext = React.createContext({state:{}, action:{}})`
- `folder/provider.js` – the (main) context provider wrapping whatever children its given with a dynamic context
  - `return <UserContext. Provider value={value}> {children} </UserContext. Provider>`
- `folder/useContext.js` – a custom hook giving components access to the current context value
  - `return useContext(UserContext); `
- The last requirement is to use a structured approach to the context value in order to increase familiarity and reuse.

- Examples: How to use the React Provider Pattern
- This pattern can be used as application-wide storage in lieu of other libraries such as redux.
- This pattern can be used as component-local storage for UI state.

- Redux (in particular when combined with redux-toolkit) has many functionalities outside of this
  - redux actually uses React Context under the hood these days.
  - It does what it does (application-wide storage) very well, but it might be overkill in a smaller (or even medium-sized) applications.
# [The State Reducer Pattern with React Hooks](https://kentcdodds.com/blog/the-state-reducer-pattern-with-react-hooks)
- Downshift is currently implemented as a render prop component, 
  - because at the time, render props was the best way to make a "Headless UI Component" (typically implemented via a "render prop" API), 
  - which made it possible for you to share logic without being opinionated about the UI. 
- Today however, we have React Hooks and hooks are way better at doing this than render props. 

- As a reminder, the benefit of the state reducer pattern is in the fact that it allows "inversion of control" which is basically a mechanism for the author of the API to **allow the user of the API to control how things work internally**.
- Ok, so the concept goes like this:
  - End user does an action
  - Dev calls dispatch
  - Hook determines the necessary changes
  - Hook calls dev's code for further changes (this is the inversion of control part)
  - Hook makes the state changes

- Now, let's say we wanted to adjust the `<Toggle />` component so the user couldn't click the `<Switch />` more than 4 times in a row unless they click a "Reset" button

- an easy solution to this problem would be to add an if statement in the `handleClick` function and not call `toggle` if `tooManyClicks` is true, 

```JS
function useToggle() {
  const [on, setOnState] = React.useState(false)
  const toggle = () => setOnState(o => !o)
  const setOn = () => setOnState(true)
  const setOff = () => setOnState(false)
  return { on, toggle, setOn, setOff }
}

// traditional solution: change useState
function Toggle() {
  const [clicksSinceReset, setClicksSinceReset] = React.useState(0);
  const tooManyClicks = clicksSinceReset >= 4;
  const { on, toggle, setOn, setOff } = useToggle();

  function handleClick() {
    toggle()
    setClicksSinceReset(count => count + 1)
  }

  return (
    <div>
      <button onClick={setOff}>Switch Off</button>
      <button onClick={setOn}>Switch On</button>
      <Switch on={on} onClick={handleClick} />
      {tooManyClicks ? (
        <button onClick={() => setClicksSinceReset(0)}>Reset</button>
      ) : null}
    </div>
  )
}
```

- use api to invert control

```JS
function Toggle() {
  const [clicksSinceReset, setClicksSinceReset] = React.useState(0);
  const tooManyClicks = clicksSinceReset >= 4;
  const { on, toggle, setOn, setOff } = useToggle({
    reducer(currentState, action) {
      const changes = toggleReducer(currenState, action);
      if (tooManyClicks && action.type === actionTypes.toggle) {
        // other changes are fine, but on needs to be unchanged
        return { ...changes, on: currentState.on }
      } else {
        // the changes are fine
        return changes
      }
    },
  });

  function handleClick() {
    toggle();
    setClicksSinceReset(count => count + 1);
  }

  return (
    <div>
      <button onClick={setOff}>Switch Off</button>
      <button onClick={setOn}>Switch On</button>
      <Switch on={on} onClick={handleClick} />
      {tooManyClicks ? (
        <button onClick={() => setClicksSinceReset(0)}>Reset</button>
      ) : null}
    </div>
  )
}
```

- We could add logic to every one of these helper functions, but I'm just going to skip ahead and tell you that this would be really annoying
- https://codesandbox.io/s/9j0pkq30lo

```JS
import Switch from './switch'

const actionTypes = {
  toggle: 'TOGGLE',
  on: 'ON',
  off: 'OFF',
}

function toggleReducer(state, action) {
  switch (action.type) {
    case actionTypes.toggle: {
      return { on: !state.on };
    }
    case actionTypes.on: {
      return { on: true };
    }
    case actionTypes.off: {
      return { on: false };
    }
    default: {
      throw new Error(`Unhandled type: ${action.type}`)
    }
  }
}

function useToggle({ reducer = toggleReducer } = {}) {
  const [{ on }, dispatch] = React.useReducer(reducer, { on: false });
  const toggle = () => dispatch({ type: actionTypes.toggle });
  const setOn = () => dispatch({ type: actionTypes.on });
  const setOff = () => dispatch({ type: actionTypes.off });
  return { on, toggle, setOn, setOff };
}
// export {useToggle, actionTypes, toggleReducer}

function Toggle() {
  const [clicksSinceReset, setClicksSinceReset] = React.useState(0);
  const tooManyClicks = clicksSinceReset >= 4;

  const { on, toggle, setOn, setOff } = useToggle({
    reducer(currentState, action) {
      const changes = toggleReducer(currentState, action)
      if (tooManyClicks && action.type === actionTypes.toggle) {
        // other changes are fine, but on needs to be unchanged
        return { ...changes, on: currentState.on };
      } else {
        // the changes are fine
        return changes;
      }
    },
  });

  return (
    <div>
      <button onClick={setOff}>Switch Off</button>
      <button onClick={setOn}>Switch On</button>
      <Switch
        onClick={() => {
          toggle()
          setClicksSinceReset(count => count + 1)
        }}
        on={on}
      />
      {tooManyClicks ? (
        <button onClick={() => setClicksSinceReset(0)}>Reset</button>
      ) : null}
    </div>
  )
}

function App() {
  return <Toggle />
}
ReactDOM.render(<App />, document.getElementById('root'))
```

- Remember, what we've done here is enable users to hook into every state update of our reducer to make changes to it. 
  - This makes our hook WAY more flexible, 
  - but it also means that the way we update state is now part of the API 
  - and if we make changes to how that happens, then it could be a breaking change for users. 
  - It's totally worth the trade-off for complex hooks/components, but it's just good to keep that in mind.

- discussion

- https://twitter.com/kentcdodds/status/1256265379648700416
  - Great talk by @kentcdodds on why having too many props in a component can hurt performance and add unnecessary complexity, followed by a practical approach on how to avoid apropcalypse by using the state-reducer pattern with hooks!
# more
- [How to write performant React code: rules, patterns, do's and don'ts](https://www.developerway.com/posts/how-to-write-performant-react-code)
  - Rule #1: If the only reason why you want to extract your inline functions in props into `useCallback` is to avoid re-renders of children components: don’t. It doesn’t work.
  - Rule #2: If your component manages state, find parts of the render tree that don’t depend on the changed state and memoise them to minimize their re-renders.
  - Rule #3. Never create new components inside the render function of another component.
  - Rule #4. When using context, make sure that `value` property is always memoised if it’s not a number, string or boolean.
