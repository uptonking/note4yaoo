---
title: note-web-dev-solution
tags: [dev, solution, web]
favorited: true
created: '2019-06-09T05:38:07.927Z'
modified: '2020-07-14T10:36:07.346Z'
---

# note-web-dev-solution

## 难点

- tree-shaking
  - 各工具库的编译方式不同，webpack各版本支持程度不同
  - webpack v4不支持，v5支持
    - Tree shaking does not apply to re-exported namespace imports
    - rollup can tree-shake `import * as foo` just like other tools
- component-to-image
- repng

## 前端基础框架开发

- 视图渲染
  - MVC/MVVM
  - VDOM结构
  - DOM更新及操作
  - 生命周期
- 状态管理
  - 拆分合并, 子树更新
- 中间件
- 网络请求
- 路由跳转
- ssr
- 同构
- ui组件库

## 前端框架通用问题

- 解决方案的选择
  - 不要浪费过多时间选择，简单采取面向star的编程，方便搜索文档和开发问题
  - 集中时间和精力解决具体一类问题
- locale: 多语言日期/国际化
  - 解决方案大多与框架相关，如react-intl，要考虑兼容性
- theme: 多主题样式
  - 解决方案大多与框架相关，如styled-components，也可以基于css变量
- css样式及布局
  - css-in-js: styled-coponents, emotion
  - css-modules:with css preprocessor
  - layout:flexbox
- icon
  - font-icon:fork-awesome
  - svg-icon:feather is a collection of SVG files
  - css-icon:icono, cssicon
- animation
  - pure css animation: animate.css
  - js animation: anime.js, react-motion, react-move, react-transition-group
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

## faq

- 弹性布局 vs 响应式布局
  - rem是弹性布局的一种实现方式，弹性布局可以算作响应式布局的一种，但响应式布局不是弹性布局
    - 弹性布局强调等比缩放，100%还原
    - 响应式布局强调不同屏幕要有不同的显示，比如媒体查询
  - 只用css，无需js，就可以实现元素大小随着屏幕宽度的变化而变化
- 如何根据不同的屏幕尺寸去动态设置html的font-size呢
  - 利用css的media query来设置，单位是px
  - 利用js动态计算并修改，可能会有闪烁问题
  - rem布局在加载的时候会出现元素一开始很小，闪烁一下恢复正常大小的问题
      - JS动态计算并修改字体大小和媒体查询，只要选择一套方案就可以了，推荐媒体查询
      - 外部css会阻塞DOM渲染，并不阻塞js解析，外部js既阻塞渲染，也阻塞解析
  - 部分安卓手机或者webview调整了系统默认字体大小
- 如何实现1px
  - 将border设置为1px, 然后将也页面的整体根据页面的dpr缩小相应的倍数，接着将rem补偿相应的倍数，这样页面中只有1px的边框缩小了，而其他内容经过缩小和扩大，还是原来的状态
  - var fontSize = width/10*(window.devicePixelRatio) + 'px'
- rem vs px
  - 结论
      - 考虑3类设备上的展示：手机、平板、pc、横竖屏
      - 考虑系统默认字体、浏览器默认字体
      - 在视觉稿要求固定尺寸的元素上使用px，比如1px线、4px的圆角边框
      - 在字号、（大多数）间距上使用rem
      - 不用em，因为会根据当前元素的字号按比例计算尺寸，若当前元素无字号则查找父元素
      - 推荐：用户业务样式代码以 px 为单位，并且以 iPhone6 屏幕 “物理像素” 宽度 750 为基准 (即普通 “逻辑像素” 值的 2 倍大小)， 使用 postcss-pxtorem 把 px 转成 rem 单位，转换基准为1rem=100px (使用 rem 实现不同设备等比缩放效果)。对于使用 webpack 的项目，在 webpack.config.js 里新增 pxtorem 配置
      - 将html元素的font-size设为62.5%(或10px)是为了方便计算，可以设置为625%
      - 当使用小于12px的字体时，chrome只会渲染12px大小的字
      - 若通过浏览器设置或系统设置或辅助功能设置了大字号，则内容及间隔都会变大，字号变大后，屏幕显示的内容会变少   
      - 类似这样的适配在pad横屏展示超级大，所以还是要根据业务需求设置临界值
      - 如果让html元素的font-size等于屏幕宽度的1/100，那1rem和1x就等价了，此时宽度为100rem
          - 如何让html字体大小一直等于屏幕宽度的百分之一呢？ 可以通过js来设置
          - 注意dom在ready,resize,rotate时更新宽度值
          - 那么如何把设计图中的获取的像素单位的值，转换为已rem为单位的值呢？
              - 375px/100rem = 48px/uNeedrem
      - css3带来了rem的同时，也带来了vw和vh，vw为视口宽度的1/100，vh为视口高度的 1/100
          - vw的兼容性不如rem好，android和ios的支持情况不同
          - 若要限制最大宽度，vw
      - 三方组件库是大家公用的，如果每个组件库的rem拆分不一致就会有很多问题，若一个库100rem就是100vw，有的是20rem是100vw，引入几个三放库中间大小肯定就不兼容了
      - rem基于html的font-size，所有元素都受影响，引入三方库修改成本要尽量低
      - 使用px的组件库，会利用js控制内联style进行适应屏幕
      - ref
        - https://www.zhihu.com/question/309599529
        - https://zhuanlan.zhihu.com/p/30413803
        - https://segmentfault.com/a/1190000014502172
        - https://github.com/ant-design/ant-design-mobile/wiki/HD
  - rem的特点是根据根元素按比例计算尺寸
      - 优点是使用rem时，若修改了根元素的字体大小，就可以自动显示相应的尺寸
      - 实现1px的border不精确，计算时常产生小数
      - 横竖屏切换时，可能需要动态计算并设置根html的大小

 `document.getElementsByTagName("html")[0].style.fontSize = (width)height/7.5 + "px";`
      - 最近在做开发的时候遇到rem的一个大坑，就是如果用户改变了手机的字体大小，而且我们的页面样式的宽用了rem,比如{width:1rem},那么页面的宽就会成倍增长，导致页面乱掉。。。还没找到办法解决，宽度还是先避免使用rem的好。
      - 字体的大小和字体宽度，并不成线性关系，所以字体大小不能使用rem；由于设置了根元素字体的大小，会影响所有没有设置字体大小的元素。可以在body上做字体修正
      - 如果用户在PC端浏览，页面过宽怎么办？一般我们都会设置一个最大宽度，大于这个宽度的话页面居中，两边留白 `body { margin: auto; width: 100rem }`
  - px的特点是固定尺寸
      - 浏览器的pixel是css pixel
      - 当用图片或一些不能缩放的展示时，必须要使用固定的px值，因为缩放可能导致变形
      - px是一直是浏览器厂商以及标准的推荐单位，是未来的主流
  - bootstrap的选择
      - While Bootstrap uses ems or rems for defining most sizes, pxs are used for grid breakpoints and container widths. This is because the viewport width is in pixels and does not change with the font size.
- 骨架屏生成方案
  - https://github.com/Jocs/jocs.github.io/issues/22
- 支持web sockets的tomcat服务器7和8有何区别

## solution-locale

- 需要国际化的组件
  - popover信息提示
  - modal对话框操作提示
  - table选择、过滤、折叠、展开, pagination分页的上一页、下一页
- 流程
  - 先选择语言，然后选择要翻译的组件，再选择要替换的文本
- react-intl
  - https://github.com/formatjs/react-intl
  - 国际化类型：string, number, datetime, (相对时间转换)
- localizify
  - https://github.com/noveogroup-amorgunov/localizify
  - no dependencies
  - imperative api

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
  - ionicons

## solution-animation

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

### modal

- usecase
  - 弹出菜单
  - user guide tour
- modal的位置
  - 一般情况，模态框和遮罩总是作为在body下的第一层子节点出现
  - 因为如果很深层次的子孙组件触发模态框，而使得该组件内的模态框组件层级较深
  - 根据z-index的规则，这样的情况很难完成模态框凌驾于页面整体而出现的，遮罩也无法覆盖整个页面
- 支持同时显示多个modal
  - 类似地图上显示多个poi的overlay信息
  - modal下层无mask
  - modal不重叠，若重叠，则先显示的在下层
- modal的开闭控制，放在props还是state
  - 示例多放在state
  - antd
- modal嵌套后的数据传递
  - 如modal重视form，点击form的field会再弹出modal来选择，点击下层弹层组件，可关闭上一层弹层，点击mask，可关闭所有
  - 弹层组件在react DOM树中的位置跟它们实际的层次以及包含关系是没有必然联系的，如果两个弹层是body下面的两个兄弟节点，但从弹层的使用角度看它们是有层次关系的，并不是并列的
- 弹层的层次关系数据是多叉树的结构
- 关闭modal是否应该移除该modal原本挂载的目标节点呢
  - 此处的目标节点是指 `ReactDOM.unstable_renderSubtreeIntoContainer(this, component, containerNode)` 中的containerNode
  - react-modal(Basic Example)关闭modal后，目标节点保持、不移除
    - 可以在body元素上动态添加和删除弹窗是否打开的属性
  - react-bootstrap中的modal对目标节点，关闭modal后即移除
  - 如果根节点删除，动画不好处理。根节点不删除，还是有动画方面的考虑复用根节点也麻烦
  - 隐藏弹窗时，先执行动画，再unmount弹窗组件
- modal状态恢复
  - 如关闭弹窗查找信息，再恢复弹窗继续填写
- modal变成悬浮按钮fab
  - 显示和隐藏的动画
- ref
  - [有赞：多层嵌套弹层组件](https://juejin.im/post/59a02c38518825244b068486)
    - 嵌套modal的结构
  - [一步一步带你封装基于react的modal组件](https://juejin.im/post/5ba5ab61e51d450e9162c4ae)
    - 进出场动画
  - [React模态框秘密和“轮子”渐进设计](https://zhuanlan.zhihu.com/p/30271961)
    - modal的位置应该放在body下的第一层、传递context到modal
  - [React实现动态调用的弹框组件](https://blog.csdn.net/qq_35757537/article/details/90322144)
    - 直接在组件外调用组件内的自定义方法传入自定义参数，来改变触发组件状态改变的setState
  - http://limoer.cc/2019/12/19/global-component/
    - 在不暴露组件实例对象的前提下，暴露修改组件内部状态的方法， `ReactDOM.render(element, container[, callback])`
    - the preferred solution is to attach a callback ref to the root element.
    - 通过高阶方法，提前在callback ref方法中调用参数方法，并传入可修改state的方法的对象
  - [React造轮系列：对话框组件 - Dialog思路](https://juejin.im/post/5cea293ef265da1bc07e15cc)
    - 通过 `ReactDOM.render` 直接实现 `<button onClick={() => alert('1')}>alert</button>`
    - 在onClick方法内直接关闭modal，通过React.cloneElement传入 `{visible: false}`
    - 还可以在ReactDOM.render完成后，返回一个包含操作modal状态方法的对象
  - [用react做一个跟随组件的 tooltip](https://zhuanlan.zhihu.com/p/143093317)
  - [侧边栏设计](https://zhuanlan.zhihu.com/p/28465951)

### sidebar

- usecase
- 兼容移动浏览器
  - 移动端浏览器，向上滑时会隐藏上面的url地址栏和下面的导航菜单，来增大显示空间
  - When viewing a web page on a smartphone browser, the browser will typically remove the URL and menu bars from the screen when the user scrolls down the page.
  - For some reason react-sidebar breaks this behavior, leaving the browser UI in place even when the page is scrolled.
  - Mobile Chrome's autohide works by listening for scroll events on the body element. 
    - As far as I can see this plugin wraps your whole app in an absolutely positioned div with an `overflow-y: auto`
    - as a result, scroll events never trigger on body and the browser chrome does not get hidden. 
- multi-sidebar: 使用多个sidebar用于导航
  - https://github.com/balloob/react-sidebar/issues/65

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
