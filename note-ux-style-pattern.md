---
title: note-ux-style-pattern
tags: [style, ux, web]
created: '2019-10-10T08:40:08.927Z'
modified: '2020-07-14T10:44:34.209Z'
---

# note-ux-style-pattern

## ux
- handwritten：素描风格，线框图风格
- unfold: 揭开效果，类似画皮的撕皮
  - https://aframe.io/aframe/examples/animation/unfold/
- skew layer effect
- 广告字符通过动画形成名称文字的动画，类似不完美的她
- 一个文字或形状，通过动画渐变成另一个
- 骨架屏效果
- 分层过渡效果
- 实现div-border-collapse效果的方法
  - https://stackoverflow.com/questions/17915865/how-to-make-borders-collapse-on-a-div
  - https://stackoverflow.com/questions/5737693/simulating-border-collapse-in-lists-no-tables
  - 不要使用display:table-cell，表格布局在频繁操作动态样式时性能差
  - 使用负值margin
    - http://jsfiddle.net/6eGdN
    - 通过父边框挡住子边框实现，或全部显示子边框

``` css
      div.gridcontainer {
        width: 7/86px;
        line-height: 0;
      }

      div.griditem {
        display: inline-block;
        border: 1px solid black;
        width: 18px;
        height: 18px;
        margin-left: -1px;
        margin-bottom: -1px;
      }
```

  - 使用父边框上左，使用子边框右下，也可交换

``` css
    div.gridcontainer
  {
      width: 76px;
      line-height: 0;
      border: solid black;
      border-width: 1px 0 0 1px;
  }
  div.griditem
  {
      display:inline-block;           
      border: solid black;
      border-width: 0 1px   1px 0;
      width: 18px;
      height: 18px;
  }
  ```

  - use box-shadow instead of using border 
    - https://codepen.io/savehansson/pen/rsIEp
  - add a left and bottom border to the ul and drop it from the li
