---
title: note-web-css-reset
tags: [css, web]
created: '2020-07-18T06:06:05.107Z'
modified: '2020-07-18T06:07:02.461Z'
---

# note-web-css-reset

## guide

- ref
  - normalize.css  /MIT/39.7kStar/201811
    - https://github.com/necolas/normalize.css
    - http://necolas.github.io/normalize.css/
    - http://nicolasgallagher.com/about-normalize-css/
    - [difference between Normalize.css and Reset CSS](https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css)
    - A modern alternative to CSS resets
    - It makes browsers render all elements more consistently and in line with modern standards. 
    - It precisely targets only the styles that need normalizing
  - minireset.css /MIT/2kStar/201910
    - https://github.com/jgthms/minireset.css
    - https://jgthms.com/minireset.css/
    - A tiny modern CSS reset
    - preserve the inline paddings of button & input
    - reset the font-sizes/block margins/tables
    - set border-box, responsive media elements
  - bootstrap-reboot
    - https://v5.getbootstrap.com/docs/5.0/content/reboot/
    - For improved cross-browser rendering, we use Reboot to correct inconsistencies across browsers and devices while providing slightly more opinionated resets to common HTML elements.
    - Reboot builds upon Normalize, providing many HTML elements with somewhat opinionated styles using only element selectors. 
    - Additional styling is done only with classes. 
    - Update some browser default values to use rems instead of ems for scalable component spacing.
    - Avoid margin-top. 
      - Vertical margins can collapse, yielding unexpected results. 
      - More importantly though, a single direction of margin is a simpler mental model.
    - For easier scaling across device sizes, block elements should use rems for margins.
    - Keep declarations of font-related properties to a minimum, using inherit whenever possible.


## minireset.css 

``` CSS
/*! minireset.css v0.0.6 */
html,
body,
p,
ol,
ul,
li,
dl,
dt,
dd,
blockquote,
figure,
fieldset,
legend,
textarea,
pre,
iframe,
hr,
h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0;
  padding: 0;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-size: 100%;
  font-weight: normal;
}

ul {
  list-style: none;
}

button,
input,
select,
textarea {
  margin: 0;
}

html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

img,
video {
  height: auto;
  max-width: 100%;
}

iframe {
  border: 0;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
}

td,
th {
  padding: 0;
}

td:not([align]),
th:not([align]) {
  text-align: left;
}
```

## normalize.css overview

- 结构
  - document-body
  - text
  - form
  - elements misc
- Normalize.css是保留浏览器的原来样式并且使浏览器显示更一致
  - aims to make built-in browser styling consistent across browsers. 
  - Elements like H1-6 will appear bold, larger in a consistent way across browsers. 
  - You're then supposed to add only the difference in decoration your design needs.
- CSS Reset把浏览器的默认样式都重置了
  - aims to remove all built-in browser styling. 
  - Standard elements like H1-6, p, strong, em, etc. end up looking exactly alike, having no decoration at all. 
  - You're then supposed to add all decoration yourself.
- Normalize.css Extended details and known issues
  - Normally, using `sub` or `sup` affects the line-box height of text in all browsers
  - By default, Chrome on OS X and Safari on OS X allow very limited styling of `select` , unless a border property is set.
  - `[type="checkbox"]`
    - It is recommended that you do not style `checkbox` and `radio` inputs as Firefox's implementation does not respect box-sizing, padding, or width
  - `[type="number"]`
    - Certain font size values applied to number inputs cause the cursor style of the decrement button to change from default to text.
  - `[type="search"]`
    - The search input is not fully stylable by default. 
    - In Chrome and Safari on OSX/iOS you can't control font, padding, border, or background. 
    - In Chrome and Safari on Windows you can't control border properly. 
- Normalize.css is intended only to give all browsers the same starting point in CSS to make development easier. 
  - If most browsers use a default line-height of 1.15, then it should be set to 1.15 here to fix the rest of the browsers to be the same. 
  - Further changes to line-height should be made either in other libraries or your own CSS.
  - 1.15不带单位，只是系数，方便元素自调节

## normalize.css src

``` css
/*! normalize.css v8.0.1 */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 * 浏览器默认line-height大约1.2，还与font-family相关
 */
html {
  line-height: 1.15;
  /* 1 */
  -webkit-text-size-adjust: 100%;
  /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */
body {
  margin: 0;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */
hr {
  box-sizing: content-box;
  /* 1 */
  height: 0;
  /* 1 */
  overflow: visible;
  /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */
pre {
  font-family: monospace, monospace;
  /* 1 */
  font-size: 1em;
  /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */
abbr[title] {
  border-bottom: none;
  /* 1 */
  text-decoration: underline;
  /* 2 */
  text-decoration: underline dotted;
  /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */
b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */
code,
kbd,
samp {
  font-family: monospace, monospace;
  /* 1 */
  font-size: 1em;
  /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */
small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */
/* img {
  border-style: none;
} */

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */
button,
input,
optgroup,
select,
textarea {
  font-family: inherit;
  /* 1 */
  font-size: 100%;
  /* 1 */
  line-height: 1.15;
  /* 1 */
  margin: 0;
  /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */
button,
input {
  /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */
button,
select {
  /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */
button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */
button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */
button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */
fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 * `fieldset` elements in all browsers.
 */
legend {
  box-sizing: border-box;
  /* 1 */
  color: inherit;
  /* 2 */
  display: table;
  /* 1 */
  max-width: 100%;
  /* 1 */
  padding: 0;
  /* 3 */
  white-space: normal;
  /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */
progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */
textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */
[type="checkbox"],
[type="radio"] {
  box-sizing: border-box;
  /* 1 */
  padding: 0;
  /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */
[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */
[type="search"] {
  -webkit-appearance: textfield;
  /* 1 */
  outline-offset: -2px;
  /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */
[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */
::-webkit-file-upload-button {
  -webkit-appearance: button;
  /* 1 */
  font: inherit;
  /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */
details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */
summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */
template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */
[hidden] {
  display: none;
}
```
