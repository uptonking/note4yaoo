---
tags: [browser, web, webkit]
title: note-webkit
created: '2019-10-17T09:05:43.329Z'
modified: '2019-10-17T09:07:19.654Z'
---

# note-webkit


## reflow
- reflow
    - 如果引起reflow，样式首先必须重新计算，因此重排会触发两种操作
    - force reflow https://gist.github.com/paulirish/5d52fb081b3570c81e3a
- 当在js中调用（requested/called）以下所有属性或方法时，浏览器将会同步地计算样式和布局，进行重排（`reflow` 或 layout thrashing ），通常是性能瓶颈
- element
    - 盒子计算
        - elem.offsetLeft/offsetTop, elem.offsetWidth/offsetHeight
        - elem.offsetParent
        - elem.clientLeft/clientTop, elem.clientWidth/clientHeight
        - elem.getClientRects(), elem.getBoundingClientRect()
    - frame/image
        - height, width
    - 滚动相关
        - elem.scrollBy(), elem.scrollTo()
        - elem.scrollIntoView(), elem.scrollIntoViewIfNeeded()
        - elem.scrollWidth/scrollHeight, elem.scrollLeft/scrollTop
    -焦点
        - elem.focus() 可以引起两次重排
    - 获取其他属性
        - elem.computedRole, elem.computedName
        - elem.innerText
- window.getComputedStyle()
    - 通常会引起样式重新计算
    - 元素在shadow tree中
    - 使用了media queries（viewport相关的一种），特别是以下某一属性
        - width, height
        - aspect-ratio,device-pixel-ratio, resolution, orientation
    - 获取以下的某一种属性
        - width, height，top, right, bottom, left
        - margin,padding
        - transform, translate, rotate, scale
        - x, y, rx, ry
- window
    - window.scrollX, window.scrollY, scrollBy(), scrollTo(),scrollX/Y
    - window.innerHeight, window.innerWidth
    - window.getMatchedCSSRules() 仅重新计算样式
    - webkitConvertPointFromNodeToPage(),webkitConvertPointFromPageToNode()
- form
    - inputElem.focus()
    - inputElem.select(), textareaElem.select()
- mouse
    - mouseEvt.layerX/layerY, mouseEvt.offsetX/offsetY
- document
    - doc.scrollingElement 仅重新计算样式
- range
    - range.getClientRects(), range.getBoundingClientRect()
- svg
    - computeCTM(), getBBox()
    - getCharNumAtPosition(),getNumberOfChars()
    - getComputedTextLength(),getSubStringLength(), selectSubString()
    - instanceRoot
    - 很多
- contenteditable
    - 非常多，包含复制图片到剪切板
- 如何避免reflow
    - for循环里触发重排或改变DOM性能最差
    - 使用DevTools Timeline分析性能问题的位置
    - 合并读写DOM操作，参考[FastDOM](https://github.com/wilsonpage/fastdom)，或使用虚拟DOM
- 参考
    - https://jinlong.github.io/2015/09/30/what-forces-layout-reflow/
    - https://www.zcfy.cc/article/fastersite-how-not-to-trigger-a-layout-in-webkit

## changelog

