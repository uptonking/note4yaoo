---
title: web-style
tags: [style, web]
created: '2019-08-05T11:51:59.761Z'
modified: '2021-04-23T17:10:55.308Z'
---

# web-style

# summary

- css要点
  - 各类选择器
  - 样式层叠规则
  - 盒模型与元素定位
  - 布局
    - 基于float
    - 基于flexbox
    - 基于css grid
  - 动画与变换

# pieces

- 全局基础样式的内容(类似styled-system提供的)
  - text, color, space, layout, border 
- flexbox vs css grid
  - Layout可以考虑Grid来做，单个Component中的东西可以考虑Flexbox来做
  - grid的兼容性chrome要57以上才能兼容，ie就呵呵，相比之下flex稍微好点
- tailwind css vs Atomic CSS
  - 都是类似css原子类的语法，但Atomic CSS写起来包含大小写和括号太丑
  - css原子类增加了记忆成本，效果和行内样式一样，仅仅是减少了需要拼写的字符数量
    - CSS原子类就基本等同于变相写inline style内联样式
    - gzip压缩后减少的体积并不大
    - **过于细碎**的原子类降低了可读性，类名过长，要严格控制数量，避免记忆压力
    - 维护工作量大，一旦修改属性值，要修改所有类名，因为类名中常包含数字，如m20
    - 修改常增加新类名
  - 参考 https://www.zhihu.com/question/22110291
- postcss vs sass
  - sass是css预处理器，支持现在css不支持的语法，方便高效编写可复用的css
    - compass库为sass操作css提供更多工具函数，but deprecated
  - postcss是css处理工具，是个开放的平台，通过插件提供处理css的方法
    - precss插件提供类似sass语法
    - autoprefixer向CSS规则添加浏览器厂商前缀
    - stylelint校验css
    - postcss-assets可以方便管理文件资源，自动更改url路径
    - cssnano优化压缩css
    - https://github.com/postcss/postcss/blob/master/README-cn.md
- transform translate() vs translate3d()
  - 移动距离要写单位，3d在移动设备上也可以使用硬件加速
  - translate3d should be faster in a lot of browsers, mostly those that use gfx hardware acceleration to speed up rendering. especially on webkit translate3d was the prefered way of forcing hardware acceleration on page items.
  - there is one drawback to using 3d transforms - in certain browser-versions/os combinations hardware accelerated rendering can slightly alter font smoothing as well as interpolation thus causing minor flicker or blur. those situations can mostly be worked around but should be kept in mind.
  - 3d移动时若包含z方向或使用百分比，有时会出现字体模糊，参考下面链接中的例子
  - https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate3d
  - https://segmentfault.com/q/1010000002926369
  - 3D变换会开启GPU加速，GPU加速动画时，并不是把原生DOM传递给GPU，它生成一个元素图像，把该图像发送到GPU，GPU将图像应用为多边形纹理贴图代表元素，GPU可以流畅快速的对这些多边形进行旋转，缩放，转换，倾斜等变换，但由于只是传递元素图像到GPU进行处理，所以它并不能重新渲染内容，图像清晰度不能保证，元素显示清晰度自然就下降了
  - 出现模糊的原因是因为元素的高度、宽度中有奇数， 使用translate(-50%, -50%)之后，相当于宽度、高度除以2的效果，会出现 0.5px。像素就是最小的单位了，要么1，2，3，要么就是0，没有小数
  - 比方说一个Div的高度是100.5px, 在Chrome浏览器在渲染的时候，会渲染成100px、101px、100px、101px、100px .... 100px 和 101px 交替渲染，就出现了模糊
- `pointer-events`
  - sets under what circumstances (if any) a particular graphic element can become the target of pointer events
  - default: `auto'`
  - `none` : The element is never the target of pointer events, pointer event to go "through" the element and target whatever is "underneath" that element instead.
- `z-index`
  - sets the z-order of a positioned element and its descendants or flex items. 设置该属性的元素的定位方式不能是static
  - 可选值包括：auto，0，-N，N
  - 无z-index或者z-index值相等时，堆叠顺序均由元素在文档中的先后位置决定，后出现的会在上面
  - 一般，z-index越大，就在越上层
  - 当向上追溯找不到含有z-index值的父元素的情况下，则可视为**自由的z-index元素**
  - 自由的z-index元素可以与其他自由的定位元素或者父元素的同级兄弟定位元素来比较z-index的值，决定其堆叠顺序
  - 在parent2的z-index大于或者等于parent1的z-index的时候，parent2以及它的子元素均位于parent1以及其子元素的上方
  - z-index值只决定同一父元素中的同级子元素的堆叠顺序，子元素依赖于父元素z-index值来获得页面中的堆叠顺序
  - https://godbasin.github.io/2016/06/25/about-position/
- `will-change`
  - 提供了一种告知浏览器该元素会有哪些变化的方法，这样浏览器可以在元素属性真正发生变化之前提前做好对应的优化准备工作可以将一部分复杂的计算工作提前准备好
- `touch-action`
  - sets how an element's region can be manipulated by a touchscreen user (for example, by zooming features built into the browser)
- position
  - fixed相对浏览器窗口定位，脱离文档流，且不占位
- css样式的渲染由浏览器实现，对开发者来说是黑盒，不用花过多时间
- 当背景图片不够大时，可以考虑使用 background-repeat
- weui的页面层级
  - content：内容层，页面主要内容
  - navi：导航层，用户滑动内容时可保持位置不动，常用语导航栏菜单
  - mask：蒙版层，用于锁定内容层和导航层，不能单独使用，常配合popout
  - popout：弹出层，常用于弹出菜单、通知、状态提示、操作提示
  - 参考 https://weui.io/#layers
- css原来的作用是复用class，现在复用组件就相当于复用了class

# css变量

- 除IE外的浏览器都已支持
  - 变量值只能用作属性值，不能用作属性名

``` css
/* 定义局部变量  */
element {
  --main-bg-color: brown;
}

/* 定义全局变量 */
:root {
  --main-bg-color: brown;
}

/* 使用变量 */
element {
  background-color: var(--main-bg-color);
}
```

# 大型项目参考

- ant-design 
  - 每个组件都有单独样式文件，如alert/index.tsx, alert/style/index.tsx(.less)
  - 支持通过babel插件导入所需组件的css
  - 依赖react, rc-table, rc-tree等组件
  - 测试依赖react-router，react-dnd，react-intl，react-resizable, antd-theme-generator, antd-tools(webpack)
- blueprint
  - 每个组件都有单独样式文件，如alert.tsx, _alert.scss
- grommet
  - 组件大多有单独样式文件，如Button.js, StyleButton.js(只有样式)
  - v2的样式基于styled-components实现
- office-ui-fabric-react
  - 每个组件都有单独的样式文件，如Checkbox.tsx, Checkbox.style.ts
- element-react
  - 每个组件都使用className指定类，样式基于scss
- rsuite
  - 每个组件都有单独的样式文件，如Alert.js, alert.less
  - style作为props传入
- uiw
  - 每个组件都有单独样式文件，如alert/index.tsx, alert/style/index.less
    - 再使用className
- misc
  - material-ui
    - 每个组件都是一个完整的js文件，里面都有一个styles对象
    - 提供单独的 `@material-ui/styles` 样式操作工具包，还提供ThemeProvider
    - 样式使用的是基于css-in-js的jss
  - react-bootstrap
    - 每个组件都使用className指定类，样式由props传入

# faq

- 怎么让触摸设备支持下拉菜单
  - 解决方案是使用Modernizr检测设备是否支持触摸，如果支持再去掉对visibilit 属性的过渡。如果设备支持触摸，Modernizr会给根元素html添加一个touch类，我们就可以针对触摸设备编写规则
- 使用@import指令导入外部样式表和使用link导入样式表性能差距大吗
  - 源码中使用@import指令可以通过css预处理器先处理成一个css，之后只需link一个css
- 是否可以有使用内联样式的伪类？
  - `<a href="http://bd.com" style="hover:text-decoration:none;">b</a>`
  - 不可以
  - 内联样式与规则集中的选择器参与同一级联，并且在级联中采用最高优先级(！重要)。因此，它们甚至优先于伪类状态。允许内嵌样式中的伪类或任何其他选择器可能会引入新的级联级别，并带来新的问题

# BFC(Block formatting contexts)

- `Formatting context` 是CSS2.1规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系、相互作用
  - 最常见的Formatting context有Block fomatting context (简称BFC)和Inline formatting context(简称IFC)
  - CSS2.1中只有BFC和IFC, CSS3中还增加了G(grid)FC和F(flex)FC
  - 在MDN中依然把flexbox跟gridbox算在BFC中，但在最新的规范里，它们已经从BFC中分离了出去，成为独立的一个CSS模块 　　
- `Block fomatting context` = block-level box + Formatting Context
  - BFC直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。 
  - display属性为block, list-item, table的元素，会生成block-level box；并且参与 block fomatting context；
  - display属性为inline, inline-block inline-table的元素，会生成inline-level box。并且参与 inline formatting context；
- BFC是一块渲染区域，那这块渲染区域到底在哪，它又是有多大，这些由生成BFC的元素决定，CSS2.1中规定满足下列CSS声明之一的元素便会生成BFC
  - 根元素
  - float的值不为none
  - overflow的值不为visible
  - display的值为inline-block、table-cell、table-caption
  - position的值为absolute或fixed，此时脱离了文档流
- BFC三特性
  - BFC会阻止垂直外边距（margin-top、margin-bottom）折叠
    - 只有同属于一个BFC时，两个元素才有可能发生垂直Margin的重叠
    - 这个包括相邻元素，嵌套元素，只要他们之间没有阻挡(例如边框，非空内容，padding等)就会发生margin重叠
    - 要解决margin重叠问题，只要让它们不在同一个BFC就行了，但是对于两个相邻元素来说，意义不大，没有必要给它们加个外壳，但是对于嵌套元素来说就很有必要了，只要把父元素设为BFC就可以了。这样子元素的margin就不会和父元素的margin发生重叠了。
  - BFC不会重叠浮动元素
  - BFC可以包含浮动
    - 只要父容器形成BFC就可以包含浮动的子元素
- BFC约束规则
  - 内部的Box会在垂直方向上一个接一个的放置，Block元素会扩展到与父元素同宽
  - 垂直方向上的距离由margin决定。（完整的说法是：属于同一个BFC的两个相邻Box的margin会发生重叠（塌陷），与方向无关。）
  - 每个元素的左外边距与包含块的左边界相接触（从左向右），即使浮动元素也是如此。（这说明BFC中子元素不会超出他的包含块，而position为absolute的元素可以超出他的包含块边界）
  - BFC的区域不会与float的元素区域重叠
  - **计算BFC的高度时，浮动子元素也参与计算**
  - BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然
- 可以给div加个display:inline-block，触每个div容器生成一个BFC
- 若块级正常流元素的高度设置为auto，而且只有块级子元素时，其默认高度将是从最高块级子元素的外边框边界到最低块级子元素外边框边界之间的距离。如果块级元素有上内边距或下内边距，或者有上边框或下边框，其高度是从其最高子元素的上外边距边界到其最低子元素的下外边距边界之间的距离
- BFC的几种方式都有各自的问题，overflow属性会影响滚动条和绝对定位的元素；position会改变元素的定位方式，这是我们不希望的，display这几种方式依然没有解决低版本IE问题
- ref
  - https://github.com/zuopf769/notebook/blob/master/fe/BFC%E5%8E%9F%E7%90%86%E5%89%96%E6%9E%90/README.md
  - https://github.com/zuopf769/notebook/blob/master/fe/%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8%E5%92%8CBFC/README.md

# css style guide  

- https://github.com/airbnb/css
- https://github.com/airbnb/javascript/tree/master/css-in-javascript
- react处理样式的建议 
  - https://reactjs.org/docs/faq-styling.html
  - using the style attribute as the primary means of styling elements is generally not recommended. 
  - In most cases, className should be used to reference classes defined in an external CSS stylesheet. 
  - style is most often used in React applications to add dynamically-computed styles at render time.
- w3c标准相关
  - https://github.com/w3c/webcomponents/blob/gh-pages/proposals/css-modules-v1-explainer.md

# web组件设计

- Ant Design
  - https://ant.design/
- WeUI
  - https://github.com/Tencent/weui
  - 同微信原生视觉体验一致的基础样式库
  - css命名基于BEM

# dev-tips

- 行内元素同样具有盒子模型
  - 行内元素的padding-top/bottom、margin-top/bottom属性设置是无效的
  - 行内元素的padding-left/right、margin-left/right属性设置是有效的
- z-index
  - For a positioned box (that is, one with any position other than static), Overlapping elements with a larger z-index cover those with a smaller one.
  - default value is `auto`
- scss中的class不要通过 `import styles from './index.scss'` 这样的方式引入， `styles.className` 未生效
- css direction: rtl, ltr - 指的是从left到right或相反
- 项目配色板 color palette
  - https://www.canva.com/learn/brand-color-palette
- `display: contents` 能使拥有该属性的元素本身不能生成任何盒模型，但是它的子元素或者伪元素可以正常生成，该元素就好像在Dom树中被子元素与伪元素所替代一样
  - 使div元素不产生任何边框，因此元素的背景、边框和填充部分都不会渲染
  - 但该元素上的其他样式还是能够影响子元素
  - 该元素就会像是不存在一样，它的子元素会替代它在Dom树中的位置
  - 如果想添加一些有语义但又不显示的元素，那么该属性是非常有用的
- 媒体查询是向不同设备提供不同样式的一种方式
  - 媒体类型Media Type是一个常见的属性，在css2中支持的设备类型共10种，常用screen、print、all、tv、tty
  - 媒体特性Media Query是css3对Media Type的增强版、其实可以将Media Query看成Media Type(判断条件) + css (符合条件的样式规则)
  - 媒体特性有时候不止一条，当出现多个条件，就需要通过关键词连接，如and, not, only
  - 断点，就是设备宽度的临界点。在Media Query中，媒体特性 min-width 和 max-width 对应的属性值就是响应式设计中的断点值
  - 参考bulma的breakpoints： https://bulma.io/documentation/overview/responsiveness/
  - 参考媒体查询介绍 
      - http://www.xsuchen.com/detail/css/11 
      - http://www.xsuchen.com/detail/css/9.html
- pseudo elements: 4
  - before, after, first-letter, first-line
  - selector.class:pseudo-element {property:value; }
- pseudo classes: 7
  - a:link, a:visited, a:hover, a:active
  - :focus, :lang
  - ：first-child
- `.styl` 样式文件是stylus扩展css语法的一种格式，stylus is similar to sass/less, except that it's based on nodejs.

# CSS模块化解决方案

## 为什么需要CSS模块化

- 命名冲突，任何一个组件的样式规则，都对整个页面有效
- css和js无法共享变量
- 需要健壮且易于扩展的css
- 参考
  - https://zhuanlan.zhihu.com/p/26878157
  - https://github.com/streamich/freestyler/blob/master/docs/en/generations.md
  - https://medium.com/@piggyslasher/the-state-of-css-css-in-js-how-styled-components-is-solving-the-problems-weve-had-for-decades-d8abbc8bc148

## 使用CSS命名规则进行模块化

- 典型代表
  - BEM： `block__element_modifier`
- 问题
  - 命名较复杂
  - JS和CSS之间依然没有打通变量和选择器等
- 原生css的问题
  - 缺少变量、嵌套支持、样式文件合并 > sass解决

## css-in-js  

- 典型代表
  - https://github.com/styled-components/styled-components
  - radium: A toolchain for React component styling
  - styled-jsx: Inline style system for React and Preact
- 彻底抛弃CSS，用JavaScript写CSS规则
- 优点
  - 使用js强大的功能编写和操作样式，支持单js文件包含组件所有样式和行为，组件独立
  - 样式跟随组件局部化，副作用少，查找快速
  - 尽管js体积增大了一点，但只需下载组件所需的css，且无需单独发送css文件请求
  - 方便根据状态数据动态修改样式和主题
  - js原生提供变量功能
  - css-in-js包含大多数css预处理器的功能
  - 将可修改的样式作为属性暴露给用户，丧失部分灵活性，但可统一样式标准
  - js功能强大，也可以实现类似sass预处理的实用功能
- 缺点
  - 无法提取出单独的css文件？ 有的库可以提取
  - 业务代码与样式代码杂糅
  - js动态解析、生成样式会消耗一定性能
  - 无法使用伪类，媒体查询？？？   2019已支持
  - 不支持web字体
  - 样式代码也会出现大量重复，特别是服务端渲染？？？   但组件复用方便
  - 不能利用成熟的CSS预处理器或后处理器，如Sass/PostCSS？？？  2019已支持
  - 如果全部使用css-in-js那将需要把每个样式都变成props，如果这个组件的dom还有多层级呢？你是无法把所有样式都添加到props中。同时也不能全部设置成变量，那就丧失了单独定制某个组件的能力。css-in-js生成的className通常是不稳定的随机串，这就给外部想灵活覆盖样式增加了困难
  - 当css设置了一半样式，另一半真的需要js动态传入，你不得不css+css-in-js混合使用，项目久了，维护的时候发现某些css-in-js不变了，可以固化在css里，css里固定的值又因为新去求变得可变了，你又得拿出来放在css-in-js里
  - css-in-js方案要考虑ts支持
- 参考
  - https://mxstbr.com/thoughts/css-in-js/ [20190218]
  - https://robinchen.me/tech/2016/08/09/tech-Refactor-CSS-into-JS.html
  - http://blog.vjeux.com/2014/javascript/react-css-in-js-nationjs.html

## 使用JS管理CSS样式模块  

- 典型代表
  - CSS Modules
- 使用JS编译原生的CSS文件，使其具备模块化的能力
- CSS Modules
  - 对class名都做了混淆处理，使用对象来保存原class和混淆后class的对应关系
  - 通过composes复用样式，无需借助sass
  - CSS Modules的命名规范是从BEM扩展而来
      - CSS文件名恰好对应block，只需要再考虑element和modifier
  -  :export关键字可以把CSS中的变量输出到JS中，实现css共享变量到js
  - 一般原则(不强制)
      - 不使用id选择器，只使用class名来定义样式
      - 不层叠多个class，只使用一个class把所有样式定义好
      - 所有样式通过composes组合来实现复用
      - 不嵌套
  - 生成混淆的class名后，可以解决命名冲突，但因为无法预知最终class名，不能通过一般选择器覆盖，可以给组件关键节点加上data-role属性，然后通过属性选择器来覆盖样式
  - css modules很好的避免了多人协同开发CSS的命名冲突问题   
- 优点
  - 最大化地结合现有CSS生态和JS模块化能力，包括sass/less
  - 发布时依旧编译出单独的JS和CSS，它并不依赖于React
  - 所有样式都是默认local的，解决了命名冲突和全局污染问题
  - class名生成规则配置灵活，可以此来压缩class名
  - 只需引用组件的JS就能搞定组件所有的JS和CSS
  - 依然是CSS，只增加了很少的学习成本
  - 现有项目能平滑迁移
      - 可以对一元素应用多个class
      - 只转换class选择器，id选择器、元素选择器、伪类不会被转换
- 缺点
  - 覆盖局部样式较复杂，写到最后可能一直在用 :global
  - 原生css能力有限，大量使用预处理器也增加学习成本
- 参考
  - https://zhuanlan.zhihu.com/p/28675375
  - http://www.alloyteam.com/2017/03/getting-started-with-css-modules-and-react-in-practice/
  - https://github.com/camsong/blog/issues/5
  - https://github.com/css-modules/css-modules/issues/187
  - https://glenmaddern.com/articles/css-modules
    - 作者之一Glen Maddern已转向styled-components

## CSS命名

- BEM
  - 命名规则： `block__element_modifier`
  - block是逻辑和功能独立的组件，block可嵌套，可重复
  - element是块的组成部分，它不能在块之外使用
  - modifier定义块的外观和行为
  - 推荐用双下划线连接 `B__E` ，用单下划线连接 `E_M` 或 `B_M`
  - 推荐描述元素的单词或多个单词使用camelCase
  - 尽量不用元素选择器，虽然每个li都写.menu-item，但能避免影响其他嵌套元素
  - 团队统一最重要
  - 参考
      - https://zhuanlan.zhihu.com/p/26407119
      - https://tech.yandex.com/bem/
      - https://en.bem.info/methodology/quick-start/
  - 优点
      - 无论DOM层级多深，统一扁平化命名B__E_M，解决scss嵌套3层以上变复杂的问题
      - 命名较长，冲突少，选择器查找元素更快
      - 命名长但模块化，可读性好，定位问题快速
  - 缺点
      - 命名长，书写得内容较多
      - class较多不是问题
      - 丑，但可读性好
- SMACSS   
  - Scalable and Modular Architecture for CSS    
  - https://smacss.com/book/  
  - 不同**类别**的组件需要以不同的方式处理
  - 类别
      - base：html默认基本样式 ，如title、a
      - layout：只定义布局，不考虑颜色和排版，如 `l-side`
      - module：可重用的模块，如按钮、list，如 `m-btn`
      - state：用来描述layout或module在特定状态下的外观，如 `is-collapsed`
      - theme：用来描述layout或module在某一主题下的外观
- OOCSS  
  - Object-Oriented CSS   
  - https://github.com/stubbornella/oocss/wiki  
  - 样式是可重用的视觉模式，为常见的视觉模式创建可复用的类
  - 样式与上下文无关
  - 样式与元素标签结构无关
  - 总是使用class来命名对象及其子元素，这样可以在不影响html结构的情况下修改样式
  - 不使用id选择器，ID会扰乱CSS优先度，还不能复用
  - 如leftCol
- AMCSS 
  - 属性模块或者说AM，其核心就是关于定义命名空间用来写样式。 
  - 给一个元素加上属性，再通过属性选择器定位到这个元素，达到避免过多的使用class
- 这些框架的相同之处远胜于其不同之处，可以组合使用最佳的部分
  - 模块化元素
      - module/模块：可复用的组件
      - element/子元素：模块中的小块，不独立使用
      - modifier修饰器：改变模块的视觉外观
  - 模块化类别
      - base
      - layout
      - module
      - state
      - helper：独立于模块，可小范围复用，如.h-uppercase
  - 模块化规则
      - 不要使用ID
      - CSS嵌套不要超过一层
      - 为子元素添加类名
      - 遵循命名约定
      - 为类名添加前缀
- 其他命名方案
  - SUITCSS

## 有缺陷的CSS最佳实践

- 不要使用过多的类？
  - 大多数情况下类选择器的副作用会比id选择器和元素选择器小
  - 如果class过多就该考虑扩大修饰范围，修饰范围过大就会出现重复，此时就该缩小范围
  - 通过控制样式的修饰范围来调整样式数量
- 不要添加无语义的元素？
  - 有时可以作为trick
  - 使用无语义但结构化的div可以统一样式
- 少使用后代选择器？
  - 后代选择器会受html标签结构变化影响，但有时更省事
- 页面要在各种设备上外观一致？
  - 没必要，根据实际用途来增减功能，特别是针对移动端

## React开发中的CSS问题

- 全局命名冲突
  - CSS使用全局选择器机制来设置样式，优点是方便重写样式，缺点是所有的样式都是全局生效，样式可能被错误覆盖
  - Web Components标准中的Shadow DOM能彻底解决这个问题，但它将样式彻底局部化，造成外部无法重写样式，损失了灵活性
  - 多人协作开发命名会混乱
- 依赖管理不彻底
  - 引入一个组件时，应该只引入它所需要的CSS样式
  - Saas/Less很难实现对每个组件都编译出单独的CSS，引入所有模块的CSS又造成浪费
  - JS的模块化已经非常成熟，如果能让JS来管理CSS依赖是很好的解决办法，Webpack的 css-loader提供了这种能力
- 无法共享变量

  -复杂组件要使用JS和CSS来共同处理样式，就会造成有些变量在JS和CSS中冗余，Sass/PostCSS/CSS等都不提供跨JS和CSS共享变量这种能力

- 代码压缩不彻底
  - 由于移动端网络的不确定性，现在对CSS压缩已经到了变态的程度，但对非常长的class名却无能为力
- 总结
  - 上面的问题如果只凭CSS自身是无法解决的，如果是通过JS来管理CSS就很好解决
  - Facebook工程师Vjeux给出的解决方案是完全的 CSS in JS
  - 完全抛弃CSS，在JS中以Object语法来写CSS

## react-css-in-js

- 可以通过在目标元素前后放置占位元素，再通过js操作，实现伪元素的::before, ::after
- w3c标准不支持在行内样式中使用伪类，如:hover, :first-child
- 内联样式中不支持定义keyframe
- css-in-js的使用方式可以分5代，根据是否支持在css模板中使用js变量，如果支持，这些变量的作用范围是否包括模块，包括组件，包括render()方法
- 五代css-in-js
  1. css located in separate .*css files
    - example: css-modules, babel-plugin-css-in-js, css-loader
    - not allowed to write styling in JavaScript and use any of JavaScript variables
    - you have to use CSS pre-processors
  2. css as inline style objects
    - example: radium
    - use inline styles in style property of your React elements
    - very dynamic, because they can use even .render() method scope variables
    - 行内样式不支持伪类，无法最大化利用css功能
  3. write static css templates in js and inject actual CSS into DOM `<style>` tags
    - example: aphrodite, cssx, glamor, styletron
    - the templates are static,defined in module scope, and thus they can't use component props
    - have access only to module scope JavaScript variables, which evaluate only once when the module is imported for the first time
  4. write dynamic css templates in js and emit CSS into DOM `<style>` tags
    - example: styled-components, glamorous
    - have access to component scope variables, such as props and state
    -  templates normally also re-render on every component prop or state change.
  5. dynamic css templates in js
    - example: freestyler, jsxstyle, style-it, superstyle
    - you can use JavaScript variables from component's `.render()` function scope.
