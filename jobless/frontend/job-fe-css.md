---
title: job-fe-css
tags: [css, frontend, job]
created: 2021-09-23T08:17:26.015Z
modified: 2021-10-10T09:17:08.066Z
---

# job-fe-css

# guide

- css要点
  - 层叠规则、特指度、选择器
  - 盒模型
  - 定位布局

- 常见伪元素 :
  - :before/after, ::first-letter/line, ::selection

- 零宽字符
  - 有时候可使用伪元素结合零宽字符使空div显示宽高
  - .class1::before{ content: "\200B"; }
# html

## html元素分类

- html元素默认分为三类：块级block、行内inline、行内块inline-block
- block
  - 单独出现在一行
  - 宽度默认为父元素 100% 宽度，设置 margin 和 padding 都生效
  - 代表：div、p、h1~h6、ul、ol、li、table、blockquote
- inline
  - 不会导致换行，width/height无效，实际宽高取决于内容
  - margin在垂直方向上不生效
  - padding在左右方向会生效，在垂直方向也生效（设置背景色会显示），但是实际上没有撑开父元素，不会影响周围元素布局
  - 代表：span、a、strong、b、i、textarea
- inline-block
  - 元素不会导致换行，但可以设置 width、height
  - 盒宽度默认为内容宽度，设置 margin 和 padding 都生效
  - 代表：input、button

- div没有内容时，默认不占位，设置宽度也没用
  - 可以设置 `min-height:1px;` 使设置的宽高生效
  - The height and width CSS properties are not inheritable. 
  - If not specified, their default value is “auto” which means “browser will calculate it“. 
  - In fact, the **actual width of empty `<div>`** is the width of the containing element. 
  - The **actual height of empty `<div>`** is `0`. 
  - for empty div, the final height would be `0` even there is a percentage height.

## src vs href

- 在 html 引入多媒体内容、`<scirpt>`标签时使用src
  - src指向外部资源的位置，**指向的内容会嵌入到文档中当前标签所在的位置**，在请求src资源时会将其指向的资源下载并应用到文档内替换当前元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕
  - href是指向网络资源所在位置（的超链接），只是用来建立和当前元素或文档之间的连接
  - 小结：src 用于替换当前元素，href 用于在当前文档和引用资源之间确立联系
# css-faq

## 绝对定位元素塌陷

- 三个盒子自外而内嵌套，position属性依次为，fixed, absolute, relative（顺序可能不一样，记不太清了）。如果给最里面的盒子添加padding，问三个盒子的高度会如何变化

- 经过实测，这道题中，relative-box 的 padding 修改时会影响 absolute-box 的高度，而最外层 fixed-box 若不设置高度宽度，则始终保持 0 0
- 对于BFC来说，绝对定位的子元素会被忽略，无法撑起高度
  - float元素可以撑起其高度
- 因此最外层盒子的高度不会改变，而绝对定位盒子的高度会随相对定位盒子高度改变

## 往 ul 里面插入10000个 li

- 使用 `document.createDocumentFragment()` API，创建一个单独的文档对象（一个微型 document），先向该对象上插入 10000 个 `<li>`，之后将该片段插入 `<ul>`，其中的 10000 个节点被一次性插入，只触发一次重新渲染过程；
  - 如果每次都直接向文档中插入 `<li>`，就会触发 10000 次重新渲染

```JS
let list = document.getElementById("list");
let frag = document.createDocumentFragment();
// var frag = new DocumentFragment()

for (let i = 0; i < 10000; i++) {
  let li = document.createElement("li");
  li.innerText = i;
  frag.appendChild(li);
}
list.appendChild(frag);
```

## 实现点击右滑动按钮，同时要求 button 自适应父元素宽度

```css
.container {
  width: 150px;
}

.btn {
  width: 100%;
  /* transition:属性名 持续时间 时间函数 推迟变化时间 */
  transition: margin-left 1s;
}

.btn:hover {
  margin-left: 50px;
}
```

## 递归判断 body 结构是否相同

```JS
let body1 = document1.body;
let body2 = document2.body;

const compareDOM = function(elem1, elem2) {
  let [children1, children2] = [elem1.children, elem2.children];
  if (children1.length != children2.length) return false;
  for (let i = 0; i < children1.length; i++) {
    if (!compareDOM(children1[i], children2[i])) return false;
  }
  if (elem1.tagName != elem2.tagName || elem1.innerText != elem1.innerText)
    return false;
  return true;
};
```

- 借助 Element.children() 可获取当前元素的子元素列表(动态的 HTMLCollection)，递归的获取子元素即可，
  - 到达最底层子节点后比较节点的 tagName 和 innerText，然后返回至上一层——`先序遍历`

- `Element.children` includes only element nodes. 
  - To get all child nodes, including non-element nodes like text and comment nodes, use `Node.childNodes`.

## 负 maring 意义

- 元素自身无宽度，设置负值水平 maring：增加元素宽度。
  - 当设置 margin-left:-100px 元素会在填充完父元素宽度后向左溢出 100px 宽度
- 元素设置了宽度，设置负值水平 maring
  - 产生位移（圣杯布局）
- 元素设置负值 margin-top
  - 与自身高度无关，会导致元素向上偏移（垂直居中）
- 元素设置负值 margin-bottom
  - 与自身高度无关，也不会偏移，会让元素 CSS 作用的范围减小，如背景色；
  - 可比较inline-block元素垂直方向的padding可以让CSS作用范围扩大，但不会增加元素实际尺寸

## 如何减少回流重绘

- transform、opacity
- 使用 display:none 隐藏元素避免回流重绘、使用 visibility:hidden 只是避免回流
- 当要有大量新增样式的操作时，可以使用 document fragment 将最终更新的结果插入，这样只触发一次回流重绘
- 使用 rAF 调节渲染
  - 很多情况下频繁的重新渲染无法避免，比如页面滚动与动画
  - 如果将所有动画函数放在 rAF 回调中，那它就会被放在下一帧渲染前执行，这样将动画效果集中在一次回流重绘中就能渲染，避免了DOM修改时再额外导致回流重绘。 
# css-knowledge
- transform: translate
  - 单个值：A percentage value refers to the width of the reference box defined by the transform-box property.
  - 两个值
    - A percentage as first value refers to the width, as second part to the height of the reference box defined by the transform-box property.

## 选择器

```css
h1 {}

.box {}

.box {}

a[title] {}

a[href="<https://example.com>"] {}

/* 伪类 :link/visited/hover/active/focus，:first-child，:enable/checked */
a:hover {}

/* 伪元素 ::before/after, ::first-letter/line, ::selection */
p::first-line {}
```

## 层叠规则

- 行内 > 内部样式表 > 外部样式表
- 行内 > id > .cls/a[title]/:hover > tag/::before

## 隐藏元素的方法

- display:none
  - 既不占据空间也不交互
  - DOM树中存在该元素，但渲染树不会包含该渲染对象，因此该元素不会在页面中占据位置，也不会响应绑定的监听事件
- visibility:hidden
  - 隐藏元素，在页面中仍占据空间，但是不会响应绑定的监听事件
- opacity:0
  - 将元素的透明度设置为0，看起来隐藏了，但是依然占据空间且可以交互，比如点击button依旧可以触发监听回调

## 居中问题

```

水平居中
行内：
		text-align:center
块级（给定宽度）：
		position:absolute 					设置绝对定位
	  left:50% 										将元素左边缘定位到页面父容器中心
		margin-left:-0.5*width 			将元素左边缘向左回调50%自身宽度
块级（不定宽度）：
		display:flex
		justify-content:center 			设置flex容器水平对齐方式
块级（不定宽度）：
		margin:0 auto
块级（不定宽度）：
		position:absolute 					设置绝对定位
		left:50% 										将元素左边缘定位到页面父容器中心
		transform:translateX(-50%) 	将元素中心点向左回调50%自身宽度

<----------------------------------------------------------------->

垂直居中
行内：
		line-height:height				  设置 line-height==height
行内块：
		vertical-align:middle				设置伪元素，调整基线
		height：100%
块级（给定高度）：
		position:absolute 					设置绝对定位
	  top:50% 										将元素上边缘定位到页面父容器中心
		margin-top:-0.5*height			将元素上边缘向上回调50%自身高度
块级（不定高度）：
		display:flex
		align-items:center 					设置flex容器水平对齐方式
块级（不定高度）：
		position:absolute 					设置绝对定位
		top:50% 										将元素上边缘定位到页面父容器中心
		transform:translateY(-50%) 	将元素中心点向上回调50%自身高度
```

### 水平居中

```CSS
/* 对父元素使用 text-align: center ，其中的行内元素可以水平居中
 */
.container {
  text-align: center;
}

/* 对子元素使用 margin: 0 auto ，左右边距自动分配 */
.center {
  height: 200px;
  width: 200px;
  margin: 0 auto;
  /* 上下0，左右自动*/
  border: 1px solid red;
}

/* 对flex容器使用 justify-content:center ，其中的子元素可以沿主轴居中 */
.center {
  display: flex;
  justify-content: center;
}

/* 子元素使用绝对定位 ,优点：宽度不固定*/
.center {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

/* 直接作用于元素，固定宽度  */
.center {
  position: absolute;
  left: 50%;
  /* 固定 */
  width: 200px;
  /* 宽度*-0.5*width */
  margin-left: -100px;
}

/* 在不知道自身宽高的情况下，与负margin-left和margin-top实现居中不同的是，margin-left必须知道自身的宽高，而translate可以在不知道宽高的情况下进行居中 */
.center {
  position: absolute;
  /*  是以左上角为原点，故不处于中心位置 */
  top: 50%;
  left: 50%;
  /* 往上x,左y移动自身长宽的50%，以使其居于中心位置 */
  transform: translate(-50%, -50%);
}
```

### 垂直居中

- 让盒子（父元素）的行高 line-height 等于盒高，其中的行内元素就会在盒子垂直居中

```CSS
.outerBox {
  width: 200px;
  height: 100px;
  border: 1px solid #000;
  line-height: 100px;
  /* line-height=height */
}
```

- 如果要居中盒内一个行内块级元素
  - 添加另一个行内块级伪元素到末端，高度取 100% 盒高。
  - 使用 vertical-align 改变行基线为 middle ，则所有行内块级元素沿基线对齐，实现盒内的垂直居中

```css
.container {
  height: 600px;
}

/* 添加一个无内容行内块元素,改变该容器基线 */
.container::after {
  display: inline-block;
  vertical-align: middle;
  content: "";
  height: 100%;
}

/* 让垂直居中的行内块元素与基线对齐 */
.center {
  display: inline-block;
  vertical-align: middle;
}

<div class="container"><div class="center">垂直居中</div></div>
```

- 块级元素——flex（不固定高度）
  - 优点：高度不固定、优雅的溢出

```CSS
.container {
  display: flex;
  align-items: center;
}
```

- 块级元素——transform（不固定高度）
  - 父元素使用相对定位，子元素使用绝对定位。
  - 子元素顶部外边距边缘定位到距离非 static 定位祖先元素顶部50%偏移处，
  - 使用 transform: translateY(-50%) 向上平移元素自身高度的50%作为补偿

```css
.container {
  height: 400px;
  position: relative;
}

.center {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

- 块级元素——绝对定位（固定高度）
- 元素的高度需要固定，margin-top 无法自动计算

```CSS
.container {
  height: 400px;
  position: relative;
}

.center {
  position: absolute;
  height: 60px;
  top: 50%;
  margin-top: -30px;
}
```

## BFC

- [BFC神奇背后的原理](https://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)
- [10分钟理解BFC原理](https://zhuanlan.zhihu.com/p/25321647)

- 在正常流中的盒子都有所属的格式化上下文，对于块级元素，对应 BFC (Block Formatting Context)，块级格式化上下文。
- BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有 Block-level box 参与， 它规定了内部的 Block-level Box 如何布局，并且与这个区域外部毫不相干。
- BFC 触发条件
  - body 根元素
  - 浮动元素：float 除 none 以外的值（被移出正常文档流）
  - 绝对定位元素：position (absolute、fixed)（被移出正常文档流）
  - display：inline-block、table-cells、flex
  - overflow： 除了 visible 以外的值 (hidden、auto、scroll)
- BFC 原理
  - 内部的块级盒子会在垂直方向（正常流方向）依次换行放置
  - 同一个 BFC 下的毗邻的块级 box 的竖直 margin 会发生折叠
  - BFC 不会与 float box 重叠，浮动元素会被包裹在 BFC 内（BFC中浮动元素可以撑起BFC高度）
  - 每个元素的 margin box 的左边， 与包含块 border box 的左边相接触
  - 创建了BFC的元素不会与它的子元素发送 margin 折叠
- BFC应用
  - 浮动清除
  - 自适应两栏布局
  - 竖直方向margin折叠的解决

## 外边距折叠

- 外边距折叠 Margin Collapse 的条件
  - 同一个 BFC 内的块级盒子
  - 两个或多个，相互折叠
  - 毗邻
  - 垂直方向，水平方向的margin不会发生折叠的现象
- 外边距叠加存在两种情况：一是父子外边距叠加；二是兄弟外边距叠加
- 父子叠加发生于(content-box)
  - 父元素padding为0，父元素和第一个块级子元素的margin-top会作为父元素的margin-top
  - 父元素和最后一个块级子元素的 margin-bottom

- 同一个BFC内正常流的块级元素才会可能边距叠加，则可以
  - 脱离正常流=》设置元素本身浮动
  - 脱离正常流=》设置元素为绝对定位
  - 非块级元素=》设置元素为inline-block
- 创建了BFC的元素不会和它的子元素发生外边距叠加，则可以通过这四种方式创建 BFC
  - float（除了none）
  - overflow（除了visible）
  - display（table-cell/table-caption/inline-block）
  - position（除了static/relative）

- [外边距折叠的解决方法](https://www.yuque.com/nepjnq/fgeemd/uyyazr)
  - 兄弟叠加
    - 令元素本身为 display:inline-block、position:absolute、float，这种方案对元素本身布局影响较大，因此更常见的方法是为元素设置外部BFC容器
    - 给每个元素设置外部BFC容器：对每个元素设置外部容器，容器上使用 display:inline-block、position:absolute、float 、overflow 之一
  - 父子叠加
    - 这种方案对元素本身布局影响较大，因此更常见的方法是为元素设置外部BFC容器， 实际少用
    - 让父元素创建 BFC
    - **设置父元素的padding-top、border-top**，避免毗邻状态

## containing block

- 包含块（containing block）就是元素用来计算和定位的一个框
  - 根元素（很多场景下可以看成是`<html>`）被称为“初始包含块”，其尺寸等同于浏览器可视窗口的大小
  - 对于其他 `relative` 或者 `static` 元素，则“包含块”取决于最近的块级祖先的 content box（因此 BFC 中的块级元素在没有创建自己的BFC时，元素margin box边界与祖先的content box边界相接）
  - 如果元素 `position:fixed`，则“包含块”是“初始包含块”，即固定定位元素相对于 `<html>` 的 border box 进行定位
  - 如果元素 `position:absolute`，则“包含块”由最近的非static的定位祖先确定，块级别元素的包含块由该祖先的 padding box 边界形成（因此绝对定位元素相对于父定位元素的 padding box 定位）

## 定位方式

- static
  - 默认值，正常文档流定位，此时 top/right/bottom/left/z-index 属性无效，
  - 块级元素从上往下纵向排布，行级元素从左向右排列
- relative
  - 相对定位，仍然处于正常文档流中，
  - 单独声明没有效果，需使用 top/right/bottom/left/z-index 表示元素相对于正常位置的偏移
- absolute
  - 生成绝对定位的元素，相对于包含块的 padding box 进行定位，如果没有，则是`<html>`元素
- fixed
  - 固定定位，生成绝对定位的元素，但是始终相对于初始包含块定位，即 `<html>`，
  - 这种情况与绝对定位区别：固定元素会始终相对于当前可视窗口固定，不随文档滚动，而绝对定位元素会随文档滚动
- sticky
  - 粘性定位，元素开始表现得像相对定位，直到滚动到某个阈值点后固定，可实现吸顶效果，必须配合 top/right/bottom/left 指定元素相对于最近滚动框（overflow :auto/scroll）的偏移，当元素盒子滚动后满足该值后（实测）：
    - 滚动祖先是初始包含快：相对于可视窗口固定定位
    - 其余情况：相对于滚动祖先的 content box 固定定位
  - 为了避免多个滚动互相嵌套式定位混乱，滚动框的父元素不能有 `overflow:visible` 以外的值

## 层叠上下文 stacking context

- 层叠上下文是渲染时的三维概念，类似BFC，但此时的渲染空间在 z 轴上。
- A stacking context is formed, anywhere in the document, by any element in the following scenarios:
  - Root element of the document (`<html>`)
  - position relative/absolute + z-index非auto
  - position fixed/sticky
  - display flex/grid + z-index非auto
  - opacity < 1 
  - transform/filter/perspective/clip-path/mask 属性值不为 `none` 时
  - Element with a `will-change` value specifying any property that would create a stacking context on non-initial value
  - Element with a `contain` value of `layout`, or `paint`, or a composite value that includes either of them (i.e. `contain: strict`, `contain: content`)

- z-index默认值为 `auto`，不会创建一个新的本地堆叠上下文。当前堆叠上下文中生成的盒子的堆叠层级和父级盒子相同
- z-index order 从远到近靠近用户/屏幕的顺序
  - background/border
  - z-index negative
  - block element
  - float element
  - inline element
  - z-index auto 或 0 (一般是非静态定位元素)
  - z-index positive

## float

- 浮动元素会脱离正常的文档流
  - 当父元素内都是浮动元素时，会造成父元素塌陷的问题——父元素高度为0，因为此时等同于父元素内容为空，所以高度为0
- 普通块级盒子会默认在内联的方向上扩展并占据父容器在该方向上的所有可用空间。但浮动盒子则完全相反，宽度只会满足包裹内容

- ❓️ 如何清除浮动：
  - 实际上闭合浮动是更准确的说法，要解决的问题：当浮动框高度超出包含框时，包含框不会自动伸高来闭合浮动元素（“高度塌陷”现象）。清除只是一种达到闭合浮动的途径。
- 👉🏻️ clear:both
  - 在最后一个浮动子元素后添加 `<div style="clear:both; "></div>`，`clear` 属性指定一个元素是否必须移动到在它之前的浮动元素下面。配合一个空div可以实现撑开父元素
- 👉🏻️ clearfix::after 伪元素法
  - 在浮动元素父容器上添加`clearfix`类，使用`::after`创建一个父容器的伪元素，效果等价于上面

```CSS
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
```

- 👉🏻️ overflow
- 使用 `overflow: auto 或 overflow: hidden`，利用 BFC 元素会包裹其中 float 元素的性质

## 盒模型

- 正常流中不同的元素会被赋予不同的盒子，主要有：块级盒子 (block box) 和 内联盒子 (inline box)
- box-sizing默认值是content-box，而不是border-box

- CSS万物皆盒子，对盒子本身和盒内元素行为的描述对应两类显示类型
  - 外部显示类型：块级或内联，可通过 `display:block` 和 `display:inline` 设置
  - 内部显示类型：默认情况下盒内元素按照正常流布局，遵循和块级与内联盒子一样的布局。设置`display:flex` 可更改盒子内部显示类型为 flex， 盒子的所有直接子元素都会成为 flex item，根据弹性盒模型布局

## flexbox

- flexbox弹性盒是一种用于按行或按列布局元素的一维布局方法，元素可以膨胀或收缩以弹性地适应空间。
  - 弹性盒模型的优势在于开发人员只是声明布局应该具有的行为，而不需要给出具体的实现方式，浏览器负责完成实际布局，
  - 当布局涉及到不定宽度，分布对齐的场景时，就要优先考虑弹性盒布局

## css继承

- 可继承性的属性：
（1）字体系列属性：font、font-family、font-weight、font-size、font-style、font-variant、font-stretch、font-size-adjust
（2）文本系列属性：text-indent、text-align、text-shadow、line-height、word-spacing、letter-spacing、text-transform、direction、color
（3）表格布局属性：caption-sideborder-collapseempty-cells
（4）列表属性：list-style-type、list-style-image、list-style-position、list-style
（5）光标属性：cursor
（6）元素可见性：visibility
（7）还有一些不常用的：speak，page，设置嵌套引用的引号类型quotes等属性

- CSS 为控制继承提供了四个特殊的通用属性值，每个css属性都可以接收这些值：
  - initial：无论该属性是否可自然继承，都还原属性值为其默认样式
  - inherit：设置该属性会使子元素属性和父元素相同，即手动继承
  - unset：将属性重置为自然值，如果属性本身可自然继承那么就是 inherit，否则同 initial
  - revert：新属性，用于回滚层叠，属性就会采用当前样式源中没有样式时的值

## line-height属性本身可以继承

- 该属性决定了：
  - 块级元素的最小 line-box 高度
  - 非替代行内元素的 line-box 高度
- line-height 常用 em、数字、百分比为单位
  - 使用百分比时，子元素均以该 父元素font-size*百分比 作为子元素 line-height
  - 使用数字时，子元素均以 自身font-size*百分比 作为子元素 line-height

## rem 使用

- 如何去根元素的font-size大小，才能让页面在不同屏幕大小看起来一致

```HTML
<meta name=”viewport” content="width=device-width, initial-scale=1">
<script type="text/javascript">
  let cw = document.documentElement.clientWidth;
  document.documentElement.style.fontSize = 32 * (cw / 640) + 'px';
</script>
```

- 1rem = 16px
- 之后的元素都是用 rem 布局：设计稿上 160px 的元素
  - 不同宽度的设备，修改 body font-size的值

## 元素的宽高

- clientWidth/Height（包括元素宽度、内边距，不包括边框和外边距）
- offsetWidth/Height（包括元素宽度、内边距和边框，不包括外边距）
- getBoundingClientRect().width/height （等于 offsetWidth/Height）
- scrollWidth/Height（包括元素宽度、内边距和溢出尺寸，不包括边框和外边距）

- offsetTop
  - dom.getBoundingClientRect().top：获取的是元素距离视口顶部的距离
  - offsetTop 得到的是当前元素距离被定位父元素 offsetParent（即使用了 fixed/absolute/relative）padding top 的距离，当未找到 offsetParent 时，则将 `<body>` 作为 offsetParent

- 获取页面可视区大小
  - document.documentElement.clientWidth/Height

- 判断元素未进入/进入/离开可视区
- 💡️方法1: getBoundingClientRect()

```JS
// 未进入，此时元素在视口之下
dom.getBoundingClientRect().top > document.documentElement.clientHeight
// 已离开
dom.getBoundingClientRect().top + dom.offsetHeight < 0
```

- 💡️方法2: 计算偏移量

```JS
// 未进入
dom.offsetTop >
  document.documentElement.clientHeight + document.documentElement.scrollTop
// 已离开
document.documentElement.scrollTop > dom.offsetTop + dom.offsetHeight
```

## transform

- 允许旋转，缩放，倾斜或平移给定block元素
- 如果动画中使用transform进行元素坐标和大小调整时无需重排reflow和重绘repaint，对应图层已经被计算出

## transition

- property：指定施加过渡的属性
- duration：指定状态改变持续时间
- delay：触发到真正状态改变的推迟
- time-func：速度函数，默认非匀速

- 局限
  - transition需要事件触发，所以没法在网页加载时自动发生
  - transition是一次性的，不能重复发生，除非一再触发
  - transition只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态
  - 一条transition规则，只能定义一个属性的变化，不能涉及多个属性

## animation

- 大部分animation属性类似transition，其中：
  - name：指定应用的一系列动画，每个名称代表一个由keyframes定义的动画序列
  - fill-mode：设置动画在执行之前和之后如何将样式应用于其目标
  none为回到动画未开始状态
  - backwards/forwards是回到并保持第一或最后一帧动画
  - direction：这是动画运行方向
  - iteration-count：指定动画迭代次数0~infinite

- keyframes关键字用来定义动画的各个状态，百分比对应了duration的执行情况，0%可以用from代表，100%可以用to代表
- animation-play-state属性可以设置动画执行时的状态，默认是回到初始状态

## requestAnimationFrame

- rAF() 可以用来执行无限循环的动画，但是其回调的间隔固定为每秒60次，为了实现精确计时，需要稍微设置：

## 自动轮播

- 基于animation和@keyframes
