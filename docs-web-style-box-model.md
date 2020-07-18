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

- line-height vertical center
  - sometimes it doesn't work
    - Depends on the line-height of the font itself. 
    - Sone font have more blank pace under so it seems not aligned.

- line-hight vs height
  - `height` is the vertical measurement of the container.
  - `line-height` is the distance from the top of the first line of text to the top of the second.
  - Assuming the text is smaller than the container:
    - Setting the `line-height` on the container specifies the minimum height of line-boxes inside it. For 1 line of text, this results in the text vertically centered inside the container.
    - If you set height on the container then the container will grow vertically, but the text inside it will start on the first (top) line inside it.
  - If you wrap the text in a div, give the div a height, and the text grows to be 2 lines (perhaps because it is being viewed on a small screen like a phone) 
    - then the text will overlap with the elements below it. 
    - On the other hand, if you give the div a line-height and the text grows to 2 lines, the div will expand (assuming you don't also give the div a height).
- 为什么 `<li>` 标签内部一张图片下方会存在 4px 的空白？即使不换行，不存在空白节点的情况下也有 4px 的空白
  - 在块级元素内部的行内元素后存在一个空白节点，由于vertical-align默认值为baseline，图片下边缘就会与该空白节点的文字下边缘的位置对齐，下方就会产生空隙
- 字号、栏宽等因素一致的情况下，相比西文，中文通常需要更大的行高数值。
  - 字号、栏宽等因素一致的情况下，相比西文，中文通常需要更大的行高数值
  - 对于典型的以小写字母为主的西文，行内主体视觉高度是 x-height（尽管有上升与下降的笔画以及大写字母）；而汉字接近 em box。因而在同等字号与同等行高设置时，西文的行间空白天生较多。
- 基线位置是由字体确定的，css的line-height指的是一行字的高度，包含了字间距，实际上就是下一行的基线到上一行的基线距离
- 行高line-height实际上只影响行内元素和其他行内内容，而不会直接影响块级元素，也可以为一个块级元素设置line-height，但这个值只是应用到块级元素的内联内容时才会有影响。在块级元素上声明line-height会为该块级元素的内容设置一个最小行框高度。
- ref
  - [height vs line-height styling](https://stackoverflow.com/questions/7616618/height-vs-line-height-styling)
  - [height 属性与 line-height 属性有什么区别](https://www.zhihu.com/question/20222907)
  - [line-height和vertical-align采坑记](https://zhuanlan.zhihu.com/p/51189193)

## text-align

## vertical-align

- vertical-align 指定了每个行内框的垂直对齐方式；
- baseline（默认值）：使元素的基线与父元素的基线对齐。HTML规范没有详细说明部分可替换元素的基线，如textarea ，这意味着这些元素使用此值的表现因浏览器而异。
- sub：使元素的基线与父元素的下标基线对齐。
- super: 使元素的基线与父元素的上标基线对齐。
- text-top：使元素的顶部与父元素的字体顶部对齐。
- text-bottom：使元素的底部与父元素的字体底部对齐。
- middle：使元素的中部与父元素的基线加上父元素- - x-height的一半对齐。
- length：使元素的基线对齐到父元素的基线之上的给定长度。可以是负数。
- percentage：使元素的基线对齐到父元素的基线之上的给定百分比，该百分比是line-height属性的百分比（基友关系暴露）。可以是负数。
- top：使元素及其后代元素的顶部与整行的顶部对齐。
- bottom：使元素及其后代元素的底部与整行的底部对齐。
- 没有基线的元素，使用外边距的下边缘替代，
  - 且vertical-align只对行内元素、表格单元格元素生效，不能用它垂直对齐块级元素
