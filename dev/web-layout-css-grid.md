---
title: web-layout-css-grid
tags: [layout, style, web]
created: 1970-01-01T00:00:00.000Z
modified: 2020-12-21T07:46:14.237Z
---

# web-layout-css-grid

# guide

- grid布局优点
  - 固定或弹性的轨道尺寸
    - 可以给每个轨道设置固定的尺寸，也可以设置auto | 1fr | 10% 等弹性的尺寸，实际展示的轨道大小会随着父级的宽高变化而变化
  - 定位项目
    - 可以给每个子项设置具体所占据的位置
  - 创建隐式的轨道
    - 当子项设置的定位位置超出了父级设定的轨道大小，会创建隐式的轨道
  - 对齐控制
    - 和flexbox一样，有多种对齐方式的控制
  - 控制重叠内容
    - 直接在子项上设置z-index的值即可

- grid布局缺点

# [CSS Grid网格布局教程_阮一峰_2019](https://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)

- Grid布局是微软在2010年提出来的一种新的布局方式，到2016年的时候提交了该布局的草案，经过发展，grid布局慢慢变的成熟，兼容性也越来越好
- Grid Container
  - 网格容器，一个元素应用了 `display: grid;` 后就是一个网格容器了，它是所有网格项的父元素
- Grid item
  - 网格项，grid容器的直接子元素，一个grid item可能占有多个cell
- Grid Line
  - 网格线，组成网格项的分界线，虚拟的，如3×4的网格里有4条水平和5条垂直网格线
- Grid track
  - 轨道，网格轨道，两个相邻的网格线之间为网格轨道，也就是列宽或行高
- Grid Cell
  - 网格单元，两个相邻的列网格线和两个相邻的行网格线组成的网格单元，
  - 网格项是HTML里的dom元素，而网格单元是定义网格容器的时候分割出来的网格单元
- Grid area
  - 网格区域，四个网格线包围的总区域，
  - 与网格单元不同的是，网格单元必须是相邻的网格线
- `fr`单位：剩余空间分配数，用于在一系列长度值中分配剩余空间，按数字比例分配

- 对于grid布局，外层div元素是容器，内层div元素是项目
- 项目只能是容器的顶层子元素，不包含项目的子元素，Grid布局只对项目生效
- 容器的水平方向为row，竖直方向为column，行列交叉的区域为cell
- grid line划分了网格区域，n行有n+1条水平网格线，m列有m+1条竖直网格线

- ## 容器属性
- `display: grid` 设置一个容器采用grid布局
  - 默认情况下，容器元素都是块级元素，但也可以用 `display: inline-grid;` 设成行内元素
  - 设为网格布局以后，容器子元素（项目）的float、display: inline-block、display: table-cell、vertical-align和column-*等设置都将失效。
- grid-template-columns/rows
  - 分别定义每一列的宽度，每一行的高度，可以使用绝对值或百分比
  - 可以定义grid布局列的分割线的名称和轨道的尺寸
  - 可以使用方括号指定每一根网格线的名称，且允许一根网格线有多个名称 `[row-5 row5]`
  - `repeat(count, val)` : 重复val值count次
  - 容器大小不确定时，如果希望每一行（或每一列）容纳尽可能多的单元格，这时可以使用 `auto-fill` 关键字表示自动填充
  - `fr` 关键字表示比例关系，也可放在绝对值后分配剩余空间
  - `minmax()` 函数产生一个长度范围，表示长度就在这个范围之中
  - `auto` 会填满容器的剩余可用空间，由浏览器决定，默认使用最大宽度或min-width
  - `max-content` : 内容的最大宽度，min-content 内容的最小宽度
- grid-template-areas
  - 定义网格区域area，一个区域由单个或多个单元格组成
  - 如果某些区域不需要利用，则使用"点" `.` 表示空的cell
  - 区域的命名会影响到网格线，每个区域的起始网格线，会自动命名为 区域名-start，终止网格线自动命名为 区域名-end
- grid-template: grid-template-columns grid-template-rows grid-template-areas
- grid-gap: row-gap col-gap 
- grid-row/column-gap
  - 指定行间距，列间距
  - 最新标准，三个属性名的grid-前缀已经删除，grid-column/row-gap简写成column/row-gap，grid-gap写成gap
- place-content: align-content justify-content 
- justify/align-content
  - justify-content: 设置整个内容区域在容器里水平空间的位置，类似flex
  - align-content: 竖直空间的位置
  - 可选值：start | end | center | stretch(项目没有指定大小时会占满) | space-around(项目间间隔比项目与容器边框间隔大一倍) | space-between(项目与容器边框无间隔) | space-evenly(项目与容器边框间隔与项目间间隔相等)
- place-items: align-items justify-items 
- justify/align-items
  - justify-items：设置单元格内容的水平位置（左中右）
  - align-items：设置单元格内容的垂直位置（上中下）
  - 可选值：start | end | center | stretch; 
  - 默认值：stretch，占满单元格的整个宽度
- grid-auto-columns/rows  
  - 设置自动创建的多余网格的列宽和行高
    - 比如网格只有3列，但是某一个项目指定在第5列。这时，浏览器会自动生成多余的网格，以便放置项目
  - 如果不设置值，浏览器会根据单元格内容的大小，决定新增网格的列宽和行高
  - 网格项目多余设置的单元格，会创建隐式轨道
- grid-auto-flow
  - 设置没有明确指定位置的grid子项的放置方式
    - 划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。
    - 默认的放置顺序是"先行后列"，即先填满第一行，再开始放入第二行
  - row/column(先列后行)
  - 默认值: row 先行后列
  - row dense: 先行后列，并尽可能填满，中间的小项目可能会提前
    - 此时使用column dense可能就刚好填满了
- grid 简写
  - gird: grid-template-rows grid-template-columns grid-template-areas grid-auto-rows grid-auto-columns grid-auto-flow
  - `grid: none` ：所有子属性都是初始化的值
  - `auto-flow` ： 表示的值为 row | column，但是统一使用 auto-flow来表示，具体需要看它放置的位置在哪里，如果放置在 / 的左侧，就表示 grid-auto-flow: row， 如果放在右侧，就表示 grid-auto-flow: column

- ## 项目属性
- grid-column/row
  - grid-column-start/end: 左/右边框所在的垂直网格线
  - grid-row-start/end: 上/下边框所在的水平网格线
  - 行或列边框在未定义的情况下从1开始递增
  - 除了指定为第几个网格线，还可以指定为网格线的名字
  - auto 全自动，包括定位和跨度
  - 每次定义四个属性才能定义单元格的边框位置是复杂的，使用span关键词来简写
  - span表示跨越几个网格
    - span并不只是向后或先下跨越网格，当把 grid-row/column-start 改为 grid-row/column-end 时， span 便表示向左/上跨越
  - 使用这四个属性，如果产生了项目的重叠，则使用z-index属性指定项目的重叠顺序
  - 简写 grid-column: grid-column-start grid-column-end
  - 简写 grid-row: grid-row-start grid-row-end
- grid-area
  - 指定项目放置的area区域名，也可以直接指定项目四边位置
  - 在定义子元素的位置时， 可以使用已经定义好的网格区域名称快速定义子项目的分布位置。
  - 简写 grid-area: grid-row-start grid-column-start grid-row-end grid-column-end 
- justify/align-self
  - justify-self: 设置单元格内容的水平位置（左中右），跟justify-items属性的用法完全一致，但只作用于单个项目
  - align-self: 属性设置单元格内容的垂直位置（上中下），见align-items
  - 可选值：start | end | center | stretch
  - 简写 place-self: align-self justify-self
- css函数
  - repeat(): 允许大量重复显示模式的行或列以更紧凑的方式编写
  - fit-content()：参数是长度值或百分比
    - 它在内容的最小值和参数中取一个最大值，然后再在内容的最大值中取一个最小值
    - 当内容少时，它取内容的长度，
    - 如果内容多，内容长度大于参数长度时，它取参数长度，
    - 可以理解为它可以控制最大值是多少
  - minmax(min, max) ：定义了长度范围区间

# pieces

- 在使用Grid布局的时候始终把容器当作是一个多行多列的网格有助于更准确的实现UI效果
- Grid属性布局分为容器属性和项目属性， 这与Flex布局的属性分类是相似的
- 使用 `display:grid` 声明一个容器， 容器以块级元素存在
  - 如果需要是容器变为行级元素可以使用 `display: inline-grid;`
- 当容器的宽度不确定的时候，如果需要容器中尽可能的充满项目，使用 `auto-fill` 属性自动填充容器。
- `minmax(min,max)` 给定项目一个长度范围，使项目的长度在这个范围当中。
- `auto` 不设定项目的宽度， 由浏览器根据实际情况决定项目的宽
- `fr` 是网格布局提供的一种表示比例关系的关键词
- 容器中的子项目的分布是由无形的一条条网格线划分的，在定义行和列的时候可以同时定义网格线的名称，方面设定子项目的位置和跨度。
- grid-template-areas：定义网格区域的名称，同网格线名称的作用相同，方便定义子项目位置，跨度的定义
- grid-auto-flow：定义子项目的排列顺序， 默认是先列后行(row)
- justify-items: 定义子项目在水平位置的分布
- align-items: 定义子项目在垂直位置上面的分布
- place-items: justify-items 和 align-items 的合并写法
- 在之前的项目中内容默认都是在左上角，可以通过配置这三个属性来改变，和Flex布局的justify-content和align-items属性的使用是相似的。

- grid布局是二维的，可以通过横轴和交叉轴来对齐grid item。
  - 它有一条轴叫 inline axis，它与文字的书写模式（水平书写、竖直书写）有关，
  - 由于我们通常不会涉及到文字的书写模式，暂且把 inline axis 看做是横轴，把 block axis 看做是与横轴交叉的轴
  - justify-items是描述items在布局区域沿着 inline axis 的对齐方式
    - In grid layouts, it aligns the items inside their grid areas on the inline axis
  - align-items在FlexBox布局中它表示items在纵轴上的对齐方式；
    - 在grid布局中，表示items在grid area竖直方向上对齐方式

# Relationship of grid layout to other layout methods

- The basic difference between CSS Grid Layout and CSS Flexbox Layout is that flexbox was designed for layout in one dimension - either a row or a column. 
- Grid was designed for two-dimensional layout - rows, and columns at the same time. 

- Grid interacts with absolutely positioned elements, which can be useful if you want to position an item inside a grid or grid area. 
- The specification defines the behavior when a grid container is a containing block and a parent of the absolutely positioned item.

- If you set an item to `display: contents` , the box it would normally create disappears, and the boxes of the child elements appear as if they have risen up a level. 
  - This means that children of a grid item can become grid items.
- This can be a way to get items nested into the grid to act as if they are part of the grid, and is a way around some of the issues that would be solved by subgrids once they are implemented. 
- You can also use `display: contents` in a similar way with flexbox to enable nested items to become flex items.

# A Complete Guide to Grid

- [A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

# 精读《用 css grid 重新思考布局》

- [精读《用 css grid 重新思考布局》](https://zhuanlan.zhihu.com/p/86519309)

- Flex是一维布局方式，我们需要不断嵌套div才能形成复杂结构，而一旦布局产生了变化，原有嵌套结构如果不能 “兼容变化” 到新结构，代码就需要重构。
- 而Grid是二维布局，即便布局方式做了很大的调整，也仅需少量修改就能适配
- 作者首先提出了Flex的问题，也是block float flex这三种布局模式的通病：
  - 布局结构由div层级描述，导致在div层级复杂且遇到结构变更时难以维护。
  - 定制能力弱。
    - Flex布局有一些不受控制的智能设定，比如宽度 50% 的子元素会被同级元素挤到 50% 以下，这种智能化在某些场景是需要的，但由于没有提供像 Grid 的 minmax 之类的 API，所以定制性不足。
- 使用Grid可以将UI结构与HTML结构分离，HTML结构仅描述包含关系，我们只需在样式文件中描述具体UI结构。
- grid-template-areas是进一步抽象的语法，将页面结构通过直观的文本描述，无论是理解还是修改都更为轻松。
- Grid通过二维结构描述，将子元素布局控制收到了父级，使布局描述更加直观。
- Flex依然有使用场景，即简单的一维结构，或者 space-between 等 Flex 独有语法的情况。
- 因此，推荐整体、复杂的二维布局采用 Grid，一维的简单布局采用 Flex。
- Grid的布局思路给了我很多启发，HTML 结构与 UI 结构的分离有助于减少 DIV 的层级结构，使代码看上去更清晰。
  - 也许有人会疑惑，Grid将HTML布局部分功能挪到了CSS，整体复杂度应该不变。
  - 其实，从 grid-template-areas 这个API可以看到，Grid 不仅仅将布局功能抽到CSS中，更是将布局描述进行了一层抽象，使代码更易维护。
- Grid可以对布局进行抽象，因为Grid将二维结构都掌握在手中，得到了更大的布局能力，才能进一步将结构化语法抽象为字符串的描述。
- 一般来说，代码抽象程度越高就越易读，越易维护
- UI是对文本的再抽象，同时可以规避一些不可能存在的语法
- 布局只能以凸多边形方式拓展，不可能分离，也不可能突然插入一个其他模块而变成凹多边形。
- 因此UI可以将这个错误规避，并简化为横竖多条线的方式对UI进行划分，显然这种描述方式效率更高。
- Grid以及图形化插件的探索，是布局领域的一大进步，是不断抽象的尝试，要解决的问题有一个：如何提供一种更直观的描述UI的方式。
- CSS Grid是一种二维布局的语法，相比Block、Flex等一维布局方案，多了一个维度可以同时从行与列角度定义布局，因此派生出 grid-template-areas 等语法，整体上更内聚更直观，抽象度也更高了。
- 布局的发展方向：让布局与DOM分离
  - 开发UI部分时，只需关心页面由哪些模块组成，去实现这些模块就行了，而不需要关心模块之间应该如何组合(与headless ui的区别？)
  - 在描述组合时，可以通过可视化或比较抽象的字符串描述布局的结构，并对应到写好的模块上，这样的代码维护性远高于用div描述结构的方案

# Things I’ve Learned About CSS Grid Layout

- [Things I’ve Learned About CSS Grid Layout_2016](https://css-tricks.com/things-ive-learned-css-grid-layout/)

- Don’t use flexbox for overall page layout.
- Flexbox is for one dimensional layout (row or column).
- CSS grid is for two dimensional layout.
- They can be combined as well. You can turn a grid item into a flex container. You can turn a flex item into a grid.
- Using negative line numbers can be really helpful
  - By using -1, you can be sure your content will always reach the end column.
- Grid areas create implicit line names
- When you absolutely position a grid item, rather than its positioning context being its container (i.e. the entire grid), we can position it in relation to its specified grid-column and grid-row start and end lines. 
  - As usual,                      `position: absolute` removes an element from the flow of the document (i.e. it is ignored by other elements). 
  - This makes absolute positioning useful if you want to overlap grid items without disrupting the grids auto-placement algorithm. 
  - Auto-placement goes out of its way not to overlap items unless you explicitly declare both a grid-column-start and grid-row-start value for every item.
- All grid items have a default order value of 0. 
  - So `order: 1;` applied to a grid item would make after everything else, not before.
- Things are way easier if you name your grid lines
- The `fr` unit removes the need for math
- Twelve columns is the default of web design. 
  - The Bootstrap grid uses 12 columns and just about every other grid framework currently out there. 
  - There is a good reason for this: twelve is divisible by both three and four, giving more flexibility in how we can lay out content across the page. 
  - We can divide our content evenly into 12 parts, 6 parts, 4 parts, 3 parts, or in half.
- While some people like the familiarity that comes with consistently using the same grid for every project, there is no need to have more columns than you actually need and you should build the grid that’s right for your content and desired layout rather than a one-size-fits all set-up.

# discuss

- ## If you are using CSS grid, avoid horizontal scrolling by setting a grid item column to `minmax(0, 1fr)` instead of `1fr`.
- https://twitter.com/shadeed9/status/1434441947003998209
  - I just helped a friend with a bug. On mobile, he was trying to make a responsive `<table>`, but there was a horizontal scroll. What causes it?
  - On the parent, the first thing I noticed was `grid-template-columns: 1fr`. It's risky and problematic to use that 1fr.
  - When a grid item contains a `<table>`, its width will expand to match the table's width. CSS grid defaults to this behavior.
  - To override that, we need to replace `1fr` with `minmax(0, 1fr)`.
  - [The Minimum Content Size In CSS Grid](https://ishadeed.com/article/min-content-size-css-grid/)
- When I ended up with horizontal scrolling on my page I try to work around the width of the grid container or I just use, overflow-x: hidden
# ref

- [CSS Grid布局那么好，为什么至今没有人开发出基于Grid布局的前端框架呢？](https://www.zhihu.com/question/397861009)
  - flexbox布局非常成熟
  - css的卖点是炫酷的design，而不是炫酷的技术
- [写给自己看的display: grid布局教程_张鑫旭](https://www.zhangxinxu.com/wordpress/2018/11/display-grid-css-css3/)
- [Grid 布局学习](https://juejin.im/post/5d8daa0f518825096d3b4dca)
- [CSS Grid 系列(上)-Grid布局完整指南](https://zhuanlan.zhihu.com/p/33030746)
- [[译] Grid布局完全指南](https://shanyue.tech/post/Grid-Guide/)
- [图解 Grid 布局 (非常详细)](https://lefex.github.io/wsy/2019/11/02/grid.html)
- [The Quirks of CSS Grid and Absolute Positioning](https://webdesign.tutsplus.com/tutorials/the-quirks-of-css-grid-and-absolute-positioning--cms-31437)
