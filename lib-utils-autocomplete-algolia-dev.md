---
title: lib-utils-autocomplete-algolia-dev
tags: [algolia, autocomplete]
created: 2023-06-05T07:03:10.223Z
modified: 2023-06-05T07:04:54.711Z
---

# lib-utils-autocomplete-algolia-dev

# guide

- features
  - 支持 display tags in the search box

- pros
  - framework-agnostic

- cons

- api设计
  - 大多数组件都是 dom-container + data/source + view/templates/vdom + options，包括react
# dev

# docs

## overview

- Autocomplete is an open source, production-ready JavaScript library for building autocomplete experiences.

- All you need to get started is:
  - A **container** to inject the experience into
    - Make sure to provide a container (like a `div`), not an `input`. Autocomplete generates a fully accessible search box for you.
  - **Data** to fill the autocomplete with
    - The data that populates the autocomplete results are called **sources**.

- The library creates an input and provides the interactivity and accessibility attributes, but you’re in full control of the DOM elements to output.

- Unlike InstantSearch, Autocomplete doesn’t provide a library of ready-made UI widgets. 

## data sources

- Sources define where to retrieve the items to display in your autocomplete dropdown. 
  - You define your sources in the `getSources` function by returning an array of source objects.
  - Each source object needs to include a `sourceId` and a `getItems` function that returns the items to display. 
  - **Sources can be static or dynamic**.
- getSources function returns an array of sources. 
  - Each source implements a getItems function to return the items to display. 
  - These items can be a simple static array, but you can also use a function to refine items based on the query. 
  - **The `getItems` function is called whenever the input changes**.
- getSources function supports promises so that you can fetch sources from any asynchronous API.

## templates/view

- Although you’ve now declared what items to display using getSources, you still won’t see anything until you’ve defined how to display the items you’ve retrieved.
- Templates 
  - define how to display items in your Autocomplete 
  - can return a string or anything that’s a valid Virtual DOM element. 

- The rendering system of Autocomplete uses an agnostic virtual DOM implementation. 
  - This ensures great performance even with many renders, safety against cross-site scripting (XSS) attacks, inline event handling, and more.
- You can return anything from each template as long as they’re valid virtual DOM elements (VNodes).
  - For example, templates can return a string, Or an HTML string, Or a Preact component
- Autocomplete uses Preact 10 to render templates by default. It isn’t compatible with earlier versions.

- Every Autocomplete template provides an `html` function that you can use as a tagged template.
  - The provided html function works in the browser without any build step

- You can use plain JavaScript to build dynamic templates.

- Returning VNodes directly
  - The JSX syntax compiles down to VNodes. 
  - If you’re using JSX in your project, you can directly return JSX templates.
  - Each template function provides access to `createElement` and Fragment to create VNodes.

- By default, Autocomplete uses Preact 10 internally to render templates. 
  - If you’re using another virtual DOM implementation, you can pass a **custom renderer**.
  - By default,  `createElement` and `Fragment` default to Preact’s `preact.createElement` (or `h`) and `preact.Fragment`. If you’re using another virtual DOM implementation, you can replace them.

- Autocomplete exposes `components` to all templates to share them everywhere in the instance.

## state

- The state is an underlying set of properties that drives the autocomplete behavior.
- The state is available in all lifecycle hooks so you can customize the behavior.

- State changes occur automatically when a user interacts with the autocomplete (updates the input text, selects an item, etc.). 
  - You can react to state changes using the `onStateChange` lifecycle hook
- You can also manually update the state using setters. 
  - When using state setters, you should also call `refresh` to update the UI with fresh sources based on the updated state.

- Sometimes you need to store arbitrary data so you can access it later in your autocomplete. 
  - Autocomplete lets you store data using its Context API and access it anywhere from the state.
  -  You can then access the context in `state.context`.
- **Context can be handy when developing Autocomplete plugins**. 
  - It avoids polluting the global namespace while still being able to pass data around across different lifecycle hooks

## plugins

- Autocomplete lets you extend and encapsulate custom behavior with its Plugin API.
  - For example, the official Algolia Insights plugin automatically sends click and conversion events to the Algolia Insights API whenever a user interacts with the autocomplete.
- Plugins execute sequentially, in the order you define them.

- An Autocomplete plugin is an object that implements the `AutocompletePlugin` interface.
- It can provide sources, react to state changes, and hook into various autocomplete lifecycle steps. 
  - It has access to setters, including the Context API, allowing it to store and retrieve arbitrary data at any time.
- If you want to package and distribute your plugin for other people to use, you might want to expose a function instead.
  - like createGitHubReposPlugin

- Official plugins
  - autocomplete-plugin-recent-searches
  - autocomplete-plugin-query-suggestions
  - autocomplete-plugin-algolia-insights
  - autocomplete-plugin-tags
  - autocomplete-plugin-redirect-url

## [Detached mode](https://www.algolia.com/doc/ui-libraries/autocomplete/core-concepts/detached-mode/)

- Autocomplete Detached aims at reproducing native experiences on the device you’re using. 
  - It doesn’t display a native input with results in a dropdown, but a search button with results in a modal. 
  - This allows a more immersive experience where the full viewport is used to display results.

- Autocomplete’s default behavior enables Detached mode when the screen is below 500 pixels wide.

## tutorials

- The most common autocomplete UX is one that displays a list of suggested searches that your users can select from as they type. 
  - Algolia provides a **Query Suggestions feature** that generates suggested search terms based on your what your users are searching for and the results within your dataset.
- Query Suggestions are different from search results. '
  - Query Suggestions are only suggestions of better queries.
- If you don’t have a Query Suggestions index yet, follow the guide on creating a Query Suggestions index.


- [Create a rich text box with Autocomplete](https://www.algolia.com/doc/ui-libraries/autocomplete/solutions/rich-text-box-with-mentions-and-hashtags/)
  - Unlike most autocomplete experiences, the Twitter compose box doesn’t process a query from a search input. 
  - Instead, it parses the content of a text box and detects when the user is trying to mention someone.
  - To replicate such an experience, you need full control over how to render the text box, meaning you must use autocomplete-core instead of autocomplete-js.
  - You only want to start searching when you’re writing or editing a mention. 
  - To do so, you need to tokenize the query and find what token is currently being edited.
  - `getActiveToken` function takes input text and a cursor position and determines, based on where the cursor is, what’s the active token.
  - To do so, it splits the input text into tokens (based on space and newlines), each containing the word and the range it covers, then returns the active token based on the cursor position.





- [Create a multi-column layout with Autocomplete](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/creating-a-multi-column-layout/)
  - Using the `render` function option of autocomplete-js, you can customize the panel rendering to create two columns or more.



- 
- 
- 
- 
- 

# codebase

# more
