---
title: note-web-layout-flexbox
tags: [layout, style, web]
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-17T08:53:14.923Z'
---

# note-web-layout-flexbox

## guide

- ref
  - [30分钟学会Flex布局](https://zhuanlan.zhihu.com/p/25303493)

 

## pieces

## summary

- ### 弹性容器
- flex-direction: 指定主轴上项目排列的方向
  - row/column/-reverse
  - 默认值：row，主轴为水平方向，起点在左端
- flex-wrap: 指定容器内的项目是否可以换行
  - nowrap, wrap, wrap-reverse
  - 默认值：nowrap，即当主轴尺寸固定时，若空间不足，则项目尺寸会随之调整变小，而并不会挤到下一行
- flex-flow: flex-direction flex-wrap
  - 默认值为：row nowrap
- justify-content: 指定项目在主轴(水平方向)的对齐方式
  - flex-start/end, center, space-between/around
  - 默认值：flex-start 左对齐
  - 要为项目设置宽度
  - 决定项目显示在一行的什么位置，以及项目在容器里如何分布
- align-items: 指定高度不同的项目在容器纵向(交叉轴)的对齐方式
  - stretch, flex-start/end, center, baseline
  - 默认值：stretch，若项目未设置高度或者设为auto，则将占满整个容器的高度，高度都相同为容器高度
- align-content: 指定多行项目的对齐方式
  - 前提条件：flex-wrap需要设置为wrap，且必须出现多行，弹性容器的高度必须大于各行项目的高度之和
  - stretch, flex-start/end, center, space-between/around
  - 默认值：stretch，轴线平分容器的竖直方向空间
    - 拉伸各个项目，让一行里的项目具有相同的高度。
    - 若项目里的内容不一样多，则各行的高度可能不同

- ### 弹性项目
- order: 指定项目在行中排列的位置顺序
  - 默认值：0，数值越小，排列越靠左或上，可为负，可不连续
  - 让元素显示顺序与html源码中的顺序无关
- align-self: 指定单个弹性项目在纵向的对齐方式
  - 默认值：auto，会继承父元素的align-items，若无父元素则stretch
  - 单个项目的设置会覆盖align-items的设置
- flex-grow: 指定项目的放大比例
  - 默认值：0，即如果存在剩余空间，也不放大
  - 当所有的项目都以flex-basis的值进行排列后，仍有剩余空间，此时flex-grow就会发挥作用了
  - 只要大于0，整行宽度就会被占满
  - 项目的宽度由2个因素确定：项目的放大比例和容器中项目的数量
- flex-shrink: 指定项目的缩小比例
  - 默认值：1，如果空间不足，该项目将缩小，负值对该属性无效
  - 当所有项目以flex-basis的值排列完后发现空间不够了，且nowrap 时，此时flex-shrink就会起作用了
  - 前提条件：当项目宽度之和大于容器宽度，且nowrap时，项目才会缩小
  - 弹性容器允许换行时flex-shrink属性没有作用
  - 若项目的flex-shrink为0，其他项目都为1，则空间不足时，前者不缩小
  - 如果收窄容器，弹性项目都无法并排显示，那么浏览器会把各个弹性项目都单独放在一行里
- flex-basis: 定义了在分配多余空间之前，项目占据的主轴空间
  - 浏览器根据这个属性，计算主轴是否有多余空间
  - 默认值：auto, 此时项目的宽高取决于width, height
  - 当主轴为水平时，当设置了flex-basis，项目的宽度设置值会失效
  - 指定弹性项目的基准宽度，可以用绝对值或百分比
  - 可理解为弹性项目的最小宽度，但具体宽度由flex属性中其他值决定
  - 当flex-basis值为0%时，是把该项目视为零尺寸的，故即使声明该尺寸为100px，也并没有什么用
  - flex-basis属性的值为0%时，弹性项目的宽度完全由flex-grow属性决定。也就是说、弹性项目里内容的量对项目的宽度没有影响 。
  - 当flex-basis值为auto时，则跟根据尺寸的设定值(如100px)，则这100px不会纳入剩余空间
- flex: flex-grow flex-shrink flex-basis 指定项目宽度变化方式
  - 默认值：0 1 auto，弹性项目的宽度由里面的内容自动确定
  - 快捷值：auto (1 1 auto) 和 none (0 0 auto)
  - 当flex取值为一个非负数字时，则该数字为flex-grow值，flex-shrink 取 1，flex-basis 取 0%
  - 当flex取值为0时，对应的三个值分别为 0 1 0%
  - 当flex取值为一个长度或百分比(如0%)时，则视为flex-basis值，flex-grow 取 1，flex-shrink 取 1
  - 当flex取值为两个非负数字，则分别视为flex-grow和flex-shrink的值，flex-basis 取 0%
  - 当flex取值为一个非负数字和一个长度或百分比，则分别视为flex-grow和flex-basis的值，flex-shrink 取 1

- ### grow和shrink的关系
- 当 flex-wrap 为 wrap/-reverse，且子项宽度和不及父容器宽度时，flex-grow 会起作用，子项会根据 flex-grow 设定的值放大（为0的项不放大）
- 当 flex-wrap 为 wrap/-reverse，且子项宽度和超过父容器宽度时，首先一定会换行，换行后，每一行的右端都可能会有剩余空间（最后一行包含的子项可能比前几行少，所以剩余空间可能会更大），这时 flex-grow 会起作用，若当前行所有子项的 flex-grow 都为0，则剩余空间保留，若当前行存在一个子项的 flex-grow 不为0，则剩余空间会被 flex-grow 不为0的子项占据
- 当 flex-wrap 为 nowrap，且子项宽度和不及父容器宽度时，flex-grow 会起作用，子项会根据 flex-grow 设定的值放大（为0的项不放大）
- 当 flex-wrap 为 nowrap，且子项宽度和超过父容器宽度时，flex-shrink 会起作用，子项会根据 flex-shrink 设定的值进行缩小（为0的项不缩小）。但这里有一个较为特殊情况，就是当这一行所有子项 flex-shrink 都为0时，也就是说所有的子项都不能缩小，就会出现讨厌的横向滚动条
- 总结上面四点，可以看出不管在什么情况下，**在同一时间flex-shrink和flex-grow只有一个能起作用**，这其中的道理细想起来也很浅显：空间足够时，flex-grow 就有发挥的余地，而空间不足时，flex-shrink 就能起作用。当然，flex-wrap 的值为 wrap | wrap-reverse 时，表明可以换行，既然可以换行，一般情况下空间就总是足够的，flex-shrink 当然就不会起作用

## Flexbox layout isn't slow

 - [Flexbox layout isn't slow](https://developers.google.com/web/updates/2013/10/Flexbox-layout-isn-t-slow)

- Wilson notes: some flexbox layouts were taking close to 100 milliseconds; reworking our layouts without flexbox reduced this to 10 milliseconds!
- Wilson's comments were about the original (legacy) flexbox that used `display: box;`
- We asked Ojan Vafai, who wrote much of the implementation in WebKit & Blink, about the newer flexbox model and implementation.
  - The new flexbox code has a lot fewer multi-pass layout codepaths. 
  - You can still hit multi-pass codepaths pretty easily though (e.g. `flex-align: stretch` is often 2-pass). 
  - In general, it should be much faster in the common case, but you can construct a case where it's equally as slow.
  - That said, if you can get away with it, regular block layout (non-float), will usually be as fast or faster than new flexbox since it's always single-pass. 
  - But new flexbox should be faster than using tables or writing custom JS-base layout code.
- Old vs New Flexbox Benchmark
  - Old is 2.3x slower than new.
  - I also ran the benchmark using `display:table-cell` and it hit 30ms, right between the two flexbox implementations.
  - The benchmarks above only represent the Blink & WebKit side of things. Due to the time of implementation, flexbox is nearly identical across Safari, Chrome & Android.
