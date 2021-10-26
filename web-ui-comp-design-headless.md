---
title: web-ui-comp-design-headless
tags: [components, headless, ui, web]
created: '2021-04-11T17:36:35.781Z'
modified: '2021-04-11T17:37:29.528Z'
---

# web-ui-comp-design-headless

# guide

- headless ui的实现思路
  - 只提供状态管理和事件行为，将组件样式和dom结构都暴露给外传入
  - 基于场景预定义react组件接口，允许替换默认使用的各个组件

- headless-ui-examples
  - headlessui
    - listbox/select,dropdown/menu,switch,radio-group
    - dialog,popover,disclosure,transition
  - react-spectrum
    - based on react-stately,react-aria
  - renderlesskit-react
    - 依赖reakit,react-aria,chakra-ui
  - reakit
    - who is using: bumbag-ui
  - reach-ui
  - react-containers: 有2种使用方式: hook, render prop
  - radix-ui: 提供了自研stitches的样式解决方案
  - downshift

- more-headless-examples
  - https://github.com/jxom/awesome-react-headless-components
# headless-ui-comparison

## [renderlesskit-react](https://renderlesskit-react.vercel.app/)

- ### How does Renderlesskit React differ from other solutions?
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

- ### Sneak peak of a headless Date Picker component
- https://twitter.com/anuraghazru/status/1331932805387808769
  - Keyboard & screen-reader accessible
  - Totally headless & renderless
  - Composable with hooks
- Built on top of @reakitjs, Components are headless and extremely flexible, 
  - The core logic only consists of state hooks pattern.
  - All the accessibility/keyboard handling logic is also handled in those hooks out of the box.
- Core principles of the library is
  - Accessible
  - Composable
  - Stylable
  - Extensible
- Which means that these components can be used as foundation for larger Design Systems and component libraries. 
  - That's why we don't even provide any default styles with it, thus "renderless"

## [radix-ui](https://radix-ui.com/primitives/docs/overview/introduction)

- Our goal is to create a well-funded, open-source component library that the community can use to build accessible design systems.

- Key Features
- Accessible
  - Components adhere to the WAI-ARIA design patterns where possible.
  -  We handle many of the difficult implementation details related to accessibility, including aria and role attributes, focus management, and keyboard navigation. 
- Unstyled
  - Components ship with zero styles, giving you complete control over styling. 
  - Components are compatible with CSS-in-JS libraries, CSS preprocessors, and vanilla CSS. 
- Opened
  - Our open component architecture provides you granular(细粒度的) access to each component part, 
  - so you can wrap them and add your own event listeners, props, or refs.
- Uncontrolled
  - Where applicable, components are uncontrolled by default but can also be controlled, alternatively. 
  - All of the behavior wiring is handled internally, so you can get up and running as smoothly as possible, without needing to create any local states.
- Developer experience
  - Radix Primitives provides a fully-typed API. 
  - All components share a similar API, creating a consistent and predictable experience. 
  - We've also implemented a truly polymorphic `as` prop, so the prop suggestions update.
- Incremental adoption
  - Each primitive can be installed individually so you can adopt them incrementally.
  - Primitives are also versioned independently
# discuss
- ## In many cases, headless React components (components that only execute code and return null) are better than hooks.
- https://twitter.com/ralex1993/status/1249705985729368068
  - Why? Because you can conditionally render them.
  - You can even loop over them!
  - And there is nothing stopping you from calling hooks inside of your headless components. This is just one easy way to conditionally call hooks.
- While this is true, if you have to choose between exposing a hook and exposing a headless component, choose the hook.
  - Users can make their own headless component out of the hook, but you can't make a hook out of a headless component.

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

- [[RFC] Material-UI v5:  Unstyled components](https://github.com/mui-org/material-ui/issues/20012)

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
