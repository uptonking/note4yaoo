---
title: lib-ui-material-ui-v5-docs
tags: [docs, material-ui, react-components]
created: 2022-03-29T05:57:53.866Z
modified: 2022-03-29T05:59:52.797Z
---

# lib-ui-material-ui-v5-docs

# guide

# overview
- MUI is using emotion as a styling engine by default. 
  - If you want to use styled-components instead, run:
  - npm install @mui/material @mui/styled-engine-sc styled-components
- In order to use prebuilt SVG Material icons, npm install @mui/icons-material

- MUI components are self-supporting, and will only inject the styles they need to display. 
  - They don't rely on any global style-sheets such as normalize.css
# faq

## Why do the fixed positioned elements move when a modal is opened?

- Scrolling is blocked as soon as a modal is opened. 
  - This prevents interacting with the background when the modal should be the only interactive content. 
  - However, removing the scrollbar can make your fixed positioned elements move. 
  - In this situation, you can apply a global `.mui-fixed` class name to tell MUI to handle those elements.

## Why does component X require a DOM node in a prop instead of a ref object?

- Components like the Portal or Popper require a DOM node in the container or anchorEl prop respectively.
- Portal might re-render after it mounts because refs are up-to-date before any effects run. 
  - However, just because a ref is up-to-date doesn't mean it points to a defined instance. 
  - If the ref is attached to a ref forwarding component, it is not clear when the DOM node will be available
  - This is especially apparent for `React.lazy` components in `Suspense`. 
  - The above implementation could also not account for a change in the DOM node.
# docs-unstyled
- @mui/base
  - Most of the unstyled components are implemented with the help of a hook (where it makes sense). 
  - Hooks encapsulate logic, while components provide structure.

- Anatomy of an unstyled component
- components
  - an object that allows you to override subcomponents (slots) used by the unstyled "host" component. 
  - Each host component will at least have the Root slot.
- component - a shortcut to components. Root. 
  - Note that if both components. Root and component are specified, component takes precedence.
  - componentsProps - an object with each slot's props
# docs-components
- The Typography component uses the variantMapping prop to associate a UI variant with a semantic element. 
  - It's important to realize that the style of a typography component is independent from the semantic underlying element.
