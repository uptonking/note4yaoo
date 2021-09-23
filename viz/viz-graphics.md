---
title: viz-graphics
tags: [graphics, viz]
created: '2020-09-25T03:52:59.024Z'
modified: '2020-12-21T07:47:15.858Z'
---

# viz-graphics

# pieces

- 用matplotlib.pyplot绘图需要知道以下几个概念：
  - 画布/画板
    - 这是一个基础载体，类似实际的画图板，用pyplot.figure()函数创建
    - 程序中允许创建多个画图板，具体操作的画板遵循就近原则（操作是在最近一次调用的画图板上实现），缺省条件下内部默认调用pyplot.figure(1)。
  - 图形区/绘图区
    - 用来绘图的实际区域，一般不直接获取，直接设定方式为pyplot.axes([x, y, w, h])
    - 即axes函数直接确定了该区域在画图板/画布中的位置为x, y，尺寸为w, h
    - axes vs axis
      - 坐标轴，标签，刻度线，数据等都是属于axes对象的一个属性，axis仅仅是坐标轴
      - axes([x, y, w, h])用来设定图形区的笛卡尔坐标区
      - axis([x_left, x_right, y_bottom, y_top])是用来设置所绘制图形的视窗大小的，表示直接展示的图形是需要满足参数中范围的值，直观表现是绘图区实际展示的坐标范围。
      - 在MATLAB中，axes是创建坐标轴对象，axis是修改坐标轴范围。
    - pyplot.axes([x, y, w, h])是用来在画图板上确认图形区的位置和大小的函数，x,y表示图形区左下角相对于画图板的坐标，w,h表示图形区的宽高。
    - pyplot.subplot(abc)本质也是用来确认图形区在画图板上位置大小的函数
      - 区别是该函数将画图板按a行b列等分，然后逐行编号，并选择编号为c的区域作为图形区用来绘图
      - subplot重复操作时如果前后两次的划分方式不一致时，会做必要的历史图形清理
  - 标签区
    - 用来展示图形相关标签的地方，该区域根据图形区进行扩展，与该区域有关联的函数是pyplot.xlabel()、pyplot.ylabel()、pyplot.title()等
