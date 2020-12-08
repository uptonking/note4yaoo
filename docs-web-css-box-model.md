---
title: docs-web-css-box-model
tags: [css-box-model, docs, web]
created: '2020-07-18T08:40:00.797Z'
modified: '2020-12-08T13:15:23.491Z'
---

# docs-web-css-box-model

## width

## height 

## padding

## margin

- The `margin-right` CSS property sets the margin area on the right side of an element. 
  - A positive value places it farther from its neighbors, while a negative value places it closer.
- initial vaule: 0 
- `margin-right: auto;`
  - The right margin receives a share of the unused horizontal space, as determined mainly by the layout mode that is used. 
  - If the values of margin-left and margin-right are both auto, the calculated space is evenly distributed.

- keyword auto默认是使用所有剩余空间，所以不论left还是right定义了auto，计算值都会是包含块的剩余空间，如果左右都设置了auto，那么就会均分剩余空间

- div没有设置width或height，会自动填充父容器的宽度
- 假设外部的容器宽度大于200，则宽度原本应该自动填充，现在因为width设置200而闲置，而 `margin:auto` 就是为了填充这个闲置的尺寸而设计
- 如果一侧定值，一侧auto，则auto为剩余空间大小
- 如果两侧均是auto，则平分剩余空间

``` HTML
.father {
width:400px;
height: 200px;
background: pink;
}
.son {
width: 200px;
height: 150px;
background: #ff00dd;
margin-left: auto;
}
<div class='father'>
  <div class='son'></div>

</div>
```

- 对于上例，因为son元素margin-right缺省，而自动填充初始值0， `margin-left：auto` 会占据所有空间，所以son元素会在右侧

- ref
  - [margin:auto与布局展示](https://zhuanlan.zhihu.com/p/57605009)

## overflow

- The `overflow` CSS shorthand property sets the desired behavior for an element's overflow — i.e. when an element's content is too big to fit in its block formatting context — in both directions.
- In order for `overflow` to have an effect, the block-level container must have either a set height ( `height` or `max-height` ) or ` white-space` set to `nowrap` .
- Specifying a value other than `visible` (the default) creates a new block formatting context. 
  - This is necessary for technical reasons — if a float intersected with the scrolling element it would forcibly rewrap the content after each scroll step, leading to a slow scrolling experience.
- Setting one axis to `visible` (the default) while setting the other to a different value results in visible behaving as auto.
- The JavaScript `Element.scrollTop` property may be used to scroll an HTML element even when `overflow` is set to `hidden` .

- **values**

``` 
Initial value	visible
Applies to	Block-containers, flex containers, and grid containers
Inherited	no
```

- visible
  - Content is not clipped and may be rendered outside the padding box.
- hidden
  - Content is clipped if necessary to fit the padding box. 
  - No scrollbars are provided, and no support for allowing the user to scroll (such as by dragging or using a scroll wheel) is allowed. 
  - The content can be scrolled programmatically (for example, by setting the value of a property such as offsetLeft), so the element is still a scroll container.
- scroll
  - Content is clipped if necessary to fit the padding box. 
  - Browsers always display scrollbars whether or not any content is actually clipped, preventing scrollbars from appearing or disappearing as content changes. 
  - Printers may still print overflowing content.
- auto
  - Depends on the user agent. 
  - If content fits inside the padding box, it looks the same as `visible` , but still establishes a new block formatting context. 
  - Desktop browsers provide scrollbars if content overflows.
- clip
  - Like for `hidden` , the content is clipped to the element's padding box. 
  - The difference between clip and hidden is that the clip also forbids all scrolling, including programmatic scrolling. 
  - The box is not a scroll container, and does not start a new formatting context. 
  - If you wish to start a new formatting context, you can use display: flow-root to do so.

### [Overflowing content](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Overflowing_content)

- Everything in CSS is a box. You can constrain the size of these boxes by assigning values of width and height (or inline-size and block-size). 
- Overflow happens when there is too much content to fit in a box. 
- Wherever possible, CSS does not hide content. This would cause data loss. 
- Instead, CSS overflows in visible ways. You are more likely to see there is a problem. 便于发现问题
- The default value of `overflow` is `visible` . With this default, we can see content when it overflows.
- If you only want scrollbars to appear when there is more content than can fit in the box, use `overflow: auto` . This allows the browser to determine if it should display scrollbars.
- When developing a site, always keep overflow in mind. 
  - Test designs with large and small amounts of content. 
  - Increase the font sizes of text. Generally ensure that your CSS works in a robust way. 
  - Changing the value of overflow to hide content, or to add scrollbars, is likely to be reserved for a few select use cases. (for example, where you intend to have a scrolling box)

### [CSS Overflow Module](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Overflow)

- There are two types of overflow that you might encounter in CSS.  
- ink overflow. 
  - This is the overflow of painting effects which do not affect layout or otherwise extend the scrollable overflow region, such as box shadows, border images, text decoration, overhanging glyphs, outlines, etc.
- scrollable overflow
  - The overflow that we sometimes need to manage in CSS is described as scrollable overflow. 
  - This is the content appearing outside of the box for which scrolling mechanisms need to be provided. 
  - The overflow properties are how we can control what happens when content overflows a box. 

## border

- The border shorthand CSS property sets an element's border. 
- It sets the values of `border-width` , `border-style` , and `border-color` .

### border-width

- The border-width shorthand CSS property sets the width of an element's border.
- Each side can be set individually using border-top/right/bottom/left-width

- **values**
- initial value each defaults to `medium`
  - 对于table cell，由于border-style默认值为none，所以不显示边框，宽度为0
- `border-top-width` is the absolute length or 0 if `border-top-style` is none or hidden

## border-style

- The border-style shorthand CSS property sets the line style for all four sides of an element's border.

- **values** 不可继承
- initial value each defaults to `none`
  - Unless a `background-image` is set, the computed value of the same side's `border-width` will be `0` , even if the specified value is something else. 
  - In the case of table cell and border collapsing, the `none` value has the **lowest** priority: if any other conflicting border is set, it will be displayed.
  - 对于table cell，默认就不显示边框
- `hidden`
  - Like the `none` keyword, displays no border. 
  - Unless a `background-image` is set, the computed value of the same side's `border-width` will be `0` , even if the specified value is something else. 
  - In the case of table cell and border collapsing, the hidden value has the **highest** priority: if any other conflicting border is set, it won't be displayed.
- dotted, dashed, solid, double
- groove(沟槽), ridge(隆起, 山脊)
  - Displays a border with a carved(雕刻) or extruded(挤压) appearance.
- inset(嵌入物), outset(n, 开始)
  - Displays a border that makes the element appear embedded(嵌入式的), or embossed(有凸起图案的)

## border-color

- The border-color shorthand CSS property sets the color of an element's border.

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
    - Sone font have more blank pace under so it seems not aligned. ??? 待验证，字体到line-height的上下边不是等距???

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

## box-shadow

- The box-shadow CSS property adds shadow effects around an element's frame. 
- You can set multiple effects separated by commas. 
- initial vaule: none

``` CSS
div {
  /* offset-x | offset-y | blur-radius | spread-radius | color */
  box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
}
```

- ref
  - [mdn: online Box-shadow generator](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Background_and_Borders/Box-shadow_generator)
