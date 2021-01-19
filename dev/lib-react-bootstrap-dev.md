---
title: lib-react-bootstrap-dev
tags: [bootstrap, lib, react]
created: '2020-12-25T12:09:41.310Z'
modified: '2020-12-25T12:10:07.972Z'
---

# lib-react-bootstrap-dev

# guide

- features
  - Rebuilt with React
    - Each component has been built from scratch as a true React component
  - Bootstrap at its core
    - By relying entirely on the Bootstrap stylesheet, React-Bootstrap just works with the thousands of Bootstrap themes you already love.
  - Accessible by default
    - Each component is implemented with accessibility in mind

- Why React-Bootstrap?
  - 总结
    - no jquery, no imperative dom update
    - easier styling, easier state management not from dom
  - React-Bootstrap is a complete re-implementation of the Bootstrap components using React. 
    - It has no dependency on either bootstrap.js or jQuery.
  - Methods and events using jQuery is done imperatively by directly manipulating the DOM. 
  - In contrast, React uses updates to the state to update the virtual DOM. 
    - In this way, React-Bootstrap provides a more reliable solution by incorporating Bootstrap functionality into React's virtual DOM.
  - The CSS and details of Bootstrap components are rather opinionated and lengthy. 
    - React-Bootstrap simplifies this by condensing(使浓缩；使冷凝) the original Bootstrap into React-styled components.
  - Since React-Bootstrap is built with React Javascript, state can be passed within React-Bootstrap components as a prop. 
    - It also makes it easier to manage the state as updates are made using React’s state instead of directly manipulating the state of the DOM. 

# Overview

- You should import individual components like: `react-bootstrap/Button` rather than the entire library. 
  - Doing so pulls in only the specific components that you use, 
  - which can significantly reduce the amount of code you end up sending to the client.

- Because React-Bootstrap doesn't depend on a very precise version of Bootstrap, **we don't ship with any included CSS**. 
  - However, some stylesheet **is required** to use these components.
  - `import 'bootstrap/dist/css/bootstrap.min.css';`
- React-Bootstrap is compatible with existing Bootstrap themes. 
  - Just follow the installation instructions for your theme of choice.
  - Because React-Bootstrap completely reimplements Bootstrap's JavaScript, it's not automatically compatible with themes that extend the default JavaScript behaviors.
- Theming
  - If you stick to the Bootstrap defined classes and variants, there isn't anything you need to do to use a custom theme with React-Bootstrap. 
    - It just works. 
  - But we also make coloring outside the lines easy to do.
    - React bootstrap builds the component classNames in a consistent way that you can rely on
    - You can control how a Component prefixes its classes locally by changing the bsPrefix prop
    - Or globally via the `ThemeProvider` Component.

- React Bootstrap v1 adds full compatibility with Bootstrap 4. 
  - Because bootstrap 4 is a major rewrite of the project, there are significant breaking changes from the pre v1 react-bootstrap.
  - Bootstrap 3 support will continue in react-bootstrap versions < v1.0.0
  - Bootstrap 4 support will be in react-bootstrap versions >= v1.0.0
  - React-Bootstrap only contains components that are present in vanilla Bootstrap. 
    - If functionality was removed from Bootstrap, then it was also removed from React-Bootstrap. 

# pieces
