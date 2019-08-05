---
title: note-viz-d3
created: '2019-08-01T05:09:11.917Z'
modified: '2019-08-01T05:16:27.296Z'
tags: [js/d3, viz]
---

# note-viz-d3

## summary

- d3.svg.arc()
    - disk 圆形
    - sector 扇形
    - annulus 圆环
    - annular sector 环形扇区
- 约定
    - tooltip 鼠标提示
    - label 数据标注
- data vs datum
    - data 将一个数组的各项分别绑定到各元素上
    - datum 将数组本身绑定到各元素上  
自定义数据绑定？

- 核心api
    - data()
    - transition()
    - enter()
    - exit()
    
- attr()用于设置DOM属性，style()用于设置css样式  
    - 添加样式1 selection.attr('class','title')  
    - 添加样式2 selection.style('width',240px)
    - 添加样式3 selection.classed('title',true)

- d3绘图套路
```
 svg.selectAll('circle')
    .data(dataset)
    .enter()
    .append('circle')
    .attr()
```
- 数据更新
    - 数量不变，值变化 enter()
    - 数量变多 enter()
    - 数量变少 exit()
- transtion()默认插值间隔是250ms
    - duration() ms
    - ease() 
    - delay() ms
- 坐标轴3部分
    - 轴线
    - 刻度线
    - 文本标签  
注意：坐标轴要与比例尺关联    
- Mike Bostock的外边距约定 http://bl.ocks.org/mbostock/3019563
- 剪切路径clip-path  
会将svg边界上和边界外的元素超出svg矩形的部分隐藏

