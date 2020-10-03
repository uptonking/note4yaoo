---
title: note-components-design-pattern
tags: [components, pattern]
created: '2020-10-02T11:42:34.698Z'
modified: '2020-10-02T11:44:11.404Z'
---

# note-components-design-pattern

## latest

- 组件库研发方向及特色
  - [跨框架开发ui组件库(stencil)](https://zhuanlan.zhihu.com/p/41974042)
    - 开发者用起来framework-agnostic，但原作者很可能要维护多个port或bridge
  - headless ui
    - 只适合简单组件，复杂组件如table实现功能时很可能与layout密切相关
    - opinionated: ui交互或技术选型具有明显的偏向性
  - ui组件
    - dom结构(非视觉结构)、样式、行为
    - foundation + adapter

## opinionated

- ui设计
  - portal的target容器默认是组件自身或document.body
  - should we show a indeterminate for the header's checkbox if partial is selected
  - Inline Editing is a very common feature in a table, but it's highly coupled with specific ui libraries, so it won't be a part of BaseTable itself.
- 交互设计
  - should we select all the children if the parent is selected
  - how to sync the staled keys if those rows are removed
- 技术选型
  - all in js

## back-garden-design-in-action

- logo: green plum
- design-system-tokens
  - text: sans serif(衬线体多用于印刷)
  - color: mineral-ui-color-palette, primary-mediumseagreen
  - bezel-less
- interaction
  - hover-color
  - click-ripple
  - loader-flower
- animation
  - flip
  - misc
    - rotate
    - unfold
    - point movement
- shape
  - point/polygon-shape-based
  - https://medium.com/google-design/you-need-a-shape-system-8d2aa9016817
- 公共api
  - variant
    - borderless
      - 部分组件提供无边框的版本，如modal
      - 也可考虑实现成dark mode的形式

## material design

### guide

- ref
  - [rmwc: Foundation Adapter Implementation](https://github.com/jamesmfriedman/rmwc/issues/141)

### material-design-components-web

- ### components-catalog
- typography
- button
- icon-button
- chips
  - Chips are compact elements that allow users to enter information, select a choice, filter content, or trigger an action.
  - 类似button group
- ripple
- layout-grid
- menu
- drawer
- tab-bar
- fab
- top-app-bar
- text-field
- radio
- checkbox
- select
- switch
- slider
- card
- list
- image-list
- data-table
- dialog
- elevation
- linear-progress
- snackbar
- theme

- ### [Architecture](https://github.com/material-components/material-components-web/blob/master/docs/code/architecture.md)
- MDC Web is split into packages. Each package is either a Subsystem or a Component. 
  - Subsystems apply to many components. They generally describe style (e.g.: color) or motion (e.g.: animation). 
  - Component packages tend to rely on many subsystem packages. 
  - On the other hand, component packages rarely depend on other component packages. 组件低耦合，相互尽量不依赖。
  - Components require an HTML structure. 
  - Some components are static, but most are dynamic and include some JavaScript.
- All of MDC Web's CSS is generated using Sass. 
  - Sass mixins let us make groups of CSS declarations that we want to reuse on multiple components. 
  - Subsystems provide a Sass mixin, which the component imports in its Sass file. 
  - Each package compiles its Sass files into a single CSS file.
- MDC Web does NOT provide any HTML templates. 
  - We simply provide documentation with the required HTML structure.
- MDC Web has split each dynamic component's JavaScript into two pieces: Foundation and Adapter. 
  - This lets us reuse Foundation code across multiple web platforms, e.g. React and Angular, by re-implementing only the Adapter. 
  - For now we've only implemented a vanilla JavaScript version of the Adapter.
  - Foundation contains the business logic that best represents Material Design, without actually referring to any DOM elements. 
    - The Foundation delegates to Adapter methods for any logic requiring DOM manipulation.
  - Adapter is an interface with all the methods the Foundation needs to implement Material Design business logic. 
    - There can be many implementations of the Adapter, allowing for interoperability with different frameworks.
- MDC Web components are written in TypeScript to increase developer velocity and reduce errors. 
- Instantiated with a root element, the Vanilla Component creates a Foundation instance with a Vanilla Adapter by overriding the getDefaultFoundation method of MDCComponent. 
  - The Vanilla Adapter implements the Adapter APIs and directly references the root element. 
  - The Vanilla Component also exposes proxy methods for any Foundation methods a developer needs to access.
  - Developers who are simply interested in consuming MDC Web (i.e. not providing a wrapper library) should only need to interact with the Component. They should not need to directly access Foundation or Adapter APIs.

- ### [Authoring Components](https://github.com/material-components/material-components-web/blob/master/docs/authoring-components.md)
- Starting out from nothing and going straight to a component/adapter/foundation implementation can be at the best daunting(令人气馁的，吓人的), at worst completely impossible from a productivity and experimentation standpoint. 
- Often times, you'll want to build a prototype component in the most straightforward way possible, and then work your way back towards a foundation and adapter. 
- start by building a prototype using vanilla HTML/CSS/Javascript, without worrying about any foundations or adapters. 
- figure out what functionality will need to be proxied through an adapter.
  - Any direct interactions with the host environment will need to be proxied, so that our foundations will be able to integrate into all frameworks across the web platform.
  - host environment refers to the context in which the component is used. It could be the browser, a server component is being rendered on, a Virtual DOM environment, or even a mobile application like React-Native.
  - it's easy to see all of the instances where we interact with the host environment: it occurs every place we read from or write to our `root` node.
  - In other cases, host environment interaction may not be straightforward, such as `window.addEventListener('resize', ...)` . These are also examples of host environment interaction and must be taken into account.
- Create the adapter interface
  - all of the host environment interactions have been replaced with adapter methods
  - We no longer recommend using `registerInteractionHandler` and `deregisterInteractionHandler` as adapter methods for adding/removing generic event listeners. 
    - Event handling varies significantly across frameworks (e.g., React Synthetic Events), so we recommend managing events in the component layer.
- Refactor your existing code into a foundation class
  - As a convention in our codebase, we define a static `defaultAdapter` getter that returns an adapter with NOP signatures for each function. 
- Build a component on top of that foundation, providing an adapter
- Component has two main jobs:
  - Provide an idiomatic(地道的、符合习惯的) interface to the foundation's functionality within the host environment
  - Provide an adapter to the foundation that will allow it to work within the host environment
- If a best practice prevents you from improving or maintaining your component, ignore it. 
  - However, justify your slight, preferably in the form of documentation or a code comment.
- Design adapter interfaces to be simple and intuitive
- Most adapter methods should be one-liners, such as "add a class" or "update a style property." 
  - Users should not have to guess about what the purpose of an adapter method is, nor what its expected input and output should be.
- setStyle
- Do not reference host objects within foundation code
  - To ensure your foundation is as compatible with as many frameworks as possible, avoid directly referencing host objects within them. 
  - This includes `window` , `document` , `console` , and others. 
  - Only reference global objects defined within the ECMAScript specification within your foundations
  - We make an exception for this rule for `requestAnimationFrame` , but in the future we may refactor that out as well. 
  - In addition, a workaround to working with host objects in a foundation is to ask for them via the adapter.
- Clean up all references on destruction
- Authoring components for MDC Web
  - A typical component within our codebase looks like so:

``` 
packages/
  ├── mdc-component/
      ├── test/
          ├── foundation.test.ts # Unit tests for component's foundation
          ├── mdc-component.test.ts # Unit tests for component
      ├── README.md # Usage instructions and API documentation
      ├── adapter.ts # Adapter interface implemented by framework wrappers and the vanilla component
      ├── foundation.ts # Framework-agnostic business logic used by wrapper libraries and the vanilla component
      ├── component.ts # Vanilla component and adapter implementations for clients who aren't using a framework
      ├── constants.ts # Constant values used by one or more files in the package (e.g., cssClasses, strings, numbers)
      ├── index.ts # Forwards exports from other files in the package (adapter, foundation, component, util, etc.)
      ├── types.ts # (optional) Contains types and interfaces exposed in public APIs unrelated to the vanilla component
      ├── util.ts # (optional) Framework-agnostic helper functions (e.g., feature detection)
      ├── mdc-component.scss # The main source file for the component's CSS
      └── package.json # The components package file
```

- Separate reusable variables and mixins from main scss
  - If variables and mixins are intended to be used outside of a single stylesheet, refactor them out into sass partials. 
  - These files can then be included in other stylesheets without having extra CSS omitted both times. 
  - As a rule of thumb, never `@import` sass files which output CSS, as it will most likely be duplicate output.
- follow BEM pattern `.mdc-block__element--modifier{}`
- Define a static `attachTo(root)` method for every component
  - `static attachTo(element: HTMLElement) => Constructor`
  - mdc-auto-init requires this method to be present
- Define a `defaultAdapter` getter for every foundation
  - All foundations must define a static defaultAdapter method which returns an adapter with all functions defined. 
  - The functions should essentially be NOPs; taking no parameters and returning the correct type
  - Our convention is to annotate the function via inline comments using Typescript's type annotations.
  - It is also a convention to override a foundation's constructor to mix in the passed adapter param to a default adapter object. 
    - This ensures that the adapter is guaranteed to have the correct shape.
- Define all exported CSS classes, strings, and numbers as foundation constants.
  - The primary purpose of this is so that our components can interoperate with aspects of Google's front-end infrastructure, such as Closure Stylesheets' CSS Class Renaming mechanism.
  - In addition, it provides the added benefit of semantic code, and less magic strings/numbers.
- To ensure that all packages behave consistently, all components must extend MDCComponent and all foundations must extend MDCFoundation
-  Before a test ends, ensure that any elements attached to the DOM have been removed.
- how to create a component instance for a single element
  - `const comp = new MDCFoo(document.querySelector('.mdc-foo'));`
 

- ### [Theming Guide](https://github.com/material-components/material-components-web/blob/master/docs/theming.md)
- MDC Web includes a theming system designed to make it easy to change your application's colors.
- MDC Web supports theming with Sass and with CSS Custom Property, with plans for CDN support as well, once that service is available.
- MDC Web theming, like Material Design theming, uses two main colors: primary and secondary.
- The secondary color is used for floating action buttons and other interactive elements, serving as visual contrast to the primary.
- MDC Web also defines a surface color, which is used as a background in components.
- MDC Web provides a number of CSS classes as part of the `mdc-theme` module to help you tackle this problem in a more maintainable way.
- Changing the theme with Sass variables affects the whole application, 
- Changing the theme with CSS Custom Properties  by simply redefining the custom property at some level.
- Ideally, we should set all of the text colors on primary, since we never know which one an MDC Web component might use. 
- Most MDC Web components provide a set of Sass mixins to customize their appearance, such as changing the fill color, ink color, stroke width, etc. T

- ### [Integrating MDC Web into Frameworks](https://github.com/material-components/material-components-web/blob/master/docs/integrating-into-frameworks.md)
- MDC Web was designed to be integrated as easily as possible into any and all web frameworks. 
- There are two approaches you can take for integrating our components into frameworks
- The **Simple Approach**: Wrapping MDC Web vanilla components.
  - Include the Component's CSS on the page any way you wish
  - Create a wrapper component for your framework of choice, and add a property which will be set to the value of the MDC Web Component. We'll call this `mdcComponent` .
  - When the wrapper component is initialized (e.g. it is instantiated and attached to the DOM), instantiate the MDC Web component with a root element, and assign it to the `mdcComponent` property.
  - When the wrapper component is destroyed (e.g. it is unbound and detached from the DOM), call `mdcComponent.destroy()` to clean up the MDC Web component.
  - This general approach will work for almost all basic use-cases.
- Many modern front-end libraries/frameworks, such as react and angular, wind up targeting more than just a web browser. 
- Every component comes with a complementary foundation class, which is usually called `MDCComponentFoundation` , where `MDCComponent` is the name of a component. 
- The **Advanced Approach**: Using foundations and adapters
  - Include the component's CSS on the page any way you wish
  - Add an instance property to your component which will be set to the proper foundation class. We'll call this `mdcFoundation` .
  - Instantiate a foundation class, passing it a properly configured adapter as an argument
  - When your component is initialized, call `mdcFoundation.init()`
  - When your component is destroyed, call `mdcFoundation.destroy()`
- some of the adapter APIs can be quite complex
  - Adapters are strictly versioned
    - any change to an adapter interface - associative or not - is considered breaking and will cause a major version update of the component.
  - Every adapter interface is thoroughly documented within each component's README
  - Most adapter methods are one-liners, and for those that aren't, we provide util objects which implement those methods.
  - We try and provide guidance on different ways to implement certain adapter methods that may seem ambiguous

- ### [MDC-101 Web: Material Components (MDC) Basics](https://codelabs.developers.google.com/codelabs/mdc-101-web/)
- By uniting style, branding, interaction, and motion under a consistent set of principles and components, product teams can realize their greatest design potential.
- When the user touches or clicks a button, it should display feedback in the form of an ink ripple(波纹). 
  - The ink ripple component requires JavaScript, 
- Using basic HTML markup and just a few lines of CSS and JavaScript, the Material Components for the web library has helped you create a beautiful login page

- ### [MDC-102 Web: Material Structure and Layout](https://codelabs.developers.google.com/codelabs/mdc-102-web/)
- We use the standard Navigation Drawer variant in this codelab. 
  - The standard variant has no drawer-specific logic, so we instantiate the MDCList inside of it directly. 
  - Dismissible and modal variants also exist, which use a dedicated MDCDrawer component for additional features.

- ### [MDC-103 Web: Material Theming with Color, Shape, Elevation and Type](https://codelabs.developers.google.com/codelabs/mdc-103-web/)
- Any global variables you wish to override (e.g. `$mdc-theme-primary` ) must be declared before importing the components' styles into your *.scss files. 
- In this case, `_common.scss` is a partial that is imported before anything else in `login.scss` and `home.scss` , so it will apply to both pages' styles.
- Typography can be set either by using the Sass mixin, or by including the specific type class (e.g. `class="mdc-typography--headline6"` ) on your element.
- Elevation is applied by invoking the `mdc-elevation` Sass mixin within a selector representing the elements you want elevated.
- change layout by update `mdc-image-list-standard-columns(4)` to `mdc-image-list-masonry-columns(4)`
- The image list component currently includes 2 variants, standard and masonry, that allow list items to be sized differently or laid out in a specific fashion.
- you can replace the variables you declared for the primary theme
  - $mdc-theme-primary/surface/background, $mdc-theme-on-primary/xxx

- ### [MDC-111 Web: Incorporating Material Components into your codebase](https://codelabs.developers.google.com/codelabs/mdc-111-web)
- Material Components for the web (MDC Web) are framework-agnostic, built using regular JavaScript. 
- MDC Web uses a CSS preprocessor called Sass.
- The MDC Select component wraps a native HTML `<select>` element.
- You've replaced some common components (text fields, select, and button) without doing a complete redesign of your app. 
- 使用MDC Web组件的流程
  - import css
  - update markup: 注意标签的结构顺序限制、class类名顺序限制
  - import js and instantiate component

- ### [MDC-112 Web: Integrating MDC with Web Frameworks](https://codelabs.developers.google.com/codelabs/mdc-112-web/)
- MDC Web is engineered to integrate into any front end framework while upholding the principles of Material Design. 
  - The following codelab guides you through building a React Component, which uses MDC Web as a foundation. 
  - The principles learned in this codelab can be applied to any JavaScript framework.
- MDC Web's JavaScript layer is comprised of three classes per component: the Component, Foundation, and Adapter. 
  - This pattern gives MDC Web the flexibility to integrate with frontend frameworks.
  - Foundation contains the business logic that implements Material Design. 
    - **The Foundation does not reference any HTML elements**. 
    - This lets us abstract HTML interaction logic into the Adapter. 
    - Foundation has an Adapter.
  - Adapter is an interface. 
    - The Adapter interface is referenced by the Foundation to implement Material Design business logic. 
    - You can implement the Adapter in different frameworks such as Angular or React. 
    - **An implementation of an Adapter interacts with the DOM structure**.
  - Component has a Foundation, and its role is to
    - Implement the Adapter, using non-framework JavaScript, and
    - Provide public methods that proxy to methods in the Foundation.
- Every package in MDC Web comes with a Component, Foundation, and Adapter. 
  - To instantiate a Component, you must pass the root element to the Component's constructor method. 
  - The Component implements an Adapter, which interacts with the DOM and HTML elements. 
  - The Component then instantiates the Foundation, which calls the Adapter methods.
- To integrate MDC Web into a framework, you need to create your own Component in that framework's language/syntax. 
  - The framework Component implements MDC Web's Adapter and uses MDC Web's Foundation.
- This codelab demonstrates how to build a custom Adapter to use the Foundation logic to achieve a Material Design React Component
- In React, the `render` method outputs the Component's HTML. 
- The approach
  - Implement the `Adapter` methods.
  - Initialize the `Foundation` in the `componentDidMount` .
  - Call the `Foundation.destroy` method in the `componentWillUnmount` .
  - Establish variant management via a getter method that combines appropriate class names.
- The non-framework JS `TopAppBar` Component implements the following Adapter methods
  - hasClass()/addClass()/setStyle()/getTopAppBarHeight()/...
  - notifyNavigationIconClicked()/registerScrollHandler()/...
- Because React has synthetic events and different best coding practices and patterns, the Adapter methods need to be reimplemented.
- React doesn't have an API to manage classes. 
  - To mimic native JavaScript's add/remove CSS class methods, add the `classList` state variable.
- Foundation instantiation happens in the componentDidMount method.
  - because the Foundation needs a DOM element.
- This tutorial highlights our decision to split MDC Web code into 3 parts, the Foundation, Adapter, and Component. 
  - This architecture allows components to share common code while working with all frameworks. 

- ### [Material Design Components Web vs material-design-lite](https://github.com/material-components/material-components-web/issues/2639)
- MDC Web tries to be framework agnostic, just like MDL. 
  - Yes there are advantages when doing this, 
  - but they come with this major major drawback: Developing new components is difficult, time consuming and error prone. 
  - There is no easy way of state managements, no templating, all the advances in virtual DOM are ignored. 
  - In our opinion, this is exactly what killed MDL and I do not see why it shouldn't kill MDC Web too.
- We're using MDC heavily with React and I agree about the framework agnostic model sometimes being a double-edged sword. 
  - In some cases we have opted to replace the MDC JS with pure React code to address issues and to make upgrades a little easier. 
  - For some components it's little more than adding/removing styles or simple event handling which is easy to replace and enhance. 
  - Other components are more problematic because there is a ton of code behind them (drawers and sliders are the big ones.) 
  - CSS ripples are also fine for example, making button and switch components simple to implement in React, plus we get to choose which classes to implement based on our own UX guidelines (so we have limited component props in some cases.)
  - MDC is very careful to never add or remove elements from the DOM, so it does fit well with multiple modern frameworks and libs, but I personally prefer reactive code over imperative.  
  - I also feel that this team does a fantastic job of doing as much with CSS as possible which makes implementing pure React components so much easier. 
  - Overall our experience with MDC has been excellent though: all that official scss alone, which is dead simple to theme, has given our web apps a modern look and feel and has saved us from spending time and money implementing our own company design language. 
- MDC Web will continue to be framework agnostic with our Foundation/Adapter pattern. 
  - This pattern allows us to push Material Design changes to wrapper libraries quickly.
  - We have not been focusing on building shallow implementations of all MD components. 
  - Instead we've focused on building a robust implementation of a few MD components. 
  - We've found that getting just one component to work in multiple situations (multiple Web platforms, multiple browsers, RTL, accessibility, color customization, typography customization) is ... well ... tricky!
  - But I am confident our level of attention on this smaller set of components will make MDC Web a long running and maintained product.
  - Breaking changes will not come to some final end, because design is never done, so MDC Web is never done.
- Material Design Lite (MDL) lets you add a Material Design look and feel to your static content websites. 
  - It doesn't rely on any JavaScript frameworks or libraries. 
  - Take note that Material Components for Web, which is MDL v2, is under early Alpha stages
- Material Components for the web is the successor to Material Design Lite. 
  - In addition to implementing the Material Design guidelines, it provides more flexible theming customization, not only in terms of color, but also typography, shape, states, and more. 
  - It is also specifically architected for adaptability to various major web frameworks.

- ### [Migrating from Material Design Lite](https://github.com/material-components/material-components-web/blob/master/docs/migrating-from-mdl.md)
- MDL is a singular, universal library consisting of all components and styles in one package.
- MDC Web is designed to be modular and is subdivided into individual component packages
- Both MDL and MDC Web require the user to provide a specific DOM structure for a component, in order for it to function correctly. 
  - This DOM has certain requirements, such as requiring the presence of specific CSS classes, a certain hierarchy, and in some cases, specific HTML elements.
  - In MDC Web, the DOM you specify must be complete; 
  - unlike MDL, the library will not create any missing elements for you.
  - This is done in order to make behavior more deterministic and give you greater freedom in customizing the non-critical parts of a component's DOM.
- Once a DOM is available, MDL manages component lifecycles automatically, by running through the page on load, identifying DOM structures that correspond to MDL components, and automatically upgrading them.
  - In MDC Web, however, you have the choice between managing components’ lifecycles yourself, or having them automatically initialized, similarly to MDL
  - For every component that you want to automatically initialize, set the `data-mdc-auto-init` attribute on the root element, with the component’s class name as the value
  - Auto-initialization needs to be triggered explicitly `mdc.autoInit();`
  - When using autoInit, you can access a component’s JavaScript instance via its root DOM element, on a property with the same name as the value you passed to `data-mdc-auto-init`
  - When instantiating manually, be sure to store the returned instance somewhere so that you can access it when you need to; 
  - unlike with auto-initialization, there is no way to retrieve it later via the DOM.
- Internally, MDL is built with Sass, but there was no effort in exposing the Sass mixins and functions to developers.
  - MDC Web similarly involves applying CSS classes to the DOM, but it also puts much more emphasis on customization via Sass mixins and functions.
- MDC Web also includes several new components/packages which have no MDL equivalents. 
