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
  - 扩展性强，支持plugins、注册components、自定义view

- cons
  - 不支持多实例

- api设计
  - 大多数组件都是 dom-container + data/source + view/templates/vdom + options，包括react
  - where to render
  - what to render
  - how to render

- autocomplate vs dropdown 区别
  - autocomplate是支持搜索的dropdown
# roadmap
- keyboard
  - tab autocomplete

- view
  - searchbox input uses vdom

- pref
  - 分析runReactives，memo计算过多的reactive
# dev

# examples

- https://github.com/typesense/typesense-autocomplete-demo
  - This is a demo that shows you how to build an autocomplete search interface using Algolia's autocomplete-js library and Typesense.
  - autocomplete.js is a standalone UI library and is unrelated to the Autocomplete widget in the Instantsearch.js UI library
- https://github.com/typesense/typesense-instantsearch-adapter
  - An adapter to use the awesome Instantsearch.js library with a Typesense Search Server, to build rich search interfaces.
  - If your search interface is built on a custom autocomplete component, or is based on @algolia/autocomplete-js, then you don't need this adapter to use it with Typesense, as typesense-js library already supports client-side fetching data from any async data sources.

- https://github.com/kalkafox/cargo-search
  - A simple web page using Algolia's Autocomplete to query cargo dependencies on the fly.


# codebase
- 自定义轻量视图渲染层
  - reactive定义可变值，runReactives批量更新
  - runEffect注册并立即执行effect fn，runEffects执行注册过的fn
  - 每次dispatch(action)，都会执行onStateChange，触发scheduleRender，renderSearchBox + renderPanel

- 自定义渲染层的问题
  - runEffects时每个fn都会执行，很可能过度执行，缺少类似onMount的一次性执行选项
  - onStateChangeRef每次state更新都会触发全量rerender，为了提高性能使用了debounce，基于setTimeout(render, 0)
  - effect是在函数执行过程中同步执行的

## architecture

- init
  - containerElement.appendChild(dom.value.root); 
  - runEffect > scheduleRender
    - renderSearchBox
    - renderPanel

- update
  - runEffect
  - scheduleRender(lastStateRef.current); 
  - api暴露的setQuery等store.dispatch(actions)，都会更新store更新+rerender

## model-layer

- redux-like store
  - every `store.dispatch` will trigger `props.onStateChange`, to update view

```typescript
export interface AutocompleteState<TItem extends BaseItem> {
  activeItemId: number | null;
  /** the search input value */
  query: string;
  /** the completed version of the query */
  completion: string | null;
  /** the autocomplete’s collections of items */
  collections: Array<AutocompleteCollection<TItem>>;
  /** whether the autocomplete display panel is open or not */
  isOpen: boolean;
  /** the autocomplete network status. useful to display UI hints when the network is unstable */
  status: 'idle' | 'loading' | 'stalled' | 'error';
  /** the global context passed to lifecycle hooks
   */
  context: AutocompleteContext;
}
```

## view-layer

- 视图层无状态，只是store某一时刻的展示

- searchbox input is created using dom
- dropdown panel is created using vdom
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
- [Autocomplete or InstantSearch.js?](https://www.algolia.com/doc/guides/building-search-ui/ui-and-ux-patterns/autocomplete/js/)
  - autocomplete doesn’t have explicit UI for filters or pagination
  - That’s where InstantSearch.js comes in. It provides a rich library of widgets to further refine your search.

- InstantSearch ships with a searchBox component, but it doesn’t provide autocomplete features like you see on YouTube and Amazon. 
  - Instead, you can replace the searchBox with an autocomplete experience, using Autocomplete.

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

- [feat(js): change renderer implementation to virtual DOM_202101](https://github.com/algolia/autocomplete/pull/381)
  - Here's a list of the problems we have with the current DOM implementation:
  - Performance. 
    - Until now, we relied solely on DOM manipulation to re-render the panel on each state change 
    - (note: a state change also happens on an item hover because the item becomes active).
  - Scrolling. 
    - Since hovering an item triggers a state change, we had UI flashes when the dropdown had a scroll bar because we used to reset the whole panel. This made advanced panel rendering impossible to use.
  - Plugins. 
    - The rendering of our plugins was coupled with the DOM and we couldn't leverage users' framework preference.

- [feat(autocomplete-js): enable HTML templating_v1.6_202203](https://github.com/algolia/autocomplete/pull/920)
  - Templates now expose an `html` function. This generates a virtual node tree (just like JSX or createElement) 
  - One benefit over classic HTML templates injected in a container is that these templates accept inline event handlers (e.g., onClick), just like JSX. It facilitates interactivity and garbage collection of event handlers in many situations.

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

- [Highlighting in InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/ui-and-ux-patterns/highlighting-snippeting/js/)
  - https://instantsearchjs.netlify.app/stories/react/?path=/story/highlight--default
- Highlighting is a vital tool for showing searchers why a result matched their query by **providing different styling to all matched query words**.
  - By default, Highlighting is enabled on all searchableAttributes

- [snippet](https://www.algolia.com/doc/api-reference/widgets/snippet/js/)
  - https://instantsearchjs.netlify.app/stories/react/?path=/story/snippet--default
- Snippeting returns parts of the matched attribute, namely, the matched words and some words around them. 
  - Unlike highlighting, you must enable snippeting for each attribute you wish to snippet, although you can set the value * to snippet all attributes.
  - The snippetted result wraps the matched words in the pre-highlighting and post-highlighting tags.
- The snippet function returns attributes in your search results in a shorter form (a snippet). Snippetted attributes are also highlighted.

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
# more

# issues

- [Is there a way to configure the triggering character? Currently colon, hash sign, 'at' char triggers suggestion popup to appear](https://github.com/algolia/autocomplete/issues/266)
  - [Create a rich text box with Autocomplete](https://www.algolia.com/doc/ui-libraries/autocomplete/solutions/rich-text-box-with-mentions-and-hashtags/)
  - https://github.com/algolia/autocomplete/tree/next/examples/twitter-compose-with-typeahead

- [Confusing interactions around linked autocomplete items and client-side routing](https://github.com/algolia/autocomplete/discussions/629)
  - I'm finding it hard to see when it'd make sense to have items behave like links when using the keyboard, but not onClick
  - Having the keyboard navigator separated from click events is a design decision that we took to keep the click navigation accessible: opening the link on click, and respecting browser's events on modifier clicks (Ctrl, Cmd, Shift)

- [fix(autocomplete-js): display warning when there are more than one instances of autocomplete](https://github.com/algolia/autocomplete/pull/1108)
  - While autocomplate can technically render multiple instances in the same document, in practice it results in inconsistent behavior when a user interacts with them.
  - This is because we currently bind pointer events on `Window` to determine whether a panel should be closed after a user clicks outside of it. This only works for one of the autocomplete added to the document.
# discuss
- ## [instantsearch.js without Algolia possible?](https://github.com/algolia/instantsearch/issues/2205)

- There are a few libraries which will help you achieve this:
  - https://github.com/meilisearch/instant-meilisearch
  - https://github.com/typesense/typesense-instantsearch-adapter

- You can now use the new option `searchClient` to be able to plug a custom client

- We don't actually lock-in the usage of InstantSearch.js to Algolia, per se (it's open source after all smile). As you mentionned there are two cases:
  - doing actual searches with another "engine": this is tricky because of the options that are required. I would say that implementing an Algolia like REST endpoint would be easier in this case (but still difficult). In this case, createAlgoliaAgent should be used to redirect the endpoints to your server.
  - mocking / caching for offline: that's seems feasible and yes the client is a perfect target for that. You only have to implement addAlgoliaAgent and search methods of the client.
