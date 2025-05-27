---
title: note-react-community-choices
tags: [alternatives, community, react]
created: 2021-07-27T10:03:39.430Z
modified: 2021-07-27T10:04:07.244Z
---

# note-react-community-choices

# discuss-stars

- ## 
# discuss-react-testing
- ## 

- ## 

- ## Never been so happy to see people uninstalling @‍testing-library/react _202504
- https://x.com/kentcdodds/status/1914971189417517382
  - it's incredibly validating that @TestingLib has been so successful that it's been adopted (rewritten natively) by @playwrightweb and @vitest_dev . My work here is done

- Why would you move from using @testing -library/react to vitest-dev-browser or playwright web? I haven’t been following along as I’ve only looked to testing library.
  - Testing in a real browser is always going to be better than a fake one. Playwright has experimental component testing that implements the same fantastic API as RTL. Real browser, same test API.

- When should and when should we not use `@testing -library/react` or vue? I always use it
  - They implemented it themselves. So you're really not moving on from it

- Waiting to start moving toward Vitest and Playwright. In the meantime, thank you SO much for @TestingLib

- Congrats on the validation—incremental wins compound when tools get native adoption. Real-world proof that small steps > big promises. Legacy systems could learn from this layered integration mindset.

- Did you know that migrating from JSDOM to Vitest Browser Mode is a matter of swapping two imports?

- heads up - this doesn't seem to work for tests located inside directories ending with '+'. Files located outside the '+' directories work great though.
  - I tried migrating Epic Stack to VBM but most tests I see there are testing the loader+component collocation. I don't think VBM is a good choice here since it runs everything in the browser. I'm voting for using E2E tests instead.

- ## @TestingLib is now THE testing solution for @reactjs _202404
- https://x.com/kentcdodds/status/1783853885960167795
- [React 19 Upgrade Guide – React](https://react.dev/blog/2024/04/25/react-19-upgrade-guide)
  - We are deprecating react-test-renderer because it implements its own renderer environment that doesn’t match the environment users use, promotes testing implementation details, and relies on introspection of React’s internals.
  - We recommend migrating your tests to `@testing-library/react` or `@testing-library/react-native` for a modern and well supported testing experience.

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
