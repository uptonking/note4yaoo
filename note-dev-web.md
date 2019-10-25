---
tags: [dev/web]
title: note-dev-web
created: '2019-06-09T05:38:07.927Z'
modified: '2019-10-14T14:08:32.688Z'
---

# note-dev-web

## 前端框架通用问题
- 解决方案的选择
    - 不要浪费过多时间选择，简单采取面向star的编程，方便搜索文档和开发问题
    - 集中时间和精力解决具体一类问题
- 多语言日期/国际化
    - 解决方案大多与框架相关，如react-intl，要考虑兼容性
- 多主题样式
    - 解决方案大多与框架相关，如styled-components，也可以基于css变量
- css样式及布局
    - css-in-js: styled-coponents, emotion
    - css-modules:with css preprocessor
    - layout:flexbox
- icon
    - font-icon:fork-awesome
    - svg-icon:feather is a collection of SVG files
    - css-icon:icono,cssicon
- animation
    - pure css animation:animate.css
    - js animation:anime.js,react-motion,react-move,react-transition-group
- drag-layout
    - react-dnd/draggable
    - react-resizable/re-resizable 
- layers多层内容
    - 基于iframe，三国杀十周年新服游戏的处理方式
    - 基于float
- 其他
    - 静态资源处理
        - webpack-loader
    - 鼠标键盘事件
        - throttle和debounce
        - tooltip提示鼠标处内容信息

## faq
- 骨架屏生成方案
    - https://github.com/Jocs/jocs.github.io/issues/22
- 支持web sockets的tomcat服务器7和8有何区别

## 多语言
- 需要国际化的组件
    - popover信息提示
    - modal对话框操作提示
    - table选择、过滤、折叠、展开, pagination分页的上一页、下一页
- 流程
    - 先选择语言，再选择组件，再选择要替换的文本
- react-intl
    - https://github.com/formatjs/react-intl
    - 国际化类型：string, number, datetime, (相对时间转换)
- localizify
    - https://github.com/noveogroup-amorgunov/localizify
    - no dependencies
    - imperative api

## 图标
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

## 组件分层方案
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

## animation
- React Transition Group is not an animation library like React-Motion, it does not animate styles by itself. Instead it exposes transition stages, manages classes and group elements and manipulates the DOM in useful ways, making the implementation of actual visual transitions much easier.

## drag-layout
### drag
- 拖拽使用场景
    - list手动排序
    - 拖拽card，modal,dialog
- tips
    - 要将pc端的mouse事件转换成移动端的touch事件
    - 在拖拽的研发中，复杂的并不是拖拽的实现，而是节点的位置确定与画布的动态扩展
- 实现方法
    - 基于HTML5的Drag Drop API，如react-dnd
        - SVG不支持HTML5的Darg Drop API
    - 通过mousedown -> mousemove -> mouseup实现拖动，如react-draggable
        - 点击节点时无法触发节点的onClick()，是由于onClick事件可分解为onMouseDown 与onMouseUp
        - 节点的onMouseDown事件使节点上方新渲染出一个dragNode，那么onMouseUp事件自然触发在它上面，造成该节点的onClick未能成功触发，给dragNode添加pointer-events: none即可解决
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
    - window.MutationObserver
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
    ```
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
    ```
    function throttle(func, delay) {
    // 操作监视开关打开
    let run = true；
    return function () {
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

### html5-drag-drop-api
- HTML drag-and-drop uses `DOM event model` and `drag events` inherited from mouse events.
- ondrag/start/enter/over/exit/leave/end
- ondrop
- Making an element `draggable` requires adding the `draggable` attribute and the `ondragstart` global event handler
- Each drag event has a `dataTransfer` property that holds the event's data. This property (which is a DataTransfer object) also has methods to manage drag data. 
- The `dropEffect` property affects which cursor the browser displays while dragging
- If an element is to become a drop zone or `droppable`, the element must have both `ondragover` and `ondrop` event handler attributes.
- 参考
    - https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API
    - https://developer.mozilla.org/en-US/docs/Web/API/Event
    - https://developer.mozilla.org/en-US/docs/Web/API/DragEvent
    - https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations
### react-dnd
- 是一组React高阶组件，只需要用对应的API将目标组件进行包裹，即可实现拖动或接受放置
- 基于redux实现
- all the `Backend` do is translate the DOM events into the internal Redux actions that React DnD can process.
    - Backend是实现DnD的方式，默认是用HTML5 DnD API，它不能在触屏环境下工作
- `Item` is a plain JavaScript object describing what’s being dragged.
    - Item是拖拽数据的表现形式，用Object来表示
- `Type`表示拖/放组件的兼容性，DragSource和DropTarget必须指定 type
    - 只有在type相同的情况下，DragSource才能放到DropTarget中
- `Monitor`是拖放状态的集合
    - Monitors用来响应拖拽事件，可以用来更新组件的的状态
- `Connector` lets you assign one of the predefined roles (a drag source, a drag preview, or a drop target) to the DOM nodes
    - 底层接触DOM，用来封装你的组件，让组件有拖拽的特性
    - 一般在collect方法中指定，然后注入到组件的props中，最后render方法中包装你自己的组件
    - spec是一个带有特定方法的Object，里面是一些响应拖拽事件的方法
    - collect是一个返回object的函数，返回的object会注入到组件的props中
- `DnD Role`  tie the types, the items, the side effects, and the collecting functions together with your components.
- `react-dnd`定义Context，提供Provider、Container factory等上层API
- `dnd-core`定义Action、Reducer，连接上下层
- `react-dnd-xxx-backend`通过Dispatch Action把native DnD状态传递到上层
- 使用流程
    - 把应用的根组件包装在DragDropContext中
    - 把可以拖拽的组件包装在DragSource中
        - 设置 type
        - 设置 spec，让组件可以响应拖拽事件
        - 设置 collect，把拖拽过程中需要信息注入组件的 props
    - 把可以接受拖拽的组件包装在DropTarget中
        - 设置 type
        - 设置 spec，让组件可以响应拖拽事件
        - 设置 collect，把拖拽过程中需要信息注入组件的 props
- 参考
    - http://www.ayqy.net/blog/react-dnd/
    - https://scarletsky.github.io/2015/11/17/react-dnd-usage/
    - https://juejin.im/post/5aebbdedf265da0ba469a56f




## 前端兼容性处理 caniuse 
- 兼容顺序
    - 3大pc浏览器：chrome、firefox、safari
    - mobile浏览器：3大pc对应的3大移动，Android, UC，Samsung，QQ Browser 


## 前端工程化
- storybook
    - UI component dev & test: React, Vue, Angular, Web Components & more
    - addon
        - Knobs: edit props dynamically using the Storybook UI
- codesandbox
    - Online Code Editor Tailored for Web Application
- eslint/tslint
- jest
- enzyme
- webpack
    - entry
    - output
    - module
        - loader
    - resolve：设置模块如何被解析
        - alias选项设置别名
        - extensions指定解析器接受的扩展名
- npm
    - 前端包管理器 
    - 常用命令
        - `npm config list`：查看npm配置信息
        - `npm ls -g --depth=0`：查看本地全局安装的包
        - `npm i -D webpack --registry=https://registry.npm.taobao.org`
    - npm vs yarn
    - npm包名规范
        - 把包名中的标点符号去掉并与现有的包进行比较，相同则不允许发布
        - 找到一个独一无二包名最简单方法就是使用作用域`@+用户名`，被划了作用域的包默认是私有的，所以要通过`--access=public`让它变为公有的包
- yarn
    - a package manager for your code
    - Running `yarn` with no command will run `yarn install`
    - workspaces
        - 提升依赖下载到根目录，减少重复下载
        - Nested workspaces are not supported at this time.
    - yarn vs lerna
        - lerna管理构建时的相互依赖和发布，yarn专注于依赖下载
        - Yarn’s workspaces are the low-level primitives that tools like Lerna can (and do!) use. 
        - They will never try to support the high-level feature that Lerna offers, but by implementing the core logic of the resolution and linking steps inside Yarn itself we hope to enable new usages and improve performance.
- lerna
    - A tool for managing JavaScript projects with multiple packages
    - 多个package是放在单个仓库里维护还是放在多个仓库里单独维护
        - monorepo：方便相互依赖的项目自动测试，但repo体积较大
        - 多仓库维护：方便多人协作
    - 多仓库包管理常见问题
        - package之间相互依赖，开发人员需要在本地手动执行npm link，维护版本号的更替
        - 每一个package都包含独立的node_modules，而且大部分都包含babel等开发时依赖，安装耗时冗余并且占用过多空间
    - 多个包管理方案
        - lerna
        - yarn workspace
        - npm link
    - lerna使用体验
        - 构建时自动解决packages之间的依赖关系，直接依赖本地项目源码
        - 根据git提交记录，自动生成changelog
        - 发布时一起发布多个包
        - 统一管理依赖版本
    - 包管理常用命令
        - `lerna init`：以所有子包共用版本号的固定模式初始化项目， --independent
        - `lerna bootstrap`：为所有项目安装依赖，类似于npm i/yarn
        - `lerna add pkgA --scope=pkgB`：将A安装到B的字段， --dev，一次只能一包
        - `lerna publish`：先确定哪些包需要publish，--skip-git/npm
            -先设置version，先打tag，再push到github，再上传npm，可通过参数拆分流程
            - `lerna publish from-package --yes --registry http:// `
            - 参考 https://github.com/lerna/lerna/issues/1648
        - `lerna ls`：显示packages下的各个package的version
        - `npm link`：可添加本地正在开发的包作为依赖


## 工程化常用工具
- git
    - 常用命令
    - `git branch branchName`:创建新分支
    - `git checkout branchName startPoint`：切换到新分支
    - `git checkout -b bName` = `g branch bName` + `g checkout bName`
    - `git merge b`：将b分支合并到当前分支
        - 执行merge之后，会产生一个新的commit
        - `git merge master feature`：将master分支合并到feature分支
    - `git rebase`：功能和`git merge`类似，
        - `git checkout feature` + `git rebase master`
        - 将整个feature分支移动到master分支的后面，将master分支上新的提交并过来
        - 不会产生新commit
    - Conventional Commits
        - add human and machine readable meaning to commit messages
        - https://www.conventionalcommits.org
        - fix, feat, chore, docs, style, refactor, perf, test

## 前端高效操作工具包
- date-fns
    - 方便在浏览器和Node中操作时间日期
    - provides the most comprehensive, yet simple and consistent toolset for manipulating JavaScript dates in a browser & Node.js
- react-markdown
    - Renders Markdown as pure React components
- marked
    - A markdown parser built for speed
- raf
    - requestAnimationFrame polyfill for node and the browser
- fast-memoize
    - fastest memoization library in js that supports N arguments
    - memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again
- memoize-one
    - Unlike other memoization libraries, memoize-one only remembers the latest arguments and result
    - memoize-one simply remembers the last arguments, and if the function is next called with the same arguments then it returns the previous result
- classnames
    - js utility for conditionally joining classNames together
- immutable-js
    - v4
        - The Iterable class has been renamed to Collection
        - improve Record impl, Record is no longer an Immutable Collection type
        - Flowtype and TypeScript type definitions have been completely rewritten

## 前端工程测试工具包
- rimraf
    - 作用是以包的形式封装rm -rf命令，用来删除文件和文件夹，不管文件夹是否为空，都可删
    - `rm -rf` for node 
    - 命令也可在windows下使用
- husky
    - 能够防止不规范代码被commit、push、merge等等
    - 在执行`git commit`之前会先执行script字段的precommit指定的命令，如yarn test
    - pre-commit包功能更灵活
- plop
    - 设置好模板内容和生成文件路径后，可在命令行输入参数，自动生成组件到路径位置
- replace-in-file
    - A simple utility to quickly replace text in one or more files or globs
- kkt
    - Create React apps with no build configuration, Cli tool for creating react apps
- tsbb
    - a zero-config CLI that helps you develop, test, and publish modern TypeScript Node.js project.
    - TypeScript + Babel = TSBB
- KaTeX
    - library for TeX math rendering on the web
- tslib
    - tslib将仅用于您的编译目标不支持的功能，以便我们生出的代码更小
- webpack
    - terser-webpack-plugin
        - uses terser to minify your JavaScript

## static-doc-site-generator
- write with markdown and then render to html
- hexo
- jbake(java)
- gatsby
- react-static
- bisheng
    - transform Markdown(and other static files with transformers) into static websites and blogs using React.


## dev-web-latest
- htm
    - Hyperscript Tagged Markup: JSX alternative using standard tagged templates, with compiler support
    - 使用标签模版字符串取代jsx
