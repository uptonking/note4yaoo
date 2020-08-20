---
title: page-css-box-model
tags: [box-model, css]
created: '2020-08-20T12:55:24.017Z'
modified: '2020-08-20T12:57:07.524Z'
---

# page-css-box-model

## [* { Box-sizing: Border-box } FTW](https://www.paulirish.com/2012/box-sizing-border-box-ftw/)

- I have a recommendation for your CSS going forward:

``` CSS
/* apply a natural box layout model to all elements, but allowing components to change */
html {
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: inherit;
}
```

- This gives you the box model you want. Applies it to all elements. 
- Turns out many browsers already use `border-box` for a lot of form elements (which is why inputs and textareas look diff at `width:100%;` ) 
- But applying this to all elements is safe and wise.
- A number of projects use this layout model by default, including the WebKit Web Inspector (aka Chrome DevTools).

- You might get up in arms about the universal `*` selector.
  - It can be slow when you specifically use it like `.foo > *` , so don’t do that. 
  - Aside from that, you are not allowed to care about the performance of `*` unless you concatenate all your javascript, have it at the bottom, minify your css and js, gzip all your assets, and losslessly compress all your images.

## [* { box-sizing: border-box } explained](https://www.abeautifulsite.net/box-sizing-border-box-explained)

- The `border-box` trick effectively changes the way dimensions are measured for every element so it includes borders and padding.
- Think of it as a box model reset that will make you enjoy writing CSS. 
- It's a tried and tested method that works all the way back to IE8, and is used in popular frameworks such as Bootstrap. There are no performance issues
- I've noticed this a few times before. If you're using a third party plugin whose styles rely on the `content-box` model, things might look a bit strange. 
- To fix this, you can create an override class or apply the following styles directly to a parent element of the plugin

``` CSS
.content-box,
.content-box * {
  box-sizing: content-box;
}
```

## ref

- [Inheriting box-sizing Probably Slightly Better Best-Practice](https://css-tricks.com/inheriting-box-sizing-probably-slightly-better-best-practice/)
