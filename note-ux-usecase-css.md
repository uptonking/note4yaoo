---
title: note-ux-usecase-css
tags: [css, usecase, ux]
created: '2020-07-17T13:58:14.640Z'
modified: '2020-08-01T07:13:13.830Z'
---

# note-ux-usecase-css

## 实现div-border-collapse效果的方法

- ref
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
  div.gridcontainer {
    width: 76px;
    line-height: 0;
    border: solid black;
    border-width: 1px 0 0 1px;
  }

  div.griditem {
    display: inline-block;
    border: solid black;
    border-width: 0 1px 1px 0;
    width: 18px;
    height: 18px;
  }
```

- use box-shadow instead of using border 
  - https://codepen.io/savehansson/pen/rsIEp
- add a left and bottom border to the ul and drop it from the li
