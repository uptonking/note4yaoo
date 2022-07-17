---
title: note-react-community-choices
tags: [alternatives, community, react]
created: 2021-07-27T10:03:39.430Z
modified: 2021-07-27T10:04:07.244Z
---

# note-react-community-choices

# discuss-stars

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## use-context-selector: [v2] new API and new implementation with useMutableSource
- https://github.com/dai-shi/use-context-selector/pull/12
- v2 implementation doesn't rely on context propagation, but use `useMutableSource` for updating components "selectively".
- I'm giving up on passing 02_tearing_spec in v2, because I don't want to use the undocumented `calculateChangedBits` in v2. 
  - Unfortunately, useMutableSource will not be able to solve this spec (which is not in their goal). I'd leave it as a limitation.

- [@fluentui/react-context-selector](https://github.com/microsoft/fluentui/tree/master/packages/react-context-selector)
  - React context by nature triggers propagation of component re-rendering if a value is changed. 
  - To avoid this, this library uses undocumented feature of `calculateChangedBits`. 
  - It then uses a subscription model to force update when a component needs to re-render.


- https://github.com/edriang/use-context-selection
  - This library was inspired by use-context-selector, but here are some key differences
  - Internally, use-context-selection manages different set of listeners per Context, while use-context-selector stores all listeners (even for different Contexts) within a single shared Set.

- ## Do you still prefer #react-intl nowadays?__201903
- https://twitter.com/adrirai/status/1106906500054859776
- No, maintenance on it has dropped off. A PR to update to new React context API has been open since September 2018. Maintainers have become unresponsive. Would avoid using react-intl for new projects.
  - There has been some renewed support recently. React context API and useIntl added in the v3 beta.
- seems not actively maintained anymore and has no native support for hooks
- react-i18next. Great ecosystem. Great docs. Easy to implement, flexible, good server side support.
