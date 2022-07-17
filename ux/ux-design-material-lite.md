---
title: ux-design-material-lite
tags: [design, material-design, ux]
created: 2020-10-07T10:53:24.928Z
modified: 2021-01-01T20:08:21.973Z
---

# ux-design-material-lite

# material-design-web vs material-ui

- [Should material-ui integrate with material-components-web](https://github.com/mui-org/material-ui/issues/6799)
  - [material-ui Comparison with other libraries](https://v3.material-ui.com/getting-started/comparison/)

- Material-UI focuses exclusively on the React library
  - Supporting one framework allows us to do less but do it better.
  - Having fewer constraints, we can make trade-offs specific to our target framework. We have fewer edge-cases to take into account.
  - We can spend more time on nailing the React use case.

- MDC-web was designed from the ground up to be fully compatible with 3rd party JS frameworks and libraries. 

- MDC Web was designed to be integrated as easily as possible into any and all web frameworks. 
- MDC-Web has less components implemented

# material-design-web vs material-design-lite

## [Material Design Components Web vs material-design-lite](https://github.com/material-components/material-components-web/issues/2639)

- MDC Web tries to be framework agnostic, just like MDL. 
  - Yes there are advantages when doing this, 
  - but they come with this major major drawback: 
    - Developing new components is difficult, time consuming and error prone. 
  - There is no easy way of state managements, no templating, all the advances in virtual DOM are ignored. 
  - In our opinion, this is exactly what killed MDL and I do not see why it shouldn't kill MDC Web too.
- We're using MDC heavily with React and I agree about the framework agnostic model sometimes being a double-edged sword. 
  - In some cases we have opted to replace the MDC JS with pure React code to address issues and to make upgrades a little easier. 
  - For some components it's little more than adding/removing styles or simple event handling which is easy to replace and enhance. 
  - Other components are more problematic because there is a ton of code behind them (drawers and sliders are the big ones.) 
  - CSS ripples are also fine for example, making button and switch components simple to implement in React, plus we get to choose which classes to implement based on our own UX guidelines (so we have limited component props in some cases.)
  - MDC is very careful to never add or remove elements from the DOM, 
    - so it does fit well with multiple modern frameworks and libs, 
    - but I personally prefer reactive code over imperative.  
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

## [Why was material design lite(MDL) deprecated with MDC?](https://stackoverflow.com/questions/41769959/why-was-material-design-litemdl-deprecated-with-mdc)

- MDC Web is built in a way that is completely framework agnostic, so the same code base can be used in idiomatic JS, React, Angular
- we accomplish this by splitting up concerns into two concepts: Components and Foundations. 
- A Component is a ready-to-use JavaScript component, while a Foundation contains all of the shared UI code. 
- The Foundation is useful for low-level usage by frameworks like React/Angular/Vue etc..., and more complex rendering logic.
- Adapter is a configuration object that gets passed to the Foundation. 
  - This will include any logic surrounding templating， data-binding, key/input handling, etc... 
  - What this all boils down to is a logical set of defaults which can be overridden if you're using a framework like React or SSR where those things diverge from how they are done in vanilla javascript in the browser.

## [Migrating from Material Design Lite to web](https://github.com/material-components/material-components-web/blob/master/docs/migrating-from-mdl.md)

- MDL is a singular, universal library consisting of all components and styles in one package.
- MDC Web is designed to be modular and is subdivided into individual component packages
- Both MDL and MDC Web require the user to provide a specific DOM structure for a component, in order for it to function correctly. 
  - This DOM has certain requirements, such as requiring the presence of specific CSS classes, a certain hierarchy, and in some cases, specific HTML elements.
  - In MDC Web, the DOM you specify must be complete; 
  - unlike MDL, the library will not create any missing elements for you.
  - This is done in order to make behavior more deterministic 
    - and give you greater freedom in customizing the non-critical parts of a component's DOM.
- Once a DOM is available, MDL manages component lifecycles automatically, 
  - by running through the page on load, 
  - identifying DOM structures that correspond to MDL components, and automatically upgrading them.
- In MDC Web, however, you have the choice between managing components’ lifecycles yourself, or having them automatically initialized, similarly to MDL
  - For every component that you want to automatically initialize, set the `data-mdc-auto-init` attribute on the root element, with the component’s class name as the value
  - Auto-initialization needs to be triggered explicitly `mdc.autoInit();`
  - When using autoInit, you can access a component’s JavaScript instance via its root DOM element, on a property with the same name as the value you passed to `data-mdc-auto-init`
  - When instantiating manually, be sure to store the returned instance somewhere so that you can access it when you need to; 
  - unlike with auto-initialization, there is no way to retrieve it later via the DOM.
- Internally, MDL is built with Sass, but there was no effort in exposing the Sass mixins and functions to developers.
  - MDC Web similarly involves applying CSS classes to the DOM, but it also puts much more emphasis on customization via Sass mixins and functions.
- MDC Web also includes several new components/packages which have no MDL equivalents. 
