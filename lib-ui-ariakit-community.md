---
title: lib-ui-ariakit-community
tags: [ariakit, community]
created: 2023-06-22T05:33:03.466Z
modified: 2023-06-22T05:33:12.658Z
---

# lib-ui-ariakit-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## There's an @​ariakit/core library where most of the code will live._20230430
- https://twitter.com/diegohaz/status/1652542224679288832
  - Right now, it includes component stores, but it will have more component logic in the future.
  - Also, our integration tests are framework-agnostic already

- downshift was such an interesting project by @kentcdodds . 
  - It was my first encounter of a headless UI library that doesn't render HTML but just provide a bunch of props. 
  - I've been lately searching for UI libraries that has a foundation of such headless approach.
  - If the core library provides methods for actions and prop getters for potential elements, the next step would be to build actual components in any frontend framework.
  - Any UI library like that approach?
- @zag_js and/or ark-ui
- @tannerlinsley has a few! Virtualizers, tables, oh my!

- The dream is to get folks building such libraries with `Mitosis` which can be responsible for that adapter layer that changes for each web framework.
  - Interesting. In order for you to support all the frameworks, you've chosen to **write DSL and convert it to JSON**. Not what I had in mind, but it seems like a good idea.

- ember-headless-table is another headless ui library that doesn't render HTML on its own.
Instead, it provides the math, calculations, and props for managing common table features (because no one needs to be re-implementing those every time they switch companies)

## [ariakit RFC: Component stores_202209](https://github.com/ariakit/ariakit/issues/1875)

- https://codesandbox.io/s/ariakit-component-stores-forked-248do5
- The problems
- We can't reuse the state logic outside of React
- Host components render on every state update
- Methods as deps in useEffect, useCallback, etc.
- Component stores
- The store would be implemented with vanilla JS so we can reuse it in other frameworks. 
- The React hook would use the `useSyncExternalStore` hook internally, so we can keep it compatible with concurrent rendering.
- Accessing state inside event handlers without re-rendering
- Computed selectors can be easily achieved in userland

- [ariakit RFC: Support controlled state hooks](https://github.com/ariakit/ariakit/issues/487)
- another proposal will be fully possible in Reakit v3: a single parameter that can receive both uncontrolled and controlled state.
- `const state = useDialogState({ initialVisible: false })`; 
- `const state = useDialogState({ visible, setVisible })`; 

### [Framework-agnostic architecture for examples](https://github.com/ariakit/ariakit/issues/1854)

### [Offer Vue components / hooks](https://github.com/ariakit/ariakit/discussions/1723)
