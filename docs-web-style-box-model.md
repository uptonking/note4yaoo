---
title: docs-web-style-box-model
tags: [docs, web]
favorited: true
created: '2020-07-18T08:40:00.797Z'
modified: '2020-07-18T08:40:56.062Z'
---

# docs-web-style-box-model


## font-size

- sets the size of the font. 
- Changing the font size also updates the sizes of the font size-relative length units, such as em, ex, and so forth
- A `px` value is static. 
  - This is an OS-independent and cross-browser way of literally telling the browsers to render the letters at exactly the number of pixels in height that you specified. 
- Defining font sizes in `px` is not accessible, 
  - because the user cannot change the font size in some browsers. 
  - For example, users with limited vision may wish to set the font size much larger than the size chosen by a web designer. 
  - Avoid using them for font sizes if you wish to create an inclusive design.
- The size of an `em` value is dynamic. 
  - When defining the f `ont-size` property, an `em` is equal to the font size of the element on which the `em` is used. 
  - If you haven't set the font size anywhere on the page, then it is the browser default, which is often 16px. 
  - So, by default 1em = 16px
- `rem` values were invented in order to sidestep the compounding problem. 
  - `rem` values are relative to the root `html` element, not the parent element. 
  - In other words, it lets you specify a font size in a relative fashion without being affected by the size of the parent, thereby eliminating compounding.
- ref
  - [mdn font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size)

## line-height

- sets the height of a line box. 
- Desktop browsers (including Firefox) use a default value of roughly `1.2` , depending on the element's `font-family` .
- It's commonly used to set the distance between lines of text. 
- On block-level elements, it specifies the minimum height of line boxes within the element. 
- On non-replaced inline elements, it specifies the height that is used to calculate line box height.
- Use a minimum value of 1.5 for line-height for main paragraph content. This will help people experiencing low vision conditions
- If the page is zoomed to increase the text size, using a unitless value ensures that the line height will scale proportionately

- line-hight vs height
  - `height` is the vertical measurement of the container.
  - `line-height` is the distance from the top of the first line of text to the top of the second.
  - Assuming the text is smaller than the container:
    - Setting the `line-height` on the container specifies the minimum height of line-boxes inside it. For 1 line of text, this results in the text vertically centered inside the container.
    - If you set height on the container then the container will grow vertically, but the text inside it will start on the first (top) line inside it.
  - If you wrap the text in a div, give the div a height, and the text grows to be 2 lines (perhaps because it is being viewed on a small screen like a phone) 
    - then the text will overlap with the elements below it. 
    - On the other hand, if you give the div a line-height and the text grows to 2 lines, the div will expand (assuming you don't also give the div a height).
  - ref
    - [height vs line-height styling](https://stackoverflow.com/questions/7616618/height-vs-line-height-styling)

## text-align

## vertical-align
