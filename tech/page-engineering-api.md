---
title: page-engineering-api
tags: [api, engineering]
created: 2020-12-27T10:26:58.415Z
modified: 2020-12-27T10:32:58.026Z
---

# page-engineering-api

# [Material-UI API Design Approach](https://material-ui.com/guides/api/)

- As Sebastian Markbage pointed out, no abstraction is superior to wrong abstractions. 
  - We are providing low-level components to maximize composition capabilities.

- Composition
  - Using the `children` property is the idiomatic way to do composition with React.
  - Sometimes we only need limited child composition, 
    - for instance when we don't need to allow child order permutations(排列；数列). 
    - In this case, providing explicit properties makes the implementation simpler and more performant; 
    - for example, the `Tab` takes an `icon` and a `label` property.
  - API consistency matters.

- Spread
  - Props supplied to a component which are not explicitly documented, are spread to the root element; 
    - for instance, the `className` property is applied to the root.

- Avoid native properties
  - We avoid documenting native properties supported by the DOM like `className`.

- CSS Classes
  - All components accept a `classes` prop to customize the styles. 
  - The classes design answers two constraints: to make the classes structure as simple as possible, while sufficient to implement the Material Design specification.
  - The class applied to the root element is always called `root`.
  - All the default styles are grouped in a single class.
  - The classes applied to non-root elements are prefixed with the name of the element, e.g. `paperWidthXs` in the Dialog component.
  - The variants applied by a boolean property aren't prefixed, e.g. the rounded class applied by the `rounded` property.
  - The variants applied by an enum property are prefixed, e.g. the `colorPrimary` class applied by the `color="primary"` property.
  - A variant has one level of specificity. 
    - The color and variant properties are considered a variant.
    - The lower the style specificity is, the simpler it is to override.
  - We increase the specificity for a variant modifier. 
    - We already have to do it for the pseudo-classes (:hover, :focus, etc.). 
    - It allows much more control at the cost of more boilerplate. 
    - Hopefully, it's also more intuitive.

- Nested components
  - Nested components inside a component have their own
    - flattened properties
    - `xxxProps` property
    - `xxxComponent` property
    - `xxxRef` prop

- Property naming
  - The name of a boolean property should be chosen based on the default value.

- Controlled components
  - Most of the controlled component are controlled via the `value` and the `onChange` properties, 
  - however, the `open/onClose/onOpen` combination is used for display related state.

- boolean vs enum
  - There are two options to design the API for the variations of a component: 
    - with a boolean
      - This API enables the shorthand notation
    - or with an enum/联合类型
      - This API is more verbose
      - However it prevents an invalid combination from being used, bounds the number of properties exposed, and can easily support new values in the future.
  - Material-UI components use a combination of the two approaches according to the following rules:
    - A boolean is used when 2 possible values are required.
    - An enum is used when > 2 possible values are required, or if there is the possibility that additional possible values may be required in the future.

- Ref
  - The `ref` is forwarded to the root element. 
  - This means that, without changing the rendered root element via the `component` prop, it is forwarded to the outermost DOM element which the component renders. 
  - If you pass a different component via the `component` prop, the ref will be attached to that component instead.
