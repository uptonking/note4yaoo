---
title: note-web-style-attr
tags: [css, style, web]
created: '2019-10-09T01:32:01.391Z'
modified: '2020-07-14T10:48:18.073Z'
---

# note-web-style-attr

## pieces

- width
  - `width: auto;`
    - initial width of a block level element like div or p is auto. 
    - This makes it expand to occupy all available horizontal space within its containing block. 
    - If it has any horizontal padding or border, the widths of those do not add to the total width of the element.
    - 该元素的margin,border,padding,content**全部都会在父元素之内**，若元素超出父元素，超出部分会隐藏
  - `width: 100%;`
    - if you specify width:100%, the element’s total width will be 100% of its containing block plus any horizontal margin, padding and border (unless you’ve used box-sizing:border-box, in which case only margins are added to the 100% to change how its total width is calculated). This may be what you want, but most likely it isn’t.
    - 该元素content宽度为父元素宽度，该元素可能会超出父元素，超出部分会显示，box-sizing若为content-box，则该元素总宽度还要加上padding+border+margin，若为border-box，则总宽度要加上margin
  - 参考
      - https://stackoverflow.com/questions/17468733/difference-between-width-auto-and-width-100-percent
- border
  - 浏览器默认 border-width: medium, 盒模型默认不显示边框，只是常设为1px
  - div-collapse-border
    - 实现方式有多种
  - css outline vs border
    - 在浏览器里，当鼠标点击或使用Tab键让一个链接或者一个radio获得焦点的时候，该元素将会被一个轮廓虚线框围绕，这个轮廓虚线框就是outline
      - outline能告诉用户那一个可以触发事件的html元素获取了焦点，提示键盘操作
    - border可应用于几乎所有有形的html元素，而outline是针对链接、表单控件和ImageMap等元素设计
    - outline的效果将随元素的focus而自动出现，相应的由blur而自动消失，这些都是浏览器的默认行为，无需JavaScript配合CSS来控制
    - outline是不占空间的，outline不会像border那样影响元素的尺寸或者位置
  - border-none-0
    - border:none 浏览器不进行渲染，不占用内存，等价于border-style:none
      - border:initial none initial;
    - border:0 浏览器对border-width、border-color进行渲染，占用内存
      - border:0 initial  initial;
    - 当定义边框时,必须定义边框的显示样式，因为边框默认样式为不显示none,所以仅设置边框宽度,由于样式不存在,边框的宽度也自动被设置为0，最终不会显示
- scroll
  - `window.scrollbars` property returns the scrollbars object, whose visibility can be checked.
  - window.scrollbars 值为 `BarProp {visible:true}` ，在无滚动条时也是此值
  - 浏览器默认 scrollbar width: 17pixels
  - firefox的滚动条和chrome的滚动条显示样式有明显区别，如何处理差异
  - 差异
    - width: firefox滚动条会自动隐藏并收窄宽度
    - color: firefox滚动条颜色会自动与背景色一致
    - pos: Firefox displays scrollbar inside right padding area and Chrome displays scrollbar outside right padding area
      - 这会导致水平滚动条一个显示，一个不显示
      - https://drafts.csswg.org/css-overflow-3/#scrollable
  - 可比较在线版google-spreadsheets和office-excel，所以滚动时右侧边框要注意处理，容易空白
  - As of late 2018, since Firefox 64, it is possible to use new specs for a simple Scrollbar styling (not as complete as in Chrome with vendor prefixes).
  - css的scrollbar-width属性可设置滚动条宽度
    - auto，默认值
    - thin，更窄的滚动条
    - none，不显示滚动条，但能滚动
    - 此属性目前**仅firefox支持**
    - https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Scrollbars
