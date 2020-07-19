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

- **values**
- user's default font size (which is `medium` )
- `<length>`
  - A positive `<length>` value. 
  - For most font-relative units (such as `em` and `ex` ), the font size is relative to the parent element's font size.
  - For font-relative units that are root-based (such as rem), the font size is relative to the size of the font used by the `<html>` (root) element.
- A positive `<percentage>` value, relative to the parent element's font size.

- A `px` value is static. 
  - This is an OS-independent and cross-browser way of literally telling the browsers to render the letters at exactly the number of pixels in height that you specified. 
- Defining font sizes in `px` is not accessible, 
  - because the user cannot change the font size in some browsers. 
  - For example, users with limited vision may wish to set the font size much larger than the size chosen by a web designer. 
  - Avoid using them for font sizes if you wish to create an inclusive design.

- The size of an `em` value is dynamic. 
  - When defining the `font-size` property, an `em` is equal to the font size of the element on which the `em` is used. 
  - If you haven't set the font size anywhere on the page, then it is the browser default, which is often 16px. 
  - So, by default 1em = 16px

- `rem` values were invented in order to sidestep the compounding problem. 
  - `rem` values are relative to the root `html` element, not the parent element. 
  - In other words, it lets you specify a font size in a relative fashion without being affected by the size of the parent, thereby eliminating compounding.

- Chrome从某个版本开始，设置font-size只要小于12px，，都会以12px的大小显示
  - 可以用用 `transform: scale()` ，先以12px的font-size设置文字，根据比例再进行缩小
  - chrome最新版已经可以显示小于12px的字体了
  - Chrome and Firefox now allow a minimum font size setting of zero. Chrome 73 had downstream problems with this, and since then Chrome changed their policy and user interface for this setting
- Say I have a single span element defined as an inline-block. It's only contents is plain text. When the font size is very large, you can clearly see how the browser adds a little padding above and below the text.
  - 字体较大时，能看到字体之上的背景处有空白
  - The browser is not adding any padding. Instead, letters (even uppercase letters) are generally considerably smaller in the vertical direction than the height of the font, not to mention the line height, which is typically by default about 1.2 times the font height (font size).
  - There is no general solution to this because fonts are different. Even for fixed font size, the height of a letter varies by font. And uppercase letters need not have the same height in a font.
  - Practical solutions can be found by experimentation, but they are unavoidably font-dependent. You will need to set the line-height smaller than the font-size. 
  - `line-height: 0.8;`
- ref
  - [mdn font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size)

## line-height

- sets the height of a line box. 
- Desktop browsers (including Firefox) use a default value of roughly `1.2` , depending on the element's `font-family` .
  - normalize.css将html的line-height设置为1.15
- It's commonly used to set the distance between lines of text. 
- On block-level elements, it specifies the minimum height of line boxes within the element. 
- On non-replaced inline elements, it specifies the height that is used to calculate line box height.

- **vaules**
- `<number>` (unitless)
  - The used value is this unitless `<number>` multiplied by the element's own font size. 
  - The computed value is the same as the specified `<number>` . 
  - In most cases, this is the preferred way to set line-height and avoid unexpected results due to inheritance.
- `<length>`
  - The specified `<length>` is used in the calculation of the line box height. 
  - Values given in `em` units may produce unexpected results (see example below).

``` HTML
<div class="box green">
  <h1>Avoid unexpected results by using unitless line-height.</h1>
  length and percentage line-heights have poor inheritance behavior ...
</div>

<div class="box red">
  <h1>Avoid unexpected results by using unitless line-height.</h1>
  length and percentage line-heights have poor inheritance behavior ...
</div>
.green {
line-height: 1.1;
border: solid limegreen;
}

.red {
line-height: 1.1em;
border: solid red;
}

h1 {
font-size: 30px;
}

.box {
width: 18em;
display: inline-block;
vertical-align: top;
font-size: 15px;
}
```

- 上面的示例中，h1元素的line-height都是继承自div
  - 继承自green类number的1.1，然后乘以自己的font-size，得到30
  - 继承自red类length的1.1em，即1.1x15=16.5
  - number仅指定数字时（无单位），实际行距为字号乘以该数字得出的结果。可以理解为一个系数，子元素仅继承该系数，子元素的真正行距是分别与自身元素字号相乘的计算结果。大多数情况下推荐使用
  - 有单位时，子元素继承了父元素计算得出的行距；无单位时继承了系数，子元素会分别计算各自行距（推荐使用）。

- `<percentage>` 实际计算与em类似，100%=1em
  - Relative to the font size of the element itself. 
  - The computed value is this `<percentage>` multiplied by the element's computed font size. 
  - 150%是根据父元素的字体大小计算出行高，并且子元素依然沿用这个计算后的行高

- Use a minimum value of 1.5 for line-height for main paragraph content. This will help people experiencing low vision conditions
- If the page is zoomed to increase the text size, using a unitless value ensures that the line height will scale proportionately

- Height of an inline box, given by line-height
  - An element with `display: inline` generates an inline box:
    - An inline box is one that is both inline-level and whose contents participate in its containing inline formatting context. A non-replaced element with a display value of inline generates an inline box.
  - And `line-height` determines the height of that box:
    - The height of the inline box encloses all glyphs and their half-leading on each side and is thus exactly 'line-height'
- Height of a line box
  - In an inline formatting context, boxes are laid out horizontally, one after the other, beginning at the top of a containing block. 
  - Horizontal margins, borders, and padding are respected between these boxes. 
  - The boxes may be aligned vertically in different ways: their bottoms or tops may be aligned, or the baselines of text within them may be aligned. 
  - The rectangular area that contains the boxes that form a line is called a line box.
  - The height of a line box is determined by the rules given in the section on line height calculations.
  - In case a line box only contains non-replaced inline boxes with the same line-height and vertical-align, those rules say that the height of the line box will be given by line-height.
- Height of the content area of an inline box
  - The height of the content area should be based on the font, but this specification does not specify how.

- line-height vertical center
  - sometimes it doesn't work
    - Depends on the line-height of the font itself. 
    - Sone font have more blank pace under so it seems not aligned. ??? 待验证，字体到line-height的上下边不是等距？

- line-hight vs height
  - `height` is the vertical measurement of the container.
  - `line-height` is the distance from the top of the first line of text to the top of the second.
  - Assuming the text is smaller than the container:
    - Setting the `line-height` on the container specifies the minimum height of line-boxes inside it. For 1 line of text, this results in the text vertically centered inside the container.
    - If you set height on the container then the container will grow vertically, but the text inside it will start on the first (top) line inside it.
  - If you wrap the text in a div, give the div a height, and the text grows to be 2 lines (perhaps because it is being viewed on a small screen like a phone) 
    - then the text will overlap with the elements below it. 
    - On the other hand, if you give the div a line-height and the text grows to 2 lines, the div will expand (assuming you don't also give the div a height).
- 为什么 `<li>` 标签内部一张图片下方会存在4px的空白？即使不换行，不存在空白节点的情况下也有4px的空白
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

## vertical-align

- sets vertical alignment of an inline, inline-block or table-cell box.
- vertical-align property can be used in two contexts:
  - To vertically align an inline element's box inside its containing line box. 
    - For example, it could be used to vertically position an `<img>` in a line of text
  - To vertically align the content of a cell in a table
- vertical-align only applies to inline, inline-block and table-cell elements
  - you can't use it to vertically align block-level elements
- **Parent-relative values**
- These values vertically align the element relative to its parent element
  - baseline
    - Aligns the baseline of the element with the baseline of its parent. 
  - text-top/bottom
    - Aligns the top of the element with the top of the parent element's font.
  - middle
    - Aligns the middle of the element with the baseline plus half the x-height of the parent.
  - sub/super
  - length/percentage
- **Line-relative values**
- These values vertically align the element relative to the entire line
  - top/bottom
    - Aligns the top of the element and its descendants with the top of the entire line.
- For elements that do not have a baseline, the bottom margin edge is used instead.

- vertical-align 指定了每个行内框的垂直对齐方式
  - baseline（默认值）：使元素的基线与父元素的基线对齐。HTML规范没有详细说明部分可替换元素的基线，如textarea，这意味着这些元素使用此值的表现因浏览器而异。
  - sub：使元素的基线与父元素的下标基线对齐。
  - super: 使元素的基线与父元素的上标基线对齐。
  - text-top：使元素的顶部与父元素的字体顶部对齐。
  - text-bottom：使元素的底部与父元素的字体底部对齐。
  - middle：使元素的中部与父元素的基线加上父元素x-height的一半对齐。
  - length：使元素的基线对齐到父元素的基线之上的给定长度。可以是负数。
  - percentage：使元素的基线对齐到父元素的基线之上的给定百分比，该百分比是line-height属性的百分比（基友关系暴露）。可以是负数。
  - top：使元素及其后代元素的顶部与整行的顶部对齐。
  - bottom：使元素及其后代元素的底部与整行的底部对齐。
- 没有基线的元素，使用外边距的下边缘替代，
  - 且vertical-align只对行内元素、表格单元格元素生效，不能用它垂直对齐块级元素
- ref
  - [mdn vertical-align](https://developer.mozilla.org/en-US/docs/Web/CSS/vertical-align)

## text-align

- sets the horizontal alignment of a block element or table-cell box. 
- This means it works like `vertical-align` but in the horizontal direction. 
- The standard-compatible way to center a block itself without centering its inline content is setting the left and right margin to auto, `margin: 0 auto;`
