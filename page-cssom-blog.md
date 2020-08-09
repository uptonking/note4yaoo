---
title: page-cssom-blog
tags: [cssom, style]
created: '2020-08-08T17:40:23.318Z'
modified: '2020-08-08T17:40:43.088Z'
---

# page-cssom-blog

## [mdn: Determining the dimensions of elements](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)

- There are several properties you can look at in order to determine the width and height of elements, 
  - and it can be tricky to determine which is the right one for your needs.
  - Note that all these properties are read-only. 
  - If you want to set the width and height of an element, use width and height or the overriding min-width and max-width, and min-height and max-height properties.
- ### How much room does it use up?
- offsetWidth/Height
- ### What's the size of the displayed content?
- clientWidth/height
- ### How big is the content?
- scrollWidth/Height

## [mdn: Using dynamic styling information](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Using_dynamic_styling_information)

- The CSS Object Model (CSSOM), part of the DOM, exposes specific interfaces allowing manipulation of a wide amount of information regarding CSS. 
- In many cases, and where possible, it really is best practice to dynamically manipulate classes via the `className` property since the ultimate appearance of all of the styling hooks can be controlled in a single stylesheet.
- Note also that, as with individual element's DOM styles, when speaking of manipulating the stylesheets, this is not actually manipulating the physical document(s), but merely the internal representation of the document.
- The basic `style` object exposes the `Stylesheet` and the `CSSStylesheet` interfaces. 
- Those interfaces contain members like `insertRule` , `selectorText` , and `parentStyleSheet` for accessing and manipulating the individual style rules that make up a CSS stylesheet.
- To get to the `style` objects from the `document` , you can use the `document.styleSheets` property and access the individual objects by index (e.g., `document.styleSheets[0]` is the first stylesheet defined for the `document` , etc.).

``` JS
var stylesheet = document.styleSheets[0];
stylesheet.cssRules[0].style.backgroundColor = "blue";
```

- The element style property (see also the section "DOM Style Object" below) can also be used to get and set the styles on an element. However, this property only returns style attributes that have been set in-line (e.g, `<td style="background-color: lightblue">` returns the string `"background-color:lightblue"` , or directly for that element using `element.style.propertyName` , even though there may be other styles on the element from a stylesheet).

- The `style` object represents an individual style statement. Unlike the individual rules available from the `document.styleSheets collection` , the `style` object is accessed from the `document` or from the elements to which that style is applied. It represents the in-line styles on a particular element.
- Note that you can also change style of an element by getting a reference to it and then use its `setAttribute` method to specify the CSS property and its value.
- However, `setAttribute` removes all other style properties that may already have been defined in the element's `style` object

## [Constructable Stylesheets: seamless reusable styles](https://developers.google.com/web/updates/2019/02/constructable-stylesheets)

- As of October 2019, Constructable Stylesheets are only available in Chrome (versions 73 and higher).
- It has always been possible to create stylesheets using JavaScript. 
- However, the process has historically been to create a `<style>` element using `document.createElement('style')` , and then access its sheet property to obtain a reference to the underlying `CSSStyleSheet` instance. 
- This method can produce duplicate CSS code and its attendant bloat, and the act of attaching leads to a flash of unstyled content whether there is bloat or not. 
- The `CSSStyleSheet` interface is the root of a collection of CSS representation interfaces referred to as the `CSSOM` , offering a programmatic way to manipulate stylesheets as well as eliminating the problems associated with the old method.
- Constructable Stylesheets make it possible to define and prepare shared CSS styles, and then apply those styles to multiple Shadow Roots or the Document easily and without duplication. 
- Updates to a shared CSSStyleSheet are applied to all roots into which it has been adopted, and adopting a stylesheet is fast and synchronous once the sheet has been loaded.
