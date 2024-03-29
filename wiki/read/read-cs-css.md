---
title: read-cs-css
tags: [book, cs, css, read]
created: 2020-06-30T04:05:22.389Z
modified: 2020-12-08T14:44:40.651Z
---

# read-cs-css

# book-CSS实战手册. 第4版_David McFarland_2016

- css-toc
  - css基础：选择器(层叠规则) + 盒模型 + 定位布局
  - 常用功能：文本+图片+动画
  - 页面布局：float/flexbox/css grid/响应式设计
  - 高级功能：sass

- CSS(Cascading Style Sheets)是一种用来为结构化文档（如HTML文档或XML应用）添加样式（字体、间距和颜色等）的计算机语言，由W3C定义和维护
- html提出的目的是以一种易于理解的结构组织页面内容
  - 只负责内容的结构，可以控制部分外观，但不建议使用html来控制外观
  - html标签用于标记各部分内容的作用，要尽量体现作用，ul可用css调样式为横向
- css的作用是控制页面的外观和布局
- IE8及之前的版本不支持html5的新增标签，微软于2016年1月停止支持IE8
- 不推荐使用的html标签
  - font > css
  - b, i > strong, em
  - 布局使用table标签 > css
  - br > 块级元素
  - 不要使用任何仅用于改变文字或图像外观的标签和属性，该用css 
- 推荐使用语义化标签
  - 用于标记元素的通用标签：div, span
  - blockquote
  - article
- html5的文档类型声明： `<!doctype html>`
- css版本
  - css1
    - 1996年发布，定义了样式基本结构，提出选择符
  - css2
    - 添加了媒体查询
    - 新增了选择符
  - css2.1 
    - 所有浏览器都实现的这一版
  - css3 标准模块化
    - 选择器模块
    - 盒式对齐模块
    - 值和单位模块
- 样式规则包括两部分：选择器，装饰指令声明
- 浏览器会忽略空格和制表符
- 样式表
  - 外部样式表：推荐使用，所有样式保存在单独的文件，可以缓存，ctrl+F5不使用缓存
    - `<link rel="stylesheets" href="path/to/style.css">`
  - 内部样式表：放在 `<head>` 标签内的 `<style>` 标签中
  - 行内样式：不推荐使用，可复用性差，多用于测试

- selector 选择器
  - [CSS选择器笔记_阮一峰](http://www.ruanyifeng.com/blog/2009/03/css_selectors.html)
  - 元素选择器：可选取所有指定html标签，不够精细
  - 类选择器：以 `点号` 开头，类名区分大小写
  - ID选择器：以 `#号` 开头，尽量不用id选择器，用类选择器
  - 通用选择器： `*号` 表示选择所有元素标签，也可作为后代选择器的部分
  - 群组选择器：多个选择器用 `逗号` 分开，选择各选择器指定的元素并集，可混用多种选择器
  - 后代选择器：多个选择器用 `空格` 分开，选择一个标签的所有后代，包括子代和孙代
  - 子代选择器： `el1 > el2` ，只选择直接子代，不选孙代
    - 还可以使用伪类，如:first-child，:nth-child(n)
    - tr:nth-child(odd/even/3n+X/-n+2/9)
    - 子代类型选择器：选取的是特定类型的子代标签，如 `.sidebar p:first-of-type`
  - 同级选择器
    - `+` ：紧邻元素选择器，E+F选择紧随E元素之后的第一个同级元素F，只会影响后面对应标签的第一个（相邻的）兄弟节点的标签样式，若是li+li,则会影响除第一个li的所有li
    - `~` ：普通同级元素选择器，E~F选择E后的所有同级F，若是li+li则除第一个都影响
    - [CSS的兄弟选择器+和~的区别](https://blog.csdn.net/jarisMA/article/details/100105595)
  - 属性选择器
    - `el[attrName]，.class[attrName]`,可以筛选出设定了特定属性的标签 
    - `el[attrName="value"]`，还可以选取属性值以特定值开头 `^=` 、结尾 `$=` 或包含指定值 `*=` 的元素
    - el[att~=val]匹配所有att属性具有多个空格分隔的值、其中一个值等于val的E元素
  - 伪类 :link/visited/hover/active/focus，:first-child，:enable/checked
    - 反选伪类：用于选择不符合指定条件的标签，如el:not(.clsName),not不用连用
    - 结构性伪类:	E:root, E:nth-child(n)
    - E:target,	常用于点击后让另一个元素具有特殊的外观，依赖于id属性，功能类似js
  - 伪元素 ::before/after, ::first-letter/line, ::selection
    - 伪类和伪元素用来选择页面中不由标签表示但易于标识的部分

- 通过css继承来简化样式表
  - 影响元素在页面所在位置的属性，以及外边距、背景色和边框的属性不会被继承
    - border属性不会继承
  - 样式冲突时，优先使用特指度更高的
- cascade 层叠  
  - 用于控制样式之间相互作用的方式，具体通过比较样式的优先级
  - 继承时默认使用最近父辈的样式
  - 特指度specificity：样式所依赖的所有选择器得分的和
    - 行内样式：1000
    - id选择器：100
    - 类选择器：10
    - 元素选择器：1
  - 特指度相同时，使用后声明的选择器，注意外部样式表和内部样式表的位置
    - 最好先链接外部样式表，仅当需要在单个页面中添加样式时才使用内部样式表
  - 若要忽略特指度，只需在某个css属性之后分号前添加 `!important` ，只作用于单个属性
    - 不推荐使用
- css reset 重置
  - 浏览器为所有html标签提供了默认样式，不同浏览器实现的默认样式会有差异
  - 清除浏览器内置样式这种行为称为css重置
  - css重置其实就是在样式表开头放一些核心标签的样式，在这些样式中设置在各种浏览器中表现不一致的属性，统一基准 
  - https://github.com/necolas/normalize.css
- 使用字体 font-family
  - `p { font-family: Arial, "Times New Roman", sans-serif, serif; }`
  - 使用font-family指定首选字体和后备字体，只能使用电脑中已经安装的字体
  - 若计算机未安装指定字体，则使用浏览器的默认字体
  - 可以使用web font，先获取字体文件，再用@font-face指令说明字体名称和下载地址
    - google fonts
    - Adobe Typekit 可将字体同步至你的电脑或网站当中
    - 其他：Open Sans、Lato、PT Sans、Lobster、Rokkitt
    - 最好指定后备字体
    - 字形和变体会加大工作量
  - 通用字体：Arial，serif，sans-serif
- 常用字体
  - 衬线字体：serif，"Times New Roman", Georgia
  - 无衬线体：sans-serif，Arial，Helvetica，Verdana
  - 等宽字体：monospace，Courier，常用于显示代码
- 字体类型
  - eot：ie5开始支持的字体，只有ie支持
  - ttf和otf：常用电脑字体
  - woff/2：web开放字体格式，体积小，大概是ttf的一半，所有现代浏览器都支持
  - svg字体：浏览器支持十分有限，体积是ttf的两倍
- html支持的颜色名称 color
  - https://developer.mozilla.org/zh-CN/docs/Web/CSS/color_value
  - rgba和text-shadow，box-shadow联合使用，ie8之前不支持rgba
- 字号 font-size
  - px：最常用，与浏览器的设置无关
  - 关键字：xx-small, medium(=16px), x-large
  - em：与%原理相同，1=100%
  - rem：字号的大小基于根元素而定，通常基于基准字号16px，但可以为根部html元素设置20px后，其他元素就可以使用rem来设置百分比了
  - %：100%==16px
  - 对像素字号来说，在有视网膜显示屏的设备中，浏览器会把设定的像素值乘以2 
  - 若样式表未设定字号，则使用浏览器预设字号，默认是16px
  - em、百分比、关键字的设置字号方式会在浏览器预设字号的基础上增大或减小
  - 修改基准字号要调整浏览器的偏好设置
- 字体操作技巧
  - text-transform : uppercase/capitalize/none
  - text-decoration: underline/line-through/none
  - letter-spacing：0.1em; 字符间距，中文文字间距
  - word-spacing：2px/em/%    单词间距，用空格隔开的中文也是单词，若无空格则无效果
  - text-shadow: 横偏移 纵偏移 阴影模糊度 投影颜色，为文本添加投影
  - line-height: 150%； 推荐使用百分比，默认值为120%
  - text-indent： 缩进
- list  
  - ul默认3种符号：circle空心圆形，disc实心圆形，square实心方形
  - ol默认6种编号：decimal(-leading-zero), alpha, roman
  - list-style-type：指定编号类型
  - list-style-position: 控制符号位置
  - list-style-image：只能指定图形，不能控制位置

- css盒模型
  - box = content + padding + border + margin
  - background-color包括padding和border
  - 如果边框的样式是点划线或虚线，点划线和虚线的空隙之间能看到背景色，要避免这种情况可使用 `background-clip: padding-box;`
- 外边距折叠
  - 外边距用来指定非浮动元素与其周围盒子边缘的最小距离
  - 两个或两个以上的相邻的垂直外边距会被折叠并使用它们之间较大的那个外边距值
  - 把外边距设为负值还能模拟负的内边距
- 块级元素与行内元素
  - 可用左右内外边距在行内元素的左右添加空白，但不可用上下外边距增加行内元素的高度
  - display：inline-block，元素前后无换行，且能设置上下内外边距和高度
  - display:none，在载入网页的时候会忽略这个元素，不会下载其内容，无宽高
  - visibility:hidden，视觉上隐藏元素，但在浏览时保留位置空间，具有宽高
- border
  - 浏览器将所有元素视为盒子
  - box-shadow在盒子的外边界添加阴影
- 一般来说，不要设置元素在页面中的高度，设置了要考虑指定overflow，还要测试不同字号
- overflow
  - 指定如何显示超出盒子边界的内容
  - visible：默认值。相当于不设置overflow属性
  - scroll：一直显示滚动条，即使比盒子内容小也显示
  - auto：需要时才显示滚动条
  - hidden：隐藏超出盒子边界的内容
- float
  - float把元素移到外层元素左侧或右侧，浮动元素下面的内容会上移，围绕在浮动元素周围
  - 浏览器对浮动的行内元素的处理方式与块级元素一样
  - 浏览器只会让文字围绕浮动的元素显示，而不包括边框或背景，解决方法
    - 为浮动元素下面设置了背景或边框的元素添加 `overflow:hidden`
    - 在浮动元素的四周添加边框线，将边框颜色设为与背景色相同
- clear属性告诉元素不要围着浮动的元素显示，作用是强制让元素显示在浮动的元素下面
  - none: 默认值，不清除浮动
  - left: 让元素显示在左浮动的元素下面，不过仍然围着右浮动的元素 
- box-sizing
  - 盒子模型的默认定义，对一个元素所设置的width与height只会应用到content
  - content-box：默认值。 设置的宽度 = contentWidth，不包含padding, border, margin
  - border-box：设置的宽度 = contentWidth+padding+border，不包含margin
    - 使用方便

- 背景图片
  - `background-image: url('path/to/a.jpg')`
  - url的路径可绝对可相对，相对路径是相对样式表文件位置而言
    - 而不是相对要应用样式的html文件而言
    - 以 `./` 开头为相对当前样式文件，以 `/` 开头为相对根目录
  - background-repeat可以控制平铺方式，round和space作为值可禁止裁剪
  - 定位属性
- css sprite
  - 在一个图像中包含不同状态
  - 浏览器发送一个大文件要比发送多个小文件体验好
- transform 变换
  - 类型：缩放scale、平移translate、旋转rotate、倾斜skew
  - skew可用于实现3D效果
  - skewX和skewY分别沿X轴、Y轴倾斜，而skew(top, right)分别沿上边与右边倾斜，还可用矩阵控制更精细的变换
  - 多个变换方法用逗号隔开
  - 默认情况下，浏览器以元素中心作为变换的原点，transform-origin可改变原点
  - 3D变换有专门的主题
- transition 过渡
  - 过渡是一种简单的动画，在一定时间内从一组CSS属性变成另一组属性，IE10后才支持
  - 支持过渡的属性包括上面的变换，还包括 animatable properties
  - 属性：transition-property/duration/timing-function/delay
  - 过渡效果需要使用css选择器触发，如:hover, :focus，若想点击触发需要使用js
  - cpu友好型的变换包括不透明度、缩放、平移、旋转
  - 可以通过加入无实际视觉效果的 `transform: translateZ(0);` 来利用GPU加速渲染
- animation 动画
  - 过渡只能把一系列css属性从一个状态变到另一个状态，动画则能从状态1 > 2 > . > N
  - 动画可重播，动画无需触发就可播放，过渡只可播放一次
  - 通过 `@keyframe` 定义一系列状态
  - 暂停动画可在css伪类中使用 `animation-play-state: paused` ，更常用js
- table 表格
  - 不推荐使用table布局，css布局更灵活，表格本来的用途是显示数据
  - text-align控制横向对齐，会被继承
  - vertical-align控制纵向对齐，不会被继承
  - 若不明确禁止，浏览器会在单元格间添加几像素宽的间隙，为单元格添加边框后间隙会变明显
  - 如果去掉了单元格之间的间隙，单元格的边框会叠到一起，宽度加倍
  - 列的背景在单元格后面，注意覆盖顺序 

- 页面布局的类型
  - 固定宽度布局：不管浏览器窗口多宽，页面内容的宽度始终一致，不适合移动端
  - 流式布局：宽度使用百分比设定，难以确保在各种尺寸的窗口中都美观
  - 响应式设计：使用css技巧如media query为不同宽度的浏览器提供不同的布局
  - 传统布局方式：table + div
  - 很多网页都使用float实现布局
  - 也可以使用absolute position把元素定位在页面的任意位置
    - 使用绝对定位难以控制整体布局
- 布局策略
  - mobile first
  - 先画草图，确定盒子内容
  - 使用纵向常规文档流
  - 分层显示元素
- 基于float的布局
  - float的作用是把元素移到页面（或容器）的某一边。
    - 浮动元素后面的HTML代码会上移，围绕着浮动的元素显示
    - 浮动元素的HTML代码必须在围绕浮动元素显示的HTML代码之前
    - 如果不是浮动有既定宽度的图像，一定要为浮动的元素设定宽度。
    - 浮动的元素有固定的宽度，浏览器才能留出空间显示围绕它的内容。宽度可以是定值或百分比
  - 浮动所有分栏时，要特别留意各栏的宽度。
    - 如果所有分栏的宽度之和大于可用空间，例如浏览器窗口较窄，或者分栏在一个宽度固定div标签里，那么最后一栏会下坠，显示在其他分栏下面
    - 浮动的元素必须在围绕其显示的内容之前，因此在示例中，主内容区必须在所有侧边栏后面
  - 在浮动的元素中浮动，可以把一栏分成多栏
  - 处理溢出的4种方式
  - 多栏布局：column-count/gap/rule
  - box-sizing:border-box能避免浮动下坠
- position 定位
  - static：默认显示方式，从上到下
  - relative：相对于该元素在常规文档流的位置，原先的位置会留空
  - absolute：脱离文档流，绝对定位元素的位置是相对于最近的祖先定位元素的边界而定的
  - fixed：脱离文档流，将元素固定在屏幕某个位置
  - 隐藏元素的3种方式:display, visibility, opacity
- responsive 响应式设计
  - 媒体查询：为不同宽度编写不同样式
  - 弹性栅格布局：小屏单栏，宽屏多栏
  - 弹性媒体：自适应图片或视频，暂无标准的解决方案 
  - 对非响应式桌面网页，移动浏览器会自动缩小页面来显示整个网页，有时很难阅读
  - 把width属性的值设为auto，与设为100%差不多，作用是让元素与容器一样宽 
- media query 媒体查询
  - 根据浏览器宽度或高度为页面提供不同样式
  - 使用场景：调整分栏、弹性宽度、导航目录、隐藏内容
  - breakpoint：切换样式的宽度
  - 创建方式 link+media, @media
- 栅格系统
  - 布局栅格是有条理的行和列，对css来说，栅格系统是预先定义好的样式表
    - 栅格是种把内容组织到行和列中的方式，而且各列的宽度是一致的
    - 先把页面的整个宽度分成一系列“单元”，然后自由组合单元，形成不同宽度的分栏
    - 大多数css栅格系统都使用百分比值定义单元的宽度 
    - 常用的单元数是12，一个单元大约是页面总宽度的1/12
  - 使用一系列嵌套的div标签实现三种不同的页面布局元素
    - container: 可包含一行或多行，常使用max-width
    - row：放在container中，一行可包含一列或多列
    - column：一行里的一个div
  - Skeleton是一个响应式栅格系统
    - 它允许在页面中放置多栏，但是当浏览器窗口的宽度小于550px时，会纵向排列各个分栏
    - 使用12个单元格
    - 没有延伸container样式的宽度到窗口的边界，可在外层添加div，并在外层div设置背景色
- flexbox 弹性盒
  - 弹性容器的每个直接子代都会自动变成弹性项目
    - 弹性容器不是块级元素，因此有些属性不能用到弹性容器或项目上
      - column属性不能用到弹性容器
      - float,clear不能用到弹性项目
  - 使用建议
    - 把所有弹性项目放在一行里
    - 保持一行里各个项目的宽度比例，但是当容器太窄，无法并排显示项目时，允许换行
    - flex-basis的值用于确定何时换行，可以结合断点设计
- css grid
  - display:grid
- css使用建议
  - 能够简写的属性：font，padding，margin，background
  - 重置浏览器的默认样式 css reset
- sass
  - 嵌套选择器
  - source-map
# book-CSS设计指南. 第3版_Charles Wyke-Smith_2013
- toc
  - 选择器
  - 盒模型
  - 文本
  - 布局
- html的闭合标签常用于显示文本，自闭合标签常用显示引用内容
  - 闭合标签包含的是会显示的实际内容，
  - 而自闭合标签只是给浏览器提供一个对要显示内容的引用 
- css规则： `选择符 { prop: value }`
- 通用选择符 `*` 可以匹配任何元素
- id选择器和类选择器可以不用考虑文档结构层次
- 多类选择器 `.clsA.clsB` ，无空格，取交集，即选择同时具有clsA和clsB类名的元素
  - 若加了空格，则会变成后代选择器
  - 也可以是 `el.clsName`
- id也可以用在页内导航链接中
  - 使用 `<a href='#id'>` 可以链接到同一页面的目标id元素位置
  - 若属性中只有一个井号 `<a href='#'>` ， 则会返回顶部
  - `href=""` reloads the page
  - `href="#"` adds an extra entry to the browser history, 多次点击后只用返回一次
  - `href="javascript:;"` works in both Android and iOS webviews, 也不添加历史记录
  - [Is an empty href valid?](https://stackoverflow.com/questions/5637969/is-an-empty-href-valid)
- pseudo-class: link, visited, hover, active, focus, first-child
- pseudo-elements: before, after, first-letter/line
- 搜索引擎不会取得伪元素的信息（因为它在标记中并不存在）
  - 因此，不要通过伪元素添加你想让搜索引擎索引的重要内容
- css层叠规则提炼版
  - 找到应用给每个元素和属性的所有声明
  - 按照来源顺序排序
  - 按特指度specificity排序
  - 顺序决定权重：若特指度相同，则后声明的规则会生效
- css层叠规则实践版
  - id选择器优先于class选择器
  - 行内样式优先于内外部样式表
  - 设定的样式优先于继承的样式

- 盒模型，就是浏览器为页面中的每个HTML元素生成的矩形盒子
  - 这些盒子按照visual formatting model在页面上排布
- visual formatting model主要与3个属性相关
  - position控制元素间的位置关系
  - display控制元素的堆叠、并排、隐藏
  - float控制元素浮动
- 每个元素都会在页面上生成一个盒子，页面由盒子组成
  - 默认所有盒子边框不可见，背景透明，所以不能直接看到盒子结构
  - border属性默认值
    - border-width:medium
    - border-style:none，默认不显示边框
    - border-color:black
    - border-radius不影响盒模型的定位
  - padding包含盒子的背景
  - 垂直方向上的外边距margin不会叠加，会使用二者的较大值
  - 不同浏览器默认的内外边距不同，特别是对表单和列表等复合元素，建议使用css重置
  - 垂直外边距会折叠，但水平外边距正常叠加
- 若不设置块级元素的width，则默认值为auto，即元素宽度会扩展到填满父元素的宽度
- 盒子的width默认是content的宽度，padding、border、margin都会加宽盒子

- float
  - 浮动元素脱离了常规文档流之后，原来紧跟其后的元素就会在空间允许的情况下，向上提升到与浮动元素并排
  - css设计float的目的是为了实现文本绕排图片的效果
  - 浮动非图片元素时，必须给它设定宽度，否则后果难以预料。图片本身有默认的宽度。
  - 如果几个相邻的元素都具 有设定的宽度，都是浮动的，而且水平空间也足以容纳它们，它们就会并列排在一行
  - 浮动元素脱离了文档流，其父元素也看不到它了，因而也不会包围它
- 围住浮动元素的方法
  - 给父元素添加 `overflow:hidden` ，强迫父元素包含浮动的子元素
    - 不能在下拉菜单的顶级元素上使用
  - 让父元素也浮动，设置父元素width:100%，对不希望提升的元素clear
    - 不能对已经靠外边距居中的元素使用
  - 给父元素最后添加一个非浮动的子元素，然后给子元素添加clear
    - 由于包含元素一定会包围非浮动的子元素，而且清除会 让这个子元素位于（清除一侧）浮动元素的下方，因此包含元素一定会包含这个子元素——以及前面的浮动元素
    - 可以给父元素新添加最后一个子元素div并clear:left
    - 还可以通过伪元素:after给父元素添加一个无高度且clear过的伪元素

```CSS
.clearfix:after {
  content: ".";
  display: block;
  height: 0;
  visibility: hidden;
  clear: both;
}
```

- position
  - static：默认方式，每个元素都处在常规文档流，自上而下堆叠
  - relative：相对于元素在常规文档流中的位置，距离常规文档流位置的上边/左边
  - absolute：绝对定位的元素脱离了文档流，相对于定位上下文进行定位
    - 默认定位上下文是body元素
    - 此外会寻找最近的postion为relative的祖先元素作为定位上下文
  - fixed：脱离了文档流，定位上下文是浏览器窗口或屏幕，不会随页面滚动而滚动
  - 在常规文档流中，若外部div没有内容，内部div就会跟它共享相同的起点。只有将元素的position属性设定为relative、absolute或fixed，这个元素的 top、right、bottom 和 left 属性才会起作用
  - 若未设置外层元素的position为relative/absolute/fixed，则内层元素的left/top等定位属性不会生效，会被忽略，默认都是static定位，内层div会和外层div同左上角起点
  - 常用的定位模式是：外层relative，内层absolute
  - float元素也会脱离文档流

- background-color会应用到内容背景和padding背景，color前景色会应用到内容和边框

- 页面布局
  - 一般不应该给元素设定高度，保持height属性默认值auto
    - 若明确设置了高度，则会根据overflow属性判定
  - auto能使元素随着自己所包含内容的增加而在垂直方向扩展，若设置了高度则会滚动条
  - 块级元素的宽度默认填满父元素宽度 
- 在一个包含多个同辈元素的容器内，这些同辈元素都会构造一个堆叠上下文，
  - 在这个上下文中，它们的子元素会上下堆叠起来，z-index属性用于控制元素的在堆叠上下文中的次序
- 响应式设计的要点
  - 媒体查询
  - 流式布局
  - 弹性图片
- 媒体查询
  - 媒体类型：screen，print，handled，tv，tty，all，...
  - 媒体特性：min/max-device-width，min/max-width，orientation
  - 可以使用逻辑运算符 and、not、or 及关键字 all、only 组合媒体类型和媒体特性
- breakpoint指的是媒体查询其作用的宽度
  - `@media screen and (max-width:640px)`
  - 不要针对某款具体的设备设置断点，要慢慢缩小浏览器窗口，为某个宽度范围的屏幕提供样式
- `<meta name="viewport" content="width=device-width; maximumscale=1.0" />`
  - 告诉浏览器按照屏幕宽度来显示网页，不要缩小网页
- 支持触摸的设备会跳过:hover规则中对visibility属性的过渡
  - 解决方案是使用modernizr检测设备是否支持触摸，若不支持，则去掉相关样式
