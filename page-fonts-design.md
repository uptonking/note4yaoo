---
title: page-fonts-design
tags: [fonts, ux]
created: '2020-07-19T02:13:28.320Z'
modified: '2020-07-19T02:17:32.746Z'
---

# page-fonts-design

## 字体结构解剖(Anatomy)

![纵向结构图](https://upload-images.jianshu.io/upload_images/7078482-107d1bab72608f82.jpg)

- **baseline**（基线）：可理解为坐标原点
  - 字母列表中字符底部所处的那条隐形的线。它相当于某个字体x高的底边
  - 是一根不可见的基准线，所有字母都停靠在这根线上
- **x-height**: 字体中小写字母“x”的高度
  - x-height反映了一个字体的整体高度。通常x-height 大的字体能增加文本的可读性，原因是x-height 大的字母会有更多的内部空白，比如 “O” 中间的圆形会比较大。
  - 这是决定字体视觉大小的重要因素，字体会根据x的比例关系做其他字母的延伸部
- **cap height**: 大写字高
  - 是指从baseline开始测量的大写平整字母（比如M，N，I）的高度
- **ascent/ascender**（上伸部）：基线之上字体占有的空间
  - 一个字符中，从x高向上延伸的笔画，小写字母中向上的垂直笔画有时会超出Cap height，比如上图的小写字母“d” 
- **descent/descender**（下伸部）: 基线之下字体占有的空间
  - 小写字母中向下的垂直笔画有时会超过Baseline，比如字母p, j
  - 从基线向下延伸的笔画
- **line gap**（行间距 leading）:descent之下再到下一行的头的距离
- **line-height**（行高）：ascent + descent + line-gap
  - top到bottom的距离
- line height/leading：控制两条baseline之间的距离。行距和字体的字号成正比
- letter-spacing/tracking：每个字母之间的间距
  - 和kerning不同，kerning是指每个单词之间的间距。像标题这样字号大的内容通常会缩小字母之间间距来提高可读性。

![字体结构图](https://pic3.zhimg.com/80/v2-d8ce7c8b9741fa0f5159e9aa5bc2d598_720w.jpg)

- 看图 
  - font-size = ascent + descent
  - content-area height = text-top与text-bottom间的距离

- 设置了同样大小的font-size为什么会出现宽度相同高度不同这样的差异呢？
  - 字体设计时，不出意外都是在上下1000units(font-size)这个单元格之间的范围内设计
  - Win/HHead Ascent使用在windows系统，HHead Ascent是用在Mac系统，比ascent更高，也就是比font-size更高
- `display:inline` 的元素（如：span, label, i, 等元素）的基线就是其中的元素的字体的基线。几个不同的inline元素放在同一行的时候，就是把几个的baseline对齐就可以了
- `display:inline-block` 从图中可以看出div元素的baseline是以其包含的inline元素的最后一行最为自己的baseline。下一个同一行中的元素将会把baseline与div的这条基线对齐
- `display:inline-block;` 的元素的baseline，当其中有inline元素是按inline的baseline, 当没inline元素是，按最底边
- The baseline of an 'inline-block' is the baseline of its last line box in the normal flow, unless it has either no in-flow line boxes or if its 'overflow' property has a computed value other than 'visible', in which case the baseline is the bottom margin edge.

- ref
  - [字体基础知识](https://www.jianshu.com/p/b788f7b188f8)
  - [深度剖析CSS Baseline](https://zhuanlan.zhihu.com/p/30169829)
  - [字体术语集](https://zhuanlan.zhihu.com/p/136840798)
