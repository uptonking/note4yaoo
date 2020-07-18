---
title: docs-web-style-layout
tags: [docs, layout, web]
favorited: true
created: '2020-07-17T09:46:19.722Z'
modified: '2020-07-18T09:32:06.258Z'
---

# docs-web-style-layout

## display

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
