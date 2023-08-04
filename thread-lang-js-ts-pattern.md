---
title: thread-lang-js-ts-pattern
tags: [js, pattern, architecture]
created: 2023-08-04T18:28:05.397Z
modified: 2023-08-04T18:28:26.530Z
---

# thread-lang-js-ts-pattern

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

## 💡 [Which has better performance in JavaScript: a switch or a lookup table?](https://twitter.com/kadikraman/status/1680886385010528256)

- 待确认: You can speed up the lookup access, by checking if it's a property first by using `name in obj`

- I would hope the switch stmt given the compiler knows the choices will never change. Even if you moved the object creation out of the loop.

- The magic of JS, they probably optimize for switch because of the high usage compare to lookup. Note that a lookup has an upfront init cost which makes it useless on small datasets. Bottom line, a constant (0(1)) vs O(n) is a no-brainer.

- ## Goal: Allow the user to select items in a list.
- https://twitter.com/housecor/status/1668946224198680578
  - Three state approaches, from worst, to best:
  - 1. list and selectedList 👎
  - 2. list and selectedIds 👎
  - 3. list with a selected property 👍
  - Principle: Store related data in one array. This simplifies and avoids out-of-sync bugs.
  - I should have added a 4th option: Store the selected ids in an "map" object. This is a fine option too. The map makes it efficient to check if a given record is selected.

- Adding a "selected" field to the User model kind of breaks seperation of concerns. Like beeing selected is not an attribute of a User but knowing which items are selected is an attribute of the list.
So IMO option two is the cleanest - but as alwas there is no right or wrong here

- i have a strong preference for lookup maps
