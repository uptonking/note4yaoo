---
title: docs-web-css-selector
tags: [css, docs, web]
created: '2020-07-25T12:20:19.299Z'
modified: '2020-07-25T12:20:37.613Z'
---

# docs-web-css-selector

# CSS Specificity

- The following list of selector types increases by specificity:
  - Type selectors (e.g., h1) and pseudo-elements (e.g., ::before).
  - Class selectors (e.g., .example), attributes selectors (e.g., [type="radio"]) and pseudo-classes (e.g., :hover).
  - ID selectors (e.g., #example).
- Universal selector (*), combinators (+, >, ~, ' ', ||) and negation pseudo-class (:not()) have no effect on specificity. 
  - (The selectors declared inside :not() do, however.)
- Inline styles added to an element (e.g. `style="font-weight: bold;"`) always overwrite any styles in external stylesheets, 
  - and thus can be thought of as having the highest specificity.

- Specificity is the means by which browsers decide which CSS property values are the most relevant to an element and, therefore, will be applied. 

- The matches-any pseudo-class `:is()`  and the negation pseudo-class `:not()` are not considered a pseudo-class in the specificity calculation. 
  - But selectors placed into the pseudo-class count as normal selectors when determining the count of selector types.

- Specificity is based on the form of a selector. 
  - In the following case, the selector `*[id="foo"]` counts as an attribute selector for the purpose of determining the selector's specificity, even though it selects an ID.

- Styles for a directly targeted element will always take precedence over inherited styles, regardless of the specificity of the inherited rule. 

- [Does the :not pseudo class increase the specificity of a selector?](https://stackoverflow.com/questions/35038546)
  - The specificity of the `:not` pseudo class is the specificity of its argument. 
    - The `:not()` pseudo class does not add to the selector specificity, unlike other pseudo-classes.
    - So the specificity of .red:not(.blue) is equal to that of .red.blue — 2 class selectors

# `:root`

- The `:root` CSS pseudo-class matches the root element of a tree representing the document. 
- In HTML `:root` represents the `<html>` element and is identical to the selector `html`, except that its specificity is higher.

- The `:root` selector allows you to target the highest-level “parent” element in the DOM, or document tree. 
  - css3才引入
  - since CSS is a styling language that can be used with other document formats, such as SVG and XML, the `:root` pseudo-class can refer to different elements in those cases. 
    - Regardless of the markup language, `:root` will always select the document’s top-most element in the document tree.
- While the :`root` selector and `html` selector both target the same HTML elements, it may be useful to know that `:root` actually has a higher specificity. 
  - Pseudo-class selectors (but not pseudo-elements) have a specificity equal to that of a class, which is higher than a basic element selector.

- [What is the benefit of using :root CSS selector instead of html CSS selector?](https://stackoverflow.com/questions/61409490)
  - The only benefit I found is that a CSS variable set in `:root` can also be used to style SVG graphics. Is it the only benefit?
  - Remember that CSS is also designed to be compatible with more than just HTML and SVG, 
    - it's also designed to be compatible with XML, and with XML the root element might share the same element-name as a child-element 
    - so this is a way to work with those kinds of documents because CSS offers no other way of selecting only the root element for styling, 
    - so it's in the same family as `:first-child, :first-of-type, :last-of-type`, etc.
  - I'll add there's also the risk that a malformed HTML document might have an illegal `<html>` element located elsewhere in the DOM. 
    - If you use just `html` as a selector then those additional `<html>` elements will also be styled
    - Changing it to `html:root { ... }` fixes that.

# [pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)

``` CSS
selector::pseudo-element {
  property: value;
}
```

- pseudo-elements can be used to style a specific part of an element.
- a pseudo-element selector applies styles to parts of your document content in scenarios where there isn't a specific HTML element to select.
- A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s). 
- You can use only one pseudo-element in a selector. 
  - It must appear after the simple selectors in the statement.

- 伪元素常用
- `::after/before/first-letter/first-line/marker/part/selection/...`

# [pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

``` CSS
selector:pseudo-class {
  property: value;
}
```

- pseudo-classes can be used to style an element based on its state.
- a pseudo-class selector targets elements depending on their state rather than on information from the document tree.
- A CSS pseudo-class is a keyword added to a selector that specifies a special state of the selected element(s). 
- Pseudo-classes let you apply a style to an element not only in relation to the content of the document tree, but also in relation to external factors like 
  - the history of the navigator (:visited, for example), 
  - the status of its content (like :checked on certain form elements), 
  - or the position of the mouse (like :hover)

- 伪类类别
  - Linguistic pseudo-classes
    - :lang/dir
  - Location pseudo-classes
    - :visited/link/target/scope
  - User action pseudo-classes
    - :hover/active/focus
  - Time-dimensional pseudo-classes
    - :current/past/future
  - Resource state pseudo-classes
    - :playing/paused
  - The input pseudo-classes
    - :enabled/disabled/read-only/read-write/placeholder-shown
    - :default/checked/interminate/blank/valid/invalid
    - :in-range/out-of-range/required/optional/user-invalid
  - Tree-structural pseudo-classes
    - :root/empty/nth-child/first-child/only-child/nth-of-type

- Like regular classes, you can chain together as many pseudo-classes as you want in a selector.

# `:first-of-type` pseudo-class 

- represents the first element of its type among a group of sibling elements.
- `article :first-of-type { background-color: pink; }`
- `article *:first-of-type { background-color: pink; }`
  - This example shows how nested elements can also be targeted. 
  - Note that the universal selector ( `*` ) is implied when no simple selector is written.
  - 会修改所有不同类型元素的第一个元素的样式

# `::before` pseudo-elements

- In CSS,  `::before` creates a pseudo-element that is the first child of the selected element. 
- It is often used to add cosmetic(表面的) content to an element with the `content` property. 
- **It is inline by default**.
- The pseudo-elements generated by `::before` and `::after` are contained by the element's formatting box, and thus don't apply to replaced elements such as `<img>` , or to `<br>` elements.

# `:nth-child()`

- The `:nth-child()` CSS pseudo-class matches elements based on their position in a group of siblings.

``` CSS
/* Selects the second <li> element in a list */
li:nth-child(2) {
  color: lime;
}

/* Selects every fourth element among any group of siblings */
:nth-child(4n) {
  color: lime;
}

/* select the odd rows of an HTML table: 1, 3, 5, etc.*/
tr:nth-child(odd) or tr:nth-child(2n+1)
```
