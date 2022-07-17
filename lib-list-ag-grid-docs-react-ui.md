---
title: lib-list-ag-grid-docs-react-ui
tags: [ag-grid, docs, react]
created: 2021-08-20T12:24:06.284Z
modified: 2021-08-20T12:24:38.227Z
---

# lib-list-ag-grid-docs-react-ui

# guide

# docs

## [React Data Grid: React UI](https://www.ag-grid.com/react-data-grid/reactui/)

- What's Next for React UI
  - In AG Grid v26.2 has a production ready version of React UI. 
    - It is turned on by setting the grid property reactUi=true.
  - In AG Grid v27 we plan to make this the default with a fallback property to keep the old rendering. 
    - The fallback property will be for emergency only and will be released as deprecated.
  - In AG Grid v28 we plan to remove the old way of React rendering.

- Up until now AG Grid React wrapped the JavaScript version of AG Grid. 
  - The next generation of AG Grid React will have it's UI written purely in React. 
- Up until now AG Grid's core was written in Plain JavaScript using our in house rendering engine. 
  - All the frameworks, including React, wrapped the core Plain JavaScript rendering engine.
- The advantage of this was one grid for all frameworks, meaning all of our focus went into one excellent grid, rather than focusing on many grids (one for each framework).
- The disadvantage of this for the React community was sometimes it didn't feel very "Reacty", as AG Grid was not a component written in React.
- React UI is an evolution of how AG Grid uses the React framework. 
  - AG Grid React UI will not be a React wrapper around our in house rendering engine. 
  - AG Grid React UI will have the AG Grid UI ported to React.
- The latest AG Grid v26.0 has a large portion of the grid UI written in React, ready for you to get stuck into and tell us what you think.

- AG Grid React UI does not use portals to host custom components (eg Cell Renderers).
  - Previous to React UI, when the rendering engine was written in Plain JavaScript, React Portals were used to host instances of provided components i.e. Cell Renderer's and Cell Editors etc. 
  - This caused issues such as additional div's appear in the DOM to host the portal, and also sometimes flickering or delayed rendering was visible.
- Before React UI, the grid used to create a React Portal to include the React Cell Renderer. 
  - Now with React UI, the React Cell Renderer is inserted directly.
