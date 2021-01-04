---
title: docs-web-css-layout
tags: [docs, layout, web]
favorited: true
created: '2020-07-17T09:46:19.722Z'
modified: '2020-12-08T13:16:16.666Z'
---

# docs-web-css-layout

# display

- The display CSS property sets whether an element is treated as a block or inline element and the layout used for its children, such as flow layout, grid or flex.
- `display` property sets an element's inner and outer display types. 
  - The outer type sets an element's participation in flow layout. 
  - The inner type sets the layout of children. 
  - Some values of display are fully defined in their own individual specifications; for example the detail of what happens when `display: flex` is declared is defined in the CSS Flexible Box Model specification.

- **values-outer**
  - outer display type, which is essentially its role in flow layout.
- block
  - The element generates a block element box, generating line breaks both before and after the element when in the normal flow.
- inline
  - The element generates one or more inline element boxes that do not generate line breaks before or after themselves. 
  - In normal flow, the next element will be on the same line if there is space
- run-in
  - The element generates a run-in box. 
  - If the adjacent sibling of the element defined as `display: run-in` box is a block box, the `run-in` box becomes the first inline box of the block box that follows it. 
  - Run-in elements act like inlines or blocks, depending on the surrounding elements. 
  - If the run-in box contains a block box, same as block. 
  - If a block box follows the run-in box, the run-in box becomes the first inline box of the block box. 
  - If an inline box follows, the run-in box becomes a block box.
- Note: 
  - Browsers that support the two value syntax, on finding the outer value only, such as when `display: block` or `display: inline` is specified, will set the inner value to `flow` . 
  - This will result in expected behavior; for example if you specify an element to be block, you would expect that the children of that element would participate in block and inline normal flow layout.

- **values-inner**
  - inner display type, which defines the type of formatting context that its contents are laid out in (assuming it is a non-replaced element).
- flow  
  - The element lays out its contents using flow layout (block-and-inline layout).
  - If its outer display type is `inline` or `run-in` , and it is participating in a block or inline formatting context, then it generates an inline box. Otherwise it generates a block container box.
  - Depending on the value of other properties (such as position, float, or overflow) and whether it is itself participating in a block or inline formatting context, it either establishes a new block formatting context (BFC) for its contents or integrates its contents into its parent formatting context.
- flow-root
  - The element generates a block element box that establishes a new block formatting context, defining where the formatting root lies.
- table
  - These elements behave like HTML `<table>` elements. 
  - It defines a block-level box.
- flex
  - The element behaves like a block element and lays out its content according to the flexbox model.
- grid
  - The element behaves like a block element and lays out its content according to the grid model.
- ruby
  - The element behaves like an inline element and lays out its content according to the ruby formatting model. 
  - It behaves like the corresponding HTML `<ruby>` elements.
- Note:
  - Browsers that support the two value syntax, on finding the inner value only, such as when `display: flex` or `display: grid` is specified, will set their outer value to `block` . 
  - This will result in expected behavior; for example if you specify an element to be display: grid, you would expect that the box created on the grid container would be a block level box.

- **values-listitem**
- list-item
  - The element generates a block box for the content and a separate list-item inline box.
  - A single value of list-item will cause the element to behave like a list item. 
  - This can be used together with `list-style-type` and `list-style-position` .

- **values-internal**
  - internal display values for complex internal structure, which only have meaning within that particular layout mode
- table-row-group: like tbody
- table-header-group: like thead
- table-row: like tr
- table-cell: like td
- table-colummn: like col
- ruby-base: like rb

- **values-box**
  - These values define whether an element generates display boxes at all.
- none
  - Turns off the display of an element so that it has no effect on layout 
  - (the document is rendered as though the element did not exist). 
  - All descendant elements also have their display turned off.
- contents
  - These elements don't produce a specific box by themselves. 
  - They are replaced by their pseudo-box and their child boxes. 
  - Please note that the CSS Display Level 3 spec defines how the `contents` value should affect "unusual elements" - elements that aren’t rendered purely by CSS box concepts such as replaced elements. 
  - Due to a bug in browsers this will currently remove the element from the accessibility tree — screen readers will not look at what's inside.

- **values-legacy**
  - CSS 2 used a single-keyword syntax for the display property
- inline-block
  - The element generates a block element box that will be flowed with surrounding content as if it were a single inline box (behaving much like a replaced element would).
  - It is equivalent to `inline flow-root` .
- inline-table
  - It is equivalent to `inline table` .
- inline-flex
  - It is equivalent to `inline flex` .
- inline-grid
  - It is equivalent to `inline grid` .
- Note:
  - The Level 3 specification details two values for the `display` property — enabling the specification of the outer and inner display type explicitly — but this is not yet well-supported by browsers.

- `display：contents`
  - 元素本身不能生成任何盒模型，但是它的子元素或伪元素可以正常生成。
  - 为了盒模型的生成与布局，该元素就好像在DOM树中被子元素与伪元素所替代一样
  - 上述规范说明了我们可以在文档中添加一个HTML元素，并在该元素的选择器中添加 `display:contents` 样式，那么该元素就会像是不存在一样，它的子元素会替代它在DOM树中的位置。
  - 如果为外层Div元素添加display:contents属性，外层Div消失了，我们看不到外层Div的背景和边框，甚至应用到该元素的宽度也已经失效了，内层Div元素则占据了整个视口。
    - 内部Div元素不能继承的属性仅仅是那些与盒模型生成或布局相关的。
    - 我们可以在外层Div元素上设置font-size属性，其子元素则会继承该属性
  - 它能使div不产生任何框，因此不会渲染其背景边框和内边距，但颜色/字体等继承的属性还是会对其子元素产生效果
    - 即在盒子上添加 `display: contents` , 当前盒子若设置了 background border padding width height 等属性会失效

- ref
  - [display：contents 与消失的盒模型](https://www.zcfy.cc/article/vanishing-boxes-with-display-contents-1693.html)

# position

- sets how an element is positioned in a document. 
- The top, right, bottom, and left properties determine the final location of positioned elements.

- **values**
- static 
  - 默认值
  - The element is positioned according to the normal flow of the document. 
  - The top, right, bottom, left, and z-index properties have no effect. 
- relative
  - The element is positioned according to the normal flow of the document, and then offset relative to itself based on the values of top, right, bottom, and left. 
  - The offset does not affect the position of any other elements; thus, the space given for the element in the page layout is the same as if position were static.
  - This value creates a new stacking context when the value of `z-index` is not `auto` . Its effect on table-*-group, table-row, table-column, table-cell, and table-caption elements is undefined.
- absolute
  - The element is removed from the normal document flow, and no space is created for the element in the page layout. 
  - It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block. Its final position is determined by the values of top, right, bottom, and left.
  - This value creates a new stacking context when the value of `z-index` is not `auto` . The margins of absolutely positioned boxes do not collapse with other margins.
  - An element that is absolutely positioned is taken out of the flow; thus, other elements are positioned as if it did not exist. 
  - The absolutely positioned element is positioned relative to its nearest positioned ancestor (i.e., the nearest ancestor that is not static). 
  - If a positioned ancestor doesn't exist, it is positioned relative to the ICB (initial containing block — see also the W3C definition), which is the containing block of the document's root element.
  - If you want an element to remain in its static position (where it would normally be if it were not positioned) but simply take it out of normal flow, simply specifying position: absolute is perfectly acceptable. The behavior is as described in sections 10.3.7 and 10.6.4 of the spec, and every browser behaves correctly.
  - the main purpose of relatively positioning some ancestor of an absolutely-positioned element is for designating its containing block. 
- fixed
  - The element is removed from the normal document flow, and no space is created for the element in the page layout. 
  - It is positioned relative to the initial containing block established by the viewport, except when one of its ancestors has a `transform` , `perspective` , or `filter` property set to something other than `none` (see the CSS Transforms Spec), in which case that ancestor behaves as the containing block.
  - Note that there are browser inconsistencies with perspective and filter contributing to containing block formation.
  - Its final position is determined by the values of top, right, bottom, and left.
  - This value always creates a new stacking context. In printed documents, the element is placed in the same position on every page.
  - This can be used to create a "floating" element that stays in the same position regardless of scrolling. 
- sticky
  - The element is positioned according to the normal flow of the document, and then offset relative to its nearest scrolling ancestor and containing block (nearest block-level ancestor), including table-related elements, based on the values of top, right, bottom, and left. 
  - The offset does not affect the position of any other elements.
  - This value always creates a new stacking context. 
  - Note that a sticky element "sticks" to its nearest ancestor that has a "scrolling mechanism" (created when overflow is hidden, scroll, auto, or overlay), even if that ancestor isn't the nearest actually scrolling ancestor. 
  - This effectively inhibits(阻止) any "sticky" behavior (see the GitHub issue on W3C CSSWG).
  - Sticky positioning can be thought of as a hybrid of relative and fixed positioning. 
  - A stickily positioned element is treated as relatively positioned until it crosses a specified threshold, at which point it is treated as fixed until it reaches the boundary of its parent.
  - A common use for sticky positioning is for the headings in an alphabetized list. 
  - You must specify a threshold with at least one of top, right, bottom, or left for sticky positioning to behave as expected. Otherwise, it will be indistinguishable from relative positioning.

- **A positioned element** is an element whose computed position value is either relative, absolute, fixed, or sticky. 
  - In other words, it's anything except `static` .
- A relatively positioned element is an element whose computed position value is `relative` . 
  - The top/b/left/r properties specify the vertical/horizontal offset from its normal position
- An absolutely positioned element is an element whose computed position value is `absolute` or `fixed` . 
  - The top, right, bottom, and left properties specify offsets from the edges of the element's containing block. (The containing block is the ancestor relative to which the element is positioned.) 
  - If the element has margins, they are added to the offset. 
  - The element establishes a new block formatting context (BFC) for its contents.
- A stickily positioned element is an element whose computed position value is `sticky` . 
  - It's treated as relatively positioned until its containing block crosses a specified threshold (such as setting top to value other than auto) within its flow root (or the container it scrolls within), at which point it is treated as "stuck" until meeting the opposite edge of its containing block.
- Most of the time, absolutely positioned elements that have height and width set to `auto` are sized so as to fit their contents. 
  - However, non-replaced, absolutely positioned elements can be made to fill the available vertical space by specifying both top and bottom and leaving height unspecified (that is, `auto` ). 
  - They can likewise be made to fill the available horizontal space by specifying both left and right and leaving width as auto.

- Scrolling elements containing `fixed` or `sticky` content can cause performance and accessibility issues. 
  - As a user scrolls, the browser must repaint the sticky or fixed content in a new location. 
  - Depending on the content needing to be repainted, the browser performance, and the device's processing speed, the browser may not be able to manage repaints at 60 fps, causing accessibility concerns for people with sensitivities and jank for everyone. 
  - One solution is to add `will-change: transform` to the positioned elements to render the element in its own layer, improving repaint speed and therefore improving performance and accessibility.

- ref
  - [mdn: positon](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

# float

- 容器并没有把浮动的子元素包围起来，俗称塌陷
- 如果父元素只包含浮动元素，且父元素未设置高度和宽度的时候，那么它的高度就会塌缩为零，也就是所谓的**高度塌陷**
  - 此时如果父级元素包含背景或者边框，那么溢出的元素就不像父级元素的一部分
  - 解决方法
    - 浮动父级元素。如果让父级元素浮动，父级元素的高度就会扩大，直到完全包含它里面的浮动元素，虽然这个方法很奇怪，但是很有效。如果选择这种方法，一定要在该元素的下个元素添加 `clear:both` , 确保浮动元素落到父级元素的下方。
    - overflow:hiden
- overlfow-hidden
  - 当父div拥有固定的高度时，如height:500px，可以使用overflow:hidden来隐藏溢出
  - 当父元素的高为height:auto时，我们使用 overflow：hidden 清除浮动
    - 若为div1和div2加上一个属性 `float: left` 后，会发现：背景色为黑色父div消失了，这是因为浮动的元素脱离文档流，不占据空间。不浮动的元素会直接无视掉这个元素，父div无视了自己的两个子div，其高度为0（因为我们没有设置父div的高度），所以父div没有显现。
    - 第一种方法是让父元素也浮动起来，给父div添加 float: right，再给父div设宽度就可见背景色了
    - 第二种方法是给父元素添加 overflow:hidden 属性用以清除浮动
      - 因为overflow可以使父容器形成BFC，BFC可以包含浮动
