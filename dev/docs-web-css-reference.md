---
title: docs-web-css-reference
tags: [api, css, docs, web]
created: '2020-07-17T09:40:02.135Z'
modified: '2020-11-13T10:19:20.931Z'
---

# docs-web-css-reference

# guide

- [Common CSS Properties Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference)
  - list of the most common CSS properties with the equivalent of the DOM notation which is usually accessed from JavaScript
  - float > cssFloat
# [scrollbar-gutter](https://developer.mozilla.org/en-US/docs/Web/CSS/scrollbar-gutter)
- 所有浏览器都不支持(202108)

- An element's `scrollbar-gutter` is the **space between the inner border edge and the outer padding edge**, where the browser may display a scrollbar. 
  - If no scrollbar is present, the gutter will be painted as an extension of the padding.
- The browser determines whether classic scrollbars or overlay scrollbars are used:
  - Classic scrollbars are always placed in a gutter, consuming space when present.
  - Overlay scrollbars are placed over the content, not in a gutter, and are usually partially transparent.

- ref
  - [scrollbar-gutter](https://css-tricks.com/almanac/properties/s/scrollbar-gutter/)
# css predefined values

## [initial](https://developer.mozilla.org/en-US/docs/Web/CSS/initial)

- `initial` CSS keyword applies the initial (or default) value of a property to an element. 
  - It can be applied to any CSS property. 
  - ie不支持
- The initial value of a CSS property is its default value, as listed in its definition table in the specification.
- For inherited properties, the initial value is used on the root element only, as long as no specified value is supplied.
- For non-inherited properties, the initial value is used on all elements, as long as no specified value is supplied.

## [inherit](https://developer.mozilla.org/en-US/docs/Web/CSS/inherit)

- `inherit` CSS keyword causes the element for which it is specified to take the computed value of the property from its parent element. 
  - It can be applied to any CSS property
- For inherited properties, this reinforces the default behavior, and is only needed to override another rule. 
- For non-inherited properties, this specifies a behavior that typically makes relatively little sense and you may consider using initial instead, or unset on the all property.
- Inheritance is always from the parent element in the document tree, even when the parent element is not the containing block.

## [unset](https://developer.mozilla.org/en-US/docs/Web/CSS/unset)

- `unset` CSS keyword resets a property to its inherited value if the property naturally inherits from its parent, and to its initial value if not. 
  - In other words, it behaves like the `inherit` keyword in the first case, when the property is an inherited property, and like the `initial` keyword in the second case, when the property is a non-inherited property.
  - unset can be applied to any CSS property, 

## [revert](https://developer.mozilla.org/en-US/docs/Web/CSS/revert)

- `revert` CSS keyword reverts the cascaded value of the property from its current value to the value the property would have had if no changes had been made by the current style origin to the current element. 
  - Thus, it resets the property to its inherited value if it inherits from its parent or to the default value established by the user agent's stylesheet (or by user styles, if any exist).
  - It can be applied to any CSS property
- The `revert` keyword works exactly the same as `unset` in many cases. 
  - The only difference is for properties that have values set by the browser or by custom stylesheets created by users (set on the browser side).
- The `revert` keyword is different from and should not be confused with `initial`, which uses the initial value defined on a per-property basis by the CSS specifications.
  - In contrast, user-agent stylesheets set default values on the basis of CSS selectors.
  - For example, the initial value for the display property is inline, whereas a normal user-agent stylesheet sets the default display value of `<div>`s to `block`, of `<table>`s to `table`, etc.
# color
- The `color` CSS property sets the foreground color value of an element's text and text decorations, and sets the `<currentcolor>` value. 
  - `currentcolor` may be used as an indirect value on other properties and is the default for other color properties, such as border-color.
