---
title: docs-web-style-layout
tags: [docs, layout, web]
favorited: true
created: '2020-07-17T09:46:19.722Z'
modified: '2020-07-18T09:32:06.258Z'
---

# docs-web-style-layout

## display

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

## position

## float

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
