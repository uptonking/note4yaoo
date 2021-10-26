---
title: ux-design-material
tags: [design, material-design, ux]
created: '2020-10-03T15:28:12.712Z'
modified: '2021-01-01T20:08:06.371Z'
---

# ux-design-material

# material-design

- ref
  - https://material.io/design/introduction/
- theme
  - https://material-ui.com/customization/default-theme/

- breakpoints
  - xs, sm, md, lg, xl
  - 0, 600, 960, 1280, 1920
- typography
  - 1.25-1.5-2.25-3-3.75-6
- palette
  - gray
  - primary:light/dark/main
  - secondary
  - success, info, warning, error
- shadows
- zIndex
  - speedDial1000, drawer1200, modal1300, snackbar1400, tooltip1500

# material-design-components-web

- ## dev
- If you decide to add new components into the DOM after the initial `mdc.autoInit()` , you can make subsequent calls to `mdc.autoInit()` . 
  - This will not reinitialize existing components. 
  - This works since mdc-auto-init will add the `data-mdc-auto-init-state="initialized"` attribute, which tracks if the component has already been initialized.
- mdc-auto-init
  - Create a non-writable, non-enumerable property on the Node whose name is the value of `data-mdc-auto-init` and whose value is `instance` .
  - `instance` be the result of calling `Ctor.attachTo()` and passing in the element as an argument.
- MDC Base contains core foundation and component classes that serve as the base classes for all of MDC Web's foundation classes and components (respectively).
  - Most of the time, you shouldn't need to depend on mdc-base directly. 
  - It is useful however if you'd like to write custom components that follow MDC Web's pattern

- MDCFoundation provides the basic mechanisms for implementing foundation classes. 
  - Provide `init()` and `destroy()` lifecycle methods
  - Provide implementations of the proper static getters where necessary.
    - The static getters specify constants that can be used within the foundation class
    - remember to always put constants into these getters. 
    - This will ensure your component can interop in as many environments as possible, like stylesheet,i18n
- MDCComponent provides the basic mechanisms for implementing component classes.
  - MDCComponent calls its foundation's init() function within its constructor, and its foundation's destroy() function within its own destroy() function.
  - `static attachTo(root)`
    - instantiate and return an instance of the class using the root element provided.
  - `getDefaultFoundation()`
    - Called when no foundation instance is given within the constructor.
  - `initialize()`
    - Called after the root element is attached to the component, but before the foundation is instantiated.
  - `destroy()`
    - perform any additional cleanup work when a component is destroyed.
  - `initialSyncWithDOM()`
    - Called within the constructor. Subclasses may override this method if they wish to perform initial synchronization of state with the host DOM element.
  - `listen(type: string, handler: EventListener)`
    - this is simply a proxy to `this.root_.addEventListener` .
  - `unlisten(type: string, handler: EventListener)`
    - this is simply a proxy to `this.root_.removeEventListener` .
  - `emit(type: string, data: Object, shouldBubble: boolean = false)`
    - Dispatches a custom event of type `type` with detail `data` from the component's root node. 
    - This is the preferred way of dispatching events within our vanilla components.

- theme基于sass变量实现
  - 定义变量 `$black: #000 !default; $border-radius: 0.25rem !default;`
  - 覆盖样式 `@use 'library' with ( $black: #222, $border-radius: 0.1rem );`
- To fix problems with accessibility and design, we suggest you use our Sass mixins, such as `button.filled-accessible()`
- theme工具方法
  - `theme.property()` mixin also accepts a custom property Map for the $value argument
  - `theme.luminance($color)` calculates the luminance value (0 - 1) of a given color.
  - `theme.contrast($back, $front)` calculates the contrast ratio between two colors.
  - `theme.tone($color)` determines whether the given color is "light" or "dark".
  - `theme.text-emphasis($emphasis)` returns opacity value for given emphasis.

- ## [Architecture](https://github.com/material-components/material-components-web/blob/master/docs/code/architecture.md)
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

- ## [Authoring Components](https://github.com/material-components/material-components-web/blob/master/docs/authoring-components.md)
- Starting out from nothing and going straight to a component/adapter/foundation implementation can be at the best daunting(令人气馁的，吓人的), at worst completely impossible from a productivity and experimentation standpoint. 
- Often times, you'll want to build a prototype component in the most straightforward way possible, and then work your way back towards a foundation and adapter. 
- start by building a prototype using vanilla HTML/CSS/Javascript, without worrying about any foundations or adapters. 
- figure out what functionality will need to be proxied through an adapter.
  - Any direct interactions with the host environment will need to be proxied, so that our foundations will be able to integrate into all frameworks across the web platform.
  - host environment refers to the context in which the component is used. It could be the browser, a server component is being rendered on, a Virtual DOM environment, or even a mobile application like React-Native.
  - it's easy to see all of the instances where we interact with the host environment: 
    - it occurs every place we read from or write to our `root` node.
  - In other cases, host environment interaction may not be straightforward, such as `window.addEventListener('resize', ...)` .
- Create the adapter interface
  - all of the host environment interactions have been replaced with adapter methods
  - We no longer recommend using `registerInteractionHandler` and `deregisterInteractionHandler` as adapter methods for adding/removing generic event listeners. 
  - Event handling varies significantly across frameworks(e.g., React Synthetic Events), so we recommend managing events in the component layer.
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
  - This includes `window/document/console` , and others. 
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

 

- ## [Theming Guide](https://github.com/material-components/material-components-web/blob/master/docs/theming.md)
- tips
  - 全局级theme基于sass变量，组件级theme基于css vars

- MDC Web includes a theming system designed to make it easy to change your application's colors.
- At the moment, MDC Web supports theming with Sass and with CSS Custom Property, with plans for CDN support as well, once that service is available.
- MDC Web theming, like Material Design theming, uses two main colors: primary and secondary.
  - The primary color is used throughout most of the application and components, as the main color for your application. 
  - The secondary color is used for floating action buttons and other interactive elements, serving as visual contrast to the primary.
  - MDC Web also defines a surface color, which is used as a background in components.
  - Finally, MDC Web has a number of text colors, 
    - which are used for rendering text and other shapes on top of the primary, secondary and background colors
    - These are specified as either dark or light, in order to provide sufficient contrast to what's behind them
- color-usage
  - Primary, used for most text.
  - Secondary, used for text which is lower in the visual hierarchy.
  - Hint, used for text hints 
    - (such as those in text fields and labels).
  - Disabled, used for text in disabled components and content.
  - Icon, used for icons.
  - On-surface, used for text that is on top of a surface background.
  - On-secondary, used for text that is on top of a secondary - background.
  - On-primary, used for text that is on top of a primary background.

- Building a themed application
  - each card to have a color scheme that matches its category
- Step 1: No theming
- Step 2: Use the MDC Web colors in your own markup
  - Not everything has a `--primary` option, though, particularly where it comes to your own markup
  - Bad approach: write your own custom CSS rules
  - that would not take advantage of MDC Web's theming and would thus be brittle(脆弱的；易碎的)
  - MDC Web provides a number of CSS classes as part of the `mdc-theme` module to help you tackle this problem in a more maintainable way.
  - `mdc-theme--primary-bg, mdc-theme--on-primary`
- Step 3: Changing the theme with Sass
  - The application-wide theme colors that are used as the default across your entire application can be set in Sass.
  - This is as easy as defining three variables (`$primary/$secondary/$background`) in your Sass file, before importing any MDC Web modules.
  - These definitions will override the defaults included in the mdc-theme module, which every themeable component depends on.
  - As for the text colors, these will all be automatically calculated from the primary, secondary and background you provide, as part of the Sass definitions in mdc-theme
- Step 4: Changing the theme with CSS Custom Properties
  - Changing the theme with Sass variables affects the whole application
  - The generated MDC Web CSS uses CSS Custom Properties with hardcoded fallbacks, 
    - which are set to the colors provided in Sass. 
    - This means that you can define your default theme in Sass (like we did above), 
    - but override it in CSS, dependent on context or user preference.
  - you can easily override the colors that get used in MDC Web components by simply redefining the custom property at some level.
  - The custom properties used by MDC Web follow a similar naming convention to the Sass variables and CSS classes
  - The problem is that we only set the `--mdc-theme-primary` custom property.
    - Whereas setting `$mdc-theme-primary` in Sass allows for calculating all the related text colors, it's currently not possible to perform those complex contrast calculations in CSS.
    - This means you'll also have to set all the related text colors
  - Ideally, we should set all of the text colors on primary, since we never know which one an MDC Web component might use. 

- Most MDC Web components provide a set of Sass mixins to customize their appearance, such as changing the fill color, ink color, stroke width, etc.

- Color Theming
  - You can define the theme color sass variables before importing any MDC Web components
  - Inevitably there will be some components that do not work "out of the box". 
    - To fix problems with accessibility and design, we suggest you use our Sass mixins, such as `button.filled-accessible()`
  - Only a very limited number of Material Design color customization features are supported for non-Sass clients. 
    - They are a set of CSS custom properties, and a set of CSS classes.

- Shape Theming
  - Currently shape system for web only supports rounded corners.
  - Only rounded shape designs are currently supported to be customized with sass variables
  - Do not use percentage values with custom properties, since they cannot be resolved by `shape.radius()` at runtime.

- ## [Integrating MDC Web into Frameworks](https://github.com/material-components/material-components-web/blob/master/docs/integrating-into-frameworks.md)
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

- ## [MDC-101 Web: Material Components (MDC) Basics](https://codelabs.developers.google.com/codelabs/mdc-101-web/)
- By uniting style, branding, interaction, and motion under a consistent set of principles and components, product teams can realize their greatest design potential.
- When the user touches or clicks a button, it should display feedback in the form of an ink ripple(波纹). 
  - The ink ripple component requires JavaScript, 
- Using basic HTML markup and just a few lines of CSS and JavaScript, the Material Components for the web library has helped you create a beautiful login page

- ## [MDC-102 Web: Material Structure and Layout](https://codelabs.developers.google.com/codelabs/mdc-102-web/)
- We use the standard Navigation Drawer variant in this codelab. 
  - The standard variant has no drawer-specific logic, so we instantiate the MDCList inside of it directly. 
  - Dismissible and modal variants also exist, which use a dedicated MDCDrawer component for additional features.

- ## [MDC-103 Web: Material Theming with Color, Shape, Elevation and Type](https://codelabs.developers.google.com/codelabs/mdc-103-web/)
- Any global variables you wish to override (e.g. `$mdc-theme-primary` ) must be declared before importing the components' styles into your *.scss files. 
- In this case `_common.scss` is a partial that is imported before anything else in `login.scss` and `home.scss` , so it will apply to both pages' styles.
- Typography can be set either by using the Sass mixin, or by including the specific type class (e.g. `class="mdc-typography--headline6"` ) on your element.
- Elevation is applied by invoking the `mdc-elevation` Sass mixin within a selector representing the elements you want elevated.
- change layout by update `mdc-image-list-standard-columns(4)` to `mdc-image-list-masonry-columns(4)`
- The image list component currently includes 2 variants, standard and masonry, that allow list items to be sized differently or laid out in a specific fashion.
- you can replace the variables you declared for the primary theme
  - $mdc-theme-primary/surface/background, $mdc-theme-on-primary/xxx

- ## [MDC-111 Web: Incorporating Material Components into your codebase](https://codelabs.developers.google.com/codelabs/mdc-111-web)
- Material Components for the web (MDC Web) are framework-agnostic, built using regular JavaScript. 
- The MDC Select component wraps a native HTML `<select>` element.
- You've replaced some common components (text fields, select, and button) without doing a complete redesign of your app. 
- 使用MDC Web组件的流程
  - import css
  - update markup: 注意标签的结构顺序限制、class类名顺序限制
  - import js and instantiate component

- ## [MDC-112 Web: Integrating MDC with Web Frameworks](https://codelabs.developers.google.com/codelabs/mdc-112-web/)
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
    - Implement the Adapter, using non-framework JavaScript
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

- ## [example of integrating with React without Foundation/Adapter pattern](https://github.com/material-components/material-components-web/issues/407)
- What I see is that the foundation used in the React example mostly wires up the native components (vie this.refs). 
- The beauty part is that you are still actually using the Foundation/Adapter pattern, you just don't have to think about it. 
  - If you choose to not interact with the foundation by passing a custom adapter, the component creates one for you with the proper shape, using the element you pass the component.
- you are just using the default foundation which is the one for the web. So it naturally works.

``` typescript
import React from 'react'
import { textfield } from 'material-components-web'

export default class TextField extends React.PureComponent {
  
  // Instantiate the vanilla material component once the react component mounts
  componentDidMount() {
    this.mdcComponent = new textfield.MDCTextfield(this.mdcMount)
  }

  // Clean up the vanilla material component along with the react component 
  componentWillUnmount() {
    this.mcdComponent.destroy()
  }

  render() {
    // Note in the second opening div how I get a reference to the DOM element of text field
    return (
      <div className="mdc-form-field">
        <div className="mdc-textfield" ref={(div) => { this.mdcMount = div }}>
          <input
            type="text"
            className="mdc-textfield__input"
            id="demo-input"
            onChange={this.props.onChange}
          />
          <label htmlFor="demo-input" className="mdc-textfield__label">
            {this.props.label}
          </label>
        </div>
      </div>
    )
  }
}
```
