---
title: page-cssom-blog
tags: [cssom, style]
created: '2020-08-08T17:40:23.318Z'
modified: '2020-08-08T17:40:43.088Z'
---

# page-cssom-blog

## cssom

### [Working with the new CSS Typed Object Model_201803](https://developers.google.com/web/updates/2018/03/cssom)

- TLDR: CSS now has a proper object-based API for working with values in JavaScript

``` JS
el.attributeStyleMap.set('padding', CSS.px(42));
const padding = el.attributeStyleMap.get('padding');
console.log(padding.value, padding.unit); // 42, 'px'
```

- The days of concatenating strings and subtle bugs are over!
  - Chrome 66 adds support for the CSS Typed Object Model for a subset of CSS properties.

- CSS has had an old object model (CSSOM) for many years. 
  - In fact, any time you read/set `element.style` in JavaScript you're using it

``` JS
// Element styles.
el.style.opacity = 0.3;
typeof el.style.opacity === 'string' // Ugh. A string!?

// Stylesheet rules.
document.styleSheets[0].cssRules[0].style.opacity = 0.3;
```

- The new CSS Typed Object Model (Typed OM), part of the Houdini effort, expands this worldview by adding types, methods, and a proper object model to CSS values. 
  - Instead of strings, values are exposed as JavaScript objects to facilitate performant (and sensible) manipulation of CSS.
  - you'll be accessing styles through a new `.attributeStyleMap` property for elements and a .`styleMap` property for stylesheet rules. 
    - Both return a `StylePropertyMap` object.
    - `StylePropertyMap`s are Map-like objects, they support all the usual suspects (get/set/keys/values/entries), so flexible

``` JS
// Element styles.
el.attributeStyleMap.set('opacity', 0.3);
typeof el.attributeStyleMap.get('opacity').value === 'number' // Yay, a number!

// Stylesheet rules.
const stylesheet = document.styleSheets[0];
stylesheet.cssRules[0].styleMap.set('background', 'blue');
```

- So what problems is CSS Typed OM trying to solve? 
  - you might argue that CSS Typed OM is far more verbose than the old object model. 
- typed om key features
  - Fewer bugs.
  - Arithmetic operations & unit conversion.
  - Value clamping & rounding
  - Better performance
    - The browser has to do less work serializing and deserializing string values. 
    - Now, the engine uses a similar understanding of CSS values across JS and C++.
  - Error handling.
  - no more guessing if names are camel-cased or strings
    - CSS property names in Typed OM are always strings, matching what you actually write in CSS

- CSS `var()` become a `CSSVariableReferenceValue` object in the Typed OM. 
  - Their values get parsed into `CSSUnparsedValue` because they can take any type (px, %, em, rgba(), etc).

- Conclusion
  - It's nice to finally have an updated object model for CSS. 
  - Working with strings never felt right to me. 
  - The CSS Typed OM API is a bit verbose, 
  - but hopefully it results in fewer bugs and more performant code down the line.

### [mdn: Determining the dimensions of elements](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)

- There are several properties you can look at in order to determine the width and height of elements, 
  - and it can be tricky to determine which is the right one for your needs.
  - Note that all these properties are read-only. 
  - If you want to set the width and height of an element, use width and height or the overriding min-width and max-width, and min-height and max-height properties.
- How much room does it use up?
  - offsetWidth/Height
- What's the size of the displayed content?
  - clientWidth/height
- How big is the content?
  - scrollWidth/Height

### [mdn: Using dynamic styling information](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Using_dynamic_styling_information)

- The CSS Object Model (CSSOM), part of the DOM, exposes specific interfaces allowing manipulation of a wide amount of information regarding CSS. 
- In many cases, and where possible, it really is best practice to dynamically manipulate classes via the `className` property since the ultimate appearance of all of the styling hooks can be controlled in a single stylesheet.
- Note also that, as with individual element's DOM styles, when speaking of manipulating the stylesheets, this is not actually manipulating the physical document(s), but merely the internal representation of the document.
- The basic `style` object exposes the `Stylesheet` and the `CSSStylesheet` interfaces. 
- Those interfaces contain members like `insertRule/selectorText/parentStyleSheet` for accessing and manipulating the individual style rules that make up a CSS stylesheet.
- To get to the `style` objects from the `document` , you can use the `document.styleSheets` property and access the individual objects by index (e.g. `document.styleSheets[0]` is the first stylesheet defined for the `document` , etc.).

``` JS
var stylesheet = document.styleSheets[0];
stylesheet.cssRules[0].style.backgroundColor = "blue";
```

- The element style property (see also the section "DOM Style Object" below) can also be used to get and set the styles on an element. However, this property only returns style attributes that have been set in-line (e.g <td style="background-color: lightblue">` returns the string `"background-color:lightblue"` , or directly for that element using `element.style.propertyName` , even though there may be other styles on the element from a stylesheet).

- The `style` object represents an individual style statement. Unlike the individual rules available from the `document.styleSheets collection` , the `style` object is accessed from the `document` or from the elements to which that style is applied. It represents the in-line styles on a particular element.
- Note that you can also change style of an element by getting a reference to it and then use its `setAttribute` method to specify the CSS property and its value.
- However,  `setAttribute` removes all other style properties that may already have been defined in the element's `style` object

### [Constructable Stylesheets: seamless reusable styles](https://developers.google.com/web/updates/2019/02/constructable-stylesheets)

- As of October 2019, Constructable Stylesheets are only available in Chrome (versions 73 and higher).
- It has always been possible to create stylesheets using JavaScript. 
- However, the process has historically been to create a `<style>` element using `document.createElement('style')` , and then access its sheet property to obtain a reference to the underlying `CSSStyleSheet` instance. 
- This method can produce duplicate CSS code and its attendant bloat, and the act of attaching leads to a flash of unstyled content whether there is bloat or not. 
- The `CSSStyleSheet` interface is the root of a collection of CSS representation interfaces referred to as the `CSSOM` , offering a programmatic way to manipulate stylesheets as well as eliminating the problems associated with the old method.
- Constructable Stylesheets make it possible to define and prepare shared CSS styles, and then apply those styles to multiple Shadow Roots or the Document easily and without duplication. 
- Updates to a shared CSSStyleSheet are applied to all roots into which it has been adopted, and adopting a stylesheet is fast and synchronous once the sheet has been loaded.
