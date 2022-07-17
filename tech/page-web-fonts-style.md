---
title: page-web-fonts-style
tags: [fonts, style, web]
created: 2020-07-18T16:29:28.838Z
modified: 2020-07-18T16:29:56.497Z
---

# page-web-fonts-style

# 深入理解CSS：字体度量、line-height 和 vertical-align

``` html
<div>
  <span class="a">Ba</span>
  <span class="b">Ba</span>
  <span class="c">Ba</span>
</div>
div { font-size: 100px }
.a { font-family: Helvetica }
.b { font-family: Gruppo }
.c { font-family: Catamaran }
```

- font-size相同，font-family不同，得到的span元素的高度会不同
- 为什么 ` font-size: 100px` 不能得到相同高度的元素呢
  - 一款字体会定义一个 **em-square**，它是用来盛放字符的容器。这个 em-square 一般被设定为宽高均为1000相对单位
  - 字体度量都是基于这个相对单位设置的，包括 ascender、descender、capital height、x-height 等
  - 在浏览器中，上面的1000相对单位会按照你需要的 font-size 缩放
  - 测试中，em-square 是 1000, ascender 是 1100，descender 是 540
  - 这个计算出来的高度决定了HTML元素的 content-area，可以认为 content-area 就是background作用的区域。
  - em 是基于 font-size，而不是基于计算出来的高度
- 当 p 元素出现在屏幕上时，它可能包含了多行内容，每行内容由多个内联元素组成（内联标签或者是包含文本的匿名内联元素），每一行都叫做一个 line-box。
  - line-box 的高度是由它所有子元素的高度计算得出的。浏览器会计算这一行里每个子元素的高度，再得出 line-box 的高度（具体来说就是从子元素的最高点到最低点的高度），所以默认情况下，一个 line-box 总是有足够的高度来容纳它的子元素。
  - 每个 HTML元素实际上都是由多个 line-box 的容器，如果你知道每个 line-box 的高度，那么你就知道了整个元素的高度。
  - line-box的难点在于我们看不见它，而且不能用 CSS 控制它。即使我们用 ::first-line 给第一行加上背景色，我们也看不出第一个 line-box 的高度。
- line-box 的高度是根据子元素的高度计算出来的，而不是子元素的 content-area 的高度
  - 一个内联元素有两个高度：content-area高度和 virtual-area高度 
  - content-area 的高度是由字体度量定义的（见上文）
  - vitual-area 的高度就是 line-height，这个高度用于计算 line-box 的高度
  - virtual-area 和 content-area 高度的差异叫做 leading。leading 的一半会被加到 content-area 顶部，另一半会被加到底部。因此 content-area 总是处于 virtual-area 的中间。
  - 计算出来的 line-height（也就是 virtual-area 的高度）可以等于、大于或小于 content-area。
  - 如果 virtual-area 小于 content-area，那么 leading 就是负的，因此 line-box 看起来就比内容还矮了。
- 当 line-height 的值是一个数字时，其实就是相对 font-size 的倍数，而不是相对于 content-area。
  - 所以 line-height:1 很有可能使得 virtual-area 比 content-area 矮，从而引发很多其他的问题
- 于内联元素，padding 和 border 会增大 background 区域，但是不会增大 content-area（不是 line-box 的高度）。一般来说你无法再屏幕上看到 content-area。margin-top 和 margin-bottom 对两者都没有影响。
- 对于可替换内联元素（replaced inline elements）、inline-block 元素和 blockified 内联元素，padding、margin 和 border 会增大 height（译者注：注意 margin），因此会影响 content-area 和 line-box 的高度
- 用 vertical-align: middle 会不会好一点呢？读 CSS 文档你会发现，middle 的意思是「用父元素 baseline 高度加上父元素中 x-height 的一半的高度来对齐当前元素的垂直方向的中点」。
  - baseline 所处的高度跟字体有关，x-height 的高度也跟字体有关，所以 middle 对齐也不靠谱。
  - 更糟糕的是，一般来说，middle 根本就不是居中对齐！内联元素的对齐受太多因素影响，因此不可能用 CSS 实现
- vertical-align: top/bottom，表示与line-box的顶部或底部对齐
- vertical-align: text-top/text-bottom，表示与content-area的顶部或底部对齐
- vertical-align的值也可以是数字，表示根据baseline升高或降低，不到万不得已还是别用数字吧。
- 内联元素的对齐，首先就要分为2种，替换内联，非替换内联，
  - 替换内联对齐的是整个元素的下边缘（注: 包括margin的下边缘，如果有文字出现，那么对齐的会变为文字的baseline），
  - 非替换内联默认对齐的是文字内容的baseline，一般大多数情况下都是图片与文字的对齐，这种情况下，要么你将2者line-height设为固定值（px值），同时图片不设置任何上下的padding和margin，如果要保证2段文字对齐，尽量保证字体类型，大小相同，此时你可以设置line-height，如果不相同，那么最好不要设置line-height，寻找其他办法保证垂直居中，因为他们默认的文字基线是一样的。
- 首先假设不设置box-sizing时，那么默认值为content-box，他这儿说的content-area所代表的意思应该是content-box的范围，很明显，如果代表的意思是content-area，那就有点奇了，字体度量代表了content-area，而实际意义上content-area此时就等于content-box + padding-box的范围，也就是background的生效范围，但是字体度量只是字体生效的范围，很明显，二者不相等。
- ref
  - [字体度量、line-height 和 vertical-align](https://zhuanlan.zhihu.com/p/25808995)
