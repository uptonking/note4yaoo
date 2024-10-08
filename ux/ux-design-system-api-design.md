---
title: ux-design-system-api-design
tags: [api-design, design-system, ux]
created: 2021-01-02T22:26:48.350Z
modified: 2023-01-09T15:44:42.139Z
---

# ux-design-system-api-design

# adobe spectrum

## pieces

- `@spectrum/spectrum-dna` has been updated to `@spectrum-css/vars`
  - The vars component contains all the variables that drive the presentation of a component.

## components

## styling

- React Spectrum components are designed to be consistent across all Adobe applications. 
  - They include built-in styling that has been considered carefully, and extensively tested. 
  - In general, customizing Spectrum design is discouraged, 
  - but most components do offer control over layout and other aspects. 
  - In addition, you can use Spectrum defined variables to ensure your application conforms to design requirements, and is adaptive across platform scales and color schemes.

- Style props
  - All React Spectrum components support a limited set of styling options, including layout, spacing, sizing, and positioning options. 
  - While **internal component styles such as padding, colors, borders and text styles are included in Spectrum and not available to override**, external styles like margins and sizes can be set on all components.
  - Supported styling options are available as props on every React Spectrum component

- While the traditional `className` and `style` props are not supported in React Spectrum components, there are two escape hatches that you can use at your own risk. 
  - These are `UNSAFE_className` and `UNSAFE_style`. 
  - Use of these props should be considered a last resort.
  - They can be used to work around bugs or limitations in React Spectrum

## theming

- Colors, sizing, and spacing options can be customized through the use of CSS variables which are defined using the `Provider` component. 
  - Themes consist of variable definitions for light and dark color schemes, along with medium and large platform scales. 
  - Themes can also be nested to allow different parts of an application to adopt a different appearance.
- By default, React Spectrum automatically switches between color schemes according to the operating system setting using the `prefers-color-scheme` media query

- Themes are specified by passing a `Theme` object to the `Provider` component. 
  - This object includes several css modules which define the values for the variables in each color scheme and platform scale. 
  - Each CSS module defines a CSS class which includes the variables it defines, 
    - and Provider applies these classes according to media queries and prop settings.
- React Spectrum includes three themes by default.
  - The defaultTheme uses the Spectrum light and darkest color themes
  - The darkTheme uses the Spectrum dark and darkest color themes
  - The lightTheme uses the Spectrum lightest and darkest color themes

## layout

- The Flex and Grid components are containers, which are responsible for the layout of their children. 
  - Flex follows the CSS flexbox algorithm, while Grid implements CSS grid
  - These components provide props with pre-defined Spectrum variables for sizing, spacing, and other layout options. 
- In general, you should prefer using flex and grid over other CSS layout models. 
- Spacing between components should be left to parent layout components rather than added as via margins to specific children. 
  - This helps ensure components are composable when reused in different places, and ensures that spacing is consistent.
- Several React Spectrum components include pre-defined layouts that you can insert elements into via slots. 
  - Slots are named areas in a component that receive children and provide style and layout for them. 
  - This often occurs automatically through the use of semantic elements like Header, Content, and Footer, which include default slots out of the box.
# discuss
- ## 

- ## 

- ## 

- ## 🆚️ What’s a better DX for you all, asChild in Radix or a render prop like in Ariakit?
- https://x.com/vladyslavmoroz/status/1836383274429473193
- render by far:
  - easier to refactor, it's a prop that can by added/removed versus having to manipulate a tree. with `asChild` , you can't pass `children` to the component because `props.children` is already occupied by the render target
  - can still pass children to the component
  - supports callback API too for advanced use cases

- with asChild you have to deal with open and close tags, while with render you select a single string and can remove it or move it somewhere else

- The only thing I dislike about asChild is seeing an additional nesting level. My brain thinks two elements are being rendered until I realize an asChild prop is present.

- both render and asChild rely on cloning if you want to pass additional props, so if that's the goal - both are bad, cloning is terrible
- What’s terrible about cloning exactly?
  - perf overhead and also the basic idea, when you try to pass something to the child without it being actively accepting what you are passing, you are basically shoveling props into component's throat
  - cloning as a way to move an instance from one place to nother in some rare cases, might be acceptable, depending on the overhead react currently has on that, but generally its a hack, we need to avoid that

- render is good when you can take it as is, without passing props

- ## [Theme, States, Modifiers, and Overrides](https://github.com/souporserious/jsxui/discussions/16)
- Problem
  - Managing Design Systems for React and React Native can be difficult
  - There are great features of CSS, but these don't carry over into JSX
  - Lack of constraints make static analysis hard
- Solution
  - Primitives to help make building UIs easier and more ergonomic
  - The goal of this library is to make building, maintaining, and analyzing Design Systems easier while bringing some of the niceties of writing CSS into JSX.

- ## [Implementing Spectrum: Getting Organizational Buy-In on Design Systems_201809](https://xd.adobe.com/ideas/principles/design-systems/implementing-spectrum-how-adobe-is-coming-together-to-build-a-new-design-system/)
- When design values aren’t connected to a single source of truth, implementations quickly become misaligned.
- Keeping things connected to a single source of truth ensures our design intent is mapped consistently across a variety of implementations, and that makes Spectrum an “easier sell” as a design system for multiple product teams with their own individual needs.
- One way we do this is via our repository of design variables, which we call Spectrum DNA. 
- This repository, which is co-managed by a designer and engineer on the Spectrum team, is a collection of values that defines visual attributes
  - colors, type styles, padding, and so forth 
  - (basically, any aspect of the design that can be expressed as data).
