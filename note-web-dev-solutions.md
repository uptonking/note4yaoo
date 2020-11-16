---
title: note-web-dev-solutions
tags: [dev, solutions, web]
favorited: true
created: '2019-06-09T05:38:07.927Z'
modified: '2020-11-16T12:40:13.553Z'
---

# note-web-dev-solutions

## 前端框架经典问题

- 解决方案的选择
  - 技术选型时，参考知名项目或大公司项目的选择
    - 不要浪费过多时间选择，可先采取面向star的编程，方便搜索文档和开发问题
  - 集中时间和精力解决具体一类业务问题
- locale: 多语言日期/国际化
  - 解决方案大多与框架相关，如react-intl，要考虑兼容性
- theme: 动态主题
  - 解决方案大多与框架相关，如styled-components，也可以基于css变量
  - 实现theme的方法: css变量、带theme名称的子选择器、react-context consumer
  - 可提供几套预定义的精美主题，手动选择任意颜色做主题不推荐，荣易造成视觉冲突、对比度降低
- css样式及布局
  - 趋势：静态提取、主题切换、无重复原子类、带约束的属性
  - 必备：局部样式、动态样式、主题切换
  - 推荐使用css in js作为预处理器
    - 这样自动生成的类名既可以是单个普通类名，又可以是多个原子类空格拼接而成的类名，更灵活
  - css-in-js: styled-components, emotion
  - css-modules:with css preprocessor
  - layout:flexbox
  - 实现动态样式的方法：css变量层叠、inline、data-属性
  - 大公司开始选择css in js的方法了，但css in js易与框架耦合，不方便切换框架
- icon
  - font-icon:fork-awesome
  - svg-icon:feather is a collection of SVG files
  - css-icon:icono, cssicon
- animation
  - pure css animation: animate.css
  - js animation 
    - 封装css动画
    - 基于flip:react-flip-toolkit
    - 基于physics:react-motion
    - 基于frame和timeline
    - misc: anime.js,react-move
  - svg/canvas/webgl animation
- drag-layout-events
  - react-dnd/draggable
  - react-resizable/re-resizable 
- layer多层内容
  - 基于iframe，三国杀十周年新服游戏的处理方式
  - 基于float
- 其他
  - 静态资源处理
    - webpack-loader
  - 鼠标键盘事件
    - throttle和debounce
    - tooltip提示鼠标处内容信息

## solution-locale

- 需要国际化的组件
  - popover信息提示
  - modal对话框操作提示
  - table选择、过滤、折叠、展开, pagination分页的上一页、下一页
- 流程
  - 先选择语言，然后选择要翻译的组件，再选择要替换的文本
- [react-intl](https://github.com/formatjs/react-intl)
  - 国际化类型：string, number, datetime, (相对时间转换)
- [localizify](https://github.com/noveogroup-amorgunov/localizify)
  - 无依赖，imperative api

## solution-theme

- 与选择的css方案紧密相关
- 传统css/sass/postcss
- css-in-js

## solution-css

- atomic css的方案
  - 原子类优点
    - 需要敲击的样式字符串长度较短
    - 提高代码复用程度，很多前端框架的CSS部分，特别是网格系统，都是原子类的具体应用
    - 解决了程序员最大的难题 - 命名，而且语义还算比较清晰
  - 原子类缺点
    - 调试困难，维护困难，想要临时修改值查看效果，结果所有值都变了，网页可能打乱
    - 打算修改某个元素的样式时，有点崩溃，我究竟要用原子类的方式，还是传统的选择器？不自然
    - 编码时，特别是维护代码时，需要经常查阅原子类名的定义，检查是否篡改
    - 可能出现代码冗余，常用的尺寸都定义了m*和p*等。但实际只会用到其中几个，剩下的都是冗余代码
    - dom元素的类名变得很长
  - 理想的情况是，开发时编译出唯一样式名，方便调试，发布时编译出原子类，追求最小体积与影响

## solution-icon

- svg图标
  - svg渲染的视觉体验更好
  - svg图标单独使用，修改更灵活
  - svg支持的动画效果更好
  - 图标若不使用按需加载体积会过大
- font-icon
  - 生成环境通常用cdn先导入字体，这不利于本地离线项目，字体加载常有延迟或fallback
  - 使用方便，只需图标名称
  - 基于css修改图标样式
  - 图标作为字体渲染，视觉体验有时不佳
- 图标解决方案参考
  - https://speakerdeck.com/ninjanails/death-to-icon-fonts
  - https://github.blog/2016-02-22-delivering-octicons-with-svg/
- 使用图标库
  - feather/react-feather
  - fork-awesome

## solution-animation

- FLIP
- React Transition Group 
  - It is not an animation library like React-Motion, it does not animate styles by itself. 
  - Instead it exposes transition stages, manages classes and group elements and manipulates the DOM in useful ways, making the implementation of actual visual transitions much easier.

## solution-drag-layout-events

### drag

- 拖拽使用场景
  - list手动排序
  - 拖拽card，modal, dialog
- tips
  - 要将pc端的mouse事件转换成移动端的touch事件
  - 在拖拽的研发中，复杂的并不是拖拽的实现，而是节点的位置确定与画布的动态扩展
- 实现方法
  - 基于HTML5的Drag Drop API，如react-dnd
    - SVG不支持HTML5的Darg Drop API
  - 通过mousedown -> mousemove -> mouseup实现拖动，如react-draggable
    - 点击节点时无法触发节点的onClick()，是由于onClick事件可分解为onMouseDown与onMouseUp
    - 节点的onMouseDown事件使节点上方新渲染出一个dragNode，那么onMouseUp事件自然触发在它上面，造成该节点的onClick未能成功触发
      - 给dragNode添加pointer-events: none即可解决
- 参考
  - react-draggable
    - DraggableCore
    - Draggable

### resize

- 缩放使用场景
  - 缩放card、modal
- resize events are only fired on `window` object (i.e. returned by document.defaultView). 
  - 普通DOM元素尺寸变化不会触发resize事件，当调整浏览器窗口的大小时，发生resize事件，div的size发生了变化，但是window的size并没有改变
- Only handlers registered on window object will receive resize events.
  - resize事件只能加在window对象上，并不能监听具体某个DOM元素
- 如何监听某个DOM元素的resize事件？
  - window. MutationObserver
    - 监控到DOM中的改变并且等待一系列改变结束后就会触发回调函数
    - 它与事件的不同之处在于，它在DOM变化时，会记录每一个DOM的变化（为一个MutationRecord对象），但是到DOM变化结束时触发回调
    - DOM变化可能是一系列的（比如元素的宽和高同时改变），那么这一系列的变化就会产生一个队列，这个队列会作为参数传递给回调函数
    - 兼容性好，浏览器几乎都支持
  - ResizeObserver 
    - 允许我们观察DOM元素的盒模型大小（宽度、高度）的变化，并做出相应的响应
    - 兼容性不好，直到Chrome 64才支持，safari不支持
- 还可以通过scroll来监听resize事件，resize和scroll事件经常相关联
- 参考
  - https://zhuanlan.zhihu.com/p/24887312
  - https://juejin.im/post/5c26d01a6fb9a049b07d6ce2
  - react-resizable
    - Resizable
    - ResizableBox

### events

- scroll
  - The scroll event is fired when the document view or an element has been scrolled.
  - 当元素大于其父级元素，且父级元素允许其滚动的时候，该元素可以进行滚动
- debounce 函数去抖 操作结束后等一段时间再执行
  - 目标
    - 持续触发不执行
    - 触发结束一段时间之后再执行
    - 或当数值达到最大值时去抖
  - 方法

``` js
  function debounce(func, delay) {
    let timeout；
    return function() {
      // 如果操作持续触发，那么就清除定时器，定时器的回调就不会执行
      clearTimeout(timeout)；
      timeout = setTimeout(() => {
        func.apply(this, arguments)
      }, delay)；
    }
  }
```

- throttle 函数节流 操作开始后每隔一段时间执行一次
  - 目标
      - 持续触发并不会持续不断地一直执行
      - 等到一定时间再去执行
  - 方法

``` js
  function throttle(func, delay) {
    // 操作监视开关打开
    let run = true；
    return function() {
      // 如果开关关闭了，那就直接不执行下边的代码
      if (!run) {
        return；
      }
      // 若持续触发，run一直是false，就会停在上面的判断
      run = false；
      setTimeout(() => {
        func.apply(this, arguments);
        // 定时器到时间之后，会把开关打开，我们的函数就会被执行
        run = true;
      }, delay)；
    }
  }
```

- 参考
  - https://zhuanlan.zhihu.com/p/72923073
- Some of our requirements have different behavior of scrubs on player timeline
  - when you do touch scrub, the indicator on timeline move, but mouse doesn't
  - when you do mouse hover and keep moving, the indicator move as well

### react-dnd

- 是一组React高阶组件，只需要用对应的API将目标组件进行包裹，即可实现拖动或接受放置
- 基于redux实现
- all the `Backend` do is translate the DOM events into the internal Redux actions that React DnD can process.
  - Backend是实现DnD的方式，默认是用HTML5 DnD API，它不能在触屏环境下工作
- `Item` is a plain JavaScript object describing what’s being dragged.
  - Item是拖拽数据的表现形式，用Object来表示
- `Type` 表示拖/放组件的兼容性，DragSource和DropTarget必须指定 type
  - 只有在type相同的情况下，DragSource才能放到DropTarget中
- `Monitor` 是拖放状态的集合
  - Monitors用来响应拖拽事件，可以用来更新组件的的状态
- `Connector` lets you assign one of the predefined roles (a drag source, a drag preview, or a drop target) to the DOM nodes
  - 底层接触DOM，用来封装你的组件，让组件有拖拽的特性
  - 一般在collect方法中指定，然后注入到组件的props中，最后render方法中包装你自己的组件
  - spec是一个带有特定方法的Object，里面是一些响应拖拽事件的方法
  - collect是一个返回object的函数，返回的object会注入到组件的props中
- `DnD Role` tie the types, the items, the side effects, and the collecting functions together with your components.
- `react-dnd` 定义Context，提供Provider、Container factory等上层API
- `dnd-core` 定义Action、Reducer，连接上下层
- `react-dnd-xxx-backend` 通过Dispatch Action把native DnD状态传递到上层
- 使用流程
  - 把应用的根组件包装在DragDropContext中
  - 把可以拖拽的组件包装在DragSource中，或 把可以接受拖拽的组件包装在DropTarget中
    - 设置 type
    - 设置 spec，让组件可以响应拖拽事件
    - 设置 collect，把拖拽过程中需要信息注入组件的 props
- 参考
  - http://www.ayqy.net/blog/react-dnd/
  - https://scarletsky.github.io/2015/11/17/react-dnd-usage/
  - https://juejin.im/post/5aebbdedf265da0ba469a56f

## solution-layer

- 图层顺序
  - background: 背景层，一般在最底层
    - 不单独实现，可通过动画模拟上层组件边卸载背景层边出现
  - content: 内容层，页面主要内容
  - nav: 导航层，内容层之上，一般是主菜单按钮
    - 长期存在，在用户滑动内容层时可保持位置不动，通常用于承载导航栏等需要固定在页面的元素
  - quickAction: 快捷菜单、快速输入等次级导航面板
    - 可长期存在，也可短期存在，支持连续多个操作，如fab
  - mask: 蒙板层，用于锁定内容层和导航层操作，一般不单独使用，常配合pop层使用
  - pop: 弹出层
    - 用于弹窗、通知、操作菜单、成功或加载中等状态的Toast、表单报错提示等弹出内容
    - 存在时间很短，用完即删
  - ad: 广告层，一般在最上层
  - 考虑：z-index
- 弹出层组件的结构
  - portal将react elements渲染到组件树之外
  - popover提供触发事件管理、弹层定位
- trigger的位置和大小
  - 点击trigger组件时，会触发弹出组件overlay的开关
  - trigger和弹出overlay的大小都会变化，每次dom update后要检测大小，若需要则重新定位 

### 组件分层实现

- 使用场景
  - popover、tooltip、toast
  - modal、dialog
- react-layer-stack
  - api
    - Layer: layer definition and controller
      - props: id, to, use, children()
    - LayerToggle: helper to access layer state, N LToggle > 1 Layer
      - props: for,children()
    - LayerStackMountPoint: a mount point for layer
      - props: id,children()
- bottom-to-up alternative ways
  - redux
  - react-portal
  - react-overlays
