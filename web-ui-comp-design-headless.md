---
title: web-ui-comp-design-headless
tags: [components, headless, ui, web]
created: '2021-04-11T17:36:35.781Z'
modified: '2021-04-11T17:37:29.528Z'
---

# web-ui-comp-design-headless

# guide

- headless-ui-examples
  - headlessui
  - renderlesskit-react
  - react-spectrum
  - reakit
    - bumbag-ui,renderlesskit-react
  - reach-ui
  - react-containers
  - downshift

# discuss

- ## In many cases, headless React components (components that only execute code and return null) are better than hooks.
- https://twitter.com/ralex1993/status/1249705985729368068
  - Why? Because you can conditionally render them.
  - You can even loop over them!
  - And there is nothing stopping you from calling hooks inside of your headless components. This is just one easy way to conditionally call hooks.
- While this is true, if you have to choose between exposing a hook and exposing a headless component, choose the hook.
  - Users can make their own headless component out of the hook, but you can't make a hook out of a headless component.

- ## How does Renderlesskit React differ from other solutions?
- https://survivejs.com/blog/renderlesskit-interview/
- Under the hood, Renderlesskit uses Reakit
  - There are two parts for creating any components in Reakit: component hook and state hook.
- The main difference is that unlike traditional component libraries, Renderlesskit does not have any styling opinions nor does it depend on any CSS frameworks while providing as much flexibility as possible.
- It also differs from other libraries in the aspect of the core system. 
  - We are only extending the Reakit component ecosystem using reakit-system. 
  - It is similar to react-aria but uses reakit-system to achieve the same behaviors.
- Bumbag, radix-ui, downshiftjs, headlessui, react-spectrum
  - These are all amazing libraries which are very similar at core
  - but what we wanted is an in-house component library at timelessco to use as a foundation for our next design system.
  - The hope is that we can build a UI library and ultimately to create a nocode design system designer.

- There is a new style of component libraries like reach-ui and @radix_ui that just offer functionality and doesn't try to be a design system. 
  - IMO this is the most important thing that has happened to the react ecosystem since... Probably React.

- ## material-ui: Provide a version of the components without any styles
- https://github.com/mui-org/material-ui/issues/6218
- SliderBase is a version of the component with almost no dependencies (it's very bundle-size efficient). The component can be customize with a couple of approaches.
  - global class names. This might be the simplest approach. It works well with CSS-modules, raw CSS, and styled-components.
  - a components prop to inject nested custom components. This works well with styled-components and for performing DOM changes.
- Alternative approaches
- hooks
  - It doesn't scale to complex components, can't work with an advanced data grid or date picker. I think that react-table surface this limitation well.
- Closer to DOM nodes
  - simpler customization
  - Implementation more challenging, need to support more permutations

- ## Will hooks kill #headless components like #downshift?
- https://twitter.com/sseraphini/status/1072421758043611137
- They will be eventually re-written with hooks. 
  - But there's still room for render props. 
  - One case is rendering components dynamically (inside conditions or loops).

- ## We all know base + variant pattern in design system. 
- https://twitter.com/dev__adi/status/1308632176502611969
  - Problem is that when you make a new variant from the base you throw away lot of UI logic. 
  - But suppose that logic is abstracted in a hook then all variants can use the hook and not throw away existing work.
- Think of React hooks as Headless UI. 
  - You can write all your logic in them and then inside your component use the logic but customize the styles just like you want.
- How do you usually implement variants in React?
  - [React Buttons with the Base + Variant Pattern](https://devadi.netlify.app/blog/design-systems-react-buttons-base-variant)

# ref
